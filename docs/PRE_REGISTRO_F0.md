# PRÉ-REGISTRO F0 — PROJETO IGNIÇÃO
### Definição de escopo, evento e critérios de morte · v1 · 2026-08-05

> **Status:** documento de pré-registro. Fixa definições **antes** de qualquer
> exame de dado. Torna-se imutável no merge ao repositório próprio do projeto.
> Enquanto o repositório não existir, esta versão é rascunho ratificável —
> mas as definições numéricas da §5 e §7 **já estão congeladas por decisão de
> Marcelo em 2026-08-05** e não podem ser alteradas após o primeiro censo.
>
> **Sucede:** `HANDOFF — Projeto IGNIÇÃO v0` (2026-08-01), que é insumo
> exploratório e **não** tem força de pré-registro.
>
> **Não bloqueia nem é bloqueado por:** Ciclo 2 do SMC Monitor (forward em
> curso, T0 = 2026-08-03, veredito em 2026-12-03). Frentes independentes.

---

## §0. Convenções vigentes

`[Certo]` evidência forte · `[Provável]` inferência forte · `[Suposição]`
preenchimento de lacuna.

Regras herdadas e vigentes: pré-registro antes do dado · ledger append-only ·
cemitério com registro · exploratório nunca promove · nenhuma assinatura é
descartada, todas retornam ao acervo · veredito único ao fim de janela, sem
decisão intermediária.

---

## §1. Justificativa aprovada e justificativa reprovada

**Aprovada:** construir um ativo de dados irreversível (§5.2 do handoff v0 —
OI, funding, tape e book em alta frequência não são recuperáveis
retroativamente) e testar uma hipótese em cima dele.

**Reprovada:** encontrar uma estratégia lucrativa porque as anteriores não
deram. O Setup Atirador encerrou uma família; o Ciclo 1 do SMC Monitor
encerrou outra, com nove assinaturas e zero edge validado fora de amostra.
Se a motivação for "o outro não deu, este vai dar", o projeto nasce viciado.

**Cenário modal declarado antes do dado:** morte na F2. [Provável] Isso é a
máquina funcionando.

---

## §2. Cláusula de fronteira (dura, herdada)

> Qualquer detector construído **apenas** sobre OHLCV+volume está DENTRO da
> família já encerrada por dois projetos e é **proibido** como feature
> preditiva principal. IGNIÇÃO só é admissível porque usa outra classe de
> dado: derivativos, fluxo, microestrutura e metadado de calendário.
>
> Candle entra como **contexto** e como **definição de evento** — nunca como
> preditor.

### §2.1 PONTO ABERTO — estatuto da análise gráfica

Marcelo manifestou intenção de investigar "padrão de comportamento, tanto de
análise gráfica quanto de fundamentos, que antecede a maioria dos pumps".

Análise gráfica é OHLCV. A intenção **conflita diretamente** com a cláusula
acima. Este ponto fica registrado como **aberto** e exige adjudicação
explícita e escrita antes da F4 (feature engineering).

Três desfechos possíveis, a escolher — não a improvisar:

1. **Manter a fronteira.** Padrão gráfico não entra. Recomendado. [Provável]
2. **Admitir OHLCV como covariável de controle**, nunca como preditor
   isolado, com a exigência de que qualquer resultado seja reportado também
   no modelo sem ela. Admissível.
3. **Relaxar a fronteira.** Constitui reabertura formal de família encerrada;
   exige documento próprio justificando por que a terceira tentativa difere
   das duas anteriores. Não recomendado.

Até a adjudicação, vale o desfecho 1.

---

## §3. Fenômeno alvo

Escopo v1 = **B primário + C rotulado em coorte separada**, com a taxonomia
declarada **incompleta e expansível** (§3.2).

| Cód | Fenômeno | Estatuto v1 |
|---|---|---|
| A | P&D coordenado em canal fechado (Telegram/Discord) | **FORA.** Decisão de Marcelo: não é o objeto de busca. Sem escuta de canal. |
| B | Short squeeze alavancado (OI subindo, funding comprimido/negativo, cascata de liquidação) | **ALVO PRIMÁRIO** |
| C | Evento de catálogo (listagem, unlock, anúncio, **mudança de status regulatório de token em exchange**) | **COORTE ROTULADA À PARTE** |
| D | Rotação de narrativa / beta de setor | **FORA.** É cross-section, outra frente. |

