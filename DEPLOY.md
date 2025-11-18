# Guide de Déploiement - Hot Takes

Ce guide vous explique comment déployer votre application Hot Takes sur Render (backend) et Netlify (frontend).

## 1. Déployer le Backend sur Render

### Étape 1: Créer un compte Render
1. Allez sur [render.com](https://render.com)
2. Inscrivez-vous avec GitHub

### Étape 2: Créer un nouveau Web Service
1. Cliquez sur **"New +"** → **"Web Service"**
2. Connectez votre repository GitHub
3. Sélectionnez le repository `nodejs_hot_takes`
4. Configuration:
   - **Name**: `hot-takes-backend`
   - **Region**: Europe (Frankfurt) ou US
   - **Branch**: `main`
   - **Root Directory**: `backend`
   - **Runtime**: `Node`
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
   - **Instance Type**: `Free`

### Étape 3: Ajouter les variables d'environnement
Dans la section **Environment Variables**, ajoutez:

```
MONGO_URI=mongodb+srv://arumugamjuth_db_user:gXkOFBTNlzoVKtOf@cluster0.hgloprs.mongodb.net/hot-takes?retryWrites=true&w=majority
NODE_ENV=production
```

### Étape 4: Déployer
1. Cliquez sur **"Create Web Service"**
2. Attendez que le déploiement se termine (2-5 minutes)
3. **IMPORTANT**: Notez l'URL de votre backend (ex: `https://hot-takes-backend.onrender.com`)

---

## 2. Déployer le Frontend sur Netlify

### Étape 1: Mettre à jour la configuration Netlify
Avant de déployer, vous devez mettre à jour le fichier `frontend/netlify.toml`:

1. Ouvrez `frontend/netlify.toml`
2. Remplacez `YOUR-BACKEND-URL` par l'URL de votre backend Render:
   ```toml
   [[redirects]]
     from = "/api/*"
     to = "https://hot-takes-backend.onrender.com/api/:splat"
     status = 200
     force = true
   ```

### Étape 2: Commiter et pousser les changements
```bash
git add .
git commit -m "Configure deployment"
git push origin main
```

### Étape 3: Créer un compte Netlify
1. Allez sur [netlify.com](https://netlify.com)
2. Inscrivez-vous avec GitHub

### Étape 4: Déployer le site
**Option A: Via GitHub (Recommandé)**
1. Cliquez sur **"Add new site"** → **"Import an existing project"**
2. Sélectionnez **"Deploy with GitHub"**
3. Choisissez votre repository `nodejs_hot_takes`
4. Configuration:
   - **Base directory**: `frontend`
   - **Build command**: (laisser vide)
   - **Publish directory**: `frontend`
5. Cliquez sur **"Deploy"**

**Option B: Drag & Drop**
1. Cliquez sur **"Add new site"** → **"Deploy manually"**
2. Glissez-déposez le dossier `frontend` entier
3. Attendez la fin du déploiement

### Étape 5: Obtenir l'URL
Netlify vous donnera une URL (ex: `https://random-name.netlify.app`)
