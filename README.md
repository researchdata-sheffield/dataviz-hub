This repository holds the source for the University of Sheffield's data visualisation hub. The site is generated from the files here using the [Nikola](http://getnikola.com) static site generator.

To contribute, raise an issue on GitHub or make a pull request that adds or modifies files in the `pages` directory. You will probably want to install Nikola so that you can test your contribution before submitting it.

If you are comfortable using the commandline and have a working installation of Python 3 and `pip`, here are some quick-start instructions:

1. Install [Pipenv][]: `pip install pipenv`
    - [Detailed installation instructions for Pipenv][Pipenv install]
2. Create a virtualenv and install dependencies in one step: `pipenv install --dev`
3. Start a local web server to preview the site: `pipenv run nikola auto`
4. Visit <http://localhost:8000> in your browser

There are also some [full installation instructions for Nikola][Nikola install].

[Pipenv]: https://docs.pipenv.org/
[Pipenv install]: https://docs.pipenv.org/#install-pipenv-today
[Nikola install]: https://getnikola.com/getting-started.html
