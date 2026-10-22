# Monte das Cortes · logo reveal para web (SVG + GSAP)

Esta é a animação do logo em código, não em vídeo:
- **fundo transparente**;
- **nítida em qualquer tamanho**;
- **funciona em todos os browsers**, incluindo o Safari no iPhone e no Mac.

O movimento é igual ao dos vídeos aprovados.

**Peso total:** cerca de 45 KB comprimidos (gzip), já com o GSAP incluído.

Para ver a animação a funcionar, abre `exemplo.html` no browser, com duplo clique. Mostra as 8 versões.

## Ficheiros

| Ficheiro | O que é |
|---|---|
| `montecortes-reveal.js` | A animação: o logo, os traços e a coreografia (~32 KB, 13 KB comprimido) |
| `vendor/gsap.min.js` | GSAP 3.14.2, o motor de animação (gratuito, uso comercial incluído) |
| `vendor/DrawSVGPlugin.min.js` | Plugin do GSAP para desenhar as volutas e o "cortes" |
| `vendor/CustomEase.min.js` | Plugin do GSAP para a curva da meia volta |
| `exemplo.html` | Página de demonstração com as 8 versões |

## Como pôr no site

1. Copia a pasta para o site (por exemplo, para `/assets/montecortes/`).
2. Coloca o logo onde quiseres, dentro de um elemento com a largura pretendida:

```html
<div style="max-width: 640px">
  <div data-montecortes-reveal data-layout="full" data-tone="color" data-spin="180"></div>
</div>
```

3. Antes de `</body>`, carrega os scripts por esta ordem:

```html
<script src="/assets/montecortes/vendor/gsap.min.js"></script>
<script src="/assets/montecortes/vendor/DrawSVGPlugin.min.js"></script>
<script src="/assets/montecortes/vendor/CustomEase.min.js"></script>
<script src="/assets/montecortes/montecortes-reveal.js"></script>
```

Não é preciso mais nada: cada elemento com `data-montecortes-reveal` arranca sozinho.

> **Se o site já usa GSAP**, não carregues o `gsap.min.js` uma segunda vez. Basta acrescentar os dois plugins e o `montecortes-reveal.js`.
>
> **Em alternativa à pasta `vendor/`**, podes usar o CDN do GSAP:
> `https://cdn.jsdelivr.net/npm/gsap@3.14.2/dist/gsap.min.js`, `.../DrawSVGPlugin.min.js` e `.../CustomEase.min.js`

## Opções

As opções são atributos `data-*` do elemento:

| Atributo | Valores | Por defeito |
|---|---|---|
| `data-layout` | `full` (ícone + texto) · `icon` (só o ícone) | `full` |
| `data-tone` | `color` (azuis da marca) · `white` (branco, para fundos escuros ou imagens) | `color` |
| `data-spin` | `180` (meia volta do ícone) · `0` (sem volta) | `180` |
| `data-trigger` | `view` (começa quando aparece no ecrã) · `load` (ao abrir a página) · `manual` | `view` |
| `data-delay` | segundos de espera antes de começar, por exemplo `0.5` | `0` |
| `data-label` | texto alternativo para leitores de ecrã | `Monte das Cortes` |

**Tamanho:** o logo ocupa 100% da largura do elemento onde está. A altura acompanha automaticamente:
- na versão completa, a proporção é de cerca de 4:1;
- na versão só com o ícone, é quase quadrada.

Para mudar o tamanho, muda a largura desse elemento.

## Controlo por JavaScript (opcional)

```js
// criar à mão (em vez dos atributos data-*)
var logo = MonteCortesReveal.create(document.querySelector("#logo"), {
  layout: "full", tone: "white", spin: 0, trigger: "manual"
});

logo.play();     // começa (respeita o delay)
logo.restart();  // repete do início
logo.finish();   // salta para o logo final, sem animação
logo.destroy();  // remove
```

Se o elemento já tiver arrancado sozinho, a instância está em `elemento.__mcReveal`, por exemplo `elemento.__mcReveal.restart()`.

## Notas

- **Acessibilidade:** quem tem "reduzir movimento" ligado no sistema vê logo o logo final, sem animação. O SVG tem `role="img"` e um texto alternativo.
- **Margens:** no início, o ícone aparece ao centro e um pouco maior, e durante a meia volta passa ligeiramente fora da caixa do logo.
  - O SVG está com `overflow: visible`, por isso não é cortado.
  - Se o elemento-pai tiver `overflow: hidden`, convém deixar uma pequena margem à volta, cerca de 10% da altura.
- **Várias instâncias:** podes pôr vários logos na mesma página; cada um é independente.
- **WordPress, Webflow, Shopify, etc.:**
  1. Carrega os 4 ficheiros `.js` como recursos do tema.
  2. Cola o `<div data-montecortes-reveal ...>` num bloco de HTML.
- **Duração:**
  - completo com meia volta: ~3,8 s;
  - completo sem volta: ~3,3 s;
  - só o ícone: o movimento principal acaba aos ~2,5 s, mas o ícone ainda se aproxima muito ligeiramente até aos 3,3 s.

  No fim, o logo fica parado na versão exata da marca.
