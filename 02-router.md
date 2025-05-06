# 🛣️ Router

> Padrão de roteamento centralizado para sistemas multi-agente.

## Descrição
O padrão Router utiliza um agente central responsável por receber as solicitações e encaminhá-las para agentes especialistas, de acordo com o tipo de tarefa ou contexto. Esse padrão é muito útil quando há diferentes tipos de processamento ou serviços que podem ser acionados dinamicamente.

## Diagrama
```
Usuário
   |
   v
+----------------+
|   TravelAgent  |
+----------------+
     /      \
    v        v
+-----------+   +-----------+
| Flight    |   |  Hotel    |
|  Agent    |   |  Agent    |
+-----------+   +-----------+
    |              |
    v              v
Flight Out     Hotel Out
```

### Características
- **Centralização da decisão:** Um agente router decide qual especialista deve tratar cada requisição.
- **Flexibilidade:** Permite adicionar ou remover especialistas sem alterar o fluxo principal.
- **Escalabilidade horizontal:** Novos especialistas podem ser adicionados conforme a demanda.

### Quando usar
- Sistemas de atendimento ao cliente (roteamento para agentes de pagamento, suporte, etc.)
- Orquestração de microserviços
- Gateways de API

### Vantagens
- Redução de acoplamento entre agentes
- Facilidade para manutenção e evolução
- Permite lógica de roteamento sofisticada

### Desvantagens
- Ponto único de falha (se o router cair, o sistema para)
- Pode se tornar gargalo em sistemas de alta demanda

## Exemplo de Código (FastAPI + LangChain)
```python
from fastapi import FastAPI
from langchain.llms import OpenAI
from langchain.prompts import PromptTemplate

app = FastAPI()

flight_prompt = PromptTemplate("Procure voos para: {input}")
hotel_prompt = PromptTemplate("Procure hotéis para: {input}")
llm = OpenAI(temperature=0)

def router(query: str):
    if "voo" in query.lower():
        return flight_prompt | llm
    elif "hotel" in query.lower():
        return hotel_prompt | llm
    else:
        return "Tipo de consulta não suportado."

@app.post("/consulta/")
def consulta(query: str):
    agente = router(query)
    if isinstance(agente, str):
        return {"output": agente}
    return {"output": agente.run({"input": query})} 