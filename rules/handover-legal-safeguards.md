---
description: Aplicar exclusivamente durante a geração de artefatos de encerramento de projeto, Termos de Sign-off, Handover e Runbooks de Produção.
trigger: model_decision
---

# SALVAGUARDAS LEGAIS PARA HANDOVER E ENCERRAMENTO (BLOCO 2 - FASE 3)

1. **Separação Estrita de Delivery vs. Operações / AMS (Runbook):**
   - O *Runbook de Produção* deve estabelecer formalmente que a gestão de infraestrutura em nuvem, dimensionamento de servidores, monitoramento ativo 24/7, gestão de backups e acionamento de procedimentos de rollback competem exclusivamente à equipe de operações do Cliente (ou exigem contrato autônomo de AMS/Sustentação).
   - O documento deve conter roteiro objetivo de Rollback tanto para a imagem de container quanto para o banco de dados (reversão de migrations).

2. **Matriz de Débitos Técnicos e Conversão Comercial para AMS:**
   - O encerramento do projeto exige listar com transparência os pequenos defeitos cosméticos tolerados (P3/P4) e os débitos técnicos arquiteturais assumidos para viabilizar os prazos. A subscrição do Cliente neste documento blinda a software house contra alegações futuras de vícios ocultos.
   - Os itens barrados pelo processo de *Change Request* durante o projeto devem ser convertidos estruturadamente em um roadmap de oportunidades de evolução para fechar contratos de sustentação (AMS).

3. **Cessão de Propriedade Intelectual Condicionada (Termo de Sign-off):**
   - O Termo de Sign-off é o documento final do projeto. Nele, a transferência definitiva dos repositórios de código (*Foreground IP*) para o Cliente **deve estar expressamente vinculada à condição suspensiva de liquidação e quitação financeira integral (100%)** de todas as faturas e *Change Requests* do projeto, conforme amarrado no Anexo 1 (SOW).
   - Deve ser incluído um quadro demonstrativo de liquidação financeira comprovando o status de pagamento de cada fatura.
   - O documento deve ratificar a cessão da licença de uso perpétua, não-exclusiva e gratuita sobre os aceleradores e *Background IP* da Contratada embutidos na solução.

4. **Vigência da Garantia Técnica e Bloco de Assinaturas:**
   - O Go-Live ativa formalmente o relógio dos 60 (sessenta) dias corridos de Garantia Técnica, restrita a defeitos impeditivos P1 e P2 de responsabilidade da Contratada.
   - O encerramento requer a assinatura digital do Representante Legal do Cliente, do Tech Lead da Contratada e de 2 testemunhas com nome e CPF, conferindo plena eficácia jurídica ao instrumento.
