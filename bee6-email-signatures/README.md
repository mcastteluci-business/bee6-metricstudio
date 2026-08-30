# Assinaturas de E-mail — Bee6

Padrão oficial de assinaturas de e-mail da Bee6, em **HTML** (não mais imagem única).
Serve tanto para **instalar a assinatura no Gmail** quanto como **fonte de verdade** para as ferramentas internas.

> **Owner:** Mari (New Business) · **Dev/handoff:** Arthur, Guilherme
> **Repo de assets:** `mcastteluci-business/bee6-metricstudio`

---

## Por que saímos da imagem única

A assinatura antiga era uma imagem única (`.png`). Isso prejudica e-mail — principalmente cold/prospecção:

- Clientes de e-mail **bloqueiam imagens por padrão** → o destinatário via um retângulo vazio.
- Imagem grande + banner é **padrão de e-mail de marketing** → pior pontuação nos filtros de spam.
- Texto dentro de imagem **não é clicável nem indexável** → e-mail e telefone ficavam inúteis.

A versão HTML resolve tudo: texto real, links reais, leve.

---

## As duas versões

| Versão | Quando usar | Contém |
|---|---|---|
| **Institucional** | E-mails quentes, respostas, interno, parceiros | Logo, foto, nome, cargo real, cargo-fantasia, contatos, tagline |
| **Cold / Prospecção** | **1º toque frio** (aquisição) | Só texto: nome, cargo, pitch, e-mail, telefone. Sem logo, sem foto, **sem link** |

**Regra de ouro do cold:** no primeiro contato, nada de imagem nem link (derrubam a entregabilidade). O link só entra a partir da resposta do lead (aí usa a Institucional).

---

## Estrutura

```
bee6-email-signatures/
├── README.md                     ← este documento
├── preview.html                  ← abre no navegador; mostra as 8 assinaturas
├── templates/
│   ├── institucional.html        ← {{PLACEHOLDERS}}
│   └── cold.html                 ← {{PLACEHOLDERS}}
├── signatures/                   ← snippets prontos (produção)
│   ├── mariana-castteluci.html   │   arthur-rodrigues.html
│   ├── luciano-monaco.html       │   marcio-botelho.html
│   └── cold/                     ← versões cold por pessoa
└── assets/
    └── README.md                 ← specs de logo/foto + hospedagem
```

---

## Design tokens (fonte de verdade)

| Token | Valor | Uso |
|---|---|---|
| Laranja da marca | `#ee8d49` | Cargo, filete, contorno, tagline, links |
| Texto principal | `#1A1A1A` | Nome |
| Texto secundário | `#333333` / `#666666` | Contatos / pitch |
| Fonte | `Arial, Helvetica, sans-serif` | Web/e-mail-safe (sem web fonts) |
| Foto | 82×82px, círculo | `border-radius:50%` |
| Largura | 474px | Institucional |
| **Telefone** | `+55 11 XXX XXX XXX` | País + DDD + grupos de 3 |

Tudo **inline** em cada snippet (CSS externo é ignorado por clientes de e-mail).

---

## Imagens hospedadas (GitHub) — atenção: `raw`, não `blob`

O link de página do GitHub (`github.com/.../blob/...`) **não funciona** como imagem em e-mail.
Use sempre o link **`raw`**:

```
Página (blob, NÃO usar):
https://github.com/mcastteluci-business/bee6-metricstudio/blob/main/logo%20bee6.png

Imagem (raw, USAR no <img src>):
https://raw.githubusercontent.com/mcastteluci-business/bee6-metricstudio/main/logo%20bee6.png
```
Regra: troque `github.com` por `raw.githubusercontent.com` e **remova o `/blob`**.

**Referência por branch `main` (auto-atualizável):** todos os snippets apontam para `.../main/<arquivo>`.
Assim, ao trocar a imagem no repo, a assinatura atualiza sozinha — sem editar os arquivos.

**Aplicados:**
- Logo: `.../main/logo%20bee6.png` ✅
- Foto Mari: `.../main/mari.png` ✅

**Faltam subir no repo (mesma branch `main`):**
- `arthur.png`, `luciano.png`, `marcio.png`

---

## Instalar no Gmail

1. Abra `signatures/<seu-slug>.html` no navegador → selecione tudo → copie.
2. Gmail → **Configurações → Ver todas → Geral → Assinatura** → cole.
3. Para prospecção, repita com `signatures/cold/<seu-slug>.html` (2ª assinatura).

---

## Adicionar um novo membro (replicável)

1. Duplique `templates/institucional.html` e `templates/cold.html`.
2. Substitua: `{{NOME}}`, `{{CARGO_REAL}}`, `{{FANTASIA_LINHA1}}`, `{{FANTASIA_LINHA2}}`, `{{EMAIL}}`, `{{TELEFONE}}`, `{{SITE_URL}}`, `{{SITE_LABEL}}`, `{{LOGO_URL}}`, `{{PHOTO_URL}}`, `{{PITCH_NICHO}}`.
3. Suba a foto no repo de assets (specs em `assets/README.md`) e use o link **raw**.
4. Salve como `signatures/<slug>.html` e `signatures/cold/<slug>.html`.

Telefone: `+55 11 XXX XXX XXX`. Slug: `nome-sobrenome` (minúsculo, sem acento).

---

## Equipe atual

| Pessoa | Cargo real | Cargo-fantasia | E-mail | Telefone | Foto |
|---|---|---|---|---|---|
| Mariana Càstteluci | New Business | Falcoeira do Digital * | mari@bee6.com.br | +55 11 981 930 415 | ✅ no repo |
| Arthur Rodrigues | Martech | Antigo Druida das Planilhas | arthur.rodrigues@bee6.com.br | +55 11 979 723 332 | ⬜ falta foto `arthur.png` (snippet pronto) |
| Luciano Monaco | New Business | Grande Mestre do Inbox | luciano.monaco@bee6.com.br | +55 11 969 281 962 | ⬜ falta foto `luciano.png` (snippet pronto) |
| Márcio Botelho | New Business | Dom Quixote do Digital | marcio.botelho@bee6.com.br | +55 11 946 150 398 | ⬜ falta foto `marcio.png` (snippet pronto) |

\* Trocado de "Andarilha do Digital" para **"Falcoeira do Digital"** (decisão da Mari). Reverter é só editar o snippet.

---

## Notas para os devs (Arthur / Guilherme)

- `signatures/` = HTML inline autocontido (embed direto ou referência de render).
- `templates/` usam `{{PLACEHOLDERS}}` → fáceis de plugar num gerador (por pessoa ou via API).
- **Não** usar `<style>` externo, classes, `<script>` ou web fonts (clientes de e-mail removem). Tudo inline.
- **Sem animação:** CSS/JS animation não roda em e-mail; único motion possível seria GIF (fora de escopo por entregabilidade).
- Imagens **sempre** via `raw.githubusercontent.com` (nunca `blob`).
- Acentos como entidades HTML (`&agrave;`, `&aacute;`) para máxima compatibilidade.
