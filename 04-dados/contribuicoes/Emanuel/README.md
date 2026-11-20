# Contribuição Individual – Emanuel

**Projeto:** EvenTicket – Controle de Eventos  
**Equipe:** Grupo 05  
**Integrante:** Emanuel

## Atividades realizadas

Responsável por iniciar o **modelo lógico relacional (versão 1)** do EvenTicket, a partir do Diagrama Entidade-Relacionamento (DER) desenvolvido pela equipe.

O modelo foi organizado em **sete tabelas**: `local`, `categoria`, `evento`, `atividade`, `participante`, `telefone_participante` e `inscricao`. Foram definidas as chaves primárias (PK), chaves estrangeiras (FK) e as transformações dos relacionamentos:

- **1:N:** chaves estrangeiras no lado N, como `local_id` e `categoria_id` em `evento`.
- **N:N:** tabela associativa `inscricao`, com unicidade para o par (`participante_cpf`, `evento_codigo`).
- **Entidade fraca:** `atividade`, identificada pela chave primária composta (`evento_codigo`, `numero_atividade`).
- **Atributo multivalorado:** `telefone`, representado pela tabela `telefone_participante`.

Também foram indicadas chaves estrangeiras obrigatórias em `evento` e `inscricao`, além da restrição de valores para `inscricao.status` (`ativa` ou `cancelada`). Os atributos `idade` e `vagas_disponiveis` não foram incluídos como colunas, por serem derivados de outras informações.

## Arquivos desta contribuição

- **Entrega_Emanuel.pdf** – Documento da atividade individual de 06/11/2026, com descrição das atividades, justificativas e o modelo lógico apresentado.
- **modelo_logico_emanuel.drawio** – Arquivo editável do modelo lógico relacional utilizado na consolidação da contribuição.

## Observação

Esta contribuição individual registra a elaboração inicial do modelo lógico e serve como referência para a consolidação do modelo de dados oficial do projeto EvenTicket. Conforme indicado na entrega individual, o dicionário de dados e as regras de integridade foram previstos para etapas posteriores.
