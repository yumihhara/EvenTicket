# Dicionário de dados — modelo lógico EvenTicket (v1)

**Convenção:** PK = chave primária; FK = chave estrangeira; NN = obrigatório/não nulo. Tipos são **sugestões de projeto**, pois os slides não especificam um SGBD nem tipos SQL concretos.

## `local`
| Campo | Tipo sugerido | Regra | Significado |
|---|---|---|---|
| id_local | INTEGER | PK, NN | Identificador do local |
| nome | VARCHAR(120) | NN | Nome |
| logradouro | VARCHAR(160) | NN | Logradouro do endereço |
| numero | VARCHAR(20) | NN | Número/complemento de identificação |
| cidade | VARCHAR(100) | NN | Cidade |
| capacidade | INTEGER | NN, > 0 | Limite físico do local |

## `categoria`
| Campo | Tipo sugerido | Regra | Significado |
|---|---|---|---|
| id_categoria | INTEGER | PK, NN | Identificador da categoria |
| nome | VARCHAR(80) | NN | Classificação do evento |

## `evento`
| Campo | Tipo sugerido | Regra | Significado |
|---|---|---|---|
| codigo | INTEGER | PK, NN | Código do evento |
| nome | VARCHAR(140) | NN | Nome do evento |
| data | DATE | NN | Data programada |
| capacidade_maxima | INTEGER | NN, > 0 | Limite de inscrições do evento |
| local_id | INTEGER | FK → local.id_local, NN | Local onde ocorre |
| categoria_id | INTEGER | FK → categoria.id_categoria, NN | Categoria atribuída |

## `participante`
| Campo | Tipo sugerido | Regra | Significado |
|---|---|---|---|
| cpf | CHAR(11) | PK, NN | CPF como texto de 11 dígitos |
| nome | VARCHAR(140) | NN | Nome |
| email | VARCHAR(254) | NN | E-mail de contato |
| data_nascimento | DATE | NN | Base de cálculo da idade |

## `telefone_participante`
| Campo | Tipo sugerido | Regra | Significado |
|---|---|---|---|
| participante_cpf | CHAR(11) | PK (parte), FK → participante.cpf, NN | Titular do telefone |
| telefone | VARCHAR(20) | PK (parte), NN | Número cadastrado |

## `atividade`
| Campo | Tipo sugerido | Regra | Significado |
|---|---|---|---|
| evento_codigo | INTEGER | PK (parte), FK → evento.codigo, NN | Evento ao qual pertence |
| numero_atividade | INTEGER | PK (parte), NN | Numeração dentro do evento |
| titulo | VARCHAR(140) | NN | Título da atividade |
| horario_inicio | TIME | NN | Horário de início |
| horario_fim | TIME | NN | Horário de término |

## `inscricao`
| Campo | Tipo sugerido | Regra | Significado |
|---|---|---|---|
| id_inscricao | INTEGER | PK, NN | Identificador de inscrição |
| participante_cpf | CHAR(11) | FK → participante.cpf, NN | Pessoa inscrita |
| evento_codigo | INTEGER | FK → evento.codigo, NN | Evento escolhido |
| data_inscricao | DATE | NN | Data de inscrição |
| status | VARCHAR(12) | NN, ativa/cancelada | Situação atual |
| data_cancelamento | DATE | Opcional | Data de cancelamento, quando aplicável |

Restrição adicional em `inscricao`: `UNIQUE(participante_cpf, evento_codigo)`.

## Não armazenados
- `Participante.idade`: calculada com `data_nascimento` e a data de referência.
- `Evento.vagas_disponiveis`: `capacidade_maxima - COUNT(inscricoes com status = 'ativa')`.

> Revisão pendente do grupo: confirmar tipos, obrigatoriedade de e-mail/endereço, tratamento de data de cancelamento e se o modelo deve permitir nova inscrição após cancelamento.
