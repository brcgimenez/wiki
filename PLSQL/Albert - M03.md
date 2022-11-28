# PL/SQL - Treinamento Albert - Extra - M03

* Objetos procedurais -> stored subprograms / stored procedures / stored functions / packages / triggers

* Subprogramas armazenados (Stored Subprograms)
	* São desenvolvidos, compilados e armazenados no banco de dados Oracle. Estão disponíveis para leitura e execução;
	* Uma vez compilados, se tornam objetos na forma de stored procedures ou stored functions que podem ser acessados pelos usuarios e aplicações conectadas ao banco de dados.
	* Procedure não retorna valores, function sim
	
	```sql
	CREATE [OR REPLACE] PROCEDURE -- cria uma procedure
	CREATE [OR REPLACE] FUNCTION  -- cria uma function
	```
	
* Stored Procedures
	* PROCEDURE é um bloco PL/SQL nomeado que pode receber parâmetros e que pode ser referenciada por nome;
	* Para transformar um bloco PL/SQL anônimo em uma PROCEDURE, basta eliminar a palavra DECLARE (se existir) e adicionar
	
	```sql
	CREATE [OR REPLACE] PROCEDURE nome_da_procedure (par1, par2, ..., parN) IS
	```
	
	* Sintaxe
	
	```sql
	CREATE [OR REPLACE] PROCEDURE procedure_name
	[(parameter_name [IN | OUT | IN OUT] type [, ...])]
	{IS | AS}
	BEGIN
		<CORPO>
	END procedure_name;
	```
	
	* A lista de parâmetros opcionais contém nome, modo e tipo.
	* Nos parametros, IN representa o valor que será passado de fora para dentro da procedure; OUT representa o parâmetro que será utilizado para retornar um valor para fora do procedimento
	* podem ser chamadas a partir de: Blocos anonimos / procedures / triggers / functions
	* modos de parametros:
		* IN -> somente leitura; pode ser passado uma constante, literal, variável inicializada ou expressão; pode inicializar com valor padrão, no entanto, nesse caso, ele é omitido da chamada; modo padrão de passagem; são passados por referencia.
		* OUT -> retorna um valor para o programa de chamada, seja no próprio banco ou aplicações; dentro do subprograma, atua como uma variável; pode alterar seu valor e fazer referencia ao valor depois de atribui-lo; o argumento passado deve ser variável e é passado por valor.
		* IN OUT -> pssar um valor inicial para o subprograma e retorna um valor atualizado para o chamados; pode ser alterado; o argumento passado deve ser uma variável, não pode ser constante ou expressão; o argumento é passado por valor.
	* parametros podem ser passados de 3 formas:
		* Position notation -> passa o argumento de acordo com a posição do parametro;
		* named notation -> passa o argumento usando o nome do parametro e para isso utiliza o simbolo '=>';
		* mixed notation -> nesse caso é possível misturar os dois modos, observando que a partir do momento que eu usar uma 'named notation', os argumentos posteriores devem seguir também como a mesma.
	* para chamar procedures, posso utilizar:
		* 'EXECUTE nome_procedure;' -> essa opção pode ser usada para procedures com ou sem parametros; traca como um programa e não precisa informar o '()';
		* 'CALL nome_procedure();' -> essa opção é usada para procedures com parametros; trata como procedimento e precisa informar o '()';
	* Chamando de um bloco anonimo e recebendo retorno
		* Procedure
		
			```sql
			CREATE OR REPLATE PROCEDURE PROC_TREINAMENTO_VENDA
			(
				p_codigo_informado IN INTEGER, 
				p_valor_venda OUT treinamento_venda.valor%type,
				p_valor_venda_10 IN OUT treinamento_venda.valor%type)
			IS
				v_codigo	treinamento_venda.codigo%type;
				v_descricao	treinamento_venda.descricao%type;
				v_valor		treinamento_venda.valor%type;
				v_minha_excecao	EXCEPTION;
			BEGIN
				
				IF p_codigo_informado > 200 THEN
					RAISE v_minha_excecao;
				END IF;
			
			
				SELECT codigo, descricao, valor INTO v_codigo, v_descricao, v_valor
				FROM treinamento_venda 
				WHERE codigo=p_codigo_informado;
				
				p_valor_venda := v_valor;
				p_valor_venda_10 := p_valor_venda_10 + (p_valor_venda * 1.1);

				DBMS_OUTPUT.PUT_LINE('Descrição da venda selecionada = ' || v_descricao);
				
				EXCEPTION
					WHEN v_minha_excecao THEN
						DBMS_OUTPUT.PUT_LINE('Por favor, informa um código menor que 200. Código => ' || p_codigo_informado);
					WHEN no_data_found THEN
						DBMS_OUTPUT.PUT_LINE('Não existe venda para o código informado. Código => ' || p_codigo_informado);
					WHEN OTHERS THEN
						DBMS_OUTPUT.PUT_LINE('Um problema ocorreu no sistema.');
			END;
			```
			
		* Chamando de um bloco anonimo
			```sql
			DECLARE
				valor_venda NUMBER;
				valor_venda_calculado NUMBER := 50;
			BEGIN
				PROC_TREINAMENTO_VENDA(20, valor_venda, p_valor_venda_10 => valor_venda_calculado);
				DBMS_OUTPUT.PUT_LINE('Valor da venda que retornou = '|| valor_venda);
				DBMS_OUTPUT.PUT_LINE('Valor da venda calculado = '|| valor_venda_calculado);
			END;
			/
			```
		
