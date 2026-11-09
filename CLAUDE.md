# Treino na Sala

App de treino em casa sem equipamento (força, condicionamento e perda de gordura), feito para o Mardonyo usar no celular. É um PWA publicado pelo GitHub Pages e instalado no Android pelo Chrome.

- Endereço: https://mdmorais25-bot.github.io/treino-na-sala/
- Repositório: mdmorais25-bot/treino-na-sala, branch `main`, publicado a partir da raiz (`/`).

## Arquivos

- `index.html`: o app inteiro (HTML, CSS e JavaScript num arquivo só, sem build nem dependências).
- `manifest.webmanifest`: nome, cores e ícones para instalar.
- `sw.js`: service worker. Busca a página na rede primeiro e cai para o cache quando estiver offline.
- `icon-192.png`, `icon-512.png`, `apple-touch-icon.png`: ícone azul com o boneco agachado.

## Como o app está organizado (dentro do index.html)

- Abas: Hoje, Plano, Histórico, Perfil (rota pelo `#hash`).
- Treinos: A (pernas e core, força), B (peito, costas e braços, força), C (circuito de condicionamento). Cada um tem 3 níveis: Iniciante, Intermediário, Avançado (`W`).
- Cada sessão: aquecimento geral, 2 min de mobilidade específica do treino (`MOB`), o treino, alongamento específico no final (`COOLS`). Mobilidade e alongamento nunca são cortados.
- Tempo disponível (15/20/30/45 min): `config()` escolhe exercícios, séries ou voltas para caber no tempo.
- Perfil opcional (peso, altura, objetivo, atividade, teste de flexões e agachamentos, dias, saúde): `recommend()` define níveis, frequência e fase de adaptação para sedentários.
- Sessão guiada: demonstração dos exercícios (pode pular), contagem "3, 2, 1", voz em pt-BR (pode desligar), cronômetro nas séries por repetição.
- Ilustrações: bonecos de traço animados entre duas poses (`PO` e `FIG`).
- Dados ficam no `localStorage` do aparelho (chave `treino-sala`). Não há servidor.

## Para publicar uma versão nova

1. Edite `index.html`.
2. Em `sw.js`, aumente o número em `const CACHE = 'treino-na-sala-vN'`.
3. Commit e push na `main`. O GitHub Pages atualiza em cerca de 1 minuto.
4. Confira com `curl` se o site publicado já está igual ao arquivo (o domínio `mdmorais25-bot.github.io` está liberado na rede).
5. No celular, a versão nova chega ao abrir o app com internet.

## Preferências do Mardonyo para este app

- Tudo em português do Brasil, linguagem simples.
- Ilustrações enxutas, só o necessário para entender o movimento.
- Ele usa pelo celular e prefere que o Claude faça e confira tudo pelo chat.
