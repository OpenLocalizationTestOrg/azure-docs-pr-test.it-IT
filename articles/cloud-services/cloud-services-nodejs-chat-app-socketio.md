---
title: applicazione di aaaNode.js utilizzando Socket.io | Documenti Microsoft
description: "Informazioni su come socket.io toouse in un'applicazione node.js è ospitato in Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 7f9435e0-7732-4aa1-a4df-ea0e894b847f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 47c6c4a748938959315b880340f41f31faab4ea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a>Creazione di un'applicazione di chat Node.js con Socket.IO in un servizio cloud di Azure
Socket.IO fornisce comunicazioni in tempo reale tra il server node.js e i client. In questa esercitazione verrà illustrato l'hosting di un'applicazione di chat basata su socket.IO in Azure. Per altre informazioni su Socket.IO, vedere <http://socket.io/>.

Di seguito viene riportata una schermata dell'applicazione hello completata:

![Una finestra del browser visualizzazione servizio hello ospitato in Azure][completed-app]  

## <a name="prerequisites"></a>Prerequisiti
Verificare che hello i seguenti prodotti e le versioni sono installate toosuccessfully hello completo esempio in questo articolo:

* Installare [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)
* Installare [Node.js](https://nodejs.org/download/)
* Installare [Python versione 2.7.10](https://www.python.org/)

## <a name="create-a-cloud-service-project"></a>Creazione di un progetto di servizio cloud
Hello i passaggi seguenti Crea progetto di servizio cloud hello che ospiterà l'applicazione Socket.IO hello.

1. Da hello **Menu Start** o **schermata Start**, cercare **Windows PowerShell**. Fare infine clic con il pulsante destro del mouse su **Windows PowerShell** e scegliere **Esegui come amministratore**.
   
    ![Icona di Azure PowerShell][powershell-menu]
2. Creare una directory denominata **c:\\node**. 
   
        PS C:\> md node
3. Modificare le directory toohello **c:\\nodo** directory
   
        PS C:\> cd node
4. Immettere i seguenti comandi toocreate una nuova soluzione denominata hello **chatapp** e un ruolo di lavoro denominato **WorkerRole1**:
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    Verrà visualizzato hello seguente risposta:
   
    ![output di Hello del nuovo hello-azureservice e azurenodeworkerrolecmdlets aggiungere](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-hello-chat-example"></a>Scaricare l'esempio Chat hello
Per questo progetto, si utilizzerà l'esempio di chat hello dalla hello [repository Socket.IO GitHub]. Eseguire l'esempio hello toodownload di passaggi seguente hello e aggiungerla toohello progetto creato in precedenza.

1. Creare una copia locale del repository hello utilizzando hello **Clone** pulsante. È inoltre possibile utilizzare hello **ZIP** progetto hello toodownload di button.
   
   ![Una finestra del browser visualizzazione https://github.com/LearnBoost/socket.io/tree/master/examples/chat, con icona di download ZIP hello evidenziato][chat-example-view]
2. Esplorare la struttura di directory hello del repository locale hello fino a giungere al hello **esempi\\chat** directory. Copiare il contenuto di hello del toothe directory **c:\\nodo\\chatapp\\WorkerRole1** directory creato in precedenza.
   
   ![Soluzioni, visualizzazione contenuto hello degli esempi di hello\\directory chat estratti dall'archivio hello][chat-contents]
   
   gli elementi evidenziati nella schermata di hello precedente Hello sono file hello copiati dal hello **esempi\\chat** directory
3. In hello **c:\\nodo\\chatapp\\WorkerRole1** directory, hello di eliminazione **server.js** file e quindi rinominare hello **app.js**file troppo**server.js**. Questa operazione rimuove predefinito hello **server.js** file creato in precedenza da hello **Add-AzureNodeWorkerRole** cmdlet e sostituire con un'applicazione hello file hello esempio chat.

### <a name="modify-serverjs-and-install-modules"></a>Modificare Server.js e installare i moduli
Prima di un'applicazione hello test in hello dell'emulatore di Azure, è necessario apportare alcune modifiche minori. Eseguire i seguenti passaggi toothe server.js file hello:

1. Aprire hello **server.js** file in Visual Studio o qualsiasi editor di testo.
2. Trovare hello **le dipendenze del modulo** sezione all'inizio di hello di server.js e modificare hello riga contenente **poi = require('.. //.. LIB//socket.IO')** troppo**poi = require('socket.io')** come illustrato di seguito:
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. un'applicazione hello tooensure in ascolto sulla porta corretta di hello, aprire server.js in blocco note o l'editor preferito e quindi modificare la riga seguente, sostituendo **3000** con **process.env.port** come illustrato di seguito:
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

Dopo aver salvato le modifiche di hello troppo**server.js**, utilizzare hello alla procedura seguente per installare i moduli necessari e quindi testare l'applicazione hello nell'emulatore di Azure:

1. Utilizzando **Azure PowerShell**, modificare le directory toohello **c:\\nodo\\chatapp\\WorkerRole1** hello directory e l'utilizzo successivo comando tooinstall hello moduli necessari per questa applicazione:
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   Verranno installati i moduli di hello elencati nel file package. JSON hello. Al termine del comando di hello, verrà visualizzato il seguente toothe simili di output:
   
   ![comando di installazione di output di Hello di hello npm][The-output-of-the-npm-install-command]
2. Poiché in questo esempio è stato originariamente parte di hello repository Socket.IO GitHub e direttamente a cui fa riferimento libreria Socket.IO hello percorso relativo, Socket.IO non esiste alcun riferimento nel file package. JSON hello, pertanto è necessario installarlo eseguendo hello comando seguente:
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a>Test e distribuzione
1. Avviare l'emulatore hello eseguendo hello comando seguente:
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > Se si verificano problemi con l'avvio dell'emulatore, ad esempio Start-AzureEmulator: Errore imprevisto.  Dettagli: Rilevato un errore imprevisto hello oggetto di comunicazione System.ServiceModel.Channels.ServiceChannel, non utilizzabile per la comunicazione perché è nello stato Faulted hello.
   
      reinstallare AzureAuthoringTools 2.7.1 e AzureComputeEmulator 2.7 - verificare che la versione corrisponda.
   >
   >


2. Aprire un browser e andare troppo**http://127.0.0.1**.
3. Quando viene visualizzata una finestra hello, immettere un nome alternativo e quindi premere INVIO.
   In questo modo si toopost messaggi come un nome alternativo specifico. funzionalità multiutente tootest, aprire finestre del browser aggiuntive utilizzando lo stesso URL e immettere i nomi alternativi diversi.
   
   ![Due finestre del browser con i messaggi della chat di User1 e User2](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. Dopo l'applicazione hello test, arrestare l'emulatore hello eseguendo il comando seguente:
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. toodeploy hello applicazione tooAzure, utilizzare il **pubblica AzureServiceProject** cmdlet. ad esempio:
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > Essere toouse che un nome univoco, in caso contrario hello processo di pubblicazione avrà esito negativo. Una volta completata la distribuzione di hello, hello browser aprire e passare servizio toohello distribuito.
   > 
   > Se si riceve un errore indicante che hello fornito nome della sottoscrizione non esiste in hello importato profilo di pubblicazione, è necessario scaricare e importare il profilo di pubblicazione hello per la sottoscrizione prima della distribuzione tooAzure. Vedere hello **distribuzione tooAzure applicazione hello** sezione [compilare e distribuire un tooan applicazione Node.js servizio Cloud di Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)
   > 
   > 
   
   ![Una finestra del browser visualizzazione servizio hello ospitato in Azure][completed-app]
   
   > [!NOTE]
   > Se si riceve un errore indicante che hello fornito nome della sottoscrizione non esiste in hello importato profilo di pubblicazione, è necessario scaricare e importare il profilo di pubblicazione hello per la sottoscrizione prima della distribuzione tooAzure. Vedere hello **distribuzione tooAzure applicazione hello** sezione [compilare e distribuire un tooan applicazione Node.js servizio Cloud di Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)
   > 
   > 

L'applicazione è ora in esecuzione in Azure ed è in grado di inoltrare i messaggi di chat tra diversi client tramite Socket.IO.

> [!NOTE]
> Per semplicità, in questo esempio viene limitato toochatting tra gli utenti connessi toohello stessa istanza. Ciò significa che se il servizio cloud hello crea due istanze del ruolo di lavoro, gli utenti potranno solo toochat con altri utenti connessi toohello stessa istanza del ruolo worker. tooscale hello applicazione toowork con più istanze del ruolo, è possibile utilizzare una tecnologia simile Bus di servizio tooshare hello Socket.IO archiviare lo stato tra più istanze. Per esempi, vedere esempi di utilizzo di argomenti e code del Bus di servizio hello in hello [Azure SDK per Node.js GitHub repository](https://github.com/WindowsAzure/azure-sdk-for-node).
> 
> 

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione è stato descritto come toocreate un'applicazione di chat base ospitato in un servizio Cloud di Azure. toolearn come toohost questa applicazione in un sito Web di Azure, vedere [compilare un'applicazione di Chat Node.js con Socket.IO sul sito Web di Azure][chatwebsite].

Per ulteriori informazioni, vedere anche hello [Centro per sviluppatori di Node.js](/develop/nodejs/).

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[repository Socket.IO GitHub]: https://github.com/LearnBoost/socket.io/tree/0.9.14
[Azure Considerations]: #windowsazureconsiderations
[Hosting hello Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


