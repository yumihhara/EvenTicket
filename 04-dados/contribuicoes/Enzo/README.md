# Contribuição Individual – Enzo Zaffaroni

**Projeto:** EvenTicket – Controle de Eventos  
**Equipe:** Grupo 05  
**Integrante:** Enzo Zaffaroni  
**Data da atividade:** 06/11/2026

## Atividades realizadas

Responsável pela consolidação do **modelo conceitual (DER)** do EvenTicket, reunindo em um único diagrama, na **notação de Chen**, as contribuições do grupo.

O modelo reúne as cinco entidades principais (**Local, Evento, Participante, Categoria e Atividade**) e a entidade associativa **Inscrição**, representando os relacionamentos **Sedia, Classifica, Possui e Inscrição**.

Também foram conferidos os requisitos mínimos de modelagem previstos no edital: um relacionamento **N:N** entre Participante e Evento, resolvido por Inscrição; a entidade dependente **Atividade**; o atributo multivalorado **telefone**; e os atributos derivados **idade** e **vagas_disponiveis**.

Foram registradas as decisões de modelagem para que a equipe pudesse justificá-las na defesa, incluindo a separação de Local e Categoria como entidades, a dependência de Atividade em relação a Evento e a escolha da notação de Chen.

## Arquivos desta contribuição

- [Entrega_Enzo_Zaffaroni.pdf](./Entrega_Enzo_Zaffaroni.pdf) - Documento individual de 06/11/2026, com atividades realizadas, justificativa e DER anexado.
- [der_consolidado_enzo.drawio](./der_consolidado_enzo.drawio) - Versão editável do DER consolidado, baseada no diagrama conceitual oficial do grupo; pode ser aberta no diagrams.net (draw.io).
- [der_consolidado_enzo.drawio.pdf](./der_consolidado_enzo.drawio.pdf) - Versão em PDF do DER consolidado, para visualização.

## Observação

Esta contribuição individual documenta a consolidação do modelo conceitual e serve como referência para o projeto EvenTicket. Os arquivos oficiais e consolidados da equipe permanecem em `04-dados/`, especialmente `02_modelo_conceitual_v1` e `03_decisoes_modelagem.md`.
