# Decisões de modelagem — EvenTicket

1. **Separar Local de Evento.** Um mesmo local recebe diversos eventos; armazenar dados do local em cada evento provocaria repetição e divergência. `Sedia` é 1:N.
2. **Separar Categoria.** A categoria é reutilizada por vários eventos. Cada evento possui uma categoria; `Classifica` é 1:N.
3. **Representar Inscrição como entidade associativa.** O relacionamento entre Evento e Participante é N:N e possui atributos próprios (`id_inscricao`, datas, status). No modelo lógico, há duas FKs e unicidade do par participante-evento.
4. **Manter cancelamentos sem apagar a inscrição.** O status muda para cancelada e a inscrição deixa de ocupar vaga; isso preserva a existência do registro. A política de reinscrição deve ser definida explicitamente devido à unicidade do par.
5. **Modelar Atividade como entidade fraca.** Uma atividade pertence a um Evento e usa identificação composta (`evento_codigo`, `numero_atividade`). Em Chen, a representação usa retângulo duplo para entidade fraca e losango duplo em `Possui`. O número da atividade é **identificador parcial**, não atributo derivado.
6. **Tratar telefone como multivalorado.** O modelo conceitual usa elipse dupla; no lógico há `telefone_participante`, separando as ocorrências.
7. **Usar atributos derivados.** `idade` deriva da data de nascimento e `vagas_disponiveis` da capacidade menos as inscrições ativas; não são persistidos no modelo lógico.
8. **Representar endereço como composto.** No conceitual, logradouro, número e cidade são partes de `endereco`; no lógico tornam-se colunas separadas de `local`.
9. **Capacidade do evento limitada à do local.** Regra acrescentada pelo grupo que compara registros de duas tabelas; depende de verificação de processo ou implementação adicional.
10. **Notação.** DER representado em notação de Chen, conforme a disciplina; modelo lógico com tabelas, PK e FK.

## Alternativas e limitações
- **Alternativa descartada:** repetir local e categoria dentro da tabela Evento, o que aumenta redundância.
- **Limitação:** o modelo de sete tabelas documenta a estrutura mas não implementa o controle de vagas; um `CHECK` comum não conta inscrições de outra tabela. A implementação futura deve ser atômica e resistente a inscrições simultâneas.
- **Ponto de revisão:** `UNIQUE(participante_cpf, evento_codigo)` proíbe qualquer segundo registro para o mesmo par, inclusive após cancelamento.
- **Ponto de revisão visual:** o DER anterior entregue individualmente usava traços em `numero_atividade`; na reconstrução editável a identificação parcial foi explicitada.
