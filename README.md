# Deploying JSON Server on Render

This document provides step-by-step instructions to deploy a local `json-server` to Render and solutions to common deployment errors.

---

## **1. Prerequisites**
Ensure you have the following installed:
- [Node.js](https://nodejs.org/) (Latest version)
- [Git](https://git-scm.com/)
- A [GitHub](https://github.com/) account
- A [Render](https://dashboard.render.com/) account

---

## **2. Setting Up Local JSON Server**
### **Step 1: Initialize a Node.js Project**
```sh
mkdir json-server-api
cd json-server-api
npm init -y
```

### **Step 2: Install Dependencies**
```sh
npm install json-server
```

### **Step 3: Create `db.json` (Mock Database)**
Create a `db.json` file and add sample data:
```json
{
  "comments": [
    { "id": 1, "content": "Hello, world!" }
  ]
}
```

### **Step 4: Define Start Script**
Modify `package.json`:
```json
"scripts": {
  "api": "json-server --watch db.json --port 4000"
}
```

### **Step 5: Run Locally**
```sh
npm run api
```
This starts a local server at `http://localhost:4000`.

---

## **3. Deploy to GitHub**
### **Step 1: Initialize Git Repository**
```sh
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/yourusername/json-server-api.git
git push -u origin main
```

### **Step 2: Create a Public Directory (Fix for Render Error)**
```sh
mkdir public
touch public/index.html
```
Add `public/index.html` with some basic content:
```html
<!DOCTYPE html>
<html>
<head><title>JSON Server</title></head>
<body><h1>JSON Server Deployed</h1></body>
</html>
```

Commit and push the changes:
```sh
git add .
git commit -m "Added public folder to fix Render deployment"
git push origin main
```

---

## **4. Deploy on Render**
### **Step 1: Create a Web Service**
- Log in to [Render](https://dashboard.render.com/).
- Click **New Web Service**.
- Select **GitHub Repository** (`json-server-api`).

### **Step 2: Configure Deployment**
- **Build Command:**
  ```sh
  npm install -g json-server
  ```
- **Start Command:**
  ```sh
  npm run api
  ```

### **Step 3: Deploy & Verify**
- Click **Deploy**.
- Check **Logs** for errors.
- Test API Endpoint: `https://your-render-url.onrender.com/comments`

---

## **5. Fixing Common Errors**
### **🚨 Error 1: `json-server: Permission denied`**
**Cause:** Render couldn’t execute `json-server`.

**Fix:** Use a global install:
```sh
npm install -g json-server
```

### **🚨 Error 2: `Error: ENOENT: no such file or directory, scandir '/opt/render/project/src/public'`**
**Cause:** Render couldn’t find the `public/` folder.

**Fix:**
```sh
mkdir public
touch public/index.html
git add .
git commit -m "Added public folder to fix Render deployment"
git push origin main
```

---

## **6. Conclusion**
You have successfully deployed a local JSON server to Render! 🎉
If you face further issues, check the [Render Logs](https://dashboard.render.com/) or [Render Documentation](https://render.com/docs).

