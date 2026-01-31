Projeto realizado para a disciplina de Fundamento de Banco de Dados. 

O projeto foi divido en três etapas que consistiam em modelagem EER, 
modelagem relacional, criação e povoamento do banco de dados, um CRUD e um gráfico.

Escolhemos o tema: Gestão de Patrimônios Históricos 
a equipe foi composta por:

Graziele Ferreira Barbosa
grazielebarbosa.cc@gmail.com

Davyd Pinheiro Jacinto
davydpinheiro0@gmail.com

João Lucas Patrício de Lima Veras 
joaolucasplv@gmail.com

Escolhemos o tema: Gestão de Patrimônios Históricos.
Introdução ao projeto:
O Instituto do Patrimônio Histórico e Artístico Nacional (IPHAN) é o principal  órgão responsável pelo processo administrativo
de tombamento no nível federal, e tem a responsabilidade de proteção, preservação e fiscalização de bens tombados. Para um bem 
ser tombado, é necessário um pedido direcionado ao IPHAN ou algum órgão estadual ou municipal também responsável. Após o pedido, 
o órgão avalia o pedido de tombamento, avaliando a sua relevância histórica, cultural e artística do bem. A partir da avaliação,
o órgão responsável pode solicitar uma audiência pública para ouvir a comunidade e especialistas para avaliar os impactos do 
tombamento. Se o processo for aceito, ele é encaminhado para o IPHAN para aceitar ou rejeitar o pedido. Se o pedido for aceito, 
o bem é escrito nos livros do tombo. 
Os objetivos gerais da aplicação é gerenciar o processo de pedido, manutenção, análise, e visitas do patrimônio. Os usuários
envolvidos são os órgãos estaduais ou municipais responsáveis, o IPHAN e a comunidade no geral. 
O propósito do banco de dados é reunir todas as informações, permitindo maior controle e acesso aos dados.

Antes de partirmos para a modelagem EER, definimos os requisitos funcionais que faziam sentido para representar o mini mundo de uma 
gestão de patrimônios históricos. Dividimos os requisitos funcionais em três categorias: Cadastros Gerais, processos de visita e 
processos de solicitação externa. Os cadastros gerais reúnem as informações básicas necessárias ao funcionamento do sistema.
Os processos de visita tratam do planejamento e registro das visitas aos patrimônios. Já os processos de solicitação externa 
englobam pedidos como manutenção, tombamento, análises técnicas e audiências públicas.

catrastros gerais:
RF01-Cadastro de Patrimônio
RF02 - CADASTRO/EDIÇÃO/APAGAMENTO DE LOCAL
RF03 - Cadastro/Edição/Apagamento de responsável Técnico
RF04 - Cadastro/Edição/Apagamento de autor do pedido formal
RF05 - Cadastro/Edição/Apagamento de órgão responsável

Processo de visita:
RF06-Cadastro de Visita
RF07 - Cadastro Organização da visita 
RF08 - Solicitação de visita

Processo de solicitação externa:
RF09 - Solicitação de manutenção
RF10 - Solicitação de Audiência Pública
RF11 - Solicitação de análise técnica
RF12 - Solicitação de Tombamento

Modelo EER, Relacional, Banco de Dados e povoamento:
https://drive.google.com/drive/u/2/folders/12wVVYI_FQBVq7ylQ_u4EtPlXHdRswNd8

Para o CRUD da aplicação, fiz a tela referente às visitas aos patrimônios. É possível cadastrar uma visita informando o local, dia, 
horário de entrada e saída e a quantidade de pessoas. Também é possível editar e excluir uma visita. Na consulta com filtragem fiz uma
filtro por data, onde coloca a data e uma quantidade mínima de pessoas e é retornado as informações das visitas naquele dia. 
Para ser possível adicionar o local da visita, adicionei uma coluna na tabela visita_cultural:
alter table visita_cultural add column localizacao varchar(300);
Após isso, peguei o nome do patrimônio x que estava relacionado com o id_vista e atualizei a tabela visita_cultural com  nova coluna localizacao:
update visita_cultural vc set localizacao = p.nome_atribuido from recebe_visita_cultural rvc join patrimonio p on p.id_patrimonio = rvc.id_patrimonio where vc.id_visita = rvc.id_visita_cultural;
Sobre o gráfico, fiz uma consulta que mostra a quantidade de pessoas que visitaram cada patrimônio registrado. Usei a função coalesce porque como relacionei a nova coluna 
(localização) em visita_cultural ao nome do patrimônio, há novas inserções de lugares que não estão inseridas no patrimônio e não apareciam na consulta pois são lugares que 
não estavam no povoamento e não mexi nessa parte. Essa função retorna o nome que está em algum dos parâmetros. Ou no nome do patrimônio ou na localização, ambos são as 
mesmas coisas porém povoados em momentos distintos e com propósitos diferentes. Segue a consulta e o gráfico.

