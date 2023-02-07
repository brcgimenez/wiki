# Oftalmologia (Conceito)
* Objetivos
	<<IMAGEM objetivos-oftalmologia>>
* Conceito oftalmologia
<<IMAGEM conceito-oftalmologia>>
* Principais doenças
<<IMAGEM principais-doencas-oftalmologia>>
* Outas doenças
<<IMAGEM outras-doencas-oftalmologia>>
* Principais exames
<<IMAGEM principais-exames-oftalmologia>>
* Exames
<<IMAGEM exames-oftalmologia>>
* Fluxograma
	<<IMAGEM fluxograma-oftalmologia>>
	* Paciente - Quando é solicitado uma avaliação do especialista onde o mesmo fará alguns exames
	* É necessário gerar uma consulta
	
* Principais funcionalidades
	* Permite acessar a função através das agendas (exames, etc)
	* permite definir o tipo de conuslta realizada pelo medico e prof de saude de acordo com os itens utilizados
	* permite registrar os principais exames oftalmologicos com registros de imagens e fotos (é possivel gerar uma receita de oculos, receita medica>receita de oculos)
	* permite definir os itens que serão apresentados na aba visao conforme a necessidade (personalizavel)
* principais comunicações entre funcções
	* Gestão da agenda cirurgica
	* agenda de exames
	* agenda de consultas
	* Prescrição eletronica do paciente - REP
	* PEP


# Oftalmologia - Agendamento(html5)
* Agendamento
	* As consultas oftalmologicas são possiveis de serem realizadas após o agendamento dos pacientes que serão atendidos pelo oftalmo
	* Alem disso, favorecem outros processos da oftalmologia que estão relacionadas ao pre-exame, procedimento ambulatorial e cirurgia
* Agendamento
	* pode ser usada as funções Agenda de consultas e gestao da agenda cirurgica que estão vinculadas a função Oftalmologia
	* ou pela função entrada unica do paciente
	* ou função agenda de exames
	* Função agenda de exames
		* localizar pela agenda "oftalmo exames"
		* informações importantes
			* pode ser paciente externo ou internado
			* duração advem do cadastro
			* coluna exames - apresenta o nome do procedimento, exame ou consulta
			* Coluna classificação - agendado, encaixe, retorno
			* coluna status do paciente - monitoramento (aguardando autorização do convenio, encaminhado para exame, aguardando na recepção) (realizam exames previos a consulta)
		* 2 cliques no horario livre
			* localizar paciente
			* preencher exames (nome do requisitante, procedimento)
			* preencher agendamento (procedencia, forma agendamento)
			* classificação - agendado
		* btn dir> alterar status agenda > confirmada
		* btn dir> alterar status paciente > Aguardando na recepção
		* btn dir> gerar/consultar atendimento - permite abrir a função entrada unica do paciente para abrir o atendimento
			* alterar tipo atendimento para Externo
		* btn dir> gerar/consultar oftalmologia
			* abre a função oftalmologia
				* informar o tipo de consulta

