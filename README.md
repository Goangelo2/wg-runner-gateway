# WireGuard Gateway sur GitHub Actions Runner

Ce dépôt permet de transformer un runner GitHub Actions en passerelle WireGuard,
avec génération automatique du QR code et téléversement de la configuration en artefact.

## 🚀 Utilisation

1. Onglet **Actions** → workflow **WireGuard Gateway (Runner)** → **Run workflow**.
2. Renseignez :
   - `endpoint_host` : IP publique / domaine à mettre dans le client (défaut `127.0.0.1`).
   - `listen_port` : port UDP (défaut `51820`).
   - `job_duration_minutes` : durée de maintien (défaut `300`, max `350`).
3. Lancez le workflow.
4. Deux façons de récupérer la config :
   - **Scannez le QR code** affiché dans les logs de l'étape *Afficher le QR code*.
   - **Téléchargez** l'artefact `wireguard-client-config` depuis le résumé du job.

## ⚠️ Limites

- Le runner GitHub est **derrière un NAT** : `endpoint_host` doit pointer vers une adresse
  réellement joignable depuis le téléphone. Sinon, le tunnel ne pourra pas s'établir.
- Pour un accès réel depuis un téléphone, utilisez **Tailscale** (exit node) ou une
  technique de **NAT traversal** (ex. projet `yomaser`).
- Le tunnel s'arrête à la fin du job (max 6 h).
- La configuration contient la **clé privée du client** : supprimez l'exécution après usage
  si le dépôt est public.

## 🔐 Sécurité

- Ne committez **jamais** `wg-config/` (déjà dans `.gitignore`).
- Supprimez les runs après usage si le dépôt est public.
