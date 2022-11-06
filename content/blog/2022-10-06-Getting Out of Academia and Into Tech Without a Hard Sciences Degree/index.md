---
date: 2022-10-06
draft: false
enableEmoji: true
hasMath: false
notebook: true
slug: "leaving-academia"
tags: ['academia', 'social sciences', 'tech', 'industry', 'data science']
title: "Getting Out of Academia and into Tech Without a Hard Sciences Degree"   
---
{{% jupyter_cell_start markdown %}}

More and more people are flocking to the high-paying, flexible, and engaging work that the technology space has to offer. And with some of the highest training from the sharpest minds in their fields, the transition seems almost natural for academics. Almost. Tech is lauded as being a non-credentialed space - it doesn't care about where you went to school or what previous roles you've had. While this is true to an extent, it is more true for some fields than others. Transitioning from a physicist to a machine learning engineer is a story I've heard a million times. But what about someone with a social science Ph.D. or a humanity degree?

I left my Ph.D. program in sociology from the University of Notre Dame in 2017 without even finishing my degree. Today I am working as a data scientist at a tech company - in retrospect, a career much better suited for me personally. I want to use this post as an opportunity to share my thoughts on how my transition went and give a glimpse into a more unusual transition into a tech career.
<!--more-->

# Why I Left Academia

{{<figure src="/images/leaving-academia/Willie-ND-2015.png"
width="600"
caption="I'm still the face of ND sociology (as of Oct 2022)" >}}

I want to say upfront that I loved my time at Notre Dame (Go Irish :football:). I had some of the greatest professors and mentors. But it just wasn't for me.
    
The initial draw of why I entered a Ph.D. program, was the research. I was fascinated with why people behaved the way they did, particularly from a quantitative lense. And my time in academia cultivated those skills. [Jeffrey Wooldridge's Econometrics textbook]((https://www.amazon.com/Introductory-Econometrics-Modern-Approach-Economics/dp/1111531048)) remains the foundation of my statistics. And my thesis was my first real exposure to collecting, cleaning, and analyzing large datasets (my dissertation proposal was around using census data to predict neighborhood gentrification - don't ask me more than that cause I don't remember much more...). But there is SO much more to academia than just research. Between the politics of the department, the constant pressure to come up with something new and innovative (even if you're not interested in it), and the looming fact that there is only a tiny pool of tenure-track jobs available after (if) you graduate, it left me feeling disillusioned and disenchanted with academia.
    
I loved research, but surely there must be a way to do it without the pressure of grants, publications, and all the other political bullshit.

# Less of a Transition More of a Free Fall
    
After mulling it over, I decided to leave my Ph.D. program. I thought to myself "I have Ph.D. training from a prestigious institution like Notre Dame, I should be an attractive candidate in the tech space". And I wasn't completely incorrect.
- I knew how to do robust quantitative research.
- I had a strong statistical base, particularly in inference (regressions, significance testing, etc.).
- I knew the basics of coding (initially trained in Stata, but had learned R by the time I left ND).
- To be frank, was a workaholic. Being a graduate student to this day is one of the hardest things I've ever done.

At the same time, I also
- Had a 3-page CV.
- Wore a suit to my first interview.

You get the picture, a Ph.D. prepares you to be highly trained in a very niche field. It does not train you to pass an HR screening or a take-home test. That's not to say there aren't skills you learned that aren't highly extensible to the industry, but it takes some refinement.
This is true of anyone transitioning from academia, but it is doubly true if you have a degree in one of the less common fields (e.g. social sciences, humanities).
    
