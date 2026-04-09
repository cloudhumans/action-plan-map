# Dúvidas e Gaps — Vivastays — 2026-04-06

## Dúvidas sobre Features/Configurações
- [ ] `query_transform` (OFF): O que exatamente essa feature faz no contexto de Vivastays? É aplicável para canal WhatsApp/chat? Qual o impacto esperado na retenção?
- [ ] `output_transformation` (ON): Está ativa, mas qual transformação está sendo aplicada? Está funcionando corretamente? Algum impacto mensurável?
- [ ] `start_with_bot` (OFF): Vivastays usa qual canal principal? Se for WhatsApp, faz sentido ativar?
- [ ] `agentic_enabled` (OFF): Feature nova — qual o comportamento esperado? Já foi testada em projetos similares?
- [ ] `attachment_handover` (OFF): Hóspedes enviam fotos de problemas (manutenção, SCI)? Se sim, ativar pode melhorar o fluxo.
- [ ] `clarification_enabled` (null): Campo retorna null — significa que não está configurado? Qual o default?
- [ ] `tone_of_voice_enabled` (null): Campo retorna null — está usando Base Prompt para tom de voz ou existe config separada?
- [ ] `agentic_handoff_flow`: 852 N2 (7.4%) por "Agentic handoff flow" — mas `agentic_enabled` está OFF. Como esse motivo de N2 aparece se o agentic está desativado? Existe outro mecanismo que dispara esse handoff?

## Dados que Faltaram para Análise Completa
- [ ] **CSAT**: Zero respostas de CSAT no período. Sem esse dado, não é possível avaliar qualidade percebida pelo hóspede. Está configurada a pesquisa de CSAT? Qual canal?
- [ ] **IDS completa**: Não foi feita análise da IDS (duplicatas, qualidade de escrita). Quantos conteúdos N1 vs N2 existem atualmente?
- [ ] **Eddie flows existentes**: Não foi possível listar os Eddie flows ativos. Quais fluxos já existem? Algum com erro recorrente?
- [ ] **Auditoria**: Não executei Layer 3 (Q3-AuditErrors, Q3-ShouldTransfer). Seria útil para validar se os N1 atuais estão realmente corretos.
- [ ] **Canal principal**: Qual o canal predominante (WhatsApp, chat web, email)? Impacta nas recomendações de config.

## Hipóteses que Precisam de Validação
- [ ] **Hipótese:** A IDS está invertida (mais N2 que N1) porque o projeto é de hotelaria onde muitos temas requerem ação humana (manutenção, acesso físico). **Validação:** Confirmar com AM se esses conteúdos foram deliberadamente marcados como N2 ou se há oportunidade de automação.
- [ ] **Hipótese:** O alto volume de "Falar com humano" (524 tix) pode ser reduzido com Venda do Bot / FORWARD_TO_HUMAN_CHECK. **Validação:** Verificar se já existe algum FlowPrompt configurado para esse cenário.
- [ ] **Hipótese:** Os 852 N2 por "Agentic handoff flow" podem estar relacionados a algum fluxo de integração com PMS do cliente. **Validação:** Verificar configuração do agentic e qual trigger está ativando.
- [ ] **Hipótese:** Guarda-volumes (209 tix) e Utensílios extras (141 tix) poderiam ser N1 simples (resposta informativa). **Validação:** Confirmar com AM se a resposta pode ser padronizada sem intervenção humana.

## Sugestões de Dados Adicionais
- [ ] Acesso aos Eddie flows configurados para Vivastays (CloudBlocks → Eddie)
- [ ] Lista completa da IDS com contagem de N1 vs N2 vs INTERACTIVE
- [ ] FlowPrompts configurados (especialmente FORWARD_TO_HUMAN_CHECK e MULTIPROMPT)
- [ ] Dados de auditoria (Layer 3) para validar qualidade dos N1 atuais
- [ ] Informação sobre integrações existentes (PMS Stays, sistema de smart locks, sistema de reconhecimento facial) — crucial para avaliar viabilidade de Eddie flows
