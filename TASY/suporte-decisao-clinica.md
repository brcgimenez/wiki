# Suporte a decisao clinica - mentor
	* para utilizar é necessário cadastrar as regras e ações no Suporte a Decisão clinica (SDC)
	* Cadastros de regras no SDC para as acções: Sinais vitais, diagnosticos, exames laboratoriais, eventos, curativos, protocolo e triagem
		* processo inicia na recepção > enfermagem > medico
		* cadastros de regras, ações e executores
		* quando o medico entrar no PEP receberá alerta do mentor, não precisando acessar o prontuário do paciente

	* Função Suporte a decisao clinica (SDC) - mentor
		* cbx - Sinais vitais
			* wbp esq
				* descrever a pendencia relacionada a regras (ex Sinais vitais e Monitorização)
			* wdbp dir - Regra (definições dos sinais vitais)
				* (ex saturação, temperatura, hipertermia)
				* obrig - descrição, sinal vital
				* campos - setor paciente, escala dor, dor, vl minimo, vl maximo, idade min, idade max, peso min e max, decisao a criterio do profissional(ele quem podera decidir se seguira com o protocolo ou não), protocolos assistenciais
				* 2 cliques
					* aba ações -> descrição, interv enfermagem (sae), cuidados (saps), prescricao protocolo, subtipo do protocolo, alertas e eventos(relacionada a funcao gestão de alertas e eventos, serve para gerar info de sms, ci e email), link, gerar acao ja liberada conforme regra, exige justificativa ao cancelar.
						* na função gestao de alertas e eventos, cbx Cadastros/eventos, cadastrar um evento e regras, no wdbp dir>aba regra de destino (ex CI)
						* 2 cliques
							* regra de executores (define qual vai ser o responsável pela ação gerada -> tipo de pessoa destino, (equipe ou especialidade ou pessoa destino)
								* influencia na função gestão da qualidade de pessoal (é onde cria os tipos de pessoa de destino)
									* shift + F11 -> cadastros gerais > Cadastros de Pessoas > equipes
								
					* aba liberação -> estabelecimento, perfil, setor usuario
					* aba Regras complementares (caso nao retorne resultado na sql, a regra de sdc nao será considerada para o atendimento) -> titulo,sql, documentação
		
		* cbx - diagnosticos
			* wdbp esq - Pendencias (Diagnostico H1N1) (sugere ou gera automaticamente o protocolo de cuidado)
			* wdbp dir - Regra -> descricao *, Diagnostico*, setor, idades, pesos, decisoes a criterio do prof, protocolos assistenciais
				* 2 cliques
					* aba ações (toda ação será vinculada na regra de executor, conforme anterior)-> descrição, interv enfermagem (sae), cuidados (saps), prescricao protocolo (diagnostico mentor), subtipo do protocolo(diagnostico gripe), alertas e eventos(relacionada a funcao gestão de alertas e eventos, serve para gerar info de sms, ci e email), link, gerar acao ja liberada conforme regra, exige justificativa ao cancelar.
						* na função gestao de alertas e eventos, cbx Cadastros/eventos, cadastrar um evento e regras, no wdbp dir>aba regra de destino (ex CI)
						* 2 cliques
							* regra de executores (define qual vai ser o responsável pela ação gerada -> tipo de pessoa destino, (equipe ou especialidade ou pessoa destino)
								* influencia na função gestão da qualidade de pessoal (é onde cria os tipos de pessoa de destino)
									* shift + F11 -> cadastros gerais > Cadastros de Pessoas > equipes
								
					* aba liberação -> estabelecimento, perfil, setor usuario
					* aba Regras complementares (caso nao retorne resultado na sql, a regra de sdc nao será considerada para o atendimento) -> titulo,sql, documentação
		
		* cbx - exames de laboratorio
			* wdbp esq - Pendencias (exames laboratoriais)
			* wdbp dir - Regra (ex potassio) (descricao, exame são obrig)
		
		* cbx - escalas e indices
			* wdbp esq - Pendencias (braden - muito elevada)
			* wdbp dir - Regra (ex braden elevada) (descricao, escala são obrig), pode selecionar score flex, resposta descritiva (quando a escala não esta relacionada a valor)
				** Ao vincular a regra aso protocolos assistenciais, nao se vincula uma ação, pois o mesmo será informado no cadastro do protocolo assistencial**
		
		* cbx - curativos
			* wdbp esq - Pendencias (estadiamento da lesao de pele)
			* wdbp dir - Regra (descricao) campo grau, valores min e max (depende do cadastro da sae de qual dos campos ira verificar)
		
		* cbx - eventos
			* wdbp esq - Pendencias (eventos assistenciais)
			* wdbp dir - Regra (evento - queda do paciente (enfermagem ou medico)) (descricao, evento) 
			
		* cbx - classificação de risco
			* wdbp esq - Pendencias (emergencia ou classificação de risco)
			* wdbp dir - Regra (protocolo atendimento) (descricao) classificação, setor, manchester-fluxograma, manchester-discriminadores
			
		* cbx - protocolos assistenciais
			* wdbp esq - Pendencias (Teste da orelhinha, protocolo glicemico, uti pacientes internados) (utilizada quando entrada do paciente em UTI, internações e RN) gerar de forma automatica a prescrição no ato da internação sem a necessidade de esperar o medico (podem ter regras vinculadas aos cadastros anteriores, para isso o check de protocolos assistenciais tem que estar marcado e não precisa ter uma ação)
			* wdbp dir - Regra (internacao protocolo) (descricao, evento (quando associados é bloqueado os campos) quantidade de regras, quantidade associados obrigatorios
				* quando protocolo glicemico (evento nascimento)
					* cadastro de protocolo, tipos de protocolo > protocolos vinculados (ex protocolo de glicemia) > sub-tipo do protocolo, marcar "Protocolo de glicemia MENTOR"
				* 2 cliques
					* Aba ações
					* Aba Regras associadas (quando ira gerar a ação)
						* (regra obrig) - horas retroativas
					* Aba liberação
			
			
			
			
			
