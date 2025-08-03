# Deploying to Vercel via GitHub Integration

This guide provides a step-by-step approach to deploy your Quiz Spark application to Vercel using GitHub integration, which is often the most reliable method for deployment.

## Prerequisites

1. A GitHub account
2. Your project pushed to a GitHub repository
3. A Vercel account (can be created with your GitHub account)
4. MongoDB Atlas account with a cluster set up
5. Clerk account with an application set up

## Step 1: Push Your Code to GitHub

1. If you haven't already, create a new repository on GitHub
2. Initialize Git in your project (if not already done):
   ```bash
   git init
   ```
3. Add all files to Git:
   ```bash
   git add .
   ```
4. Commit the changes:
   ```bash
   git commit -m "Initial commit for Vercel deployment"
   ```
5. Add your GitHub repository as a remote:
   ```bash
   git remote add origin https://github.com/yourusername/your-repo-name.git
   ```
6. Push your code to GitHub:
   ```bash
   git push -u origin main
   ```
   (Use `master` instead of `main` if that's your default branch)

## Step 2: Connect Vercel to GitHub

1. Go to [Vercel](https://vercel.com/) and sign in with your GitHub account
2. Click on "Add New..." > "Project"
3. Select the GitHub repository containing your Quiz Spark project
4. Vercel will automatically detect that it's a Next.js project

## Step 3: Configure Project Settings

1. **Project Name**: Enter a name for your project (e.g., "quiz-spark")
2. **Framework Preset**: Ensure "Next.js" is selected
3. **Root Directory**: Leave as `.` if your project is at the root of the repository
4. **Build and Output Settings**: Leave as default unless you have specific requirements

## Step 4: Set Up Environment Variables

1. Expand the "Environment Variables" section
2. Add the following environment variables:

   | Name | Value |
   |------|-------|
   | `MONGODB_URI` | Your MongoDB connection string (e.g., `mongodb+srv://username:password@cluster.mongodb.net/quizdb?retryWrites=true&w=majority`) |
   | `MONGO_URL` | Same as `MONGODB_URI` |
   | `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY` | Your Clerk publishable key |
   | `CLERK_SECRET_KEY` | Your Clerk secret key |
   | `NEXT_PUBLIC_CLERK_SIGN_IN_URL` | `/sign-in` |
   | `NEXT_PUBLIC_CLERK_SIGN_UP_URL` | `/sign-up` |
   | `NEXT_PUBLIC_CLERK_AFTER_SIGN_IN_URL` | `/` |
   | `NEXT_PUBLIC_CLERK_AFTER_SIGN_UP_URL` | `/` |
   | `NEXT_PUBLIC_ADMIN_USERNAME` | Your admin username |
   | `NEXT_PUBLIC_ADMIN_PASSWORD` | Your admin password |

3. Click "Add" for each variable

## Step 5: Deploy

1. Click "Deploy"
2. Vercel will start the build and deployment process
3. Wait for the deployment to complete (this may take a few minutes)

## Step 6: Verify Deployment

1. Once deployment is complete, Vercel will provide a URL for your application
2. Click on the URL to open your deployed application

## Step 7: Test Deployment

1. **Initial Verification**: First check the health endpoint: `https://your-deployment-url.vercel.app/api/health`
   - This will show if your Next.js application is running correctly
   - It will display which environment variables are present

2. **Database Verification**: Then test the database connection: `https://your-deployment-url.vercel.app/api/test-vercel`
   - This will verify your MongoDB connection
   - If successful, you'll see detailed information about your deployment

3. **Full Application Test**: Navigate to your application's main URL and test the functionality
   - Try signing in with Clerk
   - Test the admin panel with your admin credentials
   - Create a quiz and test the quiz-taking functionality

## Troubleshooting

If you encounter issues during deployment:

1. **Check Deployment Logs**:
   - In your Vercel dashboard, go to the deployment
   - Click on "View Logs" to see detailed build and runtime logs

2. **Check Environment Variables**:
   - Verify all environment variables are set correctly
   - Ensure there are no typos in variable names or values

3. **MongoDB Connection Issues**:
   - Check that your MongoDB Atlas cluster is running
   - Ensure your IP whitelist in MongoDB Atlas includes `0.0.0.0/0` (for testing)
   - Verify your connection string is correct

4. **Continuous Deployment**:
   - Any changes pushed to your GitHub repository will trigger a new deployment
   - You can disable automatic deployments in the Vercel project settings if needed

## Benefits of GitHub Integration

1. **Reliable Deployments**: Avoids issues with direct CLI deployments
2. **Deployment History**: Each commit creates a new deployment with its own URL
3. **Preview Deployments**: Pull requests automatically get preview deployments
4. **Easy Rollbacks**: You can easily revert to a previous deployment if needed
5. **Team Collaboration**: Multiple team members can deploy without sharing credentials

## Next Steps

1. Set up a custom domain in Vercel (optional)
2. Configure additional environment variables for production
3. Set up monitoring and analytics
4. Implement CI/CD workflows for testing before deployment