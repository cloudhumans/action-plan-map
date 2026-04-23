# Dúvidas e Gaps — Nextfit — 23/04/2026

## Dúvidas sobre Features/Configurações
- [ ] FORWARD_TO_HUMAN_CHECK: Verificar se já há config de Venda do Bot parcial ativa
- [ ] query_transform: Validar impacto em latência antes de ativar (7k+ tickets/mês)
- [ ] agentic_enabled: Feature nova, não documentada
- [ ] output_transformation: Verificar se existe e qual impacto
- [ ] tone_of_voice_enabled = null: Diferente de base_prompt_modules?

## Dados que Faltaram
- [ ] CSAT por tag
- [ ] Dados de auditoria (% erros, % tags corretas)
- [ ] Eddie flows ativos e métricas
- [ ] Conversas por canal

## Hipóteses que Precisam de Validação
- [ ] GenCX 16.8% parcialmente causado por conteúdos de baixa qualidade (8 conteúdos com retenção <50%)
- [ ] Par duplicado "Como Solicitar Atendimento" confunde classificador
- [ ] Muitos N2 por transfer message são frustração, não casos não resolvíveis
