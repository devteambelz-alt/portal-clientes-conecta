# Deploy do frontend (Next.js) na Vercel

Este repositório é um monorepo com `backend/` e `frontend/`. O deploy será somente do diretório `frontend/` na Vercel.

## Pré‑requisitos

- Conta na Vercel ([https://vercel.com](https://vercel.com))
- Acesso ao repositório Git (GitHub, GitLab ou Bitbucket) ou Vercel CLI instalado localmente

## Passo a passo (Dashboard da Vercel)

1. Importar o repositório na Vercel (New Project → Import Git Repository).
2. Em Root Directory selecione `frontend` (isso é essencial em monorepos).
3. Framework Preset: Next.js (detectado automaticamente).
4. Node.js Version: 18.x ou 20.x (padrão da Vercel; o projeto suporta >=18.17).
5. Build & Output Settings (normalmente autoconfigurados):
   - Install Command: `npm install`
   - Build Command: `npm run build`
   - Output Directory: `.next`
6. Clique em Deploy.

Observações sobre fontes (next/font/google): o build local pode falhar sem internet (ex.: bloqueio a `fonts.googleapis.com`). Na Vercel isso funciona normalmente, pois a rede está disponível no build. Se preferir builds totalmente offline, considere migrar para `next/font/local` com fontes self‑hosted.

## Passo a passo (Vercel CLI)

Se preferir pela CLI, rode os comandos dentro do diretório `frontend/`:

```powershell
# Dentro do diretório frontend/
npm install -g vercel
vercel login
vercel               # primeira vez: cria o projeto e vincula
vercel --prod        # deploy de produção
```

Dicas:

- Garanta que está dentro de `frontend/` ao rodar `vercel` para que a raiz do projeto aponte para o app Next.
- Você também pode usar `vercel link` para vincular a pasta local a um projeto já existente.

## Scripts relevantes

- `npm run dev` – desenvolvimento local (Turbopack)
- `npm run build` – build de produção (sem Turbopack)
- `npm start` – servir build localmente

## Troubleshooting

- Erros de rede ao baixar fontes Google durante `npm run build` local: verifique conexão e DNS. Alternativa: realizar o build direto na Vercel ou migrar para `next/font/local`.
- Versão do Node: na Vercel ajuste para 18.x/20.x nas configurações do projeto se necessário.
