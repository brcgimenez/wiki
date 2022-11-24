# PL/SQL - Treinamento Albert - Extra - M01
**Funções de 1 linha** 

* São funções prontas no Oracle.
* São usadas principalmente para manipular os valores que serão apresentados.
* Aceitam 1 ou + argumentos e retornam um único valor para cada linha do dataset gerado pela consulta.

**Funções de 1 linha - Numéricas**

* No Oracle, não funciona SELECT sem FROM, para isso existe a tabela DUAL:
	* SELECT 'exemplo' :x:
	* SELECT 'exemplo' FROM dual; :heavy_check_mark:
* Tabela DUAL -> o Oracle possui essa tabela contendo 1 coluna e 1 linha.
* Consulta das funções na documentação do Oracle:
	* [Documentação Oracle](docs.oracle.com/en/) > No campo de consulta: 'SQL language reference' > seção '7 Function'
* Tipos de funções:
	* ABS
	
		```sql
		SELECT ABS(-15) "Valor Absoluto" FROM DUAL;
		```
		
	* CEIL - Função que arredonda valores para cima ignorando casas decimais
	
		```sql
		SELECT CEIL(1.251) "Arredondamento" FROM DUAL; -- 2
		SELECT CEIL(-1.9) "Arredondamento" FROM DUAL; -- -1
		```
		
	* FLOOR - Função que arredonda valores para baixo ignorando casas decimais
	
		```sql
		SELECT FLOOR(1.251) "Arredondamento" FROM DUAL; -- 1
		```
		
	* MOD - Função que retorna o resto de uma divisão
	
		```sql
		SELECT MOD(11, 4) "Modulus" FROM DUAL; -- 3
		SELECT MOD(12, 4) "Modulus" FROM DUAL; -- 0
		```
		
	* ROUND - Função que arredonda de acordo com as casas decimais; Segundo parametro é a quantidade de casas decimais que deve verificar
	
		```sql
		SELECT ROUND(1.9) "Arredondamento" FROM DUAL; -- 2
		SELECT ROUND(1.95) "Arredondamento" FROM DUAL; -- 2
		SELECT ROUND(1.45) "Arredondamento" FROM DUAL; -- 1
		
		SELECT ROUND(1.4999, 2) "Arredondamento" FROM DUAL; -- 1,5
		SELECT ROUND(1.27777, 3) "Arredondamento" FROM DUAL; -- 1,278
		```
		
	* TRUNC - Função que corta/trunca o número; Segundo parametro é a quantidade de casas decimais que deve verificar
	
		```sql
		SELECT TRUNC(1.27123, 2) "Arredondamento" FROM DUAL; -- 1,27
		SELECT TRUNC(1.27923, 2) "Arredondamento" FROM DUAL; -- 1,27
		```
		
**Funções de 1 linha - Caracteres(string)**

* Tipos de funções que retornam caracteres:
	* CHR - Função que retorna o caracter Alfanumérico referente ao valor ASCII passado por parametro
	
		```sql
		SELECT CHR(67)||CHAR(65)||CHR(84) "DOG" FROM DUAL; -- CAT
		```
		
	* CONCAT - Função que concatena 2 ou mais strings
	
		```sql
		SELECT CHR(67)||CONCAT('A', 'T') "DOG" FROM DUAL; -- CAT
		```
		
	* INITCAP - Função que retorna a primeira letra de cada palavra em Uppercase
	
		```sql
		SELECT INITCAP('the soap') "Capitals" FROM DUAL; -- The Soap
		SELECT INITCAP('eu trabalho na philips') "Capitals" FROM DUAL; -- Eu Trabalho Na Philips
		```
		
	* LOWER - Função que retorna todas as letras em Lowercase
	
		```sql
		SELECT LOWER('eU trABAlho na PHILIPS') "Lower" FROM DUAL; -- eu trabalho na philips
		```
		
	* UPPER - Função que retorna todos os caracteres em Uppercase
	
		```sql
		SELECT LOWER('eU trABAlho na PHILIPS') "Lower" FROM DUAL; -- EU TRABALHO NA PHILIPS
		```
		
	* LPAD - Função preenche os caracteres com a quantidade de caracteres informado e com o caracter informado
		* Primeiro parametro - String a ser usada coomo referencia
		* Segundo parametro - Tamanho total da string de retorno
		* Terceiro parametro - Caracteres a ser preenchido para dar o tamanho total informado
	
		```sql
		SELECT LPAD('Page 1', 15, '*.') "LDAP Example" FROM DUAL; -- '*.*.*.*.*Page 1'
		SELECT LPAD('123', 5, '0') "LDAP Example" FROM DUAL; -- '00123'
		```
		
	* RPAD - Igual ao anterior porém preenche a direita
	
		```sql
		SELECT LPAD('123', 5, '0') "LDAP Example" FROM DUAL; -- '12300'
		SELECT LPAD('Bruno', 10, ' ') "LDAP Example" FROM DUAL; -- 'Bruno     '
		```
		
	* SUBSTR - Função que retorna parte da string
		* Primeiro parametro - String a ser usada
		* Segundo parametro - Posição inicial que será cortada a string; começa a contar a string a partir da posição 1
		* Terceiro parametro - Quantidade de caracteres que irá cortar após a posição inicial
	
		```sql
		SELECT SUBSTR('ABCDEFG', 3, 4) "Substring" FROM DUAL; -- CDEF
		```	
		
