
![Thumb](https://github.com/user-attachments/assets/f6cce7e5-5bae-42be-a5d3-2271992d3b48)

**Link do Figma:**

[https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1](https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1)

**Loom sobre o projeto**

<https://www.loom.com/share/d2d86548e3da469185c8a66efd4218e8?sid=85e02418-34cc-49f9-bf55-7dab3b20b7b1>

### **1. Implementar CRUD de Ferramentas (Tools)**

**Descrição da Tarefa:**

Desenvolver as operações de Create, Read, Update e Delete para a entidade **Ferramentas**, integrando o backend e o frontend. Implementar modelos, controladores, rotas RESTful e interfaces de usuário correspondentes. A funcionalidade deve permitir que os líderes da empresa possam gerenciar as Ferramentas de forma intuitiva.

**Rotas:**

- `POST /api/tools` - Criar uma nova ferramenta.
- `GET /api/tools` - Listar todas as ferramentas.
- `GET /api/tools/:id` - Obter detalhes de uma ferramenta específica.
- `PUT /api/tools/:id` - Atualizar uma ferramenta existente.
- `DELETE /api/tools/:id` - Excluir uma ferramenta.
- `POST /api/packages/:package_id/tools` - Adicionar uma ferramenta a um pacote.
- `DELETE /api/packages/:package_id/tools/:tool_id` - Remover uma ferramenta de um pacote.

**Regras de Negócio:**

- **Validações de Campos Obrigatórios:** `name`, `type`, `implementation_fee_cents`, `monthly_price_cents`, `currency`, `description`.
- **Versionamento:**
  - **Mecanismo de Versionamento:** Ao realizar uma operação de **Update** (`PUT /api/tools/:id`), o sistema **não atualiza** a linha existente. Em vez disso, **cria uma nova linha** no banco de dados.
  - **Manutenção do Original ID:** A nova linha manterá o campo `originalToolId` apontando para o ID da ferramenta original.
  - **Incremento da Versão:** O campo `version` será incrementado automaticamente para refletir a nova versão da ferramenta.
- **Valores Monetários:** Armazenar valores monetários em centavos para evitar problemas de precisão. Validar que os valores sejam números inteiros não negativos.
- **Timestamps:** Preencher automaticamente `created_at` e `updated_at` nas operações correspondentes.
- **Associações:** Permitir associar Ferramentas a Pacotes através das rotas adicionais mencionadas.

**Descrição Adicional sobre Versionamento:**

> **Processo de Atualização com Versionamento:**
>
> 1. **Passo 1:** Quando um líder da empresa solicita a atualização de uma ferramenta existente através da rota `PUT /api/tools/:id`, o sistema primeiro **valida** os dados recebidos.
> 2. **Passo 2:** Em vez de **modificar** a linha atual da ferramenta no banco de dados, o sistema **cria uma nova entrada** com os dados atualizados.
> 3. **Passo 3:** A nova linha terá:
>    - `originalToolId` igual ao ID da ferramenta original.
>    - `version` incrementado em 1 em relação à versão anterior.
> 4. **Benefícios:** Esse mecanismo garante que todas as versões anteriores da ferramenta sejam preservadas para histórico e auditoria, mantendo a integridade dos dados.

**Requisitos do Frontend:**

- **Formulário de Criação/Edição:** Campos para `name`, `type`, `implementation_fee_cents`, `monthly_price_cents`, `currency`, `description`.
- **Listagem de Ferramentas:** Exibir uma tabela com todas as ferramentas, permitindo busca e paginação.
- **Detalhes da Ferramenta:** Visualizar informações completas de uma ferramenta específica.
- **Associação a Pacotes:** Interface para adicionar ou remover Ferramentas de Pacotes.
- **Validações no Frontend:** Garantir que todos os campos obrigatórios sejam preenchidos e que os valores inseridos sejam válidos.
- **Confirmação de Exclusão:** Solicitar confirmação antes de excluir uma ferramenta.

**Testes Unitários:**

- Desenvolver testes unitários para as funcionalidades do backend e do frontend.
- Garantir cobertura dos casos principais, incluindo validações e regras de negócio.

**Documentação:**

- Documentar todas as rotas da API relacionadas a Ferramentas.
- Incluir exemplos de requisições e respostas.
- Atualizar a documentação do sistema para refletir as novas funcionalidades.

**Link do Figma:**

[https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1](https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1)

---

### **2. Implementar CRUD de Entregáveis (Deliverables)**

**Descrição da Tarefa:**

Desenvolver as operações de CRUD para a entidade **Entregáveis**, integrando o backend e o frontend. A funcionalidade deve permitir que os líderes da empresa gerenciem os Entregáveis e os associem a Serviços.

**Rotas:**

- `POST /api/deliverables` - Criar um novo entregável.
- `GET /api/deliverables` - Listar todos os entregáveis.
- `GET /api/deliverables/:id` - Obter detalhes de um entregável específico.
- `PUT /api/deliverables/:id` - Atualizar um entregável existente.
- `DELETE /api/deliverables/:id` - Excluir um entregável.
- `POST /api/services/:service_id/deliverables` - Adicionar um entregável a um serviço.
- `DELETE /api/services/:service_id/deliverables/:deliverable_id` - Remover um entregável de um serviço.

**Regras de Negócio:**

- **Validações de Campos Obrigatórios:** `name`, `type`, `description`.
- **Versionamento:**
  - **Mecanismo de Versionamento:** Ao realizar uma operação de **Update** (`PUT /api/deliverables/:id`), o sistema **cria uma nova linha** no banco de dados.
  - **Manutenção do Original ID:** A nova linha manterá o campo `originalDeliveryId` referenciando o ID do entregável original.
  - **Incremento da Versão:** O campo `version` será incrementado automaticamente.
- **Timestamps:** Gerenciar corretamente `created_at` e `updated_at`.

**Descrição Adicional sobre Versionamento:**

> **Processo de Atualização com Versionamento:**
>
> 1. **Passo 1:** Solicitação de atualização via `PUT /api/deliverables/:id`.
> 2. **Passo 2:** Validação dos dados recebidos.
> 3. **Passo 3:** Criação de uma nova entrada no banco de dados com:
>    - `originalDeliveryId` apontando para o entregável original.
>    - `version` incrementado.
> 4. **Resultado:** Preservação das versões anteriores para histórico e rastreabilidade.

**Requisitos do Frontend:**

- **Formulário de Criação/Edição:** Campos para todos os atributos necessários.
- **Listagem de Entregáveis:** Permitir busca, filtragem e ordenação.
- **Associação a Serviços:** Interface para adicionar ou remover Entregáveis de Serviços.
- **Validações no Frontend:** Assegurar que os dados inseridos pelos usuários são válidos antes de enviar ao backend.

**Testes Unitários:**

- Desenvolver testes unitários para as funcionalidades do backend e do frontend.
- Cobrir cenários de criação, atualização, exclusão e associações.

**Documentação:**

- Documentar as rotas da API para Entregáveis e associações com Serviços.
- Incluir exemplos e detalhes das regras de negócio.

**Link do Figma:**

[https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1](https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1)

---

### **3. Implementar CRUD de Cargos (Employee Roles)**

**Descrição da Tarefa:**

Desenvolver as operações de CRUD para a entidade **Cargos**, integrando o backend e o frontend. Permitir que os líderes gerenciem os Cargos e os associem a Profissionais de Serviço.

**Rotas:**

- `POST /api/employee_roles` - Criar um novo cargo.
- `GET /api/employee_roles` - Listar todos os cargos.
- `GET /api/employee_roles/:id` - Obter detalhes de um cargo específico.
- `PUT /api/employee_roles/:id` - Atualizar um cargo existente.
- `DELETE /api/employee_roles/:id` - Excluir um cargo.
- `POST /api/services/:service_id/employees` - Adicionar um profissional (com cargo) a um serviço.
- `DELETE /api/services/:service_id/employees/:employee_id` - Remover um profissional de um serviço.

**Regras de Negócio:**

- **Campos Obrigatórios:** `name`, `measurement_unit`, `level`.
- **Validação de Nível:** O campo `level` deve aceitar apenas valores pré-definidos (por exemplo, Júnior, Pleno, Sênior).
- **Versionamento:**
  - **Mecanismo de Versionamento:** Atualizações através de `PUT /api/employee_roles/:id` resultam na criação de uma nova linha no banco de dados.
  - **Manutenção do Original ID:** A nova linha mantém `originalRoleId` referenciando o cargo original.
  - **Incremento da Versão:** O campo `version` é incrementado automaticamente.
- **Timestamps:** Manter os campos `created_at` e `updated_at` atualizados.

**Descrição Adicional sobre Versionamento:**

> **Processo de Atualização com Versionamento:**
>
> 1. **Passo 1:** Quando um líder solicita a atualização de um cargo existente através da rota `PUT /api/employee_roles/:id`, o sistema **valida** os dados recebidos.
> 2. **Passo 2:** Em vez de **modificar** a linha atual do cargo no banco de dados, o sistema **cria uma nova entrada** com os dados atualizados.
> 3. **Passo 3:** A nova linha terá:
>    - `originalRoleId` igual ao ID do cargo original.
>    - `version` incrementado em 1 em relação à versão anterior.
> 4. **Benefícios:** Esse mecanismo preserva todas as versões anteriores dos cargos para histórico e auditoria, garantindo a integridade dos dados.

**Requisitos do Frontend:**

- **Formulário de Criação/Edição:** Incluir seleção de unidades de medida e níveis pré-definidos.
- **Listagem de Cargos:** Exibir informações relevantes com opções de busca e filtragem.
- **Associação a Serviços:** Interface para associar Cargos a Serviços através de Profissionais de Serviço.
- **Validações no Frontend:** Garantir a entrada correta dos dados.

**Testes Unitários:**

- Implementar testes para validações de nível, criação e atualização de cargos, e associações com Serviços.

**Documentação:**

- Documentar rotas relacionadas a Cargos e suas associações.
- Incluir detalhes sobre os valores permitidos para `level`.

**Link do Figma:**

[https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1](https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1)

---

### **4. Implementar CRUD de Serviços (Services)**

**Descrição da Tarefa:**

Desenvolver as operações de CRUD para a entidade **Serviços**, integrando o backend e o frontend. Permitir que os líderes gerenciem os Serviços, associando Entregáveis e Profissionais.

**Rotas:**

- `POST /api/services` - Criar um novo serviço.
- `GET /api/services` - Listar todos os serviços.
- `GET /api/services/:id` - Obter detalhes de um serviço específico.
- `PUT /api/services/:id` - Atualizar um serviço existente.
- `DELETE /api/services/:id` - Excluir um serviço.
- `POST /api/services/:service_id/deliverables` - Adicionar entregáveis a um serviço.
- `DELETE /api/services/:service_id/deliverables/:deliverable_id` - Remover um entregável de um serviço.
- `POST /api/services/:service_id/employees` - Adicionar profissionais a um serviço.
- `DELETE /api/services/:service_id/employees/:employee_id` - Remover um profissional de um serviço.

**Regras de Negócio:**

- **Campos Obrigatórios:** `name`, `type`, `description`, `price_cents`, `markup_percentage`, `royalties_charge_method`, `hq_royalties_percentage`, `is_active`.
- **Validação Financeira:** Assegurar que `markup_percentage` e `hq_royalties_percentage` estão dentro de limites aceitáveis (0-100%).
- **Versionamento:**
  - **Mecanismo de Versionamento:** Operações de **Update** (`PUT /api/services/:id`) criam uma nova linha no banco de dados.
  - **Manutenção do Original ID:** A nova linha inclui `originalServiceId` apontando para o serviço original.
  - **Incremento da Versão:** O campo `version` é automaticamente incrementado.
- **Associações:** Gerenciar corretamente as relações com Entregáveis e Profissionais de Serviço.

**Descrição Adicional sobre Versionamento:**

> **Processo de Atualização com Versionamento:**
>
> 1. **Passo 1:** Solicitação de atualização via `PUT /api/services/:id`.
> 2. **Passo 2:** Validação dos dados recebidos, especialmente os campos financeiros.
> 3. **Passo 3:** Criação de uma nova entrada no banco de dados com:
>    - `originalServiceId` referenciando o serviço original.
>    - `version` incrementado.
> 4. **Benefícios:** Mantém um histórico completo das alterações dos serviços, facilitando futuras análises e auditorias, além de garantir que todas as associações com Entregáveis e Profissionais reflitam a versão mais recente.

**Requisitos do Frontend:**

- **Formulário de Criação/Edição:** Incluir campos para informações financeiras e opções para associar Entregáveis e Profissionais.
- **Listagem de Serviços:** Exibir status de ativação e permitir filtragem por tipo ou outros critérios.
- **Associação de Entregáveis e Profissionais:** Interface para gerenciar as associações de forma intuitiva.
- **Validações no Frontend:** Garantir integridade dos dados inseridos.

**Testes Unitários:**

- Desenvolver testes para validações financeiras, criação e atualização de serviços, e associações.

**Documentação:**

- Documentar rotas para Serviços e suas associações com Entregáveis e Profissionais.
- Incluir exemplos e detalhes das regras de negócio.

**Link do Figma:**

[https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1](https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1)

---

### **5. Implementar CRUD de Pacotes (Packages)**

**Descrição da Tarefa:**

Desenvolver as operações de CRUD para a entidade **Pacotes**, integrando o backend e o frontend. Permitir que os líderes possam gerenciar os Pacotes, incluindo Serviços e Ferramentas.

**Rotas:**

- `POST /api/packages` - Criar um novo pacote.
- `GET /api/packages` - Listar todos os pacotes.
- `GET /api/packages/:id` - Obter detalhes de um pacote específico.
- `PUT /api/packages/:id` - Atualizar um pacote existente.
- `DELETE /api/packages/:id` - Excluir um pacote.
- `POST /api/packages/:package_id/services` - Adicionar serviços a um pacote.
- `DELETE /api/packages/:package_id/services/:service_id` - Remover um serviço de um pacote.
- `POST /api/packages/:package_id/tools` - Adicionar ferramentas a um pacote.
- `DELETE /api/packages/:package_id/tools/:tool_id` - Remover uma ferramenta de um pacote.

**Regras de Negócio:**

- **Campos Obrigatórios:** `name`, `description`.
- **Versionamento:**
  - **Mecanismo de Versionamento:** Atualizações através de `PUT /api/packages/:id` resultam na criação de uma nova linha no banco de dados.
  - **Manutenção do Original ID:** A nova linha mantém `originalPackageId` referenciando o pacote original.
  - **Incremento da Versão:** O campo `version` é incrementado automaticamente.
- **Associações:** Gerenciar relações com Serviços e Ferramentas.

**Descrição Adicional sobre Versionamento:**

> **Processo de Atualização com Versionamento:**
>
> 1. **Passo 1:** Solicitação de atualização via `PUT /api/packages/:id`.
> 2. **Passo 2:** Validação dos dados recebidos.
> 3. **Passo 3:** Criação de uma nova entrada no banco de dados com:
>    - `originalPackageId` referenciando o pacote original.
>    - `version` incrementado.
> 4. **Resultado:** Preservação das versões anteriores do pacote para referência futura e garantia de que todas as associações com Serviços e Ferramentas estão alinhadas com a versão mais recente.

**Requisitos do Frontend:**

- **Formulário de Criação/Edição:** Permitir a seleção de Serviços e Ferramentas a serem incluídos no Pacote.
- **Listagem de Pacotes:** Mostrar informações resumidas, incluindo a versão atual.
- **Associação de Itens:** Interface para gerenciar a inclusão e exclusão de Serviços e Ferramentas.
- **Validações no Frontend:** Assegurar que todas as associações são válidas.

**Testes Unitários:**

- Implementar testes para criação, atualização e exclusão de pacotes, bem como para as associações com Serviços e Ferramentas.

**Documentação:**

- Documentar rotas para Pacotes e associações.
- Incluir detalhes sobre o versionamento.

**Link do Figma:**

[https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1](https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1)

---

### **6. Implementar CRUD de Addons**

**Descrição da Tarefa:**

Desenvolver as operações de CRUD para a entidade **Addons**, integrando o backend e o frontend. Permitir que os líderes gerenciem os Addons e os associem aos Pacotes requeridos.

**Rotas:**

- `POST /api/addons` - Criar um novo addon.
- `GET /api/addons` - Listar todos os addons.
- `GET /api/addons/:id` - Obter detalhes de um addon específico.
- `PUT /api/addons/:id` - Atualizar um addon existente.
- `DELETE /api/addons/:id` - Excluir um addon.

**Regras de Negócio:**

- **Campos Obrigatórios:** `name`, `description`, `requiredPackageId`.
- **Validação de Associação:** O `requiredPackageId` deve referenciar um Pacote existente e ativo.
- **Versionamento:**
  - **Mecanismo de Versionamento:** Ao realizar uma operação de **Update** (`PUT /api/addons/:id`), o sistema **cria uma nova linha** no banco de dados.
  - **Manutenção do Original ID:** A nova linha manterá o campo `originalAddonId` apontando para o ID do addon original.
  - **Incremento da Versão:** O campo `version` será incrementado automaticamente.
- **Integridade dos Dados:** Garantir que a exclusão ou inativação de um Pacote não deixe Addons órfãos.

**Descrição Adicional sobre Versionamento:**

> **Processo de Atualização com Versionamento:**
>
> 1. **Passo 1:** Solicitação de atualização via `PUT /api/addons/:id`.
> 2. **Passo 2:** Validação dos dados recebidos, especialmente a referência ao `requiredPackageId`.
> 3. **Passo 3:** Criação de uma nova entrada no banco de dados com:
>    - `originalAddonId` referenciando o addon original.
>    - `version` incrementado.
> 4. **Resultado:** Preservação das versões anteriores dos addons para manter a integridade e rastreabilidade, além de garantir que a associação com Pacotes esteja sempre atualizada.

**Requisitos do Frontend:**

- **Formulário de Criação/Edição:** Incluir seleção do Pacote requerido.
- **Listagem de Addons:** Exibir o Pacote associado e permitir filtragem.
- **Validações no Frontend:** Assegurar que o Addon está corretamente associado a um Pacote válido.

**Testes Unitários:**

- Desenvolver testes para criação, atualização e exclusão de Addons, e validações de associação.

**Documentação:**

- Documentar rotas para Addons.
- Incluir detalhes sobre as regras de associação com Pacotes.

**Link do Figma:**

[https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1](https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1)

---

### **7. Implementar Visualização de Pacotes e Addons para Clientes**

**Descrição da Tarefa:**

Desenvolver funcionalidades que permitam aos clientes visualizar os Pacotes e Addons disponíveis, integrando o backend e o frontend. Preparar a interface para futura integração com o processo de checkout.

**Rotas:**

- `GET /api/client/packages` - Listar todos os Pacotes disponíveis.
- `GET /api/client/packages/:id` - Obter detalhes de um Pacote específico.
- `GET /api/client/addons` - Listar todos os Addons disponíveis.
- `GET /api/client/addons/:id` - Obter detalhes de um Addon específico.

**Regras de Negócio:**

- **Filtragem de Itens Ativos:** Apenas Pacotes e Addons marcados como ativos devem ser retornados.
- **Inclusão de Detalhes:** As respostas devem incluir informações completas dos itens associados (Ferramentas, Serviços, Entregáveis).
- **Segurança:** Garantir que apenas informações necessárias são expostas, protegendo dados sensíveis.

**Requisitos do Frontend:**

- **Catálogo de Pacotes e Addons:** Apresentar uma lista clara e atrativa dos itens disponíveis.
- **Detalhes dos Itens:** Permitir que o cliente visualize informações detalhadas, incluindo todos os componentes.
- **Preparação para Checkout:** Estruturar a interface de forma que seja fácil integrar com o processo de checkout futuramente.

**Testes Unitários:**

- Implementar testes para garantir que apenas itens ativos são exibidos e que os detalhes são corretos.

**Documentação:**

- Documentar as rotas da API para clientes.
- Incluir exemplos de respostas e detalhes sobre a segurança.

**Link do Figma:**

[https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1](https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1)

---

### **8. Implementar CRUD de Leads**

**Descrição da Tarefa:**

Desenvolver as operações de Create, Read, Update e Delete para a entidade **Leads**, integrando o backend e o frontend. Permitir que o sistema gerencie informações de leads necessárias para o processo de checkout.

**Rotas:**

- `POST /api/leads` - Criar um novo lead.
- `GET /api/leads` - Listar todos os leads.
- `GET /api/leads/:id` - Obter detalhes de um lead específico.
- `PUT /api/leads/:id` - Atualizar um lead existente.
- `DELETE /api/leads/:id` - Excluir um lead.

**Regras de Negócio:**

- **Campos Obrigatórios:**
  - `franchiseId`
  - `phone`
  - `email`
  - `tradingName`
  - `document`
- **Validação de Dados:**
  - **Email:** Verificar se o formato do email é válido.
  - **Telefone:** Validar o número de telefone quanto ao formato e comprimento.
  - **Documento:** Validar CPF ou CNPJ conforme o tipo de documento fornecido.
- **Integridade dos Dados:**
  - Garantir que `franchiseId` refere-se a uma franquia existente através da nossa API.
- **Timestamps:**
  - Manter os campos `created_at` e `updated_at` atualizados automaticamente.

**Requisitos do Frontend:**

- **Formulário de Criação/Edição:**
  - Campos para todos os atributos necessários, com validações em tempo real.
- **Listagem de Leads:**
  - Permitir busca, filtragem e ordenação por diferentes critérios (nome, email, data de criação).
- **Detalhes do Lead:**
  - Exibir informações completas de um lead específico.
- **Validações no Frontend:**
  - Assegurar que os dados inseridos pelos usuários são válidos antes de enviar ao backend.
- **Confirmação de Exclusão:**
  - Solicitar confirmação antes de excluir um lead.

**Testes Unitários e Documentação:**

- **Testes Unitários:**
  - Desenvolver testes para criação, leitura, atualização e exclusão de leads.
  - Testar validações de campo e regras de negócio.
- **Documentação:**
  - Documentar as rotas da API para Leads, incluindo parâmetros, corpos de requisição e respostas esperadas.
  - Incluir exemplos de requisições e respostas.

**Link do Figma:**

[https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/\[Profit-pulse\]-Release-2?node-id=0-1\&node-type=canvas\&t=1m1S6uRcs4vmxElh-0](https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1)

---

### **9. Implementar Funcionalidades de Checkout**

**Descrição da Tarefa:**

Desenvolver as funcionalidades necessárias para o processo de **Checkout**, incluindo a criação de checkouts, associação de pacotes e addons ao checkout, e gestão do status do checkout. Integrar o backend e o frontend para proporcionar uma experiência completa ao usuário.

**Rotas:**

- **Checkouts:**
  - `POST /api/checkouts` - Criar um novo checkout.
  - `GET /api/checkouts` - Listar todos os checkouts.
  - `GET /api/checkouts/:id` - Obter detalhes de um checkout específico.
  - `PUT /api/checkouts/:id` - Atualizar um checkout existente.
- **Associação de Pacotes ao Checkout:**
  - `POST /api/checkouts/:checkout_id/packages` - Adicionar pacotes a um checkout.
  - `DELETE /api/checkouts/:checkout_id/packages/:package_id` - Remover um pacote de um checkout.
- **Associação de Addons ao Checkout:**
  - `POST /api/checkouts/:checkout_id/addons` - Adicionar addons a um checkout.
  - `DELETE /api/checkouts/:checkout_id/addons/:addon_id` - Remover um addon de um checkout.

**Regras de Negócio:**

- **Campos Obrigatórios ao Criar um Checkout:**
  - `franchise_id`
  - `lead_id`
  - `payment_method` (e.g., cartão de crédito, boleto)
  - `status` (e.g., iniciado, pendente, concluído)
  - `amount_cents`
  - `total_discount_cents`
  - `total_amount_cents`
  - `installments`
  - `payment_day`
- **Validação de Dados:**
  - Verificar que `lead_id` refere-se a um lead existente.
  - Verificar que `franchise_id` é válido.
  - Validar o método de pagamento (`payment_method`) e número de parcelas (`installments`).
- **Cálculo de Valores:**
  - Atualizar `total_amount_cents` baseado em `amount_cents` e `total_discount_cents`.
  - Aplicar descontos conforme regras pré-definidas.
- **Status do Checkout:**
  - Gerenciar status como 'iniciado', 'pendente', 'concluído', 'cancelado'.
  - Implementar transições de status apenas conforme permitido (por exemplo, não é possível voltar de 'concluído' para 'pendente').
- **Associação de Pacotes e Addons:**
  - Garantir que apenas pacotes e addons disponíveis podem ser adicionados ao checkout.
  - Validar compatibilidade entre pacotes e addons selecionados.
- **Timestamps:**
  - Manter o campo `created_at` atualizado automaticamente.
  - Atualizar `updated_at` sempre que houver uma modificação.

**Requisitos do Frontend:**

- **Processo de Checkout:**
  - **Seleção de Pacotes e Addons:** Interface para que o cliente escolha pacotes e addons disponíveis.
  - **Formulário de Pagamento:** Coletar informações necessárias para o pagamento, respeitando normas de segurança.
  - **Resumo do Pedido:** Exibir um resumo com os itens selecionados, valores individuais, descontos aplicados e valor total.
- **Visualização do Carrinho:**
  - Permitir que o cliente revise e modifique o carrinho antes de finalizar.
  - Atualização dinâmica dos valores ao adicionar ou remover itens.
- **Validações no Frontend:**
  - Garantir que todos os campos obrigatórios são preenchidos.
  - Validar formatos de dados, como números de cartão de crédito, datas e códigos de segurança.
- **Feedback ao Usuário:**
  - Exibir mensagens de sucesso ou erro após cada ação.
  - Fornecer indicações claras em caso de problemas, como itens indisponíveis.

**Testes Unitários e Documentação:**

- **Testes Unitários:**
  - Desenvolver testes para todas as rotas e funcionalidades do checkout.
  - Testar cenários de sucesso e falha, incluindo:
    - Criação de checkouts com dados válidos e inválidos.
    - Adição e remoção de pacotes e addons.
    - Cálculo correto dos valores e descontos.
    - Transições de status permitidas e não permitidas.
  - Cobrir casos de validação de dados e regras de negócio.
- **Documentação:**
  - Documentar todas as rotas da API relacionadas ao Checkout, incluindo parâmetros, corpos de requisição e respostas esperadas.
  - Incluir exemplos detalhados de uso das rotas.

**Link do Figma:**

[https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/\[Profit-pulse\]-Release-2?node-id=0-1\&node-type=canvas\&t=1m1S6uRcs4vmxElh-0](https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1)

---

Entendi. A seguir, apresento **apenas o item 11** sobre a **Renderização e Download de PDF no Final do Checkout**, simplificado conforme solicitado.

---

### **10. Implementar Renderização e Download de PDF no Final do Checkout**

**Descrição da Tarefa:**

Desenvolver a funcionalidade que permite gerar e disponibilizar um **PDF** detalhando as informações do **checkout** para o cliente ao final do processo de compra. Isso inclui a criação de uma rota para download e a integração dessa funcionalidade no frontend, proporcionando uma experiência fluida e intuitiva para o usuário.

**Rotas:**

- `GET /api/checkouts/:id/pdf` - Gerar e obter o PDF detalhado de um checkout específico.

**Regras de Negócio:**

- **Conteúdo do PDF:**

  - Informações do cliente (nome, email, telefone, etc.).
  - Detalhes dos pacotes e addons adquiridos.
  - Valores financeiros detalhados (preço dos pacotes, addons, descontos aplicados, total).
  - Informações de pagamento (método, número de parcelas, data de pagamento).
  - Status do checkout.
  - Timestamps relevantes (`created_at`, `updated_at`).

- **Design e Formatação:**
  - Seguir o layout e design especificado no **Figma** para garantir consistência visual.
  - Incluir o logo da empresa e outros elementos de branding.

**Requisitos do Frontend:**

- **Botão de Download de PDF:**

  - Disponibilizar um botão claramente visível na página de confirmação do checkout.
  - Exibir um ícone ou indicador que represente o download de documentos.

- **Experiência do Usuário:**

  - Fornecer feedback visual durante o processo de geração e download (ex.: loader, mensagens de sucesso ou erro).
  - Garantir que o download seja iniciado de forma suave, sem necessidade de recarregar a página.

- **Responsividade e Acessibilidade:**
  - Assegurar que o botão e os feedbacks sejam adequados para diferentes dispositivos e tamanhos de tela.
  - Garantir que a funcionalidade seja acessível a todos os usuários, incluindo suporte a leitores de tela e navegação por teclado.

**Link do Figma:**

[https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1](https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1)

---

### **11. Implementar Verificação de Atualização de Entidades e Sincronização via Eventos**

**Descrição da Tarefa:**

Adicionar uma funcionalidade que, ao atualizar qualquer uma das entidades principais (**Deliverables**, **EmployeeRoles**, **Tools**, **Services**, **Packages**, **Addons**), dispara eventos que propagam a atualização para todas as entidades pai relacionadas que dependem da entidade atualizada. Isso garante que todas as entidades associadas utilizem as versões mais recentes, mantendo a integridade e a consistência dos dados no sistema.

**Regras de Negócio:**

1. **Detecção de Atualização:**

   - Sempre que uma operação de **Update** (`PUT`) for realizada em qualquer uma das entidades principais (**Deliverables**, **EmployeeRoles**, **Tools**, **Services**, **Packages**, **Addons**), o sistema deve disparar um evento específico para essa entidade.

2. **Versionamento:**

   - Ao atualizar uma entidade, incrementar o campo `version` da entidade atualizada.
   - Manter o campo `originalEntityId` referenciando a entidade original para controle de versionamento.

3. **Propagação de Eventos:**

   - **Evento de Atualização da Entidade Principal:**

     - **Deliverables:** Disparar o evento `DeliverableUpdated`.
     - **EmployeeRoles:** Disparar o evento `EmployeeRoleUpdated`.
     - **Tools:** Disparar o evento `ToolUpdated`.
     - **Services:** Disparar o evento `ServiceUpdated`.
     - **Packages:** Disparar o evento `PackageUpdated`.
     - **Addons:** Disparar o evento `AddonUpdated`.

   - **Evento de Atualização das Entidades Pai:**
     - **Serviços:** Ao receber um evento como `DeliverableUpdated`, atualizar todos os Serviços que utilizam o Deliverable atualizado.
     - **Pacotes:** Ao receber um evento como `ServiceUpdated` ou `ToolUpdated`, atualizar todos os Pacotes que utilizam esses Serviços ou Tools.
     - **Addons:** Ao receber um evento como `PackageUpdated`, atualizar todos os Addons que dependem desses Pacotes.
     - **Cadeia de Eventos:** Cada atualização de entidade disparará eventos subsequentes para garantir que todas as entidades pai relacionadas sejam atualizadas adequadamente.

4. **Integridade Referencial:**
   - Garantir que todas as referências entre entidades estejam atualizadas para apontar para a versão mais recente das entidades associadas.
   - Manter a consistência dos dados através de todas as entidades envolvidas na cadeia de dependências.

**Testes Unitários:**

1. **Testes de Disparo de Eventos:**

   - Verificar se, ao atualizar cada uma das entidades principais, o evento correspondente é disparado corretamente.

2. **Testes de Manejadores de Eventos:**

   - Assegurar que cada handler de evento identifica corretamente as entidades pai dependentes e atualiza suas referências para a versão mais recente.
   - Testar a atualização em cascata, garantindo que a propagação de eventos ocorra conforme esperado.

3. **Testes de Versionamento:**

   - Confirmar que o campo `version` é incrementado corretamente em todas as entidades atualizadas.

4. **Testes de Integridade de Dados:**

   - Garantir que, após a atualização, todas as referências entre entidades estão consistentes e apontam para as versões mais recentes.
   - Validar que nenhuma entidade pai permanece associada a uma versão antiga da entidade atualizada.

5. **Testes de Transações:**
   - Verificar que, em caso de falha durante a atualização em cascata, todas as mudanças são revertidas, mantendo a consistência do banco de dados.

**Documentação:**

- **Descrição da Funcionalidade:**

  - Explicar o mecanismo de detecção de atualizações em entidades principais e a propagação de eventos para sincronizar entidades pai relacionadas.

- **Fluxo de Atualização via Eventos:**

  - Detalhar o fluxo desde a atualização de uma entidade principal até a atualização das entidades pai associadas através de eventos.
  - Incluir diagramas de sequência para ilustrar o processo de disparo e manejo de eventos.

- **Definição de Eventos:**

  - Listar e descrever todos os eventos implementados (`DeliverableUpdated`, `EmployeeRoleUpdated`, etc.), incluindo os dados que cada evento transporta.

- **Implementação dos Manejadores de Eventos:**

  - Descrever como os handlers são registrados e como eles processam os eventos para realizar as atualizações necessárias.

- **Considerações de Versionamento:**

  - Detalhar como o versionamento é gerenciado, incluindo a utilização dos campos `version` e `originalEntityId`.

- **Exemplos de Uso:**

  - Incluir cenários ilustrativos mostrando como a atualização de uma entidade principal impacta as entidades pai relacionadas através da propagação de eventos.

- **Referência Técnica:**.
  - Fornecer trechos de código exemplificando a implementação dos eventos e handlers.

---

### **12. Testes e Garantia de Qualidade**

**Descrição da Tarefa:**

Realizar testes completos em todas as funcionalidades desenvolvidas, tanto no backend quanto no frontend. Garantir que todas as rotas funcionam conforme esperado e que as regras de negócio são respeitadas.

**Atividades:**

- **Testes Unitários:** Escrever testes para as principais funções e métodos, cobrindo casos de sucesso e falha.
- **Testes de Integração:** Validar a interação entre diferentes componentes e serviços.
- **Testes de Interface:** Verificar a usabilidade e a experiência do usuário no frontend.
- **Correção de Bugs:** Resolver quaisquer problemas identificados durante os testes.

**Documentação:**

- Documentar os casos de teste e resultados.
- Atualizar a documentação com quaisquer alterações necessárias identificadas durante os testes.

**Link do Figma:**

Aplicável para referência durante os testes de interface.

[https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1](https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1)

---

### **13. Documentação Geral**

**Descrição da Tarefa:**

Documentar todas as rotas da API, incluindo descrições, parâmetros, respostas e exemplos de uso. Atualizar a documentação do sistema para refletir as novas funcionalidades.

**Atividades:**

- **API Documentation:** Utilizar ferramentas apropriadas (como Swagger) para gerar documentação acessível.
- **Guias de Usuário:** Criar manuais ou tutoriais para orientar os líderes da empresa no uso do sistema.
- **Comentários no Código:** Assegurar que o código está bem comentado para facilitar futuras manutenções.

**Link do Figma:**

Utilizar como referência visual ao criar guias de usuário.

[https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1](https://www.figma.com/design/bQZGsFq50Oug3CsFR7iBzd/%5BProfit-pulse%5D-Release-2?node-id=0-1&t=fiRCOCJG3l0QNcag-1)

---

**Observações Gerais:**

- **Comunicação:** Mantenha a equipe informada sobre o progresso e quaisquer impedimentos encontrados.
- **Padrões de Codificação:** Siga os padrões estabelecidos pela empresa para garantir a consistência do código.
- **Prazo:** Organize as tarefas de acordo com as prioridades e prazos estabelecidos.
- **Integração Contínua:** Utilize ferramentas de CI/CD para automatizar testes e deploys.
- **Segurança:** Assegure-se de que todas as práticas de segurança estão sendo seguidas, especialmente na exposição de dados aos clientes.

Se tiver alguma dúvida ou precisar de esclarecimentos adicionais sobre qualquer tarefa, não hesite em me procurar.

---

** Padrão de Projetos V4 Company (Javascript / NestJS)**

```
├── prisma
└── src
    ├── config          # Diretório para arquivos de configuração da aplicação.
    ├── leads           # Módulo responsável pelo gerenciamento de leads.
    │   ├── app
    │   │   ├── dto         # Objetos de Transferência de Dados utilizados para comunicar entre camadas.
    │   │   ├── mappers     # Funções para mapear entidades de domínio para DTOs e vice-versa.
    │   │   └── use-cases   # Implementação dos casos de uso ou serviços da aplicação.
    │   ├── domain
    │   │   ├── events      # Eventos de domínio relacionados aos leads.
    │   │   ├── repositories # Interfaces dos repositórios que definem os métodos de acesso aos dados.
    │   │   └── schemas     # Esquemas de validação e definição das entidades de domínio.
    │   └── infra
    │       ├── controllers # Controladores que expõem as rotas e endpoints da API.
    │       └── database
    │           ├── fake    # Implementações fake ou mock para testes.
    │           └── kysely  # Implementações utilizando o Kysely para consultas tipadas.
    └── shared              # Código e recursos compartilhados entre os módulos da aplicação.
        ├── domain
        │   └── value-objects # Objetos de valor genéricos utilizados em múltiplos domínios.
        ├── exceptions        # Exceções customizadas para tratamento de erros.
        └── infra
            ├── database      # Configurações e conexões de banco de dados compartilhadas.
            ├── events
            │   └── sqs       # Integração com o Amazon SQS para gerenciamento de filas de mensagens.
            └── tracing       # Ferramentas e configurações para rastreamento e monitoramento da aplicação.
```

Essa estrutura modularizada permite uma clara separação de responsabilidades, facilitando a manutenção e escalabilidade do sistema. Cada módulo contém suas próprias camadas de aplicação, domínio e infraestrutura, criada com base no livro **Domain-Driven Design**.

**MER**

<img src="https://www.mermaidchart.com/raw/d70b94f1-5e68-42d7-8fe5-179e6e57352a?theme=light&version=v0.1&format=svg">
