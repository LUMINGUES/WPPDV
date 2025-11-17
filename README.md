🛍️ WPPDV - Sistema de Ponto de Venda (PDV) para WordPress
WPPDV é um sistema robusto de Ponto de Venda (PDV) integrado ao WordPress e opcionalmente ao WooCommerce, oferecendo módulos essenciais para a gestão de varejo e agora com infraestrutura de Pré-Faturamento Fiscal (NF-e).

Descrição
O WPPDV transforma seu painel de administração em uma completa ferramenta de frente de caixa. Ele gerencia produtos, estoque, vendas e clientes, com foco na agilidade do atendimento no balcão. A integração opcional com o WooCommerce permite o gerenciamento unificado de produtos e inventário, enquanto a nova funcionalidade fiscal prepara automaticamente os dados para emissão de Nota Fiscal Eletrônica (NF-e).

Características Principais ✨
Frente de Caixa (PDV): Interface otimizada para agilidade com leitura de código de barras/SKU e cálculo automático de troco e descontos.

Gestão de Estoque: Módulos de cadastro e entrada de estoque com suporte a produtos simples e variáveis.

Integração WooCommerce: Utiliza os produtos e estoque do WooCommerce se estiver ativo, mantendo a sincronia.

Módulo Fiscal (NF-e): Cria um registro de pré-faturamento (mpdm_fiscal) com os dados fiscais (NCM, CEST, CFOP) para integração posterior com serviços de emissão (ex: NFE.io).

Gerenciamento de Clientes: Integração com o "CRM Central de Clientes" (se ativo) para buscar dados e aplicar descontos.

Relatórios & Análises: Relatórios visuais de vendas por período, produtos mais vendidos, estoque baixo e produtos a vencer.

Configurações: Personalização de dados da empresa (logo, endereço) e chave Pix para recibos.

Instalação
1. Requisitos
WordPress 5.0 ou superior.

PHP 7.4 ou superior.

A extensão ZipArchive do PHP é necessária para a função de exportação de relatórios em massa.

2. Ativação
Faça o upload da pasta wppdv para o diretório /wp-content/plugins/.

Ative o plugin através do menu 'Plugins' no WordPress.

Após a ativação, as tabelas de banco de dados customizadas (mpdm_products, mpdm_sales, mpdm_customer_sales, mpdm_fiscal) serão criadas automaticamente.

Utilização
1. Configurações Iniciais ⚙️
Acesse Meu PDV > Configurações.

Preencha o Nome da Empresa, Endereço, Telefone e carregue o Logo.

Configure a Chave Pix para a frente de caixa.

Defina a regra para avisos de Produtos perto de vencer.

2. Cadastro de Produtos
Acesse Meu PDV > Cadastro de Produtos.

Com WooCommerce Ativo: O plugin gerencia produtos através do CPT product do WC.

Novos campos fiscais (NCM, CFOP, CEST) são adicionados na nova aba Dados Fiscais (PDV) na edição de produtos do WooCommerce.

O estoque é gerenciado pelo sistema de inventário do WooCommerce.

Com WooCommerce Inativo: Os produtos são gerenciados na tabela customizada mpdm_products.

3. Frente de Caixa (PDV)
Acesse Meu PDV (Frente de Caixa).

Use o campo de identificação para ler o código de barras ou digitar o SKU do produto.

Opcionalmente, insira o CPF do cliente para aplicar descontos baseados no CRM.

Clique em Finalizar Venda e escolha a forma de pagamento (Dinheiro ou Pix).

O recibo da venda pode ser impresso para o cliente.

4. Gestão Fiscal (NF-e)
Acesse Meu PDV > Fiscal (NF-e).

Todas as vendas finalizadas são registradas na tabela mpdm_fiscal com status pendente.

A coluna Itens Fiscais contém um JSON estruturado com NCM, CFOP e CEST do item, pronto para ser consumido por um sistema externo de Nota Fiscal (ex: NFE.io).

Estrutura do Banco de Dados 💾
O plugin cria as seguintes tabelas (se o WooCommerce não estiver ativo para o caso da tabela de produtos):

Tabela	Descrição	Integração
wp_mpdm_products	Cadastro e estoque (fallback se WC inativo).	
wp_mpdm_sales	Histórico completo de transações do PDV.	Chave wc_order_id para pedidos WC.
wp_mpdm_fiscal	NOVO: Pré-faturamento de Notas Fiscais (NF-e).	
wp_mpdm_customer_sales	Histórico de vendas por cliente.	
wp_wpcrm_customers	Tabela Centralizada para dados do cliente (Usada por WPDDV_CRM_TABLE).	

Ganchos (Hooks) de Ação e Filtro
Desenvolvedores podem estender o plugin usando os seguintes ganchos:

Filtros
Gancho	Descrição
woocommerce_product_data_tabs	Adiciona a aba Dados Fiscais (PDV) no editor do produto WC.
mpdm_export_sales_csv_content	Filtra o conteúdo CSV da exportação de vendas.


Ações
Gancho	Descrição
admin_enqueue_scripts	Carrega estilos e scripts (incluindo JsBarcode e Chart.js).
wp_ajax_mpdm_finalize_sale	Dispara a lógica de registro de venda, baixa de estoque e pré-faturamento fiscal.
woocommerce_process_product_meta_simple	Salva os campos fiscais em produtos simples no WC.
woocommerce_process_product_meta_variable	Salva os campos fiscais em produtos variáveis (parent) no WC.


Licença
Este plugin é licenciado sob a GPL-2.0+.
