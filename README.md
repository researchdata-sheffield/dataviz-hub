# shef datavis
## data visualisation hub

[![Build Status](https://travis-ci.org/researchdata-sheffield/dataviz-hub.svg?branch=develop)](https://travis-ci.org/researchdata-sheffield/dataviz-hub)

<br>

## installation

This repository holds the source for the University of Sheffield's data visualisation hub. The site is generated from the files here using the [Nikola](http://getnikola.com) static site generator.

To contribute, raise an issue on GitHub or make a pull request that adds or modifies files in the `pages` directory. You will probably want to install Nikola so that you can test your contribution before submitting it.

If you are comfortable using the command-line and have a working installation of Python 3 and `pip`, here are some quick-start instructions:

1. Install [Pipenv][]: `pip install pipenv`
    - [Detailed installation instructions for Pipenv][Pipenv install]
2. Create a virtualenv and install dependencies in one step: `pipenv install --dev`
3. Start a local web server to preview the site: `pipenv run nikola auto`
4. Visit <http://localhost:8000> in your browser

There are also some [full installation instructions for Nikola][Nikola install].

[Pipenv]: https://docs.pipenv.org/
[Pipenv install]: https://docs.pipenv.org/#install-pipenv-today
[Nikola install]: https://getnikola.com/getting-started.html


## Create a page

Have a look at the contributing page for general guidance

Install Nikola

**Fork this repo, clone it to your machine and enter the directory.**

*<-- insert any branch specific insturctions here -->*

Create a file in the **`pages/`** directory. It will need to start with a header like this: 

```
<!--
.. title: Accelerated versions of R for Iceberg
.. author: Mike Croucher # optional
.. slug: intel-R-iceberg # optional
.. date: 2016-09-12 00:31:35 UTC # optional
.. tags: # optional
.. category: # optional
-->
```

The `slug` refers to the end of the URL and it will need to be unique.


### Adding a new page:
#### New markdown
- (on github) create new page by clicking `create new file` in **`pages/`** dir.
#### New rmarkdown
- if `.rmd`, create in **`rmd/`** and render to the  **`pages/`** dir.
#### New jupyter notebook
- if an `.ipnb` in the  **`pages/`** dir.
  - create new `.ipnb`
  - in the `.ipnb`, go to **`edit`**,  then **`edit notebook metadata`** and add the following snippet to the top level of the **notebook metadata.json**
    ```
    "nikola": {
        "title": "Visualising Networks",
        "slug": "visualising-networks",
        "date": "2012-09-15 19:52:05 UTC"
    }
    ```

## Create a new blog post.

### Create a new `rst` blog post 

```bash
nikola new_post
``` 


## Create a new blog post.

### Create a new `rst` blog post 

```bash
nikola new_post -f markdown
``` 


***

## Testing the build

You can build and test your post on your own machine using:

```bash
cd site
nikola build
```

If the build is OK, you can look at it on your browser with 

```bash
nikola serve --browser
```

As an alternative to repeatedly running `nikola build` every time you make a change you can run:

```bash
nikola auto
```

to detect changes, automatically rebuild your site and refresh your browser.

When you are happy, submit a Pull Request.

## For site admins

To publish a post, accept the PR then from the `site` directory you can run a single command to:

* commit a rendered version of the site to the `master` branch then 
* push this to the `origin` (_not_ `upstream`) branch on GitHub

this command being:

```bash
nikola github_deploy
```


