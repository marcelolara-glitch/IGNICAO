# CASO_001 — TUTUSDT (perpétuo)

**Caminho canônico proposto:** `docs/casos/CASO_001_TUTUSDT.md`
**Status:** registro de exposição — append-only, não editar retroativamente
**Data do registro:** 2026-08-09 (UTC)
**Origem:** menção do Marcelo em chat de arquitetura, com magnitude e direção
já conhecidas.

---

## 1. Natureza deste documento

Este documento **não é uma análise**. É uma entrada obrigatória no ledger de
exposição (Regra 4) e uma delimitação prévia do que pode e do que não pode
ser feito com este caso.

Nenhum dado de TUTUSDT foi examinado no momento deste registro. Nenhuma
hipótese sobre a causa do movimento foi adotada.

---

## 2. Registro de exposição

| Campo | Valor |
|---|---|
| Símbolo | `TUTUSDT` (perpétuo) |
| Exchange de referência | a determinar (F1 ainda aberta) |
| Janela alegada | ~10 dias, data exata **não determinada** |
| Magnitude alegada | ~+2000%, **não verificada** |
| Fonte da alegação | memória/observação do Marcelo |
| Conhecimento prévio no momento do registro | direção (alta), ordem de grandeza, existência do evento |
| P&L pessoal associado | sem posição; exposição por observação de tela apenas |

### 2.1 Consequência imediata (Regra 4)

`[Certo]` **TUTUSDT está desqualificado como OOS primário em IGNIÇÃO, de
forma permanente e irreversível.** Qualquer resultado positivo em que TUT
contribua para a estatística de decisão é evidência contaminada e não pode
sustentar veredito de F3+ em diante.

`[Certo]` A contaminação foi consumada no momento em que o caso foi
verbalizado com outcome conhecido. Registrar o caso não aumenta o dano;
não registrar seria violação do ledger.

---

## 3. Status epistêmico do que se sabe

| Afirmação | Tag | Observação |
|---|---|---|
| Existe perp `TUTUSDT` listado em múltiplas exchanges | `[Provável]` | consistente entre fontes públicas |
| Houve movimento de alta de grande magnitude | `[Provável]` | relatado, não medido |
| A magnitude foi ~+2000% em ~10 dias | `[Suposição]` | fontes públicas devolvem preços mutuamente incoerentes; **exige medição em klines da exchange** |
| A causa envolveu short squeeze / liquidações / listagem de perp | `[Suposição]` | narrativa de mídia de exchange, não é evidência |
| A janela exata do evento | `[Suposição]` | indeterminada |

`[Certo]` **Nenhuma frase causal sobre TUT pode ser escrita em documento de
IGNIÇÃO até que a janela e a magnitude estejam medidas por script contra a
API da exchange.** §0 aplica-se integralmente.

---

## 4. Proibições derivadas deste caso

As seguintes ações são **vedadas** e sua proposta constitui reabertura de
família encerrada, exigindo adjudicação registrada:

1. **Proibido** construir, ajustar ou calibrar qualquer regra de detecção
   usando TUT como alvo, exemplo positivo ou caso de validação.
2. **Proibido** alterar limiar, janela ou forma funcional da definição de
   evento da F0 com a justificativa de "incluir TUT". Isso é morte por
   invalidação (Regra 9), não conserto.
3. **Proibido** derivar feature preditiva a partir de OHLCV+volume de TUT.
   É a família barrada pela cláusula de fronteira.
4. **Proibido** promover qualquer observação sobre TUT a premissa ou a
   candidata (Regra 6). Este caso é exploratório por definição.
5. **Proibido** generalizar de n=1. "Casos como esse" é uma classe que não
   existe até o censo da F2 definir a população e contá-la.

---

## 5. Usos legítimos (os únicos três)

### 5.1 Teste de recall da definição de evento congelada

Aplicar a definição de evento **já escrita em `PRE_REGISTRO_F0.md`**, sem
qualquer modificação, ao histórico de TUT.

- Resultado A — a definição marca TUT: a definição sobrevive ao teste.
  Nenhuma ação.
