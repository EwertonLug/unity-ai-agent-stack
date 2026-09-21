# 🤖 unity-ai-agent-stack (Stack de Desenvolvimento Unity com IA)

Bem-vindo ao repositório do **unity-ai-agent-stack**. 

Este workflow utiliza ferramentas gratuitas e/ou open source para permitir que agentes de IA interajam diretamente com projetos Unity. Ele combina o protocolo MCP, Unity CLI, Unity Pipeline e Skills especializadas para criar um ambiente de desenvolvimento autônomo e assistido.

---

## 📋 Visão Geral da Stack

| Tecnologia | Função |
| :--- | :--- |
| **OpenCode Desktop** | Interface e agente de IA utilizado como ambiente principal. |
| **Unity MCP** | Comunicação entre o agente de IA e o Unity Editor. |
| **Unity CLI** | Automação e controle do ambiente Unity via terminal. |
| **Unity Pipeline** | (`com.unity.pipeline`) Ponte entre Unity CLI e Unity Editor. |
| **Unity Agent Plugin** | Skills e instruções especializadas para desenvolvimento Unity. |
| **acplugin** | Conversão das Skills do formato Claude Code para formatos compatíveis com outros agentes (incluindo OpenCode). |

---

## 1. OpenCode Desktop
O **OpenCode Desktop** funciona como o ambiente principal onde o agente de IA executa as tarefas de desenvolvimento.

**O agente pode:**
- Analisar o projeto
- Ler e modificar scripts C#
- Criar e alterar arquivos
- Executar comandos
- Utilizar ferramentas externas
- Interagir com o Unity através de MCP
- Utilizar Skills especializadas para compreender workflows específicos de Unity

**Papel no workflow:**
```text
OpenCode ➔ Agente de IA ➔ Skills + Ferramentas ➔ Unity MCP / CLI ➔ Unity Editor
```

