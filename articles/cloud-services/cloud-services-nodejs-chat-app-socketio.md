---
title: Applicazione Node.js con Socket.io | Documentazione Microsoft
description: Informazioni su come usare socket.io in un'applicazione node.js ospitata in Azure.
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
ms.openlocfilehash: a85d4348a13b79b5b7542362de9956aa3398375a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a><span data-ttu-id="ac1ac-103">Creazione di un'applicazione di chat Node.js con Socket.IO in un servizio cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="ac1ac-103">Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service</span></span>
<span data-ttu-id="ac1ac-104">Socket.IO fornisce comunicazioni in tempo reale tra il server node.js e i client.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-104">Socket.IO provides realtime communication between between your node.js server and clients.</span></span> <span data-ttu-id="ac1ac-105">In questa esercitazione verrà illustrato l'hosting di un'applicazione di chat basata su socket.IO in Azure.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-105">This tutorial will walk you through hosting a socket.IO based chat application on Azure.</span></span> <span data-ttu-id="ac1ac-106">Per altre informazioni su Socket.IO, vedere <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-106">For more information on Socket.IO, see <http://socket.io/>.</span></span>

<span data-ttu-id="ac1ac-107">Di seguito è riportata una schermata dell'applicazione completata:</span><span class="sxs-lookup"><span data-stu-id="ac1ac-107">A screenshot of the completed application is below:</span></span>

![Finestra del browser con il servizio ospitato in Azure][completed-app]  

## <a name="prerequisites"></a><span data-ttu-id="ac1ac-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ac1ac-109">Prerequisites</span></span>
<span data-ttu-id="ac1ac-110">Assicurarsi che i seguenti prodotti e versioni siano installati per completare correttamente l'esempio in questo articolo:</span><span class="sxs-lookup"><span data-stu-id="ac1ac-110">Ensure that the following products and versions are installed to successfully complete the example in this article:</span></span>

