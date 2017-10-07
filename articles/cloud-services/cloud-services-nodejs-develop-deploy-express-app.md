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
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a><span data-ttu-id="9c890-103">Creazione di un'applicazione Web Node.js utilizzando Express in un servizio cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="9c890-103">Build a Node.js web application using Express on an Azure Cloud Service</span></span>
<span data-ttu-id="9c890-104">Node.js include un set di funzionalità minimo in fase di esecuzione core hello.</span><span class="sxs-lookup"><span data-stu-id="9c890-104">Node.js includes a minimal set of functionality in hello core runtime.</span></span>
<span data-ttu-id="9c890-105">Gli sviluppatori spesso utilizzano 3rd party moduli tooprovide funzionalità aggiuntive quando si sviluppa un'applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="9c890-105">Developers often use 3rd party modules tooprovide additional functionality when developing a Node.js application.</span></span> <span data-ttu-id="9c890-106">In questa esercitazione si creerà una nuova applicazione utilizzando hello [Express] [ Express] modulo, che fornisce un framework MVC per la creazione di applicazioni web Node. js.</span><span class="sxs-lookup"><span data-stu-id="9c890-106">In this tutorial you will create a new application using hello [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span></span>

<span data-ttu-id="9c890-107">Di seguito viene riportata una schermata dell'applicazione hello completata:</span><span class="sxs-lookup"><span data-stu-id="9c890-107">A screenshot of hello completed application is below:</span></span>

