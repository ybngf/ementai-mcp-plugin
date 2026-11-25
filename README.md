# EmentAI

Cursor / Grok Bot plugin for the [EmentAI](https://ementai.com.br) remote MCP server: Brazilian case-law, qualified precedents, súmulas and statutes, with official source citations.

This repository is the **marketplace plugin package only**. It points at the hosted server at `https://ementai.com.br/mcp`. It does not include server source code or any secrets.

EmentAI is already listed in the Claude connector directory: [claude.ai/directory/ementai](https://claude.ai/directory/ementai).

## What it does

Large language models often invent plausible-looking citations. EmentAI lets an assistant search a real Brazilian legal corpus and return the text plus the official source link, so you can check every result.

The hosted server covers:

- Court decisions from superior courts (STF, STJ, TST), all 27 state courts of justice, federal, electoral, military and audit bodies (including TCU and CARF)
- Súmulas, including cancelled ones, with their current status
- Qualified STJ precedents (repetitive themes, IAC, controversies, SIRDR, PUIL)
- Federal legislation by article, plus state legislation, with revoked provisions marked

EmentAI is a research tool, not legal advice. It is an independent service and is not affiliated with the courts or bodies whose data it indexes. Always check the official source of each result.

## Tools

| Tool | What it does |
| --- | --- |
| `pesquisar_jurisprudencia` | Hybrid text + semantic search over real court decisions (process, rapporteur, date, court, authority level, official link). Uses 1 search credit. |
| `pesquisar_precedentes` | Qualified STJ precedents (themes, IAC, and related types), with the legal question, thesis and status. Uses 1 search credit. |
| `pesquisar_sumulas` | STJ and TCU súmulas, including cancelled ones, with status and the official link. Does not use a search credit. |
| `pesquisar_legislacao` | Federal and state statutes by topic or citation (for example `art. 927 do CPC`). Uses 1 search credit. |
| `obter_decisao` | Full available text of a decision by id (long texts come in parts). Does not use a search credit. |
| `obter_norma` | Summary or article text of a federal or state statute. Does not use a search credit. |
| `verificar_citacao` | Checks whether a cited decision, súmula, theme or article exists and whether rapporteur, date and thesis match. Decisions and themes use 1 search credit; súmulas and articles do not. |
| `conferir_peca` | Reviews citations in a petition, appeal or opinion (up to 30 citations per call). Uses 1 search credit if decisions or themes are checked. |
| `consultar_processo` | Looks up a CNJ case number in public DataJud (existence, class, movements; no parties or full judgment text). Does not use a search credit. |
| `listar_tribunais` | Shows current database coverage by court and statute type. Does not use a search credit. |
| `meu_consumo` | Shows the signed-in plan and remaining monthly search quota. Does not use a search credit. |
| `search` / `fetch` | Generic search plus fetch-by-id, for clients that expect that pair. `search` uses 1 search credit; `fetch` does not. |

## How to connect

The server is remote **Streamable HTTP** at:

```text
https://ementai.com.br/mcp
```

Authentication is **OAuth 2.0** (authorization code + PKCE, with dynamic client registration). Cursor starts the sign-in in the browser when you enable the plugin. You can also sign in with an API key from your EmentAI account; do not put a key in this repository or in `mcp.json`.

### From this plugin (Cursor)

1. Install the plugin from the Cursor Marketplace, or copy this folder to `~/.cursor/plugins/local/ementai` and reload the window.
2. Open Customize and enable the EmentAI MCP server.
3. Complete the OAuth sign-in in the browser (create a free account if you do not have one).
4. Ask, for example: “Qual a tese do Tema 1016 do STJ?”

Connection guide: [ementai.com.br/conectar](https://ementai.com.br/conectar)

### Manual `mcp.json` (any Cursor workspace)

```json
{
  "mcpServers": {
    "ementai": {
      "url": "https://ementai.com.br/mcp"
    }
  }
}
```

### Account and plans

Self-signup is open at [ementai.com.br/assinar](https://ementai.com.br/assinar). You confirm the account through an email link. The **Free** plan is 10 searches per month and does not require a credit card. Paid plans are listed on the site. Sign-in is a one-time email link (no password) at [ementai.com.br/entrar](https://ementai.com.br/entrar).

## Privacy and terms

- Privacy policy: [https://ementai.com.br/privacidade](https://ementai.com.br/privacidade)
- Terms of use: [https://ementai.com.br/termos](https://ementai.com.br/termos)

The site states that the text of your queries is not stored; only daily usage counts are kept for quota.

## License

This plugin package is licensed under the [MIT License](LICENSE). Copyright 2026 BNGF Tecnologia e Soluções Digitais LTDA.

---

## Português

O EmentAI é um servidor MCP de busca de jurisprudência brasileira. A IA consulta decisões, súmulas, precedentes qualificados e leis que existem de fato, com o link da fonte oficial em cada resultado, em vez de inventar ementas.

Este repositório é só o **pacote do plugin** para o Cursor Marketplace e o Grok Bot. Ele aponta para o servidor hospedado em `https://ementai.com.br/mcp`. O código do servidor e qualquer segredo ficam de fora.

Já está no diretório de conectores do Claude: [claude.ai/directory/ementai](https://claude.ai/directory/ementai).

### Como conectar

1. Instale o plugin no Cursor Marketplace ou copie esta pasta para `~/.cursor/plugins/local/ementai` e recarregue a janela.
2. Em Customize, ative o servidor MCP EmentAI.
3. Conclua o login OAuth no navegador (crie uma conta gratuita em [ementai.com.br/assinar](https://ementai.com.br/assinar) se ainda não tiver; o plano gratuito é de 10 pesquisas por mês, sem cartão).
4. Pergunte, por exemplo: “Qual a tese do Tema 1016 do STJ?”

Guia: [ementai.com.br/conectar](https://ementai.com.br/conectar)

O transporte é Streamable HTTP. A autenticação é OAuth (o Cursor registra o cliente sozinho). Também é possível usar uma chave de API da sua conta; não coloque chave neste repositório.

### Privacidade e termos

- Política de privacidade: [https://ementai.com.br/privacidade](https://ementai.com.br/privacidade)
- Termos de uso: [https://ementai.com.br/termos](https://ementai.com.br/termos)

O EmentAI é uma ferramenta de pesquisa e não presta aconselhamento jurídico. Confira sempre a fonte oficial.