* Stored Functions
	* FUNCTIONS são blocos PL/SQL nomeado que pode, ou não, receber parâmetros e que deve ser referenciada por nome;
	* Deve obrigatóriamente ter um valor de retorno associado a ela
	* A clausula RETURN especifica o tipo de dados que será retornado
	* Sintaxe
	
    ```sql
    CREATE [OR REPLACE] FUNCTION function_name
    [(parameter_name [IN | OUT | IN OUT] type [, ...])]
    RETURN return_datatype
    {IS | AS}
    BEGIN
      <CORPO>
    END function_name
    ```
	
	* Chamando de um bloco anonimo e recebendo retorno
		* Function
		
			```sql
			CREATE OR REPLATE FUNCTION FUNC_TREINAMENTO_VENDA
			(
				p_codigo_informado IN INTEGER, 
				p_valor_venda OUT treinamento_venda.valor%type,
				p_valor_venda_10 IN OUT treinamento_venda.valor%type)
				RETURN VARCAHR2
			IS
				v_codigo	treinamento_venda.codigo%type;
				v_descricao	treinamento_venda.descricao%type;
				v_valor		treinamento_venda.valor%type;
				v_minha_excecao	EXCEPTION;
			BEGIN
				
				IF p_codigo_informado > 200 THEN
					RAISE v_minha_excecao;
				END IF;
			
			
				SELECT codigo, descricao, valor INTO v_codigo, v_descricao, v_valor
				FROM treinamento_venda 
				WHERE codigo=p_codigo_informado;
				
				p_valor_venda := v_valor;
				p_valor_venda_10 := p_valor_venda_10 + (p_valor_venda * 1.1);

				DBMS_OUTPUT.PUT_LINE('Descrição da venda selecionada = ' || v_descricao);
				
				RETURN v_descricao;
				
				EXCEPTION
					WHEN v_minha_excecao THEN
						DBMS_OUTPUT.PUT_LINE('Por favor, informa um código menor que 200. Código => ' || p_codigo_informado);
					WHEN no_data_found THEN
						DBMS_OUTPUT.PUT_LINE('Não existe venda para o código informado. Código => ' || p_codigo_informado);
					WHEN OTHERS THEN
						DBMS_OUTPUT.PUT_LINE('Um problema ocorreu no sistema.');
			END;
			```
			
		* Chamando de um bloco anonimo
			```sql
			DECLARE
				valor_venda NUMBER;
				valor_venda_calculado NUMBER := 50;
				retorno_da_funcao VARCAHR2(100);
			BEGIN
				retorno_da_funcao := FUNC_TREINAMENTO_VENDA(20, valor_venda, p_valor_venda_10 => valor_venda_calculado);
				DBMS_OUTPUT.PUT_LINE('Valor da venda que retornou = '|| valor_venda);
				DBMS_OUTPUT.PUT_LINE('Valor da venda calculado = '|| valor_venda_calculado);
				DBMS_OUTPUT.PUT_LINE('Descricao da venda selecionada = '|| retorno_da_funcao);
			END;
			/
			```
			
