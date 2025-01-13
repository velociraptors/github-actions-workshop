# GitHub Actions: From Zero to Hero Workshop

In this workshop we're going to cover GitHub Actions. For a tangentially related workshop of using GitHub Actions to deploy to Azure using Bicep, check out this repo: https://github.com/scottsauber/workshop-dotnet-azure-github-bicep.

## Pre-requisites:

- Basic Git Knowledge
- GitHub Account
- Recommended: an editor with a GitHub Actions extension installed for intellisense (ie [VS Code](https://code.visualstudio.com/) with the [GitHub Actions extension](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-github-actions))
- Optional: .NET 9 installed locally to run the app locally

## Module 1 - Slides: CI/CD Pipelines

No hands-on work, just going over slides

## Module 2 - Slides: GitHub Actions

No hands-on work, just going over slides

## Module 3 - Hands On: Creating a PR Verify Workflow

1. Fork this repository if you haven't already.
1. Create a new branch
1. Create a `.github` folder in the root
1. Under the `.github` folder, create a `workflows` folder
1. Under the `workflows` folder, create a `pr-verify.yml` file
1. Paste the following into that file:

   ```yml
   name: PR Verify

   on:
     pull_request:
       branches: ["main"]
     workflow_dispatch:

   jobs:
     build:
       name: PR Verify
       runs-on: ubuntu-22.04

       steps:
         - uses: actions/checkout@v4

         - name: Set up .NET Core
           uses: actions/setup-dotnet@v4
           with:
             dotnet-version: 9.0.x

         - name: Build with dotnet
           run: dotnet build --configuration Release

         - name: Test
           run: dotnet test --configuration Release --no-build
   ```

1. Commit, Push, and Open a PR
1. Do you think the GitHub Action will trigger when it's not committed on the `main` branch?
1. Scroll down to the bottom of the PR and notice you have a new status check called "PR Verify" and click on it
1. Watch the build succeed
1. Make a change that makes the code not compile. ie open the src/WorkshopDemo/Program.cs file and add a letter to the first line
1. Commit and push and watch it fail
1. Undo that change and let's make a test fail.
1. Open /src/WorkshopDemo.Core.Tests/Common/FileServiceTests.cs and change the assertion on line 19 to something like `result.Should().Be("Hello world");`
1. Commit and push and watch it fail
1. Undo that change and commit and push
1. Do not merge it in yet

## Module 4 - Slides: Optimal GitHub settings

## Module 5 - Hands On: Merge PR and Required Rule set

1. Merge the PR from Module 3
1. Setup a required rule set