- Resultado B — a definição não marca TUT: registra-se a divergência como
  **observação**, não como defeito. Qualquer alteração de limiar em resposta
  a este resultado é morte por invalidação.

Este teste só é executável **depois** que a definição de evento estiver
desambiguada (ponto de adjudicação nº 2 da `EMENDA_01_F0`). Antes disso, o
teste não é bem-definido.

### 5.2 Especificação de requisitos de captura (uso primário)

A pergunta correta não é "como pegar TUT". É:

> **Qual stream, com qual granularidade e com qual latência de observação,
> teria carregado assinatura antes do movimento — e desses, quais não são
> recuperáveis retroativamente?**

Isso alimenta diretamente o teto de escopo v1 (3 classes de dado, 30
símbolos, 1 exchange). Inventário a produzir:

| Classe de dado | Recuperável retroativamente? | Tag | Ação |
|---|---|---|---|
| OHLCV / klines | sim, histórico longo | `[Provável]` | contexto e definição de evento apenas — **nunca preditor** |
| aggTrades / tape | provavelmente sim, via dumps diários | `[Provável]` | verificar empiricamente cobertura e granularidade |
| Open Interest | apenas janela curta via REST | `[Provável]` | **candidato a captura contínua** |
| Funding rate | histórico disponível, baixa frequência | `[Provável]` | verificar granularidade real |
| Liquidações | **não recuperável** | `[Suposição]` | **candidato prioritário a captura contínua** |
| Book / profundidade | **não recuperável** | `[Provável]` | avaliar custo contra teto de escopo |

`[Certo]` Cada linha desta tabela é hipótese até ser medida contra a API.
Nenhuma decisão de escopo pode ser tomada sobre ela no estado atual.

### 5.3 Estimativa de ordem de grandeza para o censo

O caso pode informar a expectativa de **quantos** eventos de magnitude
comparável existem na população — número que a F2 vai medir. Se o censo
devolver contagem incompatível com a intuição formada por este caso, a
intuição está errada, não o censo.

---

## 6. Perguntas a responder ANTES de olhar qualquer dado de TUT

Pré-registro deste mini-estudo. Congelar antes de executar:

1. Qual exchange é a referência? (bloqueado pela F1 — ponto de adjudicação nº 6)
2. Qual a definição de evento vigente e desambiguada? (bloqueado — ponto nº 2)
3. Qual a regra de deduplicação? (bloqueado — ponto nº 3)
4. TUT satisfaz os critérios de admissão ao universo **congelados**, avaliados
   sem referência ao seu retorno? Se não satisfaz, o caso é irrelevante para
   IGNIÇÃO e este documento fecha aqui.
5. O símbolo existia no universo no início da janela, ou foi listado durante
   ela? (viés de sobrevivência — ponto nº 5)

`[Certo]` **Enquanto 1–3 estiverem abertos, nenhuma medição sobre TUT deve
ser executada.** Medir agora e definir depois é olhar o resultado antes do
critério.

---

## 7. Critério de morte deste caso

Este caso é encerrado, sem resultado, se qualquer uma ocorrer:

- TUT não satisfizer os critérios de admissão congelados do universo;
- a janela do evento for anterior ao início da coleta contínua **e** todas as
  classes de dado não-OHLCV relevantes forem irrecuperáveis — nesse cenário o
  caso não é estudável e vira apenas insumo de especificação de captura;
- surgir pressão para ajustar definição de evento em função dele.

Encerramento por qualquer desses motivos é a máquina funcionando.

---

## 8. Pendências para o Marcelo

- [ ] Declarar P&L pessoal associado a TUT, se houver (§2). Campo obrigatório.
- [ ] Declarar se houve exposição a outros símbolos com movimento análogo no
      mesmo período — cada um exige entrada própria no ledger.
- [ ] Confirmar caminho canônico do ledger de exposição no repositório.

---

## 9. Nota de método

`[Provável]` O impulso de partir de um caso vívido e conhecido é o mesmo que
produziu os resultados negativos dos dois projetos anteriores. A diferença
em IGNIÇÃO não é evitar o impulso — é registrá-lo, delimitá-lo e impedir que
ele contamine a estatística de decisão. Este documento é esse registro.
