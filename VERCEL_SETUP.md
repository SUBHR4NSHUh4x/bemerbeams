# Vercel Deployment Setup Guide

## Issue Identified

The deployment is failing because of two main issues:

1. The Vercel CLI has hit a rate limit ("Resource is limited - try again in 15 minutes")
2. The environment variables referenced in vercel.json were using secret references that don't exist

## Manual Deployment Steps

### Step 1: Prepare Your Project

1. Make sure your project is pushed to GitHub
2. Ensure you have the updated vercel.json file (with the environment variable references fixed)

### Step 2: Deploy via Vercel Dashboard

1. Go to [Vercel Dashboard](https://vercel.com/dashboard)
2. Click "Add New" → "Project"
3. Import your GitHub repository
4. Select the repository containing your Quiz Spark project

### Step 3: Configure Environment Variables

Add the following environment variables in the Vercel dashboard:

```
MONGO_URL=mongodb+srv://aparajitapriyadarshini079:nbcLH3P6RXebsCCF@cluster0.jvcwiba.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0
MONGODB_URI=mongodb+srv://aparajitapriyadarshini079:nbcLH3P6RXebsCCF@cluster0.jvcwiba.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0

# Clerk Authentication
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_YWxlcnQtc25pcGUtNTkuY2xlcmsuYWNjb3VudHMuZGV2JA
CLERK_SECRET_KEY=sk_test_RlrCrEm1NstsVtEy4gI5FE4uSVzuReSTISogxQMHYM

NEXT_PUBLIC_CLERK_SIGN_IN_URL=/sign-in
NEXT_PUBLIC_CLERK_SIGN_UP_URL=/sign-up
NEXT_PUBLIC_CLERK_AFTER_SIGN_IN_URL=/dashboard
NEXT_PUBLIC_CLERK_AFTER_SIGN_UP_URL=/dashboard

# Admin Authentication
NEXT_PUBLIC_ADMIN_USERNAME=beamer
NEXT_PUBLIC_ADMIN_PASSWORD=BemerBrands@admin
```

To set these variables:

1. In your Vercel project dashboard, go to "Settings" → "Environment Variables"
2. Add each variable with its corresponding value
3. Make sure to select all environments (Production, Preview, Development)
4. Click "Save"

### Step 4: Configure Build Settings

Vercel should automatically detect that this is a Next.js project, but you can verify the settings:

1. Framework Preset: Next.js
2. Build Command: `npm run build`
3. Output Directory: `.next`
4. Install Command: `npm install`

### Step 5: Deploy

1. Click "Deploy" to start the deployment process
2. Vercel will clone your repository, install dependencies, build the project, and deploy it
3. Once deployment is complete, you'll receive a URL for your deployed application

## Troubleshooting Common Deployment Issues

### Diagnostic Endpoints

The application includes two special endpoints to help diagnose deployment issues:

1. **Health Check Endpoint**: `https://your-deployment-url.vercel.app/api/health`
   - This lightweight endpoint doesn't require database access
   - It shows if your Next.js application is running correctly
   - It displays which environment variables are present (without revealing values)
   - Use this as your first check after deployment

2. **Database Test Endpoint**: `https://your-deployment-url.vercel.app/api/test-vercel`
   - This endpoint tests your MongoDB connection
   - It provides detailed diagnostic information about your deployment
   - It attempts to perform basic database operations to verify functionality

### 1. Build Failures

If your build fails, check the build logs for specific errors. Common issues include:

- Missing dependencies
- Environment variable references that don't exist
- Syntax errors in your code

### 2. MongoDB Connection Issues

Ensure your MongoDB Atlas cluster allows connections from Vercel's IP addresses:

1. Go to MongoDB Atlas dashboard
2. Navigate to Network Access
3. Add `0.0.0.0/0` to allow connections from anywhere (for testing purposes)

### 3. Environment Variable Issues

Double-check that all environment variables are correctly set in the Vercel dashboard. Make sure there are no typos or missing variables.

### 4. Clerk Authentication Issues

Verify that your Clerk authentication keys are correct and that you've set up the proper redirect URLs in your Clerk dashboard.

## Redeploying After Changes

When you push changes to your GitHub repository, Vercel will automatically redeploy your application. You can also manually trigger a redeployment from the Vercel dashboard.

## Important Notes

1. The `vercel.json` file in your project contains important configuration settings for your deployment
2. Make sure your MongoDB connection is optimized for serverless environments
3. Consider using Vercel's preview deployments for testing changes before they go to production
4. If you continue to face rate limit issues with the Vercel CLI, always use the dashboard for deployments