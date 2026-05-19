# TODO Manager - ISA DevOps/SRE Lab

Aplicație web demonstrativă pentru laboratorul de Inginerie Software Avansată.

## Structura proiectului

```
isa-devops-lab/
├── app/           # Aplicația web (HTML + CSS + JS)
├── tests/         # Teste unitare Node.js
└── .github/
    └── workflows/
        ├── ci.yml          # CI: build + teste la fiecare push
        ├── cd.yml          # CD: deploy automat pe GitHub Pages
        └── sli-monitor.yml # Monitorizare SLI/SLO
```

## Rulare locală

```bash
# Deschide aplicația în browser
open app/index.html   # macOS
# sau dublu-click pe app/index.html în Windows/Linux

# Rulează testele
node tests/todo.test.js
```

## Workflows

| Workflow    | Declanșator                 | Scop                               |
| ----------- | --------------------------- | ---------------------------------- |
| CI          | push / pull_request pe main | Build + 15 teste unitare automate  |
| CD          | după CI pe main             | Deploy automat pe GitHub Pages     |
| SLI Monitor | orar + manual               | Metrici disponibilitate și latență |

## Rezumat conceptual

| Concept SRE       | Cum apare în acest laborator                                                      |
| ----------------- | --------------------------------------------------------------------------------- |
| **Automatizare**  | Workflow-urile se declanșează fără intervenție manuală la fiecare push            |
| **CI**            | Testele rulează automat la fiecare commit; erorile sunt detectate imediat         |
| **CD**            | Deploy-ul în „producție" (Pages) este complet automatizat după CI                 |
| **SLI**           | `curl` măsoară disponibilitate (HTTP 200?) și latență (ms)                        |
| **SLO**           | Pragurile definite în workflow (`slo_latency_ms`, `slo_availability`)             |
| **Error Budget**  | Calculat live: `100% - SLO` → minute permise de downtime pe lună                 |
| **Observabilitate** | `$GITHUB_STEP_SUMMARY` generează rapoarte Markdown vizibile în Actions          |
| **Alertare**      | `exit 1` marchează workflow-ul roșu când SLO-ul este depășit                     |
