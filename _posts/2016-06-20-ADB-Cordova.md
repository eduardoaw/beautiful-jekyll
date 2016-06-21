---
layout: post
title: Montando um ambiente para depurar aplicativos Android desenvolvidos com Apache Cordova
---
<a href="#cordova-android-adb">
	<img src="/img/posts/adb-cordova/cordova_android_adb.jpg" style="float:right;margin-left:15px;max-width:300px" class="img-thumbnail img-responsive" alt="Cordova + Android ADB">
</a>

<a href="#_" class="lightbox" id="cordova-android-adb">
	<img src="/img/posts/adb-cordova/cordova_android_adb.jpg" class="img-thumbnail" alt="Cordova + Android ADB">
</a>

Se você chegou até aqui é porque esta usando o **Cordova** para desenvolvimento de aplicativos móveis
e deve estar impressionado com seu poder de desenvolvimento. É muito legal mesmo ver o código **JS/HTML**
rodando em forma de um aplicativo, mas o que você irá ver aqui irá lhe deixar
ainda mais impressionado. Estou falando sobre a facilidade de depurar a sua aplicação. 

Mas o que torna isto tudo tão simples? 
A resposta é simples! **ADB**!

**ADB** ou Android Debug Bridge é uma ferramenta que permite a comunicação
com emuladores e dispositivos físicos Android, é executada via linha de comando e esta presente
no SDK Android que é o Kit de desenvolvimento de aplicações Android,
e pode ser encotrada em `<sdk android>/platform-tools/`.

Para que **ADB** funcione ao seu favor algumas configurações devem ser feitas:
	
A primeira é ativar o Modo Desenvolvedor em seu dispositivo Android, para isto vá nas configurações e verifique se já existe o menu **Opções do desenvolvedor**, caso não exista vá até o menu **Sobre o telefone/tablet** e dê 7 cliques sobre o menu **Número da versão**, isto irá habilitar o menu **Opções do desenvolvedor**.
	
Conecte o seu dispositivo no seu computador utilizando o cabo USB.

<a href="#depurar-usb">
	<img src="/img/posts/adb-cordova/depurar_usb.jpg" class="img-thumbnail img-responsive center-block" alt="Depurar USB">
</a>
<a href="#_" class="lightbox" id="depurar-usb">
	<img src="/img/posts/adb-cordova/depurar_usb.jpg" class="img-thumbnail" alt="Depurar USB">
</a>

Em **Opções do desenvolvedor** localize por **Depuração USB** e ative-a. Com isto será gerado um aviso **Permitir a depuração USB?**. Fica a seu critério marcar ou não a opção **Sempre permitir a partir deste computador**, eu sempre marco. 
Clique em OK para finalizar.
	
<blockquote><p>Este reconhecimento pode demorar em algumas situações, caso não ocorra verifique se os drivers usb do dispositivo estão instalados em seu computador.</p></blockquote>
	
O próximo passo é adicionar **ADB** em suas variáveis de ambiente. 
A imagem abaixo demonstra o que deve ser feito.
	
<a href="#adb-variavel-ambiente">	
	<img src="/img/posts/adb-cordova/adb_variavel_ambiente.JPG" class="img-thumbnail img-responsive center-block" alt="Variáveis de Ambiente ADB">
</a>
<a href="#_" class="lightbox" id="adb-variavel-ambiente">
	<img src="/img/posts/adb-cordova/adb_variavel_ambiente.JPG" class="img-thumbnail" alt="Variáveis de Ambiente ADB">
</a>

<blockquote><p>O guia foi desenvolvido utilzando sistema operacional Windows, com o sdk android para Windows.</p></blockquote>
		
Com ADB em suas variáveis de ambiente você já está pronto para usá-la!
	
Use o comando `adb devices` para listar o seu dispositivo. Na imagem abaixo é possível observar o meu dispositivo foi identificado por um número serial `C4F12A612FC621F`, se pra você também apareceu um serial está tudo ok até aqui.

<a href="#adb-devices-install">
	<img src="/img/posts/adb-cordova/adb_devices_install.JPG" class="img-thumbnail img-responsive center-block" alt="ADB devices install">
</a>
<a href="#_" class="lightbox" id="adb-devices-install">
	<img src="/img/posts/adb-cordova/adb_devices_install.JPG" class="img-thumbnail" alt="ADB devices install">
</a>	
	
Vá até o seu projeto cordova e de um `build`. Com o build finalizado irá gerar o `android-debug.apk` que está localizado em 
`<seu projeto cordova>`
`/platforms/android/build/`
`outputs/apk/`
	
O comando `adb install android-debug.apk` irá mover e também realizar uma nova instalação do instalador gerado, caso deseje sobrepor uma instalação existente adicione o comando -r,	desta forma `adb install -r android-debug.apk`.

Abra o navegador Google Chrome e digite no campo da url `chrome://inspect`

<a href="#chrome-inspect">	
	<img src="/img/posts/adb-cordova/chrome_inspect.JPG" class="img-thumbnail img-responsive center-block" alt="Chrome Inspect">
</a>
<a href="#_" class="lightbox" id="chrome-inspect">
	<img src="/img/posts/adb-cordova/chrome_inspect.JPG" class="img-thumbnail" alt="Chrome Inspect">
</a>
		
Localize seu aplicativo e clique em inspect e sua aplicação estará disponível para ser depurada.
	
<a href="#debugg-application">	
	<img src="/img/posts/adb-cordova/debugg_application.JPG" class="img-thumbnail img-responsive center-block" alt="Chrome Debugger">
</a>
<a href="#_" class="lightbox" id="debugg-application">
	<img src="/img/posts/adb-cordova/debugg_application.JPG" class="img-thumbnail" alt="Chrome Debugger">
</a>

Incrível né! Você poder depurar seu aplicativo que está rodando no seu dispositivo físico utilizando seu navegador, sem dúvidas uma ótima ferramenta para melhorar a sua produtividade no desenvolvimento de aplicativos.
	
ADB possuí ainda outras funcionalidades e você pode encontrá-las [aqui](https://developer.android.com/studio/command-line/adb.html) 
	
Se ficou com alguma dúvida ou tem alguma sugestão deixe seu comentário abaixo.
