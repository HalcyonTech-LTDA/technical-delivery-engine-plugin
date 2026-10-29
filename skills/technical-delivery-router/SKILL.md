---
name: technical-delivery-router
description: >-
  Orquestrador Event-Driven baseado em Triagem (Router). Avalia o pedido do utilizador (Inception, Homologação/QA ou Go-Live/Handover),
  injeta o template correspondente e despacha a execução exclusivamente para o Agente Especialista daquela fase.
---

# Technical Delivery Engine (Event-Driven Router)

Esta skill atua como o **Router Central** para a geração de todos os Artefatos de Execução e Handover de Engenharia (Bloco 2). Como os artefatos de delivery são espaçados no tempo (ex.: o Runbook só é feito meses após o C4 Model), este orquestrador opera por demanda.

A inteligência de orquestração reside em identificar em que fase do ciclo de vida o pedido se encontra e acionar apenas a rota adequada, otimizando o consumo de tokens e garantindo hiperfoco.

---

## Gatilhos e Invocação Canônica

A invocação oficial é realizada através do comando registrado da skill:

```bash
/technical-delivery-router [modo] [contexto_path] [output_dir]
```

### Parâmetros Suportados:
- `[modo]`:
  - `auto`: Triagem automática baseada na intenção do prompt do usuário.
  - `fase1`: Força a geração dos artefatos da **Fase 1 (Inception & Setup Estrutural)**.
  - `fase2`: Força a geração dos artefatos da **Fase 2 (Entrega Contínua, Release Notes & QA)**.
  - `fase3`: Força a geração dos artefatos da **Fase 3 (Go-Live, Runbook & Handover Sign-off)**.
- `[contexto_path]`: Caminho para o arquivo ou diretório de contexto.
- `[output_dir]`: Diretório de destino dos artefatos (padrão: `./artefatos_delivery`).

---

## Tipos de Insumo Adequados por Fase

Ao contrário de pipelines lineares de pré-venda, os artefatos de engenharia demandam insumos compatíveis com o momento do projeto:
- **Para a Fase 1 (Inception):** O contexto deve ser a SOW contratual (Anexo 1), o Dossiê Técnico de Pré-venda ou o arquivo JSON de baseline arquitetural.
- **Para a Fase 2 (Construção & QA):** O contexto deve conter os dados específicos do pacote/sprint entregue (entregáveis concluídos, Known Issues, credenciais de teste em Staging, rotas de API e métricas da esteira de CI/CD). Se o usuário fornecer apenas o contrato macro, o Router solicitará ou inferirá os dados específicos da release em homologação.
- **Para a Fase 3 (Go-Live & Handover):** O contexto deve incluir os parâmetros do encerramento (data da subida em produção, débitos técnicos aceitos, checklist de transferência de ativos e status de liquidação financeira das faturas).

---

## Lógica de Triagem e Execução (O Fluxo do Router)

O modelo orquestrador DEVE seguir estes passos para atender ao utilizador:

### Passo 1: Avaliação do Pedido e Determinação da Rota
Analise o comando explícito ou a intenção textual do utilizador:
- **Se envolver:** Arquitetura, setup, C4 Model (Contexto e Contêineres), matriz de integração, infraestrutura base, Sprint 0 ou Backlog Refinado.
  $\rightarrow$ **IR PARA A ROTA A (Fase 1: Inception)**
- **Se envolver:** Entrega de sprint, release notes, protocolo de homologação, Swagger/OpenAPI, relatórios de QA, mocks ou evidências de CI/CD.
  $\rightarrow$ **IR PARA A ROTA B (Fase 2: Construção & QA)**
- **Se envolver:** Go-live, produção, operação, Runbook, rollback, débitos técnicos, encerramento de projeto ou termo de sign-off/cessão de IP.
  $\rightarrow$ **IR PARA A ROTA C (Fase 3: Handover & Encerramento)**

---

### Passo 2: Execução Roteada (Single-Agent Dispatch)

Defina o diretório de saída: se não especificado pelo usuário, utilize `{{output_dir}} = ./artefatos_delivery`. Crie o diretório se ele não existir.

Execute **apenas uma** das rotas abaixo:

#### Rota A: Inception e Setup (Fase 1)
1. **Leia** o conteúdo integral do template: `skills/technical-delivery-router/templates/FASE1_INCEPTION_ARTIFACTS.template.md`.
2. **Acione** exclusivamente o subagente `phase1-inception-architect`, fornecendo o contexto da SOW/baseline e a string integral do template.
3. **Salve** o resultado em `{{output_dir}}/FASE1_INCEPTION_ARTIFACTS.md`.

#### Rota B: Entrega Contínua e QA (Fase 2)
1. **Leia** o conteúdo integral do template: `skills/technical-delivery-router/templates/FASE2_RELEASE_NOTES_QA.template.md`.
2. **Acione** exclusivamente o subagente `phase2-release-engineer`, fornecendo os dados da sprint/release fornecidos pelo usuário e a string integral do template.
3. **Salve** o resultado em `{{output_dir}}/FASE2_RELEASE_NOTES_QA_[NOME_DA_RELEASE].md`.

#### Rota C: Go-Live e Handover (Fase 3)
1. **Leia** o conteúdo integral do template: `skills/technical-delivery-router/templates/FASE3_HANDOVER_SIGNOFF.template.md`.
2. **Acione** exclusivamente o subagente `phase3-handover-closer`, fornecendo o histórico do projeto, débitos conhecidos, status financeiro e a string integral do template.
3. **Salve** o resultado em `{{output_dir}}/FASE3_HANDOVER_SIGNOFF.md`.

---

### Passo 3: Auditoria de Integridade e Validação de Saída

Antes de encerrar a resposta ao utilizador, o Router DEVE validar a qualidade do artefato gerado:
1. **Verificação de Placeholders:** Confirmar que não restou nenhum marcador não resolvido no formato `{{...}}`.
2. **Higienização de HTML:** Confirmar que todos os comentários `<!-- ... -->` foram expurgados.
3. **Sintaxe Mermaid:** Assegurar que os diagramas C4 em `flowchart TD` possuem todos os nós textuais entre aspas duplas (`["..."]`).
4. **Completude Estrutural:** Confirmar que as tabelas de salvaguardas contratuais (RACI, protocolo de aceite tácito, mocks e cessão de IP) foram devidamente preenchidas com dados ricos.

---

### Passo 4: Entrega ao Utilizador
- Apresente um resumo executivo dos artefatos gerados para a fase demandada.
- Destaque as principais salvaguardas contratuais ativadas naquele documento.
- Forneça o caminho absoluto com link clicável para o arquivo markdown gerado.
