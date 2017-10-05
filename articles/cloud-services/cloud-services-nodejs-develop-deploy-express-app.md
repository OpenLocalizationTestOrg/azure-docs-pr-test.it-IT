---
title: App Web con Express (Node.js) | Documentazione Microsoft
description: Esercitazione basata sull'esercitazione del servizio cloud e che illustra come usare il modulo Express.
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
ms.openlocfilehash: 54b715695e24786ec4e8dfcabefc648d76179c8b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a><span data-ttu-id="95c09-103">Creazione di un'applicazione Web Node.js utilizzando Express in un servizio cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="95c09-103">Build a Node.js web application using Express on an Azure Cloud Service</span></span>
<span data-ttu-id="95c09-104">Node.js include un set minimo di funzionalità nel runtime core.</span><span class="sxs-lookup"><span data-stu-id="95c09-104">Node.js includes a minimal set of functionality in the core runtime.</span></span>
<span data-ttu-id="95c09-105">Gli sviluppatori usano spesso moduli di terze parti per fornire funzionalità aggiuntive durante lo sviluppo di un'applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="95c09-105">Developers often use 3rd party modules to provide additional functionality when developing a Node.js application.</span></span> <span data-ttu-id="95c09-106">In questa esercitazione si creerà una nuova applicazione usando il modulo [Express][Express] che fornisce un framework MVC per la creazione di applicazioni Web Node.js.</span><span class="sxs-lookup"><span data-stu-id="95c09-106">In this tutorial you will create a new application using the [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span></span>

<span data-ttu-id="95c09-107">Di seguito è riportata una schermata dell'applicazione completata:</span><span class="sxs-lookup"><span data-stu-id="95c09-107">A screenshot of the completed application is below:</span></span>

