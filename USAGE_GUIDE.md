# USAGE_GUIDE.md

## 1. Objetivo do sistema

- Este sistema serve para ajudar a analisar uma oportunidade de aposta antes de decidir entrar.
- O objetivo principal e organizar o raciocinio, melhorar a consistencia e reduzir decisoes impulsivas.
- Nao e um sistema de previsoes automaticas.
- Nao foi feito para dar picks cegas.
- E um sistema de apoio a decisao.
- A pergunta central e: devo entrar nesta aposta ou nao, e por que motivo?

---

## 2. Como iniciar uma analise

- O pedido deve ser claro e direto.
- Sempre que possivel, indicar:
  - evento
  - mercado
  - lado
  - odds
  - contexto relevante

### O que descrever

- `Evento`: o jogo, corrida ou confronto em causa.
- `Mercado`: por exemplo moneyline, spread, total, BTTS, qualifying H2H, race H2H.
- `Lado`: a selecao que esta a ser considerada.
- `Odds`: o preco atual, de preferencia com hora ou momento de referencia.

### Exemplo de pedido para futebol

- "Quero analisar Arsenal vs Liverpool no mercado BTTS. Estou a considerar o Yes a 1.78. Lesoes relevantes: um defesa titular do Arsenal esta em duvida."

### Exemplo de pedido para NBA

- "Quero analisar Celtics vs Bucks no spread. Estou a olhar para Celtics -4.5 a 1.91. Os Bucks jogam em back-to-back e ha duvida sobre um titular."

### Exemplo de pedido para NBA props

- "Quero analisar Jalen Brunson over 8.5 assistencias em Knicks vs Heat. Estou a olhar para 1.87. Preciso de confirmar minutos, role e quem joga ao lado dele."

### Exemplo alternativo para F1

- "Quero analisar o qualifying H2H entre Leclerc e Russell em Monza. O preco atual do Leclerc e 1.85. Ainda faltam confirmacoes finais de condicoes da pista."

### Formato especial para listas diarias

- Se a mensagem comecar exatamente por `Análises do dia:` e terminar exatamente com `Abraço`, o sistema entra em modo de lote diario.
- Nesse modo, cada linha com `-` e tratada como uma candidata separada.
- O sistema faz triagem rapida, define faixa de odd, checks necessarios e estado inicial.
- O sistema reutiliza sempre o mesmo Google Sheets tracker.
- O sistema nao cria um ficheiro novo por dia.

### Exemplo de lote diario

```text
Análises do dia:

-Empate anula Bayern

-0.5+ golos equipa Sporting

-Vence Fluminense

-Ambas marcam jogo Wrexham

-Empate anula Nordajaelland

Abraço
```

### Formato especial para entradas ja feitas

- Se a mensagem comecar exatamente por `Entradas feitas:`, o sistema entra em modo de promocao de entradas.
- Neste modo, o objetivo ja nao e criar candidatas novas.
- O sistema tenta encontrar as candidatas existentes e promovê-las para `Base_Entradas`.
- Nao precisa de terminar com nenhuma frase especial.
- O campo recomendado para ligar tudo sem ambiguidade e `candidate_id`.
- Mas o sistema tambem deve aceitar o formato cru copiado da casa de apostas, sem ires buscar ids manualmente.

### Exemplo de lote de entradas

```text
Entradas feitas:

- Sporting over 0.5
candidate_id: CAND-20260407-001
odd_entrada: 1.47
hora_entrada: 2026-04-07 18:10
observacoes: linha mantida dentro da faixa

- Bayern dnb
candidate_id: CAND-20260407-002
odd_entrada: 1.71
hora_entrada: 2026-04-07 19:02
```

### Exemplo de lote de entradas em formato cru

```text
Entradas feitas:

Bayern Munich
1.74
Draw no bet
Real Madrid vs Bayern Munich
07/04, 20:00
Possible payout: EUR 0.87

Details
07/04, 08:25

yes
1.63
Both teams to score
Wrexham AFC vs Southampton FC
07/04, 20:00

Possible payout: EUR 0.81

Details
07/04, 08:26
```

Neste caso, o sistema deve tentar ligar automaticamente cada bloco usando sobretudo:
- evento
- mercado
- lado
- hora do jogo
- hora da entrada

---

## 3. Fluxo de utilizacao

- O sistema segue sempre uma ordem consistente.
- A ideia e nao saltar diretamente para uma conclusao.

### 1. Intake

- O sistema organiza o pedido.
- Identifica o evento, o mercado, o lado, o preco e o objetivo da analise.
- Em modo de lote diario, primeiro identifica o envelope do lote, cria um batch e divide as linhas em candidatas.
- Em modo de promocao de entradas, primeiro divide a mensagem em blocos de entrada e tenta ligar cada bloco a uma candidata existente.

### 2. Validacao dos dados

- O sistema verifica se ha dados suficientes.
- Tambem tenta perceber se os dados estao atualizados e se fazem sentido para esse mercado.

### 3. Analise do desporto

- O sistema faz a leitura especifica do desporto.
- No futebol, olha para o contexto competitivo, forma, cobertura estatistica e disponibilidade.
- Na NBA, olha para lesoes, rotacao, descanso, travel e matchup.
- Na F1, olha para o momento do fim de semana, ritmo, estrategia, penalties, weather e reliability.

### 4. Avaliacao de mercado

- O sistema verifica se a leitura do evento realmente encaixa no mercado escolhido.
- Uma boa leitura do jogo nem sempre significa uma boa aposta naquele mercado.

### 5. Avaliacao de risco

- O sistema mede o peso da incerteza.
- Verifica fragilidade da tese, informacao por confirmar e sinais de risco.

