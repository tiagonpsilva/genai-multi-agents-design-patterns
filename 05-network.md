# 🌐 Network

> Padrão de colaboração totalmente conectada para sistemas multi-agente.

## Descrição
O padrão Network representa um modelo colaborativo totalmente conectado, onde um meta-agente coordena especialistas que podem interagir entre si de forma bidirecional. Esse padrão é indicado para cenários complexos, onde diferentes agentes precisam compartilhar informações e colaborar ativamente.

## Índice
- [Descrição](#descrição)
- [Diagrama](#diagrama)
- [Características](#características)
- [Quando usar](#quando-usar)
- [Vantagens](#vantagens)
- [Desvantagens](#desvantagens)
- [Exemplo de Código](#exemplo-de-código-fastapi--langchain)

## Diagrama
```
Usuário
   |
   v
+------------+
| MetaAgent  |
+------------+
   /      \
  v        v
+---------+   +----------+
| Coding  |<->| Debugging|
+---------+   +----------+
   \\         //
    +---------+
         |
      Output
```

### Características
- **Colaboração intensa:** Agentes especialistas podem se consultar e trocar informações livremente.
- **Meta-agente:** Um agente central supervisiona e coordena a colaboração.
- **Bidirecionalidade:** Comunicação entre agentes não é restrita a um único sentido.

### Quando usar
- Projetos de design arquitetural
- Revisão cruzada de código, segurança e compliance
- Soluções que exigem múltiplas perspectivas simultâneas

### Vantagens
- Alta qualidade das soluções geradas
- Redução de erros por meio de revisões cruzadas
- Flexibilidade para resolver problemas complexos

### Desvantagens
- Complexidade de comunicação e sincronização
- Maior custo de coordenação
- Dificuldade de monitoramento

## Exemplo de Código (FastAPI + LangChain)
```python
from fastapi import FastAPI
from langchain.llms import OpenAI
from langchain.prompts import PromptTemplate

app = FastAPI()

meta_prompt = PromptTemplate("Coordene especialistas para: {input}")
coding_prompt = PromptTemplate("Implemente: {input}")
debug_prompt = PromptTemplate("Depure: {input}")
llm = OpenAI(temperature=0)

def network_pipeline(query: str):
    meta = (meta_prompt | llm).run({"input": query})
    code = (coding_prompt | llm).run({"input": meta})
    debug = (debug_prompt | llm).run({"input": code})
    # Simula interação entre especialistas
    return f"Meta: {meta}\nCode: {code}\nDebug: {debug}"

@app.post("/network/")
def network(query: str):
    return {"output": network_pipeline(query)}
``` 