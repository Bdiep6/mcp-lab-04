# GitHub Actions Setup Instructions

## Overview
This repository now has a GitHub Actions workflow that will automatically build and deploy your ASP.NET Core MCP server to Azure whenever you push to the `main` branch.

## Required Setup Steps

### 1. Get Azure Publish Profile
1. Go to the [Azure Portal](https://portal.azure.com)
2. Navigate to your App Service: `bdiep-mcp-fja7abdvgkerbmfr`
3. Click on **"Get publish profile"** in the overview section
4. Download the `.publishsettings` file
5. Open the file in a text editor and copy all the contents

### 2. Add GitHub Secret
1. Go to your GitHub repository: https://github.com/Bdiep6/mcp-lab-04
2. Click on **Settings** (repository settings, not your profile)
3. In the left sidebar, click **Secrets and variables** → **Actions**
4. Click **New repository secret**
5. Name: `AZUREAPPSERVICE_PUBLISHPROFILE`
6. Value: Paste the entire contents of the publish profile file
7. Click **Add secret**

### 3. Workflow Features
- **Automatic deployment**: Triggers on every push to `main` branch
- **Manual deployment**: Can be triggered manually from the Actions tab
- **Build process**: Restores, builds, tests, and publishes your .NET 9 app
- **Artifact upload**: Saves build output for deployment
- **Azure deployment**: Uses Azure Web Apps Deploy action

### 4. Testing the Deployment
Once you've added the publish profile secret:

1. Make any small change to your code
2. Commit and push to the `main` branch:
   ```bash
   git add .
   git commit -m "Test deployment"
   git push
   ```
3. Go to the **Actions** tab in your GitHub repository to watch the deployment
4. Once successful, test your API at: `https://bdiep-mcp-fja7abdvgkerbmfr.canadacentral-01.azurewebsites.net`

## Workflow Structure
- **Build Job**: Builds and tests the application on Ubuntu
- **Deploy Job**: Deploys the application to Azure App Service
- **Environment**: Uses 'Production' environment (you can add approval requirements if needed)

## Troubleshooting
- If deployment fails, check the Actions logs in GitHub
- Ensure the publish profile secret is correctly formatted
- Verify your Azure App Service name matches the workflow configuration