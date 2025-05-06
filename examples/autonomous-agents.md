# 06 - 🤖 Autonomous Agents

## Descrição
O padrão Autonomous Agents é caracterizado por agentes descentralizados que interagem entre si sem a necessidade de um orquestrador central. Cada agente é responsável por suas próprias decisões e ações, promovendo máxima autonomia e resiliência do sistema.

### Características
- **Descentralização:** Não há ponto único de controle ou falha.
- **Autonomia:** Cada agente pode agir e se adaptar de acordo com o contexto.
- **Interação peer-to-peer:** Comunicação direta entre agentes.

### Quando usar
- Sistemas embarcados autônomos (robótica, IoT)
- Ambientes dinâmicos e imprevisíveis
- Simulações de ecossistemas ou mercados

### Vantagens
- Alta robustez e tolerância a falhas
- Adaptação dinâmica a mudanças
- Escalabilidade natural

### Desvantagens
- Dificuldade de monitoramento e depuração
- Sincronização descentralizada pode ser complexa
- Possível redundância de esforços

## Diagrama
```
Usuário
  |
  v
+--------+    <---->   +--------+
| Agent1 | <---------> | Agent2 |
+--------+             +--------+
   |                      |
 Output                Output
```

## Exemplo de Código (LangChain)
```python
from langchain.llms import OpenAI
from langchain.prompts import PromptTemplate

# Dois agentes autônomos trocando mensagens
agent1_prompt = PromptTemplate("Agente 1 recebeu: {input}. Responda para o Agente 2.")
agent2_prompt = PromptTemplate("Agente 2 recebeu: {input}. Responda para o Agente 1.")
llm = OpenAI(temperature=0)

mensagem = "Iniciar colaboração"
for _ in range(3):
    resposta1 = (agent1_prompt | llm).run({"input": mensagem})
    resposta2 = (agent2_prompt | llm).run({"input": resposta1})
    mensagem = resposta2
print("Última mensagem trocada:", mensagem)
```

---

## Architecture Haiku

**Descrição breve do sistema:**
Agentes autônomos trocam informações diretamente, sem orquestrador, para resolver tarefas colaborativas.

**Principais objetivos de negócio:**
- Eliminar ponto único de falha
- Maximizar autonomia
- Permitir adaptação dinâmica

**Principais restrições identificadas:**
- Dificuldade de monitoramento
- Sincronização descentralizada
- Complexidade de depuração

**Prioridade dos atributos de qualidade:**
Autonomia > Robustez > Observabilidade

**Principais decisões de design:**
- LangChain para modelar agentes
- Comunicação peer-to-peer
- Sem API centralizada 