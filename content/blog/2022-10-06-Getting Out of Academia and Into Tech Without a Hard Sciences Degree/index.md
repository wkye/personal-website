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

I left my Ph.D. program in sociology at the University of Notre Dame in 2017 without finishing my Doctorate. Today I am working as a data scientist at a tech company - in retrospect, a career much better suited for me personally. I want to use this post as an opportunity to share my thoughts on how my transition went and give a glimpse into a more unusual path into a tech career.

<!--more-->

# Why I Left Academia

{{<figure src="/images/leaving-academia/Willie-ND-2015.png"
width="600"
caption="I'm still the face of ND sociology (as of Oct 2022)" >}}

The initial draw of why I entered a Ph.D. program was the research. I was fascinated with why people behaved the way they did, particularly from a quantitative lens. And my time in academia cultivated those skills. [Jeffrey Wooldridge's Econometrics textbook]((https://www.amazon.com/Introductory-Econometrics-Modern-Approach-Economics/dp/1111531048)) remains the foundation of my statistics and my research was my first real exposure to collecting, cleaning, and analyzing large datasets (my dissertation proposal was around using census data to predict neighborhood gentrification - don't ask me more than that cause I don't remember much more...). But there is SO much more to academia than just research. Between the politics of the department, the constant pressure to come up with something new and innovative (even if you're not interested in it), and the looming fact that there is only a tiny pool of tenure-track jobs available after you graduate, it left me feeling disillusioned and disenchanted with academia.

I loved research, but surely there must be a way to do it without the pressure of grants, publications, and all the other political bullshit.

# Transitioning to Tech

After mulling it over, I decided to leave my Ph.D. program. I thought to myself "I have advanced training| from a prestigious institution like Notre Dame, I should be an attractive candidate in the tech space". And I wasn't completely wrong.
- I knew how to do robust quantitative research.
- I had a strong statistical base, particularly in inference (regressions, significance testing, etc.).
- I knew the basics of coding (initially trained in Stata, but had learned R by the time I left ND).
- To be frank, was a workaholic. Being a graduate student to this day is one of the hardest things I've ever done.

At the same time, I also had a 3 page CV instead of a resume.

You get the picture, a Ph.D. prepares you to be highly trained in a very niche field. It does not train you to pass an HR screening or a take-home test. That's not to say there aren't skills you learned that can't be highly extensible to the industry, but it takes some refinement.
This is true of anyone transitioning from academia, but it is doubly true if you have a degree in one of the less common fields (e.g. social sciences, humanities).

# How Common is "Sociology" in Job Postings vs. "Mathematics" and Other Hard Science Degree   

