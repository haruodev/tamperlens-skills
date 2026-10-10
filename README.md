# Tamperlens skills

Agent skills for [Tamperlens](https://tamperlens.com), the document trust API. They teach a
coding agent (Claude Code, Codex, Cursor, Gemini CLI and the others the
[`skills` CLI](https://github.com/vercel-labs/skills) supports) when to check a document
and how to call the API without pulling untrusted text into its own context.

| Skill | What it does |
|---|---|
| `tamperlens-document-check` | Checks a PDF, Office file or photo for signs it was changed after it was created, and reports the signals without a fake or genuine verdict. |
| `tamperlens-compare-pdfs` | Compares a PDF against the original you hold: identical, original plus appended revisions, or rewritten. |
| `tamperlens-prompt-injection-check` | Screens a PDF or Office file for text addressed to a language model before the agent reads it, with that text withheld. |

## Install

```bash
npx skills add haruodev/tamperlens-skills
```

One skill only:

```bash
npx skills add haruodev/tamperlens-skills --skill tamperlens-document-check
```

## API key

`tamperlens-document-check` and `tamperlens-prompt-injection-check` run without a key on
the anonymous allowance (10 documents an hour). `tamperlens-compare-pdfs` needs one. A free
key covers 50 documents a month with no card: create it at
[tamperlens.com/account](https://tamperlens.com/account) and set it in your shell profile or
your agent's environment settings:

```bash
export TAMPERLENS_API_KEY=tl_...
```

The skills read the key from that variable and tell the agent never to print it or ask for
it in the chat. Do not put it in a file you commit.

## What leaves your machine

Each check uploads the file you name to `https://tamperlens.com` over HTTPS. Files are
parsed in memory and not stored; the only record kept is a usage row that holds no part of
the document. Details: [tamperlens.com/security](https://tamperlens.com/security).

## Requirements

`curl`, `jq` and network access to `tamperlens.com`. If the
[`tamperlens-mcp`](https://www.npmjs.com/package/tamperlens-mcp) server is connected to
your agent, the skills use its tools instead of `curl`.

## Links

[API reference](https://tamperlens.com/api-reference) ·
[Field guide to every signal](https://tamperlens.com/pdf-fraud-signals) ·
[What Tamperlens measures and what defeats it](https://tamperlens.com/evidence) ·
[Pricing](https://tamperlens.com/pricing)

MIT licensed.
