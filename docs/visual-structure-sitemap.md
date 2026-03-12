# Estrutura Visual e Sitemap

Data do mapeamento: 2026-03-12
Base: navegacao observada em `https://alabadaue.com` + sitemaps XML publicos do dominio

## Leitura geral da plataforma

O site atual funciona como um ecossistema de varios produtos ao mesmo tempo:

- home institucional/editorial
- portfolio de projetos
- revista de conteudo
- vitrine de marcas
- banco de artistas
- area de educacao/produtos digitais
- loja/checkout

Essa ambicao e forte, mas hoje a arquitetura parece crescer por acumulacao. Para o refactor, vale separar melhor os papeis.

## Estrutura visual da home atual

Ordem percebida:

1. Header com assinatura da marca, logo, sociais e menu
2. Hero com destaque rotativo
3. Mini destaque editorial adicional
4. Tabs de categorias
5. Grid de cards mistos
6. Bloco institucional com metricas
7. Faixa de logos/parceiros
8. Footer institucional

## Problema da estrutura atual

Na home, convivem ao mesmo tempo:

- conteudo
- projeto
- marca
- artista
- produto
- formulario

Isso torna dificil responder rapidamente:

- o que a Badauê e
- para quem ela serve
- qual acao principal o usuario deve tomar

## Arquitetura recomendada para o ponto 1

### Nivel 1. Entrada principal

- Home
- Projetos
- Conteudos
- Marcas
- Educacao
- Artistas
- Produtos
- Contato/Orcamento

### Nivel 2. Hubs claros

- `Projetos`: cases, servicos, segmentos
- `Conteudos`: artigos, entrevistas, tendencias
- `Marcas`: vitrine curada e possiveis collabs
- `Educacao`: relatorios, cursos, publicacoes
- `Artistas`: busca, filtros, perfil
- `Produtos`: produtos fisicos/digitais

### Nivel 3. Paginas de detalhe

- case individual
- artigo individual
- perfil de artista
- pagina de produto
- landing de inscricao/orcamento

## Sitemap observado

### Navegacao principal

- `/`
- `/laboratorio-2/`
- `/folhetim/`
- `/budega/`
- `/academia/`
- `/banco/`
- `/souvenir/`

### Paginas institucionais e operacionais vistas

- `/laboratorio/`
- `/orcamento/`
- `/trabalhe-na-badaue/`
- `/checkout/`
- `/painel-do-cliente/`
- `/termos-de-uso/`
- `/contrato-do-artista/`
- `/formulario-de-inscricao/`

### Contagens vindas dos sitemaps publicos

- `page-sitemap.xml`: `57` URLs
- `post-sitemap.xml`: `125` URLs
- `portfolio_page-sitemap.xml`: `24` URLs
- `sc_product-sitemap.xml`: `3` URLs
- `category-sitemap.xml`: `56` URLs

## Principais hubs e exemplos

### Projetos

URL observada:

- `/laboratorio-2/`
- tambem existe `/laboratorio/`

Sinal de atencao:
- existem duas rotas muito parecidas para laboratorio/projetos

Exemplos de cases vistos:

- `Terrone Pizzeria`
- `Melody Garden`
- `Tanning Club`
- `Elemental Trancoso`
- `Canto Belem`
- `Zeferina Producoes`
- `Universidade da Floresta`
- `Gondwana Brasil`

### Conteudos

URL observada:

- `/folhetim/`

Funcao:
- hub editorial e de pensamento

Exemplos vistos:

- `Entre passaros e sonhos...`
- `Mulheres empreendedoras...`
- `Ja sabiamos: nossa lingua e brasileira`

### Marcas

URL observada:

- `/budega/`

Exemplos vistos:

- `RAVO`
- `Costa Brazil`
- `Tua Folha Palavra`
- `Origem`
- `Balla Studios`
- `Feel`

### Educacao

URL observada:

- `/academia/`

Exemplos vistos:

- `Territorios do Futuro... 2026/2027`
- `A Arte e a Estrategia de Criar Marcas Com Gingado`
- `Territorios do Futuro... 2025/2026`

### Artistas

URL observada:

- `/banco/`

Funcao:
- banco de artistas e talentos

Exemplos vistos:

- `Thalita R Almeida`
- `Karen Eppinghaus`
- `Bruna Costa`
- `Mayara Ferrao`

### Produtos

URL observada:

- `/souvenir/`

Exemplos vistos:

- `Camiseta Yemanja`
- `Camiseta Coracao Brasileiro`
- `Camiseta Bahia`

Observacao:
- o sitemap de produtos (`/products/...`) e a pagina `/souvenir/` parecem fazer parte de uma camada comercial ainda pouco integrada

## Estrutura recomendada para a nova versao

## Opcao A. Manter o ecossistema em um so dominio

### Navegacao principal

- Inicio
- Solucoes
- Projetos
- Conteudos
- Banco de Artistas
- Educacao
- Loja
- Contato

### Home sugerida

1. Hero manifesto + CTA principal
2. Prova de autoridade: marcas, projetos, comunidade
3. Blocos de entrada para as 4 frentes principais
4. Cases em destaque
5. Conteudos em destaque
6. Banco de artistas em destaque
7. CTA final

Vantagem:
- mais claro para novos visitantes

### Reorganizacao de nomenclatura

- `Laboratorio` -> `Projetos` ou `Solucoes`
- `Budega` -> `Marcas`
- `Folhetim` pode continuar se for nome editorial assumido
- `Souvenir` -> `Loja`

## Opcao B. Separar experiencia institucional da experiencia editorial/comercial

### Site principal

- Home
- Sobre
- Solucoes
- Projetos
- Contato

### Plataformas conectadas

- Folhetim
- Banco de Artistas
- Academia
- Loja

Vantagem:
- reduz carga cognitiva da home
- melhora narrativa comercial

## Mapa de componentes para reconstruir

Componentes-base necessarios:

- Header
- Menu mobile
- Hero manifesto
- Card feature
- Card editorial
- Card projeto
- Card artista
- Card produto
- Tabs/filtros
- Faixa de logos
- CTA section
- Footer

## Dependencias de conteudo para o rebuild

Antes de implementar, vale consolidar:

- taxonomia oficial dos hubs
- prioridade de CTA por pagina
- diferenca entre projetos, marcas e produtos
- politica de atualizacao dos numeros/metricas
- se a loja continua integrada ao site principal

## Observacoes de arquitetura

- a home atual aponta para uma plataforma viva, mas a hierarquia nao esta totalmente resolvida
- o refactor deve priorizar clareza de navegacao antes de sofisticacao de widget
- o sitemap publico mostra volume suficiente para justificar uma arquitetura modular e nao uma home monolitica
