# seurat-dora-reproducibility2

# Seurat v4 Reproducibility Environment

Questo repository contiene la configurazione Docker e le automazioni per la creazione di un ambiente di analisi bioinformatica riproducibile, basato su **Seurat v4** e **Jupyter**.

L'immagine Docker viene compilata e pubblicata automaticamente sul registro remoto **GitHub Container Registry (ghcr.io)** ad ogni aggiornamento della repository tramite **GitHub Actions**.

---

## 🛠️ Architettura dell'Ambiente

- **Ambiente di Base:** R 4.x con **Seurat v4.3.0** preinstallato (`satijalab/seurat:4.3.0`).
- **Python:** Python 3.11.11 compilato direttamente da sorgente in un percorso dedicato (`/home/python4Jup`).
- **Interfaccia:** JupyterHub / JupyterLab configurato con kernel per R (`IRkernel`) e Python.
- **Utente predefinito:** `jovyan` (ambiente non-root per sicurezza delle esecuzioni).

---

## 🚀 Workflow di Automazione (CI/CD)

Il file `.github/workflows/docker-build.yml` gestisce la pipeline automatica:
1. Intercetta i nuovi `push` sul branch principale (`main`).
2. Effettua l'autenticazione su **GitHub Container Registry** (`ghcr.io`).
3. Compila il `Dockerfile`.
4. Rilascia e aggiorna l'immagine finale con il tag `:latest`.

---

## 🖥️ Come eseguire il Container sul Server

Per scaricare ed eseguire l'immagine sul server di analisi, esegui i seguenti comandi da terminale:

### 1. Autenticazione a GitHub Packages
Crea un **Personal Access Token (PAT)** su GitHub con permessi `read:packages` ed esegui il login:

```bash
echo "IL_TUO_PERSONAL_ACCESS_TOKEN" | docker login ghcr.io -u nicolo-beltrami --password-stdin
