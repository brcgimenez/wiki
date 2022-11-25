# Trilha entrada única de pacientes

## Entrada Única de Pacientes (Conceitual)

**Objetivos do modulo de atendimento**

* Destina-se ao atendimento pacientes, incluindo sua entrada, o acompanhamento da sua movimentação e seu processo de alta. Dá visão geral da ocupação da instituição, bem como gerencia todas as vagas existentes;
* permite mais agilidade no atendimento do paciente;
* disponibiliza informações, em tempo real, da ocupação hospitalar, visando otimizar a utilização dos leitos;
* eficiencia na gestão de movimentações e altas de pacientes, facilitando a localização dos pacientes.

**Recursos existentes**

* registrar os pertences do pacientes na entrada de um setor ou leito, controlando suas devoluções/
* realizar reserva de leitos, bem como gerenciar lista de espera para internação;
* disponibiliza formas de cadastro de paciente completo e simplificado;
* registrar atendimentos de pacientes internados, ambulatoriais e pa;
* permite cadastro de vários endereços para o paciente;
* disponibiliza recurso para "ocultar" pessoas, se necessário, como por exemplo, celebridades ou por solicitação da justiça;
* no atendimento permite identificar: procedência do paciente; clínica; caráter de atendimento; pessoa que indicou

**Fluxo de atividade**

* cadastros gerais > abertura do atendimento > controle da ocupação > registro das movimentações > alta

**Principais integrações**

* ocupação hospitalar;
* pertences do paciente;
* movimentação de pacientes
* conta paciente

## Entrada Única de Pacientes - Cadastros e parâmetros (ADM)

**Entrada única de pacientes**

* Pertence ao módulo de Recepção e Internação, sendo módulo associado a área de Atendimento do sistema;
* na abertura do atenidmento podemos informar o motivo do atendimento, tipo de atendimento, clínica do atendimento, procedência do paciente, forma de chegada do paciente,
médico responsável pelo atendimento, dados do convênio como categoria e plano, setor de atendimento e em casos de atendimentos realizados a execução de exames é possível informar
o exame a ser realizados
* permite fazer o cadastro de alertas, registro de troca de médico responsável, disgnostico, declaração de óbito, dados da funerária, etc.

**Cadastros apresentados e tabela que precisa estar liberada para o usuário**

**Cadastros - shift+f11**

* Aplicação principal > Médico > Classificação da atuação do médico no atendimento (MEDICO_CLASSIF_ATEND)
	* classificação que o médico vai assumir no atendimento
	
* Aplicação principal > Médico > Topografia (Corpo Humano) (TOPOGRAFIA_DOR)
	* topografia da lesão

* Aplicação principal > Recepção > Classificação de cuidados especiais ao paciente (CLASSIF_ESPECIAL_PACIENTE)
	* tipos de cuidados especiais com o paciente, ex.: deficiencia fisica, mental, etc.

* Aplicação principal > Atendimento > Classificação dos atendimentos (CLASSIFICACAO_ATENDIMENTO)
	* tipo de atendimento ex.: consulta, exames, cirurgico, ambulatorial, pa, etc
	* associado tem a liberação das classificacoes do atendimento e liberação por convenio que podem usar essa classificação cadastrada
	
* Aplicação principal > Atendimento > Forma de chegada do paciente (FORMA_CHEGADA)
	* Ambulancia, bombeiro, propriea, pc, pm, pr, uti movel, etc
	
* Aplicação principal > Atendimento > Informações sobre o atendimento (INFORMACAO_ATENDIMENTO)
	* Particular, gravidade, origem, acidente
	
* Aplicação principal > Atendimento > Locais de destino ao informar saída real (LOCAL_DESTINO_SAIDA_REAL)
	* para quando ha alta, pode utilizar o recurso para registrar a saida real apos paciente ter esperado no quarto pelo fechamento da conta, ex.: residencia, consultorio, outro hospital
	
* Aplicação principal > Atendimento > Tipos de lesão (TIPO_LESAO_ATEND)
	* profunda, superficial, ucera de pressao, etc
	
* Aplicação principal > Atendimento > Triagem classificatória de prioridade (TRIAGEM_CLASSIF_PRIORIDADE)
	* idoso, gestante, normal, crianca < 5 anos, deficientes fisicos
	* pode dar valor a prioridade (quanto menor mais alta prioridade), cor, sexo, idades, tempos para atend
	

* Aplicação principal > Laudos > Forma de entrega de laudos (FORMA_ENTREGA_LAUDO)
	* ex.: paciente vai retirar, pela internet
	* pode definir regra ajuste data entrega - tempo previsto e estimado para entrega do laudo
	

