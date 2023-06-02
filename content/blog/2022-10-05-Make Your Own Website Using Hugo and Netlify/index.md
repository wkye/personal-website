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

# Table of Contents

- <a href="#introduction">Introduction</a><br>
- <a href="#online_resources">Online Resources</a><br>
- <a href="#getting_started_hugo">Hugo</a><br>
- <a href="#getting_started_poetry">Poetry</a><br>
- <a href="#getting_started_netlify">Netlify</a><br>
- <a href="#homepage">Setting up your home page</a><br>
- <a href="#customize_homepage">Customizing your home page</a><br>
- <a href="#about_me">Adding an About Me Page</a><br>
- <a href="#posts">Creating Posts</a><br>
- <a href="#advanced">Advanced Customizations</a><br>
- <a href="#summary">Summary</a><br>

{{% jupyter_cell_end %}}{{% jupyter_cell_start markdown %}}

<p><a name="introduction"></a></p>

# Introduction
    
I have no formal training in computer science and would not consider myself an engineer. I do, however, think of myself as someone who "gets the job done". As I have worked in several startups (each subsequent company tends to get smaller :eyes:), I've picked up a scrappy mindset where I love learning new things. And fortunately, these smaller starts up offer the latitude to fail quickly and learn (more?) quickly!

In this post, I will show you the process of how I learned how to make this website!
<!--more-->

{{% jupyter_cell_end %}}{{% jupyter_cell_start markdown %}}

<p><a name="online_resources"></a></p>

# Online Resources

