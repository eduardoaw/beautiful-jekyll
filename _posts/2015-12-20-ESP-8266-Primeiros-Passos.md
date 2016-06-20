---
layout: post
title: ESP8266 Primeiros Passos
---

<img src="/img/posts/esp8266-intro/esp8266.jpg" style="float:right;max-height:230px;margin-left:15px" class="img-thumbnail img-responsive" alt="ESP8266">
No primeiro artigo desta página, falo sobre as primeiras experiências que tive com o módulo WiFi **ESP8266**, que para ser mais preciso é uma interface WiFi com suporte ao protocolo **TCP/IP** e serve para prover conectividade à microcontroladores, IoT e etc...

Este módulozinho me chamou atenção desde a primeira vez que o vi e das coisas que mais gostei nele foram, seu tamanho reduzido frente a outras opções de conectividade disponíveis e principalmente seu preço que é bem acessível. 

Agora vou demonstrar como utilizar o **ESP8266** em conjunto com o **Arduino UNO** utilizando comandos **AT**, mas esta não é a única forma de utilização deste módulo, uma vez que o mesmo possuí um pequeno processador interno que pode ser programado para operar de forma independente e também possuí um par de [portas GPIO](https://pt.wikipedia.org/wiki/General_Purpose_Input/Output) que permitem controlar outros dispositivos. Atualmente existem trabalhos na comunidade para utilizar o ESP8266 [sem o arduino](http://nodemcu.com/index_en.html), mas isto é assunto para outros artigos. (Interessou-se sobre este assunto? Já pode adicionar [isto](https://www.sparkfun.com/products/9873) a sua lista de desejos!)

<h3>Ligação entre Arduino e ESP8266</h3>

Muita atenção nesta parte, poís, o ESP8266 utiliza apenas **3,3v** para alimentação e I/O. Já o arduino utiliza **5v** nos seu pinos de I/O e se você tentar conecta-lo diretamente, na melhor das hipóteses, pode simplesmente não funcionar e na pior poderá causar danos ao módulo ESP8266. Para contornar isto será necessário o desenvolvimento de um [divisor de tensão](https://en.wikipedia.org/wiki/Voltage_divider) para baixar os 5v do Arduino para os 3,3v suportados pelo ESP8266. Já vi alguns tutoriais que dispensam o uso do divisor de tensão ou ainda que usam os 3,3v do próprio arduino, eu sei que é frustrante chegar aqui e ter que adquirir mais alguns itens e isto pode demorar dias... Aconteceu comigo também, fique a vontade para fazer suas experiências, sempre levando em consideração que isto pode ser fatal para o seu ESP8266.

<img src="/img/posts/esp8266-intro/espconnection.jpg" style="float:left;margin-right:15px" class="img-thumbnail img-responsive" alt="ESP8266 Conexão">

A conexão do ESP8266 não serve em uma protoboard, resolvi isto soldando alguns jumpers para facilitar o manuseio, como mostra a imagem ao lado.

O consumo de corrente é ponto a ser observado, ESP8266 pode consumir até **250mA** e isto pode ser muito para o Arduino conseguir alimenta-lo. Foi o que aconteceu no meu caso, tive que adquirir uma fonte de **12v x 500mA** e um **adaptador de alimentação 3,3v/5v para protoboard** como [este](http://www.usinainfo.com.br/fontes-e-reguladores/fonte-ajustavel-para-protoboard-33v-e-5v-2537.html), para fazer tudo funcionar corretamente. 

E ai está a ligação do ESP8266 com o Arduino!

<img src="/img/posts/esp8266-intro/esparduinoconnections.jpg" class="img-thumbnail img-responsive center-block" alt="ESP8266 Ligação">

Você pode verificar o esquema de ligação com mais detalhes [aqui](https://github.com/eduardoaw/eduardoaw.github.io/blob/master/files/esparduinofritzing.jpg).

<h3>Programa</h3>

Com a ligação pronta mãos a massa no código! Depois de uma hora coçando a cabeça e tentando fazer ESP8266 comunicar com o arduino utilizando tutoriais que encontrei pela internet, percebi que precisava fazer o básico! Que é uma simples comunicação **RX/TX** utilizando um terminal serial, que pode ser encontrado na IDE do Arduino (Serial Monitor - Símbolo de uma pequena lupa no canto superior direito). Para isto desenvolvi este programa que é pequeno e de fácil entendimento. 

{% highlight c++ linenos %}
#include <SoftwareSerial.h>

SoftwareSerial ESP(2, 3); //RX | TX

void setup() { 
                      //baud rate = 9600, 57600 or 115200
  Serial.begin(9600);
  ESP.begin(9600); 
}

void loop() {
  
  if (ESP.available()) {
    char response = ESP.read();
    Serial.print(response);
  }
  
  if (Serial.available()) {  
    char command = Serial.read();
    ESP.print(command);
  }
}
{% endhighlight %}

O código utiliza a Biblioteca [SoftwareSerial](https://www.arduino.cc/en/Reference/SoftwareSerial) que foi desenvolvida para permitir a comunicação serial em outros pinos digitais do Arduino, além do 0 e 1 que possuem suporte embutido para comunicação serial. Isto facilita o upload do código da IDE para o Arduino e evita problemas como [este](http://stackoverflow.com/questions/23433513/avrdude-stk500-getsync-not-in-sync-resp-0x00-arduino), ao mesmo tempo que deixa as portas 0 e 1 livres para fins de depuração. No nosso projeto os pinos 2 e 3 serão utilizados para a conexão RX/TX do ESP8266.

Na função `setup()` do código declaro `ESP.begin(9600);` ou seja, [`baud rate`](https://en.wikipedia.org/wiki/Baud) `= 9600`, mas dependendo da versão do firmware do ESP8266 a taxa de transmissão pode ser `9600, 57600 ou 115200`. 

Dentro do `loop()` temos uma estrutura de código que permite digitar um comando na janela do Serial monitor e envia-lo ao ESP8266 com `ESP.print(command);` e receber a resposta ao comando com `ESP.read();`.

O gif abaixo mostrar como operar o Serial Monitor na IDE do Arduino.

<img src="/files/git_at_esp8266.gif" class="img-thumbnail img-responsive center-block" alt="Serial Monitor operação">

<h3>Comandos AT do ESP8266</h3>

Esta tabela de comandos AT reúne quase todos os comandos disponíveis para ESP8266, caso queira uma mais completa acesse [aqui](https://cdn.sparkfun.com/assets/learn_tutorials/4/0/3/4A-ESP8266__AT_Instruction_Set__EN_v0.30.pdf), porém, seja cauteloso, alguns destes comandos podem ser prejudiciais ao seu ESP8266 se não usados corretamente.

<img src="/img/posts/esp8266-intro/atcommandsesp.jpg" class="img-thumbnail img-responsive center-block" alt="ESP8266 Ligação">

<h3>Testando comandos AT</h3>

Usando o programa criado anteriormente é possível testar os comandos AT da tabela acima, vejamos alguns.

</h4>Comandos Básicos<h4>

Para testar os comandos a seguir é importante setar os parametros `Both NL & CR` e a `baud rate` que poderá ser `9600, 57600 ou 115200`.
Para enviar o comando desejado basta preencher o campo texto da janela do Serial Monitor com o comando e após isto clicar em `Send`.

<h4>Resetando e setando o modo de operação</h4>

<img src="/img/posts/esp8266-intro/resetsetesp.jpg" class="img-thumbnail img-responsive center-block" alt="Reset e set modo de operação">

Comandos:

1. `AT+RST`
	- Aqui estou resentando o ESP8266
		
2. `AT+CWMODE=3`
	- Configurando o modo WiFi como ponto de acesso e estação
	
<h4>Conectando-se a uma rede</h4>

<img src="/img/posts/esp8266-intro/connectesp.jpg" class="img-thumbnail img-responsive center-block" alt="Conectando-se a uma rede">

Comandos:

1. `AT+CWLAP`
	- Listando redes WiFi próximas
2. `AT+CWJAP="NomeDaRede","Senha"`
	- Conectando-se a uma rede 
3. `AT+CIPSTA="192.168.1.100"`
	- Atribuindo um endereço IP válido para o ESP8266
	
<blockquote><p>Atribuir um endereço IP para o ESP8266 vai ser útil para montar um servidor TCP nos próximos passos</p></blockquote>


<h4>Conexão TCP</h4>

Para testar a conectividade do ESP8266 criei uma ferramenta chamada [Simple Socket IO](https://github.com/eduardoaw/simplesocketio) e você pode baixa-la [aqui](https://raw.githubusercontent.com/eduardoaw/simplesocketio/master/files/SimpleSocketIO.jar). Simple Socket IO é multiplataforma (para rodar basta ter o [java](https://www.java.com/pt_BR/) instalado em sua máquina) e permite criar um servidor ou cliente TCP. Sinta-se a vontade para construir sua própria implementação de um cliente/servidor em java, c++, python ou em outra linguagem.

<h4>Criando um cliente TCP para conectar-se na porta 3000 de um servidor</h4>

Escolha a opção `Server Mode` do Simple Socket IO para simular um servidor TCP, configure de acordo com a imagem e clique em `Listen`. Neste momento Simple Socket IO está pronto para receber clientes, que no nosso caso será o ESP8266. Clique no Serial Monitor da IDE do Arduino para iniciar o programa no ESP8266.

<img src="/img/posts/esp8266-intro/clienttcpesp.jpg" class="img-thumbnail img-responsive center-block" alt="Cliente TCP">

Comandos: 

1. `AT+CIPMUX=1`
	- Setando ESP8266 para multiplas conexões 
2. `AT+CIPSTART=0,"TCP","192.168.1.3",3000`
	- 1º Parâmetro id da conexão
	- 2º Parametro conexão do tipo TCP
	- 3º Parâmetro IP do computador que esta o Simple Socket IO
	- 4º Parâmetro Porta de conexão TCP
3. `+IP,0,33:Ola ESP8266! Eu sou seu servidor!`
	- Esta é uma mesagem que o ESP8266 recebeu do servidor, o comando iniciado por `+IP` indica isto
	- 1º Parâmetro id da conexão, que no caso é 0
	- 2º Parâmetro é o tamanho da mensagem vinda do servidor, que no caso é 33
	- 3º Parâmetro é a mensagem em si vinda do servidor
4. `AT+CIPSEND=0,33`
	- Este comando indica que quero enviar uma mensagem com tamanho = 33
	- O ESP8266 vai "printar" na serial o caracter `>` indicando que esta pronto para receber a sua mensagem
	- No caso digitei `Ola servidor! Eu sou seu cliente` e pressionei `Enter` para finalizar
	- A mensagem chegou no Simple Socket IO

<blockquote><p>ESP8266 permite até 4 conexões</p></blockquote>	

<h4>Criando um servidor TCP para receber conexões na porta 5000</h4>

Escolha a função Client Mode do Simple Socket IO para simular um cliente TCP, configure de acordo com a imagem, não clique em `Connect` por enquanto, primeiro temos que subir o servidor no ESP8266, faça isso clicando no Serial Monitor da IDE do Arduino e após o comando `AT+CIPSERVER=1,5000` `OK` aparecer na janela do Serial Monitor você pode dar um `Connect`.

<img src="/img/posts/esp8266-intro/servertcpesp.jpg" class="img-thumbnail img-responsive center-block" alt="Servidor TCP">

Comandos:

1. `AT+CIPMUX=1`
2. `AT+CIPSERVER=1,5000`
	- 1º Parâmetro servidor modo open
	- 2º Parâmetro receber conexões na porta TCP 5000
3. `AT+CIPSEND=0,42`
	- Este comando indica que quero enviar uma mensagem com tamanho = 42
	- O ESP8266 vai "printar" na serial o caracter `>` indicando que esta pronto para receber a sua mensagem
	- No caso digitei `Ola Simple Socket IO! Eu sou seu servidor!` e pressionei `Enter` para finalizar
	- A mensagem chegou no Simple Socket IO
4. `+IP,0,32:Ola ESP8266! Eu sou seu cliente!`
	- Esta é uma mesagem que o ESP8266 recebeu do cliente Simple Socket IO, o comando iniciado por `+IP` indica isto
	- 1º Parâmetro id da conexão, que no caso é 0
	- 2º Parâmetro é o tamanho da mensagem vinda do servidor, que no caso é 32
	- 3º Parâmetro é a mensagem em si vinda do cliente Simple Socket IO
	
<blockquote><p>Mensagens com o tamanho maior do que foi declarado no segundo parâmetro do comando AT+CIPSEND serão enviadas parcialmente</p></blockquote>


<h3>Fazendo uma coisa útil com ESP8266</h3>

Agora que já vimos com funciona a comunicação cliente/servidor e comandos AT do ESP8266 vou mudar o código do programa inicial, para que seja possível ligar um led remotamente!!!

E ai está o código desenvolvido para que o ESP8266 seja um cliente de um servidor, é possível observar que agora automatizamos o processo. Observe o comando `ESP.print("AT+CWMODE=3\r\n");` na linha 35, ele possuí a quebra de linha `\r\n` e isto deve ser usado em todos comandos feitos por ESP8266, funciona como um `Enter` que faziamos nos passos anteriores.

Copie o código abaixo direto no [repositório](https://github.com/eduardoaw/ESP8266LedControl/blob/master/ClientESP8266LedControl/ClientESP8266LedControl.ino) para garantir sempre a versão mais atual.

{% highlight c++ linenos %}
#include <SoftwareSerial.h>
#include <TextFinder.h>

SoftwareSerial ESP(2, 3); //RX | TX
TextFinder FINDER(ESP);  

const int LED_PIN =  13;

String lenght = "";
String response = "";

String nameWiFi = "Your WiFi";
String passwdWiFi = "Password WiFi";

String addrServer = "Your Server";
int portServer = 0; // Port on your server

void setup() { 
                      //baud rate = 9600, 57600 or 115200
  Serial.begin(9600);
  ESP.begin(9600); 
  pinMode(LED_PIN, OUTPUT);
  
  delay(1000);
  
  Serial.println("Booting...");
  Serial.println("Nao se esqueca de conectar em Simple Socket IO");
  
  getRet(); //Checks whether something in the buffer

  ESP.print("AT+RST\r\n");  //Reset by software
  getRet();
  delay(10000);
  
  ESP.print("AT+CWMODE=3\r\n"); //Access point and station
  getRet();
  delay(5000);
  
  String cmdConnectWiFi = "AT+CWJAP=\"";
  cmdConnectWiFi += nameWiFi;
  cmdConnectWiFi += "\",\"";
  cmdConnectWiFi += passwdWiFi;
  cmdConnectWiFi += "\"\r\n";
  
  ESP.print(cmdConnectWiFi); //Connect to WiFi network
  getRet();
  delay(5000);

  ESP.print("AT+CIPMUX=1\r\n"); //Multiple connections
  getRet();
  delay(5000);

  String cmdConnectServer = "AT+CIPSTART=0,\"TCP\",\"";
  cmdConnectServer += addrServer;
  cmdConnectServer += "\",";
  cmdConnectServer += portServer;
  cmdConnectServer += "\r\n";
  
  ESP.print(cmdConnectServer); //Connect to server
  getRet();
  
  Serial.println("Cerifique-se que Simple Socket IO aceitou a conexao \"Accepted TCP connection from...\"");
  
}

void loop() {
  
  if(FINDER.find("+IPD,")) {
     
     char aux = ESP.read(); 
     Serial.print("ID: "); 
     Serial.println(aux);

     aux = ESP.read();
     while(aux != ':') {
       if(aux != ',')
          lenght += aux;
        aux = ESP.read(); 
     }
     
     Serial.print("Size of message: ");
     Serial.println(lenght);
     for(int i = 0; i < lenght.toInt(); i++) {
       aux = ESP.read();
       response += aux;
     }
     Serial.print("Message: ");
     Serial.println(response);
     
     handleCommand(response, lenght.toInt());
     
     lenght = "";
     response = "";
  }  
}

void getRet() {
  
    delay(1000);
    while(ESP.available()) {
      char response = ESP.read();
      Serial.print(response);
    }
}

void handleCommand(String response, int lenght) {

   if(response == "L") {
     digitalWrite(LED_PIN, HIGH);
     ESP.print("AT+CIPSEND=0,9\r\n"); 
     while(!FINDER.find(">")) {
     }
     ESP.print("LED IS ON"); //If you change the return message here, remember to adjust the message size in the previous command "AT+CIPSEND=0,9" (LED IS ON = 9) ;)
   }
   else if(response == "D") {
     digitalWrite(LED_PIN, LOW);
     ESP.print("AT+CIPSEND=0,10\r\n");
     while(!FINDER.find(">")) {
     }
     ESP.print("LED IS OFF"); //If you change the return message here, remember to adjust the message size in the previous command "AT+CIPSEND=0,10" (LED IS OFF = 10) ;)
   }
   else {
     
     String command = "AT+CIPSEND=0,";
     command += 18 + lenght;
     command += "\r\n";
     
     ESP.print(command);
     while(!FINDER.find(">")) {
     }
     
     String ret = "COMMAND "; //If you change the return message here, remember to adjust the message size in the previous command "command += 18 + lenght;" (COMMAND  NOT FOUND = 18) ;)
     ret += response;
     ret += " NOT FOUND";
     
     ESP.print(ret); 
   }
}
{% endhighlight %}

Como podem observar foi necessário adicionar a biblioteca [TextFinder](http://playground.arduino.cc/Code/TextFinder).

Na linha 68 do código faço o uso de TextFinder para indentificar se `+IPD,` ocorreu na minha serial, isto indica uma mensagem vinda de outro dispositivo externo, no caso o nosso servidor. Já na linha 129 faço um while que aguarda o ESP8266 me dar o retorno `>` que indica que ele esta pronto para receber minha mensagem que será enviada ao servidor.

As mensagens que o programa atende são `L` para ligar o led e `D` para desligar o led. Qualquer outro comando enviado para o ESP8266 será ignorado, e retornará uma mensagem de comando não encontrado. 

Fiz um vídeo que mostra a execução do programa, lembrando que estou controlando o **led 13** do arduino que já vem default na própria placa.

<blockquote><p>Assita o vídeo abaixo em 720p HD para conseguir visualizar as mensagens ;) </p></blockquote>

<div class="embed-responsive embed-responsive-16by9">
	<iframe class="embed-responsive-item" src="https://www.youtube.com/embed/8saqd-_tcZw" frameborder="0" allowfullscreen></iframe>
</div>

Também fiz um exemplo em que o ESP8266 é o servidor, acesse o [repositório](https://github.com/eduardoaw/ESP8266LedControl) do projeto.

E chegamos ao final, espero que este artigo tenha sido útil, agora você pode usar este programa e adicionar outras funções, por exemplo, adicione um [DHT11](http://www.usinainfo.com.br/sensores-e-modulos/modulo-sensor-de-umidade-e-temperatura-com-jumper-dht11-2307.html) ao seu projeto e implemente o comando `T` para solicitar a temperatura ;)

Se ficou com alguma dúvida ou tem alguma sugestão deixe seu comentário abaixo.
