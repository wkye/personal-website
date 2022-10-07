---
date: 2022-10-04
draft: false
enableEmoji: true
hasMath: false
notebook: true
slug: "website"
tags: ['engineering', 'jupyter-notebooks']
title: "Make Your Own Website Using Hugo and Netlify"   
---
{{% jupyter_cell_start markdown %}}

<video style="display:block; width:100%; height:auto;" autoplay="" muted="" loop="loop">
    <source src="/videos/personal-website/website.mp4" type="video/mp4">
</video>
    
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

Hugo is built up on Go, making it super fast and responsive. It's abstracted out enough from Go to make it simple for people who don't build websites for a living (like me) but at the same time highly extensible. First install hugo on to your machine:
```
brew install hugo
```
Once you have hugo installed, go to whatever base directory you work out of and run the following:
```
hugo new site personal-website
```
This will create a new folder titled `personal-website` with this directory tree:

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

Within your `pyproject.toml` file, copy the contents of my [pyproject.toml file](https://github.com/wkye/personal-website/blob/main/pyproject.toml). Then run the snippet below and SHAZAAM! This should create a `poetry.lock` file and now your machine should more or less function the same as mine :smiley::

```
poetry install
```

# Getting Started: Netlify

Hugo pairs nicely with Netlify. Hugo is a great service to build your website, but you need Netlify to deploy your app. There is already great documentation on [pairing the two](https://gohugo.io/hosting-and-deployment/hosting-on-netlify/), so I won't go into great detail. Just make sure you create a `netlify.toml` file and you copy and past the contents of my [netlify.toml file](https://github.com/wkye/personal-website/blob/main/netlify.toml).

# Setting up your home page

The first step to building your website is to choose your theme. I went with [hugo-theme-mini](https://github.com/nodejh/hugo-theme-mini) because I felt it was simplistic and met the purposes of my website. Copy the contents of the repo into your `themes` folder (Note, I had to make some small tweaks to my theme, so mine may not exactly match yours)
```
git clone https://github.com/nodejh/hugo-theme-mini themes/hugo-theme-mini/
```

Now that you chose and obtained your theme, update your `theme` variable within you `config.toml` file to reflect the folder that houses your theme. Your config should look something like this

```
baseURL = 'yourwebsitename'
languageCode = 'en-us'
title = 'My New Hugo Site'
theme = 'hugo-theme-mini'
```

Now if you run the following, your website will compile locally and you taken the first step towards building your website :tada:. Just type in the localhost number produced into your browser. In this case `//localhost:52500/`.
```
hugo server
```
{{<figure src="/images/personal_website/hugo_home_screen.png">}}

{{% jupyter_cell_end %}}{{% jupyter_cell_start code %}}


{{% jupyter_input_start %}}

```python

```

{{% jupyter_input_end %}}

{{% jupyter_cell_end %}}