* Aplicação principal > Cadastros pessoas > Grau Parentesco (GRAU_PARENTESCO)
	* para quando tem que informar responsável ou visitante/acompanhante
	

* Aplicação principal > Cadastros Atendimento > Localizações dos setores (PA_LOCAL)
	* pode ser usado para gestao de senhas, exames
	* regra de cor tempo - para quando atingir o tempo especifico, ficará o registro da cor informada
	* liberacao dos locais - para perfil
	* tem flag "Exige informacao do tempo", quando usado esse setor, pede para informar quanto tempo o paciente ficará nesse setor
	* campo local - utilizado para map de setores
	
* Aplicação principal > Cadastros Atendimento > Grupos de localizações dos setores (PA_GRUPO_LOCAL)
	* utilizado nas localizações dos setores
	* pode informar o controle (indivial, coletivo ou captacao)
	* relacionado aos grupos no cadastro de localizações
	
* Aplicação principal > Cadastros Atendimento > Motivo do atendimento (QUEIXA_PACIENTE)
	* aba clinica - de acordo com o motivo de atendimento (cirurgia, obstetricia)
	* aba liberacao triagem - perfil, setor
	* aba tiss tipo atendimento
	
* Aplicação principal > Cadastros Atendimento > Procedência (PROCEDENCIA)
	* informa de onde o paciente está vindo
	* aba regra de liberação das procedências - restringir por setor, perfil ou tipo atendimento
	
* Aplicação principal > Cadastros Atendimento > Status do paciente no PA (PA_STATUS_PACIENTE)
	* ex.: aguardando na recepcao, em medicacao, reavaliacao, liberacao enfermagem
	
* Aplicação principal > Cadastros Atendimento > Tipos de acidente (TIPO_ACIDENTE)
	* ex.: transito, trajeto, trabalho
	* aba tiss - tipo acidente
	
* Aplicação principal > Cadastros Atendimento > Tipos de indicação (TIPO_INDICACAO)
	* ex.: amigo, empresa, familiar, medico, revista
	* pode marcar para informar a pessoa que indicou, o tipo de mídia
	* aba regra de exibição tipo de indicação
	
* Aplicação principal > Cadastros Atendimento > Tipos de alertas (TIPO_ALERTA_ATEND)
	* isolamento, aleta de exame executado, paciente recebeu contraste
	* aba liberação - por perfil, setor, especialidade, funcao, pessoa
	

* Aplicação principal > Enfermagem > Triagem classificatória de risco (TRIAGEM_CLASSIF_RISCO)
	* emergencia, muito urgente, urgente, pouco urgente, nao urgente
	* define prioridade, cor, cor fonte
	* Aba regra da triagem de risco - liberação por setor

* Função Administração do sistema
	* aba parametros
		* aba funções
			* Entrada Única de pacientes -> precisa liberar alguns parametros, filtrar por 'tria', 'class%atend', 'locali', 'status', 'per%alerta', para conseguir utilizar no atenidmento ao paciente
			
			

## Entrada Única de Pacientes - Internação (MP)

**Objetivos**

* detina-se ao atendimento do paciente, fazendo o registro da sua entrada na instituição
* Permite flexibilidade e produtividade através de uma ferramenta de atendimento altamente parametrizavel
* possibilita eficiencia e maior numero de informações do paciente de forma centralizada

**Fluxograma**

* necessidade do registro do atendimento do paciente
* definição dos dados do atenidmento
* definição do convenio do paciente
* definição do setor de atendimento do paciente
* acomodação do paciente

**Conceito**

* Tipo de atendimento: ambulatorial, externo, internação e PS
* Integração com modulos de Autorização de Convênio, Administração de Contratos e Convênio e Particular
* Agilizar o processo de cadastro da pf nos casos de registro de informações em processo muito dinamicos, como o ps por exemplo

**Função**

* Função Entrada Unica de pacientes
	* Localizar atendimento -> Duplo clique no campo atendimento, abre modal com setores e acomodações ou clicar em localizar e informar algum dos filtros
	* Novo atendimento -> Clicar na lupa, localiza o paciente pf (abre o cadastro simplificado da pessoa para preenchimento dos dados se necessário), retorna para tela da entrada unica,
	registrar os dados do atendimento do paciente parte superior(motivo, tipo atend,clinica,procedencia, forma, medico, carater atend, tipo acidente, responsável, convênio, sintoma,classificação, senha, forma de entrega do laudo);
	parte central vinculado ao tipo de convenio; parte inferior setor e unidade de atendimento (setor, unidade, acomodação)
		* Aba serviços
			*Abas acomodação paciente, alertas, procedimento cih, lançamento automatico, SAME (local de armazenamento), troca medico atendimento, questionario, declaração de obito, cronico (periodo), doação (quais orgaos se for doador),
			Documentação, serviços paciente (que queira utilizar), avaliação do atendimento, serviços de terceiro, indicações
		* Aba Cadastro paciente
		* Aba Diagnostico
		* Aba histórico de saude
			* abas alergia/reações adversas, habitos e vicios, medicamentos em uso, doenças previas e atuais, cirurgias, ocorrencias, restrições, acessório/ortese/protese, deficiencia
		* Aba profissionais -> que estarão envolvidos no atendimento e funções desses
		* Aba Pagador
		* Aba informações adicionais
			* Abas convenio, sac, dados do atendimento, biometria, foto, histórico do atendimento
		* Aba anexos

