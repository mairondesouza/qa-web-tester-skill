# QA Web Tester — Skill para Claude Code

Skill de QA autônomo para [Claude Code](https://docs.anthropic.com/en/docs/claude-code) que testa aplicações web e analisa UX/UI, gerando relatórios estruturados com sugestões priorizadas.

## O que faz

O `/qa-web-tester` age como um **QA Sênior + Consultor UX autônomo**:

1. **Testa funcionalidades** — caminho feliz, casos negativos, validações, erros de console/rede
2. **Analisa a experiência do usuário** — hierarquia visual, clareza de fluxo, consistência, densidade de informação, feedback, acessibilidade
3. **Sugere melhorias priorizadas** — classificadas por impacto/esforço com destaque para Quick Wins
4. **Avalia sob múltiplas perspectivas** — usuário leigo, usuário avançado, e perfil customizado opcional

## Funcionalidades

- **Coleta automática de credenciais** — busca em memória, CLAUDE.md, ou pergunta ao usuário
- **Suporte a multi-tenant** — entende subdomínios e confirma tenant antes de testar
- **Memória persistente** — salva credenciais de teste para próximas sessões
- **Análise híbrida** — screenshots (visual) + snapshots de acessibilidade (estrutural)
- **Relatório estruturado** — bugs funcionais + análise UX separada com priorização
- **Perfil customizado** — flag `--perfil` para perspectiva adicional de usuário

## Pré-requisitos

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) instalado
- [`playwright-cli`](https://www.npmjs.com/package/playwright-cli) instalado globalmente:

```bash
npm install -g playwright-cli
```

## Instalação

### Opção 1: Via CLI (recomendado)

```bash
claude install github:mairondesouza/qa-web-tester-skill
```

### Opção 2: Via settings.json

Adicione ao seu `~/.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "qa-web-tester": {
      "source": {
        "source": "github",
        "repo": "mairondesouza/qa-web-tester-skill"
      }
    }
  },
  "enabledPlugins": {
    "qa-web-tester@qa-web-tester": true
  }
}
```

### Opção 3: Instalação manual

Copie a pasta `skills/qa-web-tester/` para `~/.claude/skills/`:

```bash
cp -r skills/qa-web-tester ~/.claude/skills/
```

## Uso

```bash
# Testar uma página
/qa-web-tester http://meuapp.localhost:3000/login

# Testar com perfil customizado
/qa-web-tester http://meuapp.com/dashboard --perfil="operador de call center"

# Testar por descrição
/qa-web-tester testar o formulário de cadastro de usuários
```

## Fluxo de execução

| Fase | O que faz |
|------|-----------|
| **Fase 0** | Coleta credenciais (URL, usuário, senha) |
| **Fase 1** | Reconhecimento da página |
| **Fase 2** | Testes do caminho feliz |
| **Fase 3** | Testes negativos e de borda |
| **Fase 4** | Verificação de qualidade (console, rede, LGPD) |
| **Fase 5** | Análise UX/UI (screenshots + snapshots) |
| **Fase 6** | Relatório estruturado completo |

## Exemplo de relatório

O relatório gerado inclui:

- **Resumo Executivo** — estado funcional + estado UX
- **Testes Aprovados** — lista de testes que passaram
- **Bugs Encontrados** — com severidade, passos para reproduzir, evidências
- **Erros de Console/Rede** — erros JS e requisições com falha
- **Análise UX/UI**:
  - Pontos Positivos
  - Quick Wins `[Impacto: Alto | Esforço: Baixo]`
  - Melhorias Recomendadas
  - Melhorias Desejáveis
  - Resumo com nota geral [1-5] / 5
- **Cobertura** — cenários testados, taxa de aprovação

## Matriz de priorização

| | Esforço Baixo | Esforço Médio | Esforço Alto |
|---|---|---|---|
| **Impacto Alto** | Quick Win | Recomendada | Recomendada |
| **Impacto Médio** | Recomendada | Desejável | Desejável |
| **Impacto Baixo** | Desejável | Desejável | Não reportar |

## Estrutura do projeto

```
qa-web-tester-skill/
├── .claude-plugin/
│   └── marketplace.json    # Metadata do plugin para Claude Code
├── skills/
│   └── qa-web-tester/
│       └── SKILL.md        # A skill completa
├── .gitignore
├── LICENSE                  # MIT
└── README.md
```

## Licença

MIT
