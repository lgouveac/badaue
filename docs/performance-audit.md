# Auditoria de Performance e Carregamento

Data da analise: 2026-03-12
Dominio funcional: `https://alabadaue.com`
Observacao critica: `https://www.alabadaue.com` nao resolve no teste atual, entao existe um problema de entrada/canonicalizacao logo no acesso inicial.

## Resumo executivo

A home carrega e renderiza, mas a experiencia ja nasce com sinais de excesso de complexidade tecnica:

- `domContentLoaded`: ~`2.7s`
- `loadEventEnd`: ~`3.5s`
- `243` requests de recurso na home
- `116` imagens mapeadas
- `41` imagens sem `loading="lazy"`
- `37` imagens sem `width` e/ou `height`
- `32.3 MB` de corpo codificado somado pelos recursos observados no navegador
- `89` requests iniciados por `link` e `76` por `script`

Em termos praticos: o site nao parece travar por um unico arquivo gigante, e sim por uma pilha grande de plugins, estilos, scripts de marketing, carrosseis e imagens espalhadas.

## Principais problemas encontrados

### 1. Dominio de entrada quebrado

- `www.alabadaue.com` nao resolveu durante a analise.
- Isso cria friccao antes mesmo de medir UX, SEO ou conversao.

Impacto:
- usuarios podem acreditar que o site caiu
- links antigos podem falhar
- risco de perda de trafego organico e campanhas

Acao recomendada:
- configurar redirect `301` de `www.alabadaue.com` para `https://alabadaue.com`
- alinhar canonical, Search Console e provedores de analytics com o dominio final

### 2. Excesso de plugins e CSS carregado na home

A home esta trazendo assets de varias frentes ao mesmo tempo:

- `Elementor`
- `Bridge`
- `Qi Blocks`
- `Qi Addons`
- `Qode Essential Addons`
- `King Addons`
- `HT Mega`
- `BlogLentor`
- `Ultimate Post`
- `Revolution Slider`
- `SureCart`
- `Click to Chat`
- `Complianz`

Sinal concreto:
- dezenas de folhas CSS e bibliotecas JS sao carregadas mesmo quando a home usa uma composicao visual relativamente simples
- parte disso parece vir de widgets generalistas e dependencias globais de WordPress/Elementor

Impacto:
- mais bloqueio de renderizacao
- mais disputa entre estilos
- mais custo para manutencao
- maior chance de regressao visual

Acao recomendada:
- reconstruir com stack mais enxuta
- carregar CSS por pagina/componente
- remover widgets e bibliotecas que nao participam da home

### 3. Tracking e third-parties demais para a primeira dobra

Foram vistos recursos de:

- Google Tag Manager / Google Ads / Analytics
- Meta Pixel
- HubSpot
- Microsoft Clarity
- SureCart

Contagens relevantes:

- `25` eventos para `e.clarity.ms`
- `5` requests para `www.facebook.com`
- `4` requests para `www.googletagmanager.com`
- `4` requests para `connect.facebook.net`
- `3` requests para `www.google.com`/`www.google.com.br`
- `3` requests para `js.hs-banner.com`

Impacto:
- mais CPU e rede cedo demais
- piora de TBT/INP em dispositivos medianos
- mais pontos de falha de consentimento e privacidade

Acao recomendada:
- adiar trackers nao essenciais para depois da interacao/consentimento
- consolidar tags em um plano minimo de medicao
- revisar se HubSpot, Meta e Clarity precisam estar todos ativos na home

### 4. Carrosseis e grids com custo alto para pouco ganho

A home depende muito de:

- slider hero
- cards filtrados
- carrossel de logos
- cards com imagens em mosaico

Isso aumenta:

- JS no cliente
- repaint e reflow
- comportamento inconsistente no mobile

Na pratica, uma vitrine editorial assim poderia ser servida com menos JS e mais HTML/CSS nativo.

### 5. Imagens numerosas e pouco otimizadas

Diagnostico observado:

- `116` imagens na home
- `41` nao lazy
- `37` sem dimensoes declaradas
- hero com imagens `2700x1687` servidas em contexto visual menor

Impacto:
- mais bytes e decode de imagem
- risco de layout shift
- piora significativa em 4G e aparelhos modestos

Acao recomendada:
- gerar tamanhos responsivos reais
- usar `srcset`/`sizes` de forma controlada
- lazy load fora da primeira dobra
- manter apenas 1 imagem critica para o hero inicial

### 6. Responsividade fragil no mobile

No viewport `390x844`, a home ficou visualmente comprimida:

- textos muito pequenos
- cards estreitos
- espacos verticais excessivos
- hierarquia visual perde legibilidade
- footer e areas institucionais ficam apertados

Mesmo sem overflow horizontal, a leitura mobile parece adaptada por encolhimento, nao por redesenho real.

Acao recomendada:
- refazer layout mobile-first
- trocar mosaicos muito densos por listas/carrosseis mais legiveis
- revisar tipografia e espacamento por breakpoint

### 7. Problemas de qualidade visual/estrutural ja aparentes

Na home atual:

- os contadores aparecem como `+0`
- existe um grande vazio vertical antes da area de logos
- o `h1` capturado na home nao representa a proposta da pagina, e sim um item de conteudo

Impacto:
- perda de credibilidade
- SEO semantico ruim
- leitura confusa do valor principal da marca

## Hipotese tecnica do gargalo

O problema principal nao parece ser servidor lento isoladamente. O gargalo esta mais alinhado a:

- tema WordPress generalista
- sobreposicao de plugins de UI
- scripts third-party demais
- componentes visuais montados com widgets
- home com funcao de portal, revista, portfolio, loja e CRM ao mesmo tempo

## Prioridades para o refactor

### Fase 1. Ganhos rapidos

- corrigir `www` para dominio principal
- remover contadores quebrados e espacos mortos
- desativar scripts/estilos nao usados na home
- reduzir trackers carregados antes do consentimento
- otimizar hero para 1 imagem principal

### Fase 2. Rebuild estrutural

- refazer home em arquitetura componentizada
- separar experiencia institucional, editorial, portfolio, artistas e loja
- substituir sliders pesados por componentes mais simples
- implementar design system com tokens fixos de tipografia, cor e espacamento

### Fase 3. Meta de performance

Para a nova versao, vale mirar em algo proximo de:

- menos de `90` requests na home
- menos de `4 MB` totais transferidos
- `LCP` abaixo de `2.5s`
- `INP` abaixo de `200ms`
- JS minimo na primeira dobra

## Evidencias usadas

- navegacao Playwright na home e viewport mobile
- `performance.getEntriesByType("navigation")`
- `performance.getEntriesByType("resource")`
- captura visual em desktop e mobile
- inspeção dos sitemaps XML do proprio dominio
