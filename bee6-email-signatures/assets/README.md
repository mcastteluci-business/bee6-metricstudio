# Assets — logo e fotos

Imagens das assinaturas **institucionais**. Precisam de URL pública HTTPS via **`raw.githubusercontent.com`**
(o link de página `github.com/.../blob/...` NÃO renderiza como imagem em e-mail).

## Converter blob → raw

```
blob (não usar): https://github.com/<user>/<repo>/blob/main/<arquivo>
raw  (usar):     https://raw.githubusercontent.com/<user>/<repo>/main/<arquivo>
```
Regra: troque `github.com` por `raw.githubusercontent.com` e **remova o `/blob`**.

## Por que branch `main` (e não commit fixo)

Os snippets referenciam `.../main/<arquivo>`. Assim, ao **trocar a imagem no repo**, a assinatura
atualiza sozinha — sem editar nenhum arquivo HTML. (Um commit fixo travaria a versão e exigiria
atualizar a URL a cada troca.)

## Arquivos

| Arquivo | Usado por | Specs | Status |
|---|---|---|---|
| `logo bee6.png` | Todas as institucionais | PNG, fundo transparente, exibe 30px → exportar 60px de altura (2×). < 30KB | ✅ hospedado |
| `mari.png` | Mariana | Quadrada, exibe 82px → exportar 164×164px (2×), rosto centralizado. < 50KB | ✅ hospedado |
| `arthur.png` | Arthur | idem | ⬜ subir |
| `luciano.png` | Luciano | idem | ⬜ subir |
| `marcio.png` | Márcio | idem | ⬜ subir |

Repo de assets: `mcastteluci-business/bee6-metricstudio` (branch `main`).

## URLs aplicadas nos snippets

```
Logo:   https://raw.githubusercontent.com/mcastteluci-business/bee6-metricstudio/main/logo%20bee6.png
Mari:   https://raw.githubusercontent.com/mcastteluci-business/bee6-metricstudio/main/mari.png
Demais: https://raw.githubusercontent.com/mcastteluci-business/bee6-metricstudio/main/<nome>.png
```

## Checklist

- [ ] Fotos de Arthur, Luciano e Márcio no repo, branch `main` (2×, otimizadas, quadradas)
- [ ] URLs no formato `raw`
- [ ] Testar em Gmail (web + app) e Outlook antes de padronizar
