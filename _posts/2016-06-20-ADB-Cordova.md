---
layout: post
title: Montando um ambiente de depuração de aplicativos Android desenvolvidos com Apache Cordova
---

<img src="/img/posts/adb-cordova/cordova_android_adb.jpg" style="float:right;margin-left:15px" class="img-thumbnail img-responsive" alt="Cordova + Android ADB">
Se você chegou até aqui é porque esta usando o **Cordova** para desenvolvimento de aplicativos móveis
e deve estar impressionado com seu poder de desenvolvimento. É muito legal mesmo ver o código **JS/HTML**
rodando em forma de um aplicativo, mas o que você irá ver aqui irá lhe deixar
ainda mais impressionado. Estou falando sobre a facilidade de debugar a sua aplicação. 

Mas o que torna isto tudo tão simples? 
A resposta é simples! **ADB**!

**ADB** ou Android Debug Bridge é uma ferramenta que permite a comunicação
com emuladores e dispositivos físicos Android, é executada via linha de comando e esta presente
no SDK Android que é o Kit de desenvolvimento de aplicações Android,
e pode ser encotrada em `<sdk android>/platform-tools/`.

Para que **ADB** funcione ao seu favor algumas configurações devem ser feitas:
	
1. Ativar o Modo Desenvolvedor em seu dispositivo Android, para isto vá nas configurações e verifique se já existe o menu **Opções do desenvolvedor**, caso não exista vá até o menu **Sobre o telefone/tablet** e dê 7 cliques sobre o menu **Número da versão**, isto irá habilitar o menu **Opções do desenvolvedor**.
	
<img src="/img/posts/adb-cordova/depurar_usb.jpg" class="img-thumbnail img-responsive center-block" alt="Depurar USB">
	
2. Em **Opções do desenvolvedor** localize por **Depuração USB** e ative-a. Com isto será gerado um aviso **Permitir a depuração USB?**. Fica a seu critério marcar ou não a opção **Sempre permitir a partir deste computador**, eu sempre marco. Clique em OK para finalizar.
	
<blockquote><p>Este reconhecimento pode demorar em algumas situações, caso não ocorra verifique se os drivers usb do dispositivo estão instalados em seu computador.</p></blockquote>
	
Os próximos passos serão realizados em seu computador.
	
3. Adicione **ADB** em suas variáveis de ambiente.
	
<blockquote><p>O guia foi desenvolvido utilzando sistema operacional Windows, com o sdk android para Windows.</p></blockquote>
	
<img src="/img/posts/adb-cordova/adb_variavel_ambiente.JPG" class="img-thumbnail img-responsive center-block" alt="Variáveis de Ambiente ADB">
		
Com ADB em suas variáveis de ambiente você já está pronto para usá-la!
	
4. Use o comando `adb devices` para listar o seu dispositivo. Na imagem abaixo é possível observar o meu dispositivo identificado por um número serial `C4F12A612FC621F`, se pra você também apareceu um serial está tudo ok até aqui.

<img src="/img/posts/adb-cordova/adb_devices_install.JPG" class="img-thumbnail img-responsive center-block" alt="ADB devices install">
	
5. Vá até o seu projeto cordova e de um `build`. Com o build finalizado irá gerar o `android-debug.apk` que está localizado em `<seu projeto cordova>/platforms/android/build/outputs/apk/`.
	
6. O comando `adb install android-debug.apk` irá mover e também realizar uma nova instalação do instalador gerado, caso deseje sobrepor uma instalação existente adicione o comando -r,	desta forma `adb install -r android-debug.apk`.

7. Abra o navegador Google Chrome e digite no campo da url `chrome://inspect`
	
<img src="/img/posts/adb-cordova/chrome_inspect.JPG" class="img-thumbnail img-responsive center-block" alt="Chrome Inspect">
	
8. Localize seu aplicativo e clique em inspect.
	
<img src="/img/posts/adb-cordova/debugg_application.JPG" class="img-thumbnail img-responsive center-block" alt="Chrome Debugger">
	
Incrível né! Você pode debugar seu aplicativo que está rodando no seu dispositivo físico no navegador, sem dúvidas uma ótima ferramenta para melhorar a sua produtividade no desenvolvimento de aplicativos.
	
ADB possuí ainda outras funcionalidades você pode encontra-las [aqui](https://developer.android.com/studio/command-line/adb.html) 
	
Se ficou com alguma dúvida ou tem alguma sugestão deixe seu comentário abaixo.
	
	
	
	
