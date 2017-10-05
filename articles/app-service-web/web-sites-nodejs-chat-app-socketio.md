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
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a><span data-ttu-id="78f72-103">Creazione di un'applicazione di chat Node.js con Socket.IO in Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="78f72-103">Create a Node.js chat application with Socket.IO in Azure App Service</span></span>
<span data-ttu-id="78f72-104">Socket.IO fornisce comunicazioni in tempo reale tra il server node.js e i client usando WebSocket.</span><span class="sxs-lookup"><span data-stu-id="78f72-104">Socket.IO provides real-time communication between your node.js server and clients using WebSockets.</span></span> <span data-ttu-id="78f72-105">Supporta inoltre il fallback in altri tipi di trasporto (ad esempio il polling prolungato) che funzionano con browser precedenti.</span><span class="sxs-lookup"><span data-stu-id="78f72-105">It also supports fallback to other transports (such as long polling) that work with older browsers.</span></span> <span data-ttu-id="78f72-106">In questa esercitazione verrà illustrato l'hosting di un'applicazione di chat basata su Socket.IO come app Web di Azure e verrà indicato come ridimensionare l'applicazione tramite [Cache Redis di Azure].</span><span class="sxs-lookup"><span data-stu-id="78f72-106">This tutorial will walk you through hosting a Socket.IO based chat application as an Azure web app, and show you how to scale the application using [Azure Redis Cache].</span></span> <span data-ttu-id="78f72-107">Per altre informazioni su Socket.IO, vedere <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="78f72-107">For more information on Socket.IO, see <http://socket.io/>.</span></span>

