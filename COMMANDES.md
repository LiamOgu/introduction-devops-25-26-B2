# 🚀 Commandes Rapides - TruffleHog

## Pour Tester avec GitHub Actions (le plus simple)

```bash
# 1. Ajouter les fichiers avec secrets
git add test-secrets.js test-secrets.py .env.test config-secrets.json

# 2. Commiter
git commit -m "test: secrets exposés pour TruffleHog"

# 3. Pusher
git push

# 4. Aller sur GitHub → onglet Actions → voir l'erreur ! ❌
```

## Test Local

```bash
# Option 1 : Script automatique
./run-trufflehog.sh

# Option 2 : Avec Docker
docker run --rm -v "$(pwd):/repo" trufflesecurity/trufflehog:latest filesystem /repo
```

## C'est tout ! 🎉

Les secrets seront détectés et le workflow échouera.
