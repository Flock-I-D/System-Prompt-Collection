# 🤖 System Prompts Collection

Una colección organizada de system prompts, agentes y configuraciones para IAs, con foco en Claude, Windsurf/Cascade y otros modelos de lenguaje.

## 📋 Descripción

Este repositorio mantiene una colección curada de:
- **System prompts** para diferentes propósitos
- **Agentes especializados** para Claude Code
- **Rules y Workflows** para Windsurf/Cascade
- **Templates** para Obsidian

## 📁 Estructura del Repositorio

```
├── System Prompt/
│   ├── Base/                    # Frameworks de razonamiento
│   │   ├── base.md              # ReAct + Tree of Thoughts + Chain of Thought
│   │   ├── Reflection 70b.md
│   │   └── Experimentos/
│   ├── SysP principales/        # Prompts core
│   │   ├── Prompt Ejecutivo.md
│   │   ├── Prompt Programmming.md
│   │   └── Reasoning Framework.md
│   ├── Trading/                 # Sistema de análisis cripto
│   │   ├── trading_pod_unified.md  # Sistema completo por capas
│   │   └── Antiguos/
│   ├── Creacion de app/
│   └── Varios/
│
├── claude/                      # Configuración Claude Code
│   ├── agents/                  # Agentes especializados
│   │   ├── fastapi-architect.md
│   │   ├── langgraph-multi-agent-architect.md
│   │   ├── python-code-auditor.md
│   │   ├── frontend-code-reviewer.md
│   │   ├── nextjs-expert.md
│   │   ├── css-ui-designer.md
│   │   ├── playwright-qa-engineer.md
│   │   ├── context7-docs-researcher.md
│   │   └── technical-documentation-architect.md
│   └── memory.md                # Reglas de memoria
│
├── windsurf/                    # Configuración Windsurf/Cascade
│   ├── rules/                   # Reglas de proyecto
│   │   ├── global-rules.md
│   │   ├── langgraph-project.md
│   │   ├── langchain-project.md
│   │   ├── expo_53_android_rules.md
│   │   └── migracion.md
│   └── workflows/               # Workflows reutilizables
│       ├── plan.md              # Análisis y planificación
│       ├── task_implementation.md
│       ├── finish-chat.md
│       └── contextual-new-chat.md
│
└── Obsidian/
    └── Templates/               # Templates para notas
        ├── Daily Note Template.md
        ├── Weekly.md
        └── Monthly.md
```

## 🔧 Implementación

### Claude Projects
1. Accede a tu proyecto en Claude
2. Ve a "Projects" > "Set custom instructions for project"
3. Copia y pega el prompt deseado

### Claude Code (Agentes)
1. Copia el archivo `.md` del agente a tu carpeta `.claude/agents/`
2. El agente estará disponible automáticamente

### Windsurf/Cascade
- **Rules**: Copia a `.windsurf/rules/` o configura en Global Rules
- **Workflows**: Copia a `.windsurf/workflows/` para usar con `/comando`

### Obsidian
1. Copia los templates a tu carpeta de templates de Obsidian
2. Configura en Settings > Templates

## 📝 Convenciones

Cada prompt/agente debe incluir:
- Título y versión
- Descripción del propósito
- Instrucciones de implementación
- Ejemplos de uso (cuando aplique)

## 🤝 Contribuciones

1. Fork del repositorio
2. Crea una rama (`git checkout -b feature/NuevoPrompt`)
3. Commit de cambios (`git commit -m 'Agrega nuevo prompt'`)
4. Push a la rama (`git push origin feature/NuevoPrompt`)
5. Abre un Pull Request

## 📄 Licencia

Este proyecto está bajo la Licencia MIT - ver el archivo [LICENSE](LICENSE) para más detalles.