Below is a script I wrote to query the Google Careers Search API for data science job titles and descriptions (I hid the code in custom functions in my [custom_function.py](https://github.com/wkye/leaving-academia-for-tech/blob/main/custom_functions.py) to keep the blog more readible). I use this data to see how often different educational fields comes up as a search term in data science job postings.

{{% jupyter_cell_end %}}{{% jupyter_cell_start code %}}


{{% jupyter_input_start %}}

```python
import yaml
import pprint
import pandas as pd
from serpapi import GoogleSearch
# https://github.com/wkye/leaving-academia-for-tech/blob/main/custom_functions.py
import custom_functions

with open('config.yaml', 'r') as file: keys = yaml.safe_load(file)
# query google 
combined_queries = custom_functions.query_google_jobs(q = 'data', 
                                                      location = 'New York, New York', 
                                                      api_key = keys['api_key'], 
                                                      engine = 'google_jobs',
                                                      chips = 'job_family_1:data scientist',
                                                      n_search = 100)
# clean results for querying google
jobs_df = custom_functions.clean_google_jobs_query(combined_queries)
```

{{% jupyter_input_end %}}

    https://serpapi.com/search
    https://serpapi.com/search
    https://serpapi.com/search
    https://serpapi.com/search
    https://serpapi.com/search
    https://serpapi.com/search
    https://serpapi.com/search
    https://serpapi.com/search
    https://serpapi.com/search
    https://serpapi.com/search


{{% jupyter_cell_end %}}{{% jupyter_cell_start markdown %}}

Here is what a sample data science job description looks like in the data:

{{% jupyter_cell_end %}}{{% jupyter_cell_start code %}}


{{% jupyter_input_start %}}

```python
pprint.pprint(jobs_df.iloc[0][['title','company_name']])
pprint.pprint(combined_queries[0]['description'][0:500])
```

{{% jupyter_input_end %}}

    title           Data Scientist II
    company_name               Radian
    Name: 0, dtype: object
    ('See yourself at Radian? We see you here too.\n'
     '\n'
     'At Radian, we see you. For the person you are and the potential you hold. '
     'That’s why we’ve embraced a new way of working that lets our people across '
     'the country be themselves, be their best and be their boldest. Because when '
     'each of us is truly seen, each of us gives our best – and at Radian, we’ll '
     'give you our best right back...\n'
     '\n'
     'See Yourself as a Data Scientist II\n'
     '\n'
     "The Data Scientist II's primary function is estimating, validating, "
     'monitoring and i')


{{% jupyter_cell_end %}}{{% jupyter_cell_start markdown %}}

You can see here that something like **mathematics or economics appears in data science job postings nearly 30%** of the time. In contrast, **sociology only appeared in 1% of data science job descriptions**... :cry:

This is a simple, yet powerful, example of how coming out of academia with a non-computer or hard science training drastically shapes how the job market views you.

{{% jupyter_cell_end %}}{{% jupyter_cell_start code %}}


{{% jupyter_input_start %}}

```python
# create figure to illustrate how frequently different education fields come up in data science job postings
search_terms = ['computer science','mathematics','engineering','economics','hard science', 'physics','social science','biology','sociology','psychology']
custom_functions.create_job_search_word_figure(jobs_df, search_terms, display_figure = False)
```

{{% jupyter_input_end %}}

{{% jupyter_cell_end %}}{{% jupyter_cell_start markdown %}}

{{<figure src="/images/leaving-academia/fig1.png" >}}

{{% jupyter_cell_end %}}{{% jupyter_cell_start markdown %}}

# Data Science Bootcamps:  Pros and Cons


I knew I wanted to get into data science, but I had no idea how. After showing up to an interview in a full on suit (that I also wore at my brothers wedding... cause I was a poor ex-grad student), I realized I needed to re-evaluate my options and I ended up attending 12 week data science bootcamp.

My overall takeaway from attending a bootcamp was that it **helped me my get my foot in the tech industry but it certaintly wasn't worth the hefty price tag** Anyone's experience attending a bootcamp will be highly contingent on what type of background and skillset they are alreading coming in with. But the reality of a data science bootcamp is that you can't learn machine learning or statistical inference in 12 weeks. It should be more viewed as an surface level overview of what exist out there. 

For me, the biggest benefits of attending a bootcamp were more exterior facing. Learning how to craft a resume, knowing what buzzwords to say in an HR screening, finding out that no one cares about where you've had publications, etc. There are plenty of resources out there for you to learn this on your own without having to commit thousands of dollars. I'll link several concepts and resources that I think someone can learn on there own.
 
##### RESUME

There are countless [free data science resumes out](https://towardsdatascience.com/how-to-build-a-solid-data-science-and-tech-resume-e899daceb271) there if you search hard enough. A [resume is not a CV](https://www.chronicle.com/article/from-cv-to-ra-suma/)., so keep it one page. Happy to share mine as well if you'd like, just reach out!

##### LINKEDIN

[Connect with me on LinkedIn](https://www.linkedin.com/) for an example of profile crafting! Networking is a necessary evil in life.

##### STATISTICS

Your approach to learning statistics will be highly variable on what level of statistics you already know. I found the following resources to be helpful:
- [Introductory Econometrics Modern Approach](https://www.amazon.com/Introductory-Econometrics-Modern-Approach-Economics/dp/1111531048): If you have a more traditional training and a strong base, then this book might be helpful. Heavy on theory without going to heavy into the raw math.
- [Introductory_Statistics_with_R](https://www.google.com/books/edition/Introductory_Statistics_with_R/YI0kT8cuiVUC?hl=en&gbpv=1&printsec=frontcover&bsq=Introductory%20Statistics%20with%20R%20(Statistics%20and%20Computing)): Really good beginners course on machine learning. Code is in R, but concepts are still helpful
- [Khan Academy](https://www.khanacademy.org/math/probability): Probability and basic statistics will more likely than not be part of your interview process. Good to brush up here.
- [Coursera Machine Learning](https://www.coursera.org/learn/machine-learning): Highly regarded Andrew Ng machine learning course. Definetely recommend.

##### SQL

SQL is an essential skill for anyone who wants to work in data, but it can be hard to learn because its a little bit of a chicken and an egg problem. Typically you need database access to practice SQL queries and you need to know SQL to get a role that has access to a database. That being said there are still plenty of resources out there to learn the core concepts of [SQL](https://www.w3schools.com/sql/)

##### PYTHON

I strongly recommend [learning python](https://developers.google.com/edu/python/?hl=en) over R. All my blog posts are written and entirely reproducable in Python. Python can be intimidating because there of varying level of expertise, but I would say to start, focus on learning Pandas and just basic python functions (like imports and functions). Stay away from object oriented programming and more advanced things. Its just overkill for what a beginner should know. I always found looking at example Python project to be helpful. Check out my [GitHub page](https://github.com/wkye).

##### GITHUB

Basic git hygene is good to know. Depending on whether you want to lean more analyst versus data engineering will influence to what extent you need to learn git

Data science is a fun field _because_ there is so much to learn. So don't be intimated, keep learning little by little!

# Learning to walk before you can run

{{<figure src="/images/leaving-academia/willie_today_show.png"
width="600"
caption="Me on the Today Show while at Dia. Mama we made it!" >}}
    
After much toiling, I landed my first tech job as a statistical analyst at [Dia&Co](https://www.dia.com/). You may think you need to know how to be a data scientist or analyst __before__ you land your first job (and maybe __you__ do), but for me that wasn't the case. At Dia, I was on a growth focused team that comprised of machine learning engineers, other analysts, a product manager and product designers. I learned that everything in product is somehow related to a funnel, you always lead with the summary (and definetly not the methodology), most people don't care about what statistical assumptions your model took into consideration, and that you don't email code to be reviewed, you tag your reviewer on PR. (:sweat_smile: real story).
    
I was lucky enough to have wonderful leads that took the time to mentor me and show me how to do things (rather than just do it themselves). I never wrote any production level ML code or some fancy Python package, but I was able to see the behind the scene process of how recommendation systems were build and data systms were architectured. I highly recommend that type of experience.
    
At this point, I had drunk the metaphorical kool-aid and wanted to get deeper into tech. Instead of getting my feet wet, I jumped in head first. I landed a remote job as a data analyst at [CircleCI](https://circleci.com/), one of the leading companies in CI/CD. If you don't know what CI/CD is, join my parents, who still think CircleCI is a gas station company. But going from a data team of 30 to a data team of 5, I was now able to build pipelines and tools from scatch. There was surely a lot of long nights and painful failures, but the saying holds true: Fail quickly and learn quicker.
    
Today, I'm at [clockwise](https://www.getclockwise.com/), an AI driven calendar manegment tool. I, literally, was the 2nd data hire on the team and have really been building everything from scratch. Somedays I'm on the finance team building models to forecast revenue, others I'm on the growth team identifying leaks in our monetization funnel. I'm a data engineer debugging why our fivetran to snowflake integration is down, and I'm also a software engineer finding front-end events to optimize our onboarding experience. The hats are many, and the snacks I get sent are even more plentiful (still fully remote at this point).
    
My time in tech has felt like non-stop learning. And in truth, sometimes I feel like I learn something then immediately it becomes antiquated. But I think that is the exciting part of entering the tech data world. If you have an apetite for learning, the as long as you know the right area to focus there are plenty of opportunties out there for you.

# Takeaway
    
Breaking the number 1 rule I've learned in industry, I'm putting my summary at the bottom. But the takeaway is that breaking into tech from academia is no easy thing. Particularly if you're coming from a non hard sciences background like me. At the same time, no matter what field you are coming from, if you have a sense of curiosity and a desire to learn, then I believe the core values to succeed are there. Its just a matter of learning where to focus your attention.
    
I hope that this post gave you a some sort of sense of orientation for how to navigate the tech data space. Leaving academia for tech was not an easy journey, but one I did not regret. No matter what choice you make, good luck on your journey and if there's anyway I can be of help, don't hesitate to reach out! 

{{% jupyter_cell_end %}}{{% jupyter_cell_start code %}}


{{% jupyter_input_start %}}

```python

```

{{% jupyter_input_end %}}

{{% jupyter_cell_end %}}