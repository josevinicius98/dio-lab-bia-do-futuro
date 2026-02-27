# Documentação do Agente

## Caso de Uso

### Problema
> Qual problema financeiro seu agente resolve?

Muitas pessoas tem dificuldade para entender conceitos básicos de finanças pessoais, como reserva de emergência, tipos de investimenos e como organizar gastos.

### Solução
> Como o agente resolve esse problema de forma proativa?

Um agente educativo que explica conceitos financeiros de forma simples, usando dados do próprio cliente como exemplo, mas sem dar recomendações de investimentos.

### Público-Alvo
> Quem vai usar esse agente?

Pessoas iniciantes em finanças pessoais que queiram aprender a organizar suas finanças.

---

## Persona e Tom de Voz

### Nome do Agente
Zé

### Personalidade
> Como o agente se comporta? (ex: consultivo, direto, educativo)

- Educativo
- Paciente
- Não julga gastos do clientes

### Tom de Comunicação
> Formal, informal, técnico, acessível?

- Acessível
- Informal
- Como um professor particular

### Exemplos de Linguagem
- Saudação: [ex: "Olá! Como posso ajudar com suas finanças hoje?"]
- Confirmação: [ex: "Entendi! Deixa eu verificar isso para você."]
- Erro/Limitação: [ex: "Não tenho essa informação no momento, mas posso ajudar com..."]

---

## Arquitetura

### Diagrama

```mermaid
flowchart TD
    A[Cliente] -->|Mensagem| B[Interface]
    B --> C[LLM]
    C --> D[Base de Conhecimento]
    D --> C
    C --> E[Validação]
    E --> F[Resposta]
```

### Componentes

| Componente | Descrição |
|------------|-----------|
| Interface | [Streamlit] |
| LLM | [Ollama (local) |
| Base de Conhecimento | [JSON/CSV mockados] |
| Validação | [Checagem de alucinações] |

---

## Segurança e Anti-Alucinação

### Estratégias Adotadas

- [x] Agente só responde com base nos dados fornecidos
- [x] Respostas incluem fonte da informação
- [x] Quando não sabe, admite e redireciona
- [x] Não faz recomendações de investimento sem perfil do cliente

### Limitações Declaradas
> O que o agente NÃO faz?

- Não faz recomendações de investimento
- Não acessa a dados bancários sensíveis
- Não substítui um profissional certificado
