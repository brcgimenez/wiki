# Prontuário Eletrônico do Paciente - PEP - Item Eventos (HTML5)
* Conceitos (segurança do paciente e evento(incidente))
	* Redução do risco de dados desnecessarios associados a assitencia em saude até o minimo aceitavel (segundo ONS)
	* Redução de atos inseguros nos processos assistenciais + uso das melhores praticas = segurança e melhores resultados
	* segurança do paciente
		* item do pep onde os profissionais que atuam na assistencia ao paciente podem registrar quaisquer eventos/incidentes que ocorram com o mesmo
		* importante instrumento no cuidado, visto que as informações registradas poderão ser utilizadas para melhoria de processos internos
		* promover qualificação nos processos de cuidados
		* permite consultar as informações sempre que necessários

* tipos de eventos
	* classificação incidentes
		* near miss (ou quase falha) - incidente que não atingiu o paciente (unidade de sangue conectada no paciente de forma incorreta antes da administração ou o mesmo na adm de medicação)
		* incidente sem dano - evento que atingiu o paciente, mas não causou dano (med que foi adm na dose incorreta mas não manifestou reação)
		* incidente com dano (evento adverso) - resulta em dano ao paciente (infusão da unidade de sangue errada onde o paciente vai a obito )

* grau de dano
	* leve - sintomas leves, danos minimos ou moderados de curta duração (sem intervenção ou intervenção minima)
	* moderado - paciente sintomatico, necessidade de intervenção, prolongamento da internação, perda de função permanente ou em longo prazo
	* grave - paciente sintomatico, necessidade de intervenção para suporte de vida, diminuição da expectativa de vida, com grande dado ou perda de função permanente ou de longo prazo
	* obito - evento causou ou acelerou a morte

* função pep
	1. localizar paciente
	2. Na arvore do prontuario > item Eventos
		* adicionar Evento > Aba Eventos (campo: registrir visualização do evento (será exibido somente ao usuario que informou e os gerentes, qualidade), setor, profissional, evento (tipo de evento ocorrido com o paciente, ex.: queda), classificação(tipos de evento), gravidade(grau de dano), detalhamento(descrição breve previamente cadastrada), Descrição do evento (mais importante, possibilita com btn dir o texto padrão da instituição ou do profissional - cadastros pep), Ação imediata, observação)

** Será analisado pelo setor de qualidade para melhoria dos processos**

# Gestao da qualidade - eventos do paciente
* função gestao da qualidade (relacionada ao itens do evento)
* cbx Eventos do paciente
	* cbx Questoes
		* Pode adicionar eventos da mesma forma como foi feito pelo PEP
	* btn dir
		* justificar nao abertura da não conformidade do evento
		* gerar nao conformidade evento
		* gerar questoes do evento
		* cancelar evento do paciente
		* desfazer analise
		* registrar analise
	* 2 cliques no registro
		* lat dir > cbz questoes (cadastros gerais > tipos de evento)
			* btn dir > retgirar questoes do evento
		* cbx Anexos
		* cbx Avaliação (cadastros gerais > tipos de evolução)
			* lat dir > apuração
		* cbx Historia
		* cbx Informações adicionais
		* cbx Ficha flebite (sera apresentado tambem no pep
	* cbx Não conformidade
		* Aba Analise de problemas
			* lat dir > criterios (gravidade e urgencia) - parametro 62 para definir a ferramente da analise de problemas
		* Aba nao conformidade
