# Deploying to GitHub Pages

This guide will help you deploy your Academic Workshop site to GitHub Pages at:
**https://Windyy-1007.github.io/academic-workshop**

## Prerequisites

- Git installed on your system
- A GitHub account (Windyy-1007)
- Repository already exists: `academic-workshop`

## Deployment Steps

### Step 1: Commit Your Changes

First, make sure all your changes are committed to the repository:

```powershell
# Check current status
git status

# Add all changes
git add .

# Commit with a message
git commit -m "Add competition page and update for GitHub Pages deployment"
```

### Step 2: Push to GitHub

Push your changes to the main branch:

```powershell
git push origin main
```

### Step 3: Enable GitHub Pages

1. Go to your repository on GitHub: https://github.com/Windyy-1007/academic-workshop
2. Click on **Settings** (top navigation)
3. In the left sidebar, click **Pages** (under "Code and automation")
4. Under "Build and deployment":
   - **Source**: Select "GitHub Actions"
   - (This will use the workflow file at `.github/workflows/deploy.yml`)
5. Click **Save**

### Step 4: Monitor Deployment

1. Go to the **Actions** tab in your repository
2. You should see a workflow run called "Build and Deploy Website"
3. Click on it to see the progress
4. Wait for both "build" and "deploy" jobs to complete (green checkmark ✓)

### Step 5: Access Your Site

Once deployment is complete (usually takes 2-3 minutes):

- **Main site**: https://Windyy-1007.github.io/academic-workshop
- **Competition page**: https://Windyy-1007.github.io/academic-workshop/competition/

## Automatic Deployments

The GitHub Actions workflow is configured to automatically deploy whenever you:

- Push changes to the `main` branch
- Manually trigger from the Actions tab

## Local Testing Before Deployment

Always test locally before pushing:

```powershell
# Start development server
zola serve

# Build for production (creates public/ folder)
zola build
```

## Troubleshooting

### If the site doesn't appear:

1. Check the Actions tab for any failed builds
2. Verify that GitHub Pages is enabled in Settings > Pages
3. Make sure the source is set to "GitHub Actions"
4. Wait a few minutes - DNS propagation can take time

### If links are broken:

1. Check that `base_url` in `config.toml` matches your GitHub Pages URL
2. Rebuild and redeploy

### If you need to use a custom domain:

1. In Settings > Pages, add your custom domain
2. Update `base_url` in `config.toml` to your custom domain
3. Commit and push changes

## What Happens During Deployment

The GitHub Actions workflow (`.github/workflows/deploy.yml`) automatically:

1. ✅ Checks out your code
2. ✅ Installs Zola (v0.21.0)
3. ✅ Runs `zola build` to generate static files
4. ✅ Uploads the `public/` folder
5. ✅ Deploys to GitHub Pages

## Files Changed for Deployment

- `config.toml` - Updated `base_url` to your GitHub Pages URL
- `.github/workflows/deploy.yml` - Already configured (no changes needed)
- `content/competition/_index.md` - Your new competition page

## Next Steps After Deployment

1. Share the URL: https://Windyy-1007.github.io/academic-workshop/competition/
2. Test all links and navigation
3. Continue editing content - changes will auto-deploy when pushed

---

**Ready to deploy?** Run these commands:

```powershell
git add .
git commit -m "Add competition page and configure for GitHub Pages"
git push origin main
```

Then visit the Actions tab to watch your site deploy! 🚀
