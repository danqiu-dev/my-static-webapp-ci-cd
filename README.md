# Static Web App CI/CD Project/Lab/Practice

## Background (condensed and does not mirror the actual environment)

At work, a client's dashboard was hosted on Azure Static Web Apps, with its
source code stored in a GitHub repository. When an update was merged into
`main`, it did not appear on the live site. 

## Goal

To understand and practice the correct setup, this project recreates the same
scenario from scratch:

1. Create a simple static web app (plain HTML) and store the code in `main`
   on GitHub.
2. Create a Static Web App resource in Azure and deploy it from the GitHub
   repository.
3. Make a code update, merge it into `main`.
4. Set up a CI/CD pipeline (a GitHub Actions YAML file) so that any future
   update merged into `main` is automatically built and pushed live to Azure,
   with no manual deployment step required.

## Steps

### Step 1 — Create the GitHub Repository and Static Web App Code

1. Go to github.com and create a new repository
2. Check "Add a README file" and create the repository.
3. Add a new file named `index.html` in the repository root with simple
   HTML content.
4. Commit the file directly to the `main` branch.

### Step 2 — Create the Azure Static Web App and Connect to GitHub

1. Go to portal.azure.com and search for "Static Web Apps".
2. Click Create, then fill in the basics: subscription, resource group,
   name, plan type (Free), and region.
3. Under Deployment details, select GitHub as the source.
4. Sign in to GitHub and authorize Azure when prompted.
5. Select the Organization, Repository, and Branch (`main`).
6. Under Build Details, set Build Presets to Custom, App location to `/`,
   and leave Output location blank (plain HTML, no build step).
7. Click Review + Create, then Create.

Signing in with GitHub during this step causes Azure to automatically:
- Generate a deployment token for the Static Web App.
- Add that token as a secret named `AZURE_STATIC_WEB_APPS_API_TOKEN` in the
  GitHub repository (visible under repo Settings > Secrets and variables >
  Actions).
- Create a GitHub Actions workflow YAML file in `.github/workflows/`.
- Commit that workflow file to the repo, which triggers the first deploy.

### Step 3 — Confirm the Site Is Live

1. In the GitHub repository, open the Actions tab and confirm the workflow
   run completes successfully (green checkmark).
2. In the Azure Portal, open the Static Web App resource, go to Overview,
   and click the URL shown there.
3. Confirm the page loads and displays the expected content.

   <img width="1917" height="916" alt="Static-web-app-on-azure" src="https://github.com/user-attachments/assets/5e7e55cc-ec4a-4aef-9195-24ea85910b84" />

   <img width="620" height="247" alt="Web-url" src="https://github.com/user-attachments/assets/0addbe51-0367-4cc0-add0-fca38592c302" />

### Step 4 — Make an Update and Confirm Auto-Deploy

1. Edit `index.html` in GitHub (directly, or via a pull request).
2. Commit the change to `main` (or merge the pull request into `main`).
3. In the Actions tab, confirm a new workflow run starts automatically.
4. Once the run finishes successfully, refresh the live Azure URL and
   confirm the update appears — with no manual deployment step required.

   <img width="1406" height="287" alt="github-action" src="https://github.com/user-attachments/assets/0f2dc393-27cd-492b-a347-fc617246a80a" />

   <img width="582" height="250" alt="After-update-web-url" src="https://github.com/user-attachments/assets/cd1a14b9-1561-4db3-9409-66793d7e9467" />




