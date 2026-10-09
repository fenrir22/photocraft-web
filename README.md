# photocraft-web builder

Questo repo non contiene il codice di PhotoCraft: la GitHub Action fa checkout di `storytold/photocraft@main` e ne builda il `Dockerfile` (web statico + nginx su porta 8080), poi pusha su GHCR.

## Uso

1. Crea un repo vuoto su GitHub (es. `tuo-user/photocraft-web-builder`) e pusha questa cartella:
   ```bash
   cd "C:\Users\alfio\Downloads\321"
   git init -b main
   git add .
   git commit -m "builder photocraft-web"
   git remote add origin https://github.com/TUO-USER/TUO-REPO.git
   git push -u origin main
   ```
2. Su GitHub vai su `Actions > build-photocraft-web > Run workflow` (parte anche da sola al push).
3. La prima build dura 10-20 min (Rust + Trunk, amd64+arm64).
4. Rendi pubblico il package: `Profilo > Packages > photocraft-web > Settings > Change visibility > Public`, altrimenti CasaOS non lo pulla.
5. Immagine prodotta: `ghcr.io/TUO-USER/photocraft-web:latest` (owner sempre minuscolo).

## CasaOS

Custom Install con questa immagine:

```yaml
name: photocraft
services:
  photocraft-web:
    image: ghcr.io/TUO-USER/photocraft-web:latest
    restart: unless-stopped
    ports:
      - "8090:8080"
```
