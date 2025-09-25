# Node.js Demo App

Welcome to the **Node.js Demo App**!  
This repository showcases a sample Node.js web application and demonstrates a complete CI/CD automation workflow using **GitHub Actions** and **Docker**.

---

## 🚩 Key Features

- **Sample Node.js App**: Basic web application for demonstration.
- **Automated CI/CD Pipeline**: Uses GitHub Actions to test, build, and deploy automatically.
- **Docker Integration**: Containerizes the app and pushes images to DockerHub.
- **Continuous Deployment**: Deploys on every push to the `main` branch.

---

## 🛠️ Technologies Used

- ![Node.js](https://img.shields.io/badge/Node.js-339933?logo=node.js&logoColor=white)
- ![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?logo=github-actions&logoColor=white)
- ![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
- ![DockerHub](https://img.shields.io/badge/DockerHub-2496ED?logo=docker&logoColor=white)

---

## 📦 Workflow Overview

The CI/CD workflow is defined in [`.github/workflows/main.yml`](.github/workflows/main.yml):

![CI/CD Pipeline](https://user-images.githubusercontent.com/your-image-here/pipeline-diagram.png) <!-- Replace with your actual pipeline diagram image URL -->

**Steps:**
1. **Trigger:** On push to the `main` branch.
2. **Test:** Installs dependencies and runs tests.
3. **Build:** Builds the Node.js app.
4. **Dockerize:** Builds a Docker image.
5. **Push:** Pushes image to DockerHub.
6. **(Optional) Deploy:** Extend to deploy to cloud or server.

---

## 🗂️ Example Workflow (`main.yml`)

```yaml
name: CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test

      - name: Build Docker image
        run: docker build -t ${{ secrets.DOCKERHUB_USERNAME }}/nodejs-demo-app:${{ github.sha }} .

      - name: Login to DockerHub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}

      - name: Push image to DockerHub
        run: docker push ${{ secrets.DOCKERHUB_USERNAME }}/nodejs-demo-app:${{ github.sha }}
```

---

## ▶️ How To Use

1. **Fork or Clone** this repository.
2. **Add DockerHub credentials as GitHub secrets:**
   - `DOCKERHUB_USERNAME`
   - `DOCKERHUB_TOKEN`
3. **Push changes to `main` branch** to trigger the workflow.
4. **Monitor the Actions tab** for CI/CD runs and results.

---

## 📝 Notes & Tips

- **Extendability:** Adapt workflow to deploy to AWS, Azure, GCP, or Kubernetes.
- **Security:** Store credentials in GitHub secrets.
- **Customization:** Modify jobs for your specific needs.

---

## 🎯 Learning Outcomes

By using this repository, you will:
- Understand end-to-end CI/CD automation with GitHub Actions.
- Learn Docker containerization for Node.js apps.
- Practice automated image deployment to DockerHub.

---

## 📷 Demo Screenshots

![App Screenshot](https://user-images.githubusercontent.com/your-image-here/app-screenshot.png) <!-- Replace with your actual app screenshot image URL -->
![Workflow Run](https://user-images.githubusercontent.com/your-image-here/workflow-run.png) <!-- Replace with your actual workflow run screenshot image URL -->

---

## 📧 Support

Questions or issues?  
Open an [issue](https://github.com/PranaVernekar/nodejs-demo-app/issues) in this repository.

---

Happy Coding & Shipping! 🚀
