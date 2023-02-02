# Gestão de cirurgias HTML5
* Objetivos
  * registrar os executores e participantes dos procedimentos
  * Gerenciar eventos relacionados as cirurgias, desde o tempo cirurgico ao tipo de anestesia, planejar e acompanhar as necessidades antes, durante e depois do procedimento
  * Realizar o lançamento dos insumos utilizados durante o procedimento

* Principal interação - Gestão da agenda cirurgica

# Sequencia
* Função - gestão de cirurgias
	* cbx - pacientes em sala (pacientes que estão com cirurgias em execução)
	* cbx - cirurgias finalizadas (pacientes que estão com cirurgias finalizadas)
	* cbx - agenda cirurgica (todas as cirurgias agendadas na função agenda cirurgica)
		* Obs: gerar numero da cirurgia e prescrição para o paciente (geralmente feito 1 dia antes da cirurgia para a farmacia separar os materiais e insumos a serem utilizados, podendo antecipar faltas, garantindo a segurança do paciente)
		* filtrar pela agenda de amanha
		* btn dir > Gerar cirurgia e prescrição
			* Obs: Caso tenha algum paciente agendado para hoje porém a recepção não conseguiu gerar antes o atendimento para ela, clicar com btn dir> Gerar/Consultar atendimento
				* Abrirá a função Entrada unica do paciente e gerará o numero do atendimento
		* clicar no botão "Ir para cirurgia"
			* 2 cliques no nome do paciente
				* aba Farmacia > itens previstos e não previstos para a cirurgia, materiais especiais, utilizados, devoluções e lançamento automatico
					* item Previsto> Em caso de um procedimento novo que não tem kit atrelado, btn dir > Kit > kit materiais
					* item Previsto> para lançamentodo itens, btn dir > consistir por codigo de barras
					* item Materiais especiais>
		* inicio da cirurgia, btn dir > Gerar/Consultar Atendimento
		* clicar no botão "Ir para cirurgia"
			* cbx Dados cirurgicos
				* btn dir > Status de cirurgia > iniciar cirurgia
				* 2 cliques no atendimento para mais informações
					* aba farmacia
						* dispensar material adicional, btn dir > adicionar material por barras
						* devolução, btn dir> devolução de materiais
						* ao final do procedimento a farmacia irá atender a prescrição, btn dir > atender a prescrição (dando baixa dos itens na conta do paciente)
						* **obs.:** para itens não atendidos, o sistema informará, na coluna motivo baixa, como 'Prescrição incorreta'
					* aba administrativo enfermagem (pode adicionar Procedimentos adicionais, procedimento executado, participantes, conjuntos(de cme), tempos (tempo cirurgico ex.: anestesista, preparação da sala), prescrição de equipamento, observação)
						* item participantes - pode informar participantes para cada procedimento ou, caso houver somente um, informar direto os participantes
					* Aba anatomia patologica
					* Aba consulta historico
				* btn dir > Status de cirurgia > Finalizar cirurgia
					* o sistema também traz como opção Interromper cirurgia, Desfazer inicio da cirurgia
				
					
# Gestão de cirurgias - MP
* objetivos
	* permitir registrar as informações relaciadas a cirurgia executada, assim como os itens utilizados durante o procedimento
* Fluxograma
	* Atendimento > Registro do inicio da cirurgia > lançamentos > registro do fim da cirurgia
* Conceito
	* Registrar os dados ca cirurgia
	* Registrar o lancamento de materiais utilizados durante o procedimento
* Função
	* Gestão de cirurgias
		* Aba Cirurgia > Novo
			* btn dir > iniciar cirurgia
			* btn dir > finalizar cirurgia
		* Aba Farmacia (pode lançar por kit ou individual, realizar devoluções, )
			* Atender a prescrição para baixar no estoque e na conta do paciente - btn dir> atender a prescrição
		* Aba Administrativo/enfermagem
			* sub aba Procedimentos adicionais previstos
				* btn dir > realizar procedimentos previstos (para vincular os procedimetnos executados e as outras abas)
			* executados, participantes e conjuntos



# Gestão de cirurgias - ADM
* ligado a area Assistencial
* Caracteristicas
	* Gerenciar eventos relacionados a cirurgias
	* Fazer o lançamento dos materiais consumidos na cirurgia
	* registrar os executores do procedimento
* Fluxo de atividades
	1. Cadastros basicos (salas cirurgicas - func Estrutura de atendimento, Shift+F11 ou cadastro de exames e procedimentos internos, cad de materiais, cad de PJ)
	2. Abertura de atendimento 
	3. Gestão da cirurgia (lançamento de profissionais, proced)
	4. Lançamento materiais e medicamentos
	5. Fechamento da cirurgia
