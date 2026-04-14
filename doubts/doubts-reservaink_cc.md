# Dúvidas e Gaps — Reservaink CC — 14/04/2026

## Dúvidas sobre Features/Configurações
- [ ] `clarificationsettings__enabled = NULL`: Está efetivamente desativado ou é um estado diferente de `false`? Confirmar com produto.
- [ ] `enlightenmentquestionlimit__enabled = false`: O que exatamente controla? Se ativado com limit=3, impacta os 5 N2 por "clarification limit reached"?
- [ ] `outputtransformation__enabled = false`: O que faz? Vale ativar para este projeto?
- [ ] `newtaggerenabled = NULL`: Está no sistema antigo de tagger? Migrar para novo pode melhorar classificação?
- [ ] `toneofvoice__enabled = NULL`: Diferente de base_prompt_modules? Se sim, qual o impacto de ativar?
- [ ] `frustrationthreshold = 12`: É muito tolerante? Apenas 42 N2 por frustração (1.64%) — pode estar deixando passar clientes frustrados sem escalar.
- [ ] `fup_max_minutes = 60`: Muito alto para chat? Pode estar atrasando o fechamento de tickets.

## Dados que Faltaram para Análise Completa
- [ ] CSAT por tag — não coletado em Layer 2 (GenCX estava saudável, priorizei outros sinais)
- [ ] Auditoria de tickets — não há dados de auditoria disponíveis para este projeto (projeto recente, provavelmente ainda sem auditoria configurada)
- [ ] Canal de atendimento (chat vs email vs WhatsApp) — distribuição por canal ajudaria a calibrar configs como splitMessages e FUP timing
- [ ] FlowPrompts configurados — não foi possível verificar quais FlowPrompts estão ativos (FORWARD_TO_HUMAN_CHECK, MULTIPROMPT, etc.)

## Hipóteses que Precisam de Validação
- [ ] Hipótese: O conteúdo "Problema com entrega" (0% retenção, 682 tickets) contém instrução de transferência no texto, funcionando como conteúdo N2 disfarçado de N1. | Validação: Ler o conteúdo completo no Hub e confirmar.
- [ ] Hipótese: O Multiprompt handover (307 tickets) indica que já existe alguma config de Venda do Bot, mas com prompt fraco. | Validação: Verificar FlowPrompts ativos no CloudBlocks.
- [ ] Hipótese: O projeto é recente (~4 semanas baseado no ramp-up de volume) e a IDS ainda está em fase de maturação. | Validação: Confirmar data de go-live com o AM.
- [ ] Hipótese: A queda contínua de retenção (41%→28%) pode ser causada por mudança no mix de temas dos tickets (mais temas complexos), não necessariamente piora da IDS. | Validação: Comparar distribuição de tags semana a semana.

## Sugestões de Dados Adicionais
- [ ] Acesso aos FlowPrompts ativos para validar se FORWARD_TO_HUMAN_CHECK já está configurado
- [ ] Distribuição de tickets por canal (chat/email/WhatsApp) para calibrar configs de UX
- [ ] Histórico de alterações na IDS nas últimas 4 semanas (novos conteúdos, edições, remoções)
- [ ] Dados de CSAT quando disponíveis (projeto pode não ter volume suficiente ainda)
