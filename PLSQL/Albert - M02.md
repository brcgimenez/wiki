# PL/SQL - Treinamento Albert - Extra - M02

* PL/SQL usado para criar programas dentro do Oracle
* PL/SQL (Precedural Language for SQL)

* Bloco PL/SQL
	* Os códigos criados dentro do Oracle podem ser chamados de 'Unidades de Programa PL/SQL'. Esses podem ser **Bloco Anônino**, **Procedure**, **Function**, **Package**, **Trigger**, **Biblioteca** etc.
	* Consiste de um conjuto de instruções SQL ou PL/SQL, e desempenha uma função lógica única, a fim de resolver um problema específico ou executar conjuntos de tarefas afins.
	* Os blocos podem ser anônimos ou receber um nome para serem armazenados no banco de dados.
		* Bloco Anônimo -> Não tem nome / Não está armazenado no banco / Geralmente está armazenado na aplicação
		* Subprograma Armazenado (Stored subprogram) -> Utiliza a estrutura do bloco anônimo como base / Está armazenado no banco / Recebe nome.
	* Um bloco PL/SQL contém, pelo menos, três seções:
		* Seção de declaração (DECLARE) -> Define os objetos como: variáveis, constantes, cursores e exceções definidas pelo usuário que poderão ser utilizadas dentro do bloco;
		* Seção de execução (BEGIN ... END;) -> Contém sequência de comandos PL/SQL e instruções SQL do bloco;
		* Seção de tratamento de erro (EXCEPTION) -> Utilizada para o tratamento de erros.
	* Diretrizes e Regras:
		* Apenas a seção de execução é obrigatória;
		* IS, DECLARE, BEGIN, EXCEPTION não são seguidas de ';', mas END e todas as outras instruções são;
		* Não existe bloco sem algum comando válido;
		* Pode existir aninhamento de bloco, porém estrito à seção de Execução e à seção de Tratamento de Erro;
		* As linhas da seção de Execução devem ser finalizadas com ';';
	* Block Header -> Cabeçalho do bloco, somente utilizado para blocos nomeados, ou seja, blocos anônimos não tem essa seção. Especifica a forma como o programa é chamado por outros blocos.
	* Blocos anônimos não possuem cabeçalho. Começam com DECLARE se houver seção de declaração, caso contrário, inicia com BEGIN.
	* Blocos nomeados usam o IS/AS para iniciar a seção de declaração.
	* Consulta das funções na documentação do Oracle:
		* [Documentação Oracle](docs.oracle.com/en/) > No campo de consulta: 'PL/SQL language reference' > seção '2 Overview of PL/SQL'
	
	```sql
	<<compute_ratio>>
	<<another_label>>
	DECLARE
	  numerator   NUMBER := 22;
	  denominator NUMBER := 7;
	BEGIN
	  <<another_label>>
	  DECLARE --Bloco aninhado
		denominator NUMBER := 0;
	  BEGIN
		DBMS_OUTPUT.PUT_LINE('Ratio with compute_ratio.denominator = ');
		DBMS_OUTPUT.PUT_LINE(numerator/compute_ratio.denominator);
	 
		DBMS_OUTPUT.PUT_LINE('Ratio with another_label.denominator = ');
		DBMS_OUTPUT.PUT_LINE(numerator/another_label.denominator);
	 
	  EXCEPTION
		WHEN ZERO_DIVIDE THEN
		  DBMS_OUTPUT.PUT_LINE('Divide-by-zero error: can''t divide '
			|| numerator || ' by ' || denominator);
		WHEN OTHERS THEN
		  DBMS_OUTPUT.PUT_LINE('Unexpected error.');
	  END another_label;
	END compute_ratio;
	/
	```

* Comentários
	* Comentários de 1 linha -> '--';
	* Comentários de bloco -> '/*' e para fechar '*/';

