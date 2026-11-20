# Contribuição Individual – Emanuel

**Projeto:** EvenTicket – Controle de Eventos
**Equipe:** Grupo 05
**Integrante:** Emanuel

## Atividades realizadas

Responsável por iniciar o modelo lógico relacional (04_modelo_logico_v1) a partir do DER, com 7 tabelas: local, categoria, evento, atividade, participante, telefone_participante e inscricao. Aplicou as regras de transformação: entidade vira tabela; relacionamento 1:N vira chave estrangeira no lado N (local_id e categoria_id em evento); N:N vira a tabela associativa inscricao, com unicidade do par (participante_cpf, evento_codigo); entidade fraca vira chave primária composta (evento_codigo, numero_atividade); atributo multivalorado vira tabela própria. Marcou como obrigatórias as chaves estrangeiras de evento e inscricao e registrou a restrição de domínio de inscricao.status (somente ativa ou cancelada). Os atributos derivados idade e vagas_disponiveis não são armazenados como colunas. Esta é a versão v1: normalização, dicionário de dados e regras de integridade seguem nas próximas etapas.

## Arquivos desta contribuição

- [Entrega_Emanuel.pdf](./Entrega_Emanuel.pdf) – Documento com a descrição das atividades realizadas, justificativas e diagrama.
- [modelo_logico_v1_emanuel.drawio](./modelo_logico_v1_emanuel.drawio) – Arquivo editável do diagrama do modelo lógico relacional v1.

## Observação

Esta contribuição individual será utilizada como referência para a consolidação do modelo de dados oficial do projeto EvenTicket.