> [!NOTE]
> <span data-ttu-id="78f72-108">Le procedure descritte in questa attività si applicano alle [app Web del servizio app]. Per Servizi cloud, vedere [Creazione di un'applicazione di chat Node.js con Socket.IO in un servizio cloud di Azure].</span><span class="sxs-lookup"><span data-stu-id="78f72-108">The procedures in this task apply to [App Service Web Apps]; for Cloud Services, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>
> 
> 

## <a name="download-the-chat-example"></a><span data-ttu-id="78f72-109">Scaricare l'esempio di chat</span><span class="sxs-lookup"><span data-stu-id="78f72-109">Download the chat example</span></span>
<span data-ttu-id="78f72-110">Per questo progetto, verrà utilizzato l'esempio di chat dell' [archivio GitHub Socket.IO].</span><span class="sxs-lookup"><span data-stu-id="78f72-110">For this project, we will use the chat example from the [Socket.IO GitHub repository].</span></span> <span data-ttu-id="78f72-111">Eseguire la procedura seguente per scaricare l'esempio e aggiungerlo al progetto creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="78f72-111">Perform the following steps to download the example and add it to the project you previously created.</span></span>

1. <span data-ttu-id="78f72-112">Scaricare una [versione archiviata ZIP o GZ] del progetto Socket.IO (per questo documento è stata usata la versione 1.3.5)</span><span class="sxs-lookup"><span data-stu-id="78f72-112">Download a [ZIP or GZ archived release] of the Socket.IO project (version 1.3.5 was used for this document)</span></span>
2. <span data-ttu-id="78f72-113">Estrarre l'archivio e copiare la directory **examples\\chat** in una nuova posizione.</span><span class="sxs-lookup"><span data-stu-id="78f72-113">Extract the archive and copy the **examples\\chat** directory to a new location.</span></span> <span data-ttu-id="78f72-114">Ad esempio, **\\node\\chat**.</span><span class="sxs-lookup"><span data-stu-id="78f72-114">For example, **\\node\\chat**.</span></span>

## <a name="modify-appjs-and-install-modules"></a><span data-ttu-id="78f72-115">Modificare app.js e installare i moduli</span><span class="sxs-lookup"><span data-stu-id="78f72-115">Modify app.js and install modules</span></span>
1. <span data-ttu-id="78f72-116">Rinominare il file **index.js** in **app.js**.</span><span class="sxs-lookup"><span data-stu-id="78f72-116">Rename the **index.js** file to **app.js**.</span></span> <span data-ttu-id="78f72-117">Ciò consente ad Azure di rilevare che si tratta di un'applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="78f72-117">This allows Azure to detect that this is a Node.js application.</span></span>
2. <span data-ttu-id="78f72-118">Aprire il file **app.js** in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="78f72-118">Open the **app.js** file in a text editor.</span></span> <span data-ttu-id="78f72-119">Sostituire la riga contenente `var io = require('../..')(server);` come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="78f72-119">Change the line containing `var io = require('../..')(server);` as shown below:</span></span>
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. <span data-ttu-id="78f72-120">Aprire il file **package.json** e aggiungere un riferimento a socket.io sotto `dependencies`, come di seguito indicato:</span><span class="sxs-lookup"><span data-stu-id="78f72-120">Open the **package.json** file and add a reference to socket.io under `dependencies`, as shown below:</span></span>
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. <span data-ttu-id="78f72-121">Dalla riga di comando passare alla directory **\\node\\chat** e usare npm per installare i moduli necessari per questa applicazione:</span><span class="sxs-lookup"><span data-stu-id="78f72-121">From the command-line, change to the **\\node\\chat** directory and use npm to install the modules required by this application:</span></span>
   
        npm install
   
    <span data-ttu-id="78f72-122">Verranno aperti i moduli in una sottocartella denominata **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="78f72-122">This will install the modules into a subfolder named **node_modules**.</span></span>

## <a name="create-an-azure-web-app"></a><span data-ttu-id="78f72-123">Creare un'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="78f72-123">Create an Azure Web App</span></span>
<span data-ttu-id="78f72-124">Per creare un'app Web di Azure, abilitare la pubblicazione Git e quindi abilitare il supporto WebSocket per l'app Web, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="78f72-124">Follow these steps to create an Azure web app, enable Git publishing, and then enable WebSocket support for the web app.</span></span>

> [!NOTE]
> <span data-ttu-id="78f72-125">Per completare l'esercitazione, è necessario un account Azure.</span><span class="sxs-lookup"><span data-stu-id="78f72-125">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="78f72-126">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="78f72-126">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="78f72-127">Per informazioni dettagliate, vedere la pagina relativa alla <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">versione di valutazione gratuita di Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="78f72-127">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

1. <span data-ttu-id="78f72-128">Installare l'interfaccia della riga di comando di Azure e connettersi alla propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="78f72-128">Install the Azure Command-Line Interface (Azure CLI) and connect to your Azure subscription.</span></span> <span data-ttu-id="78f72-129">Vedere [Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="78f72-129">See [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="78f72-130">Se si tratta della prima impostazione di un repository in Azure, è necessario creare le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="78f72-130">If this is your first time setting up a repository in Azure, you need to create login credentials.</span></span> <span data-ttu-id="78f72-131">Dall'interfaccia della riga di comando di Azure, immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="78f72-131">From the Azure CLI, enter the following command:</span></span>
   
        azure site deployment user set [username] [password]
3. <span data-ttu-id="78f72-132">Passare alla directory **\\node\chat** e usare il comando seguente per creare una nuova app Web di Azure e un repository Git locale.</span><span class="sxs-lookup"><span data-stu-id="78f72-132">Change to the **\\node\chat** directory and use the following command to create a new Azure web app and a local Git repository.</span></span> <span data-ttu-id="78f72-133">Verrà inoltre creato un repository Git remoto denominato .</span><span class="sxs-lookup"><span data-stu-id="78f72-133">This command also creates a Git remote named 'azure'.</span></span>
   
        azure site create mysitename --git
   
    <span data-ttu-id="78f72-134">Sostituire "mysitename" con un nome univoco per il sito Web.</span><span class="sxs-lookup"><span data-stu-id="78f72-134">You must replace 'mysitename' with a unique name for your web app.</span></span>
4. <span data-ttu-id="78f72-135">Eseguire il commit dei file esistenti nel repository locale usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="78f72-135">Commit the existing files to the local repository by using the following commands:</span></span>
   
        git add .
        git commit -m "Initial commit"
5. <span data-ttu-id="78f72-136">Effettuare il push dei file nel repository delle app Web di Azure con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="78f72-136">Push the files to the Azure Web Apps repository with the following command:</span></span>
   
        git push azure master
   
    <span data-ttu-id="78f72-137">Quando richiesto, immettere le credenziali dal passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="78f72-137">When prompted, enter your credentials from step 2.</span></span> <span data-ttu-id="78f72-138">Durante le operazioni di importazione dei moduli nel server, verranno visualizzati messaggi di stato.</span><span class="sxs-lookup"><span data-stu-id="78f72-138">You will receive status messages as modules are imported on the server.</span></span> <span data-ttu-id="78f72-139">Al termine del processo, l'applicazione sarà ospitata nell'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="78f72-139">Once this process has completed, the application will be hosted on your Azure web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="78f72-140">Durante l'installazione del modulo, è possibile notare errori di tipo Il progetto importato... non è stato trovato.</span><span class="sxs-lookup"><span data-stu-id="78f72-140">During module installation, you may notice errors that 'The imported project ... was not found'.</span></span> <span data-ttu-id="78f72-141">Tali errori possono essere ignorati.</span><span class="sxs-lookup"><span data-stu-id="78f72-141">These can safely be ignored.</span></span>
   > 
   > 
6. <span data-ttu-id="78f72-142">Socket.IO utilizza i WebSocket che non sono abilitati per impostazione predefinita in Azure.</span><span class="sxs-lookup"><span data-stu-id="78f72-142">Socket.IO uses WebSockets, which are not enabled by default on Azure.</span></span> <span data-ttu-id="78f72-143">Per abilitare i WebSocket, utilizzare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="78f72-143">To enable web sockets, use the following command:</span></span>
   
        azure site set -w
   
    <span data-ttu-id="78f72-144">Se richiesto, immettere il nome dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="78f72-144">If prompted, enter the name of the web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="78f72-145">Il comando 'azure site set -w' funzionerà solo con la versione 0.7.4 o superiore dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="78f72-145">The 'azure site set -w' command will work only with version 0.7.4 or higher of the Azure Command-Line Interface.</span></span> <span data-ttu-id="78f72-146">È anche possibile abilitare il supporto WebSocket utilizzando il [Portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="78f72-146">You can also enable WebSocket support using the [Azure Portal](https://portal.azure.com).</span></span>
   > 
   > <span data-ttu-id="78f72-147">Per abilitare i WebSocket usando il Portale di Azure, fare clic sull'app Web dal pannello App Web, selezionare **Tutte le impostazioni** > **Impostazioni dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="78f72-147">To enable WebSockets using the Azure Portal, click the web app from the Web Apps blade, click **All settings** > **Application settings**.</span></span> <span data-ttu-id="78f72-148">In **Web Socket** fare clic su **Attivato**.</span><span class="sxs-lookup"><span data-stu-id="78f72-148">Under **Web Sockets**, click **On**.</span></span> <span data-ttu-id="78f72-149">Fare quindi clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="78f72-149">Then click **Save**.</span></span>
   > 
   > 
7. <span data-ttu-id="78f72-150">Per visualizzare l'app Web in Azure, utilizzare il comando seguente per avviare il browser Web e passare all'app Web ospitata:</span><span class="sxs-lookup"><span data-stu-id="78f72-150">To view the web app on Azure, use the following command to launch your web browser and navigate to the hosted web app:</span></span>
   
        azure site browse

<span data-ttu-id="78f72-151">L'app ora è in esecuzione in Azure ed è in grado di inoltrare i messaggi di chat tra diversi client tramite Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="78f72-151">Your app is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

## <a name="scale-out"></a><span data-ttu-id="78f72-152">Scalabilità orizzontale</span><span class="sxs-lookup"><span data-stu-id="78f72-152">Scale out</span></span>
<span data-ttu-id="78f72-153">Le applicazioni Socket.IO possono essere scalate usando un **adattatore** per distribuire messaggi ed eventi tra più istanze di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="78f72-153">Socket.IO applications can be scaled out by using an **adapter** to distribute messages and events between multiple application instances.</span></span> <span data-ttu-id="78f72-154">Nonostante siano disponibili diversi adattatori, l'adattatore [socket.io-redis] può essere usato facilmente con la funzionalità Cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="78f72-154">While there are several adapters available, the [socket.io-redis] adapter can be easily used with the Azure Redis Cache feature.</span></span>

> [!NOTE]
> <span data-ttu-id="78f72-155">Un ulteriore requisito per la scalabilità orizzontale di una soluzione Socket.IO è il supporto di sessioni permanenti.</span><span class="sxs-lookup"><span data-stu-id="78f72-155">An additional requirement for scaling out a Socket.IO solution is support for sticky sessions.</span></span> <span data-ttu-id="78f72-156">Le sessioni permanenti sono abilitate per impostazione predefinita per le app Web di Azure tramite il routing delle richieste di Azure.</span><span class="sxs-lookup"><span data-stu-id="78f72-156">Sticky sessions are enabled by default for Azure Web Apps through Azure Request Routing.</span></span> <span data-ttu-id="78f72-157">Per altre informazioni, vedere il blog relativo all' [affinità delle istanze in Siti Web di Azure]</span><span class="sxs-lookup"><span data-stu-id="78f72-157">For more information, see [Instance Affinity in Azure Web Sites].</span></span>
> 
> 

### <a name="create-a-redis-cache"></a><span data-ttu-id="78f72-158">Creare una cache Redis</span><span class="sxs-lookup"><span data-stu-id="78f72-158">Create a Redis cache</span></span>
<span data-ttu-id="78f72-159">Eseguire la procedura descritta in [Creare una cache in Cache Redis di Azure] per creare una nuova cache.</span><span class="sxs-lookup"><span data-stu-id="78f72-159">Perform the steps in [Create a cache in Azure Redis Cache] to create a new cache.</span></span>

> [!NOTE]
> <span data-ttu-id="78f72-160">Salvare il **Nome host** e la **Chiave primaria** per la cache in quanto saranno necessari nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="78f72-160">Save the **Host name** and **Primary key** for your cache, as these will be needed in the next steps.</span></span>
> 
> 

### <a name="add-the-redis-and-socketio-redis-modules"></a><span data-ttu-id="78f72-161">Aggiungere i moduli redis e socket.io-redis</span><span class="sxs-lookup"><span data-stu-id="78f72-161">Add the redis and socket.io-redis modules</span></span>
1. <span data-ttu-id="78f72-162">Dalla riga di comando passare alla directory **\\node\\chat** e usare il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="78f72-162">From a command-line, change to the **\\node\\chat** directory and use the following command.</span></span>
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > <span data-ttu-id="78f72-163">Le versioni specificate in questo comando sono le stesse versioni usate nei test di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="78f72-163">The versions specified in this command are the versions used when testing this article.</span></span>
   > 
   > 
2. <span data-ttu-id="78f72-164">Modificare il file **app.js** per aggiungere le righe seguenti immediatamente dopo `var io = require('socket.io')(server);`</span><span class="sxs-lookup"><span data-stu-id="78f72-164">Modify the **app.js** file to add the following lines immediately after `var io = require('socket.io')(server);`</span></span>
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    <span data-ttu-id="78f72-165">Sostituire **redishostname** e **rediskey** con il nome host e la chiave per la cache Redis.</span><span class="sxs-lookup"><span data-stu-id="78f72-165">Replace **redishostname** and **rediskey** with the host name and key for your Redis cache.</span></span>
   
    <span data-ttu-id="78f72-166">In questo modo viene creato un client di pubblicazione e sottoscrizione alla cache Redis creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="78f72-166">This will create a publish and subscribe client to the Redis cache created previously.</span></span> <span data-ttu-id="78f72-167">I client vengono quindi usati con l'adattatore per configurare Socket.IO in modo da usare la cache Redis per passare messaggi ed eventi tra le istanze dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="78f72-167">The clients are then used with the adapter to configure Socket.IO to use the Redis cache for passing messages and events between instances of your application</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="78f72-168">Anche se l'adattatore **socket.io-redis** può comunicare direttamente con Redis, la versione corrente non supporta l'autenticazione richiesta dalla cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="78f72-168">While the **socket.io-redis** adapter can communicate directly to Redis, the current version does not support the authentication required by Azure Redis cache.</span></span> <span data-ttu-id="78f72-169">Pertanto, la connessione iniziale viene creata usando il modulo **redis**, quindi il client viene passato all'adattatore **socket.io-redis**.</span><span class="sxs-lookup"><span data-stu-id="78f72-169">So the initial connection is created using the **redis** module, then the client is passed to the **socket.io-redis** adapter.</span></span>
   > 
   > <span data-ttu-id="78f72-170">Nonostante la cache Redis di Azure supporti le connessioni sicure usando la porta 6380, alla data del 14 luglio 2014 i moduli usati in questo esempio non supportano le connessioni sicure.</span><span class="sxs-lookup"><span data-stu-id="78f72-170">While Azure Redis Cache supports secure connections using port 6380, the modules used in this example do not support secure connections as of 7/14/2014.</span></span> <span data-ttu-id="78f72-171">Il codice riportato sopra usa la porta 6379, predefinita e non sicura.</span><span class="sxs-lookup"><span data-stu-id="78f72-171">The above code uses the default, unsecure port of 6379.</span></span>
   > 
   > 
3. <span data-ttu-id="78f72-172">Salvare il file **app.js** modificato</span><span class="sxs-lookup"><span data-stu-id="78f72-172">Save the modified **app.js**</span></span>

### <a name="commit-changes-and-redeploy"></a><span data-ttu-id="78f72-173">Eseguire il commit delle modifiche ed effettuare la ridistribuzione</span><span class="sxs-lookup"><span data-stu-id="78f72-173">Commit changes and redeploy</span></span>
<span data-ttu-id="78f72-174">Dalla riga di comando nella directory **\\node\\chat**, usare i comandi seguenti per eseguire il commit delle modifiche e ridistribuire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="78f72-174">From the command-line in the **\\node\\chat** directory, use the following commands to commit changes and redeploy the application.</span></span>

    git add .
    git commit -m "implementing scale out"
    git push azure master

<span data-ttu-id="78f72-175">Dopo aver effettuato il push delle modifiche al server, è possibile scalare il sito tra più istanze tramite il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="78f72-175">Once the changes have been pushed to the server, you can scale your site across multiple instances by using the following command.</span></span>

    azure site scale instances --instances #

<span data-ttu-id="78f72-176">**#** è il numero di istanze da creare.</span><span class="sxs-lookup"><span data-stu-id="78f72-176">Where **#** is the number of instances to create.</span></span>

<span data-ttu-id="78f72-177">È possibile effettuare la connessione all'app Web da più browser o computer per verificare che i messaggi siano inviati correttamente a tutti i client.</span><span class="sxs-lookup"><span data-stu-id="78f72-177">You can connect to your web app from multiple browsers or computers to verify that messages are correctly sent to all clients.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="78f72-178">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="78f72-178">Troubleshooting</span></span>
### <a name="connection-limits"></a><span data-ttu-id="78f72-179">Limiti di connessione</span><span class="sxs-lookup"><span data-stu-id="78f72-179">Connection limits</span></span>
<span data-ttu-id="78f72-180">App Web di Azure è disponibile in più SKU, che determinano le risorse disponibili per il sito,</span><span class="sxs-lookup"><span data-stu-id="78f72-180">Azure Web Apps is available in multiple SKUs, which determine the resources available to your site.</span></span> <span data-ttu-id="78f72-181">incluso il numero di connessioni WebSocket consentite.</span><span class="sxs-lookup"><span data-stu-id="78f72-181">This includes the number of allowed WebSocket connections.</span></span> <span data-ttu-id="78f72-182">Per altre informazioni, vedere la [pagina dei dettagli dei prezzi di App Web].</span><span class="sxs-lookup"><span data-stu-id="78f72-182">For more information, see the [Web Apps Pricing page].</span></span>

### <a name="messages-arent-being-sent-using-websockets"></a><span data-ttu-id="78f72-183">I messaggi non vengono inviati usando WebSocket</span><span class="sxs-lookup"><span data-stu-id="78f72-183">Messages aren't being sent using WebSockets</span></span>
<span data-ttu-id="78f72-184">Se i browser client continuano a eseguire il fallback al polling prolungato invece di usare WebSocket, il motivo potrebbe essere uno dei seguenti.</span><span class="sxs-lookup"><span data-stu-id="78f72-184">If client browsers keep falling back to long polling instead of using WebSockets, it may be because of one of the following.</span></span>

* <span data-ttu-id="78f72-185">**Tentare di limitare il trasporto ai soli WebSocket**</span><span class="sxs-lookup"><span data-stu-id="78f72-185">**Try limiting the transport to just WebSockets**</span></span>
  
    <span data-ttu-id="78f72-186">Affinché Socket.IO possa usare WebSocket per il trasporto dei messaggi, sia il server che il client devono supportare WebSocket.</span><span class="sxs-lookup"><span data-stu-id="78f72-186">In order for Socket.IO to use WebSockets as the messaging transport, both the server and client must support WebSockets.</span></span> <span data-ttu-id="78f72-187">Diversamente, Socket.IO negozierà un altro tipo di trasporto, come il polling prolungato.</span><span class="sxs-lookup"><span data-stu-id="78f72-187">If one or the other does not, Socket.IO will negotiate another transport, such as long polling.</span></span> <span data-ttu-id="78f72-188">L'elenco predefinito dei tipi di trasporto usati da Socket.IO è ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span><span class="sxs-lookup"><span data-stu-id="78f72-188">The default list of transports used by Socket.IO is ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span></span> <span data-ttu-id="78f72-189">È possibile forzarlo in modo da usare solo WebSocket aggiungendo il codice seguente al file **app.js**, dopo la riga contenente `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="78f72-189">You can force it to only use WebSockets by adding the following code to the **app.js** file, after the line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > <span data-ttu-id="78f72-190">Si noti che i browser precedenti che non supportano WebSocket non potranno effettuare la connessione al sito mentre il codice riportato sopra è attivo, in quanto quest'ultimo limita la comunicazione ai soli WebSocket.</span><span class="sxs-lookup"><span data-stu-id="78f72-190">Note that older browsers that do not support WebSockets will not be able to connect to the site while the above code is active, as it restricts communication to WebSockets only.</span></span>
  > 
  > 
* <span data-ttu-id="78f72-191">**Usa SSL**</span><span class="sxs-lookup"><span data-stu-id="78f72-191">**Use SSL**</span></span>
  
    <span data-ttu-id="78f72-192">WebSocket si basa su intestazioni HTTP usate con minore frequenza, come l'intestazione **Upgrade** .</span><span class="sxs-lookup"><span data-stu-id="78f72-192">WebSockets relies on some lesser used HTTP headers, such as the **Upgrade** header.</span></span> <span data-ttu-id="78f72-193">Alcuni dispositivi di rete intermedi, come i proxy Web, possono rimuovere tali intestazioni.</span><span class="sxs-lookup"><span data-stu-id="78f72-193">Some intermediate network devices, such as web proxies, may remove these headers.</span></span> <span data-ttu-id="78f72-194">Per evitare il problema, è possibile stabilire la connessione WebSocket su SSL.</span><span class="sxs-lookup"><span data-stu-id="78f72-194">To avoid this problem, you can establish the WebSocket connection over SSL.</span></span>
  
    <span data-ttu-id="78f72-195">È possibile effettuare facilmente questa operazione configurando Socket.IO su `match origin protocol`.</span><span class="sxs-lookup"><span data-stu-id="78f72-195">An easy way to accomplish this is to configure Socket.IO to `match origin protocol`.</span></span> <span data-ttu-id="78f72-196">Questa configurazione fornisce a Socket.IO l'istruzione di proteggere la comunicazione WebSocket nello stesso modo della richiesta HTTP/HTTPS di origine per la pagina Web.</span><span class="sxs-lookup"><span data-stu-id="78f72-196">This instructs Socket.IO to secure WebSockets communication the same as the originating HTTP/HTTPS request for the web page.</span></span> <span data-ttu-id="78f72-197">Se un browser usa un URL HTTPS per visitare il sito Web, le comunicazioni WebSocket successive tramite Socket.IO verranno protette su SSL.</span><span class="sxs-lookup"><span data-stu-id="78f72-197">If a browser uses an HTTPS URL to visit your website, subsequent WebSocket communications through Socket.IO will be secured over SSL.</span></span>
  
    <span data-ttu-id="78f72-198">Per modificare questo esempio in modo da abilitare questa configurazione, aggiungere il codice seguente al file **app.js** dopo la riga contenente `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="78f72-198">To modify this example to enable this configuration, add the following code to the **app.js** file after the line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* <span data-ttu-id="78f72-199">**Verificare le impostazioni del file web.config**</span><span class="sxs-lookup"><span data-stu-id="78f72-199">**Verify web.config settings**</span></span>
  
    <span data-ttu-id="78f72-200">Le app Web di Azure che ospitano le applicazioni Node.js utilizzano il file **web.config** per eseguire il routing delle richieste in ingresso all'applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="78f72-200">Azure web apps that host Node.js applications use the **web.config** file to route incoming requests to the Node.js application.</span></span> <span data-ttu-id="78f72-201">Affinché i WebSocket funzionino correttamente con le applicazioni Node.js, il file **web.config** deve contenere la seguente voce.</span><span class="sxs-lookup"><span data-stu-id="78f72-201">For WebSockets to function correctly with Node.js applications, the **web.config** must contain the following entry.</span></span>
  
        <webSocket enabled="false"/>
  
    <span data-ttu-id="78f72-202">In questo modo viene disabilitato il modulo IIS WebSocket, che include la propria distribuzione di WebSocket ed è in conflitto con i moduli WebSocket specifici di Node.js come Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="78f72-202">This disables the IIS WebSockets module, which includes its own implementation of WebSockets and conflicts with Node.js specific WebSocket modules such as Socket.IO.</span></span> <span data-ttu-id="78f72-203">L'assenza di questa riga o la sua impostazione su `true`, potrebbe essere il motivo per il quale il trasporto WebSocket non funziona per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="78f72-203">If this line is not present, or is set to `true`, this may be the reason that the WebSocket transport is not working for your application.</span></span>
  
    <span data-ttu-id="78f72-204">Di norma le applicazioni Node.js non includono un file **web.config** , pertanto Siti Web di Azure ne genererà automaticamente uno per le applicazioni Node.js quando queste vengono distribuite.</span><span class="sxs-lookup"><span data-stu-id="78f72-204">Normally, Node.js applications do not include a **web.config** file, so Azure Websites will automatically generate one for Node.js applications when they are deployed.</span></span> <span data-ttu-id="78f72-205">Poiché questo file viene generato automaticamente sul server, per visualizzarlo è necessario usare l'URL FTP o FTPS per il sito Web.</span><span class="sxs-lookup"><span data-stu-id="78f72-205">Since this file is automatically generated on the server, you must use the FTP or FTPS URL for your website to view this file.</span></span> <span data-ttu-id="78f72-206">È possibile trovare gli URL FTP e FTPS per il sito nel portale classico selezionando l’app Web e quindi il collegamento **Dashboard** .</span><span class="sxs-lookup"><span data-stu-id="78f72-206">You can find the FTP and FTPS URLs for your site in the classic portal by selecting your web app, and then the **Dashboard** link.</span></span> <span data-ttu-id="78f72-207">Gli URL vengono visualizzati nella sezione **Riepilogo rapido** .</span><span class="sxs-lookup"><span data-stu-id="78f72-207">The URLs are displayed in the **quick glance** section.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="78f72-208">Il file **web.config** viene generato da Siti Web di Azure solo se non viene fornito dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="78f72-208">The **web.config** file is only generated by Azure Websites if your application does not provide one.</span></span> <span data-ttu-id="78f72-209">Se si fornisce un file **web.config** nella radice del progetto dell'applicazione, tale file verrà usato da App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="78f72-209">If you provide a **web.config** file in the root of your application project, it will be used by Azure Web Apps.</span></span>
  > 
  > 
  
    <span data-ttu-id="78f72-210">Se la voce non è presente o è impostata su un valore di `true`, è necessario creare un file **web.config** nella radice dell'applicazione Node.js e specificare un valore di `false`.</span><span class="sxs-lookup"><span data-stu-id="78f72-210">If the entry is not present, or is set to a value of `true`, then you should create a **web.config** in the root of your Node.js application and specify a value of `false`.</span></span>  <span data-ttu-id="78f72-211">Di seguito viene fornito, come riferimento, un file **web.config** predefinito per un'applicazione che usa **app.js** come punto di ingresso.</span><span class="sxs-lookup"><span data-stu-id="78f72-211">For reference, the below is a default **web.config** for an application that uses **app.js** as the entry point.</span></span>
  
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
  
    <span data-ttu-id="78f72-212">Se l'applicazione usa un punto di ingresso diverso da **app.js**, è necessario sostituire tutte le ricorrenze di **app.js** con il punto di ingresso corretto.</span><span class="sxs-lookup"><span data-stu-id="78f72-212">If your application uses an entry point other than **app.js**, you must replace all occurrences of **app.js** with the correct entry point.</span></span> <span data-ttu-id="78f72-213">ad esempio, la sostituzione di **app.js** con **server.js**.</span><span class="sxs-lookup"><span data-stu-id="78f72-213">For example, replacing **app.js** with **server.js**.</span></span>

> [!NOTE]
> <span data-ttu-id="78f72-214">Per iniziare a usare il servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app], dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="78f72-214">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="78f72-215">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="78f72-215">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="78f72-216">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="78f72-216">Next steps</span></span>
<span data-ttu-id="78f72-217">In questa esercitazione è stato illustrato come creare un'applicazione di chat ospitata in un'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="78f72-217">In this tutorial you learned how to create a chat application hosted in an Azure web app.</span></span> <span data-ttu-id="78f72-218">È inoltre possibile ospitare l'applicazione come un servizio cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="78f72-218">You can also host this application as an Azure Cloud Service.</span></span> <span data-ttu-id="78f72-219">Per le procedure che illustrano come eseguire questa operazione, vedere [Creazione di un'applicazione di chat Node.js con Socket.IO in un servizio cloud di Azure].</span><span class="sxs-lookup"><span data-stu-id="78f72-219">For steps on how to accomplish this, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>

<span data-ttu-id="78f72-220">Per ulteriori informazioni, vedere anche il [Centro per sviluppatori di Node.js].</span><span class="sxs-lookup"><span data-stu-id="78f72-220">For more information, see also the [Node.js Developer Center].</span></span>

## <a name="whats-changed"></a><span data-ttu-id="78f72-221">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="78f72-221">What's changed</span></span>
* <span data-ttu-id="78f72-222">Per una guida per il passaggio da Siti Web a Servizio app vedere: [Servizio app di Azure e i servizi di Azure esistenti]</span><span class="sxs-lookup"><span data-stu-id="78f72-222">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services].</span></span>

<!-- URL List -->

<span data-ttu-id="78f72-223">[Cache Redis di Azure]: /documentation/services/redis-cache/</span><span class="sxs-lookup"><span data-stu-id="78f72-223">[Azure Redis Cache]: /documentation/services/redis-cache/</span></span>
<span data-ttu-id="78f72-224">[app Web del servizio app]: http://go.microsoft.com/fwlink/?LinkId=529714</span><span class="sxs-lookup"><span data-stu-id="78f72-224">[App Service Web Apps]: http://go.microsoft.com/fwlink/?LinkId=529714</span></span>
<span data-ttu-id="78f72-225">[pagina dei dettagli dei prezzi di App Web]: http://go.microsoft.com/fwlink/?LinkId=511643</span><span class="sxs-lookup"><span data-stu-id="78f72-225">[Web Apps Pricing page]: http://go.microsoft.com/fwlink/?LinkId=511643</span></span>
<span data-ttu-id="78f72-226">[Creazione di un'applicazione di chat Node.js con Socket.IO in un servizio cloud di Azure]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md</span><span class="sxs-lookup"><span data-stu-id="78f72-226">[Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md</span></span>
[Install and Configure the Azure CLI]: ../cli-install-nodejs.md
<span data-ttu-id="78f72-227">[Servizio app di Azure e i servizi di Azure esistenti]: http://go.microsoft.com/fwlink/?LinkId=529714</span><span class="sxs-lookup"><span data-stu-id="78f72-227">[Azure App Service and Its Impact on Existing Azure Services]: http://go.microsoft.com/fwlink/?LinkId=529714</span></span>
<span data-ttu-id="78f72-228">[Centro per sviluppatori di Node.js]: /develop/nodejs/</span><span class="sxs-lookup"><span data-stu-id="78f72-228">[Node.js Developer Center]: /develop/nodejs/</span></span>
<span data-ttu-id="78f72-229">[Prova il servizio app]: https://azure.microsoft.com/try/app-service/</span><span class="sxs-lookup"><span data-stu-id="78f72-229">[Try App Service]: https://azure.microsoft.com/try/app-service/</span></span>
<span data-ttu-id="78f72-230">[affinità delle istanze in Siti Web di Azure]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/</span><span class="sxs-lookup"><span data-stu-id="78f72-230">[Instance Affinity in Azure Web Sites]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/</span></span>
<span data-ttu-id="78f72-231">[Creare una cache in Cache Redis di Azure]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md</span><span class="sxs-lookup"><span data-stu-id="78f72-231">[Create a cache in Azure Redis Cache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md</span></span>

<span data-ttu-id="78f72-232">[socket.io-redis]: https://github.com/socketio/socket.io-redis</span><span class="sxs-lookup"><span data-stu-id="78f72-232">[socket.io-redis]: https://github.com/socketio/socket.io-redis</span></span>
<span data-ttu-id="78f72-233">[archivio GitHub Socket.IO]: https://github.com/socketio/socket.io</span><span class="sxs-lookup"><span data-stu-id="78f72-233">[Socket.IO GitHub repository]: https://github.com/socketio/socket.io</span></span>
<span data-ttu-id="78f72-234">[versione archiviata ZIP o GZ]: https://github.com/socketio/socket.io/releases</span><span class="sxs-lookup"><span data-stu-id="78f72-234">[ZIP or GZ archived release]: https://github.com/socketio/socket.io/releases</span></span>

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