## Entrada Única de Pacientes - Registro Atendimento Ambulatorial e Externo (MP)

**Conceito**

* pertence ao modulo de recepção e internação sendo este modulo associado a área de Atendimento do sistema
* paciente de ambulatorio -> paciente que, após ser registrado ou matriculado num estabelecimento de saúde, recebe assistencia ambulatorial. 
  O mesmo que paciente externo, esse tbm usado para pequenas cirurgias e/ou coleta de exames laboratoriais

**Registrando atendimento ambulatorial e externo**

* Função Entrada Unica de pacientes
	* Novo atendimento -> Clicar na lupa, localiza o paciente pf (abre o cadastro simplificado da pessoa para preenchimento dos dados se necessário) ou criar um novo, retorna para tela da entrada unica,
	registrar os dados do atendimento do paciente parte superior(motivo, tipo atend, clinica, procedencia, forma, medico, carater atend, tipo acidente, responsável, convênio, sintoma,classificação, senha, forma de entrega do laudo);
	parte central vinculado ao tipo de convenio; parte inferior setor e unidade de atendimento (setor, unidade, acomodação)
			* informações da prescrição sobre o exame que irá realizar (formas de entrega do laudo, dados da prescricao, senhas)
		* Aba Exames/Proced
			* Aba exames, laboratório, passagem setor, avaliação -> estão na parte inferior da tela -> F3 ou btn dir para liberar a prescrição
			* ctrl+alt+s ou btn dir -> verificar e emitir a senha para o paciente acessar o resultado online
		* Aba serviços
			*Abas acomodação paciente, alertas, procedimento cih, lançamento automatico, SAME (local de armazenamento), troca medico atendimento, questionario, declaração de obito, cronico (periodo), doação (quais orgaos se for doador),
			Documentação, serviços paciente (que queira utilizar), avaliação do atendimento, serviços de terceiro, indicações
		* Aba Cadastro paciente
		* Aba Diagnostico
		* Aba profissionais -> que estarão envolvidos no atendimento e funções desses
		* Aba anexos


## Entrada Única de Pacientes - Registro Atendimento Internado e PS (MP)

**Conceito**

* pertence ao modulo de recepção e internação sendo este modulo associado a área de Atendimento do sistema
* paciente internado -> é aquele que admitido no hospital, passa a ocupar um leito por período acima de 24hs.
* paciente PS -> é aquele paciente com ou sem risco de vida, cujo agravos à saúde necessitam de atendimento imediato. Funciona 24hrs do dia e dispõe apenas de leitos de observação.

**Registrando atendimento internado e ps**

* Função Entrada Unica de pacientes
	* Novo atendimento -> Clicar na lupa, localiza o paciente pf (abre o cadastro completo da pessoa para preenchimento dos dados se necessário) ou criar um novo, retorna para tela da entrada unica,
	registrar os dados do atendimento do paciente parte superior(motivo, tipo atend, clinica, procedencia, forma, medico, carater atend, tipo acidente, responsável, convênio, sintoma,classificação, senha, forma de entrega do laudo);
	parte central vinculado ao tipo de convenio; parte inferior setor e unidade de atendimento (setor, unidade, acomodação)
			* informações da prescrição sobre o exame que irá realizar (formas de entrega do laudo, dados da prescricao, senhas)
		* Aba Exames/Proced
			* Aba exames, laboratório, passagem setor, avaliação -> estão na parte inferior da tela -> F3 ou btn dir para liberar a prescrição
			* ctrl+alt+s ou btn dir -> verificar e emitir a senha para o paciente acessar o resultado online
		* Aba serviços
			*Abas acomodação paciente, alertas, procedimento cih, lançamento automatico, SAME (local de armazenamento), troca medico atendimento, questionario, declaração de obito, cronico (periodo), doação (quais orgaos se for doador),
			Documentação, serviços paciente (que queira utilizar), avaliação do atendimento, serviços de terceiro, indicações
		* Aba Cadastro paciente
		* Aba Diagnostico
		* Aba profissionais -> que estarão envolvidos no atendimento e funções desses
		* Aba anexos
