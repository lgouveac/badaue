# Design System Extraido do Site Atual

Data da extracao: 2026-03-12
Origem observada: `https://alabadaue.com`
Objetivo: documentar a linguagem visual existente para orientar uma reconstrucao mais limpa, consistente e performatica.

## Essencia da marca

A linguagem da Badauê mistura:

- editorial cultural brasileiro
- portfolio criativo
- acervo/vitrine de talentos
- energia de revista independente
- contraste entre institucional serio e imagens com muito gingado

Nao e um site corporativo neutro. A forca esta em:

- curadoria visual
- tipografia com personalidade
- recortes fotograficos expressivos
- ritmo de galeria/magazine

## Tokens visuais observados

## Cores

Paleta percebida na interface atual:

- Preto base: `rgb(0, 0, 0)` / `#000000`
- Branco base: `rgb(255, 255, 255)` / `#FFFFFF`
- Vermelho de destaque: `rgb(255, 0, 0)` / `#FF0000`
- Vermelho escuro de apoio: `rgb(221, 0, 0)` / `#DD0000`
- Cinza texto/apoio: `rgb(34, 34, 34)` / `#222222`
- Cinza secundario: `rgb(102, 102, 102)` / `#666666`
- Azul institucional residual em paragrafos: `rgb(21, 41, 90)` / `#15295A`
- Fundo rodape: quase preto com vinho muito escuro

### Uso sugerido na reconstrução

- `--color-bg`: `#F7F4EF`
- `--color-surface`: `#FFFFFF`
- `--color-text`: `#111111`
- `--color-text-muted`: `#5E5A54`
- `--color-accent`: `#D61F12`
- `--color-accent-dark`: `#8E140C`
- `--color-footer`: `#140404`

Observacao:
o site atual usa vermelho puro em varios links. Na reconstrucao, vale manter o calor do acento sem depender de `#FF0000` em tudo.

## Tipografia

Fontes observadas:

- `Bricolage Grotesque` como principal da interface e headings
- `Lato` em blocos de texto corrido
- Google Fonts adicionais carregadas mas nem sempre necessarias: `Raleway`, `Nunito`, `Abril Fatface`, alem de pacotes gerados pelo Elementor

Estilos capturados:

- `body`: `12px`, `400`, `26px`, `Bricolage Grotesque`
- `h1`: `30px`, `700`, `37.5px`, `Bricolage Grotesque`
- `h2`: `20px`, `400`, `90px`, `Bricolage Grotesque`
- `h3`: `23px`, `500`, `25px`, `Bricolage Grotesque`
- `h5`: `16px`, `400`, `25px`, `Bricolage Grotesque`
- `p`: `14px`, `400`, `24.5px`, `Lato`

### Direcao recomendada

- manter `Bricolage Grotesque` nos titulos, navegacao e chamadas
- usar uma unica fonte de texto corrido
- eliminar familias nao usadas para cortar requests

### Escala sugerida

- Display: `clamp(2.75rem, 6vw, 5.5rem)`
- H1: `clamp(2rem, 4.5vw, 3.5rem)`
- H2: `clamp(1.5rem, 3vw, 2.25rem)`
- H3: `clamp(1.125rem, 2vw, 1.5rem)`
- Body: `1rem`
- Small: `0.875rem`

## Espacamento e ritmo

O site atual trabalha com muito branco visual, mas de forma irregular. Para a nova versao, vale sistematizar:

- `4`
- `8`
- `12`
- `16`
- `24`
- `32`
- `48`
- `64`
- `96`

Uso esperado:

- cards: `16` a `24`
- secoes: `64` a `96`
- gaps de grid: `16` a `24`
- respiros de hero/editorial: `32` a `48`

## Bordas e forma

Linguagem observada:

- cards com cantos arredondados
- imagens com clipping suave
- botoes discretos
- pouca ornamentacao geometrica fora das imagens

Tokens sugeridos:

- `--radius-sm`: `10px`
- `--radius-md`: `18px`
- `--radius-lg`: `28px`
- `--radius-pill`: `999px`

## Iconografia

Uso atual:

- icones sociais pequenos e monocromaticos
- WhatsApp flutuante chamativo
- excesso de bibliotecas de icones herdadas do tema/plugins

Direcao:

- manter iconografia monocromatica e simples
- usar um set unico de icones
- evitar packs legados do tema

## Componentes recorrentes

### 1. Header editorial

Partes:

- assinatura textual curta da marca
- logo forte no centro
- links sociais
- menu horizontal

Papel:
- posicionamento da marca como midia + agencia criativa

### 2. Hero com destaque rotativo

Partes:

- imagem grande
- chamada curta
- CTA embutido
- slider/paginacao

Problema atual:
- depende de carrossel pesado

Direcao nova:
- manter 1 destaque principal e 2 secundarios, sem slider obrigatorio

### 3. Grid curado de cards

Partes:

- tabs de categoria
- cards de tamanhos parecidos
- imagens fortes
- misto de portfolio, artigo e perfil

Papel:
- principal assinatura visual do site

Direcao:
- transformar em sistema de cards unificado
- variar pelo conteudo, nao pela tecnologia do widget

### 4. Bloco de impacto/metricas

Partes:

- manifesto curto
- numeros de comunidade/projetos/conteudos

Problema atual:
- indicadores aparecem zerados

Direcao:
- ou conectar numeros reais
- ou trocar por prova social qualitativa

### 5. Faixa de logos/parceiros

Partes:

- logos de marcas e parceiros
- leitura horizontal

Direcao:
- reduzir animacao
- priorizar legibilidade e curadoria

### 6. Footer institucional

Partes:

- manifesto institucional
- links utilitarios
- contato
- politicas

Direcao:
- reorganizar por blocos claros
- melhorar leitura mobile

## Sistema de cards recomendado

Para a reconstrucao, eu usaria apenas 4 variacoes:

- `CardFeature`: destaque grande, imagem dominante, titulo e CTA
- `CardStory`: artigo/editorial com imagem e categoria
- `CardCase`: projeto/marca com capa, tipo de servico e segmento
- `CardProfile`: artista com retrato, nome e disciplina

Cada card deve compartilhar:

- raio consistente
- overlay/legenda consistente
- comportamento de hover consistente
- proporcoes previsiveis por breakpoint

## Sistema de pagina recomendado

### Templates macro

- Home portal
- Hub de conteudo
- Hub de projetos/marcas
- Banco de artistas
- Pagina de produto/relatorio
- Pagina institucional/formulario

### Zonas de layout

- topo fixo ou semi-fixo
- hero
- grade principal
- modulo de prova social
- CTA final
- rodape

## Regras de UX para a nova versao

- mobile-first de verdade
- menos sliders, mais narrativa fixa
- menos plugins, mais componentes
- 1 CTA dominante por secao
- sem misturar loja, CRM e portfolio na mesma camada sem hierarquia
- headings semanticamente corretos

## O que preservar

- Bricolage Grotesque como gesto principal da marca
- protagonismo da imagem
- curadoria brasileira como espinha dorsal
- contraste preto/vermelho/branco
- clima de revista/plataforma cultural

## O que simplificar

- numero de fontes
- numero de plugins e bibliotecas
- excesso de tabs e sliders
- excesso de tipos de card
- excesso de tracking na primeira dobra
