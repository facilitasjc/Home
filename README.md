# Facilita Vendas SJC - Projeto Web Completo

## Estrutura de Pastas
- index.html (home)
- veiculos.html (catálogo de veículos)
- sobre.html (institucional)
- contato.html (contato)
- admin.html (painel administrativo)

### /css
- style.css (estilos globais)
- admin.css (estilos específicos do admin)

### /js
- main.js (funcionalidades da home e destaques)
- admin.js (painel administrativo)
- database.js (CRUD LocalStorage)
- imageUpload.js (upload e preview)
- utils.js (funções utilitárias)
- filters.js (filtros de veículos)

### /assets
- logo.png, hero-car.png, placeholder-car.jpg
- /icons (ícones svg básicos)

## Funcionalidades
- Cadastro, edição e exclusão de veículos (admin)
- Upload e preview de imagens
- Busca e filtros em tempo real
- Destaques na home
- Integração com WhatsApp
- Responsividade mobile

## Como usar
1. Abra `index.html` para a home.
2. Abra `veiculos.html` para ver catálogo com filtros.
3. Acesse `admin.html` para gerenciar estoque (funciona via LocalStorage).
4. Substitua imagens em `/assets` pelas reais da loja.

## Deploy no GitHub
- Inicie repositório git e suba os arquivos.
- Recomendado usar GitHub Pages para publicar.


## Ajustes realizados na versão v3
- Paginação implementada (6 itens por página) em `filters.js`.
- Google Maps adicionado em `contato.html` via iframe. Substitua a query se desejar coordenadas específicas.
- Formulário de contato integrado com Formspree (action placeholder `https://formspree.io/f/your-id`). Substitua `your-id` pelo seu endpoint Formspree.
- Sanitização básica de inputs aplicada no admin e no formulário de contato para reduzir risco de XSS.
- Upload de imagens: imagens são redimensionadas e armazenadas como Base64 via `imageUpload.js` + `admin.js` salva imagem no LocalStorage.
- Minified CSS/JS gerados (.min.css/.min.js) com minificação simples.

Observação: Para armazenar imagens como arquivos no repositório você terá que fazer o upload manual para `/assets/cars/` e atualizar o registro do veículo para referenciar `/assets/cars/nome.jpg`.


## Fluxo para publicar imagens no GitHub Pages
1. No painel admin (modo LocalStorage), cadastre veículos e carregue as imagens (serão salvas no LocalStorage como base64).
2. Clique em **Exportar para Repositório (JSON)** — isso baixa `facilita_vendas_export.json` contendo os dados e imagens em base64 (campo `_exportImage`).
3. No seu computador (fora do navegador), mova esse JSON para a raiz do repositório clonado e execute:

```bash
node scripts/import_images.js facilita_vendas_export.json
```

4. O script criará pastas em `assets/cars/{id}/photo1.jpg` e gerará `vehicles.json` com os registros atualizados apontando para os caminhos de imagem. Adicione/commit/push esses arquivos para o GitHub.

Agora o site no GitHub Pages poderá carregar imagens por caminho estático em `assets/cars/`.


## Versão v5 - Imagens genéricas incluídas
- Pastas `/assets/cars/car1..car5` com imagens e `data.json` de exemplo foram adicionadas.
- Substitua essas imagens pelas reais quando quiser; mantenha os nomes de arquivos ou atualize os `data.json` correspondentes.
- Fluxo de export/import permanece: exporte do admin e rode `node scripts/import_images.js facilita_vendas_export.json` para criar novas pastas e `vehicles.json`.
