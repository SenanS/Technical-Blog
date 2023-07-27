---
layout: post
title: How to Make a Technical Blog
subtitle: (with absolutely no Jekyll experience)
---

<aside><p>Over the last 6 years I've added some wonderful code projects to my Github. I wanted to create a blog to showcase some of the writing, documentation and stories behind my code and other passion projects I've been involved in.</p></aside>
Built using [Jekyll](https://jekyllrb.com/docs/front-matter/) & [Hyde](https://hyde.getpoole.com/).


## Initial Setup

1. Fork the [Hyde Repository](https://github.com/poole/hyde) (or my repo).
2. On your new Github Repository: navigate to to *Settings*>*Code and Automation*>*Pages*.
3. Build and deploy a Github Page from the main branch & Save. ![Build-deploy](/public/Tech-Blog=Build-deploy.png){:class="img-responsive"}
4. In the Actions tab of the repo, you can view the status of the deployed page & debug if there are any issues. ![Actions-Deploy](/public/Tech-Blog=Actions-deploy.png){:class="img-responsive"}

## Local Testing

If you want to develop/debug the site locally: 
- Clone your newly created fork to your local machine. 
- Install [Jekyll](https://jekyllrb.com/docs/installation/#guides) for your OS.

To build, host & deploy the site in the local repo directory use: 
~~~ cmd
jekyll serve
~~~
<aside><p>I enjoyed the challenge of making this site, I haven't done webdev since 2016/17. A whole lot has changed. </p></aside>

#### In case that didn't work properly
You may encounter some `_config.yml` errors using:
- `markdown: redcarpet`
	- Change to `markdown: kramdown`
- `highlighter: pygments`
	- Change to `highlighter: Rouge`
- `relative_permalinks: true`
	- Change to `relative_permalinks: false`
- Adding `plugins: [jekyll-paginate]`
- I also experienced issues with the addresses in the `head.html`, with the CSS links!![URLs](/public/Tech-Blog=URLs.png)
	- This was fixed by adding or removing a **/** before `public` in the URL.

#### Customisation
With the local copy working, you can customise the `/_includes`, `/_layouts`, `/_posts`, `_config.yml`, `/public`, `atom.xml`, `404.html`, `about.md` & `index.html` pages, but *not* the `/_site` directory, as this will be overwritten with each build of the Jekyll service.
## Adding Articles

Posts are added within the `_posts` directory, named **specifically** in the `YYYY-MM-DD-title` format.
[Kramdown markdown](https://kramdown.gettalong.org/syntax.html) is used to format the posts.

All written markdown articles should have some variation on the following header, called a [Front Matter](https://jekyllrb.com/docs/front-matter/) in Jekyll:
~~~ markdown
---

layout: post

title: How to Make a Technical Blog

---
~~~
Then start writing your markdown articles and documenting your adventures.
Thanks for joining me 😊