* Packages
	* São objetos de esquema que agrupam tipos, variáveis e subprogramas
	* Tem 2 partes obrigatórias
		* Especificação do pacote
			* É a interface para o pacote. Apesa DECLARA os tipos, variáveis, constantes, exceções, cursores e subprogramas que podem ser referenciados de fora do pacote.
			Ou seja, contém todas as informações sobre o conteúdo do pacote, mas exclui o código dos subprogramas.
			* Todos os objetos colocados aqui são chamados de objetos **publicos**.
			* Qualquer subprograma não esteja aqui as esteja codificado no corpo do pacote, é chamado de objeto **privado**.
			* O trecho a seguir mostra uma espeficicação de pacote com um único procedimento. Pode se ter vários procedimentos, funcoes e variaveis
			
			```sql
			CREATE PACKAGE salario As
				PROCEDURE buscar_salario(c_id colaborador.id%type);
			END salario
			```
			
		* Corpo ou definição do pacote
			* Tem os códigos para vários métodos declarados na especificação do pacote e outras declarações privadas, que estão ocultas do código fora do pacote.
			* O trecho a seguir mostra a declaração do corpo do pacote
			
			```sql
			CREATE OR REPLATE PACKAGE BODY salario AS
				PRECEDURE buscar_salario(c_id colaborador.id%TYPE) IS
					v_salario colaborador.valor_salario%TYPE;
				BEGIN
					SELECT valor_salario INTO v_salario
					FROM colaborador
					WHERE id = c_id;
					
					DBMS_OUTPUT.PUT_LINE('Salário: ' || v_salario);
				END buscar_salario;
			END salario;
			/
			```
			
	* Para usar os elementos do pacote tem a seguinte sintaxe:
	
	```
	<nome_pacote>.<nome_variavel_function_procedure>(pars);
	```
	
	* No exemplo a baixo, quando executado a IDE pedirá ao usuário para informar um valor e o passará como argumento
		
	```sql
	DECLARE
		codigo colaborador.id%TYPE := &cc_id;
	BEGIN
		salario.buscar_salario(codigo);
	END;
	/
	```
	
	* Exemplo ESPECIFICAÇÃO
	
	```sql
	CREATE OR REPLACE PACKAGE vendas AS
		FUNCTION pegar_nome_venda(p_codigo_informado INTEGER);
		RETURN VARCHAR2;
		
		FUNCTION pegar_valor_venda(p_codigo_informado INTEGER);
		RETURN NUMBER;
	END vendas;
	```
	
	* Depois de compilado a ESPECIFICAÇÃO, compilar o corpo
	
	```sql
	CREATE OR REPLACE PACKAGE BODY vendas AS
		
		FUNCTION pegar_nome_venda (p_codigo_informado IN INTEGER)
		RETURN VARCHAR2
		IS
			v_descricao	treinamento_venda.descricao%type;
		BEGIN
			SELECT descricao INTO v_descricao
			FROM treinamento_venda 
			WHERE codigo=p_codigo_informado;
			
			RETURN v_descricao;
		END pegar_nome_venda;
	
		FUNCTION pegar_valor_venda (p_codigo_informado IN INTEGER)
		RETURN NUMBER
		IS
			v_valor	treinamento_venda.valor%type;
		BEGIN
			SELECT valor INTO v_valor
			FROM treinamento_venda 
			WHERE codigo=p_codigo_informado;
			
			RETURN v_valor;
		END pegar_valor_venda;
	
	END vendas;
	```
	
	* Obs.: A assinatura do método na especificação tem que ser a mesma no corpo, mesmo nome de método e parametros e os mesmos tipos
	* Chamando de um bloco anonimo
			```sql
			DECLARE
				valor_venda NUMBER;
				nome_venda VARCAHR2(100);
			BEGIN
				nome_venda := vendas.pegar_nome_venda(1);
				DBMS_OUTPUT.PUT_LINE('Descrição da venda = ' || nome_venda);
				
				valor_venda := vendas.pegar_valor_venda(2);
				DBMS_OUTPUT.PUT_LINE('Valor da venda = ' || valor_venda);
			END;
			/
			```
	
* Triggers
	* Podem ser compostos por instruções SQL e PL/SQL
	* Uma stored procedure é chamada por um usuário, aplicação ou trigger; Já uma trigger são implicitamente **disparados** pelo banco quando um determinado evento ocorre.
	* São executados em resposta a qualquer um dos seguintes eventos:
		* Instrução de manipulação de banco de dados (DML) (DELETE, INSERT ou UPDATE);
		* Instrução de definição de banco de dados (DDL) (CREATE, ALTER OU DROP);
		* Operação de banco de dados (SERVERERROR, LOGON, LOGOFF, STARTUP OU SHUTDOWN).
	* Podem ser escritos para os seguintes propósitos:
		* Gerar alguns valores de coluna derivados automaticamente;
		* Aplicar a integridade referencial;
		* Registro de eventos e armazenamento de informações sobre acesso à tabela;
		* Auditoria
		* Replicação síncrona de tabelas;
		* Import autorizações de segurança;
		* Evitar transações inválidas.
	* Sintaxe:
	
	```sql
	CREATE [OR REPLACE] TRIGGER trigger_name
	{BEFORE | AFTER | INSTEAD OF}
	{INSERT [OR] | UPDATE [OR] | DELETE}
	[OF col_name]
	ON table_name
	[REFERENCING OLD AS o NEW AS n]
	[FOR EACH ROW]
	WHEN (condition)
	DECLARE
		Declaration-statements
	BEGIN
		Executable-statements
	EXCEPTION
		Exception-handling-statements
	END;
	```
	
	* Exemplo
	
	```sql
	CREATE OR REPLACE TRIGGER atualizar_valor_venda
	BEFORE INSERT OR UPDATE OR DELETE
	ON treinamento_venda
	FOR EACH ROW
	WHEN (NEW.codigo > 0)
	DECLARE
		v_diferenca NUMBER;
	BEGIN
		v_diferenca := :NEW.valor - :OLD.valor;
		DBMS_OUTPUT.PUT_LINE('Valor anterior = ' || :OLD.valor);
		DBMS_OUTPUT.PUT_LINE('Valor atual = ' || :NEW.valor);
		DBMS_OUTPUT.PUT_LINE('Diferença = ' || v_diferenca);
	END;
	/
	
	UPDATE treinamento_venda SET valor=101 WHERE codigo=1; --no uptade tem o valor de NEW e o valor de OLD para código
	INSERT INTO treinamento_venda (codigo, valor) VALUES (28, 777); --no insert tem o valor de NEW e não tem o valor de OLD para código
	DELETE FROM treinamento_venda WHERE codigo=28; --no delete não será exibido nada pois na trigger está verificando valor para NEW, e no delete não tem valor de NEW somente OLD
	```
