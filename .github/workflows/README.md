## 🚀 GitHub Actions: Deploy Astro Site

### 🔄 Trigger
- This workflow **only runs on pushes to the `deploy` branch**
- Develop your site normally on the `main` branch
- When you're ready to deploy, **merge or push to `deploy`** to trigger the build and deployment

### 🔐 Security
- Uses `secrets.GH_TOKEN` for write access during deployment
- Uses `secrets.WEBHOOK_URL` to trigger external deployments (e.g., on a Plesk server)

### 📦 Build
- Automatically detects the package manager (`npm` or `yarn`)
- Performs a clean install (`npm install`)
- Builds the Astro site into the `dist/` directory

### 📤 Export
- Exports the static site to the `data_build` branch
- ⚠️ `data_build` is used **only as an export target** and should **not be edited manually**

### 🌐 Webhook
- After a successful build, a POST request is sent to `secrets.WEBHOOK_URL`
- This can trigger a script on your server (e.g., on Plesk) to pull the latest `data_build` branch

### 🧠 Note
- On the Plesk server, you should have a cron job or hook that performs a `git pull` or similar action after receiving the webhook