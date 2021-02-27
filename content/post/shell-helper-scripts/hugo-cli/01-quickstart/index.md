---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Gohugo Quickstart"
subtitle: "Create a Hugo site using the beautiful Ananke theme."
summary: "Install Hugo, Create a new site, Add a theme, Add content, Start the Hugo Server, Site configuration, & Build static pages."
authors: ["Jack Banaszak"]
tags: ["hugo-docs", "hugo-cli"]
categories: ["shell-scripts"]
date: 2021-02-26
lastmod: 2021-02-26T19:55:30-05:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

Install the `hugo` command line client if you have not already. 

```bash
# Using Homebrew on MacOS: Catalina
brew install hugo
```

__A New Static-Site__  

Here we create and configure a new static-site on our local machine which is connected to our remote github server. 

```bash 
### Working In -->  $HOME/sites ###

# Create the Site 
hugo new site <my-site>

# Initialize the site as a git repo
cd <my-site> && git init

# Add a Theme: https://themes.gohugo.io/
git submodule add https://github.com/<account>/<theme-name>.git ./themes/<theme-name>
```
__Note__: `./themes` is the default folder to look for themes.  

Basic configuration to tell hugo to use the theme you've added as a submodule. Themes are read relative to the `themes/` folder.

```bash
# If you configure with "toml"
echo 'theme = "<theme-name>"' >> ./config.toml

# If you configure with "yaml"
echo 'theme: <theme-name>' >> ./config.yml
```

__Add content to your site!__ --> Note: _Added Content is read relative to the `./content/` folder. The generall add content command!

```bash 
# Adds to: --> content/<CATEGORY>/<FILE>.<FORMAT>
hugo new <category>/<file-name>.<format>
```

Basic Method:

```bash
# Adds to content/post/basic-post.md
hugo new post/basic-post.md
```

Best Practice Method:

```bash
# Always use index.md
hugo new post/best-practice-post/index.md
```
__Content Metadata__: Create content metadata in markdown files using yaml front-matter! Include the yaml between `---` at the start of the `.md` file.

```md
---
<!-- YAML Front Matter Here -->
---
```

```yaml
# Example Front Matter in --> content/post/basic-post.md
title: "My Basic Post"
date:  2021-02-12
draft: true
```

__The Hugo Server__: Start the hugo server in the home directory of the static site on your local machine! 

```bash 
# Render content with `draft: true` in the yaml front matter
hugo server -D 
# Or without it
hugo server

### Command Line Response ###
#> Start building sites … 
#> 
#>                    | EN  
#> -------------------+-----
#>   Pages            | 54  
#>   Paginator pages  |  0  
#>   Non-page files   |  7  
#>   Static files     |  1  
#>   Processed images | 31  
#>   Aliases          | 12  
#>   Sitemaps         |  1  
#>   Cleaned          |  0  
#> 
#> Built in 519 ms
#> 
#> Watching for changes in ~/sites/<my-site>/{assets,content,data,static}
#> 
#> Watching for config changes in 
#>    ~/sites/<my-site>/config.toml
#>    ~/sites/<my-site>/config/_default
#>    ~/sites/<my-site>/go.mod
#> 
#> Environment: "development"
#> Serving pages from memory
#> 
#> Running in Fast Render Mode. For full rebuilds on change:
#> hugo server --disableFastRender
#> 
#> Web Server is available at http://localhost:1313/ 
#>     (bind address 127.0.0.1)
#> Press Ctrl+C to stop
```

__Basic Site Configuration__: `./config.<toml|yml>`  

```toml
baseURL = "https://<domain>.<tld>/"
languageCode = "en-us"
title = "My Quickstart Site"
theme = "<theme>"
```

> __Tip__: _Make the changes to the site configuration or any other file in your site while the Hugo server is running, and you will see the changes in the browser right away, though you may need to clear your cache._

__Build The Static Site__:  

To build the site to the default output directory (`public/`) just call `hugo` or `hugo -D` to include drafted content!

```bash
# Override configured output directory
hugo --destination ./site-no-drafts
hugo -d ./site-with-drafts
```

Note: _The `-d` flag short option for `--destination` output dir_

> Tip: _Reconfigure the default output directory in the_ `config.<toml|yml>` file.

```toml
publishdir = "<site-folder>"
```












