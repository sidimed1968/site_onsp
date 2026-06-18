# ✅ Checklist de Déploiement - ONPS Site

## 📋 Avant le déploiement

### Code et Dépendances
- [ ] Toutes les dépendances (`npm install`)
- [ ] Build local réussi (`npm run build`)
- [ ] Pas d'erreurs TypeScript (`npm run typecheck`)
- [ ] Linting OK (`npm run lint`)
- [ ] Pas de fichiers `.env.local` en staging

### Base de Données
- [ ] Credentials Turso disponibles
- [ ] `TURSO_DATABASE_URL` défini
- [ ] `TURSO_AUTH_TOKEN` défini
- [ ] Backup de la BD effectué (recommandé)
- [ ] Tables schema à jour

### Environnement Netlify
- [ ] Account Netlify actif
- [ ] Repository GitHub connecté
- [ ] Variables d'environnement configurées :
  - [ ] `TURSO_DATABASE_URL`
  - [ ] `TURSO_AUTH_TOKEN`
  - [ ] `NODE_ENV=production`
  - [ ] `ADMIN_PASSWORD` (optionnel)

### Documentation
- [ ] README.md à jour
- [ ] DEPLOYMENT_VERCEL.md/NETLIFY à jour
- [ ] MAINTENANCE_UPDATE.md créé
- [ ] Logs de changements documentés

## 🚀 Pendant le déploiement

### Push vers Git
- [ ] Branche créée : `maintenance/update-dependencies-2024`
- [ ] Commits descriptifs et clairs
- [ ] Messages en français ou anglais (cohérent)
- [ ] Pas de merge conflicts
- [ ] PR créée (si workflow l'exige)

### Build Netlify
- [ ] Build déclenché automatiquement
- [ ] Logs de build sans erreurs
- [ ] Build time acceptable (~3-5 min)
- [ ] Deployment status : ✅ Success

### Tests immédiats
- [ ] Site accessible à l'URL de preview
- [ ] Pas de 500 errors
- [ ] API `/api/health` répond
- [ ] Admin panel `/admin` accessible

## ✔️ Après le déploiement

### Production
- [ ] Site accessible publiquement
- [ ] HTTPS fonctionnel
- [ ] Redirection `/` → home OK
- [ ] Menu de navigation complet

### Endpoints critiques
```bash
# À tester
✅ GET /api/health
✅ GET /api/admin/maintenance
✅ POST /api/contact (formulaire)
✅ GET /annuaire (si actif)
✅ GET /connexion (login)
```

### Performance
- [ ] Page load time < 3 secondes
- [ ] Pas d'erreurs console (F12)
- [ ] Images responsive
- [ ] Mobile-friendly (test sur téléphone)

### Monitoring
- [ ] Dashboard Netlify : vérifier les stats
- [ ] Logs d'erreurs : aucun pattern critique
- [ ] Rate limiting : fonctionnel
- [ ] Cache headers : corrects

## 🔄 Rollback (si nécessaire)

```bash
# Si problème détecté
git revert <commit-hash>
git push origin main

# Ou redéployer la version précédente depuis Netlify Dashboard
# → Deployments → Previous → Redeploy
```

## 📝 Rapport de déploiement

**À documenter après** :
- [ ] Heure de déploiement
- [ ] Version déployée
- [ ] Durée du build
- [ ] Issues rencontrées (0 = aucune)
- [ ] Performance metrics
- [ ] Signatures d'approbation

### Template de rapport
```
**Déploiement Production**
- Branche : maintenance/update-dependencies-2024
- Date : [DATE]
- Heure : [HEURE]
- Durée : [X min]
- Status : ✅ SUCCESS
- Tests : ✅ PASS
- Rollback : Non nécessaire
```

## 📞 Contacts et Escalade

**En cas de problème** :
1. Vérifier les logs Netlify
2. Vérifier la connectivité Turso
3. Rollback si critique
4. Contacter : [EMAIL_SUPPORT]

---

**Version** : 1.0  
**Dernière maj** : Juin 2024  
**Responsable** : DevOps Team ONPS