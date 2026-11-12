# English in Focus

Site gratuito para aprender inglês com leituras curtas, áudio, histórias ilustradas e interpretação. **Os visitantes não precisam criar conta.** Não há IA sendo executada no navegador nem cobrança por leitura.

## O que já funciona

- Página inicial responsiva, com foto autoral da bandeira do Brasil.
- Biblioteca de leituras com busca por título, assunto ou categoria.
- Leitura com **Level 1 (iniciante), Level 2 (intermediário) e Level 3 (avançado)**.
- Áudio MP3 para cada nível, com **reproduzir, pausar, retomar do mesmo segundo, reiniciar, avançar na linha do tempo** e velocidades de **0,5×, 1×, 1,5× e 2×**.
- Gibi de quatro cenas, com imagens e legendas em inglês.
- Vocabulário com tradução e três perguntas de interpretação por nível, incluindo correção e possibilidade de tentar novamente.
- Seção **Sobre nós** com a missão do projeto.
- O site não tem cadastro, pagamento, formulários de coleta de dados ou dependências de serviços externos.

> **Exemplo inicial:** "Artificial Intelligence and Our Thinking Skills" foi escrito para demonstrar a experiência. Os MP3 incluídos são **narrações provisórias geradas offline por eSpeak**, não vozes neurais naturais. Antes de divulgar o site, substitua-os por arquivos MP3 de um serviço TTS de sua preferência, preservando os nomes, e revise editorialmente todos os conteúdos. As quatro ilustrações são originais, produzidas com IA.

## Como ver no computador

Na raiz da pasta, abra um terminal e rode:

```bash
cd public
python -m http.server 8000
```

Visite `http://localhost:8000` no navegador. **Não abra o `index.html` diretamente com duplo clique**: por segurança, o navegador bloqueia o carregamento dos arquivos JSON em `file://`.

## Como trocar a foto da página inicial

1. Coloque a nova imagem na pasta `public/assets/`. Prefira `.webp`, comprimido, idealmente com 1400–2200 px de largura.
2. Abra `public/content/site.json` e altere `backgroundImage`, por exemplo, para `/assets/foto-da-semana.webp`.
3. Se quiser, altere também `backgroundCredit`, `backgroundAlt`, `tagline` e `subtitle`.
4. Salve e publique no GitHub.

A imagem original permanece na pasta e pode ser reutilizada. Se preferir manter apenas uma imagem, substitua `public/assets/fundo-brasil.webp` pelo novo arquivo mantendo o nome; nenhuma alteração no JSON será necessária.

## Como adicionar uma nova leitura

A estrutura de cada leitura é **um arquivo JSON por assunto**. Há um exemplo completo em `public/content/lessons/ia-e-pensamento-critico.json`.

1. Escolha um título ou um tema e peça ao ChatGPT **três textos originais em inglês** (até quatro parágrafos por nível), vocabulário, três perguntas por nível e quatro legendas para as cenas do gibi. Para fatos atuais, use fontes confiáveis e confira os dados antes de publicar. Não copie o corpo de notícias protegidas.
2. Crie um arquivo `public/content/lessons/nome-do-tema.json` usando a estrutura do exemplo. O `slug` é o nome do arquivo sem `.json`.
3. Coloque quatro imagens em `public/assets/comics/nome-do-tema/`, preferencialmente `.webp`; coloque um áudio MP3 por nível em `public/assets/audio/`.
4. Referencie esses arquivos no JSON. Use caminhos absolutos iniciados com `/`.
5. Adicione um novo item ao array `lessons` no arquivo `public/content/index.json` com os mesmos `slug`, `title`, `titlePt`, `category`, `date`, `summary`, `cover` e `readingMinutes`.
6. Rode `python scripts/check_content.py` **a partir da raiz do projeto**. Corrija qualquer erro apontado.
7. Publique as alterações no GitHub. O site exibirá a leitura automaticamente. **Não é necessário editar HTML, CSS ou JavaScript.**

### Prompt de publicação sugerido

> Quero adicionar uma nova leitura ao English in Focus sobre **[TEMA]**. Prepare um texto educativo **original em inglês**, com até quatro parágrafos para cada nível (1 iniciante, 2 intermediário, 3 avançado). Todos os níveis devem manter a mesma base factual, mas adaptar vocabulário e estrutura. Crie também cinco itens de vocabulário com tradução para português, três perguntas de múltipla escolha por nível com gabarito e explicação, e quatro cenas com legendas em inglês para um gibi. Se for notícia ou tema controverso, confira os fatos em fontes confiáveis, indique as fontes e não invente declarações, números ou acontecimentos. Gere os arquivos no formato JSON do projeto.

Com o GitHub conectado ao ChatGPT e **com o repositório do site criado e acessível**, podemos trabalhar com arquivos e propostas de alteração nos fluxos permitidos pela integração. A publicação automática ocorre pelo Cloudflare Pages **após o envio das mudanças ao GitHub**, não apenas por escrever uma mensagem no chat.

## Publicar no Cloudflare Pages

1. Crie um **novo repositório** no GitHub, por exemplo `english-in-focus`, para não afetar outros projetos.
2. Faça upload do conteúdo desta pasta para a **raiz** desse repositório (a pasta `public` precisa ficar na raiz, ao lado deste `README.md`).
3. No painel da Cloudflare, abra **Workers & Pages → Create application → Pages → Connect to Git** e selecione o repositório.
4. Use a branch `main`, **Framework preset: None**, **Build command:** deixe em branco ou use `exit 0`, e **Build output directory:** `public`.
5. Clique para publicar e teste a URL terminada em `.pages.dev` fornecida pela plataforma.

A Cloudflare Pages publica alterações automaticamente quando um commit novo chega à branch de produção. Para um domínio próprio, adicione-o nas configurações do projeto quando quiser.

Documentação oficial: [Cloudflare Pages — Static HTML](https://developers.cloudflare.com/pages/framework-guides/deploy-anything/) e [Integração Git](https://developers.cloudflare.com/pages/configuration/git-integration/).

## Arquivos principais

```text
english-in-focus/
├── README.md
├── public/                         # Pasta que Cloudflare publica
│   ├── index.html                  # Página e estrutura visual
│   ├── styles.css                  # Estilos responsivos
│   ├── app.js                      # Interação e controles
│   ├── content/
│   │   ├── site.json               # Slogan e fotografia de fundo
│   │   ├── index.json              # Catálogo de leituras
│   │   └── lessons/                # Textos de cada leitura
│   └── assets/
│       ├── audio/                  # Um MP3 para cada nível
│       └── comics/                 # Quatro imagens por leitura
└── scripts/
    ├── check_content.py           # Verificação dos arquivos
    └── generate_demo_audio.py     # Narração robótica provisória
```

## Observações

- Os links, gibis, imagens e áudios são previamente preparados por quem publica: visitantes não consomem créditos de IA.
- Para temas médicos, políticos e acontecimentos em desenvolvimento, confirme fontes e inclua explicações equilibradas. Se um título por si só for insuficiente para uma afirmação, não a transforme em fato.
- Guarde direitos de uso e atribuições necessários para fotos, imagens, vozes e outros materiais.
- Versão inicial: sem vídeo, sem login, sem anúncios, sem blog e sem assinaturas.
