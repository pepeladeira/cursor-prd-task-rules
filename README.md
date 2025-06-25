# Cursor PRD Task Rules 🚀

Um conjunto de regras do Cursor para automatizar o fluxo de desenvolvimento desde a criação de um Documento de Requisitos do Produto (PRD) até a implementação completa da funcionalidade.

## 📋 Visão Geral

Este repositório contém três regras do Cursor que trabalham em conjunto para criar um fluxo de desenvolvimento estruturado:

1. **Criar PRD** - Gera um documento de requisitos detalhado
2. **Gerar Tarefas** - Converte o PRD em uma lista de tarefas implementáveis
3. **Processar Lista de Tarefas** - Gerencia a execução das tarefas com controle de qualidade

## 🔧 Como Instalar

1. Clone este repositório:

```bash
git clone https://github.com/seu-usuario/cursor-prd-task-rules.git
cd cursor-prd-task-rules
```

2. Copie as regras para o seu projeto:

```bash
# Crie o diretório .cursor/rules no seu projeto (se não existir)
mkdir -p .cursor/rules

# Copie as regras
cp rules/*.mdc .cursor/rules/
```

3. Reinicie o Cursor para que as regras sejam carregadas.

## 📚 Regras Detalhadas

### 1. 📝 Create PRD (`create-prd.mdc`)

**O que faz:**

- Orienta a criação de um Documento de Requisitos do Produto (PRD) detalhado
- Faz perguntas esclarecedoras para entender completamente os requisitos
- Gera um PRD estruturado em formato Markdown

**Como usar:**

1. Descreva brevemente a funcionalidade que você quer implementar
2. O AI fará perguntas esclarecedoras sobre:
   - Problema que a funcionalidade resolve
   - Usuário-alvo
   - Histórias do usuário
   - Critérios de aceitação
   - Requisitos de dados
   - Casos extremos
3. Com base nas suas respostas, será gerado um PRD completo em `/tasks/prd-[nome-da-funcionalidade].md`

**Estrutura do PRD gerado:**

- Introdução/Visão Geral
- Objetivos
- Histórias do Usuário
- Requisitos Funcionais
- Não-Objetivos (Fora do Escopo)
- Considerações de Design
- Considerações Técnicas
- Métricas de Sucesso
- Questões Abertas

### 2. ✅ Generate Tasks (`generate-tasks.mdc`)

**O que faz:**

- Converte um PRD existente em uma lista de tarefas detalhada e implementável
- Quebra a funcionalidade em tarefas de alto nível e sub-tarefas específicas
- Identifica arquivos que precisarão ser criados ou modificados

**Como usar:**

1. Referencie o arquivo PRD que você quer implementar
2. O AI analisará o PRD e gerará tarefas de alto nível
3. Confirme com "Vai" para gerar as sub-tarefas detalhadas
4. O resultado será salvo em `/tasks/tasks-[nome-do-prd].md`

**Processo em duas fases:**

- **Fase 1:** Geração de tarefas principais (alto nível)
- **Fase 2:** Quebra em sub-tarefas específicas e acionáveis

### 3. 🔄 Process Task List (`process-task-list.mdc`)

**O que faz:**

- Gerencia a execução das tarefas com controle de qualidade
- Implementa protocolos de conclusão com testes e commits automáticos
- Mantém o controle de progresso da implementação

**Como usar:**

1. Abra a lista de tarefas gerada pela regra anterior
2. O AI implementará uma sub-tarefa por vez
3. Após cada sub-tarefa, você precisa autorizar a próxima com "sim", "s", "yes", "y" ou "ok"
4. Quando todas as sub-tarefas de uma tarefa pai estiverem concluídas:
   - Testes são executados automaticamente
   - Código é commitado com mensagem estruturada
   - Tarefa pai é marcada como concluída

**Protocolo de conclusão:**

- ✅ Sub-tarefa concluída → Marca como `[x]`
- 🧪 Todas sub-tarefas de uma tarefa pai concluídas → Executa testes
- ✅ Testes passaram → Adiciona ao stage (`git add .`)
- 🧹 Remove arquivos temporários
- 📝 Commit com mensagem estruturada
- ✅ Marca tarefa pai como `[x]`

## 🚀 Fluxo de Trabalho Completo

### Passo 1: Criar PRD

```
Você: "Quero criar uma funcionalidade de login com Google"
AI: [Faz perguntas esclarecedoras]
Você: [Responde as perguntas]
AI: [Gera PRD completo em /tasks/prd-login-google.md]
```

### Passo 2: Gerar Tarefas

```
Você: "Gere tarefas para o PRD prd-login-google.md"
AI: [Gera tarefas de alto nível]
Você: "Vai"
AI: [Gera sub-tarefas detalhadas em /tasks/tasks-prd-login-google.md]
```

### Passo 3: Implementar

```
AI: [Implementa primeira sub-tarefa]
Você: "sim"
AI: [Implementa próxima sub-tarefa]
Você: "s"
AI: [Continua até completar todas as tarefas]
```

## 📁 Estrutura de Arquivos

```
seu-projeto/
├── .cursor/
│   └── rules/
│       ├── create-prd.mdc
│       ├── generate-tasks.mdc
│       └── process-task-list.mdc
└── tasks/
    ├── prd-funcionalidade-1.md
    ├── tasks-prd-funcionalidade-1.md
    ├── prd-funcionalidade-2.md
    └── tasks-prd-funcionalidade-2.md
```

## 💡 Benefícios

- **Documentação Consistente**: PRDs padronizados e detalhados
- **Planejamento Estruturado**: Tarefas organizadas e priorizadas
- **Controle de Qualidade**: Testes automáticos e commits estruturados
- **Acompanhamento de Progresso**: Visualização clara do que foi feito
- **Redução de Erros**: Processo estruturado reduz esquecimentos
- **Facilita Revisões**: Histórico claro de desenvolvimento

## 🎯 Casos de Uso Ideais

- **Desenvolvimento de novas funcionalidades**
- **Refatoração de código existente**
- **Projetos com múltiplos desenvolvedores**
- **Projetos que precisam de documentação detalhada**
- **Implementações complexas que requerem planejamento**

## 📝 Exemplo de Commit Gerado

```bash
git commit -m "feat: adiciona autenticação com Google OAuth" \
-m "- Implementa fluxo de login com Google" \
-m "- Adiciona middleware de autenticação" \
-m "- Cria testes unitários para OAuth" \
-m "Relacionado a T001 no PRD prd-login-google"
```

## 💡 Inspiração

Este sistema foi inspirado pelo vídeo: [https://www.youtube.com/watch?v=fD4ktSkNCw4](https://www.youtube.com/watch?v=fD4ktSkNCw4)

## 🤝 Contribuindo

Sinta-se à vontade para sugerir melhorias ou reportar problemas através das issues do GitHub.

---

**Criado para otimizar o fluxo de desenvolvimento com Cursor AI** 🎯