Do people even hire sociologists? I built [a tool to query the google jobs posting page](https://github.com/wkye/leaving-academia-for-tech) to see how often the word "sociology" comes up in job postings.

**Out of 100 jobs, Sociology comes up 2% of the time while in contrast math comes up 54% of the time**. This is a simple, yet powerful, example of how coming out of academia with a non-hard sciences training drastically shapes how the job market views you.

{{% jupyter_cell_end %}}{{% jupyter_cell_start code %}}


{{% jupyter_input_start %}}

```python
import pandas as pd
from src.resources import resource
```

{{% jupyter_input_end %}}

{{% jupyter_cell_end %}}{{% jupyter_cell_start code %}}


{{% jupyter_input_start %}}

```python
google_jobs = resource('google')
df = google_jobs.query(q='data scientist',
                       location='New York, New York',
                       n_search=100
                       # ,serp_api_key = <your key>
)
```

{{% jupyter_input_end %}}

    2022-11-21 09:08:49.062 | INFO     | src.resources:query:74 - Query data retrieved in 1.1 seconds.
    Retrieved dataframe with 100 rows, consuming 0.0 MB.


{{% jupyter_cell_end %}}{{% jupyter_cell_start markdown %}}

{{% jupyter_cell_end %}}{{% jupyter_cell_start code %}}


{{% jupyter_input_start %}}

```python
#Data Cleaning
df["description"] = df["description"].str.lower()
df["description"] = df["description"].replace(r"\n", " ", regex=True)
key_terms = [ "sociology","social science","physic","computer science","math","engineering"]
for key_term in key_terms:
    df[key_term] = df["description"].str.contains(key_term)
```

{{% jupyter_input_end %}}

{{% jupyter_cell_end %}}{{% jupyter_cell_start code %}}


{{% jupyter_input_start %}}

```python
print('PERCENTAGE OF TIMES KEY WORDS COME UP IN JOB DESCRIPTIONS')
(df[key_terms].mean() * 100).sort_values()
```

{{% jupyter_input_end %}}

    PERCENTAGE OF TIMES KEY WORDS COME UP IN JOB DESCRIPTIONS





    sociology            2.0
    social science       2.0
    physic              24.0
    computer science    53.0
    math                54.0
    engineering         56.0
    dtype: float64



{{% jupyter_cell_end %}}{{% jupyter_cell_start markdown %}}

# Data Science Bootcamps:  Pros and Cons


I knew I wanted to get into data science, but I had no idea how. I realized I needed to re-evaluate my options and I ended up attending a 12-week data science boot camp.

My overall takeaway from attending a boot camp was that **it helped me get my foot in the tech industry but it certainly wasn’t worth the hefty price tag**. Anyone’s experience attending a boot camp will be highly contingent on what type of background and skillset they are already coming in with. But the reality of a data science boot camp is that you can’t learn machine learning or statistical inference in 12 weeks.

For me, the biggest benefits of attending a boot camp were more exterior facing. Like learning how to craft a resume, and knowing what buzzwords to say in an HR screening. There are plenty of resources out there for you to learn this on your own without having to commit thousands of dollars. I’ll link several concepts and resources that I think someone can learn on their own.

**RESUME**: There are countless [free data science resumes](https://towardsdatascience.com/how-to-build-a-solid-data-science-and-tech-resume-e899daceb271) out there if you search hard enough. A [resume is not a CV](https://www.chronicle.com/article/from-cv-to-ra-suma/), so keep it to one-page. Happy to share mine as well if you'd like, just reach out!

**LINKEDIN**: [Connect with me on LinkedIn](https://www.linkedin.com/) for an example of profile crafting! Networking is a necessary evil in life.

**STATISTICS**: Your approach to learning statistics will be highly variable on what level of statistics you already know. I found the following resources to be helpful:
- [Introductory Econometrics Modern Approach](https://hastie.su.domains/ISLR2/ISLRv2_website.pdf): If you have more traditional training and a strong base, then this book might be helpful. Good overview of theory without going too heavy into the raw math.
- [An Introduction to Statistical Learning with Applications in R](https://www.google.com/books/edition/Introductory_Statistics_with_R/YI0kT8cuiVUC?hl=en&gbpv=1&printsec=frontcover&bsq=Introductory%20Statistics%20with%20R%20(Statistics%20and%20Computing)): Really good beginner's course on machine learning. The code is in R, but concepts are still helpful.
- [Khan Academy](https://www.khanacademy.org/math/probability): Probability and basic statistics will more likely than not be part of your interview process. Good to brush up here.
- [Coursera Machine Learning](https://www.coursera.org/learn/machine-learning): Highly regarded Andrew Ng machine learning course. Definitely recommend.

**SQL**: SQL is an essential skill for anyone who wants to work in data, but it can be hard to learn because it's a little bit of a chicken and an egg problem. Typically you need database access to practice SQL queries and you need to know SQL to get a role that has access to a database. That being said there are still plenty of resources to learn the core concepts of [SQL](https://www.w3schools.com/sql/).

**PYTHON**: I strongly recommend [learning python](https://developers.google.com/edu/python/?hl=en) over R. All my blog posts are written and entirely reproducible in Python. Python can be intimidating because there of varying levels of expertise, but I would say to start, focus on learning Pandas and just basic python functions. Stay away from object-oriented programming and more advanced things. It's overkill for what a beginner should know. I always found looking at example Python projects to be helpful. Check out my [GitHub page](https://github.com/wkye).

**GITHUB**: Basic git hygiene is good to know. Depending on whether you want to learn more analyst skills versus data engineering skills will influence to what extent you need to learn git.

Data science is a fun field _because_ there is so much to learn. So don't be intimated, keep learning little by little!

# Learning to walk before you can run

{{<figure src="/images/leaving-academia/willie_today_show.png"
width="600"
caption="Me on the Today Show" >}}

After much toiling, I landed my first tech job as a statistical analyst at [Dia&Co](https://www.dia.com/). I was lucky enough to have wonderful leads that took the time to mentor me and show me how to do things (rather than just do it themselves). I never wrote any production-level ML code or some fancy Python package, but I was able to see the behind the scene process of how recommendation systems were built and data systems were architectured. I highly recommend that type of experience.

Following my time at Dia&Co, I landed a remote job as a data analyst at CircleCI, one of the leading companies in CI/CD. Going from a data team of 30 to a data team of 5, I was now able to build pipelines and tools from scratch. There were surely a lot of long nights and painful failures, but the saying holds: _Fail quickly and learn quicker._

Today, I’m at clockwise, an AI-driven calendar management tool. I, literally, was the 2nd data hire on the team and have been building everything from scratch. Somedays I’m on the finance team building models to forecast revenue, others I’m on the growth team identifying leaks in our monetization funnel. I’m a data engineer debugging why our Fivetran to snowflake integration is down, and I’m also a software engineer finding front-end events to optimize our onboarding experience.

My time in tech has felt like non-stop learning. And in truth, sometimes I feel like I learn something then immediately it becomes antiquated. But I think that is the exciting part of entering the tech data world. If you have an appetite for learning, then as long as you know the right area to focus on, there are plenty of opportunities out there for you.

# Takeaway

Breaking the number 1 rule I've learned in industry, I'm putting my summary at the bottom. But the takeaway is that breaking into tech from academia is no easy thing. Particularly if you're coming from a non-hard sciences background like me. At the same time, no matter what field you are coming from, if you have a sense of curiosity and a desire to learn, then I believe the core values to succeed are there. It's just a matter of learning where to focus your attention.

I hope that this post gave you some sort of sense of orientation on how to navigate the tech data space. Leaving academia for tech was not an easy journey, but one I do not regret. No matter what choice you make, good luck on your journey and if there's any way I can be of help, don't hesitate to reach out!

{{% jupyter_cell_end %}}{{% jupyter_cell_start code %}}


{{% jupyter_input_start %}}

```python

```

{{% jupyter_input_end %}}

{{% jupyter_cell_end %}}
