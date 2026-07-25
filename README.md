# Static Web App CI/CD Project

## Project Overview

This project is inspired by a real work case: deploying a static web app (a
plain HTML file) to Azure, and designing a CI/CD pipeline that automatically
pushes updates to Azure whenever changes are merged into the `main` branch.

## Background

At work, a client's dashboard was hosted on Azure Static Web Apps, with its
source code stored in a GitHub repository. When an update was merged into
`main`, it did not appear on the live site. 

## Project Goal

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

## What This Demonstrates

- How to connect a GitHub repository to an Azure Static Web App.
- How a GitHub Actions workflow (YAML) file defines an automatic build and
  deploy process.
- The difference between a manually deployed site and one with a proper
  CI/CD pipeline — where merging to `main` is the deploy.