* Declarações -> Para utilizar variáveis e constantes é preciso declara-las previamente. Variáveis declaradas em um bloco externo são acessíveis em qualquer parte do programa, já as declaradas no sub-bloco, são acessíveis somente dentro desse, ou seja, não são acessíveis externamente por outros sub-blocos.

	```sql
	<<externo>>
	DECLARE
		-- variavel a
		a	NUMBER := 1;
	BEGIN
		<<interno_01>>
		DECLARE
			b	NUMBER := 2;
		BEGIN
			DBMS_OUTPUT.PUT_LINE('valor de a no interno_01 = ' || a);
			DBMS_OUTPUT.PUT_LINE('valor de b no interno_01 = ' || b);
			
		EXCEPTION
			WHEN OTHERS THEN
				DBMS_OUTPUT.PUT_LINE('Erro inesperado.');
		END interno_01;
		
		<<interno_02>>
		DECLARE
			c	NUMBER := 3;
		BEGIN
			DBMS_OUTPUT.PUT_LINE('valor de a no interno_02 = ' || a);
			DBMS_OUTPUT.PUT_LINE('valor de c no interno_02 = ' || c);
			
		EXCEPTION
			WHEN OTHERS THEN
				DBMS_OUTPUT.PUT_LINE('Erro inesperado.');
		END interno_02;
		
		DBMS_OUTPUT.PUT_LINE('valor de a no externo = ' || a);
	END externo;
	/
	```

* Tipos de dados:
	* Tipos escalares -> são mais utilizados, contém um unico valor (int/char/character/long/varchar/varchar2/boolean/date/float/number/decimal);
	* Tipos compostos -> possui componentes internos que podem ser manipulados individualmente como os elementos de um array (RECORD/TABLE/VARRAY);
	* Tipos referência -> contém valores, chamdos ponteiros, que designam outros itens do programa (REF CURSOR/REF object_type);
	* Tipos LOB -> Contém valores, chamados localizadores de lob, que especificam a localização de objetos grandes, como blocos de texto ou imagens gráficas, que são armazenados separadamente (BFILE, BLOB, CLOB, NCLOB).

	* Comando %TYPE -> possibilita associar ao tipo de uma variável ao tipo de uma coluna de uma tabela, dessa maneira, a variável assumirá automaticamente o tipo de dado da coluna.
	* Comando %ROWTYPE -> cria uma estrutura de registro idêntica á uma estrutura de uma tabela.
	
	```sql
	<<externo>>
	DECLARE
		a	NUMBER := 1;
		b	a%TYPE := 2;
		c	VARCHAR2(100) := ' ESSA É UMA VARIÁVEL TEXTO ';
		d	DATE := SYSDATE;
	BEGIN
		DBMS_OUTPUT.PUT_LINE('valor de a = ' || a);
		DBMS_OUTPUT.PUT_LINE('valor de b = ' || b);
		DBMS_OUTPUT.PUT_LINE('valor de c = ' || c);
		DBMS_OUTPUT.PUT_LINE('valor de d = ' || d);
	END externo;
	/
	```

* Atribuição de valores:
	* Primeira forma -> ':=';
	* Segunda forma -> usando um SELECT com a expressão INTO. Esse SELECT obrigatóriamente deverá retornar uma e somente uma linha, caso contrário, um erro de execução será disparado:
		* NO_DATA_FOUND -> se não for retornada nenhuma linha;
		* TOO_MANY_ROWS -> se mais de uma linha for retornada.
	
	```sql
	DECLARE
		a	INTEGER := 10;
		b	INTEGER := 20;
		c	INTEGER;
		f	REAL;
	BEGIN
		c := a + b;
		DBMS_OUTPUT.PUT_LINE('valor de c = ' || c);
		
		f := 70.0/3.0;
		DBMS_OUTPUT.PUT_LINE('valor de f = ' || f);
	END externo;
	/
	```
	
	```sql
	DECLARE
		a	INTEGER := 10;
		b	INTEGER := 20;
		c	INTEGER;
		f	REAL;
		descricao_venda treinamento_venda.descricao%TYPE;
	BEGIN
		--SELECT valor INTO f FROM treinamento_venda; --isso gera um erro pois tem mais de uma linha retornando
		SELECT valor, descricao INTO f, descricao_venda 
		FROM treinamento_venda WHERE codigo=1;
		DBMS_OUTPUT.PUT_LINE('valor de f = ' || f);
		DBMS_OUTPUT.PUT_LINE('conteudo de descrição do campo descricao = ' || descricao_venda);
	END externo;
	/
	```

