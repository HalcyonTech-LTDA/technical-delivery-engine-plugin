# ARTEFATOS DE GO-LIVE E HANDOVER (FASE 3)
**Projeto:** {{TITULO_DO_PROJETO}} | **Cliente:** {{NOME_CLIENTE}} | **Data do Go-Live:** {{DATA_GO_LIVE}}

---

## 1. Runbook de Produção e Operação (Playbook Operacional)

### 1.1 Variáveis de Ambiente e Segredos de Produção
| Variável de Ambiente | Descrição / Finalidade | Sensibilidade (Plain / Secret) | Origem / Gestor de Segredos (Vault / K8s / AWS) |
| :--- | :--- | :--- | :--- |
{{FASE3_TABELA_VARIAVEIS_AMBIENTE}}

### 1.2 Procedimentos de Deploy e Estratégia de Rollback
- **Estratégia de Implantação:** {{FASE3_ESTRATEGIA_DEPLOY}} (ex.: Rolling Update, Blue/Green ou Canary)
- **Roteiro de Rollback de Aplicação:**
  1. Identificação do gatilho de falha impeditiva no ambiente de produção.
  2. Execução do comando de reversão da imagem de container para a tag estável anterior:
     ```bash
     {{FASE3_COMANDO_ROLLBACK_CONTAINER}}
     ```
  3. Reversão de schema de banco de dados (Migration Rollback):
     ```bash
     {{FASE3_COMANDO_ROLLBACK_DATABASE}}
     ```
  4. Validação de sanidade do sistema via Health Check de Produção.

### 1.3 Observabilidade, Alarmística e Logs
| Recurso de Monitoramento | Ferramenta / Plataforma | URL do Dashboard / Painel | Alertas e Limiares Configurados |
| :--- | :--- | :--- | :--- |
{{FASE3_TABELA_OBSERVABILIDADE}}

### 1.4 Termo de Demarcação Operacional (Isenção de Infraestrutura - Anexo 5)
> [!NOTE]
> A responsabilidade da Contratada encerra-se com a entrega do código homologado e do presente Runbook. Custos de nuvem, dimensionamento de servidores, gestão de backups, monitoramento ativo 24/7 e acionamento de rollbacks competem exclusivamente à equipe de operações e infraestrutura do Cliente (ou exigem a contratação autônoma de serviço de AMS/Sustentação).

---

## 2. Matriz de Débitos Técnicos (Handover Report)

### 2.1 Inventário de Defeitos Tolerados P3 / P4 (Aceitos em Homologação)
*Os vícios cosméticos abaixo foram validados durante a homologação e aceitos pelas partes sem prejuízo ao Go-Live.*

| ID | Módulo Afetado | Descrição do Comportamento | Solução de Contorno (Workaround) | Aceite Formal do Cliente |
| :--- | :--- | :--- | :--- | :--- |
{{FASE3_TABELA_DEFEITOS_P3_P4}}

### 2.2 Matriz de Débitos Técnicos Arquiteturais Mapeados
*Atalhos técnicos ou refatorações planejadas para garantir a entrega no prazo contratual.*

| Item Técnico | Racional da Decisão | Risco Associado | Horas Estimadas para Refatoração |
| :--- | :--- | :--- | :--- |
{{FASE3_TABELA_DEBITOS_ARQUITETURAIS}}

### 2.3 Roadmap Sugerido para Sustentação Contínua (Oportunidades de AMS)
*Funcionalidades barradas pelo processo de Change Request durante o projeto, convertidas em backlog evolutivo sugerido:*

| Módulo / Funcionalidade | Descrição do Benefício de Negócio | Complexidade Estimada | Pacote Sugerido de AMS |
| :--- | :--- | :--- | :--- |
{{FASE3_TABELA_ROADMAP_AMS}}

---

## 3. Termo de Encerramento e Sign-off Técnico Definitivo

### 3.1 Declaração de Go-Live e Gatilho da Garantia Técnica
As partes declaram que a solução foi implantada em Produção em **{{DATA_GO_LIVE}}**, momento em que se inicia a contagem improrrogável do período de **60 (sessenta) dias corridos de Garantia Técnica**, com término previsto para **{{DATA_TERMINO_GARANTIA}}**, estritamente para correção de defeitos impeditivos P1 e P2 do código desenvolvido.

### 3.2 Checklist Físico de Entrega e Transição de Ativos
| Ativo de Engenharia | Destino / Conta de Destino do Cliente | Status da Transferência |
| :--- | :--- | :--- |
| **Repositórios de Código-Fonte (Git)** | {{FASE3_ATIVO_GIT}} | Concluído |
| **Imagens de Containers / Registry** | {{FASE3_ATIVO_REGISTRY}} | Concluído |
| **Apontamentos DNS e Certificados SSL** | {{FASE3_ATIVO_DNS}} | Concluído |
| **Documentação Técnica e OpenAPI** | {{FASE3_ATIVO_DOCS}} | Concluído |

### 3.3 Quadro de Liquidação Financeira Integral (Condição Suspensiva de Foreground IP)
*A transferência definitiva dos direitos patrimoniais sobre o Foreground IP está expressamente subordinada à liquidação total (100%) das faturas contratuais (Cláusula de Condição Suspensiva do Anexo 1).*

| Parcela / Fatura | Marco Correspondente | Valor (R$) | Status Financeiro (Liquidado / Pendente) |
| :--- | :--- | :--- | :--- |
{{FASE3_TABELA_LIQUIDACAO_FINANCEIRA}}

### 3.4 Liberação de Propriedade Intelectual (Foreground IP vs Background IP)
1. **Foreground IP:** Cumprida a condição suspensiva de quitação de 100% das faturas acima, a Contratada transfere em caráter definitivo os direitos patrimoniais sobre o código customizado desenvolvido para o Cliente.
2. **Background IP:** A Contratada concede licença perpétua, não-exclusiva e livre de royalties sobre seus aceleradores, bibliotecas base e frameworks embutidos na solução, ficando vedada a revenda ou sublicenciamento pelo Cliente a terceiros.

---

## 4. Bloco de Assinaturas Formais

As partes firmam o presente Termo de Encerramento e Sign-off Técnico na presença de duas testemunhas, atestando a entrega integral dos artefatos contratados.

**Local e Data:** {{CIDADE_ASSINATURA}}, {{DATA_ASSINATURA}}

<br>

______________________________________________________  
**{{NOME_REPRESENTANTE_CLIENTE}}**  
{{CARGO_REPRESENTANTE_CLIENTE}}  
{{NOME_CLIENTE}}

<br>

______________________________________________________  
**{{NOME_TECH_LEAD_CONTRATADA}}**  
Líder Técnico de Engenharia  
{{NOME_SOFTWARE_HOUSE}}

<br>

**Testemunhas:**

1. _____________________________________________  
   Nome: {{TESTEMUNHA_1_NOME}}  
   CPF: {{TESTEMUNHA_1_CPF}}

2. _____________________________________________  
   Nome: {{TESTEMUNHA_2_NOME}}  
   CPF: {{TESTEMUNHA_2_CPF}}
