# Catálogo de regras de negócio — EvenTicket

**Origem:** RN-01 a RN-03 vêm da narrativa do edital; RN-04 e RN-05 foram acrescentadas nos slides do Grupo 05; RN-06 e RN-07 explicitam decisões de modelagem apresentadas.

| Código | Regra de negócio | Onde aparece no modelo | Forma de atendimento |
|---|---|---|---|
| RN-01 | Uma inscrição só é aceita se ainda houver vaga no evento. | `Evento.capacidade_maxima` e `Inscricao.status`; derivado `vagas_disponiveis` | Contar inscrições **ativas** antes de confirmar outra. Regra de processo a implementar com controle de concorrência; não pode ser garantida por um `CHECK` simples entre tabelas. |
| RN-02 | Cancelar uma inscrição libera a vaga correspondente. | `Inscricao.status` e `data_cancelamento` | Manter registro e alterar status de `ativa` para `cancelada`; a contagem de ocupação considera só ativas. |
| RN-03 | Um participante não pode se inscrever duas vezes no mesmo evento. | `Inscricao.participante_cpf`, `evento_codigo` | `UNIQUE(participante_cpf, evento_codigo)`, como no modelo lógico apresentado. |
| RN-04 | Todo evento pertence a um único local e a uma única categoria. | `Local`–`Evento` e `Categoria`–`Evento`, 1:N | Chaves estrangeiras obrigatórias em `Evento`. |
| RN-05 | A capacidade máxima de um evento não ultrapassa a capacidade do local. | `Local.capacidade`, `Evento.capacidade_maxima` | Comparação entre tabelas no cadastro/edição do evento; regra adicional a implementar. |
| RN-06 | Uma atividade existe vinculada a um único evento. | `Evento`–`Atividade`, 1:N; Atividade fraca | PK composta (`evento_codigo`, `numero_atividade`); FK para Evento. |
| RN-07 | Um participante pode ter vários telefones. | `Participante.telefone` multivalorado | Tabela `telefone_participante`. |

## Decisão que precisa ser defendida
A `UNIQUE(participante_cpf, evento_codigo)` também impede uma **nova linha** de inscrição após cancelamento, mesmo que a anterior esteja cancelada. No modelo atual, uma futura reinscrição demandaria reativar a mesma inscrição, se essa operação for permitida. É preciso manter essa decisão explícita; se o objetivo for conservar múltiplos ciclos históricos de inscrição/cancelamento, o modelo precisará ser revisto.

## Exemplo
Se o evento possui capacidade 100 e 98 inscrições ativas, `vagas_disponiveis = 2`. Cancelando uma inscrição ativa, restam 97 ativas e 3 vagas.