* Principais integrações
	* Exames e procedimentos internos - ajuda no lançamento de informações para cirurgias, ou antes no agendamento como materiais especificos, equipamentos, etc
	* Gestão da agenda cirurgica - visualizar mapa de procedimentos
	* Conta Paciente

* Cadastros gerais CIH - Tipos de cirurgias
	* funções cadastros ou shift+F11 > Controle de infecção hospitalar > Cadastros gerais > CIH - Tipo de cirurgia (classifica os tipos de cirurgias, ex.: limpa, contaminada,etc)
* Exames e Procedimentos internos
	* função Exames e Procedimentos internos (permite cadastrar a cirurgia facilitando o codigo do procedimento e os itens que serão utilizados, cme, opme
		* campos
			* Utilização proced - Cirurgico
			* Kit
			* Classificação
			* porte
			* proced cih
		* Aba Equipamentos, conjutos CME, opme, tempos, orientações, procedimentos, consentimentos, salas, serviços
* Gestão da agenda cirurgica
	* função Gestão da agenda cirurgica (horarios marcados para cirurgia, pode lançar equipamentos, cme, opme, etc)
		* sala cirurgica é cadastrada na função Estrutuda de atendimento
* Gestão de CME
	* função Gestão de CME (ciclos, adm de conjuntos, estoque)
* Gestão de cirurgias (função)
	* Aba Gestão
		* Aba Pacientes (mostra o paciente que ja estão em sala e finalizadas)
		* Aba Agenda cirurgica (verificar as agendas, para aparecer aqui é necessário, na função de gestão da agenda cirurgica, abrir registro para o paciente internado ou não, informar dados e procedimento) e pode ver procedimentos adicionais
			* btn dir 
				* Gerar encaixe
				* Travar usuario (caso necessario sair da frente do sistema sem precisar fecha-lo)
				* adicionar materiais por barra
				* gerar uma cirurgia e prescrição
				* vincular atendimento
				* consistir por codigo de barras (para lançar os materiais que realmente foram para a cirurgia, para verificar os materiais disponibilizados)
				* desvincular atendimento
			* 2 cliques no registro vai para a Aba Cirurgia para preencher os dados necessarios ou somente confirmar
				* a partir dai aparece na aba Pacientes da Aba gestão
				* btn dir > iniciar cirurgia
				* btn dir > desfazer inicio da cirurgia
				* btn dir > interromper a cirurgia
				* btn dir > desfazer a interrupção a cirurgia e refaze-la ou estornar a interrupção cirurgia
				* btn dir > localuzar pelo numero da prescrição
				* btn dir > cancelar cirurgia
				
	* Aba Cirurgia para preencher os dados necessarios ou somente confirmar
		* btn dir > finalizar a cirurgia (após isso, fará o atendimento da prescição em mat previstos)
	
	* Aba Farmacia
		* Aba mat e med previstos (pode adicionar)
			* btn dir > adicionar materiais por barras
			* btn dir > devolução de materiais
			* btn dir > consistir por codigo de barras (geralmente antes do inicio da cirurgia)
			* btn dir > excluir itens não consistidos
			* btn dir > excluir itens gerados
			* btn dir > kit de materiais
			* btn dir > excluir kit
			* btn dir > kit de estoque (kit montado dentro da função adm de estoque)
			* btn dir > kit de procedimento (de acordo com o cadastro de exames e procedimento internos, lançara o kit cadastrado nele)
			* btn dir > visualizar kit (visualizar a composição)
			* btn dir > definir convenio (do material, para ser pago pelo convenio)
		* aba mat especiais (pode gerar a prescrição de acordo, pode fazer o lançamento dos mat e med, com o material cadastrado na autorização)
			* pode consultar o saldo do material lançado
			* btn dir > liberar a prescrição
			* btn dir > atender prescrição
		* aba Mat e med utilizados (serão apresentados apos o atendimento da prescrição para os especiais, para os previstos, aparecerão após a devolução dos não utilizados e finalização da cirurgia e atendido a prescrição)
	
	* Aba Administrativo/enfermagem
		* Aba procedimentos adicionais (pode acrescentar)
			* btn dir > realizar todods os procedimentos previstos (para aparecer na aba procedimentos executados
		* Aba procedimentos executados (é gerado a partir da aba anterior, taxas)
		* Aba participantes (por procedimento ou não)
		* Aba conjuntos (conjuntos utilizados dentro da cirurgia que passa pela cme (bisturi, afastador, etc))
		* Aba prescrição de equipamentos









