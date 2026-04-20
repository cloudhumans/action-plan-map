# Dúvidas e Gaps — Darwin — 20/04/2026

## Dúvidas sobre Features/Configurações
- [ ] `clarificationsettings__enabled = null`: Qual o comportamento default quando o campo está null? É tratado como false, true, ou herda configuração de classificação? Necessita confirmação com time de produto antes de setá-lo explicitamente.
- [ ] `conversationhistoryquerytransformationsettings__enabled = FALSE` (query_transform): Qual o impacto real de ativar? A documentação não é clara sobre o mecanismo exato para este tipo de projeto (seguradora, canal WhatsApp/chat). Não recomendado sem validação prévia.
- [ ] `agentic_enabled = FALSE`: Feature nova, sem documentação suficiente para recomendar ativação. Avaliar com time de produto se faz sentido para o contexto de seguradora.

## Dados que Faltaram para Análise Completa
- [ ] Query de `active_flow_flow_id` falhou — coluna não existe no schema atual. Seria necessário para análise individual dos Eddie flows (14,56% dos N2 em 30d são Eddie N2). Avaliar se existe query alternativa ou tabela nova.
- [ ] CSAT real por tag/conteúdo — só temos GenCX. CSAT dos usuários finais ajudaria a priorizar conteúdos com impacto percebido (não só volumétrico).
- [ ] Dados operacionais do cliente (horário de atendimento, e-mail do atendimento para dispensa de vistoria 0km, prazo de retorno em casos específicos) — necessários para completar a reescrita de vários conteúdos.

## Hipóteses que Precisam de Validação
- [ ] Hipótese: Multiprompt handover em 32,92% dos N2 é impulsionado por corretores pedindo humano mesmo quando a ClaudIA poderia resolver. | Validação necessária: auditar amostra de 30-50 N2 com resolutionreason = Multiprompt handover para confirmar padrão.
- [ ] Hipótese: Os conteúdos N2 de maior volume (vistoria, pagamento serviço, oficina credenciada) são candidatos a transformação agêntica se Darwin tiver APIs disponíveis. | Validação necessária: validar com Darwin se há APIs de status de pedido/vistoria/pagamento de sinistro.
- [ ] Hipótese: O upgrade de gpt_model vai reduzir GenCX sem regredir retenção. | Validação necessária: A/B test em 7 dias após mudança.

## Sugestões de Dados Adicionais
- [ ] Acesso ao repositório de Eddie flows do Darwin para avaliar quais flows têm erro e quais são candidatos a agêntico.
- [ ] Histórico de CSAT por período para identificar se a tendência positiva da última semana é correlacionada com alguma mudança já feita.
- [ ] Auditoria manual (pelo menos 50 tickets de N2) para calibrar % de erro 1/2 na qualidade das respostas.
