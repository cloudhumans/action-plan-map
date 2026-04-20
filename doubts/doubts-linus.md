# Dúvidas / Validações Pendentes — Linus

**Gerado em:** 20/04/2026
**CS Owner:** Bruna Chaves
**Skill:** ch-action-plan v5.1

---

## 1. Trigger da queda: mudança no cliente ou na config?

**Contexto:** Retenção subiu para 67,77% na semana 30/03-05/04 e caiu para 58,39% na semana 13/04. O que mudou nessas 2 semanas?

**Como validar:**
- Checar no Slack #ch-linus se cliente lançou nova campanha, mudou fluxo de logística, ou teve ruptura de estoque
- Ver se houve alguma mudança em `cloudblockslog` ou `projects_config` nas datas de 06/04 a 12/04
- Confirmar no time de engenharia se o modelo ou integrações foram alterados

**Relevância:** Se o trigger for externo (cliente), as ações de config/conteúdo terão impacto parcial. Se for interno, revertê-lo pode ser a ação P0 real.

---

## 2. max_clarification_attempts = 2 é intencional ou histórico?

**Contexto:** Ajuste para 3 é a recomendação da ação P0 #1, mas se foi configurado em 2 deliberadamente por alguma política Linus, precisa revisar antes.

**Como validar:**
- Checar no doc de onboarding do Linus se há referência ao valor
- Perguntar ao cliente se o comportamento "ClaudIA desiste rápido" é preferível a "ClaudIA pergunta 3x"
- Monitorar CSAT por 7 dias após o ajuste

**Relevância:** A ação vale +49 N1/mês — é o maior impacto do plano. Se houver restrição, buscar alternativa (ex: ativar apenas `enlightenmentQuestionLimit`).

---

## 3. O que tem dentro dos 14 casos de "No relevant content" da última semana?

**Contexto:** Triplicou de 5 → 14 tickets. Indica tema novo não coberto. Ação P0 #4 pede criação de conteúdos.

**Como validar:**
- Extrair cloudchatids com `resolutionreason='No relevant content found' AND project='linus' AND date BETWEEN '2026-04-13' AND '2026-04-19'`
- Rodar skill `ids-no-relevant-content` ou análise manual das mensagens
- Clusterizar por tema

**Relevância:** Sem saber os temas, a ação fica genérica. A conversão de content_new cai de 60% → 30% se criarmos conteúdos que não cobrem a real demanda.

---

## 4. Upgrade de modelo GPT tem custo aprovado?

**Contexto:** Ação P2 #9 pede upgrade CHATGPT4o1120 → CHATGPT52CHAT. Custo por token é maior.

**Como validar:**
- Confirmar com Produto se há budget aprovado para o upgrade
- Validar com Linus (cliente) se aumento de custo é aceitável no contrato atual

**Relevância:** Se não houver aprovação, manter modelo atual e focar nas demais ações. Linus_email já está em CHATGPT52CHAT — provavelmente custo já está OK.

---

## 5. Eddie INTERACTIVE de status pedido — a API de rastreio está funcionando?

**Contexto:** Conteúdo ID `68ac92970e038847c35060c9` com 117 tickets e retenção 51,28%. Pode ser problema de prompt OU problema de integração (API retorna vazio/erro).

**Como validar:**
- Checar logs do flow nos últimos 14 dias
- Rodar teste manual com código de rastreio conhecido
- Confirmar se há fallback quando API falha

**Relevância:** Se for bug de integração, reescrita do prompt não resolve — é task para engenharia/Linus.