## 2. Unity MCP
🔗 **Repositório:** [CoplayDev/unity-mcp](https://github.com/CoplayDev/unity-mcp)

O MCP for Unity funciona como uma ponte entre agentes de IA compatíveis com Model Context Protocol (MCP) e o Unity Editor. Ele permite que o agente execute operações diretamente no ambiente Unity, como:

- Criação e edição de GameObjects
- Gerenciamento de cenas
- Manipulação de assets
- Edição de scripts
- Execução de testes, Profiling e Builds
- Automação de workflows dentro do Unity

*(Projeto open source sob licença MIT).*

**Papel no workflow:**
O MCP é utilizado principalmente quando o agente precisa interagir diretamente com o estado do Editor.
> **Exemplo:**  
> Usuário: *"Crie um Canvas com um botão chamado StartButton."*  
> Fluxo: `OpenCode` ➔ `Unity MCP` ➔ `Unity Editor` ➔ `Canvas + Button criados`

## 3. Unity CLI
A **Unity CLI** (Command-Line Interface) é a ferramenta oficial da Unity para gerenciamento e automação através do terminal. Ela permite:

- Instalar versões do Unity e gerenciar módulos
- Abrir projetos e controlar Editors conectados
- Executar comandos e gerenciar o Unity Pipeline
- Acessar ferramentas para agentes e configurar MCP

*Nota: A Unity atualmente classifica a CLI como experimental, portanto sua API pode sofrer alterações.*

**Papel no workflow:**
Fornece uma camada de automação e controle por terminal.
```text
OpenCode
   │
   ├── Comandos de terminal ➔ Unity CLI ➔ Unity Environment
   │
   └── MCP ➔ Unity Editor
```

## 4. Unity Pipeline (`com.unity.pipeline`)
O Unity Pipeline package é o componente que permite à Unity CLI controlar remotamente o Unity Editor. Ele disponibiliza uma API HTTP local para automação, permitindo execução de comandos, testes, builds e desenvolvimento assistido. *(Destinado ao Unity 6 ou superior).*

**Relação entre CLI e Pipeline:**
```text
Unity CLI ➔ (HTTP) ➔ com.unity.pipeline ➔ Unity Editor
```
**Instalação típica:**
```bash
unity pipeline install
```

## 5. Unity Agent Plugin
🔗 **Repositório:** [Unity-Technologies/unity-agent-plugin](https://github.com/Unity-Technologies/unity-agent-plugin)

Fornece conhecimento e workflows especializados para agentes de IA trabalhando com Unity. Ensina ao agente instruções específicas sobre:
- Arquitetura de projetos e boas práticas
- Workflows do Editor e execução de tarefas
- Utilização das ferramentas Unity

## 6. acplugin
🔗 **Repositório:** [tokenRollAI/acplugin](https://github.com/tokenRollAI/acplugin)

Atua como uma camada de conversão entre formatos de plugins e Skills de diferentes agentes. Neste workflow, adapta as Skills originalmente disponibilizadas para o Claude Code para formatos compatíveis com o OpenCode.

**Fluxo de conversão:**
```text
Unity Agent Plugin ➔ Skills/Plugins ➔ Claude Code ➔ acplugin ➔ OpenCode
```

---

## 7. 🏗️ Arquitetura Completa

```text
                    ┌─────────────────────┐
                    │       Usuário       │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │   OpenCode Desktop  │
                    │     AI Agent        │
                    └──────────┬──────────┘
                               │
                 ┌─────────────┴─────────────┐
                 │                           │
                 ▼                           ▼
        ┌─────────────────┐        ┌─────────────────┐
        │      Skills     │        │   Unity Tools   │
        │ Unity Agent     │        │                 │
        │ Plugin          │        │ MCP / CLI       │
        └─────────────────┘        └────────┬────────┘
                                            │
                              ┌─────────────┴─────────────┐
                              │                           │
                              ▼                           ▼
                    ┌─────────────────┐        ┌─────────────────┐
                    │    Unity MCP    │        │    Unity CLI    │
                    └────────┬────────┘        └────────┬────────┘
                             │                          │
                             │                          ▼
                             │                 ┌─────────────────┐
                             │                 │ com.unity       │
                             │                 │ .pipeline       │
                             │                 └────────┬────────┘
                             │                          │
                             └────────────┬─────────────┘
                                          ▼
                              ┌─────────────────────┐
                              │    Unity Editor     │
                              │                     │
                              │ - Scenes            │
                              │ - GameObjects       │
                              │ - Assets            │
                              │ - C# Scripts        │
                              │ - Tests & Builds    │
                              └─────────────────────┘
```

---

## 8. 🔄 Fluxo de Desenvolvimento

### 8.1 Planejamento
O usuário descreve a tarefa (ex: *"Implemente um sistema de Helpers persistente entre cenas"*). O OpenCode analisa o pedido e consulta as Skills relevantes.

### 8.2 Análise do Projeto
O agente localiza scripts, analisa a arquitetura, verifica dependências e entende as convenções do projeto.

### 8.3 Implementação
O agente modifica os arquivos C# diretamente. Quando precisa interagir com o Editor:
`OpenCode` ➔ `Unity MCP` ➔ `Unity Editor`

### 8.4 Operações Automatizadas
Para automação via terminal:
`OpenCode` ➔ `Unity CLI` ➔ `Unity Pipeline` ➔ `Unity Editor`

### 8.5 Validação
O agente compila, testa e valida comandos, reduzindo a necessidade de alternar manualmente entre IDE, terminal e Unity.

---

## 9. 🧠 Por que combinar MCP + CLI + Skills?

Cada componente resolve um problema específico:

| Camada | Responsabilidade |
| :--- | :--- |
| **OpenCode** | Agente e raciocínio sobre a tarefa. |
| **Skills** | Conhecimento especializado e procedimentos. |
| **Unity MCP** | Ferramentas para interação direta com o Unity Editor. |
| **Unity CLI** | Automação e controle via terminal. |
| **Unity Pipeline** | Comunicação CLI ➔ Unity Editor. |
| **acplugin** | Adaptação das Skills para diferentes agentes. |
| **Unity Editor** | Execução real do projeto. |

A principal vantagem não é apenas gerar código, mas criar um **workflow agentic completo**, onde o agente consegue:  
`Entender ➔ Analisar ➔ Modificar ➔ Executar ➔ Testar ➔ Verificar ➔ Corrigir`  
Tudo isso sem depender exclusivamente da interação manual do desenvolvedor.

---

## 10. 🎯 Resultado e Conclusão

Essa stack transforma o desenvolvimento tradicional com Unity em um workflow assistido por IA, resultando no seguinte ecossistema colaborativo:

```text
             FREE / OPEN SOURCE AI UNITY WORKFLOW

                         OpenCode
                            │
                            ▼
                   ┌────────────────┐
                   │  Unity Skills  │
                   └───────┬────────┘
                           │
              ┌────────────┴────────────┐
              ▼                         ▼
         Unity MCP                 Unity CLI
              │                         │
              │                    Unity Pipeline
              │                         │
              └────────────┬────────────┘
                           ▼
                    Unity Editor
                           │
                           ▼
                     Unity Project
```

**Conclusão:**  
O resultado é um fluxo no qual a IA atua não apenas como um gerador de código, mas como uma **camada de automação** capaz de analisar, implementar, executar e validar tarefas reais diretamente de dentro do seu projeto Unity.