# Oftalmologia - (ADM) Cadastros e parametros
* Cadastros
	* Função cadastros gerais
		* aplicação principal>medico>acuidade visual - tipos de acuidade visual conforme os valores
		* aplicação principal>medico>categorias das lentes de contato - tipo de categoria das lentes para selecionalas durante o registro
		* aplicação principal>medico>cores das lentes de contato
		* aplicação principal>medico>descrição lentes de contato - descreve qual o tipo de lente de contato utilizado, possibilita incluir marcas de lente, apresenta as varias opções de lentes definidas pela instituição
		* aplicação principal>medico>diagnósticos oftalmo - permite def diagnostimo medico de rotina, vincular ao cid 10, seq de apresentação, vincular a um grupo
		* aplicação principal>medico>lentes de contato - definir a lente conforme o nome de apresentação que está relacionada a um valor expecifico como: curva d base, grau, material, modelo, tipo, categori, etc. Também é possivel deixar sem preenchimento para o profissional preencher no atendimento
		* aplicação principal>medico>tipos de lentes de contato - 
		* aplicação principal>medico>tipo de processos oftalmologicos - MAIS IMPORTANTE, identificado no mapeamento onde será informado a maneira de trabalho
			* aba tipos de processos oftalmologicos (ex. Primeira consulta, receita, retorno, cirurgia, exame)
			* aba item da oftalmologia por tipo de processo - definir tipos de item serão apresentados nessa primeira consulta (ex. diagnostico, receita, conduta, evoluções, exame ocular exteno, fundoscopia)
			* **pode ser realizado pea recepcionista ou pelo profissional, auxilia na personalização do procedimento medico)
		* aplicação principal>medico>imagens da oftalmologia (titulo da imagem e o nome do arquivo, é possivel desenhar sobre ela ao utilizar, ou seja, apresenta a estrutura do olho para o medico marcar para auxiliar no diagnostico, necessário jpg)
		* aplicação principal>medico>oftalmologia ritual
			* aba oftalmologia ritual(consulta)
			* aba itens do ritual da oftalmologia(anamnese inicial, atestado, consentimento)
			* ação do item no ritual da oftalmologia (gerar novo registro, ou inserir texto padrao da instituição)
		* aplicação principal>medico>retorno padrão da oftalmologia (avaliação de exames, exames de rotina, consulta de rotina) informa dias de retorno, seq de apresentação
		* aplicação principal>medico>status da consulta oftalmologica - status para a consulta (aguardando anamnese, em andamento,) (definir nome, cor, seq apresentação, modif ao gerar uma consulta, modif ao finalizar uma consulta, executar a agenda, gerar alta, abrir tela de pacientes em consulta, liberar avaliações)
		* aplicação principal>oftalmologia>regra de consistencias da oftalmologia - informações de sql que serão vinculadas para startar a mensagem desejada (ex para finaliza a oftalmologia é necessario liberar a biometria) (campos momento, mensagem, forma de consistir, sql)
	* função Administração do sistema > Oftalmologia
		* aba Perfil
			* aba Cadastro > Médico oftalmo
			* aba itens Oftalmologia
				* itens relacionados a tabela do pep (registro de consentimento, receita, exames da oftalmologia, etc)
				* item agrupamento (dica de agrupamento relacionado a oftalmologia)
				* editar item ( pode informar o item, descrição da instituição, item superior (permite informar um agrupamento), seq apresentação, 
				* dica - Auto refração
				* editar exame acuidade visual - campos "apresentar inativos", "apresenta pasta "visao" no item"(permite informar se o recurso visual será posicionado na aba), "visao pelo paciente"(ativação da visao atraves do historico do paciente, ou seja, visualizar registros anteriores pelo paciente, caso desmarcado, será visualizado pelo historico atual do paciente), "questionar lib texto/medic padrao"(apresentação de um questinamento após a finalização deste item)
					* abaixo, grid itens liberados para visão (define quais itens serão visualizados no historico do paciente ou historico atual), ou seja, enquanto o medico estiver fazendo o lançamento do item, ex. cuidade visual, estará tendo a aba visão ao lado com os intes informados aqui (ex. Anamnese inicial, diagnostico, fundoscopia, etc)
	* função Administração do sistema > Aba Parametros > Aba Funções > item Oftalmologia (existem 134)
		* parametro 4 - pasta(aba) padrão para salvar as imagens (é importante definir o caminho nos padroes da instituição, são imagens ja editadas para o paciente
		* parametro 7 - permite utilizar a opção "Gerar oftalmologia" - visa beneficiar de acessar o pront no numero de atend do paciente para gerar uma consulta para registrar informações para o paciente
		* parametro 10 - importar diagnosticos para EUP após salvar o registro de diagnostico na oftalmologia (importante para pacientes ambulatoriais)
		* parametro 17 - pemite visualizar a pasta(aba) "Diasgnosticos familiares"
		* parametro 20 - Abrir a tela de "pacientes em consulta" ao entrar na função (ao acessar a função oftalmologia)
		* parametro 22 - exibir o item "Agenda Consulta" - se o médico deseja visualizar o item dentro da oftalmologia
		* parametro 23 - Questionar se deseja finalizar a consulta ao sair da função
		* parametro 29 - Exibir o item Minhas Agendas
		* parametro 41 - Item que o sistema deve posicionar após localizar o paciente
		* parametro 48 - Padrão para nomenclatura dos arquivos de imagem (nome paciente + sequencia ou sequencia do exame)
		* parametro 56 - Codigo das agendas liberadas para visualização no item "Minhas agendas" (define os códigos que serão liberados)
		* parametro 64 - Opção de seleção padrão ao dar nova receita (ex, campo padrao cliente (texto padrao da instituição, medicamentos, meus textos padrão, texto de rotina)
		* parametro 67 - Visualizar os anexos na pasta(aba) "Anexos"
		* parametro 69 - Permite visualizar a pasta "Foto do exame" no item "Anexos" - sem ter que ir em cada exame do usuario
		* parametro 74 - Destacar itens que possuem imagens vinculadas
		* parametro 81 - Modo de visualização na arvore (destacar itens do tipo da consulta, exibir itens do tipo consulta, exibir somente itens com registro apos consulta finalizada) - 
		* parametro 85 - Exibir o item Agenda cirurgia
		* parametro 86 - Exibir o item Agenda exames
		* parametro 95 - Permite gerar oftalmologia sem atendimento informado
		* parametro 99 - Exibir agendamentos do paciente ao registrar nova cirurgia na pasta Cirurgias - 
		* parametro 122 - utilizar o recurso de "Visao" dos itens da consulta oftalmologica * IMPORTANTE
		* parametro 129 - Na anamnese inicial, registrar as alergias de modo estruturado
	* função Administração do sistema > Aba Parametros > Aba Funções > Item agenda de consultas (existem 482)
		* parametro 20 - Permite gerar consulta oftalmo - opção de botão direito
		* parametro 230 - Status a ser atribuido ao agendamento ao gerar oftalmologia
		* parametro 345 - Permite utilizar a opção Consultar resumo da oftalmologia - opção de btn dir
		* parametro 401 - Após a geração do atendimento gerar a consulta oftalmologica
		* parametro 407 - Permite utilizar a chamada Oftalmologia - opção de botão direito
	* função Administração do sistema > Aba Parametros > Aba Funções > Item agenda de exames
		* parametro 48 - Permite gerar consulta oftalmo - opção de botão direito
		* parametro 369 - Após a geração do atendimento gerar a consulta oftalmologica
		* parametro 370 - Permite utilizar a opção Consultar resumo da oftalmologia - opção de btn dir
	* função Administração do sistema > Aba Parametros > Aba Funções > Item Gestão da agenda cirurgica
		* parametro 248 - Permite gerar consulta oftalmo - opção de botão direito
		* parametro 655 - Permite chamar a função Oftalmologia - opção de botão direito
		* parametro 688 - Após a geração do atendimento gerar a consulta oftalmologica
		
# Oftalmologia principais ações da agenda de consulta
* função agenda de consultas
	* Aba agenda de consultas 
		* campo agenda - selecionar a agenda do profissional
		* campo Apresentação (opções Agenda ou diaria)
		* 2 cliques no horario para agendar
			* localizar paciente (internado ou não)
			* pessoa de contato
			* status
			* convenio
			* categoria
			* plano
			* tipo acomodação
			* Sala
			* setor
			* requisitante (profissional que esta solicitando e realizando a ação)
			* indicação
			* procedencia
			* tipo midia
			* Forma agendamento
			* especialidade
			* SALVAR
		* Abaixo, incluir exames adicionais
			* procedimento/exame
		* btn dir > gerar/consultar atendimento
			* abre a EUP para abrir o atendimento
		* btn dir > vincular/desvinsular atendimento - opções
		* btn dir > exibir lista de atendimentos - opções
		* btn dir > verificar agendamentos paciente - opções
		* btn dir > gerar/consultar oftalmologia - gera um processo oftalmologico para o cliente
			* abre a função oftalmologia
				* Aba consultas
					* pode redefinir o tipo de consulta
					* pode definir o status
				* Aba historico de status
				* Aba Historico de saude
				* Aba alerta
				* pode selecionar os itens a esquerda de acordo com o que irá realizar
				* poderá fechar sem finalizar a consulta
		* btn dir > chamadas externas > oftalmologia - opções (abre a função oftalmologia)
		* btn dir > Consultar resumo oftalmologia - opções
		* btn dir > registrar controle de visita
		* btn dir > gerar plantoes a partir da agenda

# Oftalmologia principais ações da pré-consulta
* função Oftalmologia
	* Item Agenda de consulta (lat esquerda) - Realizar as principais ações do profissional de enfermagem, realizar o atendimento de pacientes, realizar exames antes da consulta
		* Aba agenda de consulta
			* 2 cliques no horario para realizar registros no prontuario
				* primeiro item da arvore
					* aba consulta
						* btn dir > gerar oftalmologia
							* na arvore a esquerda é possivel visualizar os itens que foram cadastrados para o perfil de enfermagem nos cadastros gerais da adm do sistema
								* nesse caso Pre-consulta - enfermagem e exames que serão necessarios antes do atendimento.
							* btn dir > proximo item - vai para o proximo item da arvore
							* btn dir > item anterior - vai para o item anterior da arvore
							* btn dir > gerar nova prescrição
							* btn dir > paciente em consulta - define que o paciente foi encaminhando para consulta
							* btn dir > visualizar/ocultar recurso da visao - 
							* btn dir > finalizar oftalmologia - exceto quando o paciente estiver realizando os exames
							* btn dir > iniciar oftalmologia
							* btn dir > excluir oftalmologia
							* btn dir > chamadas > prescrição protocolo ou laudo paciente
							* btn dir > visualizar/ocultar avisos - apresentado no canto inferior da tela
							* btn dir > todas do paciente - atendimento
							* btn dir > trocar o usuario
							* alterar o campo tipo de consulta e o status (ex.: consulta e em exame)
					* Aba historico de status
					* Aba historico de saudo do paciente - atraves dos registro realizados anteriormente
					* Aba alerta - será exibido ao abrir o registro do paciente
						* btn di > liberar alerta
				* item Pre consulta > Historico de saude
					* Aba Alergia/reações adversas
					* Aba Doenças previas e atuais
					* Aba Medicamentos em uso
					* Aba habitos
					* Aba cirurgias
					* etc
				* item Pre consulta > Evoluções - *Nao obrigatorio
					* definir tipo Enfermagem oftalmo e texto ou inserir texto padrão da instituição
					* btn dir>liberar item evolução
				
				* item Exames > Auto refração
					* é possivel gerar receita
				* item Exames > Tonometria pneumatica
				* item Exames > Tonometria de aplanação
				* após, o paciente estará liberado para ser encaminhando para o atendimento

# Oftalmologia principais ações da agenda de Exames
* função agenda de exames
	* Aba agenda de exames -PRINCIPAL
		* 2 cliques no horario para agendar
			* localizar paciente
			* dados do conveio; 
			* Exame (vincular o exame que será realizado)
			* CID, Profissionais, Autorização, Anestesia, setor (para o paciente), Forma agendamento
			* SALVAR
		* btn dir > gerar/consultar atendimento - ja abre a função Oftalmologia
			* abre a EUP para abrir o atendimento
		* função Oftalmologia 
			* item Agenda de exame - permite somente a visualização da agenda
		
		* btn dir > gerar/consultar oftalmologia - gera um processo oftalmologico para o cliente - caso a opção não definida não abra a janela de oftalmologia
			* abre a função oftalmologia
		* btn dir > Gerar/consultar FANEP

# Oftalmologia principais ações da gestão da agenda cirurgica
* função gestão da agenda cirurgica
	* Aba dados
		* 2 cliques no horario para agendar
			* localizar paciente (podem estar internados ou não)
		* btn dir > gerar agenda atendimento
			* abre tela para localizar o atendimento do paciente
			* completar com as informações
				* autorização, carater, status, classificação, dados de convenio
				* Procedimento
				* descrição, lado
				* cirurgião
				* anestesista
				* reserva leito, clinica
				* SALVAR
		* btn dir > gerar atendimento
			* Abre a função EUP para gerar o numero do atendimento - já abre a função Oftalmologia (depende do parametro)
				* pode alterar o tipo de consulta e o status e SALVAR
				* btn dir > gerar oftalmologia
				* btn dir > iniciar oftalmologia
				* btn dir > excluir oftalmologia
				* btn dir > chamadas > prescrição protocolo
				* btn dir > gerar nova prescrição
		* btn dir > gerar encaixe atendimento
		* btn dir > gerar encaixe
		* btn dir > gerar cirurgia e prescrição
			* abre a função Gestao de cirurgias
				* Aba Cirurgia
					* pode inserir mais dados como: potencial de contaminação, porte, estado fisico, finalidade, peso, dt inicio previso e duração previsa
					* SALVAR
					* btn dir > inicio cirurgia
		
		* btn dir > gerar/consultar oftalmologia
		* btn dir > chamadas > oftalmologia
		
		* btn dir > gerar/consultar atendimento - ja abre a função Oftalmologia
			* abre a EUP para abrir o atendimento
		* função Oftalmologia 
			* item Agenda de exame - permite somente a visualização da agenda
		
		 - gera um processo oftalmologico para o cliente - caso a opção não definida não abra a janela de oftalmologia
			* abre a função oftalmologia
		* btn dir > Gerar/consultar FANEP