### §3.1 Por que C é rotulado e não ignorado

Duas razões distintas:

1. **Higiene de amostra.** [Provável] Evento de catálogo não rotulado entra no
   censo de B como se fosse squeeze. Features de OI e funding pareceriam
   preditivas quando estariam capturando o rescaldo de um anúncio. É
   contaminação silenciosa, do tipo que só aparece depois de já se ter
   acreditado no resultado.
2. **Subclasse de C é capturável.** Ver §3.2.

### §3.2 Expansão declarada — triggers de calendário e status

Marcelo identificou um gatilho ausente do handoff v0: **anúncio de
delistagem ou mudança de status de token em exchange** (mecanismo "ST" da
Bybit e análogos), que produz corrida de fundadores/comunidade para elevar
volume e reverter o status.

Este trigger difere estruturalmente do resto de C: [Provável]

- É **calendário conhecido com antecedência de dias**, não corrida de
  latência de milissegundos
- Tem **mecanismo econômico explícito** (agente com incentivo declarado e
  prazo)
- Gera assinatura observável em dado não-OHLCV (volume por exchange, OI,
  funding)

**Consequência para o F0:** a taxonomia A–D **não é fechada**. A F1 tem como
entregável adicional obrigatório o **levantamento sistemático de gatilhos de
calendário/status** em exchanges perp — delistagem, ST e equivalentes,
unlock, migração de contrato, mudança de tier de margem, alteração de regra
de funding. Cada gatilho encontrado entra em tabela com: mecanismo,
antecedência observável, fonte de dado, e se é capturável.

**Restrição que permanece:** todo gatilho novo é avaliado sob a mesma
cláusula de fronteira (§2) e o mesmo desenho caso-controle (§6). Escopo
expansível não significa escopo livre.

---

## §4. Hipótese

> **H0 (nulo):** condicionado às variáveis observáveis em t−Δ, a
> probabilidade de um token perp-listado sofrer evento de ignição em
> [t, t+24h] é indistinguível da taxa base do universo.

> **H1:** existe vetor de features observáveis em t−Δ — derivadas de
> derivativos, fluxo, microestrutura e calendário/status — que separa
> candidatos de não-candidatos com margem que sobrevive a (a) custo de
> execução realista, (b) bootstrap por blocos de calendário, (c) modelo nulo.

**Δ primário: 60 min.** Robustez declarada em Δ ∈ {4h, 24h} — reportados
sempre, **nunca** como melhor-de-N.

---

## §5. Definição de evento de ignição (CONGELADA)

> **Evento de ignição** = retorno de fechamento a fechamento **≥ +40%** em
> janela de **≤ 24h**, em token pertencente ao universo elegível definido na
> §6, medido em candle de 1h no par perp da exchange alvo.

Congelado por decisão de Marcelo em 2026-08-05, **antes** de qualquer
contagem. Não é resultado de tuning e não pode ser ajustado após o censo.

Teste de sanidade aplicado: esta definição sobrevive à pergunta *"isto foi
escolhido para pegar o caso que eu vi na semana passada?"* — o limiar é
redondo, declarado antes da contagem, e não faz referência a nenhum caso
específico.

---

## §6. Universo elegível (critérios de ADMISSÃO, não de exclusão pós-hoc)

**Regra de ouro:** o universo é congelado **antes** de contar qualquer
evento. Olhar os eventos e então decidir quem excluir é seleção na variável
dependente — o erro nº 1 desta linha de pesquisa. [Certo]

Critérios de admissão, avaliados em janela móvel anterior a cada instante
de calendário (nunca com dado do futuro):

1. Perp **operável** na exchange alvo (se não dá para operar, não entra no
   censo)
2. Perp listado há **≥ 30 dias** no instante avaliado (evita o regime
   idiossincrático de listagem nova, que é coorte C própria)
3. Volume mediano diário do perp **≥ US$ 500k** nos 30 dias anteriores
4. Book presente com spread mediano **≤ 0,5%** nos 30 dias anteriores

**Nota explícita:** "altamente manipulado" **não é** critério de exclusão. É
o fenômeno sob estudo. Filtros de liquidez existem por operabilidade, não
por juízo sobre a natureza do movimento.

Os limiares 3 e 4 são pré-registrados. Se a F2 revelar que eles esvaziam o
universo da OKX, isso é **resultado da F2** (e possível critério de morte),
não convite para afrouxá-los.

