# Rota Financeira

Painel financeiro pessoal e compartilhado (Diego &amp; Luiza) — orçamento fixo, dívidas, plano de recuperação (notebook → job → dívida → reserva), lançamentos e investimentos.

Site estático (`index.html` + `config.js`), sem build. Dados no Supabase. Login por link mágico (sem senha).

## Publicar no GitHub Pages

1. No GitHub Desktop: **Publish repository** (o botão já aparece na tela inicial).
2. No site do GitHub, no repositório: **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: main / (root)** → Save.
3. Em 1–2 minutos o site fica disponível em `https://<seu-usuario>.github.io/<nome-do-repo>/`.

## Depois de publicar — 2 ajustes no Supabase (obrigatórios)

Projeto: `studiopicabstratofilms's Project` (supabase.com/dashboard).

1. **Authentication → URL Configuration**: defina o **Site URL** e adicione a URL do GitHub Pages (do passo acima) em **Redirect URLs**. Sem isso o link mágico do e-mail não redireciona de volta pro painel.
2. **Table Editor → allowed_users**: adicione uma linha com o e-mail da Luiza (o de Diego já está cadastrado). Só e-mails nessa tabela conseguem ver/editar os dados — qualquer outra pessoa que abrir o link recebe o painel vazio/bloqueado mesmo entrando com link mágico.

## Estrutura de dados (Supabase, schema `public`)

- `fixed_items` — orçamento fixo mensal (nome, responsável, categoria, valor, pago)
- `extras` — gastos variáveis do dia a dia
- `plan_stages` — as 4 etapas do plano (notebook, job, dívida negativada, reserva)
- `ledger` — lançamentos gerais de entrada/saída
- `investments` — carteira de investimentos
- `meta_config` — meta da reserva e dia do recebimento
- `allowed_users` — e-mails com acesso liberado (protegido por RLS)

Tudo protegido por Row Level Security: só quem faz login com um e-mail presente em `allowed_users` lê ou grava.
