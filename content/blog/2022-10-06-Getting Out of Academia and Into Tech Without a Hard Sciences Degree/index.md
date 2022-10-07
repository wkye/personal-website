---
date: 2022-10-06
draft: false
enableEmoji: true
hasMath: false
notebook: true
slug: "website"
tags: ['academia', 'social sciences', 'tech', 'industry', 'data science']
title: "Getting Out of Academia and into Tech Without a Hard Sciences Degree"   
---
{{% jupyter_cell_start markdown %}}

More and more people are flocking to the high-paying, flexible, and engaging work that the technology space has to offer. And with some of the highest training from the sharpest minds in their fields, the transition seems almost natural for academics. Almost. Tech is lauded as being a non-credentialed space - it doesn't care about where you went to school or what previous roles you've had. While this is true to an extent, it is more true for some fields than others. Transitioning from a physicist to a machine learning engineer is a story I've heard a million times. But what about someone with a social science Ph.D. or a humanity degree?

I left my Ph.D. program in sociology from the University of Notre Dame in 2017 without even finishing my degree. Today I am working as a data scientist at a tech company. In retrospect, a career much better suited for me personally. I want to use this post as an opportunity to share my thoughts on how my transition went and give a glimpse into a more unusual transition into a tech career.
<!--more-->

# Why I Left Academia

{{<figure src="/images/leaving-academia/Willie-ND-2015.png"
width="600"
caption="I'm still the face of ND sociology (as of Oct 2022)" >}}

I want to say upfront that I loved my time at Notre Dame (Go Irish :football:). I had some of the greatest professors and mentors during my time there. But it just wasn't for me.

The initial draw of why I entered a Ph.D. program, was the research. I had a fascination with why people behaved the way they did, particularly quantitatively. And my time in academia cultivated those skills. Jeffrey Wooldridge's Econometrics book remains the foundation of my statistics and I learned to clean and analyze large datasets (my dissertation idea was around using census data to predict neighborhood gentrification - don't ask me more than that cause I don't remember much more...). But there is SO much more to academia then just research. Between the politics of the department, the constant pressure to come up with something new and innovative (even if you're not interested in it), and the looming fact that there are only a small pool of tenure track jobs available after(if) you graduate, it left me feeling really disillusioned and disenchanted with academia.

I loved research, but surely there must be a way to do it without the pressure of grants, publications, and all the other political bullshit.

# Less of a Transition More of a Free Fall

After deciding to leave my Ph.D. program, I thought to myself "I have Ph.D. training from a prestigious institution like Notre Dame, I should be an attractive candidate in the tech space". And I wasn't completely incorrect.
- I knew how to do robust quantitative research
- I had a strong statistical base, particularly in inference (regressions, significance testing, etc.)
- I knew the basics of coding (initially trained in Stata, but had learned R by the time I left ND)
- To be frank, was a workaholic. Being a graduate student to this day is one of the hardest things I've ever done.

At the same time, I also
- Had a 3 page CV
- Wore a suit to my first interview

You probably get the picture. A Ph.D. prepares you to be highly trained in a very niche field. It does not train you to pass an HR screening or a take home test. That's not to say there aren't skills you learned that are highly extensible to the industry, but it takes some refinement.

This is true of anyone transitioning from academia, but it is doubly true if you have a degree in one of the less common fields (e.g. social sciences, humanities).


{{% jupyter_cell_end %}}{{% jupyter_cell_start code %}}


{{% jupyter_input_start %}}

```python
%config InlineBackend.figure_format = 'retina'
# passing in my secret API credentials from my config
import yaml
with open('config.yaml', 'r') as file:
    keys = yaml.safe_load(file)
```

{{% jupyter_input_end %}}

{{% jupyter_cell_end %}}{{% jupyter_cell_start code %}}


{{% jupyter_input_start %}}

```python
import yaml
from serpapi import GoogleSearch
import pandas as pd
```

{{% jupyter_input_end %}}

{{% jupyter_cell_end %}}{{% jupyter_cell_start code %}}


