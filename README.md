# Rota Financeira

Painel financeiro pessoal e compartilhado (Diego &amp; Luiza) — orçamento fixo, dívidas, plano de recuperação (notebook → job → dívida → reserva), lançamentos e investimentos.

Site estático (`index.html` + `config.js`), sem build. Dados no Supabase. Acesso direto pelo link — sem login.

## Publicar no GitHub Pages

1. No GitHub Desktop: **Publish repository** (o botão já aparece na tela inicial), ou **Commit** + **Push** se o repositório já estiver publicado.
2. No site do GitHub, no repositório: **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: main / (root)** → Save.
3. Em 1–2 minutos o site fica disponível em `https://<seu-usuario>.github.io/<nome-do-repo>/`.

## Publicar na Vercel (alternativa/complemento)

1. Em vercel.com, **Add New → Project** e importe o repositório `rota-financeira` do GitHub.
2. Framework: **Other** (site estático, sem build). Root Directory: `/`. Build Command e Output Directory podem ficar em branco.
3. Deploy. A Vercel gera uma URL própria (`https://rota-financeira-xxxx.vercel.app`), que também pode ser usada direto — sem login.

## Estrutura de dados (Supabase, schema `public`)

- `fixed_items` — orçamento fixo mensal (nome, responsável, categoria, valor, pago)
- `extras` — gastos variáveis do dia a dia
- `plan_stages` — as 4 etapas do plano (notebook, job, dívida negativada, reserva)
- `ledger` — lançamentos gerais de entrada/saída
- `investments` — carteira de investimentos
- `meta_config` — meta da reserva e dia do recebimento

O acesso é aberto por design (chave anon pública do Supabase + RLS permitindo leitura/escrita): quem tiver o link do site enxerga e edita os dados. Não há autenticação — a segurança aqui é não divulgar o link/URL do site para mais ninguém.
