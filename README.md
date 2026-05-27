# Portfólio — Victor Tedesco

## Estrutura de Arquivos

```
portfolio2/
├── index.html          → Homepage (carrega cards do JSON automaticamente)
├── projects.json       → FONTE DE VERDADE de todos os projetos
│
├── branding/
│   └── index.html      → Template de Identidade Visual
├── landing/
│   └── index.html      → Template de Landing Page
├── product/
│   └── index.html      → Template de Produto Digital
│
└── README.md
```

> **Atenção:** Para que o fetch do JSON funcione, abra o projeto com um **servidor local**.  
> No VS Code: use a extensão **Live Server** (botão "Go Live" no canto inferior direito).  
> Via terminal: `python3 -m http.server 8080` e acesse `http://localhost:8080`.

---

## Como adicionar um novo projeto

### 1. Abra o `projects.json`

Adicione um novo objeto ao array. Copie o bloco do mesmo tipo do seu projeto e preencha:

```json
{
  "id": "nome-do-projeto",          // slug único, usado na URL
  "type": "branding",               // "branding" | "product" | "landing"
  "title": "NOME",                  // título em caixa alta
  "loaderLine1": "categoria",       // 1ª linha do loader (cinza)
  "loaderLine2": "nome do projeto", // 2ª linha do loader (branco)
  "tags": "TAG 1 • TAG 2 • TAG 3",  // tags exibidas no topo da página
  "meta": {
    "client": "Nome do Cliente",
    "role": "Sua função no projeto",
    "year": "2025",
    "tools": "Figma, Illustrator"
  },
  "heroImage": {
    "src": "https://url-da-imagem.jpg",
    "alt": "Descrição da imagem"
  },
  "sections": ["gallery", "mockupFull"],  // veja seções disponíveis abaixo
  ...
  "behance": "https://www.behance.net/seu-link",
  "card": {
    "bgColor": "#f0f0f0",           // cor de fundo do card na homepage
    "thumb": "https://url.jpg",     // thumbnail do card (opcional)
    "aspect": "110%"                // proporção do card (ex: "90%", "130%")
  }
}
```

Salve o arquivo. O card aparece automaticamente na homepage.

---

## Seções disponíveis por tipo

Controle quais seções aparecem em cada projeto através do array `"sections"`.  
Seções fora do array ficam **ocultas automaticamente**.

### Branding (`branding/index.html`)

| Seção          | Chave no JSON    | Dados necessários          |
|----------------|------------------|----------------------------|
| Paleta de cores | `"palette"`     | array `palette`            |
| Galeria 2 imgs  | `"gallery"`     | array `gallery` (1–2 items)|
| Mockup largura total | `"mockupFull"` | objeto `mockupFull`    |

**Dados obrigatórios (sempre exibidos):** `heroImage`, `concept`, `topics`

```json
"sections": ["palette", "gallery", "mockupFull"],
"palette": [
  { "name": "Nome da Cor", "hex": "#RRGGBB" }
],
"concept": { "label": "O Conceito", "text": "Texto..." },
"topics": [
  { "title": "Tópico 1", "text": "Descrição..." },
  { "title": "Tópico 2", "text": "Descrição..." }
],
"gallery": [
  { "src": "https://...", "alt": "Alt text", "caption": "01. Legenda" },
  { "src": "https://...", "alt": "Alt text", "caption": "02. Legenda" }
],
"mockupFull": { "src": "https://...", "alt": "Alt", "caption": "03. Legenda" }
```

---

### Produto Digital (`product/index.html`)

| Seção          | Chave no JSON    | Dados necessários          |
|----------------|------------------|----------------------------|
| Galeria 2 imgs  | `"gallery"`     | array `gallery` (1–2 items)|
| Mockup largura total | `"mockupFull"` | objeto `mockupFull`    |

**Dados obrigatórios:** `heroImage`, `concept`, `topics`

```json
"sections": ["gallery", "mockupFull"],
"concept": { "label": "O Produto", "text": "Texto..." },
"topics": [
  { "title": "UX Strategy", "text": "..." },
  { "title": "Design System", "text": "..." }
],
"gallery": [ ... ],
"mockupFull": { ... }
```

---

### Landing Page (`landing/index.html`)

| Seção          | Chave no JSON    | Dados necessários          |
|----------------|------------------|----------------------------|
| Métricas        | `"metrics"`     | array `metrics` (3 items)  |
| Metas           | `"goals"`       | array `goals` (strings)    |
| Galeria 2 imgs  | `"gallery"`     | array `gallery` (1–2 items)|
| Mockup largura total | `"mockupFull"` | objeto `mockupFull`    |

**Dados obrigatórios:** `heroImage`, `concept`, `topics`

```json
"sections": ["metrics", "goals", "gallery", "mockupFull"],
"metrics": [
  { "value": "94%",    "label": "Satisfação dos usuários" },
  { "value": "98/100", "label": "PageSpeed Score" },
  { "value": "12K+",   "label": "Leads gerados" }
],
"goals": [
  "Meta 1",
  "Meta 2",
  "Meta 3"
],
"concept": { "label": "O Projeto", "text": "..." },
"topics": [ ... ],
"gallery": [ ... ],
"mockupFull": { ... }
```

---

## Como acessar um projeto

Com o servidor local rodando:

| Tipo       | URL de exemplo                              |
|------------|---------------------------------------------|
| Branding   | `http://localhost:8080/branding/?id=caju`   |
| Produto    | `http://localhost:8080/product/?id=aptr`    |
| Landing    | `http://localhost:8080/landing/?id=fabrica` |

Quando hospedado (Netlify, Vercel, GitHub Pages), as URLs ficam limpas sem o `index.html`.

---

## Projetos de exemplo incluídos

| ID       | Tipo       | Descrição                     |
|----------|------------|-------------------------------|
| `caju`   | branding   | Identidade Visual Caju Tropical |
| `aptr`   | product    | Dashboard APTR Platform         |
| `fabrica`| landing    | Landing Page Fabrica Corp       |

---

## Dicas rápidas

- **Ordem dos cards**: os projetos aparecem na homepage na ordem em que estão no JSON (coluna 1, 2, 3, 1, 2, 3...).
- **Thumbnail do card**: use imagens com pelo menos 600px de largura. Serviços como Unsplash, Cloudinary ou sua própria pasta `assets/` funcionam.
- **Projeto curto**: omita seções do array `sections` para uma página mais enxuta.
- **Behance**: o botão "Ver case completo" só aparece quando o campo `behance` está preenchido. Se não quiser exibir, deixe como `""`.