{{% jupyter_input_start %}}

```python
# utilizing the serpapi package. Eventually, I want to do a more complex
# NLP project here. But for the purposes of this blog, I kept the code
# pretty simple (I did write some functions for that *future* analysis)
from serpapi import GoogleSearch

def query_google_jobs(
    q: pd.StringDtype,
    location: pd.StringDtype,
    api_key: pd.StringDtype,
    engine: pd.StringDtype,
    chips: pd.StringDtype,
    n_search: pd.Int16Dtype
) -> list:  
    
    combined_queries = []
    
    for i in range(0,n_search,10):
        
        print(f'Number or results returned: {i+10}')
        
        jobs_results = GoogleSearch({
            "q":q,
            "location":location,
            "api_key":api_key,
            "engine":engine,
            "chips":chips,
            "start":i
        }).get_dict()
        
        combined_queries = combined_queries + jobs_results['jobs_results']
        
    return combined_queries

combined_queries  = query_google_jobs(q = 'data',
                  location = 'New York, New York',
                  api_key = keys['api_key'],
                  engine = 'google_jobs',
                  chips = 'job_family_1:data scientist',
                  n_search = 100)
```

{{% jupyter_input_end %}}

    Number or results returned: 10
    https://serpapi.com/search
    Number or results returned: 20
    https://serpapi.com/search
    Number or results returned: 30
    https://serpapi.com/search
    Number or results returned: 40
    https://serpapi.com/search
    Number or results returned: 50
    https://serpapi.com/search
    Number or results returned: 60
    https://serpapi.com/search
    Number or results returned: 70
    https://serpapi.com/search
    Number or results returned: 80
    https://serpapi.com/search
    Number or results returned: 90
    https://serpapi.com/search
    Number or results returned: 100
    https://serpapi.com/search


{{% jupyter_cell_end %}}{{% jupyter_cell_start code %}}


{{% jupyter_input_start %}}

```python
import pandas as pd

job_dict_final = {'title':[], 'description':[], 'company_name':[]}

for i in combined_queries:
    
    try:
        job_dict = { your_key: i[your_key] for your_key in ['title','description','company_name']} 
        job_dict_final['title'].append(job_dict['title'])
        job_dict_final['description'].append(job_dict['description'])
        job_dict_final['company_name'].append(job_dict['company_name'])
        
    except:
        pass

jobs_df = pd.DataFrame(job_dict_final)
# did really basic regex cleaning here. Just trying to get a rough estimate
jobs_df['description']  = jobs_df['description'].str.lower()

```

{{% jupyter_input_end %}}

{{% jupyter_cell_end %}}{{% jupyter_cell_start code %}}


{{% jupyter_input_start %}}

```python
# key terms i'm looking up in job descriptions
search_terms = ['computer science','mathematics','engineering',
               'economics','hard science', 'physics','social science','biology','sociology','psychology']

percentage_list = []

for term in search_terms:
    
    percentage = jobs_df['description'].str.contains(term).mean()*100
    percentage_list.append(percentage)

search_percentages_df = pd.DataFrame({'term':search_terms, 'percentage':percentage_list}).sort_values('percentage', ascending=False)
```

{{% jupyter_input_end %}}

{{% jupyter_cell_end %}}{{% jupyter_cell_start code %}}


{{% jupyter_input_start %}}

```python
import plotly.graph_objects as go
data = [go.Bar(x=search_percentages_df['term'],
            y=search_percentages_df['percentage'])]
fig = go.Figure(data = data)
# fig.write_image("images/fig1.png")
```

{{% jupyter_input_end %}}

{{% jupyter_cell_end %}}{{% jupyter_cell_start markdown %}}

{{<figure src="/images/leaving-academia/index_1.png" >}}

{{% jupyter_cell_end %}}{{% jupyter_cell_start code %}}


{{% jupyter_input_start %}}

```python

```

{{% jupyter_input_end %}}

{{% jupyter_cell_end %}}