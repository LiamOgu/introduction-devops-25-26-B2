# 🎬 Démo TruffleHog - Étapes Simples

## 🎯 Objectif
Faire échouer le workflow GitHub Actions en pushant des secrets exposés.

## 📝 Étapes pour Tester

### 1️⃣ Vérifier les fichiers
```bash
ls test-secrets.*
# Vous devriez voir : test-secrets.js et test-secrets.py
```

### 2️⃣ Ajouter les fichiers au commit
```bash
git add test-secrets.js test-secrets.py .env.test
git add config-secrets.json config-secrets.yaml
git add Dockerfile.test
```

### 3️⃣ Commiter
```bash
git commit -m "test: ajouter fichiers avec secrets pour tester TruffleHog"
```

### 4️⃣ Pusher sur GitHub
```bash
git push origin main
# ou : git push origin master
```

### 5️⃣ Voir les résultats
1. Allez sur GitHub → votre repo
2. Cliquez sur l'onglet **"Actions"**
3. Vous verrez le workflow **"TruffleHog Secret Scanning"**
4. ❌ Le workflow devrait **ÉCHOUER** ❌
5. Cliquez dessus pour voir les secrets détectés

## 📊 Ce que vous verrez

Le workflow va détecter environ **100+ secrets** :
- ⚠️ Clés AWS (AKIAIOSFODNN7EXAMPLE)
- ⚠️ Clés Stripe (sk_live_...)
- ⚠️ Tokens GitHub (ghp_...)
- ⚠️ Clés API Google (AIzaSy...)
- ⚠️ Passwords en clair
- ⚠️ Et bien d'autres...

## 🚨 Résultat Attendu

```
❌ TruffleHog Secret Scanning - FAILED
Found verified result 🐷🔑
Detector Type: AWS
File: test-secrets.js
Line: 17
Secret: AKIAIOSFODNN7EXAMPLE
...
```

## 🧪 Test Local (optionnel)

Avant de push, testez en local :
```bash
./run-trufflehog.sh
```

## ✅ C'est tout !

Maintenant vous savez comment TruffleHog détecte les secrets !

**En production** : Ne JAMAIS commiter de secrets comme ça ! 🔐
