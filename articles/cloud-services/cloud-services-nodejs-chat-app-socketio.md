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
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a><span data-ttu-id="df7f3-103">Creazione di un'applicazione di chat Node.js con Socket.IO in un servizio cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="df7f3-103">Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service</span></span>
<span data-ttu-id="df7f3-104">Socket.IO fornisce comunicazioni in tempo reale tra il server node.js e i client.</span><span class="sxs-lookup"><span data-stu-id="df7f3-104">Socket.IO provides realtime communication between between your node.js server and clients.</span></span> <span data-ttu-id="df7f3-105">In questa esercitazione verrà illustrato l'hosting di un'applicazione di chat basata su socket.IO in Azure.</span><span class="sxs-lookup"><span data-stu-id="df7f3-105">This tutorial will walk you through hosting a socket.IO based chat application on Azure.</span></span> <span data-ttu-id="df7f3-106">Per altre informazioni su Socket.IO, vedere <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="df7f3-106">For more information on Socket.IO, see <http://socket.io/>.</span></span>

<span data-ttu-id="df7f3-107">Di seguito viene riportata una schermata dell'applicazione hello completata:</span><span class="sxs-lookup"><span data-stu-id="df7f3-107">A screenshot of hello completed application is below:</span></span>

![Una finestra del browser visualizzazione servizio hello ospitato in Azure][completed-app]  

## <a name="prerequisites"></a><span data-ttu-id="df7f3-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="df7f3-109">Prerequisites</span></span>
<span data-ttu-id="df7f3-110">Verificare che hello i seguenti prodotti e le versioni sono installate toosuccessfully hello completo esempio in questo articolo:</span><span class="sxs-lookup"><span data-stu-id="df7f3-110">Ensure that hello following products and versions are installed toosuccessfully complete hello example in this article:</span></span>

