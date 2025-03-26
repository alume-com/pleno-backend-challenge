# :test_tube: Teste Prático Backend Pleno — Alume
Este repositório contém o desafio técnico para a vaga de **Desenvolvedor(a) Backend Pleno**, com foco em **Node.js + TypeScript**, utilizando boas práticas de arquitetura e segurança. A proposta é simular funcionalidades que façam parte de um sistema de **financiamentos estudantis para estudantes de medicina**.
---
## :brain: Contexto
Nossa startup trabalha conectando **estudantes de medicina** a **financiamentos estudantis personalizados**. Este teste simula parte de um módulo interno que permite que estudantes se cadastrem e simulem financiamentos.
Você deverá desenvolver uma **RESTful API**, com autenticação via **JWT**, onde estudantes podem:
- Se registrar
- Realizar login
- Consultar e editar seus dados
- Simular novos financiamentos baseados em parâmetros específicos
---
## :package: Requisitos Técnicos
- **Node.js com TypeScript**
- ORM (Ex: Prisma, TypeORM ou Sequelize)
- Banco de dados relacional (preferencialmente PostgreSQL ou MySQL)
- Autenticação via **JWT** com expiração de 5 minutos
- Arquitetura modular e boas práticas (controllers, services, middlewares, etc.)
- Validação de dados (com libs como `zod`, `joi` ou similares)
- Tratamento de erros
---
## :standing_person: Entidades
### Estudantes
- `id`: primary key
- `nome`: obrigatório
- `sobrenome`: obrigatório
- `email`: obrigatório e único
- `senha`: obrigatória (criptografada)
### Simulações de Financiamento
- `id`: primary key
- `id_estudante`: obrigatório
- `valor_total`: obrigatório
- `quantidade_parcelas`: obrigatório
- `juros_ao_mes`: obrigatório
- `valor_parcela_mensal`: calculado
---
## :closed_lock_with_key: Autenticação
JWT com expiração de **5 minutos**.
---
## Rotas Obrigatórias
### Estudantes
- `POST /api/register` — Criação de novo estudante
- `POST /api/login` — Autenticação
- `POST /api/me` — Retorna dados do estudante autenticado (sem senha)
- `PUT /api/me` — Atualiza dados do estudante autenticado
### Simulações de Financiamento (Requer autenticação)
- `POST /api/simulations` — Cria uma nova simulação (retorna valor estimado da parcela com base nos dados informados)
- `GET /api/simulations` — Lista todas as simulações realizadas pelo estudante
---
## :brain: Regras de Negócio
- Um estudante só pode visualizar, editar ou excluir suas próprias simulações.
- O campo `valor_parcela_mensal` da simulação deve ser calculado com base na fórmula de juros compostos abaixo.
---
## :abacus: Fórmula de cálculo da parcela
Para simular o valor mensal do financiamento, use a fórmula da **parcela fixa (Price)**:
PMT = PV * (i / (1 - (1 + i)^-n))
Onde:
- `PMT` = parcela mensal
- `PV` = valor total do financiamento
- `i` = juros ao mês (ex: 0.02 para 2%)
- `n` = número de parcelas
---
## :mailbox_with_mail: Entrega
- Suba o projeto em um repositório público no seu GitHub
- Envie o link do repositório e instruções de execução no README
- Se desejar, escreva testes automatizados para algumas rotas
- Use `.env.example` para variáveis sensíveis
---
## :white_check_mark: Dicas
- Use `bcrypt` ou `argon2` para criptografar senhas
- Use `jsonwebtoken` para JWT
- Organize o projeto em camadas (controllers, services, etc)
- Utilize boas práticas de REST e clean code
- Se quiser ir além: adicione testes, Swagger, ou documentação via Postman
---
Boa sorte e bom código! :rocket:
