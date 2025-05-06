# 04 - ⚙️ Generator

## Descrição
O padrão Generator é utilizado em fluxos iterativos, onde um divisor distribui tarefas para agentes especialistas, um gerador compila as respostas e pode haver ciclos de feedback para refinamento contínuo. Esse padrão é muito útil em processos criativos e de melhoria incremental.

### Características
- **Iteratividade:** O fluxo pode ser repetido várias vezes até atingir o resultado desejado.
- **Especialização:** Cada agente trata de um aspecto específico (ex: codificação, documentação, debugging).
- **Ciclo de feedback:** O resultado pode ser avaliado e refinado em novas iterações.

### Quando usar
- Geração automática de código e documentação
- Processos de design assistido por IA
- Workflows de revisão e melhoria contínua

### Vantagens
- Melhoria incremental da qualidade
- Flexibilidade para ajustes durante o processo
- Facilita automação de tarefas complexas

### Desvantagens
- Pode demandar mais tempo de processamento
- Complexidade de orquestração
- Dependência de feedbacks corretos

## Diagrama
```
Usuário
  |
  v
+--------+
| Divisor|
+--------+
  |   |   |
  v   v   v
+-----+  +--------------+  +----------+
|Coding|  |Documentation|  |Debugging |
+-----+  +--------------+  +----------+
   \         |         /
    +---------+--------+
              |
         +----------+
         |Generator |
         +----------+
              |
           Output
```

## Exemplo de Código (FastAPI + LangChain)
```python
from fastapi import FastAPI
from langchain.llms import OpenAI
from langchain.prompts import PromptTemplate

app = FastAPI()

coding_prompt = PromptTemplate("Implemente a função: {input}")
doc_prompt = PromptTemplate("Documente a função: {input}")
debug_prompt = PromptTemplate("Encontre bugs na função: {input}")
gen_prompt = PromptTemplate("Gere o pacote final a partir dos resultados: {input}")
llm = OpenAI(temperature=0)

def generator_pipeline(query: str):
    code = (coding_prompt | llm).run({"input": query})
    doc = (doc_prompt | llm).run({"input": code})
    debug = (debug_prompt | llm).run({"input": code})
    final = (gen_prompt | llm).run({"input": f"{code}\n{doc}\n{debug}"})
    return final

@app.post("/gerar/")
def gerar(query: str):
    return {"output": generator_pipeline(query)}
```

---

## Architecture Haiku

**Descrição breve do sistema:**
Pipeline iterativo que gera, documenta, depura e compila código automaticamente, com feedback entre etapas.

**Principais objetivos de negócio:**
- Automatizar geração de software
- Reduzir retrabalho
- Garantir qualidade e documentação

**Principais restrições identificadas:**
- Complexidade do fluxo
- Dependência de feedbacks corretos
- Custo computacional

**Prioridade dos atributos de qualidade:**
Qualidade > Automação > Desempenho

**Principais decisões de design:**
- FastAPI para expor a API
- LangChain para orquestração iterativa
- OpenAI como LLM subjacente 