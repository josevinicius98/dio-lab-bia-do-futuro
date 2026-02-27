# Base de Conhecimento

## Dados Utilizados

Descreva se usou os arquivos da pasta `data`, por exemplo:

| Arquivo | Formato | Utilização do Zé |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | Contextualizar interações anteriores, ou seja, dar continuidade ao atendimento de forma mais eficiente. |
| `perfil_investidor.json` | JSON | Personalizar as explicações sobre as dúvidas e necessidades de aprendizado do cliente. |
| `produtos_financeiros.json` | JSON | Conhecer os produtos disponíveis para que eles possam ser ensinados ao cliente. |
| `transacoes.csv` | CSV | Analisar padrão de gastos do cliente e usar essas informaçõs de forma didática. |

---

## Adaptações nos Dados

> Dados mockados? Descreva aqui.

Dados mockados e a base aumentada com o uso de IA.

---

## Estratégia de Integração

### Como os dados são carregados?
> Descreva como seu agente acessa a base de conhecimento.

Injetados diretamento no prompt ou carregar os arquivos via código

### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

Para simplificar, podemos simplesmente "injetar" os dados em nosso prompt, garantindo que o Agente tenha melhor contexto possível. Lembrando que, em soluções mais robustas, o ideal é que essas informações sejam carregadas dinâmicamente para que possamos ganhar flexibilidade.

