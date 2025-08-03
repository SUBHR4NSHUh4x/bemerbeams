# Deploying to Vercel via Dashboard

## Step 1: Log in to Vercel Dashboard

1. Go to [Vercel Dashboard](https://vercel.com/dashboard)
2. Log in with your account credentials

## Step 2: Create a New Project

1. Click the "Add New..." button
2. Select "Project" from the dropdown menu

![Add New Project](https://vercel.com/docs/static/docs-dark/add-new-project.png)

## Step 3: Import Your Git Repository

1. Connect your GitHub account if not already connected
2. Find and select your Quiz Spark repository
3. Click "Import"

## Step 4: Configure Project Settings

1. Project Name: Choose a name for your deployment (e.g., "quiz-spark")
2. Framework Preset: Make sure "Next.js" is selected
3. Root Directory: Leave as default (should be "/")

## Step 5: Add Environment Variables

Click "Environment Variables" and add the following variables:

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

Make sure to select all environments (Production, Preview, Development) for each variable.

## Step 6: Deploy

1. Click the "Deploy" button
2. Wait for the build and deployment process to complete

## Step 7: Check Deployment Status

1. Once deployment is complete, you'll see a success message
2. Click on the deployment URL to view your live application
3. **Initial Verification**: First check the health endpoint: `https://your-deployment-url.vercel.app/api/health`
   - This lightweight endpoint doesn't require database access
   - It will show if your Next.js application is running correctly
   - It will display which environment variables are present (without revealing values)
4. **Database Verification**: Then test the database connection: `https://your-deployment-url.vercel.app/api/test-vercel`
   - This will verify your MongoDB connection and environment variables
   - If successful, you'll see detailed information about your deployment
   - If there's an error, you'll see diagnostic information to help troubleshoot

## Troubleshooting Deployment Failures

If your deployment fails, follow these steps:

1. Click on the failed deployment to view the build logs
2. Look for specific error messages in the logs
3. Common issues include:
   - Missing environment variables
   - Build errors in your code
   - MongoDB connection issues

### MongoDB Connection Issues

If you see MongoDB connection errors:

1. Go to your MongoDB Atlas dashboard
2. Navigate to Network Access
3. Add `0.0.0.0/0` to allow connections from anywhere (for testing purposes)
4. Try deploying again

### Build Errors

If you see build errors:

1. Check the specific error message in the logs
2. Fix the issue in your local code
3. Push the changes to your GitHub repository
4. Redeploy from the Vercel dashboard

## Redeploying After Changes

When you push changes to your GitHub repository, Vercel will automatically redeploy your application. You can also manually trigger a redeployment:

1. Go to your project in the Vercel dashboard
2. Click on the "Deployments" tab
3. Click the "Redeploy" button next to your latest deployment

## Setting Up a Custom Domain (Optional)

1. Go to your project in the Vercel dashboard
2. Click on the "Domains" tab
3. Add your custom domain
4. Follow the instructions to configure DNS settings