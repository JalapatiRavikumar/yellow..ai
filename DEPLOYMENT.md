# Deployment Guide

This guide will help you deploy your ChatBot Platform to Netlify or Vercel.

## 📋 Prerequisites

1. **MongoDB Atlas Account** - Free tier available at [mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas)
2. **OpenRouter API Key** - Get one at [openrouter.ai](https://openrouter.ai)
3. **GitHub Repository** - Your code is already pushed ✅

## 🚀 Option 1: Deploy Frontend to Vercel (Recommended)

### Step 1: Deploy Backend First

Your backend needs a cloud database. Options:
- **Railway** (Recommended) - [railway.app](https://railway.app) - Free tier available
- **Render** - [render.com](https://render.com) - Free tier available
- **Fly.io** - [fly.io](https://fly.io) - Free tier available

#### Deploy Backend to Railway:

1. Go to [railway.app](https://railway.app) and sign in with GitHub
2. Click "New Project" → "Deploy from GitHub repo"
3. Select your repository
4. Select the `server` folder as the root directory
5. Add these environment variables in Railway dashboard:
   ```
   MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/chatbot-platform
   JWT_SECRET=your-super-secret-jwt-key-here
   OPENROUTER_API_KEY=your-openrouter-api-key
   PORT=3001
   FRONTEND_URL=https://your-frontend-url.vercel.app
   ```
6. Deploy! Railway will give you a URL like `https://your-backend.up.railway.app`

### Step 2: Deploy Frontend to Vercel

1. Go to [vercel.com](https://vercel.com) and sign in with GitHub
2. Click "Add New Project"
3. Import your GitHub repository
4. Configure the project:
   - **Root Directory**: `client`
   - **Build Command**: `npm run build`
   - **Output Directory**: `dist`
   - **Install Command**: `npm install`
5. Add environment variable:
   ```
   VITE_API_URL=https://your-backend.up.railway.app/api
   ```
6. Click "Deploy"!

Your frontend will be live at `https://your-project.vercel.app`

---

## 🌐 Option 2: Deploy Frontend to Netlify

### Step 1: Deploy Backend (same as above)
- Deploy backend to Railway or another service
- Get your backend URL

### Step 2: Deploy Frontend to Netlify

1. Go to [netlify.com](https://netlify.com) and sign in with GitHub
2. Click "Add new site" → "Import an existing project"
3. Select your GitHub repository
4. Configure build settings:
   - **Base directory**: `client`
   - **Build command**: `npm run build`
   - **Publish directory**: `client/dist`
5. Click "Show advanced" and add environment variable:
   ```
   VITE_API_URL=https://your-backend.up.railway.app/api
   ```
6. Click "Deploy site"!

Your frontend will be live at `https://your-project.netlify.app`

---

## 🔧 Setting Up MongoDB Atlas

1. Go to [mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas)
2. Create a free account
3. Create a new cluster (choose free tier)
4. Go to "Database Access" → "Add New Database User"
   - Create a username and password (save these!)
5. Go to "Network Access" → "Add IP Address"
   - Click "Allow Access from Anywhere" (0.0.0.0/0)
6. Go to "Database" → Click "Connect" on your cluster
7. Choose "Connect your application"
8. Copy the connection string
9. Replace `<password>` with your database password
10. Use this as your `MONGODB_URI` environment variable

Example: `mongodb+srv://username:password@cluster0.xxxxx.mongodb.net/chatbot-platform?retryWrites=true&w=majority`

---

## ✅ Post-Deployment Checklist

- [ ] Backend is deployed and accessible
- [ ] MongoDB Atlas cluster is connected
- [ ] Environment variables are set correctly
- [ ] Frontend can communicate with backend (check browser console)
- [ ] Test user registration and login
- [ ] Test chat functionality

---

## 🐛 Troubleshooting

### CORS Errors
- Make sure `FRONTEND_URL` in backend matches your frontend URL exactly
- Include protocol (`https://`)

### API Connection Issues
- Verify `VITE_API_URL` in frontend includes `/api` at the end
- Check backend logs for connection errors
- Ensure MongoDB connection string is correct

### Build Failures
- Check Node.js version (should be 18+)
- Verify all dependencies are in `package.json`
- Check build logs for specific errors

---

## 📝 Notes

- Your backend URL will change after each deployment to Railway/Render
- Update `FRONTEND_URL` in backend and `VITE_API_URL` in frontend if URLs change
- Consider using a custom domain for production
- MongoDB Atlas free tier has limitations (512MB storage)

Happy deploying! 🚀

