# Dúvidas e Gaps — Nextfit — 23/04/2026

## Dúvidas sobre Features/Configurações
- [ ] `clarificationsettings__enabled`: Está `null` no project_setup. Não está ativo nem desativado? Verificar se isso é intencional ou se precisa ser explicitamente ativado. Com 7% dos N2 por "clarification limit reached", pode haver oportunidade.
- [ ] `toneofvoice__enabled`: Também `null`. Diferente de Base Prompt modules? Validar com produto.
- [ ] `outputtransformation__enabled`: OFF. O que exatamente faz? Pode ajudar com formatação de respostas longas?
- [ ] `startwithbotconfiguration__enabled`: OFF. Em qual contexto deveria estar ON?
- [ ] `enlightenmentquestionlimit__enabled`: OFF com limit=3. Deveria estar ON para evitar loops de perguntas?

## Dados que Faltaram para Análise Completa
- [ ] Dados de auditoria (erros tipo 1, 2, 3) — não foram consultados nesta rodada mas seriam valiosos para validar qualidade
- [ ] CSAT por tag — não coletado; ajudaria a priorizar quais conteúdos melhorar por satisfação
- [ ] Breakdown de "transfer message" — 56% dos N2 são por transfer message. Precisamos entender quais conteúdos acionam o FORWARD_TO_HUMAN. Pode haver uma Venda do Bot (FORWARD_TO_HUMAN_CHECK) desativada

## Hipóteses que Precisam de Validação
- [ ] Hipótese: A queda de retenção de 57% para 40-45% coincide com aumento de volume (2599 tickets na semana de 06/04). Possível causa: campanha/sazonalidade trouxe perfil de cliente diferente? | Validação: checar com AM se houve evento especial
- [ ] Hipótese: As 67 duplicatas exatas são resultado de importação/migração de IDS mal feita | Validação: checar com time de onboarding
- [ ] Hipótese: 56% de N2 por "transfer message" pode ser reduzido com Venda do Bot (FORWARD_TO_HUMAN_CHECK) | Validação: checar se está ativo e, se não, se o cliente aceita ativar (ESTA É POTENCIALMENTE A MAIOR ALAVANCA DE RETENÇÃO, mas é mudança significativa de comportamento — não incluída no plano por instrução de evitar mudanças bruscas)

## Sugestões de Dados Adicionais
- [ ] Auditoria semanal mínima para validar qualidade das respostas
- [ ] Dados de Eddie flows — verificar se há Eddies ativos e com que performance
- [ ] Análise de FORWARD_TO_HUMAN_CHECK — se ativo, qual % das tentativas de retenção está funcionando
