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
- Sessão guiada: demonstração dos exercícios (pode pular), contagem "3, 2, 1", voz em pt-BR (pode desligar).
  - Narração por fases (`INTRO`, `announce`): aquecimento, mobilidade, transição de 20 s "Aquecimento concluído" (passo com `tr:1`), começo do treino, alongamento, respiração.
  - Contagem guiada das repetições (`repTick`): a voz fala cada número no ritmo do exercício (`CAD` em segundos por repetição, vezes `PACE`), troca de lado nos exercícios "por perna/braço/lado" e passa sozinha para o descanso. O boneco se move no mesmo ritmo. Pode desligar (`S.count`).
  - Descanso ajustável (`S.restPref`: 'auto' ou segundos; gestante no mínimo 60 s), mais botões −15 s e +15 s no descanso. Ajustes ficam no cartão "Ajustes do treino" da aba Plano.
- Ilustrações: bonecos de traço animados entre duas poses (`PO` e `FIG`). No modo gestante o boneco ganha barriga (`.bel`; `front:1` marca poses de frente).
- Modo gestante (`S.profile.mode==='gest'`): dados em `WG`, `WARMG`, `MOBG`, `COOLSG` (alongamento + respiração e assoalho pélvico), `LVG`. O nível é o trimestre, calculado pela semana informada mais o tempo passado (`gWeek`, `triOf`). `applyMode()` troca as variáveis `W`, `MOB`, `COOLS` etc. a cada `route()`.
  - Sem liberação do obstetra ou com alguma condição de `CONDS`, os treinos ficam pausados (`gBlocked`).
  - A partir do 2º trimestre não há exercício deitada de costas. Sem saltos, sem prender a respiração, sempre com apoio.
  - Sem sugestão de subir de nível e sem registro de peso. O fim do treino tem a opção "Senti desconforto", que mostra os sinais de alerta (`DANGER`).
  - Baseado nas recomendações do ACOG para exercício na gravidez. Qualquer mudança aqui deve manter esses cuidados.
- Tela sempre ligada na sessão (`keepAwake`/`letSleep`): Wake Lock que é pedido de novo quando o celular solta, mais um vídeo preto, mudo e invisível em loop como plano B.
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
