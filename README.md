DevTeam Wiki
A single-page developer team wiki built with Hugo and the Geekdoc theme.

Setup
Clone this repository
Install Hugo (https://gohugo.io/installation/)
Run hugo server to preview the site locally
Adding Content
All content is in a single file: content/_index.md. Edit this file to update the wiki.

Deployment
The site automatically deploys to GitHub Pages when changes are pushed to the master branch.

GitHub Pages Setup
After the first successful GitHub Action run:

Go to your repository's Settings
Navigate to Pages in the sidebar
Under "Build and deployment", select "Deploy from a branch"
Select the gh-pages branch and root (/) folder
Click Save
Your site will be available at https://yourusername.github.io/my-team-wiki/