* Controle de fluxo - Condições
	* Podemos dividir em 2 blocos:
		* IF-THEN / IF-THEN-ELSE / IF-THEN-ELSIF-THEN;
		* CASE -> pode ser usado com ou sem seletor
	
	```sql
	DECLARE
		a	INTEGER := 10;
		b	INTEGER := 20;
		c	INTEGER;
		f	REAL;
		descricao_venda treinamento_venda.descricao%TYPE;
	BEGIN
		SELECT valor, descricao INTO f, descricao_venda 
		FROM treinamento_venda WHERE codigo=1;
		
		/*
		IF ( f < 110) THEN
			DBMS_OUTPUT.PUT_LINE('o valor de f é maior que 110 ------> ' || f);
		ELSIF ( f = 110) THEN
			DBMS_OUTPUT.PUT_LINE('o valor de f é igual a 110 ------> ' || f);
		ELSE
			DBMS_OUTPUT.PUT_LINE('o valor de f é maior que 110 ------> ' || f);
		END IF;
		*/
		
		--case com seletor
		CASE f
			WHEN 50 THEN
				DBMS_OUTPUT.PUT_LINE('o valor de f é 50 ------> ' || f);
			WHEN 100 THEN
				DBMS_OUTPUT.PUT_LINE('o valor de f é 100 ------> ' || f);
			WHEN 110 THEN
				DBMS_OUTPUT.PUT_LINE('o valor de f é 110 ------> ' || f);
			WHEN 200 THEN
				DBMS_OUTPUT.PUT_LINE('o valor de f é 200 ------> ' || f);
			ELSE
				DBMS_OUTPUT.PUT_LINE('o valor de f não é nenhum dos anteriores ------> ' || f);
		END CASE;
		
		--case sem seletor
		CASE 
			WHEN f=50 THEN
				DBMS_OUTPUT.PUT_LINE('o valor de f é 50 ------> ' || f);
			WHEN f=100 THEN
				DBMS_OUTPUT.PUT_LINE('o valor de f é 100 ------> ' || f);
			WHEN f=110 THEN
				DBMS_OUTPUT.PUT_LINE('o valor de f é 110 ------> ' || f);
			WHEN f=200 THEN
				DBMS_OUTPUT.PUT_LINE('o valor de f é 200 ------> ' || f);
			ELSE
				DBMS_OUTPUT.PUT_LINE('o valor de f não é nenhum dos anteriores ------> ' || f);
		END CASE;
		
	END externo;
	/
	```

