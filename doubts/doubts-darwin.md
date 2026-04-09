# Dúvidas e Gaps — Darwin — 2026-04-06

## Dúvidas sobre Features/Configurações
- [ ] `query_transform` (OFF): O que exatamente faz? Darwin é seguradora — muitas perguntas são complexas. Poderia ajudar?
- [ ] `output_transformation` (OFF): Deveria estar ligada? Qual o impacto esperado?
- [ ] `agentic_enabled` (OFF): Feature nova — relevante para Darwin que tem processos multi-step (sinistro, cancelamento)?
- [ ] `attachment_handover` (OFF): Corretores frequentemente enviam documentos (apólices, fotos de sinistro). Ativar pode melhorar o fluxo.
- [ ] `clarification_enabled` (null): Campo retorna null — está usando o classificador? Qual o default?
- [ ] `tone_of_voice_enabled` (null): Campo retorna null — qual a configuração de tom atual?
- [ ] `max_no_valid_content` = 1: Extremamente baixo — após 1 tentativa sem conteúdo válido já transfere. É intencional? Aumentar para 2-3 poderia reter mais.
- [ ] `confidence_n2_threshold` = 0.90: Alto — está descartando conteúdos que poderiam ser usados com 85% de confiança. Testar redução para 0.85.

## Dados que Faltaram para Análise Completa
- [ ] **Detalhamento do Multiprompt handover (1,056 tix = 16.8%)**: Não consegui entender POR QUE tantos tickets saem por multiprompt. Preciso acessar LLM Calls para ver o padrão de conversa que leva ao handover. Está configurado como "Venda do Bot"? Se sim, está falhando sistematicamente.
- [ ] **IDS completa**: Quantos conteúdos existem? Quais são os Eddie flows ativos? Há duplicatas?
- [ ] **Eddie flows existentes**: 1,210 N2 por "Eddie returned N2" — quais flows estão retornando N2? São flows que realmente precisam transferir ou poderiam resolver?
- [ ] **Auditoria (Layer 3)**: Não executei — validar se os N1 atuais estão corretos, especialmente nas tags com GenCX alto.
- [ ] **Transfer messages**: 882 N2 por "transfer message sent" — quais mensagens do usuário estão sendo interpretadas como pedido de transferência? Base Prompt pode estar muito permissivo.
- [ ] **Detalhamento GenCX ruim em motivo_comercial (27.6%)**: Quais conversas específicas têm score ruim? O conteúdo está desatualizado ou a resposta é incorreta?

## Hipóteses que Precisam de Validação
- [ ] **Hipótese:** O Multiprompt handover (16.8%) está alto porque a "Venda do Bot" está mal configurada — tenta reter mas não tem conteúdo suficiente para convencer. **Validação:** Revisar FlowPrompt MULTIPROMPT e FORWARD_TO_HUMAN_CHECK no CloudBlocks.
- [ ] **Hipótese:** Os 882 N2 por "transfer message" podem incluir frases comuns de corretores de seguros ("preciso resolver isso urgente", "meu cliente precisa disso agora") sendo interpretadas como pedido de transferência. **Validação:** Amostra de LLM Calls com esse motivo de N2.
- [ ] **Hipótese:** GenCX ruim em motivo_comercial (27.6%) indica que o conteúdo sobre a própria Darwin (institucional, comercial) está desatualizado ou inadequado. **Validação:** Revisar os conteúdos N1 dessa tag na IDS.
- [ ] **Hipótese:** O modelo CHATGPT4o1120 pode estar contribuindo para timeouts (116 N2). **Validação:** Comparar com projetos que usam CHATGPT52CHAT para ver se timeout é menor.
- [ ] **Hipótese:** Posição do sinistro (404 tix) é plenamente automatizável via Eddie com API de sinistros. **Validação:** Confirmar com AM se Darwin possui API de consulta de sinistros disponível para integração.
- [ ] **Hipótese:** O `max_no_valid_content = 1` é o principal driver dos 405 N2 por "no relevant content" — transfere após 1 tentativa sem achar conteúdo. **Validação:** Aumentar para 2-3 em ambiente de teste e medir impacto.

## Sugestões de Dados Adicionais
- [ ] Acesso aos LLM Calls dos tickets com Multiprompt handover — entender o padrão
- [ ] Lista completa da IDS com contagem por tipo (N1/N2/INTERACTIVE)
- [ ] Eddie flows ativos e seus rates de N2 return
- [ ] FlowPrompts configurados (MULTIPROMPT, FORWARD_TO_HUMAN_CHECK, RESET_AND_REVERT)
- [ ] Amostra de conversas com "transfer message sent" para entender quais frases ativam
- [ ] Informação sobre APIs Darwin disponíveis (sinistros, apólices, financeiro) — crucial para Eddie flows
- [ ] Dados de auditoria (Layer 3) para % erro e N1 que deveriam ser N2
