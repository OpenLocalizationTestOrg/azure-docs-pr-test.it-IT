---
title: aaaWeb App con Express (Node.js) | Documenti Microsoft
description: Esercitazione si basa sull'esercitazione servizio cloud di hello e viene illustrato come toouse hello modulo Express.
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 24f8e7ef-e90d-4554-9b1e-a9b31d5824e5
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 91921bfbe137eeca9a110d4cb18eb57b46b0060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a>Creazione di un'applicazione Web Node.js utilizzando Express in un servizio cloud di Azure
Node.js include un set di funzionalità minimo in fase di esecuzione core hello.
Gli sviluppatori spesso utilizzano 3rd party moduli tooprovide funzionalità aggiuntive quando si sviluppa un'applicazione Node.js. In questa esercitazione si creerà una nuova applicazione utilizzando hello [Express] [ Express] modulo, che fornisce un framework MVC per la creazione di applicazioni web Node. js.

Di seguito viene riportata una schermata dell'applicazione hello completata:

![Un web browser visualizzazione tooExpress benvenuto in Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a>Creazione di un progetto di servizio cloud
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

Eseguire l'esempio hello passaggi toocreate un nuovo progetto di servizio cloud denominato 'expressapp':

1. Da hello **Menu Start** o **schermata Start**, cercare **Windows PowerShell**. Fare infine clic con il pulsante destro del mouse su **Windows PowerShell** e scegliere **Esegui come amministratore**.
   
    ![Icona di Azure PowerShell](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. Modificare le directory toohello **c:\\nodo** directory e quindi immettere i seguenti comandi toocreate una nuova soluzione denominata hello **expressapp** e un ruolo web denominato **WebRole1** :
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > Per impostazione predefinita, in **Add-AzureNodeWebRole** viene usata una versione precedente di Node.js. Hello **Set AzureServiceProjectRole** istruzione precedente indica a Azure toouse v0.10.21 del nodo.  Si noti come parametri hello maiuscole e minuscole.  È possibile verificare versione corretta di hello di Node.js è stata selezionata per il controllo hello **motori** proprietà **WebRole1\package.json**.
    > 
    > 

## <a name="install-express"></a>Installazione di Express
1. Installare generatore Express hello eseguendo hello comando seguente:
   
        PS C:\node\expressapp> npm install express-generator -g
   
    output di Hello del comando di npm hello dovrebbe essere simile toohello risultato. 
   
    ![Output di hello la visualizzazione di Windows PowerShell di npm hello installare comando express.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. Modificare le directory toohello **WebRole1** directory e utilizzare hello comando express toogenerate una nuova applicazione:
   
        PS C:\node\expressapp\WebRole1> express
   
    Si sarà toooverwrite richiesta dell'applicazione precedente. Immettere **y** o **Sì** toocontinue. Express genererà file app.js hello e una struttura di cartelle per la compilazione dell'applicazione.
   
    ![output di Hello del comando express hello](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. tooinstall dipendenze aggiuntive definite nel file package. JSON hello, immettere hello comando seguente:
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![comando di installazione di output di Hello di hello npm](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. Comando che segue di hello utilizzare hello toocopy **bin/www** file troppo**server.js**. Si tratta pertanto servizio cloud hello è possibile trovare il punto di ingresso hello per questa applicazione.
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   Dopo il completamento del comando, è necessario un **server.js** file nella directory hello WebRole1.
5. Modificare hello **server.js** tooremove uno di hello '.' hello seguente riga di caratteri.
   
       var app = require('../app');
   
   Dopo aver apportato questa modifica, la riga hello compariranno come indicato di seguito.
   
       var app = require('./app');
   
   Questa modifica è necessaria perché il file hello è spostato (in precedenza **bin/www**,) toohello stessa directory del file app hello è obbligatorio. Dopo aver apportato questa modifica, Salva hello **server.js** file.
6. Comando che segue di hello utilizzare un'applicazione hello toorun in hello dell'emulatore di Azure:
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Una pagina web contenente tooexpress iniziale.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-hello-view"></a>Modifica vista hello
A questo punto, modificare il messaggio hello vista toodisplay hello "TooExpress benvenuto in Azure".

1. Immettere i seguenti file di comando tooopen hello index.jade hello:
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![contenuto di Hello del file index.jade hello.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   Jade è di tipo motore di visualizzazione predefinito hello utilizzato dalle applicazioni di Express. Per ulteriori informazioni sul motore di visualizzazione Jade hello, vedere [http://jade-lang.com][http://jade-lang.com].
2. Modificare l'ultima riga di hello del testo aggiungendo **in Azure**.
   
   ![legge i file index.jade Hello, ultima riga hello: p benvenuto troppo\#{title} in Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. Salvare il file di hello e chiudere Blocco note.
4. Aggiornare il tuo browser per vedere le modifiche.
   
   ![Una finestra del browser, pagina hello contiene tooExpress benvenuto in Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

Dopo l'applicazione hello test, utilizzare hello **Stop AzureEmulator** dell'emulatore di cmdlet toostop hello.

## <a name="publishing-hello-application-tooazure"></a>Pubblicazione hello applicazione tooAzure
Nella finestra di PowerShell Azure hello, utilizzare hello **pubblica AzureServiceProject** servizio cloud di cmdlet toodeploy hello applicazione tooa

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

Al termine dell'operazione di distribuzione hello, il browser verrà aprire e visualizzare la pagina web hello.

![Un web browser visualizzazione pagina Express hello. URL di Hello indica che è attualmente ospitato in Azure.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere hello [Centro per sviluppatori di Node.js](/develop/nodejs/).

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


