# 🚀 Instructions de Déploiement Production

## 1️⃣ Préparation du Déploiement

### Vérifier l'état du projet
```bash
# Cloner/mettre à jour le repository
git clone https://github.com/sidimed1968/site_onsp.git
cd site_onsp

# Checkout la branche de maintenance
git checkout maintenance/update-dependencies-2024

# Mettre à jour les dépendances
npm install
```

### Vérifier la configuration locale
```bash
# Créer un fichier .env.local (ne pas commiter)
cp .env.example .env.local

# Éditer avec vos credentials Turso
nano .env.local
# ou
code .env.local
```

### Tester localement
```bash
# Build de production
npm run build

# Vérifier pas d'erreurs
npm run typecheck
npm run lint

# Tester en local
npm run dev
# Visiter http://localhost:3000
```

## 2️⃣ Merger sur la branche principale

```bash
# Mettre à jour main depuis origin
git fetch origin
git checkout main
git pull origin main

# Merger la branche de maintenance
git merge maintenance/update-dependencies-2024

# Vérifier les changements
git log --oneline -5

# Pousser vers GitHub
git push origin main
```

## 3️⃣ Déploiement sur Netlify

### Option A : Déploiement Automatique (recommandé)

Netlify détecte automatiquement les changements sur `main` :

1. Aller sur https://app.netlify.com/teams/[TEAM]/sites
2. Sélectionner le site "onps-site"
3. Vérifier dans **Deployments** que le build s'est lancé
4. Attendre que le status passe à ✅ **Published**

### Option B : Déploiement Manuel

Si le déploiement ne se déclenche pas automatiquement :

1. Dashboard Netlify → Site settings
2. Cliquer sur "Trigger deploy" → "Deploy site"
3. Attendre 3-5 minutes pour le build

### Vérifier le déploiement

```bash
# 1. Vérifier l'URL publique
curl https://votre-site.netlify.app/

# 2. Tester l'API health
curl https://votre-site.netlify.app/api/health

# 3. Vérifier les headers HTTPS
curl -I https://votre-site.netlify.app/
# Doit afficher : HTTP/2 200
```

## 4️⃣ Vérifications Post-Déploiement

### Frontend
- [ ] Site charge correctement
- [ ] CSS/Tailwind appliqués
- [ ] Images visibles
- [ ] Menu de navigation fonctionne
- [ ] Responsive sur mobile (F12 → device mode)

### API
```bash
# Health check
curl https://votre-site.netlify.app/api/health
# Réponse attendue: {"status":"ok"}

# Admin check (avec auth)
curl https://votre-site.netlify.app/api/admin/maintenance
# Doit retourner la config de maintenance
```

### Base de données
```bash
# Vérifier la connexion Turso
# (visible dans les logs Netlify si erreur)

# Vérifier les tables
# Aller sur https://console.turso.io
# → Vérifier que la DB "onps-prod" existe
# → Vérifier que les tables sont présentes
```

### Performance
- [ ] Lighthouse score > 80
- [ ] Page load time < 3s
- [ ] Core Web Vitals ✅
- [ ] Pas d'erreurs console (F12)

## 5️⃣ Configuration Netlify (une seule fois)

Si c'est la première fois que vous déployez :

### Variables d'environnement

1. Netlify Dashboard → Site settings → Build & deploy → Environment
2. Ajouter les variables :

```
TURSO_DATABASE_URL = libsql://your-db.turso.io
TURSO_AUTH_TOKEN = your_token_here
NODE_ENV = production
ADMIN_PASSWORD = your_secure_password
```

### Build settings

- Build command : `npm run build`
- Publish directory : `.next`
- Functions directory : `functions`

### Domain

1. Aller à "Domain management"
2. Ajouter votre domaine personnalisé (ex: onps.sn)
3. Configurer les DNS records
4. Vérifier le certificat HTTPS auto

## 🔄 Déploiement Régulier (maintenance)

Pour les futures mises à jour :

```bash
# 1. Créer une branche
git checkout -b maintenance/update-YYYY-MM-DD

# 2. Faire les changements
# ... modifications ...

# 3. Tester localement
npm run build && npm run typecheck

# 4. Commiter
git add .
git commit -m "chore: maintenance updates"

# 5. Pousser
git push origin maintenance/update-YYYY-MM-DD

# 6. Créer une PR sur GitHub (optionnel)
# Puis merger sur main

# 7. Netlify déploie automatiquement
```

## 🚨 En cas de problème

### Build échoue
```bash
# Vérifier les logs Netlify
# → Deployments → [failed-build] → Logs

# Cleanup local
rm -rf node_modules .next
npm install
npm run build
```

### API répond avec erreur 500
```bash
# Vérifier les variables Turso
# 1. Dashboard Netlify → Environment variables
# 2. Vérifier TURSO_DATABASE_URL
# 3. Vérifier TURSO_AUTH_TOKEN
# 4. Redéployer si changé
```

### Rollback rapide
```bash
# Via Netlify Dashboard
1. Deployments → [previous-success] → Deploy preview
2. Cliquer sur "Lock and deploy"

# Ou via Git
git revert HEAD
git push origin main
```

## 📊 Monitoring en Production

### Logs Netlify
- Dashboard → Deployments → [latest] → Logs
- Chercher les erreurs ou warnings

### Analytics
- Dashboard → Analytics
- Vérifier le traffic et les erreurs

### Uptime
- Configurer des alertes (optionnel)
- Utiliser Netlify built-in monitoring

## 📞 Support

**Docs officielles** :
- Netlify : https://docs.netlify.com
- Next.js : https://nextjs.org/docs
- Turso : https://docs.turso.tech

**Problèmes courants** :
- [Netlify FAQ](https://docs.netlify.com/getting-started/faq/)
- [Next.js Deployment](https://nextjs.org/docs/app/building-your-application/deploying)

---

**Version** : 1.0  
**Dernière maj** : Juin 2024