There were several people who's work I used as a reference to build my own site: 
- [Ethan Rosenthal](https://github.com/EthanRosenthal/website-source): My former MLE lead at Dia&Co! Built a lot of my stuff on top of the code he had already written. Was a huge help in quickly debugging my site.
- [Lugo](https://www.youtube.com/watch?v=ZFL09qhKi5I&t=1092s): My initial testing of Hugo was helped by this tutorial.
- [Design](https://github.com/nodejh/hugo-theme-mini): The design of my website leverages the themes from the hugo-theme-mini repository.

{{% jupyter_cell_end %}}{{% jupyter_cell_start markdown %}}

<p><a name="getting_started_hugo"></a></p>

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
- `static` - All of your non-dynamic files (e.g. images, css, etc).
- `themes` - The template for how your site will be displayed. There are a multitude of [themes to choose from on Hugo](https://themes.gohugo.io/)!

{{% jupyter_cell_end %}}{{% jupyter_cell_start markdown %}}

<p><a name="getting_started_poetry"></a></p>

# Getting Started: Poetry

Poetry is a package dependency tool. It will allow you to create a virtual environment that mimics the one I am currently in, and thus will enable you to reproduce any work that I do!

Once you've installed poetry, initialize poetry within your `personal-website` folder and it should create a `pyproject.toml` Within your `pyproject.toml` file, copy the contents of my [pyproject.toml file](https://github.com/wkye/personal-website/blob/main/pyproject.toml). Then run `poetry install` and SHAZAAM! This should create a `poetry.lock` file and now your machine should more or less function the same as mine :smiley::
```
# install poetry
curl -sSL https://install.python-poetry.org | python3 -
# initialize poetry within your project
poetry init
# After copying my poetry.lock file, this should install all my packages onto your machine
poetry install
```


{{% jupyter_cell_end %}}{{% jupyter_cell_start markdown %}}

<p><a name="getting_started_netlify"></a></p>

# Getting Started: Netlify

Hugo pairs nicely with Netlify. Hugo is a great service to build your website, but you need Netlify to deploy your app. There is already great documentation on [pairing the two](https://gohugo.io/hosting-and-deployment/hosting-on-netlify/), so I won't go into great detail. Create an account on netlify and connect it to your GitHub repo. Make sure you create a `netlify.toml` file and copy and paste the contents of my [netlify.toml file](https://github.com/wkye/personal-website/blob/main/netlify.toml).

{{% jupyter_cell_end %}}{{% jupyter_cell_start markdown %}}

<p><a name="homepage"></a></p>

# Setting up your home page

The first step to building your website is to choose your theme. I went with [hugo-theme-mini](https://github.com/nodejh/hugo-theme-mini) because I felt it was simplistic and met the purposes of my website. Copy the contents of the repo into your `themes` folder (Note, I had to make some small tweaks to my theme, so mine may not exactly match yours)
```
git clone https://github.com/nodejh/hugo-theme-mini themes/hugo-theme-mini/
```

Now that you chose and obtained your theme, update your `theme` variable within your` config.toml` file to reflect the folder that houses your theme. Your config should look something like this

```
baseURL = 'yourwebsitename'
languageCode = 'en-us'
title = 'My New Hugo Site'
theme = 'hugo-theme-mini'
```

Now if you run `hugo server`, your website will compile locally and you have taken the first step towards building your website :tada:. Just type in the localhost number produced into your browser. In this case `//localhost:52500/`.
```
hugo server
```
{{<figure src="/images/personal-website/hugo_home_screen.png">}}


{{% jupyter_cell_end %}}{{% jupyter_cell_start markdown %}}

<p><a name="customize_homepage"></a></p>

# Customizing your home page

You're now building your website from scratch, so the customizations are endless. But for the purposes of this tutorial, we're gonna stick closely to the template and just make some basic changes.
    
Let's start with the fundamentals of how pages are constructed. Within the `layouts` directory are HTML templates; each file determines how aspects of your page will look. The HTML code that produces the title and summary for your homepage is in [layouts/index.html](https://github.com/nodejh/hugo-theme-mini/blob/master/layouts/index.html#L8).
    
The parameters `Title` and `Params.Bio` are the variables that the HTML file is using to build your site.
```
<h1>{{ .Site.Title }}</h1>

{{ with .Site.Params.Bio }}
  <h2>{{ . | markdownify }}</h2>
{{ end }}
```
We can change the title and bio of your website by updating the variable in `config.toml` file. It should look something like this:
```
baseURL = 'yourwebsitename'
languageCode = 'en-us'
title = 'MY AWESOME NEW WEBSITE'
theme = 'hugo-theme-mini'

[params]
  bio = 'Data is fun'

```

The code that produces the image on your home page is also in [layouts/partials/profile.html](https://github.com/wkye/personal-website/blob/main/themes/hugo-theme-mini/layouts/partials/profile.html#L10)"
```
<header class="profile">
    {{ if .Site.Params.avatarLink }}
        <a href="{{ .Site.Params.avatarLink }}">
          <img class="avatar" alt="avatar" src="{{ "/images/avatar.png" | relURL }}" />
```
The static directory is where you store the images you want to you. This particular code is looking for a file name `avatar.png` within the directory `static/images/`. So let's initialize this folder structure then download this [sample image from my github](https://raw.githubusercontent.com/wkye/personal-website/main/static/images/personal-website/sample_avatar.png) and copy it to your new `/static/images/` directory.    
```
# make a new images directory under static
mkdir static/images/
# copy downloaded file to new images directory and change name to avatar.png
cp sample_avatar.png static/images/avatar.png
```

{{<figure src="/images/personal-website/sample_website_updated_avatar.png"
          width="600"
          caption="tip: use option + ⌘ + J to use developer tools to debug your code quicker">}}


{{% jupyter_cell_end %}}{{% jupyter_cell_start markdown %}}

<p><a name="about_me"></a></p>

# Adding an About Me Page

Next, I want to add an about page. To do so, we need to leverage the `content` folder. In Hugo, content is where you put your markdown files, which are the pages of your website. Hugo will generate an HTML file and create a new web directory.

In [layouts/partials/navigation.html](https://github.com/wkye/personal-website/blob/main/themes/hugo-theme-mini/layouts/partials/navigation.html#L7) is where we see the `about` tag referenced in the navigation
            
```
<a href="{{ "/about" | relURL }}">{{ with .Site.Params.about }}{{ . }}{{ else }}{{ i18n "about" }}{{ end }}</a>
```
          
Create a `_index.md` file under the `subdirectory /content/about` then open the file
```
mkdir content/about && touch content/about/_index.md
vim content/about/_index.md
```
This `/about/_index.md`\` page will represent what you will see under your about page. Let's add some content

```
---
title = "About"
description = "Description about file"
date = "2022-10-11"
author = "Your Name"
---

The picture in the avatar is from the Hayao Miyazaki musuem in LA. Highly recommend!
```
            
{{<figure src="/images/personal-website/about-me-example.png"
          width="600">}}

{{% jupyter_cell_end %}}{{% jupyter_cell_start markdown %}}

<p><a name="posts"></a></p>

# Creating Posts

To create posts, initialize as `md` file in `content/posts`. All new `md` files will show up as new posts. So for example, let's create a post named `markdown-syntax.md` where we go overview how to write markdown files.
            
```
# Create a new directory with a markdown-syntax file
mkdir content/posts && touch content/posts/markdown-syntax.md
# Update the contents of the file
vim content/about/markdown-syntax.md
```

In `markdown-syntax.md` input the following
            
``` 
---
author = "Your Name"
title = "Markdown Syntax Guide"
date = "2022-10-11"
description = "Sample article showcasing basic Markdown syntax and formatting for HTML" 
---

This article offers a sample of basic Markdown syntax that can be used in Hugo content files, also it shows whether basic HTML elements are decorated with CSS in a Hugo theme.
<!--more-->

## Headings

The following HTML `<h1>`—`<h6>` elements represent six levels of section headings. `<h1>` is the highest section level while `<h6>` is the lowest.

# H1
## H2
### H3
#### H4
##### H5
###### H6            
```
Again, everything between the three dashes is metadata. And the content above `<!--more-->` is what will show up as a precursor for the blog post and everything below that will be the actual content seen when opening up the blog. 
{{<figure src="/images/personal-website/post-example.png"width="600">}}    

{{% jupyter_cell_end %}}{{% jupyter_cell_start markdown %}}

<p><a name="advanced"></a></p>

# Advanced Customizations
            
The out-of-the-box template for hugo-theme-mini offers the bulk of what you need for a blog-based website. But let's say you want to add some of your professional handles (like Linkedin or Github) to the top of your page. In [layouts/partials/profile.html](https://github.com/wkye/personal-website/blob/main/layouts/partials/profile.html#L14) you can add HTML code for these handles:
            
```
<h1>{{ .Site.Title }}</h1>

<nav class="social-heading">
  {{ if .Site.Params.linkedin }}
    <a target="_blank" href="{{ .Site.Params.linkedin }}">LinkedIn</a>
  {{ end}}
  {{ if .Site.Params.github }}
    <a target="_blank" href="{{ .Site.Params.github }}">| GitHub</a>
  {{ end}}
  {{ if .Site.Params.twitter }}
    <a target="_blank" href="{{ .Site.Params.twitter }}">| Twitter</a>
  {{ end}}
</nav>            
```  

This is one example of many different customizations you can add to your website as you become more proficient in HTML.

{{% jupyter_cell_end %}}{{% jupyter_cell_start markdown %}}

<p><a name="summary"></a></p>
           
# Summary
            
Creating a tutorial on how to create a website was harder than I thought :sweat_smile:. I see why there aren't many resources out there.
            
But as always, if you have any questions, feedback, or just want to connect, don't hesitate to reach out!

{{% jupyter_cell_end %}}