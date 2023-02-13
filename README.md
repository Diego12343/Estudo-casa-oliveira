# Estudo de caso
## Casa Oliveira

Roberto é dono de um mercado no bairro de Vargem Grande, na cidade de Tupã. Ele herdou o negócio de seu pai, Gumercindo Oliveira, ela foi aberta em 1978 na garagem da casa da família, era uma pequena quitanda. Com o passar dos anos o negócio cresceu e Gumercindo foi obrigado a ir para outro ponto maior e ali permaneceu até os dias atuais.

Roberto, que agora é o novo dono do mercado continuou o negócio seguindo da mesma forma que o pai. Ele comprava diretamente com os fornecedores grandes volumes de produtos e armazenava em seu estoque. As vezes ele comprava muitos produtos que ainda havia em estoque causando uma sobrecarga de produtos, ele também tinha muitos produtos estragados, tais como: frutas, legumes, iogurtes, leites, frango, etc. Também havia muitos produtos com o prazo de validade vencido.

Os funcionários eram poucos e faziam muitas coisas ao mesmo tempo. O açougueiro também ajudava no estoque, a moça da limpeza ajudava na organização dos produtos das prateleira, além de ajudar na padaria, quanto o caixa estava vazio o operador ajudava a repor os laticínios e a limpar a loja. O repositor também fazia operação no caixa.

Ao realizar a venda o Roberto, que sabia o nome de quase todos os clientes, anotava em um caderno todos os produtos que vendia e que havia em estoque. Ao fim do dia , Roberto pegava o caderno de fazia os cálculos de o quanto havia vendido, somando o faturamento e realizando a atualização do estoque. Isso é feito todos os dias e tomava um tempo considerável para que tudo tenha sido feito.

Roberto fechava a loja as 18h, mas só ia para casa as 22h, após fazer todas as operações necessárias.
 Mesmo assim o negócio vai bem e Roberto pretende ir para outro ponto e aumentar o volume de negócios e contratar novos funcionários.
Marica, esposa de Roberto, vem conversando com ele há muito tempo para que ele contrate uma empresa para construir um sistema de informática para gerenciar o negócio e reduzir o tempo que ele passa trabalhando e tenha maior organização dos produtos, maior lucratividade e melhorar a gestão.

Com a intenção de aumentar o negócio, Roberto está disposto a informatizar sua empresa. Vamos ajudá-lo. Iremos começar construindo o banco de dados.







falta de funcionarios
Gerenciamento do estoque
baixa no estoque
funcionarios multifuncional
fluxo de caixa: Entrada e saida de valores
gestão do patrimonio: Computadores, prateleiras, Geladeiras, fogão, carrinho, caixas, balcões, balança, etc
setor de compras
setor financeiro


-Gestão do estoque
	-Informações sobre os produtos (fornecedor, marca,validade, lote, descrição, idproduto, categoria)

-Volume de produtos em estoque (quantidade_lote, quantidade_atual,             ultima_movimentação, quantidade_maxima, quantidade_minima, idproduto)


	-Funcionário
-informações(nome, função, salario, matricula, cpf,rg,telefone,email, estado civil, admissão, data_nascimento, endereço, usuario, senha, idfuncionario)
				    

	-Fluxo de caixa(formas de pagamento, limite_sangria, valor, entrada|saida, registro_venda)

	-Gestão de patrimonio(idpatriminio, codigopatrimonio, descrição, valor, nome, 		              setor_pertencente, data_aquisicao, setor_responsavel, data_baixa)
 
	
	

-setor de compras
-informacao_compras(idcompra, funcionario, valor_pag_produto, fornecedor, data_compra, numero_nota_fiscal, nome_produto, descricao, quantidade,     consumivel, setor_destino)				    

	-setor financeiro
-informacao_financeiro(idfuncionario, dispesas, lucro, disponibilidade_cofre, valor, tipo_valor, descricao, data_operacao, identificacao_responsavel)






!["Diagrama modelo conceitual"](./diagrama.png)

### Modelo Lógico

