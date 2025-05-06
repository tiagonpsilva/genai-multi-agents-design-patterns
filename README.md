# 🤖 Padrões de Design para Multi-Agentes

> Coleção de padrões arquiteturais para sistemas multi-agente, com exemplos práticos e diagramas ilustrativos.

## 📚 Índice
- [🤖 Padrões de Design para Multi-Agentes](#-padrões-de-design-para-multi-agentes)
  - [📚 Índice](#-índice)
  - [Sobre](#sobre)
  - [Objetivo](#objetivo)
  - [Estrutura de Pastas](#estrutura-de-pastas)
  - [Padrões Documentados](#padrões-documentados)
  - [Exemplos](#exemplos)
    - [Sequential (ASCII Art)](#sequential-ascii-art)
    - [Router (ASCII Art)](#router-ascii-art)
  - [Links Úteis](#links-úteis)

## Sobre
Este repositório reúne, explica e exemplifica padrões de arquitetura para sistemas multi-agente, facilitando o entendimento e aplicação desses conceitos em projetos reais.

## Objetivo
Oferecer uma referência prática e visual para arquiteturas de agentes, promovendo boas práticas e acelerando o aprendizado sobre o tema.

## Estrutura de Pastas
```
/
├── 01-sequential.md         # Padrão Sequencial
├── 02-router.md             # Padrão Router
├── 03-parallel.md           # Padrão Paralelo
├── 04-generator.md          # Padrão Generator
├── 05-network.md            # Padrão Network
├── 06-autonomous-agents.md  # Padrão Agentes Autônomos
├── examples/                # Exemplos práticos
└── README.md                # Documentação principal
```

## Padrões Documentados
- [Sequential](01-sequential.md)
- [Router](02-router.md)
- [Parallel](03-parallel.md)
- [Generator](04-generator.md)
- [Network](05-network.md)
- [Autonomous Agents](06-autonomous-agents.md)

## Exemplos

### Sequential (ASCII Art)
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

### Router (ASCII Art)
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

## Links Úteis
- [Badges para GitHub](https://home.aveek.io/GitHub-Profile-Badges/)
- [Multi-Agent Systems (Wikipedia)](https://en.wikipedia.org/wiki/Multi-agent_system) # genai-multi-agents-design-patterns