### 6. Decision Gate

- No fim, o sistema transforma a analise num resultado pratico:
  - `enter`
  - `pass`
  - `watchlist`
  - `insufficient data`

### 7. Output final

- O sistema devolve uma resposta estruturada.
- Essa resposta mostra nao apenas a conclusao, mas tambem a base que levou a essa conclusao.
- Em modo de lote diario, pode devolver um resumo compacto do processamento, desde que os campos estruturados fiquem no tracker.
- Em modo de promocao de entradas, pode devolver um resumo compacto das entradas promovidas e dos bloqueios de correspondencia.

---

## 4. Inputs recomendados

- Sempre que possivel, fornecer:
  - evento
  - mercado
  - lado
  - odds
  - timestamp das odds
  - contexto relevante

### Lista recomendada

- `Evento`: equipas, jogo, GP, confronto ou corrida.
- `Mercado`: exatamente qual e o mercado que queres analisar.
- Para NBA props, indicar tambem o jogador e o tipo de prop (`PTS`, `AST`, `REB`, `PA`, `PR`, `PRA`, `3PM`).
- `Odds + timestamp`: o preco atual e, se possivel, quando foi visto.
- `Contexto`: lesoes, forma recente, rotacao, lineup, penalties, weather, descanso, travel ou outro fator relevante.

### Regra pratica

- Mais contexto tende a produzir melhor analise.
- Menos contexto tende a aumentar a incerteza.
- Falta de dados pode levar a `insufficient data`.
- Se o contexto estiver incompleto mas puder ser confirmado mais tarde, o sistema pode devolver `watchlist`.
- Em lote diario, a falta de contexto nao autoriza inventar certeza. O sistema deve manter os campos em falta explicitos no tracker.

---

## 5. Como interpretar o output

- O output final tem varios campos.
- Cada um serve para uma parte diferente da decisao.

### Data Quality

- Mostra a qualidade da base informativa.
- Responde a uma pergunta simples: os dados chegam para analisar com responsabilidade?
- Leitura pratica:
  - `strong`: base muito boa
  - `usable`: base suficiente
  - `weak`: base fragil
  - `insufficient`: base insuficiente

### Edge Quality

- Mostra a qualidade da vantagem percebida.
- Responde a esta pergunta: a leitura parece realmente ter valor face ao preco atual?
- Leitura pratica:
  - `clear`: vantagem bem definida
  - `marginal`: vantagem pequena ou sensivel ao preco
  - `unclear`: leitura sem vantagem clara
  - `none`: sem valor identificavel

### Risk Load

- Mostra o peso do risco e da incerteza.
- Responde a esta pergunta: quao fragil e esta ideia?
- Leitura pratica:
  - `low`: risco controlado
  - `medium`: risco real, mas gerivel
  - `high`: risco elevado
  - `extreme`: risco demasiado alto

### Verdict

- E a decisao final do sistema.
- E o campo que diz se faz sentido entrar, passar, esperar ou assumir falta de base.

### Red Flags

- Mostra os sinais que enfraquecem a tese.
- Pode incluir:
  - dados incompletos
  - informacao desatualizada
  - tese demasiado narrativa
  - risco nao compensado
  - contexto importante por confirmar

### Stability / Confidence Note

- E uma nota curta sobre a estabilidade da analise.
- Ajuda a perceber se a leitura esta relativamente limpa ou se depende de fatores ainda instaveis.

### Regra pratica de leitura

- Nunca olhar apenas para o `Verdict`.
- O `Verdict` deve ser lido em conjunto com:
  - `Data Quality`
  - `Edge Quality`
  - `Risk Load`
  - `Red Flags`
  - `Stability / Confidence Note`

---

## 6. Significado dos resultados (Decision Gate)

### Enter

- Significa que, dentro do sistema, faz sentido entrar.
- Normalmente implica:
  - dados suficientes
  - edge clara
  - risco controlado
  - ausencia de red flags criticas por resolver

### Pass

- Significa que nao ha valor suficiente para entrar.
- Pode acontecer porque:
  - o preco nao compensa
  - a edge nao e clara
  - o risco e alto demais
  - a leitura existe, mas nao chega para justificar entrada

### Watchlist

- Significa esperar por confirmacao.
- A ideia pode ter valor, mas ainda falta algo importante.
- Exemplos:
  - confirmar lineups
  - confirmar lesoes
  - esperar por qualifying
  - esperar por weather
  - esperar por melhor preco

### Insufficient Data

- Significa que nao ha base suficiente para uma analise responsavel.
- Nao deve ser tratado como quase-enter.
- E um resultado valido e disciplinado.

---

## 7. Boas praticas

- Nao forcar entradas.
- Aceitar `pass` como resultado valido.
- Respeitar `red flags`.
- Nao ignorar `risk load`.
- Usar o sistema sempre com a mesma disciplina.
- Fornecer o maximo de contexto util sempre que possivel.
- Reavaliar quando houver atualizacoes relevantes.
- Tratar `watchlist` como espera ativa, nao como entrada adiada automaticamente.

---

## 8. Erros comuns a evitar

- Confiar apenas na leitura do evento sem olhar para o mercado.
- Ignorar as odds.
- Usar dados incompletos como se fossem suficientes.
- Transformar `watchlist` em entrada sem confirmacao.
- Ignorar um `risk load` alto porque a ideia parece boa.
- Desvalorizar `red flags`.
- Construir uma tese demasiado narrativa sem evidencia suficiente.
- Olhar so para o `Verdict` e ignorar o resto do output.

---

## Nota final

- Este sistema funciona melhor quando e usado de forma consistente.
- O objetivo nao e encontrar sempre uma entrada.
- O objetivo e decidir melhor.