!["Diagrama do modelo lógico de estoque"](./modelo%20l%C3%B3gico%20estoque_png)


---
### Modelo físico
Código e documentação do modelo físico
/*
Para o projeto de banco de dados da Casa oliveira será criado
uma estrutura física com os comandos SQL(Structure Query Language)
Iremos começar com o comando de criação de banco de dados. Este
comando pertence a categoria de comandos DDL (Data Definition Language)
Comando:
    CREATE DATABASE nome_do_banco -> CREATE DATABASE casaoliveira
*/

CREATE DATABASE casaoliveira;
/*
Após a criação do banco de dados, é necessário selecioná-lo. Para isso
iremos usar o comando USE nome_do_bancodedados
*/
USE casaoliveira;

/*
Criação das entidades em modo físico usando os comandos SQL.
Para criar uma tabela(entidade) usaremos o comando
CREATE TABLE nome_da_tabela seguido por parenteses e os 
atributos(campos) da tabela, bem como a sua tipificação, ou seja,
devemos dizer qual o tipo de dados que cada campo(atributo) da
tabela deve receber. EX.: o campo idade deve receber valores
numéricos e, portanto será definido como int(inteiro).

Vamos criar a tabela de produtos. Esta tabela possui os seguintes campos:
    -idproduto,descricao,fornecedor,validade,lote,preco,nome,marca,categoria

    ```
     Para cada será definido um tipo de dado
	 para o idproduto, iremos definir como:
        -Chave-Primária (Primary Key) é nosso campo indexador, por ele será
        realizado o relacionamento com outras tabelas;
        -Vamos definir este campo com auto_incremente, o que permite gerar
        os ids de forma automática. Esse passo é importante, pois elimina alguns problemas,
         tais como: Concorrência, geração incrementada de valores e exclusividade
         de valores;
         -Vamos definir o campo o tipo de dado numérico int(inteiro)
         ```

         ```
Para o campo descricao, usaremos o tipo de dado Text. Com este tipo podemos inserir
até 64mil caracteres. Como neste campo pode haver a possibilidade de uma descrição 
longa do produto, se faz necessário um tamnho maior.

```
Para o campo fornecedor iremos usar o tipo de dado VARCHAR. Este tipo de dados nos permite
inserir textos, mas com um limite que pode ser pre definido pelo usuário ou podemos utilizar 
o limite total de 255 caracteres. Para o fornecedor, usaremos 50 caracteres.
```
Para o campo validade iremos usar o tipo de dado DATE.
```
```
Para o campo lote será definido o tipo de dado VARCHAR, pois há a possibilidade de valor conter
caracteres alfadecimais. Sendo assim, o VARCHAR é uma ótima opção por aceitar valores diversos.
```
```
O campo preco será definido como DECIMAL. Com esse tipo é possível inserir valores númericos
com a aplicação de casas decimais. Você define o comprimento e deste tamanho é configurado as
casas decimais.EX.: DECIMAL(10,2) -> COMPRIMENTO DE 10 DIGITOS E DESTES TEMOS 2 CASAS DECIMAIS.
VEJA: R$1111111,11 -> R$ 11.111.111,11
```
```
Para os campos nome, marca e categoria será definido o tipo de dado VARCHAR, pois este tipo
é capaz de receber caracteres de texto. Presisaremos, apenas definir, o tamanho de cada campo.
EX.: nome pode ficar com o tamanho 50, marca ficar com 30 e categoria 20
```
```
*/
CREATE TABLE produto(
idproduto int auto_increment primary key,
descricao text,
fornecedor varchar(50),
validade date,
lote varchar(20),
preco decimal(8,2),
nome varchar (50),
marca varchar(30),
categoria varchar (20)
);
CREATE TABLE estoque(
idestoque int auto_increment primary key,
idproduto int,
quantidade_maxima int,
quantidade_minima int,
quantidade_atual int,
ultima_movimentacao date,
quantidade_LOTE int);
```
### Modelo físico -MER(Modelo de Entidade Relacional)
![Diagrama do Modelo de Entidade Relacional](./modelo_fisico.png)

