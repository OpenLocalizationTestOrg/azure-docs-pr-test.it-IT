---
title: un'applicazione di chat Node.js con Socket.IO in Azure App Service aaaCreate
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
ms.openlocfilehash: 3bd7867ccc297dc0a21c7a00cc9db06358877f5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a>Creazione di un'applicazione di chat Node.js con Socket.IO in Servizio app di Azure
Socket.IO fornisce comunicazioni in tempo reale tra il server node.js e i client usando WebSocket. Supporta inoltre i trasporti tooother fallback (ad esempio polling lungo) che funziona con i browser meno recenti. In questa esercitazione verrà illustrati l'hosting di un'applicazione di chat Socket.IO basato su come un'app web di Azure e mostrano come tooscale hello applicazione utilizzando [Cache Redis di Azure]. Per altre informazioni su Socket.IO, vedere <http://socket.io/>.

> [!NOTE]
> procedure di Hello in questa attività si applicano troppo[App del servizio Web App]; per i servizi Cloud, vedere [compilare un'applicazione di Chat Node.js con Socket.IO su un servizio Cloud Azure].
> 
> 

## <a name="download-hello-chat-example"></a>Scaricare l'esempio di chat hello
Per questo progetto, si utilizzerà l'esempio di chat hello dalla hello [repository Socket.IO GitHub]. Eseguire l'esempio hello toodownload di passaggi seguente hello e aggiungerla toohello progetto creato in precedenza.

1. Scaricare un [ZIP o GZ archiviati versione] del progetto Socket.IO hello (versione 1.3.5 è stato utilizzato per questo documento)
2. Estrarre hello di archiviazione e copia hello **esempi\\chat** nuovo percorso di directory tooa. Ad esempio, **\\node\\chat**.

## <a name="modify-appjs-and-install-modules"></a>Modificare app.js e installare i moduli
1. Rinominare hello **index.js** file troppo**app.js**. In questo modo toodetect Azure che si tratta di un'applicazione Node.js.
2. Aprire hello **app.js** file in un editor di testo. Modifica hello riga contenente `var io = require('../..')(server);` come illustrato di seguito:
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. Aprire hello **package. JSON** file e aggiungere un riferimento toosocket.io in `dependencies`, come illustrato di seguito:
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. Hello della riga di comando, modificare toohello  **\\nodo\\chat** directory e utilizzare npm tooinstall hello i moduli necessari per questa applicazione:
   
        npm install
   
    I moduli di hello verrà installato in una sottocartella denominata **node_modules**.

## <a name="create-an-azure-web-app"></a>Creare un'app Web di Azure
Seguire questi toocreate passaggi un'app web di Azure, abilitare la pubblicazione Git e quindi abilitare il supporto di WebSocket per l'app web hello.

> [!NOTE]
> toocomplete questa esercitazione, è necessario un account di Azure. Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">versione di valutazione gratuita di Azure</a>.
> 
> 

1. Installare l'interfaccia della riga di comando di Azure (Azure CLI) hello e connettersi tooyour sottoscrizione di Azure. Vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md).
2. Se questa è la prima impostazione del tempo di un archivio in Azure, è necessario toocreate le credenziali di accesso. Hello CLI di Azure, digitare hello comando seguente:
   
        azure site deployment user set [username] [password]
3. Modificare toohello  **\\node\chat** directory e seguente hello utilizzare comandi toocreate una nuova app web di Azure e un archivio Git locale. Verrà inoltre creato un repository Git remoto denominato .
   
        azure site create mysitename --git
   
    Sostituire "mysitename" con un nome univoco per il sito Web.
4. Eseguire il commit repository locale di hello esistente file toohello utilizzando hello seguenti comandi:
   
        git add .
        git commit -m "Initial commit"
5. Esegui il push del repository di hello file toohello App Web di Azure con hello comando seguente:
   
        git push azure master
   
    Quando richiesto, immettere le credenziali dal passaggio 2. Come i moduli vengono importati nel server di hello, si riceverà i messaggi di stato. Al termine di questo processo, un'applicazione hello verrà ospitata in un'applicazione web di Azure.
   
   > [!NOTE]
   > Durante l'installazione del modulo, è possibile riscontrare errori che ' hello progetto importato non è stato trovato '. Tali errori possono essere ignorati.
   > 
   > 
6. Socket.IO utilizza i WebSocket che non sono abilitati per impostazione predefinita in Azure. i socket web tooenable utilizzare hello comando seguente:
   
        azure site set -w
   
    Se richiesto, immettere il nome di hello dell'app web hello.
   
   > [!NOTE]
   > Hello 'set -w sito azure' verrà comando funziona solo con versione 0.7.4 o successiva di hello interfaccia della riga di comando di Azure. È inoltre possibile abilitare il supporto di WebSocket con hello [portale Azure](https://portal.azure.com).
   > 
   > utilizzo di WebSockets tooenable hello portale di Azure, fare clic su app web hello dal pannello App Web hello, fare clic su **tutte le impostazioni** > **le impostazioni dell'applicazione**. In **Web Socket** fare clic su **Attivato**. Fare quindi clic su **Salva**.
   > 
   > 
7. tooview hello app web seguenti di hello Azure, utilizzare comando toolaunch web browser e passare l'app web toohello ospitato:
   
        azure site browse

L'app ora è in esecuzione in Azure ed è in grado di inoltrare i messaggi di chat tra diversi client tramite Socket.IO.

## <a name="scale-out"></a>Scalabilità orizzontale
Applicazioni Socket.IO possono essere scalate orizzontalmente con un **adapter** toodistribute messaggi e gli eventi tra più istanze dell'applicazione. Anche se sono presenti più schede, hello [socket.io redis] adapter può essere utilizzato con funzionalità di Cache Redis di Azure hello facilmente.

> [!NOTE]
> Un ulteriore requisito per la scalabilità orizzontale di una soluzione Socket.IO è il supporto di sessioni permanenti. Le sessioni permanenti sono abilitate per impostazione predefinita per le app Web di Azure tramite il routing delle richieste di Azure. Per altre informazioni, vedere il blog relativo all' [affinità delle istanze in Siti Web di Azure]
> 
> 

### <a name="create-a-redis-cache"></a>Creare una cache Redis
Eseguire i passaggi di hello in [creare una cache in Cache Redis di Azure] toocreate una nuova cache.

> [!NOTE]
> Salvare hello **nome Host** e **chiave primaria** per la cache, come queste saranno necessarie hello passaggi successivi.
> 
> 

### <a name="add-hello-redis-and-socketio-redis-modules"></a>Aggiungere redis hello e moduli socket.io redis
1. Dalla riga di comando, modificare toohello  **\\nodo\\chat** directory e utilizzare hello comando seguente.
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > versioni di Hello specificate in questo comando sono versioni hello utilizzate per la verifica di questo articolo.
   > 
   > 
2. Modificare hello **app.js** seguenti di hello tooadd file righe immediatamente dopo`var io = require('socket.io')(server);`
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    Sostituire **redishostname** e **rediskey** con nome host hello e la chiave per la cache Redis.
   
    Verrà creata una pubblicazione e sottoscrizione toohello client della cache Redis creata in precedenza. i client Hello vengono quindi utilizzati con hello adapter tooconfigure cache Redis di Socket.IO toouse hello per il passaggio di messaggi e gli eventi tra le istanze dell'applicazione
   
   > [!NOTE]
   > Durante la hello **socket.io redis** adapter può comunicare direttamente tooRedis, la versione corrente di hello non supporta l'autenticazione di hello richiesto dalla cache Redis di Azure. La connessione iniziale hello viene creato utilizzando hello **redis** modulo, quindi client hello viene passato toohello **socket.io redis** adapter.
   > 
   > Durante la Cache Redis di Azure supporta connessioni protette tramite la porta 6380, moduli hello utilizzati in questo esempio non supportano le connessioni protette a partire da 14/7/2014. Hello sopra codice utilizza hello predefinito, la porta non protetta di 6379.
   > 
   > 
3. Salva hello modificato **app.js**

### <a name="commit-changes-and-redeploy"></a>Eseguire il commit delle modifiche ed effettuare la ridistribuzione
Dalla riga di comando in hello hello  **\\nodo\\chat** directory, utilizzare hello modifiche toocommit i comandi seguenti e ridistribuire l'applicazione hello.

    git add .
    git commit -m "implementing scale out"
    git push azure master

Una volta modifiche hello sono state inserite toohello server, è possibile ridimensionare il sito tra più istanze tramite hello comando seguente.

    azure site scale instances --instances #

Dove  **#**  hello numero di istanze toocreate.

È possibile connettersi app web tooyour da più computer o browser tooverify che i messaggi vengono inviati correttamente tooall client.

## <a name="troubleshooting"></a>Risoluzione dei problemi
### <a name="connection-limits"></a>Limiti di connessione
Le app Web di Azure è disponibile in più SKU, che determinano sito tooyour disponibili risorse di hello. Ciò include il numero di hello di connessioni WebSocket consentite. Per ulteriori informazioni, vedere hello [pagina prezzi App Web].

### <a name="messages-arent-being-sent-using-websockets"></a>I messaggi non vengono inviati usando WebSocket
Se il browser client mantenga fallback toolong polling anziché WebSocket, è possibile a causa di uno dei seguenti hello.

* **È possibile limitare hello trasporto toojust WebSocket**
  
    Affinché Socket.IO toouse WebSocket come hello trasporto di messaggistica, hello server e client deve supportare WebSocket. Se uno o altri hello, non Socket.IO negozierà un altro trasporto, ad esempio di polling lungo. elenco predefinito di Hello dei trasporti utilizzati Socket.IO ` websocket, htmlfile, xhr-polling, jsonp-polling`. È possibile imporre l'uso tooonly WebSocket aggiungendo hello seguente codice toohello **app.js** file, dopo la riga hello contenente `, nicknames = {};`.
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > Si noti che browser meno recenti che non supportano WebSocket non saranno in grado di tooconnect toohello sito mentre hello di sopra di codice è attiva, in quanto limita solo tooWebSockets di comunicazione.
  > 
  > 
* **Usa SSL**
  
    WebSocket si basano su alcuni meno intestazioni HTTP utilizzate, ad esempio hello **aggiornamento** intestazione. Alcuni dispositivi di rete intermedi, come i proxy Web, possono rimuovere tali intestazioni. tooavoid questo problema, è possibile stabilire una connessione WebSocket hello tramite SSL.
  
    Un modo semplice di tooaccomplish tratta tooconfigure Socket.IO troppo`match origin protocol`. Questo indica hello comunicazione WebSocket toosecure di Socket.IO identico hello originari HTTP/HTTPS richiesta per la pagina web hello. Se un browser, viene utilizzato per il sito Web toovisit un URL HTTPS, le comunicazioni WebSocket successive tramite Socket.IO saranno protetti tramite SSL.
  
    toomodify tooenable in questo esempio questa configurazione, aggiungere hello seguente codice toohello **app.js** file dopo la riga hello contenente `, nicknames = {};`.
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* **Verificare le impostazioni del file web.config**
  
    App web di Azure che ospitano applicazioni Node.js utilizzare hello **Web. config** tooroute file in ingresso richieste applicazione Node.js toohello. Per WebSocket toofunction correttamente con le applicazioni Node.js, hello **Web. config** deve contenere hello entrata.
  
        <webSocket enabled="false"/>
  
    Disabilita il modulo IIS WebSocket hello, che include la propria implementazione di WebSocket e in conflitto con WebSocket moduli Node.js specifici, ad esempio Socket.IO. Se questa riga non è presente o è troppo`true`, è possibile motivo hello trasporto WebSocket hello non funzionante per l'applicazione.
  
    Di norma le applicazioni Node.js non includono un file **web.config** , pertanto Siti Web di Azure ne genererà automaticamente uno per le applicazioni Node.js quando queste vengono distribuite. Poiché questo file viene automaticamente generato sul server hello, è necessario utilizzare hello FTP o FTPS URL per il sito Web tooview questo file. È possibile trovare hello FTP e FTPS URL per il sito nel portale classico hello selezionando l'app web e quindi hello **Dashboard** collegamento. Hello gli URL vengono visualizzati in hello **riepilogo rapido** sezione.
  
  > [!NOTE]
  > Hello **Web. config** file viene generato solo per siti Web di Azure, se l'applicazione non ne fornisce uno. Se si fornisce un **Web. config** file nella radice del progetto di applicazione hello da utilizzare per le app Web di Azure.
  > 
  > 
  
    Se la voce hello non è presente o è impostata un valore di tooa `true`, sarà necessario creare un **Web. config** nella radice dell'applicazione Node.js hello e specificare un valore di `false`.  Per riferimento, hello seguente è un valore predefinito **Web. config** per un'applicazione che utilizza **app.js** come punto di ingresso hello.
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used toorun node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that hello server.js file is a node.js web app toobe handled by hello iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether hello incoming URL matches a physical file in hello /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped toohello node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using hello following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes toorestart hello server
                * node_env: will be propagated toonode as NODE_ENV environment variable
                * debuggingEnabled - controls whether hello built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    Se l'applicazione utilizza un punto di ingresso diverso da **app.js**, è necessario sostituire tutte le occorrenze di **app.js** con hello correggere punto di ingresso. ad esempio, la sostituzione di **app.js** con **server.js**.

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App], in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione è stato descritto come toocreate un'applicazione di chat ospitato in un'applicazione web di Azure. È inoltre possibile ospitare l'applicazione come un servizio cloud di Azure. Per la procedura tooaccomplish questa operazione, vedere [compilare un'applicazione di Chat Node.js con Socket.IO su un servizio Cloud Azure].

Per ulteriori informazioni, vedere anche hello [Centro per sviluppatori di Node.js].

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [servizio App di Azure e relativo impatto sui servizi di Azure esistente].

<!-- URL List -->

[Cache Redis di Azure]: /documentation/services/redis-cache/
[App del servizio Web App]: http://go.microsoft.com/fwlink/?LinkId=529714
[pagina prezzi App Web]: http://go.microsoft.com/fwlink/?LinkId=511643
[compilare un'applicazione di Chat Node.js con Socket.IO su un servizio Cloud Azure]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure hello Azure CLI]: ../cli-install-nodejs.md
[servizio App di Azure e relativo impatto sui servizi di Azure esistente]: http://go.microsoft.com/fwlink/?LinkId=529714
[Centro per sviluppatori di Node.js]: /develop/nodejs/
[tenta di servizio App]: https://azure.microsoft.com/try/app-service/
[affinità delle istanze in Siti Web di Azure]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[creare una cache in Cache Redis di Azure]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[socket.io redis]: https://github.com/socketio/socket.io-redis
[repository Socket.IO GitHub]: https://github.com/socketio/socket.io
[ZIP o GZ archiviati versione]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
