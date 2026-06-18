# 🔧 Mise à Jour de Maintenance - ONPS Site

**Date**: Juin 2024  
**Version**: 1.0.1  
**Statut**: ✅ Prêt pour le déploiement

## 📋 Vue d'ensemble

Ce guide explique les mises à jour de maintenance appliquées au projet ONPS Site pour assurer la stabilité, la sécurité et la performance.

## 🔄 Mises à jour effectuées

### 1. Dépendances principales
- ✅ **Next.js** : 16.2.6 (stable et optimisé)
- ✅ **React** : 19.2.6 (dernière version stable)
- ✅ **TypeScript** : 5.9.3 (stabilité de type améliorée)

### 2. Base de données
- ✅ **Drizzle ORM** : 0.45.2 (sans changements majeurs)
- ✅ **Drizzle Kit** : 0.31.10 (migrations)
- ✅ **LibSQL Client** : 0.17.3 (Turso support)

### 3. Styles et UI
- ✅ **Tailwind CSS** : 4.1.17
- ✅ **Lucide React** : 0.468.0 (icônes)

### 4. Configuration de déploiement
- ✅ **Netlify Plugin Next.js** : 5.14.5
- ✅ **ESLint** : 9.39.4 (linting)

## 🚀 Procédure de déploiement

### Étape 1 : Préparation locale
```bash
# Cloner la branche de maintenance
git checkout maintenance/update-dependencies-2024

# Installer les dépendances mises à jour
npm install

# Vérifier la compilation
npm run build

# Tester localement
npm run dev
```

### Étape 2 : Tests
```bash
# Vérifier les types TypeScript
npm run typecheck

# Linter le code
npm run lint

# Tester la santé de l'API
curl http://localhost:3000/api/health
```

### Étape 3 : Déploiement sur Netlify

1. **Fusionner la branche** sur `main`
   ```bash
   git pull origin main
   git merge maintenance/update-dependencies-2024
   git push origin main
   ```

2. **Déclencher le déploiement** :
   - Netlify détecte automatiquement les changements
   - Vérifier le build status sur le dashboard
   - URL : https://app.netlify.com/

3. **Vérifier le déploiement** :
   ```bash
   curl https://votre-domaine.netlify.app/api/health
   ```

## ✅ Checklist pré-déploiement

- [ ] Toutes les dépendances sont à jour
- [ ] Le build Next.js s'exécute sans erreurs
- [ ] Les tests TypeScript passent (`npm run typecheck`)
- [ ] Le linting est correct (`npm run lint`)
- [ ] Les variables d'environnement sont configurées
- [ ] La base de données Turso est accessible
- [ ] Backup de la base de données effectué (optionnel mais recommandé)

## 🔒 Points de sécurité

- ✅ `.env.local` est dans `.gitignore` (jamais poussé)
- ✅ Tokens Turso configurés dans Netlify uniquement
- ✅ Build optimisé sans code de debug
- ✅ ESLint vérifie les erreurs de sécurité

## 📊 Monitoring après déploiement

**Dashboard Netlify** : 
- Vérifier les logs de build
- Surveiller les performances
- Monitorer les erreurs d'API

**Endpoints de vérification** :
```bash
# Health check
curl https://votre-domaine.netlify.app/api/health

# Admin (protégé)
curl -H "Authorization: Bearer YOUR_TOKEN" \
  https://votre-domaine.netlify.app/api/admin/users
```

## 🐛 Troubleshooting

### Build échoue
```bash
# Nettoyer le cache local
rm -rf .next node_modules
npm install
npm run build
```

### Erreurs Turso
- Vérifier `TURSO_DATABASE_URL` dans Netlify
- Vérifier `TURSO_AUTH_TOKEN` dans Netlify
- Vérifier la connexion réseau

### Performance lente
- Analyser les logs Netlify
- Vérifier les temps de réponse Turso
- Profiler avec Chrome DevTools

## 📞 Support

**Documentation officielle** :
- [Next.js Docs](https://nextjs.org/docs)
- [Netlify Docs](https://docs.netlify.com)
- [Turso Docs](https://docs.turso.tech)

---

**Créé par** : Équipe ONPS  
**Dernière mise à jour** : Juin 2024