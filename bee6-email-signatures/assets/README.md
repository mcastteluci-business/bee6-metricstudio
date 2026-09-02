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
| `fotos/arthur-rodrigues.jpg` | Arthur | 164×164, recortada quadrada, 6,2 KB | ✅ no GCS |
| `fotos/luciano-monaco.jpg` | Luciano | 164×164, recortada quadrada, 5,1 KB | ✅ no GCS |
| `fotos/marcio-botelho.jpg` | Márcio | 164×164, recortada quadrada, 5,1 KB | ✅ no GCS |

As três estão prontas em `assets/fotos/`. Sobem para o bucket bee6, não para o GitHub:

```
gcloud storage cp assets/fotos/*.jpg gs://commom-files/fotos-socios/assinatura/
```

### Por que não usar o original da câmera

Os arquivos crus em `gs://commom-files/fotos-socios/` (`arthur-rodrigues.jpg`, `luciano-monaco.jpg`)
são 4000×3000 e pesam 3–4 MB, com `EXIF Orientation = 6` (retrato girado 90°). Colocados direto
num `<img width="82" height="82">` o rosto sai **achatado**, porque o atributo força o quadrado
sobre uma imagem 4:3. Recorte quadrado tem que vir do arquivo — `object-fit:cover` não é
confiável em cliente de e-mail (Outlook usa o motor do Word e ignora).

Repo de assets: `mcastteluci-business/bee6-metricstudio` (branch `main`).

## URLs aplicadas nos snippets

```
Logo:   https://raw.githubusercontent.com/mcastteluci-business/bee6-metricstudio/main/logo%20bee6.png
Mari:   https://raw.githubusercontent.com/mcastteluci-business/bee6-metricstudio/main/mari.png
Demais: https://raw.githubusercontent.com/mcastteluci-business/bee6-metricstudio/main/<nome>.png
```

## Checklist

- [x] Fotos de Arthur, Luciano e Márcio no bucket `commom-files/fotos-socios/assinatura` (164×164, quadradas, < 7 KB)
- [x] URLs públicas HTTPS (logo e Mari em `raw`, fotos dos sócios no GCS)
- [ ] Testar em Gmail (web + app) e Outlook antes de padronizar
