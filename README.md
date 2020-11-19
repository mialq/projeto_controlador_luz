# projeto_controlador_luz
Este artigo descreve o projeto de Controlador de Luz, desenvolvido para auxiliar no controle de lâmpadas uma vez que possibilita o ajuste preciso de luminosidade da mesma.
Introdução

	Com o desenvolvimento das áreas de Computação, Engenharia, Matemática, Mecatrônica e o surgimento da IoT, podemos observar a evolução de ideias que modifica o dia a dia das pessoas e dos ambientes. Através da tecnologia de IoT podemos transformar coisas e objetos para facilitar a vida das pessoas, sociedade e do mundo.
Pensando em melhorar o ambiente desenvolvi um projeto de Controlador de Luz Remoto usando Arduino UNO. Esse projeto partiu da necessidade de modificar a intensidade de luz do ambiente, como sala de televisão. Utilizando um Arduino UNO genérico, sensores, atuadores, potenciômetro virtual, controle remoto, computador, foi possível desenvolver o sistema para controle de luz remoto, onde através do controle remoto, envio mensagem ao sensor de infravermelho que está conectado através de pinos de alimentação e portas analógicas do Arduino, que emite um sinal para o node-red, onde em seu fluxo ascende as luzes no máximo. Através do protocolo MQTT que está rodando em um servidor broker do Mosquitto e com isso o mesmo acontece na lâmpada controlada remotamente. Desenvolvimento de Dashboard para controle de intensidade, monitor de potência e histórico de uso, Comunicação de rede para replicação dos controles da luz e Dashboard monitorando potência da luz remota. 
Para controlar o liga e desliga de dispositivos como lâmpadas, normalmente utilizamos módulos relés, por exemplo, que executam este papel de forma satisfatória, nesse trabalho não foi utilizado módulos relés, porém, para projetos mais sofisticados eles são usados.
A luminosidade específica deste sistema para deixar a luz um pouco mais fraca ou um pouco mais forte é o uso do potenciômetro virtual para controle de intensidade.

. Materiais e Métodos
Apresentação Geral
Hardware
•	Arduino UNO genérico placa de interface baseada em microcontrolador;
•	LEDs – Verde/Amarelo
•	Resistores de 270 ohm
•	Controle Infravermelho
•	Celular
•	Computador
•	Protoboard
•	Fios de conexão – jumpers
O projeto conta com sensor infravermelho para captar comando de desligar a luz, potenciômetro virtual para controle de intensidade, dashboard para controle de intensidade, monitor de potência e histórico de uso, comunicação de rede para replicação dos controles da luz e dashboard monitorando potência da luz remota.
Software
Precisamos carregar o sketch StandardFirmata no software do Arduino. Esse sketch vem como exemplo quando você instala o ambiente do Arduino, portanto podemos carrega-lo utilizando o menu arquivo – exemplo – firmata – StandardFirmata, como mostrado na figura1-4
 
Figura1.1

Passos da instalação dos softwares
Passo 1 – Instalação da IDE do Arduino (https://www.arduino.cc/en/software)
Passo 2 – Instalação de correção de drivers do Arduino Genérico (https://drive.google.com/file/d/0B2YXepPR2qlAdkR6eXNDMVU3a0E/view)
Passo 3 – Carregar o Exemplo StandardFirmata no UNO pelo IDE
Passo 4 – Instalação do Servidor MQTT Mosquito (https://mosquitto.org/download/)
Passo 5 – Criação do servidor MQTT
	Acessar Prompt de Comando.
	Acessar a pasta onde o Mosquitto foi instalado (Ex: C:\Program Files\mosquitto)
	Executar o comando de criação: “mosquitto -v”
Passo 6 – Criação do servidor MQTT
	Acessar Prompt de Comando.
	Acessar a pasta onde o Mosquitto foi instalado (Ex: C:\Program Files\mosquitto)
	Executar o comando de criação de tópico: “mosquitto_sub -h localhost -p 1883 -t “NOME DO SERVIÇO””
Passo 7 – Criação do servidor MQTT
	Acessar Prompt de Comando.
	Acessar a pasta onde o Mosquitto foi instalado (Ex: C:\Program Files\mosquitto)
	Executar o comando de publicação do tópico: “mosquitto_pub -h localhost -p 1883 -t “NOME DO SERVIÇO”
Passo 08 – Instalar o NODE-RED no Windows
Primeiramente instalar o node.js - https://nodejs.org/dist/v12.16.2/node-v12.16.2-x64.msi
após essa etapa abrir o prompt de comando e digitar prompt de comando do Windows e deve-se digitar (sem aspas) “npm install -g –unsafe-perm node-red” para que a instalação seja realizada.
Para acessar a ferramenta, deve-se abrir novamente o prompt de comando do Windows e digitar node-red.
Em seguida, é necessário abrir o navegador e digite o seguinte endereço: localhost:1880
Passo 09 – Instalar no celular o aplicativo MQTT Dash (https://play.google.com/store/apps/details?id=net.routix.mqttdash&hl=pt_BR&gl=US)
Passo 10 – Configurar o Brocker no aplicativo. (IP da máquina do Mosquito, Porta do Mosquito, padrão 1883 e o nome do tópico publicado no mosquito (Ex.: LED)
Incluir os botões de controle de potência e liga e desliga (Range e Switch) conforme configurando o tópico. Ex.: LED.

Funcionamento Do Mqtt No Sistema Controlador De Luz 

O MQTT é um protocolo de mensagens leve, criado para comunicação M2M (Machine to Machine). Este é um dos protocolos mais usados para dispositivos embarcados. Uma comunicação MQTT é composta das seguintes partes: há publishers (quem irá disponibilizar informações), subscribers (quem irá receber as informações) e Broker (servidor MQTT, na nuvem/ acessível de qualquer lugar do mundo que contenha conexão com a Internet). Teoricamente, não há limite especificado de subscribers e publishers em uma mesma comunicação MQTT, pois o limite nesse aspecto é do servidor em lidar com as conexões. 
Sem entrar no mérito da especificação do protocolo MQTT uma mensagem MQTT publicada/enviada possui duas partes importantes: Tópico – “chave” /identificação da informação publicada. É usado para direcionar a informação publicada/enviada a quem assina (quem “dá subscribe”) no tópico. O tópico consiste de uma string (por exemplo: MQTTTesteTopico); Payload – informação que deseja enviar (propriamente dita). Um publisher, conectado ao Broker (servidor MQTT), envia/publica as informações em um dado momento. Os subscribers, assim como os publishers, também estão conectados aos brokers e “escutando” mensagens trafegadas com o tópico-alvo. Quando uma mensagem com o tópico alvo é publicada, automaticamente são direcionadas aos subscribers. Dessa forma, uma solução em IoT que usa MQTT possui somente um servidor (Broker), sendo todo o restante composto de clients MQTT. Importante lembrar é que um mesmo client MQTT pode ser subscriber e publisher de diversos tópicos.
Quando estiver construindo projeto com Arduino, deverá utilizar cabo USB entre o computador e o Arduino para baixar os programas para a placa. Os programas são instalados no microcontrolador.Foi utilizado energia do computador para alimentar a placa do Arduino através do cabo USB.

