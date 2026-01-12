# 🔍 Test TruffleHog - Détection de Secrets

Ce projet contient des fichiers de test pour vérifier que TruffleHog détecte correctement les secrets exposés.

## ⚠️ ATTENTION

**Tous les secrets dans ce projet sont FAUX et uniquement à des fins de test !**

Ne jamais commiter de vrais secrets dans le code source.

## 🚀 Utilisation Rapide

### Méthode 1 : Script automatique (recommandé)

```bash
chmod +x run-trufflehog.sh
./run-trufflehog.sh
```

Le script installe TruffleHog et scanne automatiquement tous les fichiers de test.

### Méthode 2 : Commande manuelle

```bash
# Installer TruffleHog (Linux)
wget https://github.com/trufflesecurity/trufflehog/releases/latest/download/trufflehog_linux_amd64.tar.gz
tar -xzf trufflehog_linux_amd64.tar.gz
sudo mv trufflehog /usr/local/bin/

# Scanner les fichiers
trufflehog filesystem . --no-update
```

### Méthode 3 : Avec Docker

```bash
docker run --rm -v "$(pwd):/repo" trufflesecurity/trufflehog:latest \
  filesystem /repo --no-update
```

## 📁 Fichiers de Test

- `test-secrets.js` - Secrets en JavaScript
- `test-secrets.py` - Secrets en Python  
- `.env.test` - Variables d'environnement
- `config-secrets.yaml` - Configuration YAML
- `config-secrets.json` - Configuration JSON
- `Dockerfile.test` - Dockerfile avec secrets

**Total : ~100+ secrets à détecter**

## 🔄 GitHub Actions

Lorsque vous push du code, GitHub Actions exécute automatiquement TruffleHog.

Le workflow se trouve dans : `.github/workflows/trufflehog.yml`

### Ce qui se passe :

1. ✅ Vous push du code sur GitHub
2. 🔍 TruffleHog scanne automatiquement
3. ❌ Si des secrets sont détectés → le workflow échoue
4. 📊 Vous voyez les erreurs dans l'onglet "Actions" de GitHub

### Tester le workflow :

```bash
git add test-secrets.js
git commit -m "test: ajouter fichier avec secrets"
git push
```

Puis allez dans l'onglet **Actions** de votre repo GitHub pour voir les résultats !

## 📊 Résultats Attendus

TruffleHog devrait détecter :

- 🔑 Mots de passe (PostgreSQL, MongoDB, Redis)
- 🌐 Clés API (AWS, Stripe, GitHub, Google, OpenAI)
- 🔐 Tokens (JWT, OAuth, Bearer)
- 🗝️ Clés privées SSH/RSA
- 🔗 Connection strings
- 📧 Credentials SMTP
- ☁️ Secrets cloud (AWS, GCP, Azure)

## ✅ Bonnes Pratiques

### ❌ À NE JAMAIS FAIRE (comme dans ces fichiers de test) :

```javascript
// ❌ Hardcoder des secrets
const password = "SuperSecretPass123!";
const apiKey = "sk_live_1234567890abcdef";

// ❌ Secrets dans les URLs
const db = "mongodb://admin:password@localhost";

// ❌ Commiter des fichiers .env
```

### ✅ À TOUJOURS FAIRE :

```javascript
// ✅ Utiliser les variables d'environnement
const password = process.env.DB_PASSWORD;
const apiKey = process.env.STRIPE_SECRET_KEY;

// ✅ Ajouter .env au .gitignore
// ✅ Utiliser des gestionnaires de secrets (Vault, AWS Secrets Manager)
// ✅ Scanner le code avec TruffleHog avant chaque commit
```

## 🧹 Nettoyage

Pour supprimer les fichiers de test :

```bash
rm -f test-secrets.* .env.test config-secrets.* Dockerfile.test
rm -f run-trufflehog.sh TRUFFLEHOG-TEST-README.md QUICK-START.md
rm -rf trufflehog-results/
```

## 📚 Documentation

- [TruffleHog GitHub](https://github.com/trufflesecurity/trufflehog)
- [Documentation complète](TRUFFLEHOG-TEST-README.md)
- [Guide rapide](QUICK-START.md)

## 🎯 Objectif

Comprendre comment TruffleHog détecte les secrets exposés et éviter de commiter des vrais secrets en production !

---

**Made for DevOps testing** 🚀
