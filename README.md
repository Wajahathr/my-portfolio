# 🚀 Zero to Hero: Automating My Portfolio Deployment to AWS S3

Hey there! 👋 Welcome to my portfolio repository. 

This project is a complete "Zero to Hero" practical implementation of Cloud Engineering and DevOps concepts. I took a standard static website (HTML, CSS, JS) and hosted it on **AWS S3**. To take it a step further, I set up a fully automated **CI/CD pipeline using GitHub Actions**. Now, whenever I push new code to this repository, my live website updates automatically!

### 🌍 Live Demo
Check out the live website here: [My AWS S3 Hosted Portfolio](http://whtr-portfolio-website.s3-website-us-east-1.amazonaws.com)

---

## 🛠️ Tech Stack
* **Frontend:** HTML, CSS, JavaScript
* **Cloud Infrastructure:** Amazon Web Services (AWS S3, IAM)
* **CI/CD Automation:** GitHub Actions

---

## 🚀 How I Built This (The Step-by-Step Process)

I broke this project down into 6 straightforward phases:

### Phase 1: Local Development
Everything started on my local machine.
* I set up my project directory in VS Code with my `index.html`, `style.css`, `script.js`, and `assets`.
* Initialized a local Git repository, staged the files, and made my initial commit.

### Phase 2: Pushing to GitHub
* Created a brand new repository here on GitHub.
* Linked my local VS Code terminal to this remote repository and pushed my code to the `main` branch.

### Phase 3: Setting Up AWS S3 (Cloud Hosting)
This is where the cloud magic happens.
* Logged into the AWS Management Console and created a new S3 bucket named `whtr-portfolio-website`.
* **Important:** Unchecked "Block all public access" because I want the world to see this site!
* Enabled "Static website hosting" in the bucket properties and set `index.html` as the default document.
* Wrote a custom JSON Bucket Policy to grant public read access so anyone on the internet can view the site.

### Phase 4: Securing AWS with IAM
Security is critical, so I didn't use my root AWS account credentials for automation.
* Went into AWS IAM (Identity and Access Management).
* Created a dedicated user just for GitHub Actions and granted it S3 access.
* Generated an **Access Key ID** and a **Secret Access Key** for this user. (Never hardcode these into your files!)

### Phase 5: Hiding Secrets in GitHub
To let GitHub talk to AWS securely, I had to store those keys safely.
* Navigated to my repository's **Settings > Secrets and variables > Actions**.
* Saved my AWS keys as repository secrets under the names `ACCESS_KEY` and `SECRET_KEY`.

### Phase 6: The CI/CD Pipeline (GitHub Actions)
The final step was automating the deployment process.
* Inside my project, I created a specific folder structure: `.github/workflows/`.
* Created a `deploy.yml` file to tell GitHub exactly what to do when new code is pushed.

Here is the exact workflow I'm using:

```yaml
name: Portfolio Deployment

on:
  push:
    branches:
    - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout Code
      uses: actions/checkout@v4

    - name: Configure AWS Credentials
      uses: aws-actions/configure-aws-credentials@v4
      with:
        aws-access-key-id: ${{ secrets.ACCESS_KEY }}
        aws-secret-access-key: ${{ secrets.SECRET_KEY }}
        aws-region: us-east-1

    - name: Deploy static site to S3 bucket
      run: aws s3 sync . s3://whtr-portfolio-website --delete --exclude ".git/*" --exclude ".github/*"
