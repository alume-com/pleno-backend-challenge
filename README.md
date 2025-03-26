# :test_tube: Teste Prático Backend Pleno — Alume
Este repositório contém o desafio técnico para a vaga de **Desenvolvedor(a) Backend Pleno**, com foco em **Node.js + TypeScript**, utilizando boas práticas de arquitetura e segurança. A proposta é simular funcionalidades que façam parte de um sistema de **gestão de contratos e financiamentos estudantis para estudantes de medicina**.
---
## :brain: Contexto
Nossa startup trabalha conectando **estudantes de medicina** a **financiamentos estudantis personalizados**. Este teste simula parte de um módulo interno que permite que estudantes se cadastrem, consultem seus contratos e simulem financiamentos.
Você deverá desenvolver uma **RESTful API**, com autenticação via **JWT**, onde estudantes podem:
- Se registrar
- Realizar login
- Consultar e editar seus dados
- Criar e consultar seus contratos de financiamento
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
### Contratos de Financiamento
- `id`: primary key
- `id_estudante`: obrigatório (relacionamento com Estudantes)
- `instituicao_ensino`: obrigatório
- `valor_total`: obrigatório (decimal)
- `valor_mensal`: obrigatório (decimal)
- `quantidade_parcelas`: obrigatório
- `status`: obrigatório (`ativo`, `quitado`, `inadimplente`)
- `criado_em`: timestamp
### Simulações de Financiamento
- `id`: primary key
- `id_estudante`: obrigatório
- `valor_total`: obrigatório
- `quantidade_parcelas`: obrigatório
- `juros_ao_mes`: obrigatório
- `valor_simulado_mensal`: calculado
---
## :closed_lock_with_key: Autenticação
JWT com expiração de **5 minutos**.
---
## :satellite_antenna: Rotas Obrigatórias
### Estudantes
- `POST /api/register` — Criação de novo estudante
- `POST /api/login` — Autenticação
- `POST /api/me` — Retorna dados do estudante autenticado (sem senha)
- `PUT /api/me` — Atualiza dados do estudante autenticado
### Contratos de Financiamento (Requer autenticação)
- `POST /api/contracts` — Criação de contrato
- `GET /api/contracts` — Lista todos os contratos do estudante autenticado
- `GET /api/contracts/:id` — Detalhes de um contrato específico
- `PUT /api/contracts/:id` — Atualização de contrato (somente se status ≠ quitado)
- `DELETE /api/contracts/:id` — Exclusão de contrato (somente se status = ativo)
### Simulações de Financiamento (Requer autenticação)
- `POST /api/simulations` — Cria uma nova simulação (retorna valor estimado da parcela com base nos dados informados)
- `GET /api/simulations` — Lista todas as simulações realizadas pelo estudante
---
## :brain: Regras de Negócio
- Um estudante só pode visualizar, editar ou excluir seus próprios contratos/simulações.
- A exclusão de um contrato não deve ser possível caso ele esteja com status `quitado` ou `inadimplente`.
- O campo `valor_simulado_mensal` da simulação deve ser calculado com base na fórmula de juros compostos.
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
