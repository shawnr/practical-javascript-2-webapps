# Building and Deploying the App

Now that we have our application configured for proper building, we can actually execute the commands to make the build happen, and then to deploy the application. 

## Build the Code
In order to process our code and build the site, execute the build command:

```bash
npm run build
```

Since we made the changes to redirect output of the build process to the `docs/` directory, we should see that directory was created. If we look inside it, we should see something like this:

![Directory listing of docs/](/img/docs-listing.png)
<br>Directory listing of `docs/`

Our files have been properly combined, processed, and built into a static website. We are now ready to deploy the site.

## Deploy the Site

Since we are using the Github Pages feature of our repository, all we need to do is commit our code and push it to Github. This might require us to make a new repository on Github and follow those directions to connect everything. Once we push the code with the site built out in the `docs/` directory, Github Pages will automatically pick that up and deploy it to the static website servers. If we look at the Settings page for our project repository we can see the URL where our site is deployed.

When we want to deploy the code we just built, we can run the following commands:

`git add docs`

Then:

`git commit -m "Built new version of site."`

Finally:

`git push origin`

## Commit Code Without Deploying the Site

It's often necessary to work on a feature for awhile before we want to deploy the new code. In these cases, we need to be able to commit our code and push it to Github for review/collaboration without deploying the site. 

Remember that the only way to update the site code is to run the `npm run build` command. If we do work elsewhere in the app, but we do NOT run the build command, then we can safely commit and push our code to Github without changing the site that is deployed to the public.

### Pro Tip: Advertise Your Link

![Github Description Link](/img/github-description-link.png)
<br>Github Description Link

When we have a repository on Github, we can add a link that will show at the top of the repo homepage. This is very handy for putting the link to the deployed version of our code. Adding a link here also helps our repositories work better as portfolio pieces when we're looking for jobs.