* <span data-ttu-id="df7f3-111">Installare [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="df7f3-111">Install [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span></span>
* <span data-ttu-id="df7f3-112">Installare [Node.js](https://nodejs.org/download/)</span><span class="sxs-lookup"><span data-stu-id="df7f3-112">Install [Node.js](https://nodejs.org/download/)</span></span>
* <span data-ttu-id="df7f3-113">Installare [Python versione 2.7.10](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="df7f3-113">Install [Python version 2.7.10](https://www.python.org/)</span></span>

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="df7f3-114">Creazione di un progetto di servizio cloud</span><span class="sxs-lookup"><span data-stu-id="df7f3-114">Create a Cloud Service Project</span></span>
<span data-ttu-id="df7f3-115">Hello i passaggi seguenti Crea progetto di servizio cloud hello che ospiterà l'applicazione Socket.IO hello.</span><span class="sxs-lookup"><span data-stu-id="df7f3-115">hello following steps create hello cloud service project that will host hello Socket.IO application.</span></span>

1. <span data-ttu-id="df7f3-116">Da hello **Menu Start** o **schermata Start**, cercare **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="df7f3-116">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="df7f3-117">Fare infine clic con il pulsante destro del mouse su **Windows PowerShell** e scegliere **Esegui come amministratore**.</span><span class="sxs-lookup"><span data-stu-id="df7f3-117">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Icona di Azure PowerShell][powershell-menu]
2. <span data-ttu-id="df7f3-119">Creare una directory denominata **c:\\node**.</span><span class="sxs-lookup"><span data-stu-id="df7f3-119">Create a directory called **c:\\node**.</span></span> 
   
        PS C:\> md node
3. <span data-ttu-id="df7f3-120">Modificare le directory toohello **c:\\nodo** directory</span><span class="sxs-lookup"><span data-stu-id="df7f3-120">Change directories toohello **c:\\node** directory</span></span>
   
        PS C:\> cd node
4. <span data-ttu-id="df7f3-121">Immettere i seguenti comandi toocreate una nuova soluzione denominata hello **chatapp** e un ruolo di lavoro denominato **WorkerRole1**:</span><span class="sxs-lookup"><span data-stu-id="df7f3-121">Enter hello following commands toocreate a new solution named **chatapp** and a worker role named **WorkerRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    <span data-ttu-id="df7f3-122">Verrà visualizzato hello seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="df7f3-122">You will see hello following response:</span></span>
   
    ![output di Hello del nuovo hello-azureservice e azurenodeworkerrolecmdlets aggiungere](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-hello-chat-example"></a><span data-ttu-id="df7f3-124">Scaricare l'esempio Chat hello</span><span class="sxs-lookup"><span data-stu-id="df7f3-124">Download hello Chat Example</span></span>
<span data-ttu-id="df7f3-125">Per questo progetto, si utilizzerà l'esempio di chat hello dalla hello [repository Socket.IO GitHub].</span><span class="sxs-lookup"><span data-stu-id="df7f3-125">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="df7f3-126">Eseguire l'esempio hello toodownload di passaggi seguente hello e aggiungerla toohello progetto creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df7f3-126">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="df7f3-127">Creare una copia locale del repository hello utilizzando hello **Clone** pulsante.</span><span class="sxs-lookup"><span data-stu-id="df7f3-127">Create a local copy of hello repository by using hello **Clone** button.</span></span> <span data-ttu-id="df7f3-128">È inoltre possibile utilizzare hello **ZIP** progetto hello toodownload di button.</span><span class="sxs-lookup"><span data-stu-id="df7f3-128">You may also use hello **ZIP** button toodownload hello project.</span></span>
   
   ![Una finestra del browser visualizzazione https://github.com/LearnBoost/socket.io/tree/master/examples/chat, con icona di download ZIP hello evidenziato][chat-example-view]
2. <span data-ttu-id="df7f3-130">Esplorare la struttura di directory hello del repository locale hello fino a giungere al hello **esempi\\chat** directory.</span><span class="sxs-lookup"><span data-stu-id="df7f3-130">Navigate hello directory structure of hello local repository until you arrive at hello **examples\\chat** directory.</span></span> <span data-ttu-id="df7f3-131">Copiare il contenuto di hello del toothe directory **c:\\nodo\\chatapp\\WorkerRole1** directory creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="df7f3-131">Copy hello contents of this directory toothe **C:\\node\\chatapp\\WorkerRole1** directory created earlier.</span></span>
   
   ![Soluzioni, visualizzazione contenuto hello degli esempi di hello\\directory chat estratti dall'archivio hello][chat-contents]
   
   <span data-ttu-id="df7f3-133">gli elementi evidenziati nella schermata di hello precedente Hello sono file hello copiati dal hello **esempi\\chat** directory</span><span class="sxs-lookup"><span data-stu-id="df7f3-133">hello highlighted items in hello screenshot above are hello files copied from hello **examples\\chat** directory</span></span>
3. <span data-ttu-id="df7f3-134">In hello **c:\\nodo\\chatapp\\WorkerRole1** directory, hello di eliminazione **server.js** file e quindi rinominare hello **app.js**file troppo**server.js**.</span><span class="sxs-lookup"><span data-stu-id="df7f3-134">In hello **C:\\node\\chatapp\\WorkerRole1** directory, delete hello **server.js** file, and then rename hello **app.js** file too**server.js**.</span></span> <span data-ttu-id="df7f3-135">Questa operazione rimuove predefinito hello **server.js** file creato in precedenza da hello **Add-AzureNodeWorkerRole** cmdlet e sostituire con un'applicazione hello file hello esempio chat.</span><span class="sxs-lookup"><span data-stu-id="df7f3-135">This removes hello default **server.js** file created previously by hello **Add-AzureNodeWorkerRole** cmdlet and replaces it with hello application file from hello chat example.</span></span>

### <a name="modify-serverjs-and-install-modules"></a><span data-ttu-id="df7f3-136">Modificare Server.js e installare i moduli</span><span class="sxs-lookup"><span data-stu-id="df7f3-136">Modify Server.js and Install Modules</span></span>
<span data-ttu-id="df7f3-137">Prima di un'applicazione hello test in hello dell'emulatore di Azure, è necessario apportare alcune modifiche minori.</span><span class="sxs-lookup"><span data-stu-id="df7f3-137">Before testing hello application in hello Azure emulator, we must make some minor modifications.</span></span> <span data-ttu-id="df7f3-138">Eseguire i seguenti passaggi toothe server.js file hello:</span><span class="sxs-lookup"><span data-stu-id="df7f3-138">Perform hello following steps toothe server.js file:</span></span>

1. <span data-ttu-id="df7f3-139">Aprire hello **server.js** file in Visual Studio o qualsiasi editor di testo.</span><span class="sxs-lookup"><span data-stu-id="df7f3-139">Open hello **server.js** file in Visual Studio or any text editor.</span></span>
2. <span data-ttu-id="df7f3-140">Trovare hello **le dipendenze del modulo** sezione all'inizio di hello di server.js e modificare hello riga contenente **poi = require('.. //.. LIB//socket.IO')** troppo**poi = require('socket.io')** come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="df7f3-140">Find hello **Module dependencies** section at hello beginning of server.js and change hello line containing **sio = require('..//..//lib//socket.io')** too**sio = require('socket.io')** as shown below:</span></span>
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. <span data-ttu-id="df7f3-141">un'applicazione hello tooensure in ascolto sulla porta corretta di hello, aprire server.js in blocco note o l'editor preferito e quindi modificare la riga seguente, sostituendo **3000** con **process.env.port** come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="df7f3-141">tooensure hello application listens on hello correct port, open server.js in Notepad or your favorite editor, and then change the following line by replacing **3000** with **process.env.port** as shown below:</span></span>
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

<span data-ttu-id="df7f3-142">Dopo aver salvato le modifiche di hello troppo**server.js**, utilizzare hello alla procedura seguente per installare i moduli necessari e quindi testare l'applicazione hello nell'emulatore di Azure:</span><span class="sxs-lookup"><span data-stu-id="df7f3-142">After saving hello changes too**server.js**, use hello following steps to install required modules, and then test hello application in the Azure emulator:</span></span>

1. <span data-ttu-id="df7f3-143">Utilizzando **Azure PowerShell**, modificare le directory toohello **c:\\nodo\\chatapp\\WorkerRole1** hello directory e l'utilizzo successivo comando tooinstall hello moduli necessari per questa applicazione:</span><span class="sxs-lookup"><span data-stu-id="df7f3-143">Using **Azure PowerShell**, change directories toohello **C:\\node\\chatapp\\WorkerRole1** directory and use hello following command tooinstall hello modules required by this application:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   <span data-ttu-id="df7f3-144">Verranno installati i moduli di hello elencati nel file package. JSON hello.</span><span class="sxs-lookup"><span data-stu-id="df7f3-144">This will install hello modules listed in hello package.json file.</span></span> <span data-ttu-id="df7f3-145">Al termine del comando di hello, verrà visualizzato il seguente toothe simili di output:</span><span class="sxs-lookup"><span data-stu-id="df7f3-145">After hello command completes, you should see output similar toothe following:</span></span>
   
   ![comando di installazione di output di Hello di hello npm][The-output-of-the-npm-install-command]
2. <span data-ttu-id="df7f3-147">Poiché in questo esempio è stato originariamente parte di hello repository Socket.IO GitHub e direttamente a cui fa riferimento libreria Socket.IO hello percorso relativo, Socket.IO non esiste alcun riferimento nel file package. JSON hello, pertanto è necessario installarlo eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="df7f3-147">Since this example was originally a part of hello Socket.IO GitHub repository, and directly referenced hello Socket.IO library by relative path, Socket.IO was not referenced in hello package.json file, so we must install it by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a><span data-ttu-id="df7f3-148">Test e distribuzione</span><span class="sxs-lookup"><span data-stu-id="df7f3-148">Test and Deploy</span></span>
1. <span data-ttu-id="df7f3-149">Avviare l'emulatore hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="df7f3-149">Launch hello emulator by issuing hello following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > <span data-ttu-id="df7f3-150">Se si verificano problemi con l'avvio dell'emulatore, ad esempio Start-AzureEmulator: Errore imprevisto.</span><span class="sxs-lookup"><span data-stu-id="df7f3-150">If you encounter issues with launching emulator, eg.: Start-AzureEmulator : An unexpected failure occurred.</span></span>  <span data-ttu-id="df7f3-151">Dettagli: Rilevato un errore imprevisto hello oggetto di comunicazione System.ServiceModel.Channels.ServiceChannel, non utilizzabile per la comunicazione perché è nello stato Faulted hello.</span><span class="sxs-lookup"><span data-stu-id="df7f3-151">Details: Encountered an unexpected error hello communication object,  System.ServiceModel.Channels.ServiceChannel, cannot be used for communication because it is in hello Faulted state.</span></span>
   
      <span data-ttu-id="df7f3-152">reinstallare AzureAuthoringTools 2.7.1 e AzureComputeEmulator 2.7 - verificare che la versione corrisponda.</span><span class="sxs-lookup"><span data-stu-id="df7f3-152">reinstall AzureAuthoringTools v 2.7.1 and AzureComputeEmulator v 2.7 - make sure that version matches.</span></span>
   >
   >


2. <span data-ttu-id="df7f3-153">Aprire un browser e andare troppo**http://127.0.0.1**.</span><span class="sxs-lookup"><span data-stu-id="df7f3-153">Open a browser and navigate too**http://127.0.0.1**.</span></span>
3. <span data-ttu-id="df7f3-154">Quando viene visualizzata una finestra hello, immettere un nome alternativo e quindi premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="df7f3-154">When hello browser window opens, enter a nickname and then hit enter.</span></span>
   <span data-ttu-id="df7f3-155">In questo modo si toopost messaggi come un nome alternativo specifico.</span><span class="sxs-lookup"><span data-stu-id="df7f3-155">This will allow you toopost messages as a specific nickname.</span></span> <span data-ttu-id="df7f3-156">funzionalità multiutente tootest, aprire finestre del browser aggiuntive utilizzando lo stesso URL e immettere i nomi alternativi diversi.</span><span class="sxs-lookup"><span data-stu-id="df7f3-156">tootest multi-user functionality, open additional browser windows using the same URL and enter different nicknames.</span></span>
   
   ![Due finestre del browser con i messaggi della chat di User1 e User2](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. <span data-ttu-id="df7f3-158">Dopo l'applicazione hello test, arrestare l'emulatore hello eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="df7f3-158">After testing hello application, stop hello emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. <span data-ttu-id="df7f3-159">toodeploy hello applicazione tooAzure, utilizzare il **pubblica AzureServiceProject** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="df7f3-159">toodeploy hello application tooAzure, use the **Publish-AzureServiceProject** cmdlet.</span></span> <span data-ttu-id="df7f3-160">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="df7f3-160">For example:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > <span data-ttu-id="df7f3-161">Essere toouse che un nome univoco, in caso contrario hello processo di pubblicazione avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="df7f3-161">Be sure toouse a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="df7f3-162">Una volta completata la distribuzione di hello, hello browser aprire e passare servizio toohello distribuito.</span><span class="sxs-lookup"><span data-stu-id="df7f3-162">After hello deployment has completed, hello browser will open and navigate toohello deployed service.</span></span>
   > 
   > <span data-ttu-id="df7f3-163">Se si riceve un errore indicante che hello fornito nome della sottoscrizione non esiste in hello importato profilo di pubblicazione, è necessario scaricare e importare il profilo di pubblicazione hello per la sottoscrizione prima della distribuzione tooAzure.</span><span class="sxs-lookup"><span data-stu-id="df7f3-163">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="df7f3-164">Vedere hello **distribuzione tooAzure applicazione hello** sezione [compilare e distribuire un tooan applicazione Node.js servizio Cloud di Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="df7f3-164">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 
   
   ![Una finestra del browser visualizzazione servizio hello ospitato in Azure][completed-app]
   
   > [!NOTE]
   > <span data-ttu-id="df7f3-166">Se si riceve un errore indicante che hello fornito nome della sottoscrizione non esiste in hello importato profilo di pubblicazione, è necessario scaricare e importare il profilo di pubblicazione hello per la sottoscrizione prima della distribuzione tooAzure.</span><span class="sxs-lookup"><span data-stu-id="df7f3-166">If you receive an error stating that hello provided subscription name doesn't exist in hello imported publish profile, you must download and import hello publishing profile for your subscription before deploying tooAzure.</span></span> <span data-ttu-id="df7f3-167">Vedere hello **distribuzione tooAzure applicazione hello** sezione [compilare e distribuire un tooan applicazione Node.js servizio Cloud di Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="df7f3-167">See hello **Deploying hello Application tooAzure** section of [Build and deploy a Node.js application tooan Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 

<span data-ttu-id="df7f3-168">L'applicazione è ora in esecuzione in Azure ed è in grado di inoltrare i messaggi di chat tra diversi client tramite Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="df7f3-168">Your application is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

> [!NOTE]
> <span data-ttu-id="df7f3-169">Per semplicità, in questo esempio viene limitato toochatting tra gli utenti connessi toohello stessa istanza.</span><span class="sxs-lookup"><span data-stu-id="df7f3-169">For simplicity, this sample is limited toochatting between users connected toohello same instance.</span></span> <span data-ttu-id="df7f3-170">Ciò significa che se il servizio cloud hello crea due istanze del ruolo di lavoro, gli utenti potranno solo toochat con altri utenti connessi toohello stessa istanza del ruolo worker.</span><span class="sxs-lookup"><span data-stu-id="df7f3-170">This means that if hello cloud service creates two worker role instances, users will only be able toochat with others connected toohello same worker role instance.</span></span> <span data-ttu-id="df7f3-171">tooscale hello applicazione toowork con più istanze del ruolo, è possibile utilizzare una tecnologia simile Bus di servizio tooshare hello Socket.IO archiviare lo stato tra più istanze.</span><span class="sxs-lookup"><span data-stu-id="df7f3-171">tooscale hello application toowork with multiple role instances, you could use a technology like Service Bus tooshare hello Socket.IO store state across instances.</span></span> <span data-ttu-id="df7f3-172">Per esempi, vedere esempi di utilizzo di argomenti e code del Bus di servizio hello in hello [Azure SDK per Node.js GitHub repository](https://github.com/WindowsAzure/azure-sdk-for-node).</span><span class="sxs-lookup"><span data-stu-id="df7f3-172">For examples, see hello Service Bus Queues and Topics usage samples in hello [Azure SDK for Node.js GitHub repository](https://github.com/WindowsAzure/azure-sdk-for-node).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="df7f3-173">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="df7f3-173">Next steps</span></span>
<span data-ttu-id="df7f3-174">In questa esercitazione è stato descritto come toocreate un'applicazione di chat base ospitato in un servizio Cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="df7f3-174">In this tutorial you learned how toocreate a basic chat application hosted in an Azure Cloud Service.</span></span> <span data-ttu-id="df7f3-175">toolearn come toohost questa applicazione in un sito Web di Azure, vedere [compilare un'applicazione di Chat Node.js con Socket.IO sul sito Web di Azure][chatwebsite].</span><span class="sxs-lookup"><span data-stu-id="df7f3-175">toolearn how toohost this application in an Azure Website, see [Build a Node.js Chat Application with Socket.IO on an Azure Web Site][chatwebsite].</span></span>

<span data-ttu-id="df7f3-176">Per ulteriori informazioni, vedere anche hello [Centro per sviluppatori di Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="df7f3-176">For more information, see also hello [Node.js Developer Center](/develop/nodejs/).</span></span>

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


