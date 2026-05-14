# scans-dashboard

Frontend estático servido em https://scans.anonshield.org/ — dashboard da
varredura DITector sobre Docker Hub.

## Arquitetura
- `index.html` + `dashboard.js` (Chart.js via CDN). Sem build step.
- Deploy: `scp` para `a9:/srv/scans-dashboard/` (Caddy serve).
- Dados vêm de `/api/v1/*` (FastAPI `scans-api` no gpu1, reverse-proxy
  pelo Caddy do a9).

## Atualizar
1. Editar `index.html` e `dashboard.js` localmente.
2. Commit + push.
3. Deploy manual: `scp index.html dashboard.js gpu1:/tmp/ && ssh gpu1 'scp /tmp/{index.html,dashboard.js} a9:/tmp && ssh a9 "sudo install -o caddy -g caddy -m 644 /tmp/index.html /tmp/dashboard.js /srv/scans-dashboard/"'`
