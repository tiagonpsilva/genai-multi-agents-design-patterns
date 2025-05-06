# 🪄 Parallel

> Padrão de execução paralela para sistemas multi-agente.

## Descrição
O padrão Parallel permite que uma tarefa seja dividida em subtarefas independentes, processadas simultaneamente por diferentes agentes. Após o processamento paralelo, os resultados são agregados para formar a resposta final. Esse padrão é fundamental para cenários onde a velocidade e a eficiência são essenciais.

## Diagrama
```
Usuário
   |
   v
+----------+
| Divisor  |
+----------+
   |     |
   v     v
+-------------+     +-------------------+
| Web Search  |     | Database Search   |
+-------------+     +-------------------+
   |                     |
   v                     v
   +---------------------+
   |     Agregador       |
   +---------------------+
            |
         Output
```

### Características
- **Divisão de trabalho:** Um agente divisor separa a tarefa em partes menores.
- **Execução simultânea:** Subtarefas são processadas em paralelo, reduzindo o tempo total de resposta.
- **Agregação de resultados:** Um agente agregador reúne e consolida as respostas dos agentes paralelos.

### Quando usar
- Recuperação de informações em múltiplas fontes
- Análise de grandes volumes de dados
- Processamento de tarefas independentes

### Vantagens
- Aumento significativo de desempenho
- Redução de latência
- Escalabilidade horizontal

### Desvantagens
- Complexidade na agregação dos resultados
- Dificuldade de sincronização
- Possível aumento de custo computacional

## Exemplo de Código (FastAPI + LangChain)
```python
from fastapi import FastAPI
from langchain.llms import OpenAI
from langchain.prompts import PromptTemplate
import asyncio

app = FastAPI()

web_prompt = PromptTemplate("Busque na web: {input}")
db_prompt = PromptTemplate("Busque no banco de dados: {input}")
llm = OpenAI(temperature=0)

async def run_agent(agent, query):
    return agent.run({"input": query})

@app.post("/buscar/")
async def buscar(query: str):
    web_agent = web_prompt | llm
    db_agent = db_prompt | llm
    results = await asyncio.gather(
        run_agent(web_agent, query),
        run_agent(db_agent, query)
    )
    return {"output": " | ".join(results)} 