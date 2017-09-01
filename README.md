[checkmark]: https://raw.githubusercontent.com/mozgbrasil/mozgbrasil.github.io/master/assets/images/logos/logo_32_32.png "MOZG"
![valid XHTML][checkmark]

[url-method]: http://www.redecard.com.br/
[requerimentos]: http://mozgbrasil.github.io/requerimentos/
[contact-redecard]: http://www.redecard.com.br/redecard/ecp/comunidade.do?app=portal&pg=20004&view=faleconosco
[tickets]: https://cerebrum.freshdesk.com/support/tickets/new
[preco]: http://www.cerebrum.com.br/preco/
[getcomposer]: https://getcomposer.org/
[uninstall-mods]: https://getcomposer.org/doc/03-cli.md#remove
[artigo-composer]: http://mozg.com.br/ubuntu/composer
[ioncube-loader]: http://www.ioncube.com/loaders.php
[acordo]: http://mozg.com.br/acordo-licenca-usuario-final/

# Mozg\Redecard

## Sinopse

Integração a [Redecard][url-method]

## Demonstração

<a href="http://mozg.com.br/assets/images/docs/2017-02-14-magento-redecard.pdf" target="_blank"><img src="http://mozg.com.br/assets/images/docs/2017-02-14-magento-redecard.gif" /></a>

## Motivação

Atender o mercado de módulos para Magento oferecendo melhorias e um excelente suporte

## Suporte / Dúvidas

Para obter o devido suporte [Clique aqui][tickets], relatando o motivo da ocorrência o mais detalhado possível e anexe o print da tela para nosso entendimento

## Preço

[Clique aqui][preco]

## Quais os recursos do módulo

- [✓] Transação
- [✓] Consulta
- [✓] Captura

## Característica técnica

No checkout é feito o processo de autorização

No retorno de "Transação autorizada" é feito redirecionamento para a página de sucesso

Na página de sucesso é enviado infomações para o recurso de notificação da transação

Via CRON deve ser processado a notificação da transação, caso o pagamento seja confirmado, deve ser alterado o status do pedido para "Processando", liberando as ações para processar a fatura e o envio

Antes do envio da mercadoria, sempre confira as informações do pedido, se o status da transação está sendo exibido que o pagamento foi confirmado, inclusive junto a operadora financeira se a transação foi capturada, caso algo esteja inconsistente será necessário cancelar o pedido até a correção da ocorrência

<!--

## Mozg OneClick

No módulo as Referências Recorrentes são salvas nos <a href="http://docs.magento.com/m1/ce/user_guide/payment/paypal-billing-agreements.html" target="_blank">Contratos de Faturamento</a> do Magento.

Todos os novos cartões salvos serão automaticamente salvos em Contratos de Faturamento do Magento.

-->

## Setup Cron

Para o uso do método é necessário ativar a <a href="https://pt.wikipedia.org/wiki/Crontab">CRON</a> para o <a href="https://magento.com/">Magento</a>

<a href="https://mozg.com.br/dicas/dicas-magento1#como-ativar-a-cron-no-magento">Clique aqui</a> para visualizar o documento da MOZG

Certifique-se de que ação esteja sendo executado a cada minuto

Esse módulo usa o cronjob para processar as notificações

O módulo executa as notificações que foram recebidas há pelo menos 5 minutos. 

## Instalação - Atualização - Desinstalação - Desativação

--

Este módulo destina-se a ser instalado usando o [Composer][getcomposer]

Execute o seguinte comando no terminal, para visualizar a existencia do Composer e sua versão

	composer --version

Caso não tenha o Composer em seu ambiente, sugiro ler o seguinte artigo [Clique aqui][artigo-composer]

--

É necessário que o servidor tenha o suporte a extensão [ionCube PHP Loader][ioncube-loader]

Para visualizar se essa extensão está ativa em seu servidor

Certique se da presença do arquivo phpinfo.php na raiz do seu projeto

	<?php phpinfo(); ?>

Caso não exista o arquivo phpinfo.php na raiz do projeto Magento, crie o mesmo adicionado o conteúdo acima