``` text
DADOS DO CLIENTE E PERFIL:
{
  "cliente_id": "C0001",
  "nome": "João Silva",
  "idade": 32,
  "profissao": "Analista de Sistemas",
  "renda_mensal": 5000.00,

  "nivel_conhecimento_financeiro": "iniciante",
  "perfil_investidor": "conservador",
  "aceita_risco": false,
  "preferencia_liquidez": "alta",
  "objetivo_principal": "Construir reserva de emergência",

  "patrimonio_total": 15000.00,
  "reserva_emergencia_atual": 10000.00,
  "reserva_emergencia_meta": 15000.00,

  "despesas_estimadas": {
    "fixas_mensais": 2200.00,
    "variaveis_mensais": 1300.00,
    "economia_alvo_mensal": 700.00
  },

  "preferencias": {
    "canal_preferido": "chat",
    "tom_de_voz": "acessivel_informal",
    "quer_alertas": true,
    "frequencia_alertas": "mensal"
  },

  "metas": [
    {
      "meta_id": "M001",
      "meta": "Completar reserva de emergência",
      "valor_necessario": 15000.00,
      "prazo": "2026-06",
      "prioridade": "alta"
    },
    {
      "meta_id": "M002",
      "meta": "Entrada do apartamento",
      "valor_necessario": 50000.00,
      "prazo": "2027-12",
      "prioridade": "media"
    }
  ]
}

HISTÓRICO DE TRANSAÇÕES DO CLIENTE:
transacao_id,cliente_id,data,descricao,categoria,valor,tipo,meio_pagamento,recorrente,essencial
T0001,C0001,2025-10-01,Salário,receita,5000.00,entrada,transferencia,sim,sim
T0002,C0001,2025-10-02,Aluguel,moradia,1200.00,saida,pix,sim,sim
T0003,C0001,2025-10-03,Supermercado,alimentacao,450.00,saida,cartao_debito,nao,sim
T0004,C0001,2025-10-05,Netflix,lazer,55.90,saida,cartao_credito,sim,nao
T0005,C0001,2025-10-07,Farmácia,saude,89.00,saida,cartao_debito,nao,sim
T0006,C0001,2025-10-10,Restaurante,alimentacao,120.00,saida,cartao_credito,nao,nao
T0007,C0001,2025-10-12,Uber,transporte,45.00,saida,cartao_credito,nao,nao
T0008,C0001,2025-10-15,Conta de Luz,moradia,180.00,saida,pix,sim,sim
T0009,C0001,2025-10-18,Internet,moradia,110.00,saida,pix,sim,sim
T0010,C0001,2025-10-20,Academia,saude,99.00,saida,cartao_credito,sim,nao
T0011,C0001,2025-10-25,Combustível,transporte,250.00,saida,cartao_credito,nao,sim
T0012,C0001,2025-10-28,Aporte Reserva Emergência,reserva,700.00,saida,transferencia,sim,sim

T0013,C0001,2025-11-01,Salário,receita,5000.00,entrada,transferencia,sim,sim
T0014,C0001,2025-11-02,Aluguel,moradia,1200.00,saida,pix,sim,sim
T0015,C0001,2025-11-03,Supermercado,alimentacao,420.00,saida,cartao_debito,nao,sim
T0016,C0001,2025-11-05,Streaming (Netflix),lazer,55.90,saida,cartao_credito,sim,nao
T0017,C0001,2025-11-06,Plano de saúde,saude,180.00,saida,pix,sim,sim
T0018,C0001,2025-11-08,Restaurante,alimentacao,95.00,saida,cartao_credito,nao,nao
T0019,C0001,2025-11-10,Transporte (Uber),transporte,60.00,saida,cartao_credito,nao,nao
T0020,C0001,2025-11-12,Conta de Luz,moradia,175.00,saida,pix,sim,sim
T0021,C0001,2025-11-14,Internet,moradia,110.00,saida,pix,sim,sim
T0022,C0001,2025-11-18,Farmácia,saude,70.00,saida,cartao_debito,nao,sim
T0023,C0001,2025-11-22,Combustível,transporte,230.00,saida,cartao_credito,nao,sim
T0024,C0001,2025-11-26,Aporte Reserva Emergência,reserva,700.00,saida,transferencia,sim,sim

PRODUTOS DISPONÍVEIS PARA ENSINO: 
[
  {
    "produto_id": "P001",
    "nome": "Tesouro Selic",
    "categoria": "renda_fixa_publica",
    "risco": "baixo",
    "rentabilidade": "pós-fixada (referenciada na Selic)",
    "aporte_minimo": 30.00,
    "liquidez": "D+1 (em geral)",
    "prazo_minimo": "sem prazo mínimo obrigatório (pode haver oscilação no curto prazo)",
    "carencia": "nao",
    "tributacao": "IR (tabela regressiva) + possíveis custos/taxas da corretora",
    "garantia": "título público (risco soberano)",
    "indicado_para": "Reserva de emergência e iniciantes (conceito)",
    "alertas": [
      "Pode oscilar no curto prazo por marcação a mercado",
      "Considere manter a reserva com foco em liquidez"
    ]
  },
  {
    "produto_id": "P002",
    "nome": "CDB Liquidez Diária",
    "categoria": "renda_fixa_bancaria",
    "risco": "baixo",
    "rentabilidade": "pós-fixada (ex.: % do CDI)",
    "aporte_minimo": 100.00,
    "liquidez": "D+0 ou D+1 (varia por emissor)",
    "prazo_minimo": "geralmente sem carência (varia)",
    "carencia": "depende",
    "tributacao": "IR (tabela regressiva) e IOF se resgatar muito cedo (conceito)",
    "garantia": "FGC (até limites vigentes, quando elegível)",
    "indicado_para": "Quem busca liquidez e segurança (conceito)",
    "alertas": [
      "Verificar se há carência e regras de resgate",
      "Comparar % do CDI e custos"
    ]
  },
  {
    "produto_id": "P003",
    "nome": "LCI/LCA",
    "categoria": "renda_fixa_bancaria",
    "risco": "baixo",
    "rentabilidade": "pós-fixada (ex.: % do CDI)",
    "aporte_minimo": 1000.00,
    "liquidez": "baixa a média (normalmente sem resgate imediato)",
    "prazo_minimo": "costuma ter carência (ex.: 90 dias ou mais)",
    "carencia": "sim",
    "tributacao": "geralmente isento de IR para pessoa física (conceito)",
    "garantia": "FGC (até limites vigentes, quando elegível)",
    "indicado_para": "Quem pode esperar o prazo e busca eficiência tributária (conceito)",
    "alertas": [
      "Carência pode impedir resgate antes do prazo",
      "Nem sempre serve para reserva de emergência"
    ]
  },
  {
    "produto_id": "P004",
    "nome": "Fundo Multimercado",
    "categoria": "fundo",
    "risco": "medio",
    "rentabilidade": "variável (depende da estratégia do fundo)",
    "aporte_minimo": 500.00,
    "liquidez": "D+1 a D+30 (varia)",
    "prazo_minimo": "médio/longo (conceito)",
    "carencia": "depende",
    "tributacao": "pode ter come-cotas e IR (depende do tipo do fundo)",
    "garantia": "nao se aplica como FGC",
    "indicado_para": "Diversificação com aceitação de oscilações (conceito)",
    "alertas": [
      "Pode ter taxa de administração/performance",
      "Pode oscilar e ter prazos de resgate maiores"
    ]
  },
  {
    "produto_id": "P005",
    "nome": "Fundo de Ações",
    "categoria": "fundo",
    "risco": "alto",
    "rentabilidade": "variável",
    "aporte_minimo": 100.00,
    "liquidez": "D+2 a D+30 (varia)",
    "prazo_minimo": "longo (conceito)",
    "carencia": "depende",
    "tributacao": "IR conforme regras aplicáveis ao tipo de fundo",
    "garantia": "nao se aplica como FGC",
    "indicado_para": "Objetivos de longo prazo com alta tolerância a risco (conceito)",
    "alertas": [
      "Alta volatilidade no curto prazo",
      "Não indicado para reserva de emergência (conceito)"
    ]
  }
]

HISTÓRICO DE ATENDIMENTO DO CLIENTE:
atendimento_id,cliente_id,data_hora,canal,tema,intencao,resumo,fonte_base,resolvido,satisfacao,follow_up
A0001,C0001,2025-09-05T10:12:00,chat,Orçamento mensal,orientacao_orcamento,Cliente pediu ajuda para separar gastos fixos e variáveis e montar regra 50/30/20,faq_conceitos.json,sim,5,nao
A0002,C0001,2025-09-15T14:08:00,chat,CDB,explicacao_produto,Cliente perguntou diferença entre CDB com liquidez diária vs vencimento e como funciona rentabilidade atrelada ao CDI,produtos_financeiros.json,sim,4,nao
A0003,C0001,2025-09-22T09:40:00,telefone,Problema no app,suporte_tecnico,Erro ao visualizar extrato após atualização do app; orientado limpar cache e atualizar versão,suporte_faq.json,sim,4,nao
A0004,C0001,2025-10-01T11:03:00,chat,Tesouro Selic,explicacao_produto,Cliente pediu explicação de Tesouro Selic com foco em reserva e liquidez e alertas de marcação a mercado,produtos_financeiros.json,sim,5,nao
A0005,C0001,2025-10-03T18:22:00,chat,Reserva de emergência,simulacao_meta,Cliente quis calcular quanto falta para completar reserva e quanto poupar por mês até 2026-06,perfil_investidor.json,sim,5,nao
A0006,C0001,2025-10-07T08:55:00,chat,Cartão de crédito,educacao_juros,Cliente pediu explicação de juros do rotativo e por que parcelar pode sair mais caro,faq_conceitos.json,sim,4,nao
A0007,C0001,2025-10-12T20:10:00,chat,Metas financeiras,acompanhamento_progresso,Cliente acompanhou progresso da reserva e pediu sugestão de lembretes mensais (sem recomendação),perfil_investidor.json,sim,5,sim
A0008,C0001,2025-10-18T16:30:00,email,Atualização cadastral,atualizacao_dados,Cliente solicitou atualização de e-mail e telefone; enviado passo a passo e confirmação,suporte_faq.json,sim,5,nao
A0009,C0001,2025-10-25T15:05:00,chat,LCI/LCA,explicacao_produto,Cliente perguntou sobre carência e isenção de IR e por que liquidez não é diária na maioria dos casos,produtos_financeiros.json,sim,4,nao
A0010,C0001,2025-11-02T10:44:00,chat,Gastos do mês,analise_gastos,Cliente pediu resumo por categoria e alerta de gastos recorrentes (streaming/academia),transacoes.csv,sim,5,sim
A0011,C0001,2025-11-10T13:12:00,chat,Fundo multimercado,explicacao_risco,"Cliente pediu entendimento de risco médio, volatilidade e prazo recomendado (sem indicar compra)",produtos_financeiros.json,sim,4,nao
A0012,C0001,2025-11-18T09:20:00,chat,Imposto de renda,duvida_tributacao,Cliente perguntou regra geral de IR em renda fixa e diferença para isentos; orientado como “conceito” e sugerido consultar fonte oficial,faq_conceitos.json,nao,3,sim

```

