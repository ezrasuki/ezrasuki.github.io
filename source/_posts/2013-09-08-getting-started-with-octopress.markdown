---
layout: post
title: "Getting started with Octopress"
date: 2013-09-08 06:28
comments: true
categories: [learn, octopress]
---

![](/images/octopress.jpg)

#A. Setting up
## 1. Clone Octopress to local machine
Clone the original octopress repo with the name I want for my blog. Running this will create an "ezrasuki.github.io" folder.
    git clone git://github.com/imathis/octopress.git ezrasuki.github.io

## 2. Install Octopress
    bundle install
    rake install

## 3. Configure Octopress
Open `_config.yml` and edit some attributes I want to change.

    url: ezrasuki.github.io
    title: .ezra.suki.
    subtitle: Adventure of Ezrasuki
    author: Ezrasuki
    simple_search: http://google.com/search
    description:

#B. Writing a post locally
From the blog root directory (In my case, the ezrasuki.github.io folder I created by cloning), run this task:
    rake new_post["Hello World"]
It will create a .markdown file under `source/_posts`, with a name that looks like: `2013-09-07-hello-world.markdown`. Open and edit so it looks something like this:

    ---
    layout: post
    title: "Hello World"
    date: 2013-09-07 23:18
    comments: true
    categories: [Test, Helloworld]
    ---

    This is the content. You can write in markdown.

Note that "categories" are basically tags.

#C. Preview blog
When done, generate HTML from the markdown with:
    rake generate

To preview the post locally, run the following command, which will start a http://localhost:4000 server you can visit.
    rake preview

#C. Deploy to Github
There are many options for hosting, but I am hosting it on Github because it's free.
##1. Create a Github repo
Create a repo with the name of your blog. It should look like this: `[your github username].github.io`. Mine is `ezrasuki.github.io`
##2. Connect Octopress with the Github repo
Octopress has a rake command which automatically takes care of all this. Run:
    rake setup_github_pages
It will ask you the github repo url. Copy the clone URL from the Github repo and paste it here. It should look something like `https://github.com/ezrasuki/ezrasuki.github.io.git`.
##3. Deploy
### A. Deploy generated blog files
Finally, deploy all the local changes (including the new post) to Github pages repo by running:
    rake deploy

### B. Deploy source files
This only deploys the master branch, which contains the generated blog content. You may also want to push the source branch. The source branch contains everything except for the generated blog files. This includes:
1. Octopress source code
2. Markdown files for posts

Therefore it is a good idea to commit these too, in order to keep track of this side as well. Run the following:
    git commit -am "Committing source"
    git push origin source

Note that `git push origin master` has been already executed automatically when we ran `rake deploy` earlier. Again, that was for pushing the final static content. And this time, `git push origin source` is for pushing the source files.