Acesse o arquivo pelo browser

Em seguida pesquise pelo termo "ionCube PHP Loader"

Caso o seu servidor não tenha o suporte a extensão, [Clique aqui][ioncube-loader]

Em "Loader Downloads API", efetue download do pacote compatível com o seu servidor

Descompacte o pacote e faça upload do arquivo "loader-wizard.php" para seu servidor, onde será demonstrado o passo a passo para a ativação da extensão

[Clique aqui](https://youtu.be/GZ2J6MLkko4) para ver os processos executados

--

Para utilizar o(s) módulo(s) da MOZG é necessário aceitar o [Acordo de licença do usuário final][acordo]

--

Sugiro manter um ambiente de testes para efeito de testes e somente após os devidos testes aplicar os devidos procedimento no ambiente de produção

--

Sugiro efetuar backup da plataforma Magento e do banco de dados

--

Antes de efetuar qualquer atualização no Magento sempre mantenha o Compiler e o Cache desativado

--

Certique se da presença do arquivo composer.json na raiz do seu projeto Magento e que o mesmo tenha os parâmetros semelhantes ao modelo JSON abaixo

	{
	  "minimum-stability": "dev",
	  "prefer-stable": true,
	  "license": [
	    "proprietary"
	  ],
	  "repositories": [
	    {
	      "type": "composer",
	      "url": "https?://packages.firegento.com"
	    }
	  ],
	  "extra": {
	    "magento-root-dir": "./",
	    "magento-deploystrategy": "copy",
	    "magento-force": true
	  }
	}

Caso não exista o arquivo composer.json na raiz do projeto Magento, crie o mesmo adicionado o conteúdo acima

### Para instalar o módulo execute o comando a seguir no terminal do seu servidor no diretório do seu projeto

	composer require mozgbrasil/magento-redecard-php56:dev-master

Você pode verificar se o módulo está instalado, indo ao backend em:

	STORES -> Configuration -> ADVANCED/Advanced -> Disable Modules Output

--

### Para atualizar o módulo execute o comando a seguir no terminal do seu servidor no diretório do seu projeto

Antes de efetuar qualquer processo que envolva atualização no Magento é recomendado manter o Compiler e Cache desativado

	composer clear-cache && composer update

Na ocorrência de erro, renomeie a pasta /vendor/mozgbrasil e execute novamente

Para checar a data do módulo execute o seguinte comando

	grep -ri --include=*.json 'time": "' ./vendor/mozgbrasil

--

### Para [desinstalar][uninstall-mods] o módulo execute o comando a seguir no terminal do seu servidor no diretório do seu projeto

	composer remove mozgbrasil/magento-redecard-php56 && composer clear-cache && composer update

--

### Para desativar o módulo

1. Antes de efetuar qualquer processo que envolva atualização sobre o Magento é necessário manter o Compiler e Cache desativado

2. Caso queira desativar os módulos da MOZG renomeie a seguinte pasta app/code/local/Mozg

A desativação do módulo pode ser usado para detectar se determinada ocorrência tem relação com o módulo

## Como configurar o método de pagamento

Para configurar o método de pagamento, acesse no backend em:

	STORES -> Configuration -> Sales/Payment Methods -> Redecard (powered by MOZG)

Você terá os campos a seguir

### Redecard - Configurações Padrão

#### Configurações necessárias

##### • **Modo Teste ou Produção**

Deve ser informado o devido ambiente

##### • **Código de filiação Komerci**

Informe o seu código de filiação

##### • **Usuário Komerci**

Informe o usuário de acesso a Redecard

##### • **Senha Komerci**

Informe a senha de acesso a Redecard

Os dados de usuário e senha é usado para o tipo de captura manual

#### Avançado: Processamento de Pedidos Magento

##### • **Status do pedido: ordem de criação**

Status dos pedidos recém-criados, antes da confirmação de resultado de pagamento via notificações de servidor da operadora

##### • **Status do pedido: autorização de pagamento**

Status dos pedidos após autorização confirmada por uma notificação de AUTORIZAÇÃO da operadora

##### • **Status do pedido: pagamento confirmado**

Status dos pedidos após captura confirmada por uma notificação de AUTORIZAÇÃO da operadora

##### • **Status do pedido: cancelamento de pedido**

Status dos pedidos após cancelamento confirmada por uma notificação de CANCELAMENTO da operadora

Se as encomendas já estiverem faturadas, não poderão ser canceladas

##### • **Status do pedido: captura de pagamento (produtos virtuais)**

Selecione somente o status atribuído ao estado concluído, deixe vazio para usar o mesmo que os produtos normais

##### • **Status do pedido: Reembolsado**

Status dos pedidos após reembolso confirmada por uma notificação de REEMBOLSO da operadora

##### • **Status do pedido: Reembolsado Parcial**

Status dos pedidos após reembolso (parcial) confirmada por uma notificação de REEMBOLSO_PARCIAL da operadora. Recomendamos que não defina este status e deixe Magento decidir o status.

##### • **Status do pedido: pedidos pendentes**

Status dos pedidos após notificação de PENDENCIA da operadora

##### • **Tipo de Captura**

Imediato é o padrão

Defina como manual se você quiser executar a captura de fundos manualmente mais tarde

##### • **Criar uma fatura pendente (apenas para captura manual)**

Isso criará uma fatura pendente se a notificação de AUTORIZAÇÃO for recebida.

 Nota: isto fará com que Magento empurre todas as encomendas para o estado: 'Processamento' uma vez que a factura é criada, ignorando todas as outras definições.

##### • **Status do pedido: Capturar no embarque**

Se você habilitar esta função será feito uma solicitação de captura para a operadora se você fizer o envio

##### • **Ativar Descancelar pedido**

Se uma pedido é cancelada por algum motivo, mas recebeu uma notificação de que o pagamento é autorizado, isso cancelará automaticamente o pedido

##### • **Cancelamento\Reembolso automático quando o pedido é cancelado**

Ativar / Desativar reembolso automático ao cancelar um pedido

##### • **E-mail da fatura**

Ativar / desativar atualizações de e-mails

##### • **Enviar e-mail de notificaçao do status do pedido**

Ativar / desativar e-mails de atualização para todas as alterações no status do pedido para o cliente

##### • **Ativar log de depuração**

Deve ser armazenado os processos do módulo em var/log/

O arquivo 

DATE_mozg.log

se trata de log do módulo sendo um log mais detalhado contendo todos os processos inclusive das execuções realizadas pelas bibliotecas externas do módulo

O arquivo

payment_METHOD.log

#### Avançado: Redecard Notificações

##### • **Ignorar notificação de reembolso**

Se o reembolso for feito na operadora, e a mesma enviar uma notificação de reembolso para o Magento, deve ser criado automaticamente uma nota de crédito. Se você definir essa configuração como 'Sim', isso não acontecerá porque ele não processará nenhuma das notificações de REEMBOLSO recebidas.

<!--
#### Avançado: Contratos de faturamento

##### • **Tipo de Contrato**

Quando ativado, os usuários podem salvar seus cartões de crédito e suas autorizações 

ONECLICK exigirá a entrada do CVC para pagamentos subsequentes, enquanto RECURRING não.
-->

#### Avançao: Experiência de Checkout

##### • **Redirecionar o destino após o cancelamento**

Determina como os compradores são redirecionados após cancelar um pagamento.

##### • **Método de pagamento método de renderização**

Determina se os métodos de pagamento serão exibidos com seu logotipo ou apenas o nome.

##### • **Idioma local (opcional)**

Isso substituirá o local do cliente padrão do armazenamento do Magento. 

Deixe vazio para deixar Magento decidir (Ex: nl_NL)

##### • **Código do país ISO (opcional)**

Isso irá substituir o país do endereço de faturamento do comprador ao determinar quais métodos de pagamento serão exibidos.

<!--
#### Avançado: Revisão manual

##### • **Status da revisão manual**

Esse status será acionado quando a operadora notificar o módulo Magento de que o pagamento foi incluído na revisão manual. Se você não tiver essa configuração ou não quiser um status separado, mantenha-o no padrão (por exemplo, '- Por Favor Selecione -').

#### • **Revisão Manual Status Aceito**

Apenas relevante se você não tiver uma ação definida quando você aceitar uma revisão manual. Este status será acionado quando uma notificação "MANUAL_REVIEW_ACCEPT" for recebida da operadora. Se você já pediu a operadora para definir uma ação para isso (por exemplo, captura) ou não quiser um status separado para isso, mantenha-o no padrão (por exemplo, '- Por Favor Selecione -')

#### Avançado: Dividir Pagamentos

##### • **Estratégia de reembolso**

É possível fazer pagamentos divididos com GiftCards, por favor configure aqui qual estratégia de reembolso você deseja usar
-->

### Cartão de Crédito Redecard Komerci Webservice

#### • **Ativar**

Para "ativar" ou "desativar" o uso do método

#### • **Ordem de exibição**

É a ordem apresentada em métodos de entrega no passo de fechamento de pedido

#### • **Título**

Nome do método que deve ser exibido

#### • **Pagamentos aplicáveis aos países**

Você pode definir se o método deve funcionar para "Todos os Países aceito" ou "Especificar Países "

#### • **Pagamentos específicos aos países**

Você deve selecionar os países que o método deve ser funcional

#### • **Tipos de Cartão de Crédito**

Selecione as bandeiras liberadas pela operadora

#### • **Visível em**

Determine a visibilidade desse método de pagamento no frontend e/ou backend do Magento

#### • **Autenticar**

Define se o comprador será direcionado ao Banco emissor para autenticação do cartão

Para pedidos feito no backend não ative essa opção, pois não deve funcionar o redirecionamento para a URL de autenticação

#### • **Ativar Parcelamentos**

Define o uso de parcelas

#### • **Parcelas padrão**

Para a coluna "Moeda" informe a sigla da moeda por exemplo BRL

Para a coluna "Montante (incl.)" informe o valor mínimo para a exibição da parcela

Para a coluna "Número máximo de parcelas" informe o número de parcelas que será exibida até o valor previamente informando para a exibição da parcela

Para a coluna "Taxa de juro (%)" informe a taxa de juro usada

-

A regra para a exibição da parcela é definida com base na faixas de preços

O módulo já vem pré-configurado da seguinte forma

Até R$ 100,00 em 1 parcela

Até R$ 200,00 em 2 parcelas

Até R$ 600,00 em 3 parcelas

Até R$ 800,00 em 4 parcelas

Até R$ 10.000,00 em 5 parcelas

Até R$ 100.000,00 em 6 parcelas

Altere conforme sua necessidade

#### • **Desativar em total geral zero**

Desative esta forma de pagamento no checkout quando o total geral da cotação for 0.

<!--### Cartão de Débito Redecard

#### • **Ativar**

Para "ativar" ou "desativar" o uso do método

#### • **Ordem de exibição**

É a ordem apresentada em métodos de entrega no passo de fechamento de pedido

#### • **Título**

Nome do método que deve ser exibido

#### • **Pagamentos aplicáveis aos países**

Você pode definir se o método deve funcionar para "Todos os Países aceito" ou "Especificar Países "

#### • **Pagamentos específicos aos países**

Você deve selecionar os países que o método deve ser funcional

#### • **Tipos de Cartão de Débito**

Selecione as bandeiras liberadas pela operadora

#### • **Visível em**

Determine a visibilidade desse método de pagamento no frontend e/ou backend do Magento

#### • **Desativar em total geral zero**

Desative esta forma de pagamento no checkout quando o total geral da cotação for 0.

### Boleto Redecard

#### • **Ativar**

Para "ativar" ou "desativar" o uso do método

#### • **Ordem de exibição**

É a ordem apresentada em métodos de entrega no passo de fechamento de pedido

#### • **Título**

Nome do método que deve ser exibido

#### • **Pagamentos aplicáveis aos países**

Você pode definir se o método deve funcionar para "Todos os Países aceito" ou "Especificar Países "

#### • **Pagamentos específicos aos países**

Você deve selecionar os países que o método deve ser funcional

#### • **Tipos de Boleto**

Selecione as bandeiras liberadas pela operadora

#### • **Status do pedido não pago**

Com Boleto é possível pagar menos do que o valor total. Selecione aqui o status, se este for o caso. Se você deixar isso em branco, ele tomará o status de pedido de pagamento autorizado como status padrão

#### • **Status do pedido pago em excesso**

Com Boleto é possível pagar mais do que o valor total. Selecione aqui o status, se este for o caso. Se você deixar isso em branco, ele tomará o status de pedido de pagamento autorizado como status padrão

#### • **Visível em**

Determine a visibilidade desse método de pagamento no frontend e/ou backend do Magento

### Transferência Eletrônica Redecard

#### • **Ativar**

Para "ativar" ou "desativar" o uso do método

#### • **Ordem de exibição**

É a ordem apresentada em métodos de entrega no passo de fechamento de pedido

#### • **Título**

Nome do método que deve ser exibido

#### • **Pagamentos aplicáveis aos países**

Você pode definir se o método deve funcionar para "Todos os Países aceito" ou "Especificar Países "

#### • **Pagamentos específicos aos países**

Você deve selecionar os países que o método deve ser funcional

#### • **Tipos de Transferência Eletrônica**

Selecione as bandeiras liberadas pela operadora

#### • **Status do pedido não pago**

Com Boleto é possível pagar menos do que o valor total. Selecione aqui o status, se este for o caso. Se você deixar isso em branco, ele tomará o status de pedido de pagamento autorizado como status padrão

#### • **Status do pedido pago em excesso**

Com Boleto é possível pagar mais do que o valor total. Selecione aqui o status, se este for o caso. Se você deixar isso em branco, ele tomará o status de pedido de pagamento autorizado como status padrão

#### • **Visível em**

Determine a visibilidade desse método de pagamento no frontend e/ou backend do Magento-->

## Perguntas mais frequentes "FAQ"

### Sobre a bandeira Hiper

Como não há biblioteca que faz a leitura desse tipo de cartão, está sendo selecionado essa bandeira caso seja retornado pela biblioteca outro tipo de cartão, foi incluido um validador baseado na bandeira hipercard

Caso essa bandeira venha a apresentar problema talvez seja necessário retirar a automação de seleção de bandeira

### Sobre Ativar Parcela do Produto na Vitrine

Na necessidade de exibição de parcela na página de produto, talvez o seguinte módulo deva atender sua necessidade

https://www.magentocommerce.com/magento-connect/preco-parcelado-1.html

Que pode ser instalado via composer

Para instalar o módulo via composer execute o seguinte comando na raiz do projeto

	composer require connect20/franciscoprado_precoparcelado

## AFILIAÇÃO E-COMMERCE - REDECARD

http://www.komerciredecard.com.br

## Configurando o produto

No Backend do Magento, acesse o menu: Sistema -> Configuração -> Cerebrum -> Métodos de pagamento -> Redecard -> Preencha os campos solicitados

## Perguntas mais frequentes "FAQ"

### Dependências

Para se afiliar à Redecard é necessário que o seu site tenha a página segura(SSL128=https).

Por padrão a Redecard libera o Komerci integrado, então para migrar a afiliação para Redecard Webservice basta cadastrar os IPs do Gateway de pagamentos pelo Portal da Redecard ou enviar um e-mail para: pool.credenciamento@redecard.com.br solicitando o cadastramento dos Ips do seu servidor.

### Oque fazer após a instalação do módulo ?

Na configuração do método, selecione o ambiente de teste e informe os seguintes dados

Código de filiação Komerci 		00000000
Usuário Komerci 				user
Senha Komerci 					pass

Efetue a finalização de um pedido sobre o ambiente de teste onde será feito o processamento da transação

Em seguida, configure para o método usar o ambiente de produção

Efetue a finalização de um pedido de R$ 0,01 sobre o ambiente de produção

### Operações de Teste (Sandbox)

Apenas o Komerci Webservice permite a realização de testes. 

A Redecard recomenda que, para testar o Komerci Integrado, sejam realizadas compras em ambiente de produção e que se execute o estorno até o fim do mesmo dia.

### Processo de Homologação

Para a conclusão da configuração Komerci Webservice, deve ser analisado se o estabelecimento está habilitado para a função de captura WebService "SIM" e se os IP os estão cadastrados corretamente.

O cadastramento de IP os pode ser realizado através do portal de serviços Redecard na área restrita e pode ser efetuado o cadastramento de até 10 IPs.

Inicialmente, somente os web-métodos de testes estarão disponíveis, com transações de valor de (1) um centavos.

Para disponibilizar o sistema em produção o estabelecimento deve efetuar uma bateria de testes e os testes devem ser analisados no Relatório de Transações do Komerci.

Se a transação constar com o status "confirmado" significa que os testes foram efetuados com sucesso. Diferente deste status, o desenvolvimento deve ser revisto.

Para confirmar a integração realizada, o cliente deve fazer uma compra teste de 0,01. Após realização de compra, é necessário verificar se a mesma foi lançada em sua conta na Redecard.

### O que significam os códigos de erro

Verifique no Manual de integração o motivo da ocorrência do erro

Códigos e mensagens de retorno Rede:

As mensagens de bancos e operadoras são genéricas, abaixo disponibilizamos uma pequena lista com erros e retornos mais frequentes sendo que um erro poderá significar algo diferente do que estamos mencionamos.

Se tiveres dúvida ou o erro não constar na lista realize contato com suporte Komerci no telefone 1140014433

#### 23 - Transação não autorizada.

	Entre em contato com sua empresa de hospedagem e solicite os IPs de saida que é usado para o seu para o seu site

    Verifique no portal da Rede se os IPs de saída do servidor onde está hospedado o site estão configurados corretamente. 
    Caso o acesso seja realizado com a afiliação de sua matriz logue no portal da Rede, selecione o menu "Dados Cadastrais > Acesso às suas filiais" e selecione sua afiliação Komerci no menu "Minha Conta > Informações cadastrais > Clique no botão "Consultar" no box "Dados Cadastrais" > Endereços IP. 

    Se o erro persistir entre em contato via telefone com o suporte da Redecard informando a ocorrência e solicite se for necessário que seja aberto um chamado para a equipe técnica de gestão de incidentes da Redecard

#### 26 - Transação não autorizada.

    Esta mensagem de erro poderá retornar quando: 

        OS IPs de saída do servidor não estão configurados corretamente no Portal da Rede, veja no item acima como verificar se estão corretos.
        Os dados de convênio, usuário e senha webservices não estão corretos na administração do Magento.

#### 27 - Cartão Inválido.

    O número de cartão informado esta incorreto, por um ou mais dos seguintes motivos: 

        O cartão de bandeira Mastercard ou Visa não é numérico com 16 posições.
        O cartão de bandeira Diners não possui de 14 a 16 posições numéricas.
        O dígito do cartão esta inconsistente. 

 #### 41 - Transação não autorizada.

         Verifique se o usuário Webservice que está configurado no Portal da Rede é o mesmo que está configurado na administração do Magento. Para verificar no portal da Rede acesse o Menu "Dados Cadastrais > Acesso às suas filiais" e selecione sua afiliação Komerci. Localize o menu "Komerci > Usuários do Komerci > Cadastrar usuário". Caso o usuário não esteja cadastrado corretamente, remova e cadastre novamente. 

 #### 51 - Estabelecimento Inválido. Por favor, entre em contato com o estabelecimento que está efetuando a venda.

    Identificamos que está mensagem de erro retornou quando:

        O estabelecimento não possui liberação para aceitar cartões emitidos no exterior. Para confirmar se realmente o problema é este realize contato com suporte Komerci Rede e informe sua filiação.
        Cartão utilizado não tem a função crédito habilitado.
        Se esta mensagem de erro aparecer em todos os pedidos é possível que estabelecimento não tenha habilitado o gerenciador webservices. O gerenciador é responsável por realizar cancelamentos e pré-autorizar pagamentos na operadora. Poderás identificar se está é a causa através de um teste simples:
                Na administração do Magento nas configurações dos meio de pagamentos Rede marque a opção Autorizar e Capturar. Após faça um pedido de teste. Funcionou? Então realize contato com o suporte Komerci e informe que deseja habilitar o gerenciador webservices para seu estabelecimento.  

#### 53 - Transação Inválida. Por favor, entre em contato com o estabelecimento que está efetuando a venda.

        Transação não foi autorizada pelo banco emissor do cartão, possíveis causas:
            Parcelamento configurado na administração do Magento não está habilitado na operadora.
            Falta de limite.
            Cartão não tem habilitado função crédito.
            Número do cartão inválido. 

#### 56 - Dado inválido. Por favor, entre em contato com o estabelecimento que está efetuando a venda. 

        Pagamento não autorizado pelo banco emissor do cartão. 

#### 58 - Problemas com o cartão. Por favor, verifique os dados de seu cartão. Caso o erro persista entre em contato com a central de atendimento de seu cartão.

        Pagamento não autorizado pelo banco emissor do cartão. 

#### 74 - Instituição sem comunicação

        Operadora Rede não conseguiu comunicação com o banco emissor do cartão para concluir o processo de pagamento.  

#### 78 - Transação não Autorizada

        Estabelecimento está com problemas no cadastramento da filiação podendo estar suspensa, cancelada ou não cadastrada no Komerci.

    Lembramos que os erros são genéricos, caso tenha dúvida sobre o problema realize contato com a operadora Rede.

### Como alterar a imagem do método

Pode ser adicionado a imagem, contendo qualquer uma das nomenclaturas a seguir

- method-creditcard.png

E adicione a imagem no diretório do seu template

/skin/frontend/<TEMPLATE>/default/images/mozg_redecard

### Dados de contato - Redecard

Suporte Técnico Komerci  
REDECARD SA  
suporte.ecommerce@userede.com.br  
1140014433 (capitais e regiões metropolitanas) Opção 3  
0800 784433 (demais localidades)

Obs. Antes de entrar em contato, tenha em mãos seu número de filiação (estabelecimento), caso seja desenvolvedor informe o número do CNPJ da empresa

Havendo alguma ocorrência de erro sugiro enviar e-mail a Redecard informando a ocorrência, caso haja necessidade de efetuar alguma atualização o suporte da Redecard deve apontar o que deve ser feito

## Manual

https://www.userede.com.br/atendimento/documentos

## Contribuintes

Equipe Mozg

## License

[Comercial License](LICENSE.txt)

## Badges

[![Join the chat at https://gitter.im/mozgbrasil](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/mozgbrasil/)
[![Latest Stable Version](https://poser.pugx.org/mozgbrasil/magento-redecard-php56/v/stable)](https://packagist.org/packages/mozgbrasil/magento-redecard-php56)
[![Total Downloads](https://poser.pugx.org/mozgbrasil/magento-redecard-php56/downloads)](https://packagist.org/packages/mozgbrasil/magento-redecard-php56)
[![Latest Unstable Version](https://poser.pugx.org/mozgbrasil/magento-redecard-php56/v/unstable)](https://packagist.org/packages/mozgbrasil/magento-redecard-php56)
[![License](https://poser.pugx.org/mozgbrasil/magento-redecard-php56/license)](https://packagist.org/packages/mozgbrasil/magento-redecard-php56)
[![Monthly Downloads](https://poser.pugx.org/mozgbrasil/magento-redecard-php56/d/monthly)](https://packagist.org/packages/mozgbrasil/magento-redecard-php56)
[![Daily Downloads](https://poser.pugx.org/mozgbrasil/magento-redecard-php56/d/daily)](https://packagist.org/packages/mozgbrasil/magento-redecard-php56)
[![Reference Status](https://www.versioneye.com/php/mozgbrasil:magento-redecard-php56/reference_badge.svg?style=flat-square)](https://www.versioneye.com/php/mozgbrasil:magento-redecard-php56/references)
[![Dependency Status](https://www.versioneye.com/php/mozgbrasil:magento-redecard-php56/1.0.0/badge?style=flat-square)](https://www.versioneye.com/php/mozgbrasil:magento-redecard-php56/1.0.0)

:cat2: