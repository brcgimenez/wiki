# Configuração do ambiente para subir local o Web Suite
Abaixo contém as configurações de ambiente necessárias para executar o projeto "Health Professional" local apontando para uma base específica.

## Verificar/Gerar as credenciais para o projeto "Health Professional" na aplicação
1. Para verificar se a aplicação tem as credenciais do projeto, execute a consulta abaixo:

    `select * from client where ds_client='HEALTHPROFESSIONAL';`

    O resultado deverá ser algo parecido com a imagem abaixo:
    ![image](https://github.com/brcgimenez/wiki/assets/114239313/5080edf9-d76b-4d0d-8cc5-f87e79290631)


2. Caso não tenha registro, far-se-á necessário executar a procedure abaixo para gerar as credenciais:
    ```
    begin
    	configure_psa_tws_pack.configure_psa_tws_healthprof(10);
    	commit;
    end;
    ```

* Para verificar se funcionou corretamente a execução da procedure, basta executar o passo 1 novamente.

## Configurar o backend para executar na base local
Após verificado/gerado as credenciais na aplicação, faça as alterações abaixo no projeto "health-professional-backend":
1. Configurar o arquivo "configuration.yml" com as credenciais da aplicação.
	
     1.1 na raiz do projeto do backend, abrir o arquivo "configuration.yml" e alterar as seguintes propriedades
       ![image](https://github.com/brcgimenez/wiki/assets/114239313/0cf3694c-69a2-4733-bd76-8ca82f0e4ade)

      1.1.1 urlSecurity => informar a url da base para a autenticação;

      1.1.2 clientID => informar com o valor do campo ID da consulta do passo 1 do processo anterior;

      1.1.2 clientSecret => informar com o valor do campo DS_SECRET da consulta do passo 1 do processo anterior;
	
	  1.2 na pasta "health-professional-service", abrir o arquivo "configuration.yml" e alterar a propriedade "jdbcUrl"
	  ![image](https://github.com/brcgimenez/wiki/assets/114239313/e72c8e01-ffa5-4ba8-8f4b-369dac3f3097)

 
2. Após configurado, executar o "clean and build" do projeto e, após finalizado, executar o "buildRun".

* Antes de executar o passo 2, far-se-á necessário para a execução do cisco umbrela
![image](https://github.com/brcgimenez/wiki/assets/114239313/d12fddb3-947b-4be4-9fae-095a6067b546)


## Configurar o frontend para executar na base local
Após configurado o backend, faça a seguinte alteração no projeto "health-professional-frontend":

1. Configurar o arquivo ".oswaldrc.json" com a URL local, conforme imagem abaixo:
![image](https://github.com/brcgimenez/wiki/assets/114239313/b4e13aec-7f3f-4b53-b5d6-c80c8e7a233c)


* para executar o projeto do frontend, certifique-se de ter as seguintes configurações e passos:
	- ter instalado o Nodejs >= 18.8.0
	- ter executado os comandos `npm install && npm run reinstall`
	- para executar o front, basta rodar o comando `npm run start`
![image](https://github.com/brcgimenez/wiki/assets/114239313/af4fbfec-5caa-4a0e-85c1-4f8397703253)


# Configuração da Base para utilização do PEP no Web Suite

## Configurar a aplicação "Profissional de saúde"
1. Acesse Administração Web Suite > Configurações > Gerais > Geral
2. No modal, selecione "Profissional de saúde"
![image](https://github.com/brcgimenez/wiki/assets/114239313/612e0b06-94e9-4ac9-aaa6-5328adbbe66c)

3. Caso não tenha registro, adicione um novo
4. No campo "Link de acesso à aplicação cadastrada", informe a URL da aplicação (obs.: informa apenas até a barra após a porta, conforme imagem abaixo)
![image](https://github.com/brcgimenez/wiki/assets/114239313/b503e34a-f542-40e1-85af-a1b27c9b59d1)


## Liberar o usuário para acesso ao mobile
1. Acesse Administração Web Suite > Usuário > Cadastro de usuários
2. Botão direito do mouse, selecione a opção "Liberar acesso para profissional de saúde"
![image](https://github.com/brcgimenez/wiki/assets/114239313/9d8ba3c6-a497-436e-9556-d53f17710c04)

3. Informe o usuário do tasy e clique em "Avançar"
![image](https://github.com/brcgimenez/wiki/assets/114239313/5a91e9cd-4e8b-4c08-a77c-48b6809aa3d7)

4. Selecione o perfil e clique em "Finalizar"
![image](https://github.com/brcgimenez/wiki/assets/114239313/0922fe28-a595-401d-86b3-9fb9e5cbff16)

** caso o perfil desejado não seja apresentado ou o campo esteja readonly, é necessário cadastrar um perfil que será utilizado no mobile, para isso basta seguir os passos do processo abaixo.

## Configurar perfil para utilização no mobile
1. Acesse Administração Web Suite > Parâmetros função > Perfil
![image](https://github.com/brcgimenez/wiki/assets/114239313/6f7b42a8-661f-4843-97a2-ab4c70ce4815)



## Configurar os parâmetros para acesso as funções no mobile
1. Acesse Administração Web Suite > Parâmetros função > Parâmetros
   
	1.1 Web Suite Profissional da saúde
   
	  1.1.1 Liberar as funções necessárias para o seu usuário
   ![image](https://github.com/brcgimenez/wiki/assets/114239313/c0a5947f-1031-4491-a841-c5d6bb9c01e3)

	1.2 Web Suite Prontuário Eletrônico do Paciente
   
	  1.2.1 Liberar os itens para o PEP
    ![image](https://github.com/brcgimenez/wiki/assets/114239313/c4159ea6-22af-4c4c-a641-e864b743fa6f)
