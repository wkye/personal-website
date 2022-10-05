---
date: 2022-10-04
draft: false
enableEmoji: true
hasMath: false
notebook: true
slug: "website"
tags: ['engineering']
title: "Make You Own Website Using Hugo and Netlify"   
---
{{% jupyter_cell_start markdown %}}

{{<figure src="/images/personal_website/making_website_wip2.png">}}

{{% jupyter_cell_end %}}{{% jupyter_cell_start markdown %}}

I have no formal training in computer science and would not consider myself an engineer. I do, however, think of myself as someone who "gets the job done". As I have worked in several startups (each subsequent company tends to get smaller :eyes:), I've picked up a scrappy mindset where I love learning new things. And fortunately, these smaller starts up offer the latitude to fail quickly and learn (more?) quickly!

In this post, I will show you the process of how I learned how to make this website!
<!--more-->

# Online Resources

There were several people who's work I used as a reference to build my own site: 
- [Ethan Rosenthal](https://github.com/EthanRosenthal/website-source): My former MLE lead at Dia&Co! Built a lot of my stuff on top of the code he had already written. Was a huge help in quickly debugging my site.
- [Lugo](https://www.youtube.com/watch?v=ZFL09qhKi5I&t=1092s): My initial testing of Hugo was helped by this tutorial.
- [Design](https://github.com/nodejh/hugo-theme-mini): The design of my website leverages the themes from the hugo-theme-mini repository.

# Getting Started: Hugo

I'm assuming that you have some knowledge of python and git but this is your first foray into hugo and netlify. Let's start with what [Hugo](https://gohugo.io/) is. 

Hugo is built up on Go, making it super fast and responsive. At the same time, it's abstracted out enough from Go to make it simple for people who don't build websites for a living (like me) but at the same time highly extensible. First install hugo on to your machine:
```
brew install hugo
```
Once you have hugo installed, go to whatever base directory you work out of. And run the following:
```
hugo new site personal-website
```
This will create a new folder titled `personal-website` with the following directory tree:

```
personal-website
├── archetypes
│   └── default.md
├── config.toml
├── content
├── data
├── layouts
├── public
├── static
└── themes
```

For the purposes of keeping this tutorial succinct, the main folders you will utilize will be:
- `config.toml` - Basic configuration file. Controls things like what language your site will render in or whether to enable emojis (obviously you should enable, duh :stuck_out_tongue_winking_eye:).
- `content` - The content in markdown form on your website.
- `static` - All of your non-dynamic files (e.g. images, css, etc)
- `themes` - The template for how your site will be displayed. There are a multitude of [themes to choose from on Hugo](https://themes.gohugo.io/)!

# Getting Started: Poetry

Poetry is a package dependency tool. It will allow you to create a virtual environment that mimics the one I am currently in, and thus allows you to reproduce any work that I do! This should install poetry:
```
curl -sSL https://install.python-poetry.org | python3 -
```

Once you've install poetry, intitalize within your `personal-website` folder and it should create a `pyproject.toml`:
```
# all prompts are optional except your name
poetry init
```

Within your `pyproject.toml` file, copy the contents of my [pyproject.toml file](https://github.com/wkye/personal-website/blob/main/pyproject.toml). Then run snippet below and shazaam! This should create a `poetry.lock` file and now your machine should more or less function the same as mine :smiley::

```
poetry install
```

{{% jupyter_cell_end %}}{{% jupyter_cell_start code %}}


{{% jupyter_input_start %}}

```python

```

{{% jupyter_input_end %}}

{{% jupyter_cell_end %}}