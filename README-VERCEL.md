# Vercel Deployment Guide

This guide explains how to deploy this monorepo application to Vercel.

## Environment Variables

Before deploying, make sure to set the following environment variables in your Vercel project settings:

### Required Environment Variables

- **DATABASE_URL**: PostgreSQL connection string for your database
- **NODE_ENV**: Set to `production` for production deployments

### Optional Environment Variables

- **PORT**: API server port (defaults to 3001)
- **CUSTOM_KEY**: Custom environment key used in the application

## Deployment Steps

1. **Connect your repository to Vercel**
   - Go to [Vercel Dashboard](https://vercel.com/dashboard)
   - Click "Add New..." → "Project"
   - Import your Git repository

2. **Configure Environment Variables**
   - In your Vercel project settings, go to "Environment Variables"
   - Add all required environment variables listed above
   - Make sure to select the appropriate environments (Production, Preview, Development)

3. **Build Configuration**
   - The project uses `vercel.json` for deployment configuration
   - Vercel will automatically detect it's a Next.js application
   - The build command is set to `pnpm build`

4. **Deploy**
   - Push changes to your repository
   - Vercel will automatically deploy your application
   - Monitor the deployment logs for any issues

## Project Structure

```
my-app/
├── apps/
│   ├── web/          # Next.js frontend application
│   └── api/          # Hono API backend
├── api/              # Vercel serverless function entry point
├── packages/         # Shared packages
├── vercel.json       # Vercel deployment configuration
└── package.json      # Root package configuration
```

## API Routes

The API is deployed as a serverless function and accessible at:
- `/api/health` - Health check endpoint
- `/api/work-items` - Work items management
- `/api/dashboard` - Dashboard data

## Database Setup

This application uses PostgreSQL with Drizzle ORM. Make sure:

1. Your database is accessible from Vercel
2. The `DATABASE_URL` environment variable is correctly set
3. Database migrations are run before deployment

## Troubleshooting

### Build Issues
- Ensure all dependencies are installed with `pnpm install`
- Check that `pnpm build` runs successfully locally

### Runtime Issues
- Verify all environment variables are set correctly
- Check the Vercel function logs for any runtime errors
- Ensure database connectivity

### API Issues
- Verify the API routes are accessible at `/api/*`
- Check CORS configuration if making requests from different domains

## Local Development

To run the project locally:

```bash
# Install dependencies
pnpm install

# Run development servers
pnpm dev
```

This will start:
- Next.js frontend on http://localhost:3000
- API server on http://localhost:3001