* Tipos de funções que retornam numeros:
	* ASCII - Função que retorna o valor da tabela ASCII de acordo com o caracter Alfanumérico passado por parametro
	
		```sql
		SELECT ASCII(64) "ASCII" FROM DUAL; -- A
		```
	
	* LENGTH - Função que retorna o tabalho da string
	
		```sql
		SELECT LENGTH('A') "LENGTH" FROM DUAL; -- 1
		SELECT LENGTH('BRUNO') "LENGTH" FROM DUAL; -- 5
		```	
	
	
**Funções de 1 linha - Data e Hora (DATE, TIMESTAMP E INTERVAL)**

* Tipos de funções:
	* TO_DATE - Função de conversão, que converte um valor, em string, para um date
		* Primeiro parametro - String com a data
		* Segundo parametro - String com a mascara
		* OBS.: O formado da String contendo a data tem que ser igual ao formato passado como mascara
	
		```sql
		SELECT TO_DATE('2022-11-24', 'yyyy-mm-dd') "Data" FROM DUAL; -- 2022-11-24
		SELECT TO_DATE('24/11/2022', 'dd/mm/yyyy') "Data" FROM DUAL; -- 24/11/2022
		```
		
	* ADD_MONTHS - Adiciona a quantidade de meses passado no parametro na data que foi passada como parametro
	
		```sql
		SELECT ADD_MONTHS(TO_DATE('01/07/2022', 'dd/mm/yyyy'), 2) "Date" FROM DUAL; -- 01/09/2022
		```
		
	* CURRENT_DATE - Função que retorna a data atual da sessão como calendario Gregoriano
	
		```sql
		SELECT CURRENT_DATE FROM DUAL; -- 2022-11-24
		```
		
	* CURRENT_TIMESTAMP - Função que retorna a data, hora e localização atual
	
		```sql
		SELECT CURRENT_TIMESTAMP FROM DUAL; -- 24/11/2022 13:26:29,12345600000 AMERICA/SAO PAULO
		```
		
	* LAST_DAY - Função que retorna o último dia do meês de determinada data passada por parametro
	
		```sql
		SELECT LAST_DAY(SYSDATE) FROM DUAL; -- 30/11/2022
		SELECT LAST_DAY('01/11/2022') FROM DUAL; -- 30/11/2022
		```
		
	* NEXT_DAY - Função que retorna a data do próximo dia da semana de acordo com a data passada e o dia da semana informado
	
		```sql
		SELECT NEXT_DAY('07/11/2022', 'SEGUNDA') FROM DUAL; -- 14/11/2022
		```

**Funções de 1 linha - Comparação**
* Determinam o maior ou o menor valor entre determinados valores
* Quando os valores passados são String, irá verificar através do valor ASCII de cada caracter

* Tipos de funções:
	* GREATEST - Função que retorna o maior valor entre os valores passados
	
		```sql
		SELECT GREATEST(89, 23, 43, 2, 56, 78) "Greatest" FROM DUAL; -- 89
		SELECT GREATEST('HARRY', 'HARRIOT', 'HAROLD') "Greatest" FROM DUAL; -- HARRY
		```
		
	* LEAST - Função que retorna o menor valor entre os valores passados
	
		```sql
		SELECT LEAST(89, 23, 43, 2, 56, 78) "Least" FROM DUAL; -- 2
		SELECT LEAST('HARRY', 'HARRIOT', 'HAROLD') "Least" FROM DUAL; -- HAROLD
		```
		
		
**Funções de 1 linha - Conversão**
* Convenção de nome - tipo_de_dato TO tipo_de_dado ou TO tipo_de_dado

* Tipos de funções:
	* ROWIDTOCHAR - Função que retorna o ID da linha como caracter
		
	* TO_CHAR - Função que retorna o que foi passado no parametro como string
		* Primeiro parametro - valor a ser convertido
		* Segundo parametro - formato desejado de saida
	
		```sql
		SELECT TO_CHAR(SYSDATE, 'dd/mm;yyyy') FROM DUAL; -- '24/11/2022'
		SELECT TO_CHAR(123.679) FROM DUAL; -- '123.679'
		SELECT TO_CHAR(123.679, '9,999,999.99') FROM DUAL; -- '      123.68' - já faz um round
		```
		
	* CAST - Função que convert um tipo de dado para outro
	
		```sql
		SELECT CAST('200' AS NUMBER DEFAULT 0 ON CONVERSION ERROR) FROM DUAL; -- 200 - NAS VERSOES MAIS NOVAS
		SELECT CAST('200' AS NUMBER) FROM DUAL; -- 200 - NAS VERSOES ANTIGAS
		```
	
**Outras funções importantes**

* Tipos de funções relacionadas a NULL:
	* COALESCE - Função que retorna a primeira expressão que não é nulla em uma lista de expressão
	* NVL - Função que avalia se um valor é nulo ou não, se não for, retorna o primeiro parametro, caso contrário, retorna o segundo
	
	
* Obs.: para retornar os dados da versão do DB e outras infos
	
	```sql
	SELECTR * FROM v$version;
	```
