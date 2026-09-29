# 🏁 Sistema de Gestão de ONG

Plataforma web fullstack que conecta uma ONG a doadores e voluntários, centralizando a divulgação de campanhas de arrecadação, o controle de estoque de itens doados e o agendamento de coletas — substituindo o controle manual/informal (planilhas, WhatsApp) por um sistema único com papéis de acesso diferenciados.

## 🧑‍💻 Membros da equipe

| Matrícula | Nome | Curso |
|---|---|---|
| 581425 | Gildean Morais da Silva | Engenharia de Software |

## 💡 Objetivo Geral

Desenvolver um sistema web fullstack (Node.js/Express + Vue 3) que permita a uma ONG divulgar campanhas de arrecadação, controlar o estoque de itens recebidos e gerenciar o agendamento de coletas de doações, com controle de acesso baseado em papéis de usuário (administrador, voluntário e doador).

## 👀 Público-Alvo

- **ONGs de pequeno/médio porte** que arrecadam doações e hoje dependem de processos manuais (planilhas, grupos de WhatsApp, papel) tanto para divulgar campanhas quanto para controlar o que entra e sai do estoque.
- **Doadores** que quiserem contribuir com itens e agendar a retirada/entrega de forma organizada.
- **Voluntários** responsáveis por confirmar coletas e registrar a movimentação do estoque (entradas de doação e saídas para distribuição).

## 🌟 Impacto Esperado

- Reduzir o atrito no processo de doação: o doador vê as campanhas ativas, os itens que cada uma precisa, e agenda a coleta sem contato manual com a ONG.
- Dar visibilidade ao doador sobre o próprio histórico de contribuições.
- Permitir que a administração acompanhe, em um único painel, campanhas ativas, nível de estoque por item (com alerta de quantidade mínima) e agendamentos pendentes.
- Distribuir a carga operacional: voluntários confirmam coletas e registram movimentações de estoque sem depender do administrador para cada ação.

## 🧑‍🤝‍🧑 Papéis ou tipos de usuário da aplicação

| Papel | Descrição |
|---|---|
| **Usuário não logado (visitante)** | Acessa o mural público de campanhas, os detalhes de cada campanha (incluindo os itens necessários e o progresso de cada um) e a página institucional da ONG |
| **Doador** | Além do acesso público, agenda coletas de doação vinculadas a uma campanha, e edita/cancela **apenas os próprios** agendamentos; consulta seu histórico |
| **Voluntário** | Visualiza todos os agendamentos de coleta (com filtro por status/campanha) e atualiza o status de cada um; registra movimentações de estoque (entrada de doações recebidas, saída para distribuição) |
| **Administrador** | Faz CRUD completo das campanhas de arrecadação e dos itens necessários de cada campanha; visualiza e gerencia todos os agendamentos, independentemente de quem os criou |

## 🚩 Principais funcionalidades da aplicação

**Acessíveis a todos os usuários (área pública, sem login):**
- Visualizar o mural de campanhas de arrecadação ativas (listagem paginada)
- Visualizar os detalhes de uma campanha, incluindo o progresso de cada item necessário (ex.: 320kg de 500kg de arroz arrecadados)
- Consultar informações institucionais da ONG
- Criar conta / fazer login

**Restritas a usuários autenticados (área restrita):**
- *Doador:* agendar a coleta de uma doação vinculada a uma campanha; editar ou cancelar seus próprios agendamentos; consultar seu histórico de doações
- *Voluntário / Administrador:* visualizar a lista completa de agendamentos, com filtro por status e por campanha; atualizar o status de um agendamento
- *Voluntário / Administrador:* consultar o inventário de estoque (busca, filtro por categoria, indicador de nível — OK / Baixo / Crítico); registrar movimentações de entrada e saída de itens
- *Administrador:* criar, editar e excluir campanhas de arrecadação; cadastrar os itens necessários de cada campanha

## 🗓️ Entidades ou tabelas do sistema

| Entidade | Principais atributos | Observações |
|---|---|---|
| **Usuario** | id, nome, email, senha (hash), papel (admin / voluntário / doador) | Base da autenticação e do controle de acesso |
| **Campanha** | id, título, descrição, data de início | CRUD completo, gerenciada pelo administrador |
| **Item** | id, nome, unidade, categoria, quantidade meta, quantidade atual, quantidade mínima, `campanha_id` (FK) | Depende de `Campanha`; CRUD completo; possui uma ação de movimentação (entrada/saída) usada por voluntários e administradores |
| **Agendamento** | id, data, horário/turno, local de retirada, status, `campanha_id` (FK), `doador_id` (FK) | Depende de `Campanha` e de `Usuario`; CRUD completo, com regras de acesso por papel |
