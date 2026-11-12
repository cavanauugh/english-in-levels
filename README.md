# English in Levels

Site gratuito de leituras em inglês, criado para brasileiros. Sem login, sem planos e sem geração de textos por visitantes.

## Tecnologias
- Astro (site estático)
- Conteúdos em JSON, preparados antecipadamente
- CSS e JavaScript para níveis, áudio e interpretação
- Deploy sugerido: Cloudflare Pages

## Executar localmente
1. Instale Node.js 22.
2. Rode `npm install`.
3. Rode `npm run dev`.
4. Rode `npm run build` para gerar a versão estática em `dist/`.

## Publicar na Cloudflare Pages
Conecte este repositório. Configuração: branch `main`, comando `npm run build`, diretório de saída `dist`. Novos commits serão publicados pelo Cloudflare quando a integração estiver ativada.

## Publicar uma leitura
Crie um arquivo `src/content/leituras/slug.json` usando o modelo existente. Cada aula contém `levels.1`, `levels.2`, `levels.3`, vocabulário, perguntas, cenas de gibi e referências consultadas. Não copie notícias: publique textos originais revisados. O site reúne os arquivos automaticamente ao compilar.

## Áudio
O campo `audio` de cada nível aceita caminho de arquivo, por exemplo `/audios/ia-level-1.mp3`. Quando vazio, o site usa a voz do navegador como **demonstração**, e a qualidade depende do dispositivo. Arquivos de áudio pré-gerados são recomendados para produção; eles garantem pausar e continuar exatamente da posição anterior.

## Atualizar foto e ilustrações
Altere `public/imagens/bandeira-brasil.svg` (ou use jpg/webp em `src/data/site.js`). A imagem inicial é uma versão comprimida da fotografia enviada pela autora e pode ser substituída pela original em melhor resolução. A foto não é alterada pelo visitante.

## Privacidade e custos
O site não exige cadastro, não usa chaves de IA no navegador e não envia textos a modelos de IA durante o acesso. Todo conteúdo, narração e gibi são produzidos previamente. Verifique direitos autorais e fatos antes de publicar.

## Estado do projeto
Primeira versão funcional de demonstração. Hospedagem e domínio dependem de configuração no Cloudflare.