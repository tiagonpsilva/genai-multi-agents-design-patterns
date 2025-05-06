# 🔗 Sequential

> Padrão de processamento sequencial para sistemas multi-agente.

## Descrição
O padrão Sequential é um dos mais simples e clássicos em sistemas multi-agente. Nele, agentes são organizados em uma cadeia linear, onde cada agente executa uma etapa específica do processamento e passa o resultado para o próximo agente da sequência. Esse padrão é ideal para fluxos de trabalho bem definidos, onde cada etapa depende do resultado da anterior.

## Diagrama
```
Usuário
   |
   v
+----------+     +----------+     +----------+
| Agent 1  | --> | Agent 2  | --> | Agent 3  |
+----------+     +----------+     +----------+
      |_________________________________|
                   |
                Output
```

### Características
- **Determinismo:** O fluxo é previsível e fácil de rastrear.
- **Facilidade de debug:** Como cada etapa é isolada, identificar falhas é mais simples.
- **Baixa paralelização:** O processamento é sequencial, o que pode limitar o desempenho em tarefas que poderiam ser paralelizadas.

### Quando usar
- Pipelines de processamento de dados (ETL)
- Processos de validação e transformação em série
- Workflows de aprovação

### Vantagens
- Simplicidade de implementação
- Facilidade de manutenção
- Clareza no fluxo de dados

### Desvantagens
- Baixa escalabilidade para tarefas independentes
- Latência acumulada em cadeias longas

## Exemplo de Código (FastAPI + LangChain)
```python
from fastapi import FastAPI
from langchain.chains import SequentialChain
from langchain.llms import OpenAI
from langchain.prompts import PromptTemplate

app = FastAPI()

# Definindo prompts para cada agente
prompt1 = PromptTemplate("Corrija o texto: {input}")
prompt2 = PromptTemplate("Resuma o texto: {input}")
prompt3 = PromptTemplate("Traduza para inglês: {input}")

llm = OpenAI(temperature=0)

chain = SequentialChain(
    chains=[
        prompt1 | llm,
        prompt2 | llm,
        prompt3 | llm
    ]
)

@app.post("/processar/")
def processar(texto: str):
    resultado = chain.run({"input": texto})
    return {"output": resultado}
``` 