![Un web browser visualizzazione tooExpress benvenuto in Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="9c890-109">Creazione di un progetto di servizio cloud</span><span class="sxs-lookup"><span data-stu-id="9c890-109">Create a Cloud Service Project</span></span>
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

<span data-ttu-id="9c890-110">Eseguire l'esempio hello passaggi toocreate un nuovo progetto di servizio cloud denominato 'expressapp':</span><span class="sxs-lookup"><span data-stu-id="9c890-110">Perform hello following steps toocreate a new cloud service project named 'expressapp':</span></span>

1. <span data-ttu-id="9c890-111">Da hello **Menu Start** o **schermata Start**, cercare **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="9c890-111">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="9c890-112">Fare infine clic con il pulsante destro del mouse su **Windows PowerShell** e scegliere **Esegui come amministratore**.</span><span class="sxs-lookup"><span data-stu-id="9c890-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Icona di Azure PowerShell](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. <span data-ttu-id="9c890-114">Modificare le directory toohello **c:\\nodo** directory e quindi immettere i seguenti comandi toocreate una nuova soluzione denominata hello **expressapp** e un ruolo web denominato **WebRole1** :</span><span class="sxs-lookup"><span data-stu-id="9c890-114">Change directories toohello **c:\\node** directory and then enter hello following commands toocreate a new solution named **expressapp** and a web role named **WebRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > <span data-ttu-id="9c890-115">Per impostazione predefinita, in **Add-AzureNodeWebRole** viene usata una versione precedente di Node.js.</span><span class="sxs-lookup"><span data-stu-id="9c890-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span></span> <span data-ttu-id="9c890-116">Hello **Set AzureServiceProjectRole** istruzione precedente indica a Azure toouse v0.10.21 del nodo.</span><span class="sxs-lookup"><span data-stu-id="9c890-116">hello **Set-AzureServiceProjectRole** statement above instructs Azure toouse v0.10.21 of Node.</span></span>  <span data-ttu-id="9c890-117">Si noti come parametri hello maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="9c890-117">Note hello parameters are case-sensitive.</span></span>  <span data-ttu-id="9c890-118">È possibile verificare versione corretta di hello di Node.js è stata selezionata per il controllo hello **motori** proprietà **WebRole1\package.json**.</span><span class="sxs-lookup"><span data-stu-id="9c890-118">You can verify hello correct version of Node.js has been selected by checking hello **engines** property in **WebRole1\package.json**.</span></span>
    > 
    > 

## <a name="install-express"></a><span data-ttu-id="9c890-119">Installazione di Express</span><span class="sxs-lookup"><span data-stu-id="9c890-119">Install Express</span></span>
1. <span data-ttu-id="9c890-120">Installare generatore Express hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9c890-120">Install hello Express generator by issuing hello following command:</span></span>
   
        PS C:\node\expressapp> npm install express-generator -g
   
    <span data-ttu-id="9c890-121">output di Hello del comando di npm hello dovrebbe essere simile toohello risultato.</span><span class="sxs-lookup"><span data-stu-id="9c890-121">hello output of hello npm command should look similar toohello result below.</span></span> 
   
    ![Output di hello la visualizzazione di Windows PowerShell di npm hello installare comando express.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. <span data-ttu-id="9c890-123">Modificare le directory toohello **WebRole1** directory e utilizzare hello comando express toogenerate una nuova applicazione:</span><span class="sxs-lookup"><span data-stu-id="9c890-123">Change directories toohello **WebRole1** directory and use hello express command toogenerate a new application:</span></span>
   
        PS C:\node\expressapp\WebRole1> express
   
    <span data-ttu-id="9c890-124">Si sarà toooverwrite richiesta dell'applicazione precedente.</span><span class="sxs-lookup"><span data-stu-id="9c890-124">You will be prompted toooverwrite your earlier application.</span></span> <span data-ttu-id="9c890-125">Immettere **y** o **Sì** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="9c890-125">Enter **y** or **yes** toocontinue.</span></span> <span data-ttu-id="9c890-126">Express genererà file app.js hello e una struttura di cartelle per la compilazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9c890-126">Express will generate hello app.js file and a folder structure for building your application.</span></span>
   
    ![output di Hello del comando express hello](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. <span data-ttu-id="9c890-128">tooinstall dipendenze aggiuntive definite nel file package. JSON hello, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9c890-128">tooinstall additional dependencies defined in hello package.json file, enter hello following command:</span></span>
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![comando di installazione di output di Hello di hello npm](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. <span data-ttu-id="9c890-130">Comando che segue di hello utilizzare hello toocopy **bin/www** file troppo**server.js**.</span><span class="sxs-lookup"><span data-stu-id="9c890-130">Use hello following command toocopy hello **bin/www** file too**server.js**.</span></span> <span data-ttu-id="9c890-131">Si tratta pertanto servizio cloud hello è possibile trovare il punto di ingresso hello per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="9c890-131">This is so hello cloud service can find hello entry point for this application.</span></span>
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   <span data-ttu-id="9c890-132">Dopo il completamento del comando, è necessario un **server.js** file nella directory hello WebRole1.</span><span class="sxs-lookup"><span data-stu-id="9c890-132">After this command completes, you should have a **server.js** file in hello WebRole1 directory.</span></span>
5. <span data-ttu-id="9c890-133">Modificare hello **server.js** tooremove uno di hello '.' hello seguente riga di caratteri.</span><span class="sxs-lookup"><span data-stu-id="9c890-133">Modify hello **server.js** tooremove one of hello '.' characters from hello following line.</span></span>
   
       var app = require('../app');
   
   <span data-ttu-id="9c890-134">Dopo aver apportato questa modifica, la riga hello compariranno come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="9c890-134">After making this modification, hello line should appear as follows.</span></span>
   
       var app = require('./app');
   
   <span data-ttu-id="9c890-135">Questa modifica è necessaria perché il file hello è spostato (in precedenza **bin/www**,) toohello stessa directory del file app hello è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="9c890-135">This change is required since we moved hello file (formerly **bin/www**,) toohello same directory as hello app file being required.</span></span> <span data-ttu-id="9c890-136">Dopo aver apportato questa modifica, Salva hello **server.js** file.</span><span class="sxs-lookup"><span data-stu-id="9c890-136">After making this change, save hello **server.js** file.</span></span>
6. <span data-ttu-id="9c890-137">Comando che segue di hello utilizzare un'applicazione hello toorun in hello dell'emulatore di Azure:</span><span class="sxs-lookup"><span data-stu-id="9c890-137">Use hello following command toorun hello application in hello Azure emulator:</span></span>
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Una pagina web contenente tooexpress iniziale.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-hello-view"></a><span data-ttu-id="9c890-139">Modifica vista hello</span><span class="sxs-lookup"><span data-stu-id="9c890-139">Modifying hello View</span></span>
<span data-ttu-id="9c890-140">A questo punto, modificare il messaggio hello vista toodisplay hello "TooExpress benvenuto in Azure".</span><span class="sxs-lookup"><span data-stu-id="9c890-140">Now modify hello view toodisplay hello message "Welcome tooExpress in Azure".</span></span>

1. <span data-ttu-id="9c890-141">Immettere i seguenti file di comando tooopen hello index.jade hello:</span><span class="sxs-lookup"><span data-stu-id="9c890-141">Enter hello following command tooopen hello index.jade file:</span></span>
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![contenuto di Hello del file index.jade hello.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   <span data-ttu-id="9c890-143">Jade è di tipo motore di visualizzazione predefinito hello utilizzato dalle applicazioni di Express.</span><span class="sxs-lookup"><span data-stu-id="9c890-143">Jade is hello default view engine used by Express applications.</span></span> <span data-ttu-id="9c890-144">Per ulteriori informazioni sul motore di visualizzazione Jade hello, vedere [http://jade-lang.com][http://jade-lang.com].</span><span class="sxs-lookup"><span data-stu-id="9c890-144">For more information on hello Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span></span>
2. <span data-ttu-id="9c890-145">Modificare l'ultima riga di hello del testo aggiungendo **in Azure**.</span><span class="sxs-lookup"><span data-stu-id="9c890-145">Modify hello last line of text by appending **in Azure**.</span></span>
   
   ![legge i file index.jade Hello, ultima riga hello: p benvenuto troppo\#{title} in Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. <span data-ttu-id="9c890-147">Salvare il file di hello e chiudere Blocco note.</span><span class="sxs-lookup"><span data-stu-id="9c890-147">Save hello file and exit Notepad.</span></span>
4. <span data-ttu-id="9c890-148">Aggiornare il tuo browser per vedere le modifiche.</span><span class="sxs-lookup"><span data-stu-id="9c890-148">Refresh your browser and you will see your changes.</span></span>
   
   ![Una finestra del browser, pagina hello contiene tooExpress benvenuto in Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

<span data-ttu-id="9c890-150">Dopo l'applicazione hello test, utilizzare hello **Stop AzureEmulator** dell'emulatore di cmdlet toostop hello.</span><span class="sxs-lookup"><span data-stu-id="9c890-150">After testing hello application, use hello **Stop-AzureEmulator** cmdlet toostop hello emulator.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="9c890-151">Pubblicazione hello applicazione tooAzure</span><span class="sxs-lookup"><span data-stu-id="9c890-151">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="9c890-152">Nella finestra di PowerShell Azure hello, utilizzare hello **pubblica AzureServiceProject** servizio cloud di cmdlet toodeploy hello applicazione tooa</span><span class="sxs-lookup"><span data-stu-id="9c890-152">In hello Azure PowerShell window, use hello **Publish-AzureServiceProject** cmdlet toodeploy hello application tooa cloud service</span></span>

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

<span data-ttu-id="9c890-153">Al termine dell'operazione di distribuzione hello, il browser verrà aprire e visualizzare la pagina web hello.</span><span class="sxs-lookup"><span data-stu-id="9c890-153">Once hello deployment operation completes, your browser will open and display hello web page.</span></span>

![Un web browser visualizzazione pagina Express hello.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a><span data-ttu-id="9c890-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9c890-156">Next steps</span></span>
<span data-ttu-id="9c890-157">Per ulteriori informazioni, vedere hello [Centro per sviluppatori di Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="9c890-157">For more information, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


