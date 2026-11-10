# Aldren Core Template

Plantilla de prácticas de ingeniería para proyectos de Aldren Studio Lab.

## Elephant–Goldfish Model (EGM)

**Fuente:** https://github.com/google/elephant-goldfish-model  
**Licencia del proyecto original:** Apache-2.0  
**Versión examinada:** 0.1.1 (2026-11-10)

EGM es un **plugin para asistentes de programación**: no es un modelo LLM, un scanner ni una dependencia de ejecución de nuestras aplicaciones. Conserva el contexto del producto para idear y redactar especificaciones (*Elephant*) y usa revisores independientes con contexto conversacional nuevo (*Goldfish*) para detectar vacíos y supuestos antes de implementar.

**Decisión:** usar EGM como herramienta de **desarrollo opcional**, instalada en el entorno del agente, sin copiar ni ejecutar su repositorio dentro de cada producto. Esta plantilla contiene solamente convenciones y referencias. El plugin original es la fuente de las skills y los estándares.

### Instalación en el entorno de desarrollo

Codex CLI:

```sh
codex plugin marketplace add google/elephant-goldfish-model
codex plugin add egm@egm
```

Claude Code:

```sh
claude plugin marketplace add google/elephant-goldfish-model
claude plugin install egm@egm
```

Para **ChatGPT/Codex desktop**, abrir [EGM en el directorio de plugins](https://chatgpt.com/plugins/plugins_6aeb90f47ec88191a3c107e01d3eb357) e instalarlo en la aplicación de escritorio. No equivale a habilitarlo en una conversación web o una sesión cloud.

Reiniciar la sesión del agente y verificar que las skills estén disponibles. **No alcanza con copiar solamente `skills/`**: EGM necesita también los revisores (`agents/`) y los estándares (`resources/`).

### Proceso sugerido

1. Identificar el problema, objetivo, límites y criterios verificables. Para cambios triviales no imponer burocracia.
2. Usar `egm-brainstorm` y `egm-draft` para preparar propuesta y diseño.
3. Usar `egm-review` sobre un diseño existente, siempre que el entorno disponga de subagentes con contexto conversacional fresco.
4. Resolver los hallazgos relevantes y solicitar aprobación humana del diseño antes de implementar.
5. Implementar en rama de trabajo con pruebas y revisión; registrar la especificación aprobada en `docs/designs/`.
6. Aplicar `egm-drift-report` cuando cambien el código o el contrato documentado.

En Codex, elegir la skill desde el selector; la sintaxis exacta del comando varía según el agente. Para un proyecto existente, empezar por **revisar un diseño pequeño** antes de adoptar el proceso completo.

### Estructura de artefactos

- `.dev/docs/`: borradores y resultados temporales de revisión, fuera de Git.
- `docs/designs/`: especificaciones aprobadas y versionadas.
- `AGENTS.md`: reglas estables, alcance de los agentes y ruta de artefactos.

### Límites y seguridad

- Un review de EGM **no sustituye pruebas, revisión de código, revisión de seguridad ni criterio humano**.
- Requiere soporte real de subagentes independientes. Si la plataforma no lo ofrece o no se puede verificar, no declarar que se hizo un Goldfish review aislado.
- Los agentes pueden acceder a los archivos que autorice el entorno. No enviar credenciales, información de clientes ni datos sensibles a revisiones innecesarias.
- EGM **no habilita automáticamente** funciones para clientes dentro de BREAKERS, Llave360 u otras apps. Integrar esa capacidad como producto requeriría diseño, implementación, consentimiento del usuario y pruebas separados.

Documentación oficial: [README](https://github.com/google/elephant-goldfish-model/blob/main/README.md), [harnesses](https://github.com/google/elephant-goldfish-model/blob/main/docs/harnesses.md), [privacidad](https://github.com/google/elephant-goldfish-model/blob/main/docs/privacy.md).

## Aplicación inicial

Piloto de convenciones de diseño y revisión documental en [Breakers](https://github.com/Ch1405041C0/Breackers.co), sin modificar el runtime de SCAN/STRIKE.
