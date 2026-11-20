# Regras de integridade — EvenTicket

## Integridade estrutural (restrições propostas)
| Regra | Mecanismo projetado | Efeito |
|---|---|---|
| Cada local, categoria, evento, participante e inscrição tem ID próprio. | PK em cada tabela | Impede repetição do mesmo identificador. |
| Evento aponta para local e categoria existentes. | FK obrigatórias `evento.local_id`, `evento.categoria_id` | Evita eventos sem referência válida. |
| Atividade aponta para evento existente. | FK `atividade.evento_codigo` + PK composta | Impede atividade órfã e numeração duplicada no mesmo evento. |
| Inscrição aponta para participante e evento existentes. | FKs em `inscricao` | Evita referências inválidas. |
| Um participante não possui duas inscrições para o mesmo evento. | `UNIQUE(participante_cpf, evento_codigo)` | Impede duplicação do par. |
| Status tem apenas valores conhecidos. | `CHECK (status IN ('ativa','cancelada'))` | Evita valores inesperados. |
| Capacidades positivas. | `CHECK (capacidade > 0)` e `CHECK (capacidade_maxima > 0)` | Evita limites impossíveis. |
| Mesmo telefone não é repetido para o mesmo CPF. | PK composta de `telefone_participante` | Evita duplicar número no cadastro. |

## Regras que dependem de verificação entre registros/tabelas
**RN-01 — Vagas:** antes de confirmar uma inscrição, consultar capacidade máxima do evento, contar inscrições **ativas** e rejeitar se o total atingir o limite. Em eventual implementação, a contagem e a inclusão devem estar protegidas por transação/controle de concorrência para evitar duas pessoas ocuparem a última vaga simultaneamente. Não é uma restrição `CHECK` simples entre tabelas.

**RN-02 — Cancelamento:** mudar `inscricao.status` para `cancelada` e registrar `data_cancelamento` preservando o registro. A inscrição deixa de participar da contagem de vagas ocupadas.

**RN-05 — Capacidade compatível com local:** impedir criar/atualizar `evento.capacidade_maxima` acima de `local.capacidade`; verificar também alterações posteriores da capacidade do local.

**Consistência de datas:** se o status for `cancelada`, deve haver uma data de cancelamento; se for `ativa`, a data de cancelamento normalmente fica vazia. Isso é refinamento sugerido, a ser aprovado pela equipe.

## Exemplo de validação
Evento com capacidade 100 e 98 inscrições ativas: há 2 vagas. Depois de cancelar uma inscrição ativa: 97 ativas e 3 vagas. Quando há 100 inscrições ativas, uma nova inscrição deve ser recusada.

## Limitações e política de reinscrição
A unicidade do par CPF-evento impede inserir nova linha após cancelamento. **Decisão a confirmar:** uma pessoa pode reativar sua inscrição cancelada (mediante nova verificação de vagas) ou não pode se reinscrever? Se for preciso preservar múltiplos ciclos de histórico, haverá alteração no modelo.

## Estado do trabalho
Documento de **projeto e validação conceitual**, não evidência de execução. O grupo não apresentou nos materiais disponibilizados um SGBD implementado, testes SQL ou transações em funcionamento.