* Controle de repetições - Laços
	* Encontramos 3 tipos:
		* LOOP simples
		* WHILE-LOOP
		* FOR-LOOP

	```sql
	DECLARE
		i	INTEGER;
		a	INTEGER := 10;
		f	REAL;
		descricao_venda treinamento_venda.descricao%TYPE;
	BEGIN
		/*
		LOOP
			a := a + 1;
			
			SELECT valor, descricao INTO f, descricao_venda 
			FROM treinamento_venda WHERE codigo=a;
			
			DBMS_OUTPUT.PUT_LINE('valor de f = ' || f);
			DBMS_OUTPUT.PUT_LINE('conteudo de descrição do campo descricao = ' || descricao_venda);
			DBMS_OUTPUT.PUT_LINE('-------------------------------------------');
			
			IF (a>15) THEN
				EXIT;
			END IF;
		END LOOP;
		*/
		
		/*
		WHILE a<15 LOOP
			a := a + 1;
			
			SELECT valor, descricao INTO f, descricao_venda 
			FROM treinamento_venda WHERE codigo=a;
			
			DBMS_OUTPUT.PUT_LINE('valor de f = ' || f);
			DBMS_OUTPUT.PUT_LINE('conteudo de descrição do campo descricao = ' || descricao_venda);
			DBMS_OUTPUT.PUT_LINE('-------------------------------------------');
		END LOOP;
		*/
		
		/*
		--EXECUTA O FOR INCREMENTANDO I
		FOR i IN 1 .. 15 LOOP
			SELECT valor, descricao INTO f, descricao_venda 
			FROM treinamento_venda WHERE codigo=i;
			
			DBMS_OUTPUT.PUT_LINE('valor de f = ' || f);
			DBMS_OUTPUT.PUT_LINE('conteudo de descrição do campo descricao = ' || descricao_venda);
			DBMS_OUTPUT.PUT_LINE('-------------------------------------------');
		END LOOP;
		
		--EXECUTA O FOR DECREMENTANDO I
		FOR i IN REVERSE 1 .. 15 LOOP
			SELECT valor, descricao INTO f, descricao_venda 
			FROM treinamento_venda WHERE codigo=i;
			
			DBMS_OUTPUT.PUT_LINE('valor de f = ' || f);
			DBMS_OUTPUT.PUT_LINE('conteudo de descrição do campo descricao = ' || descricao_venda);
			DBMS_OUTPUT.PUT_LINE('-------------------------------------------');
		END LOOP;
		*/
		
		--POSSO USAR LAÇOS ANINHADOS
	END externo;
	/
	```

* Labels
	* São usados para melhorar a leitura do programa PL/SQL;
	* São aplicados a Blocos ou Loops;
	* Deve preceder imediatamente um bloco ou LOOP e deve ser delimitado por '<<' e '>>'
	* A cláusula END ou END LOOP pode fazer referência ao label
	* Seu uso é vantajoso quando existem vários blocos aninhados
	
	```sql
	DECLARE
		i	INTEGER;
		a	INTEGER := 10;
		f	REAL;
		descricao_venda treinamento_venda.descricao%TYPE;
	BEGIN
		<<laco_externo>
		FOR i IN 1 .. 15 LOOP
			SELECT valor, descricao INTO f, descricao_venda 
			FROM treinamento_venda WHERE codigo=i;
			
			DBMS_OUTPUT.PUT_LINE('valor de f = ' || f);
			DBMS_OUTPUT.PUT_LINE('conteudo de descrição do campo descricao = ' || descricao_venda);
			DBMS_OUTPUT.PUT_LINE('-------------------------------------------');
		
		
			<<laco_interno>
			FOR a IN REVERSE 1 .. 15 LOOP
				
				IF (a=3) THEN
					CONTINUE;
				END IF;
				
				DBMS_OUTPUT.PUT_LINE('valor de A = ' || a);
				DBMS_OUTPUT.PUT_LINE('conteudo de descrição do campo descricao = ' || descricao_venda);
				
				IF (a = 8) THEN
					EXIT;
				END IF;
				
				/*IF (a+i = 15) THEN
					EXIT laco_externo;
				END IF;*/
			END LOOP laco_interno;
		
		END LOOP laco_externo;
		
		--POSSO USAR LAÇOS ANINHADOS
	END externo;
	/
	```

