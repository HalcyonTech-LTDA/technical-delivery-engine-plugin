---
description: Aplicar exclusivamente durante a geração de artefatos técnicos de delivery, C4 Models, Release Notes, QA Reports e Swagger/OpenAPI.
trigger: model_decision
---

# PADRÕES DE QUALIDADE DE ENTREGA E EVIDÊNCIAS DE HOMOLOGAÇÃO (BLOCO 2)

1. **Protocolo Formal de Homologação e Gatilho do Aceite Tácito (Fase 2):**
   - Toda entrega de pacote/sprint deve iniciar obrigatoriamente pelo **Protocolo Formal de Homologação**, registrando a data/hora exata do envio (Dia 0) e a data/hora limite (Dia 5 útil subsequente às 18h00).
   - É expressamente vedado o uso de canais informais (Slack, WhatsApp, e-mails soltos) para disparo de releases. O rito deve formalizar o canal único oficial de apontamento (Jira ou Portal do PO).
   - Apenas defeitos impeditivos **P1 (Bloqueante)** e **P2 (Crítico)** suspendem o prazo de homologação. Divergências estéticas ou fluxos de exceção **P3/P4 não suspendem o aceite nem o faturamento**.

2. **Evidência Obrigatória de CI/CD e Mocks (Blindagem contra Legados):**
   - Na Fase 2, todo Relatório de QA (`QA Report`) deve conter, compulsoriamente, evidência de que a suíte de testes de integração rodou na esteira de CI/CD utilizando simuladores (*mocks/stubs*) para as APIs e ERPs do Cliente.
   - Isso materializa a cláusula de "Não-Interrupção por Instabilidade de Sistemas Legados" (Anexo 3), provando juridicamente que o código da software house funciona independentemente de o ERP ou gateways do Cliente estarem inoperantes durante a janela de 5 dias úteis.
   - A esteira deve comprovar cobertura de código mínima de 80% e zero vulnerabilidades críticas no SAST.

3. **C4 Model em Dois Níveis Distintos (Fase 1):**
   - A arquitetura deve ser documentada estritamente sob a notação **C4 Model**, gerando dois diagramas Mermaid independentes:
     1. **Diagrama de Contexto (Nível 1):** Delimita os atores, o sistema e as integrações externas corporativas.
     2. **Diagrama de Contêineres (Nível 2):** Detalha SPAs, APIs, Workers, filas de mensageria e bancos de dados.
   - **Regra de Sintaxe Mermaid:** Todo nó textual deve estar protegido entre aspas duplas (`["..."]` ou `[("...")]`) para impedir falhas de renderização.

4. **Especificação OpenAPI/Swagger e Comandos cURL Executáveis:**
   - Na Fase 2, as APIs entregues devem ser acompanhadas de tabela síntese de rotas e comandos cURL interativos completos, apontando diretamente para o host de Staging, contendo verbos HTTP, headers de autenticação (`Authorization: Bearer <TOKEN>`) e payloads JSON válidos.

5. **Restrição de Verbos em Release Notes e Tabela de Known Issues:**
   - As *Release Notes* devem relatar estritamente o que foi concluído e testado. É vedado usar verbos no futuro ou prometer escopo vindouro.
   - Toda limitação temporária deve ser catalogada na tabela de *Known Issues* com justificativa contratual (Sprint de destino), blindando a software house contra chamados indevidos.