* <span data-ttu-id="ac1ac-111">Installare [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span><span class="sxs-lookup"><span data-stu-id="ac1ac-111">Install [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)</span></span>
* <span data-ttu-id="ac1ac-112">Installare [Node.js](https://nodejs.org/download/)</span><span class="sxs-lookup"><span data-stu-id="ac1ac-112">Install [Node.js](https://nodejs.org/download/)</span></span>
* <span data-ttu-id="ac1ac-113">Installare [Python versione 2.7.10](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="ac1ac-113">Install [Python version 2.7.10](https://www.python.org/)</span></span>

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="ac1ac-114">Creazione di un progetto di servizio cloud</span><span class="sxs-lookup"><span data-stu-id="ac1ac-114">Create a Cloud Service Project</span></span>
<span data-ttu-id="ac1ac-115">Eseguire le operazioni seguenti per creare il progetto servizio cloud che ospiterà l'applicazione Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-115">The following steps create the cloud service project that will host the Socket.IO application.</span></span>

1. <span data-ttu-id="ac1ac-116">Nel **menu Start** o nella **schermata Start** cercare **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-116">From the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="ac1ac-117">Fare infine clic con il pulsante destro del mouse su **Windows PowerShell** e scegliere **Esegui come amministratore**.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-117">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Icona di Azure PowerShell][powershell-menu]
2. <span data-ttu-id="ac1ac-119">Creare una directory denominata **c:\\node**.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-119">Create a directory called **c:\\node**.</span></span> 
   
        PS C:\> md node
3. <span data-ttu-id="ac1ac-120">Passare alla directory **c:\\node**.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-120">Change directories to the **c:\\node** directory</span></span>
   
        PS C:\> cd node
4. <span data-ttu-id="ac1ac-121">Immettere i comandi seguenti per creare una nuova soluzione denominata **chatapp** e un ruolo di lavoro denominato **WorkerRole1**:</span><span class="sxs-lookup"><span data-stu-id="ac1ac-121">Enter the following commands to create a new solution named **chatapp** and a worker role named **WorkerRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    <span data-ttu-id="ac1ac-122">Verrà visualizzata la risposta seguente:</span><span class="sxs-lookup"><span data-stu-id="ac1ac-122">You will see the following response:</span></span>
   
    ![Output dei cmdlet new-azureservice e add-azurenodeworkerrole](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-the-chat-example"></a><span data-ttu-id="ac1ac-124">Download dell'esempio di chat</span><span class="sxs-lookup"><span data-stu-id="ac1ac-124">Download the Chat Example</span></span>
<span data-ttu-id="ac1ac-125">Per questo progetto, verrà usato l'esempio di chat dell' [archivio GitHub Socket.IO].</span><span class="sxs-lookup"><span data-stu-id="ac1ac-125">For this project, we will use the chat example from the [Socket.IO GitHub repository].</span></span> <span data-ttu-id="ac1ac-126">Eseguire la procedura seguente per scaricare l'esempio e aggiungerlo al progetto creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-126">Perform the following steps to download the example and add it to the project you previously created.</span></span>

1. <span data-ttu-id="ac1ac-127">Creare una copia locale dell'archivio usando il pulsante **Clone** .</span><span class="sxs-lookup"><span data-stu-id="ac1ac-127">Create a local copy of the repository by using the **Clone** button.</span></span> <span data-ttu-id="ac1ac-128">È inoltre possibile usare il pulsante **ZIP** per scaricare il progetto.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-128">You may also use the **ZIP** button to download the project.</span></span>
   
   ![Finestra del browser con https://github.com/LearnBoost/socket.io/tree/master/examples/chat e l'icona per il download di ZIP evidenziata][chat-example-view]
2. <span data-ttu-id="ac1ac-130">Spostarsi nella struttura di directory del repository locale fino alla directory **examples\\chat**.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-130">Navigate the directory structure of the local repository until you arrive at the **examples\\chat** directory.</span></span> <span data-ttu-id="ac1ac-131">Copiare il contenuto di questa directory nella directory **C:\\node\\chatapp\\WorkerRole1** creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-131">Copy the contents of this directory to the **C:\\node\\chatapp\\WorkerRole1** directory created earlier.</span></span>
   
   ![Esplora risorse con il contenuto della directory examples\\chat estratto dall'archivio][chat-contents]
   
   <span data-ttu-id="ac1ac-133">Gli elementi evidenziati nello screenshot precedente sono i file copiati dalla directory **examples\\chat**.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-133">The highlighted items in the screenshot above are the files copied from the **examples\\chat** directory</span></span>
3. <span data-ttu-id="ac1ac-134">Nella directory **C:\\node\\chatapp\\WorkerRole1** eliminare il file **server.js** e quindi rinominare il file **app.js** in **server.js**.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-134">In the **C:\\node\\chatapp\\WorkerRole1** directory, delete the **server.js** file, and then rename the **app.js** file to **server.js**.</span></span> <span data-ttu-id="ac1ac-135">Il file **server.js** predefinito creato in precedenza dal cmdlet **Add-AzureNodeWorkerRole** verrà così rimosso e sostituito con il file dell'applicazione dell'esempio di chat.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-135">This removes the default **server.js** file created previously by the **Add-AzureNodeWorkerRole** cmdlet and replaces it with the application file from the chat example.</span></span>

### <a name="modify-serverjs-and-install-modules"></a><span data-ttu-id="ac1ac-136">Modificare Server.js e installare i moduli</span><span class="sxs-lookup"><span data-stu-id="ac1ac-136">Modify Server.js and Install Modules</span></span>
<span data-ttu-id="ac1ac-137">Prima di testare l'applicazione nell'emulatore di Azure, è necessario apportare alcune piccole modifiche.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-137">Before testing the application in the Azure emulator, we must make some minor modifications.</span></span> <span data-ttu-id="ac1ac-138">Eseguire la procedura seguente per il file server.js:</span><span class="sxs-lookup"><span data-stu-id="ac1ac-138">Perform the following steps to the server.js file:</span></span>

1. <span data-ttu-id="ac1ac-139">Aprire il file **server. js** in Visual Studio o qualsiasi altro editor di testo.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-139">Open the **server.js** file in Visual Studio or any text editor.</span></span>
2. <span data-ttu-id="ac1ac-140">Trovare la sezione **Module dependencies** all'inizio del file server.js e sostituire la riga contenente **sio = require('..//..//lib//socket.io')** con **sio = require('socket.io')**, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="ac1ac-140">Find the **Module dependencies** section at the beginning of server.js and change the line containing **sio = require('..//..//lib//socket.io')** to **sio = require('socket.io')** as shown below:</span></span>
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. <span data-ttu-id="ac1ac-141">Per assicurarsi che l'applicazione resti in ascolto sulla porta corretta, aprire il file server.js nel Blocco note o in un altro editor di testo e quindi modificare la riga seguente sostituendo **3000** con **process.env.port**, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="ac1ac-141">To ensure the application listens on the correct port, open server.js in Notepad or your favorite editor, and then change the following line by replacing **3000** with **process.env.port** as shown below:</span></span>
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

<span data-ttu-id="ac1ac-142">Dopo aver salvato le modifiche apportate al file **server.js**, eseguire la procedura seguente per installare i moduli necessari, quindi testare l'applicazione nell'emulatore di Azure:</span><span class="sxs-lookup"><span data-stu-id="ac1ac-142">After saving the changes to **server.js**, use the following steps to install required modules, and then test the application in the Azure emulator:</span></span>

1. <span data-ttu-id="ac1ac-143">Con **Azure PowerShell** passare alla directory **C:\\node\\chatapp\\WorkerRole1** e usare il comando seguente per installare i moduli necessari per l'applicazione:</span><span class="sxs-lookup"><span data-stu-id="ac1ac-143">Using **Azure PowerShell**, change directories to the **C:\\node\\chatapp\\WorkerRole1** directory and use the following command to install the modules required by this application:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   <span data-ttu-id="ac1ac-144">Verranno installati i moduli elencati nel file package.json.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-144">This will install the modules listed in the package.json file.</span></span> <span data-ttu-id="ac1ac-145">Dopo il completamento del comando, l'output dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="ac1ac-145">After the command completes, you should see output similar to the following:</span></span>
   
   ![Output del comando npm install][The-output-of-the-npm-install-command]
2. <span data-ttu-id="ac1ac-147">Poiché l'esempio in origine faceva parte dell'archivio GitHub Socket.IO e faceva riferimento direttamente alla libreria Socket.IO mediante percorso relativo, a Socket.IO non viene fatto riferimento nel file package.json, quindi è necessario installarlo immettendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ac1ac-147">Since this example was originally a part of the Socket.IO GitHub repository, and directly referenced the Socket.IO library by relative path, Socket.IO was not referenced in the package.json file, so we must install it by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a><span data-ttu-id="ac1ac-148">Test e distribuzione</span><span class="sxs-lookup"><span data-stu-id="ac1ac-148">Test and Deploy</span></span>
1. <span data-ttu-id="ac1ac-149">Avviare l'emulatore immettendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ac1ac-149">Launch the emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > <span data-ttu-id="ac1ac-150">Se si verificano problemi con l'avvio dell'emulatore, ad esempio Start-AzureEmulator: Errore imprevisto.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-150">If you encounter issues with launching emulator, eg.: Start-AzureEmulator : An unexpected failure occurred.</span></span>  <span data-ttu-id="ac1ac-151">Dettagli: Errore imprevisto Impossibile utilizzare l'oggetto di comunicazione, System.ServiceModel.Channels.ServiceChannel per la comunicazione perché è nello stato Faulted.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-151">Details: Encountered an unexpected error The communication object,  System.ServiceModel.Channels.ServiceChannel, cannot be used for communication because it is in the Faulted state.</span></span>
   
      <span data-ttu-id="ac1ac-152">reinstallare AzureAuthoringTools 2.7.1 e AzureComputeEmulator 2.7 - verificare che la versione corrisponda.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-152">reinstall AzureAuthoringTools v 2.7.1 and AzureComputeEmulator v 2.7 - make sure that version matches.</span></span>
   >
   >


2. <span data-ttu-id="ac1ac-153">Aprire un browser e passare a **http://127.0.0.1**.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-153">Open a browser and navigate to **http://127.0.0.1**.</span></span>
3. <span data-ttu-id="ac1ac-154">Quando si apre la finestra del browser, immettere un nome alternativo e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-154">When the browser window opens, enter a nickname and then hit enter.</span></span>
   <span data-ttu-id="ac1ac-155">In questo modo sarà possibile inviare messaggi con un nome alternativo specifico.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-155">This will allow you to post messages as a specific nickname.</span></span> <span data-ttu-id="ac1ac-156">Per testare la funzionalità multiutente, aprire altre finestre del browser usando lo stesso URL e immettere nomi alternativi diversi.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-156">To test multi-user functionality, open additional browser windows using the same URL and enter different nicknames.</span></span>
   
   ![Due finestre del browser con i messaggi della chat di User1 e User2](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. <span data-ttu-id="ac1ac-158">Dopo aver testato l'applicazione, immettere il comando seguente per interrompere l'emulatore:</span><span class="sxs-lookup"><span data-stu-id="ac1ac-158">After testing the application, stop the emulator by issuing the following command:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. <span data-ttu-id="ac1ac-159">Per distribuire l'applicazione in Azure, usare il cmdlet **Publish-AzureServiceProject**.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-159">To deploy the application to Azure, use the **Publish-AzureServiceProject** cmdlet.</span></span> <span data-ttu-id="ac1ac-160">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ac1ac-160">For example:</span></span>
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > <span data-ttu-id="ac1ac-161">Assicurarsi di usare un nome univoco, in caso contrario il processo di pubblicazione avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-161">Be sure to use a unique name, otherwise the publish process will fail.</span></span> <span data-ttu-id="ac1ac-162">Al termine della distribuzione, verrà visualizzata una finestra del browser che consente di passare al servizio distribuito.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-162">After the deployment has completed, the browser will open and navigate to the deployed service.</span></span>
   > 
   > <span data-ttu-id="ac1ac-163">Se viene visualizzato un messaggio di errore indicante che il nome della sottoscrizione specificato non esiste nel profilo di pubblicazione importato, è necessario scaricare e importare il profilo di pubblicazione per la sottoscrizione prima della distribuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-163">If you receive an error stating that the provided subscription name doesn't exist in the imported publish profile, you must download and import the publishing profile for your subscription before deploying to Azure.</span></span> <span data-ttu-id="ac1ac-164">Vedere la sezione **Distribuzione dell'applicazione in Azure** dell'argomento [Creazione e distribuzione di un'applicazione Node.js in un servizio cloud di Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="ac1ac-164">See the **Deploying the Application to Azure** section of [Build and deploy a Node.js application to an Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 
   
   ![Finestra del browser con il servizio ospitato in Azure][completed-app]
   
   > [!NOTE]
   > <span data-ttu-id="ac1ac-166">Se viene visualizzato un messaggio di errore indicante che il nome della sottoscrizione specificato non esiste nel profilo di pubblicazione importato, è necessario scaricare e importare il profilo di pubblicazione per la sottoscrizione prima della distribuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-166">If you receive an error stating that the provided subscription name doesn't exist in the imported publish profile, you must download and import the publishing profile for your subscription before deploying to Azure.</span></span> <span data-ttu-id="ac1ac-167">Vedere la sezione **Distribuzione dell'applicazione in Azure** dell'argomento [Creazione e distribuzione di un'applicazione Node.js in un servizio cloud di Azure](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span><span class="sxs-lookup"><span data-stu-id="ac1ac-167">See the **Deploying the Application to Azure** section of [Build and deploy a Node.js application to an Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)</span></span>
   > 
   > 

<span data-ttu-id="ac1ac-168">L'applicazione è ora in esecuzione in Azure ed è in grado di inoltrare i messaggi di chat tra diversi client tramite Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-168">Your application is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

> [!NOTE]
> <span data-ttu-id="ac1ac-169">Per semplicità, in questo esempio viene illustrata solo la chat tra utenti connessi alla stessa istanza.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-169">For simplicity, this sample is limited to chatting between users connected to the same instance.</span></span> <span data-ttu-id="ac1ac-170">Questo significa che se il servizio cloud crea due istanze del ruolo di lavoro, gli utenti saranno in grado di comunicare solo con altri connessi alla stessa istanza.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-170">This means that if the cloud service creates two worker role instances, users will only be able to chat with others connected to the same worker role instance.</span></span> <span data-ttu-id="ac1ac-171">Per scalare l'applicazione in modo da usare più istanze del ruolo, è possibile usare una tecnologia come il bus di servizio per condividere lo stato dell'archivio Socket.IO tra le istanze.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-171">To scale the application to work with multiple role instances, you could use a technology like Service Bus to share the Socket.IO store state across instances.</span></span> <span data-ttu-id="ac1ac-172">Per alcuni esempi, vedere le apposite sezioni relative a code e argomenti del bus di servizio nel [repository GitHub di Azure SDK per Node.js](https://github.com/WindowsAzure/azure-sdk-for-node).</span><span class="sxs-lookup"><span data-stu-id="ac1ac-172">For examples, see the Service Bus Queues and Topics usage samples in the [Azure SDK for Node.js GitHub repository](https://github.com/WindowsAzure/azure-sdk-for-node).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ac1ac-173">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ac1ac-173">Next steps</span></span>
<span data-ttu-id="ac1ac-174">In questa esercitazione è stato illustrato come creare un'applicazione di chat di base ospitata in un servizio cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="ac1ac-174">In this tutorial you learned how to create a basic chat application hosted in an Azure Cloud Service.</span></span> <span data-ttu-id="ac1ac-175">Per informazioni su come ospitare questa applicazione in un sito Web di Azure, vedere [Creazione di un'applicazione di chat Node.js con Socket.IO in un sito Web di Azure][chatwebsite].</span><span class="sxs-lookup"><span data-stu-id="ac1ac-175">To learn how to host this application in an Azure Website, see [Build a Node.js Chat Application with Socket.IO on an Azure Web Site][chatwebsite].</span></span>

<span data-ttu-id="ac1ac-176">Per ulteriori informazioni, vedere anche il [Centro per sviluppatori di Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="ac1ac-176">For more information, see also the [Node.js Developer Center](/develop/nodejs/).</span></span>

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
<span data-ttu-id="ac1ac-177">[archivio GitHub Socket.IO]: https://github.com/LearnBoost/socket.io/tree/0.9.14</span><span class="sxs-lookup"><span data-stu-id="ac1ac-177">[Socket.IO GitHub repository]: https://github.com/LearnBoost/socket.io/tree/0.9.14</span></span>
[Azure Considerations]: #windowsazureconsiderations
[Hosting the Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[The output of the Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