---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.

```
- Cliente (C0001):

João Silva, 32, Analista de Sistemas. Renda mensal: R$ 5.000. Patrimônio total: R$ 15.000.
Conhecimento financeiro: iniciante. Perfil: conservador, não aceita risco, prefere alta liquidez.
Objetivo principal: Reserva de emergência. Reserva atual: R$ 10.000 | meta: R$ 15.000 (faltam R$ 5.000) | prazo: 2026-06 (prioridade alta).
Outras metas: Entrada do apartamento (R$ 50.000 até 2027-12, prioridade média).
Planejamento (estimado): fixas R$ 2.200, variáveis R$ 1.300, economia-alvo R$ 700/mês.
Preferências UX: canal chat, tom acessível/informal, quer alertas mensais.

- Transações (amostra: out/2025 e nov/2025):

Entradas: R$ 5.000/mês (salário).
Saídas totais (inclui aporte reserva): R$ 3.298,90 (out) | R$ 3.295,90 (nov).
Aporte para reserva (recorrente): R$ 700/mês (out e nov).
Principais categorias (saídas):
Moradia: R$ 1.490 (out) | R$ 1.485 (nov)
Alimentação: R$ 570 (out) | R$ 515 (nov)
Transporte: R$ 295 (out) | R$ 290 (nov)
Saúde: R$ 188 (out) | R$ 250 (nov)
Lazer: R$ 55,90/mês
Reserva: R$ 700/mês
Recorrentes relevantes: Aluguel (R$ 1.200), Luz (~R$ 175–180), Internet (R$ 110), Streaming (R$ 55,90), Aporte reserva (R$ 700) (+ Academia em out; Plano de saúde em nov).
Observação operacional: a amostra sugere “folga” mensal alta (entrada – saídas) ~R$ 1.700/mês, indicando despesas não registradas ou amostra parcial (importante para o agente sinalizar quando fizer análises).

- Histórico de atendimento (set–nov/2025, 12 registros):

Canal predominante: chat. Intenções recorrentes: explicação de produtos (Tesouro Selic, CDB, LCI/LCA), simulação de meta (reserva), educação de juros (cartão), análise de gastos, risco de fundos, suporte/app e atualização cadastral.
Ponto pendente: IR/tributação (A0012) não resolvido, satisfação 3, com follow-up.

- Produtos disponíveis para ensino (sem recomendar compra):

P001 Tesouro Selic: risco baixo, liquidez D+1, IR regressivo; alerta de oscilação curta (marcação a mercado).
P002 CDB Liquidez Diária: risco baixo, liquidez D+0/D+1, IR regressivo/IOF (conceito), possível FGC; checar carência/regras.
P003 LCI/LCA: risco baixo, geralmente carência, isento IR PF (conceito), possível FGC; pode não servir para reserva por liquidez.
P004 Fundo Multimercado: risco médio, liquidez variável, pode ter taxas/come-cotas; oscila e pode ter prazos maiores.
P005 Fundo de Ações: risco alto, longo prazo, volatilidade; não serve para reserva (conceito).
```
