
# Gestão de Petrimônios Históricos

Projeto realizado para a disciplina de **Fundamentos de Banco de Dados**.

Relato de projeto passo a passo: [Uploading GESTÃO DE PATRIMONIO HISTORICO (2).pdf…]()

O projeto foi dividido em etapas, que consistiam em:
- Modelagem **EER**
- Modelagem **Relacional**
- Criação e povoamento do **Banco de Dados**
- Implementação de um **CRUD**
- Geração de um **gráfico**

---

### Equipe
- **Graziele Ferreira Barbosa**  
  📧 grazielebarbosa.cc@gmail.com

- **Davyd Pinheiro Jacinto**  
  📧 davydpinheiro0@gmail.com

- **João Lucas Patrício de Lima Veras**  
  📧 joaolucasplv@gmail.com

---

## Introdução

O **Instituto do Patrimônio Histórico e Artístico Nacional (IPHAN)** é o principal órgão responsável pelo processo administrativo de tombamento em nível federal, tendo como atribuições a **proteção, preservação e fiscalização** de bens tombados.

Para que um bem seja tombado, é necessário um pedido direcionado ao IPHAN ou a algum órgão estadual ou municipal também responsável. Após o pedido, o órgão avalia sua **relevância histórica, cultural e artística**. A partir dessa avaliação, pode ser solicitada uma **audiência pública**, com a participação da comunidade e de especialistas, para avaliar os impactos do tombamento.

Caso o processo seja aceito, ele é encaminhado ao IPHAN para decisão final. Se aprovado, o bem é inscrito nos **Livros do Tombo**.

O objetivo geral da aplicação é **gerenciar o processo de pedido, manutenção, análise e visitas aos patrimônios históricos**. Os usuários envolvidos são:
- Órgãos estaduais ou municipais responsáveis
- IPHAN
- Comunidade em geral

O propósito do banco de dados é **centralizar as informações**, permitindo maior controle e acesso aos dados.

---

## Requisitos Funcionais

Antes de partir para a modelagem EER, foram definidos os **requisitos funcionais** que representam o mini-mundo da gestão de patrimônios históricos. Eles foram divididos em três categorias:

### 1. Cadastros Gerais
Reúnem as informações básicas necessárias ao funcionamento do sistema.

- **RF01** – Cadastro de Patrimônio  
- **RF02** – Cadastro / Edição / Apagamento de Local  
- **RF03** – Cadastro / Edição / Apagamento de Responsável Técnico  
- **RF04** – Cadastro / Edição / Apagamento de Autor do Pedido Formal  
- **RF05** – Cadastro / Edição / Apagamento de Órgão Responsável  

### 2. Processos de Visita
Tratam do planejamento e registro das visitas aos patrimônios.

- **RF06** – Cadastro de Visita  
- **RF07** – Cadastro da Organização da Visita  
- **RF08** – Solicitação de Visita  

### 3. Processos de Solicitação Externa
Englobam pedidos relacionados à gestão do patrimônio.

- **RF09** – Solicitação de Manutenção  
- **RF10** – Solicitação de Audiência Pública  
- **RF11** – Solicitação de Análise Técnica  
- **RF12** – Solicitação de Tombamento  

---

## Modelos e Banco de Dados

Os modelos **EER**, **Relacional**, bem como o **Banco de Dados** e seu **povoamento**, estão disponíveis no link abaixo:

🔗 https://drive.google.com/drive/u/2/folders/12wVVYI_FQBVq7ylQ_u4EtPlXHdRswNd8

---

## CRUD da Aplicação

O projeto utiliza Python como linguagem principal, sendo executado em Jupyter Notebook. O banco de dados utilizado é o PostgreSQL.

Para o CRUD da aplicação, foi desenvolvida a tela referente às **visitas aos patrimônios**. As funcionalidades incluem:

- Cadastro de visitas informando:
  - Local
  - Data
  - Horário de entrada
  - Horário de saída
  - Quantidade de pessoas
- Edição e exclusão de visitas
- Consulta com filtragem por:
  - Data
  - Quantidade mínima de pessoas

### Alterações no Banco de Dados

Para possibilitar o registro do local da visita, foi adicionada uma nova coluna à tabela `visita_cultural`:

ALTER TABLE visita_cultural 
ADD COLUMN localizacao VARCHAR(300);

Em seguida, o nome do patrimônio relacionado à visita foi utilizado para atualizar essa nova coluna:

UPDATE visita_cultural vc
SET localizacao = p.nome_atribuido
FROM recebe_visita_cultural rvc
JOIN patrimonio p
  ON p.id_patrimonio = rvc.id_patrimonio
WHERE vc.id_visita = rvc.id_visita_cultural;

### Gráfico e Consulta

Foi criada uma consulta que exibe a **quantidade de pessoas que visitaram cada patrimônio registrado**.

Utilizou-se a função `COALESCE`, pois a nova coluna `localizacao` passou a armazenar nomes de lugares que nem sempre estão cadastrados na tabela de patrimônios. Dessa forma, a função retorna:

- O nome do patrimônio **ou**
- A localização registrada na visita

Isso garante que todos os registros apareçam no gráfico, mesmo aqueles inseridos posteriormente e fora do povoamento inicial.

A consulta e o gráfico resultante ilustram a quantidade de visitantes por patrimônio ou local registrado.

