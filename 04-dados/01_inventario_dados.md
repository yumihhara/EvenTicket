# Inventário de dados — EvenTicket

| Entidade | Identificador | Informações necessárias | Papel no cenário |
|---|---|---|---|
| Local | `id_local` | nome, endereço (logradouro, número, cidade), capacidade | Local que sedia um ou vários eventos. |
| Evento | `codigo` | nome, data, capacidade_maxima, local, categoria; vagas_disponiveis (derivado) | Evento promovido pela produtora. |
| Categoria | `id_categoria` | nome | Classificação do evento: Música, Tecnologia etc. |
| Atividade | (`evento_codigo`, `numero_atividade`) | título, horário_início, horário_fim | Programação de um evento; depende dele. |
| Participante | `cpf` | nome, email, data_nascimento; telefone (multivalorado); idade (derivado) | Pessoa que se cadastra e pode se inscrever. |
| Inscrição (associativa) | `id_inscricao` | participante, evento, data_inscricao, status, data_cancelamento | Vincula participante e evento; guarda situação e histórico do cancelamento. |

## Relacionamentos e cardinalidades
- `Local (0,N)` — **Sedia** — `Evento (1,1)`: um local pode sediar muitos eventos; cada evento ocorre num local.
- `Categoria (0,N)` — **Classifica** — `Evento (1,1)`: uma categoria agrupa eventos; cada evento tem uma categoria.
- `Evento (0,N)` — **Possui** — `Atividade (1,1)`: atividade só existe vinculada a um evento.
- `Evento (0,N)` — **Inscrição** — `Participante (0,N)`: relacionamento N:N resolvido pela associativa.

## Tipos especiais
- **Composto**: endereço de Local em logradouro, número e cidade.
- **Multivalorado**: telefone de Participante (vira tabela independente no lógico).
- **Derivados**: idade calculada pela data de nascimento; vagas_disponiveis calculadas por `capacidade_maxima - inscrições ativas`. Não armazenados no modelo lógico proposto.
- **Entidade fraca**: Atividade, identificada pelo código do evento mais seu número dentro do evento.

## Escopo
Não foram introduzidas entidades de pagamento, ingressos vendidos ou equipamentos de palco, pois não aparecem na modelagem apresentada pela equipe.
