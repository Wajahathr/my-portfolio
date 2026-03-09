# Wajahat Rasool - Personal Portfolio 🚀

Welcome to the repository of my personal portfolio website! This project showcases my skills as a Cloud & DevOps Engineer, featuring my tech stack, certifications, and upcoming hands-on projects.

## 🌐 Live Website
**[👉 Click here to view My Portfolio](http://whtr-portfolio-website.s3-website-us-east-1.amazonaws.com)**

## 🛠️ Architecture & Technologies Used
* **Frontend:** HTML5, CSS3, Bootstrap 5, JavaScript
* **Hosting:** AWS S3 (Static Website Hosting)
* **CI/CD Pipeline:** GitHub Actions
* **Version Control:** Git & GitHub

## ⚙️ Automated Deployment (CI/CD)
This repository is fully automated using **GitHub Actions**. The deployment pipeline is designed so that whenever a new commit is pushed to the `main` branch, the CI/CD workflow automatically triggers. It configures AWS credentials and syncs the latest HTML, CSS, and asset files directly to the **AWS S3 Bucket**, updating the live website instantly without any manual intervention.

## 🚀 How The Pipeline Works
1. Code changes (e.g., updating a project or adding an image) are pushed to GitHub.
2. The GitHub Actions workflow detects the push event.
3. The runner checks out the code and sets up the AWS CLI.
4. Using secure GitHub Secrets (`AWS_ACCESS_KEY_ID` & `AWS_SECRET_ACCESS_KEY`), it authenticates with AWS.
5. The `aws s3 sync` command replaces the old files in the bucket with the updated files.
6. The live portfolio reflects the changes immediately!

## 💻 Run Locally
To view or edit this project locally on your machine:
1. Clone this repository:
   ```bash
   git clone [https://github.com/yourusername/your-repo-name.git](https://github.com/yourusername/your-repo-name.git)
2. Navigate to the folder and simply open the index.html file in your favorite web browser. No  
   local server is required.

