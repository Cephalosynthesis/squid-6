# Setup 

## Installing Jekyll

Local setup of Jekyll isn't strictly necessary as changes can be made from the git repo itself. Commits will trigger a rebuild of the site via Github Actions. However, if any substantial changes are to be made being able to preview locally is very useful.

Installation guides for various OS's can be found on [Jekyll's installation page](https://jekyllrb.com/docs/installation/). 

## Setting up the repository locally 

1. Clone the repo.
2. Inside of the repo call:
`bundle install`
To install the necessary Ruby Gems (packages).
3. Proceed to Building & Serving the Site Locally section.

## Building and Serving the Site Locally

In order to build and serve the site locally call this command:

``` shell
bundle exec jekyll --baseurl ""
```

>[!Important]
> The additional `--baseurl ""` flag _is necessary_ for the site to build locally. This differs from what you will see on the Jekyll Quickstart page because the baseurl set in `_config` is what is needed for hosting on GithubPages. This breaks what is required locally and thus needs to be overridden. If you forget this you will hit the 404 page.

This should launch the site on local host - visit: `127.0.0.1:4000` in your web browser of choice. If there are any build errors they should appear in the terminal.