---

## §7. Critérios de morte (CONGELADOS, pré-registrados antes do censo)

### §7.1 Morte na F2 (censo retrospectivo, 12 meses)

Qualquer um destes, isoladamente, mata o projeto com registro:

| # | Critério | Racional |
|---|---|---|
| M1 | **< 50 eventos** com perp operável em 12 meses | Amostra nunca formará base estatística útil |
| M2 | **> 60% do movimento** ocorre nos primeiros 15 min | Evento inatingível por qualquer detecção realista |
| M3 | **Meia-vida da reversão < 30 min** | Janela de saída menor que latência de execução realista |
| M4 | **≥ 70% dos eventos concentrados em < 10 tokens** | Não é fenômeno de população, é idiossincrasia de alguns ativos |

### §7.2 Morte na F4

Nenhuma feature com separação além do esperado por acaso sob limiar
pré-registrado no fim da F1 → morte com registro.

### §7.3 Morte na F5

Falha em bootstrap por blocos **OU** no modelo nulo **OU** custo total
(taxa + funding + slippage + risco de liquidação) consumindo a margem →
morte com registro, sem renegociação.

### §7.4 Morte por invalidação (a qualquer momento)

Alteração de qualquer definição desta §5, §6 ou §7 após o início do censo
encerra o ciclo por **invalidação**, não por resultado.

---

## §8. Exchange alvo

**Primária v1: OKX.** Justificativa: credencial, símbolos e padrão de
conexão WebSocket já dominados; melhor resposta operacional em projetos
anteriores, sem travas.

### §8.1 PONTO ABERTO — tensão OKX vs Bybit

Registrado como conflito não resolvido, a adjudicar na F1: [Provável]

- Marcelo declarou que a OKX tem **a menor disponibilidade de tokens
  pequenos**
- O universo onde os eventos de ignição vivem é justamente o long-tail
- O gatilho mais promissor identificado (§3.2, ST) é **mecanismo Bybit**

Escolher a exchange por conveniência de conexão e depois estudar um
fenômeno que mora em outra é otimizar a variável errada.

**Entregável obrigatório da F1:** contagem preliminar de símbolos perp
elegíveis (§6) em OKX **e** em Bybit. Se a OKX tiver universo elegível
substancialmente menor, a exchange primária é revista **antes** da F2, com
emenda datada a este documento. Segunda exchange para validação cruzada
permanece adiada para pós-F2.

---

## §9. Tamanho de posição hipotético e o que ele muda

**Declarado:** US$ 20 de margem a 10–20x ⇒ nocional US$ 200–400. Aumento
apenas condicionado a sucesso comprovado, nunca antes.

Duas consequências diretas, ambas importantes:

1. **Impacto de mercado é desprezível nesse nocional.** [Provável] Isso
   **rebaixa a prioridade do coletor de book (F3.3)**, que era o tier mais
   caro da infraestrutura e cuja justificativa central era simulação de
   preenchimento com impacto. Book passa de requisito a **feature
   desejável**, e fica **gateado na sobrevivência da F2**.
2. **O modo de morte dominante deixa de ser impacto e passa a ser
   liquidação.** [Certo] A 20x, ~5% de movimento adverso liquida a posição.
   Pumps revertem violentamente e com gaps. A F5 é **obrigada** a modelar
   liquidação e ADL — não como robustez, como custo de primeira ordem. 10x
   já é agressivo para este ativo; 20x precisa de justificativa própria.

---

## §10. Teto de escopo (substitui o teto de horas)

Teto de horas/semana foi rejeitado por Marcelo — disponibilidade variável
torna a métrica artificial. Substituído por mecanismo equivalente e mais
verificável:

**Teto de escopo v1, congelado:**

- **Máximo 30 símbolos** sob coleta contínua simultânea
- **Máximo 3 classes de dado** em coleta contínua (OI+funding, tape
  agregado, liquidações). Book é a 4ª e está gateada na F2.
- **1 exchange** em coleta contínua até a F2 fechar

**Regra de acionamento:** se a manutenção do coletor exigir intervenção
não-planejada em **3 semanas consecutivas**, a resposta obrigatória é
**cortar escopo** (menos símbolos ou menos classes), nunca absorver o custo.
O corte é registrado em emenda datada.

