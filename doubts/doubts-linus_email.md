# Dúvidas / Validações Pendentes — Linus Email

**Gerado em:** 20/04/2026
**CS Owner:** Bruna Chaves
**Skill:** ch-action-plan v5.1

---

## 1. ConversationHistoryQueryTransformation foi intencionalmente desativado?

**Contexto:** Ação P0 #1 recomenda ativar `conversationHistoryQueryTransformationSettings.enabled=true`. Se foi desativado por problema específico (custo de tokens, latência, alucinação), precisa revisar antes.

**Como validar:**
- Verificar no histórico de `projects_config` ou `cloudblockslog` se a flag já foi `true` e foi revertida
- Perguntar ao time de Produto / Engenharia se há restrição conhecida para email
- Comparar com outros projetos de email (bowe, doc9_whom_email, linus_email) para ver padrão

**Relevância:** É a única ação que isoladamente pode recuperar 12 N1/mês. Se houver razão técnica para manter desativado, precisamos encontrar alternativa.

---

## 2. Handover by timeout DOBROU — é problema real ou flutuação estatística?

**Contexto:** 2 → 5 tickets em 1 semana. Com volume baixo (200/mês), uma oscilação de 3 tickets pode ser ruído, mas a ação P0 #3 trata como sinal real.

**Como validar:**
- Extrair os 5 cloudchatids da semana 13/04 com `resolutionreason LIKE '%timeout%'`
- Inspecionar conversas individualmente: são erros técnicos ou clientes que realmente abandonaram?
- Verificar `maximumMinutesWithoutResponse` atual — se estiver configurado como canal chat (10min), aumentar para 24h é essencial

**Relevância:** Se todos forem abandono orgânico, a ação tem impacto zero. Se houver erro técnico travando, impacto pode ser maior que o estimado.

---

## 3. INTERACTIVE "status pedido" com 25,93% GenCX ruim — é bug do flow ou resposta correta mas insatisfatória?

**Contexto:** Retenção alta (71,43%) mas qualidade baixa (25,93% GenCX ruim) sugere que ClaudIA "retém" com resposta errada. Ação P0 #2 assume problema no prompt.

**Como validar:**
- Rodar `ids-quality-eval` no conteúdo específico
- Amostrar 10 conversas marcadas como GenCX ruim
- Validar se API de rastreio retorna dados corretos nesses casos

**Relevância:** Se a API está retornando dados certos e o prompt só formata mal, reescrita resolve. Se a API falha silenciosamente, problema é de integração.

---

## 4. Ativar Venda do Bot em canal email — cliente concorda?

**Contexto:** Ação P0 #4 propõe ativar retenção de handover por prompt. Em email, isso significa que ClaudIA vai tentar negociar com cliente antes de transferir — pode gerar atrito.

**Como validar:**
- Conversar com Linus (cliente) sobre política de atendimento para email
- Mostrar exemplos do FORWARD_TO_HUMAN_CHECK + MULTIPROMPT para o cliente aprovar
- Validar com outros clientes de email (doc9, etc) se essa tática funcionou

**Relevância:** Se o cliente rejeitar, a ação é perdida (6 N1/mês). Melhor perguntar antes de implementar.

---

## 5. ProblemResolvedChecker (FUP) para email — política explícita?

**Contexto:** `fup_active=false` no linus_email vs. `true` no linus. Pode ser intencional ou esquecimento.

**Como validar:**
- Revisar contratos e handover doc do Linus
- Perguntar diretamente ao cliente se quer FUP também no email
- Benchmark: outros projetos de email têm FUP ativado?

**Relevância:** A ação P2 #11 é marcada como "NÃO ativar cegamente" — precisa validação explícita antes. Baixa prioridade.

---

## 6. Volume baixo (200/mês) — vale investir tantas horas de ajuste?

**Contexto:** O impacto total de +63 N1/mês é menor em termos absolutos que qualquer projeto Tier 1. Mas em termos percentuais (+12 a +18pp) é gigante.

**Como decidir:**
- Se email é estratégico para Linus (canal premium, casos complexos), vale 100% do esforço
- Se é canal marginal, priorizar linus (chat) que tem 10x o volume

**Relevância:** Define o esforço relativo que a Bruna deve investir nas 2 threads.
