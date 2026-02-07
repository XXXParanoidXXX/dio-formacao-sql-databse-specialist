# dio-formacao-sql-databse-specialist

Banco de Dados E-commerce

Este repositório contém a modelagem e a estrutura lógica de um banco de dados relacional para um sistema de e-commerce, conforme o Diagrama Entidade-Relacionamento (DER) anexo.

O modelo foi concebido para suportar múltiplos clientes, plataformas, parceiros comerciais, pedidos, produtos, estoque e diferentes formas de pagamento, utilizando princípios clássicos de modelagem conceitual e lógica.

⸻

📌 Visão Geral da Modelagem

O banco de dados foi estruturado com base nos seguintes pilares:
	•	Separação clara entre clientes, parceiros e plataformas
	•	Uso de especialização/generalização (herança) para:
	•	Cliente → Pessoa Física / Pessoa Jurídica
	•	Pagamento → Cartão / PIX / Boleto
	•	Parceiro → Fornecedor / Vendedor
	•	Relacionamentos 1:N e N:N resolvidos por tabelas associativas
	•	Persistência de dados de pagamento sem armazenar informações sensíveis

⸻

👤 Clientes

Entidade Cliente

Armazena os dados básicos de endereço e identificação do cliente.

Relacionamentos:
	•	Um cliente pode estar vinculado a uma ou mais plataformas
	•	Um cliente pode realizar vários pedidos
	•	Um cliente possui uma especialização obrigatória: Pessoa Física ou Pessoa Jurídica

Especialização de Cliente
	•	Pessoa_Fisica
	•	Nome
	•	Sobrenome
	•	CPF
	•	Pessoa_Juridica
	•	Razão Social
	•	CNPJ

A especialização é total e disjunta: todo cliente é exatamente PF ou PJ.

⸻

🛒 Pedidos

Entidade Pedido

Representa uma compra realizada por um cliente.

Principais características:
	•	Cada pedido pertence a um único cliente
	•	Um cliente pode ter vários pedidos
	•	O pedido armazena dados de endereço de entrega (snapshot no momento da compra)
	•	Controle de status, cancelamento e rastreio

⸻

📦 Produtos e Estoque

Entidade Produto

Representa os itens comercializados na plataforma.

Relacionamentos:
	•	Um produto pertence a uma plataforma
	•	Um produto é fornecido por um fornecedor
	•	Um produto pode estar associado a vários vendedores

Estoque
	•	Estoque: entidade base de controle
	•	Produto_has_Estoque: tabela associativa que controla a quantidade disponível por produto

⸻

🤝 Parceiros

Entidade Parceiro

Entidade genérica que representa participantes comerciais do ecossistema.

Especializações:
	•	Fornecedor
	•	Responsável pelo fornecimento dos produtos
	•	Vendedor
	•	Responsável pela comercialização dos produtos

A especialização é disjunta.

⸻

💳 Pagamentos

Entidade Pagamento

Representa uma transação financeira associada a um cliente.

Características:
	•	Um pagamento pertence a uma Pessoa Física ou Jurídica
	•	Armazena informações comuns: forma, status e data/hora

Especialização de Pagamento

A entidade Pagamento é especializada em:
	•	Cartao
	•	Tipo
	•	Bandeira
	•	Últimos 4 dígitos
	•	Parcelas
	•	PIX
	•	Chave PIX
	•	Status do PIX
	•	Boleto
	•	Código de barras
	•	Data de vencimento

Essa especialização é:
	•	Total (todo pagamento é de um tipo)
	•	Disjunta (um pagamento não pode ser de mais de um tipo)

Cada subclasse possui relacionamento 1:1 com Pagamento, utilizando a chave primária como chave estrangeira.

⸻

🔗 Plataformas

Entidade Plataforma

Representa os marketplaces ou canais onde os produtos são ofertados.

Relacionamentos:
	•	Plataforma ↔ Cliente: N:N, resolvido por Plataforma_has_Cliente
	•	Plataforma ↔ Produto: 1:N

⸻

🧩 Tabelas Associativas

O modelo utiliza tabelas associativas para resolver relacionamentos muitos-para-muitos:
	•	Plataforma_has_Cliente
	•	Produto_has_Estoque
	•	Produto_has_Vendedor

Essas tabelas garantem integridade referencial e flexibilidade na modelagem.

⸻

🔐 Boas Práticas Adotadas
	•	Não persistência de dados sensíveis de pagamento
	•	Uso de chaves substitutas (IDs)
	•	Integridade referencial via chaves estrangeiras
	•	Especializações bem definidas e normalizadas

⸻

📄 Observação Final

Este modelo é adequado tanto para fins acadêmicos quanto como base para projetos reais, podendo ser estendido para incluir:
	•	Histórico de status de pedidos
	•	Múltiplos pagamentos por pedido
	•	Logs de transações
	•	Integração com gateways de pagamento

⸻

📌 DER: consulte a imagem do diagrama para visualização completa das entidades e relacionamentos.