Racional: depois de meses de coletor rodando, qualquer teto declarado a
posteriori será racionalizado por sunk cost. O teto existe para ser
inconveniente no momento certo.

---

## §11. Ordem de execução

| Fase | Depende de VM? | Quando |
|---|---|---|
| **F1** — literatura + prior art + **levantamento de gatilhos §3.2** + contagem OKX vs Bybit | Não | Imediato |
| **F2** — censo retrospectivo, REST histórico, 12 meses | **Não** | Imediato, em paralelo com F1 |
| **F3.1** — coletor de OI + funding (dado perecível, volumetria baixa) | Sim | Imediato — o dado não volta |
| **F3.2** — coletor de tape agregado | Sim | Após F3.1 estável |
| **F3.3** — coletor de book top-N | Sim | **Gateado na sobrevivência da F2** (§9.1) |
| **F4** — dataset caso-controle | Não | Após F2 sobreviver |
| **F5** — falsificação (bootstrap por blocos + nulo + custo + liquidação) | Não | Após F4 |
| **F6** — shadow forward, 8–12 semanas, veredito único no fim | Sim | Após F5 |
| **F7** — decisão binária: capital ou morte com registro | — | 1 dia |

**Cláusula anti-atalho (§11.1):** entre "o estudo mostrou alpha" e "rodar com
dinheiro" existem F5 e F6 integralmente. [Certo] Alpha em F4 é observação,
não licença de execução. Encurtar essa ponte reproduz exatamente o que o
protocolo do Ciclo 1 do SMC Monitor impediu: a promoção da A4a por
PASS-treino sedutor, que virou FAIL-OOS com inversão de sinal.

---

## §12. Isolamento de infraestrutura

Coleta contínua roda em **partição dedicada na VM do Setup Atirador**, não na
VM do SMC Monitor.

**Regra dura:** [Certo]

- Nenhum processo, banco, cron ou credencial compartilhado com qualquer
  outro projeto. No máximo, a máquina.
- **Quota de disco rígida** na partição, não convenção. Disco cheio derruba
  serviço em silêncio, e é o modo de falha mais provável de coleta contínua.
- **Verificação obrigatória antes de ligar qualquer coletor:** identificar o
  que está de pé na VM do Atirador e se existe janela pré-registrada com
  data de veredito. Se existir, a quota é dimensionada para que o estouro do
  IGNIÇÃO seja impossível de afetá-la. Falha em IGNIÇÃO nunca pode invalidar
  janela alheia.

---

## §13. Ativos herdados e ativos barrados

**Herdado (método, não código):** protocolo de pré-registro e
anti-derivação · ledger append-only e de exposição · disclosure de
contaminação OOS · tagging epistêmico · `AGENTS.md` como esqueleto de
governança · máquina de juiz (bootstrap por blocos + modelo nulo, do Setup
Atirador) · protocolo de shadow forward com veredito único.

**Barrado (Camada D):** engine SMC portada do LuxAlgo · assinaturas A1–A10 ·
FSM de setup · golden dataset · integração Freqtrade e `SMCStrategyCandidate`
· documentos canônicos SMC · lib `smartmoneyconcepts`.

Qualquer proposta futura de usar item barrado constitui reabertura de
família encerrada e exige adjudicação explícita e registrada — não entra por
conveniência de implementação.

---

## §14. O que este documento NÃO decide

- Não autoriza gasto de capital
- Não decide operar nada
- Não promove nenhuma feature
- Não resolve os pontos abertos §2.1 (análise gráfica) e §8.1 (exchange)
- Não altera o Ciclo 2 do SMC Monitor, cuja conduta está congelada até
  2026-12-03

---

## §15. Pontos abertos que devem fechar antes da F4

| # | Ponto | Prazo |
|---|---|---|
| 1 | Estatuto da análise gráfica (§2.1) — desfecho 1, 2 ou 3 | Antes da F4 |
| 2 | Exchange primária (§8.1) — OKX confirmada ou revista para Bybit | Antes da F2 |
| 3 | Limiar de separação da F4 (§7.2) | Fim da F1 |
| 4 | Alavancagem 10x vs 20x (§9.2) | Antes da F5 |

---

*Escrito em 2026-08-05. Definições da §5, §6, §7 e §10 congeladas por decisão
de Marcelo na mesma data, antes de qualquer contagem de evento.*

