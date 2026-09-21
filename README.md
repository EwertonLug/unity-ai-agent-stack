# 🤖 Stack de Desenvolvimento Unity com IA

Bem-vindo ao repositório da Stack de Desenvolvimento Unity com IA. 

Este workflow utiliza ferramentas gratuitas e/ou open source para permitir que agentes de IA interajam diretamente com projetos Unity. Ele combina o protocolo MCP, Unity CLI, Unity Pipeline e Skills especializadas para criar um ambiente de desenvolvimento autônomo e assistido.

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
