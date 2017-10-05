---
title: Creazione di un'applicazione di chat Node.js con Socket.IO in Servizio app di Azure
description: Esercitazione che illustra l'uso di socket.io in un'applicazione Web node.js ospitata in Azure.
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: e1aa539e1134884261ea7464bfda6d14815618d4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a>Creazione di un'applicazione di chat Node.js con Socket.IO in Servizio app di Azure
Socket.IO fornisce comunicazioni in tempo reale tra il server node.js e i client usando WebSocket. Supporta inoltre il fallback in altri tipi di trasporto (ad esempio il polling prolungato) che funzionano con browser precedenti. In questa esercitazione verrà illustrato l'hosting di un'applicazione di chat basata su Socket.IO come app Web di Azure e verrà indicato come ridimensionare l'applicazione tramite [Cache Redis di Azure]. Per altre informazioni su Socket.IO, vedere <http://socket.io/>.

> [!NOTE]
> Le procedure descritte in questa attività si applicano alle [app Web del servizio app]. Per Servizi cloud, vedere [Creazione di un'applicazione di chat Node.js con Socket.IO in un servizio cloud di Azure].
> 
> 

## <a name="download-the-chat-example"></a>Scaricare l'esempio di chat
Per questo progetto, verrà utilizzato l'esempio di chat dell' [archivio GitHub Socket.IO]. Eseguire la procedura seguente per scaricare l'esempio e aggiungerlo al progetto creato in precedenza.

1. Scaricare una [versione archiviata ZIP o GZ] del progetto Socket.IO (per questo documento è stata usata la versione 1.3.5)
2. Estrarre l'archivio e copiare la directory **examples\\chat** in una nuova posizione. Ad esempio, **\\node\\chat**.

## <a name="modify-appjs-and-install-modules"></a>Modificare app.js e installare i moduli
1. Rinominare il file **index.js** in **app.js**. Ciò consente ad Azure di rilevare che si tratta di un'applicazione Node.js.
2. Aprire il file **app.js** in un editor di testo. Sostituire la riga contenente `var io = require('../..')(server);` come illustrato di seguito:
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. Aprire il file **package.json** e aggiungere un riferimento a socket.io sotto `dependencies`, come di seguito indicato:
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. Dalla riga di comando passare alla directory **\\node\\chat** e usare npm per installare i moduli necessari per questa applicazione:
   
        npm install
   
    Verranno aperti i moduli in una sottocartella denominata **node_modules**.

## <a name="create-an-azure-web-app"></a>Creare un'app Web di Azure
Per creare un'app Web di Azure, abilitare la pubblicazione Git e quindi abilitare il supporto WebSocket per l'app Web, attenersi alla procedura seguente.

> [!NOTE]
> Per completare l'esercitazione, è necessario un account Azure. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">versione di valutazione gratuita di Azure</a>.
> 
> 

1. Installare l'interfaccia della riga di comando di Azure e connettersi alla propria sottoscrizione. Vedere [Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md).
2. Se si tratta della prima impostazione di un repository in Azure, è necessario creare le credenziali di accesso. Dall'interfaccia della riga di comando di Azure, immettere il comando seguente:
   
        azure site deployment user set [username] [password]
3. Passare alla directory **\\node\chat** e usare il comando seguente per creare una nuova app Web di Azure e un repository Git locale. Verrà inoltre creato un repository Git remoto denominato .
   
        azure site create mysitename --git
   
    Sostituire "mysitename" con un nome univoco per il sito Web.
4. Eseguire il commit dei file esistenti nel repository locale usando i comandi seguenti:
   
        git add .
        git commit -m "Initial commit"
5. Effettuare il push dei file nel repository delle app Web di Azure con il comando seguente:
   
        git push azure master
   
    Quando richiesto, immettere le credenziali dal passaggio 2. Durante le operazioni di importazione dei moduli nel server, verranno visualizzati messaggi di stato. Al termine del processo, l'applicazione sarà ospitata nell'app Web di Azure.
   
   > [!NOTE]
   > Durante l'installazione del modulo, è possibile notare errori di tipo Il progetto importato... non è stato trovato. Tali errori possono essere ignorati.
   > 
   > 
6. Socket.IO utilizza i WebSocket che non sono abilitati per impostazione predefinita in Azure. Per abilitare i WebSocket, utilizzare il comando seguente:
   
        azure site set -w
   
    Se richiesto, immettere il nome dell'app Web.
   
   > [!NOTE]
   > Il comando 'azure site set -w' funzionerà solo con la versione 0.7.4 o superiore dell'interfaccia della riga di comando di Azure. È anche possibile abilitare il supporto WebSocket utilizzando il [Portale di Azure](https://portal.azure.com).
   > 
   > Per abilitare i WebSocket usando il Portale di Azure, fare clic sull'app Web dal pannello App Web, selezionare **Tutte le impostazioni** > **Impostazioni dell'applicazione**. In **Web Socket** fare clic su **Attivato**. Fare quindi clic su **Salva**.
   > 
   > 
7. Per visualizzare l'app Web in Azure, utilizzare il comando seguente per avviare il browser Web e passare all'app Web ospitata:
   
        azure site browse

L'app ora è in esecuzione in Azure ed è in grado di inoltrare i messaggi di chat tra diversi client tramite Socket.IO.

## <a name="scale-out"></a>Scalabilità orizzontale
Le applicazioni Socket.IO possono essere scalate usando un **adattatore** per distribuire messaggi ed eventi tra più istanze di applicazioni. Nonostante siano disponibili diversi adattatori, l'adattatore [socket.io-redis] può essere usato facilmente con la funzionalità Cache Redis di Azure.

> [!NOTE]
> Un ulteriore requisito per la scalabilità orizzontale di una soluzione Socket.IO è il supporto di sessioni permanenti. Le sessioni permanenti sono abilitate per impostazione predefinita per le app Web di Azure tramite il routing delle richieste di Azure. Per altre informazioni, vedere il blog relativo all' [affinità delle istanze in Siti Web di Azure]
> 
> 

### <a name="create-a-redis-cache"></a>Creare una cache Redis
Eseguire la procedura descritta in [Creare una cache in Cache Redis di Azure] per creare una nuova cache.

> [!NOTE]
> Salvare il **Nome host** e la **Chiave primaria** per la cache in quanto saranno necessari nei passaggi successivi.
> 
> 

### <a name="add-the-redis-and-socketio-redis-modules"></a>Aggiungere i moduli redis e socket.io-redis
1. Dalla riga di comando passare alla directory **\\node\\chat** e usare il comando seguente.
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > Le versioni specificate in questo comando sono le stesse versioni usate nei test di questo articolo.
   > 
   > 
2. Modificare il file **app.js** per aggiungere le righe seguenti immediatamente dopo `var io = require('socket.io')(server);`
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    Sostituire **redishostname** e **rediskey** con il nome host e la chiave per la cache Redis.
   
    In questo modo viene creato un client di pubblicazione e sottoscrizione alla cache Redis creata in precedenza. I client vengono quindi usati con l'adattatore per configurare Socket.IO in modo da usare la cache Redis per passare messaggi ed eventi tra le istanze dell'applicazione
   
   > [!NOTE]
   > Anche se l'adattatore **socket.io-redis** può comunicare direttamente con Redis, la versione corrente non supporta l'autenticazione richiesta dalla cache Redis di Azure. Pertanto, la connessione iniziale viene creata usando il modulo **redis**, quindi il client viene passato all'adattatore **socket.io-redis**.
   > 
   > Nonostante la cache Redis di Azure supporti le connessioni sicure usando la porta 6380, alla data del 14 luglio 2014 i moduli usati in questo esempio non supportano le connessioni sicure. Il codice riportato sopra usa la porta 6379, predefinita e non sicura.
   > 
   > 
3. Salvare il file **app.js** modificato

### <a name="commit-changes-and-redeploy"></a>Eseguire il commit delle modifiche ed effettuare la ridistribuzione
Dalla riga di comando nella directory **\\node\\chat**, usare i comandi seguenti per eseguire il commit delle modifiche e ridistribuire l'applicazione.

    git add .
    git commit -m "implementing scale out"
    git push azure master

Dopo aver effettuato il push delle modifiche al server, è possibile scalare il sito tra più istanze tramite il comando seguente.

    azure site scale instances --instances #

**#** è il numero di istanze da creare.

È possibile effettuare la connessione all'app Web da più browser o computer per verificare che i messaggi siano inviati correttamente a tutti i client.

## <a name="troubleshooting"></a>Risoluzione dei problemi
### <a name="connection-limits"></a>Limiti di connessione
App Web di Azure è disponibile in più SKU, che determinano le risorse disponibili per il sito, incluso il numero di connessioni WebSocket consentite. Per altre informazioni, vedere la [pagina dei dettagli dei prezzi di App Web].

### <a name="messages-arent-being-sent-using-websockets"></a>I messaggi non vengono inviati usando WebSocket
Se i browser client continuano a eseguire il fallback al polling prolungato invece di usare WebSocket, il motivo potrebbe essere uno dei seguenti.

* **Tentare di limitare il trasporto ai soli WebSocket**
  
    Affinché Socket.IO possa usare WebSocket per il trasporto dei messaggi, sia il server che il client devono supportare WebSocket. Diversamente, Socket.IO negozierà un altro tipo di trasporto, come il polling prolungato. L'elenco predefinito dei tipi di trasporto usati da Socket.IO è ` websocket, htmlfile, xhr-polling, jsonp-polling`. È possibile forzarlo in modo da usare solo WebSocket aggiungendo il codice seguente al file **app.js**, dopo la riga contenente `, nicknames = {};`.
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > Si noti che i browser precedenti che non supportano WebSocket non potranno effettuare la connessione al sito mentre il codice riportato sopra è attivo, in quanto quest'ultimo limita la comunicazione ai soli WebSocket.
  > 
  > 
* **Usa SSL**
  
    WebSocket si basa su intestazioni HTTP usate con minore frequenza, come l'intestazione **Upgrade** . Alcuni dispositivi di rete intermedi, come i proxy Web, possono rimuovere tali intestazioni. Per evitare il problema, è possibile stabilire la connessione WebSocket su SSL.
  
    È possibile effettuare facilmente questa operazione configurando Socket.IO su `match origin protocol`. Questa configurazione fornisce a Socket.IO l'istruzione di proteggere la comunicazione WebSocket nello stesso modo della richiesta HTTP/HTTPS di origine per la pagina Web. Se un browser usa un URL HTTPS per visitare il sito Web, le comunicazioni WebSocket successive tramite Socket.IO verranno protette su SSL.
  
    Per modificare questo esempio in modo da abilitare questa configurazione, aggiungere il codice seguente al file **app.js** dopo la riga contenente `, nicknames = {};`.
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* **Verificare le impostazioni del file web.config**
  
    Le app Web di Azure che ospitano le applicazioni Node.js utilizzano il file **web.config** per eseguire il routing delle richieste in ingresso all'applicazione Node.js. Affinché i WebSocket funzionino correttamente con le applicazioni Node.js, il file **web.config** deve contenere la seguente voce.
  
        <webSocket enabled="false"/>
  
    In questo modo viene disabilitato il modulo IIS WebSocket, che include la propria distribuzione di WebSocket ed è in conflitto con i moduli WebSocket specifici di Node.js come Socket.IO. L'assenza di questa riga o la sua impostazione su `true`, potrebbe essere il motivo per il quale il trasporto WebSocket non funziona per l'applicazione.
  
    Di norma le applicazioni Node.js non includono un file **web.config** , pertanto Siti Web di Azure ne genererà automaticamente uno per le applicazioni Node.js quando queste vengono distribuite. Poiché questo file viene generato automaticamente sul server, per visualizzarlo è necessario usare l'URL FTP o FTPS per il sito Web. È possibile trovare gli URL FTP e FTPS per il sito nel portale classico selezionando l’app Web e quindi il collegamento **Dashboard** . Gli URL vengono visualizzati nella sezione **Riepilogo rapido** .
  
  > [!NOTE]
  > Il file **web.config** viene generato da Siti Web di Azure solo se non viene fornito dall'applicazione. Se si fornisce un file **web.config** nella radice del progetto dell'applicazione, tale file verrà usato da App Web di Azure.
  > 
  > 
  
    Se la voce non è presente o è impostata su un valore di `true`, è necessario creare un file **web.config** nella radice dell'applicazione Node.js e specificare un valore di `false`.  Di seguito viene fornito, come riferimento, un file **web.config** predefinito per un'applicazione che usa **app.js** come punto di ingresso.
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used to run node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that the server.js file is a node.js web app to be handled by the iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether the incoming URL matches a physical file in the /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped to the node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using the following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes to restart the server
                * node_env: will be propagated to node as NODE_ENV environment variable
                * debuggingEnabled - controls whether the built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    Se l'applicazione usa un punto di ingresso diverso da **app.js**, è necessario sostituire tutte le ricorrenze di **app.js** con il punto di ingresso corretto. ad esempio, la sostituzione di **app.js** con **server.js**.

> [!NOTE]
> Per iniziare a usare il servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app], dove è possibile creare un'app Web iniziale temporanea nel servizio app. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione è stato illustrato come creare un'applicazione di chat ospitata in un'app Web di Azure. È inoltre possibile ospitare l'applicazione come un servizio cloud di Azure. Per le procedure che illustrano come eseguire questa operazione, vedere [Creazione di un'applicazione di chat Node.js con Socket.IO in un servizio cloud di Azure].

Per ulteriori informazioni, vedere anche il [Centro per sviluppatori di Node.js].

## <a name="whats-changed"></a>Modifiche apportate
* Per una guida per il passaggio da Siti Web a Servizio app vedere: [Servizio app di Azure e i servizi di Azure esistenti]

<!-- URL List -->

[Cache Redis di Azure]: /documentation/services/redis-cache/
[app Web del servizio app]: http://go.microsoft.com/fwlink/?LinkId=529714
[pagina dei dettagli dei prezzi di App Web]: http://go.microsoft.com/fwlink/?LinkId=511643
[Creazione di un'applicazione di chat Node.js con Socket.IO in un servizio cloud di Azure]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure the Azure CLI]: ../cli-install-nodejs.md
[Servizio app di Azure e i servizi di Azure esistenti]: http://go.microsoft.com/fwlink/?LinkId=529714
[Centro per sviluppatori di Node.js]: /develop/nodejs/
[Prova il servizio app]: https://azure.microsoft.com/try/app-service/
[affinità delle istanze in Siti Web di Azure]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[Creare una cache in Cache Redis di Azure]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[socket.io-redis]: https://github.com/socketio/socket.io-redis
[archivio GitHub Socket.IO]: https://github.com/socketio/socket.io
[versione archiviata ZIP o GZ]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
