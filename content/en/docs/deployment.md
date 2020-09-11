---
title: Deployment
date: 2017-12-24
type: book
weight: 90
---

Sites built using Academic can be deployed in a large variety of ways due to the static nature of the generated website. The recommended deployment method alongside a few of the other most popular techniques are described below.

If using Netlify, your site will be built automatically, otherwise run the `hugo` command in your terminal to generate your site in the `public/` folder - now it is ready to copy across to your host.

With Academic, you can make a great impression on your visitors with your own [custom domain name]({{< relref "domain.md" >}}).

## Netlify

We recommend deploying your site with Netlify. Netlify is free and provides fast global access, automated deployment when you add or modify content, and one-click HTTPS security. [Check out our guide to deploy with Netlify]({{< relref "install.md#install-with-web-browser" >}}).

## GitHub Pages

Go to [Github](http://www.github.com/) and register for an account if you have not done so already. Github encourage using your real name as your username, and this can help your Github URL (which you will be assigned later) to have a professional appearance.

[Install Git](https://help.github.com/articles/set-up-git/) if it's not already present on your system. You can check by running `git --version` in your Command Prompt/Terminal app.

Once you have created your Github account and setup Git on your computer, we will create two new repositories (often abbreviated as *repos*) on Github with the following names:

- `academic-kickstart` or any other name you like - we will save your **content** to this repo
- `<USERNAME>.github.io` where `<USERNAME>` is your Github username - we will save the **generated website** to this repo

To create the `<USERNAME>.github.io` repository, click the "+" icon in the top right corner and then choose “New Repository”.

To create the `academic-kickstart` repository, [**fork**](https://github.com/sourcethemes/academic-kickstart#fork-destination-box) the *Academic Kickstart* repository and clone your fork with Git (download it to your computer) by replacing `<USERNAME>` in the following command with your Github username:

    git clone https://github.com/<USERNAME>/academic-kickstart.git My_Website
    cd My_Website
    git submodule update --init --recursive

In your `config.toml` file, set `baseurl = "https://<USERNAME>.github.io/"`, where `<USERNAME>` is your Github username. Stop Hugo if it's running and delete the `public` directory if it exists (by typing `rm -r public/`).

Add your *<USERNAME>.github.io* repository into a submodule in a folder named *public*, replacing *<USERNAME>* with your Github username:

    git submodule add -f -b master https://github.com/<USERNAME>/<USERNAME>.github.io.git public

Add everything to your local git repository and push it up to your remote repository on GitHub:

    git add .
    git commit -m "Initial commit"
    git push -u origin master

Whilst running the above commands you may be prompted for your Github username and password.

Next, **regenerate** your website's HTML code by running Hugo and uploading the *public* submodule to GitHub:

    hugo
    cd public
    git add .
    git commit -m "Build website"
    git push origin master
    cd ..

Once Git has finished uploading your site to Github, you can open your new `https://<USERNAME>.github.io` website in your browser, substituting *<USERNAME>* with your Github username.

### Automating deployment

If you are feeling more adventurous, you can consider automating deployment so that when a change, such as a new blog post, is pushed to your `academic-kickstart` repository, your website (`<USERNAME>.github.io` repository) is automatically re-built. Check out the [discussion forum](http://discourse.gohugo.io/) for inspiration!

If you prefer easy automated deployments whenever you make a change to your site, we recommend deploying with Netlify (see above) rather than Github Pages.

## Gitlab pages

[Gitlab](https://www.gitlab.com) pages works similarly to Github pages, but simplifies even more the automatic build process of your website. One key benefit is that it only requires a single repository, which can be private (visitors can not easily see the whole website content).

The process is similar to the one for Github:
1. Create an account on [Gitlab](http://www.gitlab.com/).
2. [Install Git](https://help.github.com/articles/set-up-git/) on your system.
3. Create _one_ repository on Gitlab. Give it a meaningful name, as your website URL will have the following form: `https://<USERNAME>.gitlab.io/<REPOSITORY>`.

On your system, edit the `config.toml` file to set `baseurl = "https://<USERNAME>.github.io/<REPOSITORY>"`, where `<USERNAME>` is your Gitlab username and `<REPOSITORY>` is the name of the repostory. Stop Hugo if it's running and delete the `public` directory if it exists (by typing `rm -r public/`).

Follow the instruction on Gitlab in order to link the existing folder on your system with the Gitlab repository. Add everything and push your initial commit.

Whilst running the above commands you may be prompted for your Gitlab username and password.

### Automating deployment

At this point, only the website content has been published to the Gitlab repository. It has not yet been compiled with Hugo and is not available publicly. The last step is therefore to configure Gitlab to build and publish the website automatically.

To do that, create a file called `.gitlab_ci.yml` in the root of the folder on your computer and add the following content:
```
image:
  name: klakegg/hugo:edge-ext-alpine
  entrypoint: [""]

variables:
  GIT_SUBMODULE_STRATEGY: recursive

test:
  script:
    - hugo
  except:
    - master

pages:
  script:
    - hugo
  artifacts:
    paths:
      - public
  only:
    - master
```

Then commit this file to Gitlab

    git add .
    git commit -m "Configure pipeline"
    git push -u origin master

From now on, each time you commit something to Gitlab, a job will run automatically to recompile your website and publish it to Gitlab pages.

Note that if the repository is private (default), you need to tweak the visibility of the page to allow everyone to see your website. Simply go to your repository on Gitlab > Settings (bottom of the left column) > General > Visibility.

If you prefer easy automated deployments whenever you make a change to your site, we recommend deploying with Netlify (see above) rather than Github Pages.


## Amazon S3

By uploading the contents of your `public` folder to [Amazon S3](https://aws.amazon.com/s3/), your site can be served with dynamic scaling to almost unlimited traffic. This approach has the benefit of being one of the cheapest and most reliable hosting options available as you only pay for what you use.

## Web host via FTP

Use an FTP client to upload the contents of your `public` folder to a web host. This may be especially convenient for academic students and staff who are provided with university web space.
