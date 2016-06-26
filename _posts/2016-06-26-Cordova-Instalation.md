---
layout: post
title: Instalando o ambiente de desenvolvimento de aplicativos Apache Cordova
---

<a href="#cordova">
	<img src="/img/posts/install-cordova/cordova.png" style="float:right;max-height:230px;margin-left:15px" class="img-thumbnail img-responsive" alt="Cordova Devices">
</a>
<a href="#_" class="lightbox" id="cordova">
	<img src="/img/posts/install-cordova/cordova.png"  class="img-thumbnail" alt="Cordova Devices">
</a>

[Apache Cordova](https://cordova.apache.org/) é um popular framework de desenvolvimento de aplicativos móveis, que permite a desenvolvedores de software construir aplicações para dispositivos móveis usando CSS3, HTML5 e JavaScript em vez de depender de APIs de plataforma específicas como Android, iOS ou Windows Phone. 
	
Você já deve ter se perguntado, desenvolvo meu aplicativo com **Cordova** ou [PhoneGap](http://phonegap.com), se sim considere ler [7 Things to Consider When Making iOS and Android Apps with Cordova or PhoneGap](http://www.addthis.com/blog/2014/10/27/7-things-to-consider-when-making-ios-and-android-apps-with-cordova-or-phonegap/#.V2vysvkrJxA) para tirar esta dúvida. O texto também abrange informações sobre dispositivos e sistemas operacionais suportados, é uma boa leitura antes de começar.

Ao final do texto deste tutorial você estará apto a criar sua primeira aplicação, com uma instalação "limpa", usando somente **Cordova**, sem a necessidade de instalação de IDEs ou ferramentas auxiliares para isto.
	
Para realizar os passos de instalação, assume-se que você esteja usando **Windows 7** ou superior. 
	
Outro requsito é ter alguma experiência com o **Prompt de comando** do Windows (Menu iniciar > Executar > cmd), além de saber como adicionar **variáveis de ambiente**. Se variáveis de ambiente lhe é estranho, te explico na imagem abaixo como configura-las.
	
<a href="#var-ambiente">
	<img src="/img/posts/install-cordova/variaveis-ambiente.jpg" class="img-thumbnail img-responsive" alt="Variáveis de Ambiente Windows">
</a>
<a href="#_" class="lightbox" id="var-ambiente">
	<img src="/img/posts/install-cordova/variaveis-ambiente.jpg" class="img-thumbnail" alt="Variáveis de Ambiente Windows">
</a>

<blockquote><p>Menu iniciar > Computador > Propriedades > Configurações avançadas do sistema > Variáveis de ambiente > Localizar Path (Se não existir crie um novo) > Editar/Novo > Valor da variável > Endereço do executável separado por ; </p></blockquote>
	
Sempre que solicitado para adicionar variáveis de ambiente volte a este tópico.
	
Esta [questão](http://pt.stackoverflow.com/questions/5024/como-mudar-o-path-nos-windows) em Stackoverflow pode lhe tirar mais dúvidas sobre, caso ainda tenha alguma.  
	
<h3>Instalação Cordova</h3>
	
<h4>Node.js</h4> 
	
**Cordova** é executado na plataforma **Node.js**, que precisa ser instalado como o primeiro passo.	Baixe o instalador em http://nodejs.org e execute-o.
	
Verifique se o **Node.js** está instalado em seu sistema, abrindo uma nova janela do **prompt de comando** e digitando `node --version`.
	
<a href="#install-node">
	<img src="/img/posts/install-cordova/node-version.jpg" class="img-thumbnail img-responsive" alt="Instalação Node.js">
</a>
<a href="#_" class="lightbox" id="install-node">
	<img src="/img/posts/install-cordova/node-version.jpg" class="img-thumbnail" alt="Instalação Node.js">
</a>
	
<blockquote><p>No momento que escrevo este tutorial a verão é 4.4.4, note que a versão Node.js pode ser maior para você.</p></blockquote>
	
Caso `node --version` não retorne o número da versão, verifique se o caminho de Node.js que no meu caso é `C:\Program Files\nodejs` está em suas **variáveis de ambiente**. 
	
<h4>Git</h4>
**Git** é um sistema de controle de versão e é utilizado por Cordova por "trás das cortinas". Faça o download em [http://git-scm.com](http://git-scm.com) e instale-o seguindo as configurações padrões que são recomendadas durante a instalação.
	
<h4>NPM</h4>
**Cordova** está disponível no **NPM(Node Package Manager)**, instale-o através do comando `npm install -g cordova`.
	
Ao final verifique se **Cordova** está instalado em seu sistema, abra uma nova janela do **prompt de comando** e digite `cordova --version`.
	
Se você vê a versão de cordova está tudo ok.
	
<h3>Instalação de dependências Cordova</h3>
	
<h4>Apache Ant</h4>
	
[Apache Ant](http://ant.apache.org) é um sistema de compilação **Java**, que é usado por **Cordova** e o **SDK do Android**.
	
Baixe-o em [http://ant.apache.org/bindownload.cgi](http://ant.apache.org/bindownload.cgi), localize o link para baixar pesquisando por `apache-ant-1.9.7-bin.zip` (A versão poderá ser maior no momento em que está lendo este tutorial).
	
Descompacte o arquivo zip baixado em `C:\Program Files (x86)` e em seguida adicione **Ant** em suas variáveis de ambiente, no meu caso é `C:\Program Files (x86)\apache-ant-1.9.7\bin`.
	
Verifique se `ANT_HOME` está em suas variáveis de ambiente, caso não, adicione com o caminho da instalação **Ant**, que no meu caso é `C:\Program Files (x86)\apache-ant-1.9.7`.
	
Abra uma nova janela do **prompt de comando** e digite `ant -version`, se você vê a versão de **Ant** está tudo ok. 
	
<h4>Java</h4> 
	
Para rodar o **Android SDK** que será visto no próximo passo é necessário instalar JDK(Java Development Kit) Java em seu sistema.

Se você já possuí a JDK instalada(com versão maior ou igual 1.6)  passe para o próximo passo, caso não, baixe em [www.oracle.com/technetwork/java/javase/downloads/](www.oracle.com/technetwork/java/javase/downloads/) e em seguida instale seguindo as configurações padrões da instalação.
		
Após instalada verifique a sua versão abrindo uma nova janela do **prompt de comando** e digitando `javac -version`.
	
<a href="#javac-version">
	<img src="/img/posts/install-cordova/javac-version.jpg" class="img-thumbnail img-responsive" alt="Javac Version">
</a>
<a href="#_" class="lightbox" id="javac-version">
	<img src="/img/posts/install-cordova/javac-version.jpg" class="img-thumbnail" alt="Javac Version">
</a>
	
Caso não retorne a versão, adicione o caminho de instalação java + pasta bin nas suas **variáveis de ambiente**, que no meu caso é `C:\Program Files\Java\jdk1.8.0_91\bin`.

Verifique se `JAVA_HOME` está em suas **variáveis de ambiente**, caso não, adicione com o caminho da instalação **Java**, que no meu caso é `C:\Program Files\Java\jdk1.8.0_91`.
	
<h4>Android SDK</h4>
	
**Android SDK** é usado por **Cordova** para construir aplicativos **Android**.
	
Baixe o instaldor do **SDK** em [https://developer.android.com/sdk](https://developer.android.com/sdk) (Cuidado, **Android** deseja que você instale a sua própria IDE **Android Studio** e não é isto o que queremos para este tutorial, por isto o link do SDK pode parecer um pouco escondido, para localiza-lo vá até a parte de baixo da página).
	
Durante a instalação o instalador irá lhe perguntar se deseja instalar **Android SDK** para o seu usuário ou para todos usuários.
	
Fica desta forma o local de instalação dependendo do que selecionar:
Seu usuário > `C:\Users\eduardo\AppData\Local\Android\android-sdk` 
Todos usuários > `C:\Program Files\Android\android-sdk`

No meu caso optei pela instalação para o meu usuário, desta forma, os caminhos que devo colocar em minhas **variáveis de ambiente** são estes: `C:\Users\eduardo\AppData\Local\Android\android-sdk\tools` e `C:\Users\eduardo\AppData\Local\Android\android-sdk\platform-tools`.
	
<blockquote><p>O caminho do tutorial foi gerado na minha máquina, use o caminho do Android SDK que foi gerado na sua ;)</p></blockquote>
	
Abra uma nova janela do **prompt de comando** e digite `android`, em seguida deverá abrir o **Android SDK**.
	
Na seção `Tools` selecione a versão mais recente de `Android SDK Tools`, `Android SDK Platform-tools` e `Android SDK Build-tools`.
	
No momento que escrevo este tutorial **Android 6.0 (API 23)** é a API mais recente e recomendada por cordova, selecione-a também e em seguida instale.
	
E chegamos ao fim da instalação, agora você já é capaz de criar um aplicativo utilizando o **Cordova**.
	
<h3>Criando seu primeiro aplicativo</h3>
	
Diz a lenda que quando estamos aprendendo uma coisa nova devemos fazer um exemplo HelloWorld antes de qualquer coisa. Há algumas pessoas que ainda dúvidam disto [Você acredita na maldição/lenda do "Olá Mundo"?](https://br.answers.yahoo.com/question/index?qid=20140805161003AAKccK5) ^^
	
Na via das dúvidas vamos criar um HelloWorld para compreender como funciona o processo de criação de um aplicativo **Cordova**.

Primeiro abra uma nova janela do prompt de comando e digite o comando `cordova create hello com.example.hello HelloWorld`.
	
Cordova irá criar a pasta hello que consiste no parametro que vem após `create` do comando digitado anteriormente. Observe a estrutura criada (imagem abaixo), a pasta `www` contém os arquivos HTML, CSS e JS em uma estrutura na qual você já deve estar acostumado a ver em projetos Web.
	
<a href="#new-project">
	<img src="/img/posts/install-cordova/new-project.JPG" class="img-thumbnail img-responsive" alt="New Project Cordova">
</a>
<a href="#_" class="lightbox" id="new-project">
	<img src="/img/posts/install-cordova/new-project.JPG" class="img-thumbnail" alt="New Project Cordova">
</a>

O próximo passo é adicionar uma plataforma na qual o aplicativo irá executar depois de compilado, no caso adicionaremos Android. Faça isto executando o comando `cordova platform add android`.
	
Com a plataforma adicionada estamos prontos para compilar o nosso primeiro aplicativo. Faça isto executando o comando `cordova build`.
	
O primeiro build é normal demorar um pouco, poís é necessário baixar o **Gradle** que consite em um sistema avançado de automatização de builds que une o melhor da flexibilidade do **Ant** com o gerenciamento de dependencias e as convenções do **Maven**.
	
Ao final do build teremos o **.apk** que é o instalador do seu aplicativo localizado em `<seu projeto> \platforms\android\build\outputs\apk` 

<a href="#cordova-platform">
	<img src="/img/posts/install-cordova/cordova-platform.JPG" class="img-thumbnail img-responsive" alt="Cordova Platform">
</a>
<a href="#_" class="lightbox" id="cordova-platform">
	<img src="/img/posts/install-cordova/cordova-platform.JPG" class="img-thumbnail" alt="Cordova Platform">
</a>
	
Transfira o instalador para o seu dispositivo e execute-o, caso solicitado habilite a instalação de fontes desconhecidas.
	
Você também pode executar seu aplicativo em um emulador em sua máquina, para isto execute o comando `cordova emulate android`
	
<a href="#cordova-emulate">
	<img src="/img/posts/install-cordova/cordova-emulate.JPG" class="img-thumbnail img-responsive" alt="Cordova Emulate">
</a>
<a href="#_" class="lightbox" id="cordova-emulate">
	<img src="/img/posts/install-cordova/cordova-emulate.JPG" class="img-thumbnail" alt="Cordova Emulate">
</a>
	
<blockquote><p>A menos que você tenha um super computador eu não aconselho emular aplicativos, poís é muito lento. Indico utilizar o seu dispositivo fisíco para isto.</p></blockquote>
	
Se você chegou até aqui, recomendo seguir um outro tutorial que fiz, [Montando um ambiente para depurar aplicativos Android desenvolvidos com Apache Cordova](https://eduardoaw.github.io/2016-06-20-ADB-Cordova/) em que mostro como facilitar o processo de instalação e depuração de aplicativos feitos com **Cordova**.

E é isto, caso tenha alguma dúvida ou sugestão comente abaixo.
	
<b>Fontes</b>
[Apache Cordova](https://cordova.apache.org/).
[Apache Cordova, Create your first app](https://cordova.apache.org/docs/en/latest/guide/cli).
[EVO Things, Installing Cordova on Windows](https://evothings.com/doc/build/cordova-install-windows.html).
[Adriano Lisboa, Afinal de contas, o que é o gradle e como usá-lo?](http://adrianolisboa.com/afinal-de-contas-o-que-e-o-gradle-e-como-usa-lo/).
