# SIA-2-PIPELINE FOR STATIC WEBSITE WITH CI/CD  
## A Guide to Create and Deploy a Static Website with CI/CD  

---

### Step 1: Generate a GitHub Personal Access Token
1. Open the **Settings** of your GitHub account.  
2. Navigate to **Developer Settings** in the left sidebar.  
3. Click **Personal Access Tokens**, then select **Tokens (classic)**.  
4. Click **Generate new token**.  
5. Add a note (e.g., "GitHub Pages Deploy Token") and select the necessary scopes (start with `repo` for full control).  
6. Click **Generate token**.  
7. **Important:** Copy and save the token somewhere secure as you will not be able to view it again.  

---

### Step 2: Create a Repository
1. Create a new repository and optionally include a `README.md` file to describe your project.  
2. If you're using a free GitHub account, make sure the repository is **Public** for deployment.  

---

### Step 3: Create a GitHub Repository Secret
1. Go to the **Settings** of your repository.  
2. In the left sidebar, select **Secrets and variables** → **Actions**.  
3. Click **New repository secret**.  
4. Enter a name for your secret (e.g., `SECRET_GITHUB_TOKEN`).  
5. In the value field, paste the GitHub Personal Access Token you generated in Step 1.  
6. Click **Add secret**.  

---

### Step 4: Create Your Static Website
1. Build your static website and place the files in a folder or the root directory, based on your preference.  

---

### Step 5: Create Workflow Files
1. Create a folder named `.github` in your project.  
2. Inside the `.github` folder, create a subfolder named `workflows`.  
3. Inside the `workflows` folder, create a `.yml` file (e.g., `deploy.yml`).  

Here’s a sample workflow content for deployment:

```yaml
name: Deploy to GitHub Pages

# Define the events that trigger this workflow
on:
  push:
    branches:
      - main  # Replace with the branch that holds your code

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.SECRET_GITHUB_TOKEN }}
          publish_dir: ./  # Or ./"the folder name where your static files are located"

```

### Step 6: Configure GitHub Pages
1. Open the **Settings** of your repository.  
2. Select **Pages** in the left sidebar.  
3. Under **Branch**, select the branch that contains your static website files (e.g., `main`).  
4. Specify the **Folder** path where your static files are located (e.g., `/root` or `/docs`).  
5. Click **Save**.  

---

### Step 7: Deploy Your Website
1. Go to the **Code** tab in your repository.  
   - You’ll see a status indicator (a small colored circle) for the workflow triggered by your `.yml` file.  
2. GitHub will process your workflow using the `.yml` file and validate your code. If any issues are found, deployment will stop.  
3. If the process succeeds, the site will be deployed, and you can find the link in the **Actions** tab.  
   - Go to the **Deployment** job under **Management**, where you’ll see the deployment URL.  
4. For Updating the website, you can just commit the changes then it will automatically verify and rerun it with the CI CD.

**Deployed URL Format:**  
`https://<your-username>.github.io/<repository-name>/`

---

Congratulations! Your static website is now live and integrated with a CI/CD pipeline. 🚀

### Step 8: Update Your Website
1. Make changes to your website files in the repository.
2. Commit your changes with a descriptive message.
3. Push the changes to your GitHub repository.
4. GitHub Actions will automatically detect the push to the repository and rerun the CI/CD pipeline, verifying the changes and deploying the updated website.

---

This process ensures that every update is automatically deployed without the need for manual intervention.