* Cursores -> O Oracle cria uma àrea de memória, conhecida como àrea de contexto, que contém todas as informações necessárias para o processamento do SQL.
	* Um cursor é um ponteiro para esta área de contexto;
	* Um cursor contém as linhas (1 ou +) retornadas por uma instrução SQL;
	* O conjunto de linhas que o cursor mantém é chamado de conjunto ativo (active set).
	* Existem 2 tipos:
		* Cursores implícitos -> são criados automaticamente pelo Oracle sempre que uma instrução SQL é executada
			* Os programadores não podem controla-los e nem as informações neles contidas;
			* Sempre que uma instrução DML (INSERT, UPDATE E DELETE) é emitida, um cursor implícito é associado a essa instrução;
				* Operações INSERT -> o cursor mantém os dados que precisam ser inseridos;
				* Operações UPDATE e DELETE -> o cursor identifica as linhas que seriam afetadas.
			* Para acessar o cursor implícito é utilizado o comando 'sql%', ex.: sql%notfound
			
		* Cursores Explícitos -> São definidos pelo programador para obter mais controle sobre a área de contexto;
			* Deve ser definido na seção de declaração do bloco;
			* É criado em uma instrução de SELECT que retorna mais de uma linha.
			* É necessário seguir as etapas:
				* Declarar o cursor para inicializar a memória (DECLARE);
				* Abrir o cursor para alocar a memória (OPEN);
				* Buscar o cursor para recuperar os dados (FETCH);
				* Fechar o cursor para liberar a memória alocada (CLOSE).
	
	![image](https://user-images.githubusercontent.com/114239313/204035549-657d15b3-d027-4f03-b619-ac5710dfd097.png)
				
	```sql
	/*
	DECLARE
	BEGIN
		UPDATE treinamento_venda SET valor = valor * 1.1;
		
		IF SQL%notfound THEN
			DBMS_OUTPUT.PUT_LINE('Nenhuma venda foi afetada');
		ELSIF SQL%found THEN
			DBMS_OUTPUT.PUT_LINE('Algumas vendas foram afetadas. Quantas?');
			DBMS_OUTPUT.PUT_LINE(SQL%rowcount);
		END IF;
	END;
	/
	*/
	
	DECLARE
		v_codigo	treinamento_venda.codigo%type;
		v_descricao	treinamento_venda.descricao%type;
		v_valor		treinamento_venda.valor%type;
		CURSOR cur_venda IS
			SELECT codigo, descricao, valor FROM treinamento_venda;
	BEGIN
		OPEN cur_venda;
		
		LOOP
			FETCH cur_venda INTO v_codigo, v_descricao, v_valor;
			EXIT WHEN cur_venda%notfound;
				
				DBMS_OUTPUT.PUT_LINE('Código da venda = ' || v_codigo);
				DBMS_OUTPUT.PUT_LINE('Descrição da venda = ' || v_descricao);
				DBMS_OUTPUT.PUT_LINE('Valor da venda = ' || v_valor);
		END LOOP;
		CLOSE cur_venda;
	END;
	/
	```

* Tratamento de Exceções
	* Existem dois tipos:
		* Exceções definidas pelo sistema
		* Exceções definidas pelo usuário
		* Conceitos:
			* Erro de execução ou exceção -> situação adversa que ocasiona interrupção na execução do programa podendo ser motivada por falha na concepção do sistema, codificação equivocada, falha de hardware, etc.;
			* Exceção PL/SQL -> é o objeto de programação PL/SQL que nos permite evitar a interrupção abrupta do programa caso este seja acometido por um erro de execução;
			* Tratamento da exceção -> indica qual ação ou quais ações deverão ser tomadas quando o programa for acometido por um erro de execução.
			
	```sql
	DECLARE
		v_codigo_informado	INTEGER := 500;
		v_codigo	treinamento_venda.codigo%type;
		v_descricao	treinamento_venda.descricao%type;
		v_valor		treinamento_venda.valor%type;
		v_minha_excecao	EXCEPTION;
	BEGIN
		
		IF v_codigo_informado > 200 THEN
			RAISE v_minha_excecao;
		END IF;
	
	
		SELECT codigo, descricao, valor INTO v_codigo, v_descricao, v_valor
		FROM treinamento_venda 
		WHERE codigo=v_codigo_informado;

		DBMS_OUTPUT.PUT_LINE('Descrição da venda selecionada = ' || v_descricao);
		
		EXCEPTION
			WHEN v_minha_excecao THEN
				DBMS_OUTPUT.PUT_LINE('Por favor, informa um código menor que 200. Código => ' || v_codigo);
			WHEN no_data_found THEN
				DBMS_OUTPUT.PUT_LINE('Não existe venda para o código informado. Código => ' || v_codigo);
			WHEN OTHERS THEN
				DBMS_OUTPUT.PUT_LINE('Um problema ocorreu no sistema.');
	END;
	/
	```