![Visualizzazione di Welcome to Express in Azure in un Web browser](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="95c09-109">Creazione di un progetto di servizio cloud</span><span class="sxs-lookup"><span data-stu-id="95c09-109">Create a Cloud Service Project</span></span>
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

<span data-ttu-id="95c09-110">Eseguire la procedura seguente per creare un nuovo progetto di servizio cloud denominato 'expressapp':</span><span class="sxs-lookup"><span data-stu-id="95c09-110">Perform the following steps to create a new cloud service project named 'expressapp':</span></span>

1. <span data-ttu-id="95c09-111">Nel **menu Start** o nella **schermata Start** cercare **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="95c09-111">From the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="95c09-112">Fare infine clic con il pulsante destro del mouse su **Windows PowerShell** e scegliere **Esegui come amministratore**.</span><span class="sxs-lookup"><span data-stu-id="95c09-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Icona di Azure PowerShell](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. <span data-ttu-id="95c09-114">Passare alla directory **c:\\node** e immettere i comandi seguenti per creare una nuova soluzione denominata **expressapp** e un ruolo Web denominato **WebRole1**:</span><span class="sxs-lookup"><span data-stu-id="95c09-114">Change directories to the **c:\\node** directory and then enter the following commands to create a new solution named **expressapp** and a web role named **WebRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > <span data-ttu-id="95c09-115">Per impostazione predefinita, in **Add-AzureNodeWebRole** viene usata una versione precedente di Node.js.</span><span class="sxs-lookup"><span data-stu-id="95c09-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span></span> <span data-ttu-id="95c09-116">La precedente istruzione **Set-AzureServiceProjectRole** indica ad Azure di usare la versione 0.10.21 di Node.</span><span class="sxs-lookup"><span data-stu-id="95c09-116">The **Set-AzureServiceProjectRole** statement above instructs Azure to use v0.10.21 of Node.</span></span>  <span data-ttu-id="95c09-117">Si noti che i parametri fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="95c09-117">Note the parameters are case-sensitive.</span></span>  <span data-ttu-id="95c09-118">È possibile verificare di aver selezionato la versione corretta di Node.js controllando la proprietà **engines** in **WebRole1\package.json**.</span><span class="sxs-lookup"><span data-stu-id="95c09-118">You can verify the correct version of Node.js has been selected by checking the **engines** property in **WebRole1\package.json**.</span></span>
    > 
    > 

## <a name="install-express"></a><span data-ttu-id="95c09-119">Installazione di Express</span><span class="sxs-lookup"><span data-stu-id="95c09-119">Install Express</span></span>
1. <span data-ttu-id="95c09-120">Installare il generatore di Express eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="95c09-120">Install the Express generator by issuing the following command:</span></span>
   
        PS C:\node\expressapp> npm install express-generator -g
   
    <span data-ttu-id="95c09-121">L'output del comando npm dovrebbe essere analogo al risultato mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="95c09-121">The output of the npm command should look similar to the result below.</span></span> 
   
    ![Visualizzazione dell'output del comando npm install express in Windows PowerShell.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. <span data-ttu-id="95c09-123">Passare alla directory **WebRole1** e usare il comando express per generare una nuova applicazione:</span><span class="sxs-lookup"><span data-stu-id="95c09-123">Change directories to the **WebRole1** directory and use the express command to generate a new application:</span></span>
   
        PS C:\node\expressapp\WebRole1> express
   
    <span data-ttu-id="95c09-124">Verrà richiesto di sovrascrivere l'applicazione precedente.</span><span class="sxs-lookup"><span data-stu-id="95c09-124">You will be prompted to overwrite your earlier application.</span></span> <span data-ttu-id="95c09-125">Immettere **y** o **yes** per continuare.</span><span class="sxs-lookup"><span data-stu-id="95c09-125">Enter **y** or **yes** to continue.</span></span> <span data-ttu-id="95c09-126">Express genererà il file app.js e una struttura di cartelle per creare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="95c09-126">Express will generate the app.js file and a folder structure for building your application.</span></span>
   
    ![Output del comando express](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. <span data-ttu-id="95c09-128">Per installare le dipendenze aggiuntive definite nel file package.json, immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="95c09-128">To install additional dependencies defined in the package.json file, enter the following command:</span></span>
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![Output del comando npm install](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. <span data-ttu-id="95c09-130">Usare il comando seguente per copiare il file **bin/www** in **server.js**.</span><span class="sxs-lookup"><span data-stu-id="95c09-130">Use the following command to copy the **bin/www** file to **server.js**.</span></span> <span data-ttu-id="95c09-131">In questo modo, il servizio cloud potrà trovare il punto di ingresso per questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="95c09-131">This is so the cloud service can find the entry point for this application.</span></span>
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   <span data-ttu-id="95c09-132">Dopo il completamento del comando, nella directory WebRole1 dovrebbe essere presente un file **server.js** .</span><span class="sxs-lookup"><span data-stu-id="95c09-132">After this command completes, you should have a **server.js** file in the WebRole1 directory.</span></span>
5. <span data-ttu-id="95c09-133">Modificare il file **server.js** rimuovendo uno dei caratteri '.' dalla riga seguente.</span><span class="sxs-lookup"><span data-stu-id="95c09-133">Modify the **server.js** to remove one of the '.' characters from the following line.</span></span>
   
       var app = require('../app');
   
   <span data-ttu-id="95c09-134">Dopo questa modifica la riga dovrebbe avere un aspetto analogo al seguente.</span><span class="sxs-lookup"><span data-stu-id="95c09-134">After making this modification, the line should appear as follows.</span></span>
   
       var app = require('./app');
   
   <span data-ttu-id="95c09-135">Questa modifica è obbligatoria perché il file (in precedenza **bin/www**) è stato spostato nella stessa directory del file dell'app richiesto.</span><span class="sxs-lookup"><span data-stu-id="95c09-135">This change is required since we moved the file (formerly **bin/www**,) to the same directory as the app file being required.</span></span> <span data-ttu-id="95c09-136">Al termine di questa modifica, salvare il file **server.js** .</span><span class="sxs-lookup"><span data-stu-id="95c09-136">After making this change, save the **server.js** file.</span></span>
6. <span data-ttu-id="95c09-137">Utilizzare il comando seguente per eseguire l'applicazione nell'emulatore di Azure:</span><span class="sxs-lookup"><span data-stu-id="95c09-137">Use the following command to run the application in the Azure emulator:</span></span>
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Una pagina Web contenente Welcome to Express.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-the-view"></a><span data-ttu-id="95c09-139">Modifica della visualizzazione</span><span class="sxs-lookup"><span data-stu-id="95c09-139">Modifying the View</span></span>
<span data-ttu-id="95c09-140">Modificare le visualizzazione in modo che il messaggio visualizzato sia "Welcome to Express in Azure".</span><span class="sxs-lookup"><span data-stu-id="95c09-140">Now modify the view to display the message "Welcome to Express in Azure".</span></span>

1. <span data-ttu-id="95c09-141">Immettere il comando seguente per aprire il file index.jade:</span><span class="sxs-lookup"><span data-stu-id="95c09-141">Enter the following command to open the index.jade file:</span></span>
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![Contenuto del file index.jade.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   <span data-ttu-id="95c09-143">Jade è il motore di visualizzazione predefinito utilizzato dalle applicazioni Express.</span><span class="sxs-lookup"><span data-stu-id="95c09-143">Jade is the default view engine used by Express applications.</span></span> <span data-ttu-id="95c09-144">Per altre informazioni sul motore di visualizzazione Jade, vedere [http://jade-lang.com][http://jade-lang.com].</span><span class="sxs-lookup"><span data-stu-id="95c09-144">For more information on the Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span></span>
2. <span data-ttu-id="95c09-145">Modificare l'ultima riga di testo aggiungendo **in Azure**.</span><span class="sxs-lookup"><span data-stu-id="95c09-145">Modify the last line of text by appending **in Azure**.</span></span>
   
   ![File index.jade che nell'ultima riga riporta: p Welcome to \#{title} in Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. <span data-ttu-id="95c09-147">Salvare il file e chiudere il Blocco note.</span><span class="sxs-lookup"><span data-stu-id="95c09-147">Save the file and exit Notepad.</span></span>
4. <span data-ttu-id="95c09-148">Aggiornare il tuo browser per vedere le modifiche.</span><span class="sxs-lookup"><span data-stu-id="95c09-148">Refresh your browser and you will see your changes.</span></span>
   
   ![Una finestra del browser in cui la pagina contiene Welcome to Express in Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

<span data-ttu-id="95c09-150">Dopo aver testato l'applicazione, usare il cmdlet **Stop-AzureEmulator** per arrestare l'emulatore.</span><span class="sxs-lookup"><span data-stu-id="95c09-150">After testing the application, use the **Stop-AzureEmulator** cmdlet to stop the emulator.</span></span>

## <a name="publishing-the-application-to-azure"></a><span data-ttu-id="95c09-151">Pubblicazione dell'applicazione in Azure</span><span class="sxs-lookup"><span data-stu-id="95c09-151">Publishing the Application to Azure</span></span>
<span data-ttu-id="95c09-152">Nella finestra di Azure PowerShell usare il cmdlet **Publish-AzureServiceProject** per distribuire l'applicazione a un servizio di cloud</span><span class="sxs-lookup"><span data-stu-id="95c09-152">In the Azure PowerShell window, use the **Publish-AzureServiceProject** cmdlet to deploy the application to a cloud service</span></span>

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

<span data-ttu-id="95c09-153">Al termine dell'operazione di distribuzione, verrà aperto il browser e verrà visualizzata la pagina Web.</span><span class="sxs-lookup"><span data-stu-id="95c09-153">Once the deployment operation completes, your browser will open and display the web page.</span></span>

![A web browser displaying the Express page.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a><span data-ttu-id="95c09-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="95c09-156">Next steps</span></span>
<span data-ttu-id="95c09-157">Per ulteriori informazioni, vedere il [Centro per sviluppatori di Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="95c09-157">For more information, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


