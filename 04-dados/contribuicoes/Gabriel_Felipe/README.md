# Contribuição de Gabriel Felipe
Projeto: EvenTicket — Grupo 05
Origem: Entrega_Gabriel_Felipe_Xavier.pdf, produção individual de 06/11/2026.
O que foi definido
O relacionamento entre Participante e Evento é N:N: um participante pode estar em vários eventos e cada evento pode reunir vários participantes. A entidade associativa Inscrição resolve esse relacionamento e mantém dados próprios:
Campo
Finalidade
id_inscricao
Identificador substituto da inscrição
participante_cpf
Referência ao participante (FK no modelo lógico)
evento_codigo
Referência ao evento (FK no modelo lógico)
data_inscricao
Data da inscrição
status
ativa ou cancelada
data_cancelamento
Preenchida em caso de cancelamento
Decisões justificadas
Sem inscrições duplicadas: o par (participante_cpf, evento_codigo) deve ser único. Como essa decisão também impede uma segunda inscrição após cancelamento, a política de reinscrição precisa ser acordada pelo grupo.
Cancelamento sem exclusão: uma inscrição cancelada permanece no banco como histórico, mas deixa de contar nas vagas ocupadas.
Verificação de capacidade: antes de confirmar nova inscrição, é preciso contar as inscrições ativas do evento e comparar com a capacidade. Um CHECK tradicional, sozinho, não executa essa contagem em outra tabela. O mecanismo transacional seguro fica previsto para uma futura implementação.
Onde integrar na entrega da equipe
00_catalogo_rn.md: regras de não duplicidade, cancelamento e capacidade.
02_modelo_conceitual_v1: entidade associativa Inscrição no DER consolidado.
03_decisoes_modelagem.md: justificativa do N:N, da entidade associativa e de seus atributos.
04_modelo_logico_v1: tabela inscricao, PK, FKs e restrição UNIQUE.
06_regras_integridade.md: integridade de referências, status, unicidade e regra de vagas.
Este arquivo é uma contribuição individual a ser incorporada ao repositório coletivo; não substitui os sete documentos oficiais. O PDF do anexo é uma reprodução da página 2 da entrega individual, e o arquivo .drawio é uma reconstrução editável de apoio, não uma cópia exata da notação de Chen original.
