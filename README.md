# Setting Up Github Pages site with Jekyll Tutorial

Jekyll is a static site generator. With Jekyll, you can write your pages in markdown from which it will build your html pages based on the layout settings. For example, if the markdown file you're writing is `project1.markdown`, Jekyll will build the `project1.html` file for you. There's no need to tweak the html, css, or whatever it is for the layout unless you want to do some customization. The Jekyll theme you're using alone already allowed some customization (think of working with Bootstrap) and you can easily change them using the provided field. 

## Live Version

Check the live version of my portfolio [https://azukacchi.github.io/](https://azukacchi.github.io/)

## Assumptions

1. You are already familiar with git
2. You have the project documentation ready in markdown

## Tutorial Links

- [setting up jekyll (Windows)](https://jekyllrb.com/docs/installation/windows/)
- [free jekyll themes](https://jekyllthemes.io/free)
- [github pages official documentation](https://docs.github.com/en/github/working-with-github-pages/creating-a-github-pages-site)
- ["just-the-docs" theme source code](https://github.com/pmarsceill/just-the-docs)
- ["just-the-docs" theme documentation](https://pmarsceill.github.io/just-the-docs/)
- ["just-the-docs" github pages DEMO](https://github.com/pmarsceill/jtd-remote)

Other reading
- [simplest tutorial](https://towardsdatascience.com/9-minutes-to-a-data-science-portfolio-website-80b79ced6c54), but you can't run your site locally

## Steps

### Install Ruby and Jekyll

Follow the instruction from this page [for Windows](https://jekyllrb.com/docs/installation/windows/).

### Prepare Your Project Folder

We will prepare and test out pages *locally* first. These first steps are modified from [this](https://docs.github.com/en/github/working-with-github-pages/creating-a-github-pages-site-with-jekyll).

1. Make the new project folder. Choose any names, e.g. `myblog`, because this won't be the name for your repository, as your default github page is `username.github.io`.
2. Open command prompt and navigate to project folder.
3. Choose the directory where you are going to publish your site.
    - If you choose to publish your site from the root of the repository, `/`, your github pages will appear directly on the root, e.g. `username.github.io`. If you choose this, you don't need to make any new directory
    - If you choose to publish your site from a specific folder of the repository, e.g. `/docs`, your github pages will appear on that page, e.g. `username.github.io/docs`. If you choose this, make a new directory, then navigate to that folder.
        ```
        $ mkdir docs
        # Creates a new folder called docs
        $ cd docs
        ```

4.  Create a new Jekyll site in the current directory
    ```
    jekyll new
    ```
5. Install your theme, e.g. "Just-the-Docs" theme. The default theme for new Jekyll site is "minima".
    ```
    gem install just-the-docs
    ```

    ```
    # add it to your your Jekyll site’s Gemfile
    gem "just-the-docs"
    ```
6. Add Just the Docs theme to your Jekyll site’s `_config.yml`
    ```
    theme: "just-the-docs"
    ```

7. Run your local Jekyll server then open your local site on browser: http://localhost:4000
    ```
    bundle exec jekyll serve
    ```

## Make Changes to Your Pages

In this step, you can try adding some pages, customization, and test them locally. When you're changing the `_config.yml` file, the update will not be applied unless you restart the server and run this line again: `bundle exec jekyll serve`

**Always** check the theme documentation to write your pages and setting them up! When you want to customize your theme CSS, check the theme documentation.

After you've completed setting up your pages and your site is running okay locally, proceed to the next step.

## Push Existing Project to Github 

1. Create a new repository on Github. Type a name for your repository. If you're creating a user site, your repository **must** be named `<yourusername>.github.io`. Do not add any files because we're going to push the files from local.
2. Unless you're already working in the root of your project folder, navigate to the root. Initialize git repository in the current directory (must be the root folder).
    ```
    git init
    ```
3. Edit the Gemfile that Jekyll created.
    
    - Add "#" to the beginning of the line that starts with gem "jekyll" to comment out this line.
    - Add the github-pages gem by editing the line starting with `# gem "github-pages"`. Change this line to:
        ```
        gem "github-pages", "~> GITHUB-PAGES-VERSION", group: :jekyll_plugins
        ```
        Replace GITHUB-PAGES-VERSION with the latest supported version of the github-pages gem. Check the version here: ["Dependency versions"](https://pages.github.com/versions/).
    - Save and close the Gemfile
4. If you're using Jekyll theme other than the [supported themes](https://pages.github.com/themes/), edit your `_config.yml` file. For example, for "Just-the-Docs" theme, change this line: `theme: "just-the-docs` to this:
    ```
    remote_theme: pmarsceill/just-the-docs
    ```
    For another theme, check the theme documentation.
5. From the command line, run `bundle update`
6. Add your GitHub repository as a remote
    ```
    git remote add origin https://github.com/<username>/<username>.github.io.git
    ```
7. Then add, commit, and push your files to the remote
    ```
    git add .
    git commit -m "initial commit"
    git remote -v
    git push origin master
    ```
8. Open your github pages. If there's something wrong, e.g. theme doesn't load, check your email! When there's something wrong, you will get a Page build failure or Page build waning email.

## Use a Customized CSS

If you're using a customized CSS (e.g. changing or adding new styles) and run them locally, you usually edit the theme by editing a scss file in the directory of the theme. For example, for "Just-the-Docs" theme, your custom.scss file is in this directory:
```
C:\Ruby27-x64\lib\ruby\gems\2.7.0\gems\just-the-docs-0.3.3\_sass\custom\custom.scss
```

Check the path to the installed theme directory using this `bundle info --path "THEME-NAME"`

However, when you're running your page on Github Pages, you **must** make the directory and the file yourself in the folder where you will publish your site. The exact directory is different for each theme, e.g. for "Just-the-Docs", the directory for the new file is `_sass/custom/custom.scss`. You should follow your theme documentation when you add the contents of the new file. Example with Minima theme [here](https://docs.github.com/en/github/working-with-github-pages/adding-a-theme-to-your-github-pages-site-using-jekyll#customizing-your-themes-css).