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
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a><span data-ttu-id="81077-103">Creazione di un'applicazione di chat Node.js con Socket.IO in Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="81077-103">Create a Node.js chat application with Socket.IO in Azure App Service</span></span>
<span data-ttu-id="81077-104">Socket.IO fornisce comunicazioni in tempo reale tra il server node.js e i client usando WebSocket.</span><span class="sxs-lookup"><span data-stu-id="81077-104">Socket.IO provides real-time communication between your node.js server and clients using WebSockets.</span></span> <span data-ttu-id="81077-105">Supporta inoltre i trasporti tooother fallback (ad esempio polling lungo) che funziona con i browser meno recenti.</span><span class="sxs-lookup"><span data-stu-id="81077-105">It also supports fallback tooother transports (such as long polling) that work with older browsers.</span></span> <span data-ttu-id="81077-106">In questa esercitazione verrà illustrati l'hosting di un'applicazione di chat Socket.IO basato su come un'app web di Azure e mostrano come tooscale hello applicazione utilizzando [Cache Redis di Azure].</span><span class="sxs-lookup"><span data-stu-id="81077-106">This tutorial will walk you through hosting a Socket.IO based chat application as an Azure web app, and show you how tooscale hello application using [Azure Redis Cache].</span></span> <span data-ttu-id="81077-107">Per altre informazioni su Socket.IO, vedere <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="81077-107">For more information on Socket.IO, see <http://socket.io/>.</span></span>

> [!NOTE]
> <span data-ttu-id="81077-108">procedure di Hello in questa attività si applicano troppo[App del servizio Web App]; per i servizi Cloud, vedere [compilare un'applicazione di Chat Node.js con Socket.IO su un servizio Cloud Azure].</span><span class="sxs-lookup"><span data-stu-id="81077-108">hello procedures in this task apply too[App Service Web Apps]; for Cloud Services, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>
> 
> 

## <a name="download-hello-chat-example"></a><span data-ttu-id="81077-109">Scaricare l'esempio di chat hello</span><span class="sxs-lookup"><span data-stu-id="81077-109">Download hello chat example</span></span>
<span data-ttu-id="81077-110">Per questo progetto, si utilizzerà l'esempio di chat hello dalla hello [repository Socket.IO GitHub].</span><span class="sxs-lookup"><span data-stu-id="81077-110">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="81077-111">Eseguire l'esempio hello toodownload di passaggi seguente hello e aggiungerla toohello progetto creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="81077-111">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="81077-112">Scaricare un [ZIP o GZ archiviati versione] del progetto Socket.IO hello (versione 1.3.5 è stato utilizzato per questo documento)</span><span class="sxs-lookup"><span data-stu-id="81077-112">Download a [ZIP or GZ archived release] of hello Socket.IO project (version 1.3.5 was used for this document)</span></span>
2. <span data-ttu-id="81077-113">Estrarre hello di archiviazione e copia hello **esempi\\chat** nuovo percorso di directory tooa.</span><span class="sxs-lookup"><span data-stu-id="81077-113">Extract hello archive and copy hello **examples\\chat** directory tooa new location.</span></span> <span data-ttu-id="81077-114">Ad esempio, **\\node\\chat**.</span><span class="sxs-lookup"><span data-stu-id="81077-114">For example, **\\node\\chat**.</span></span>

## <a name="modify-appjs-and-install-modules"></a><span data-ttu-id="81077-115">Modificare app.js e installare i moduli</span><span class="sxs-lookup"><span data-stu-id="81077-115">Modify app.js and install modules</span></span>
1. <span data-ttu-id="81077-116">Rinominare hello **index.js** file troppo**app.js**.</span><span class="sxs-lookup"><span data-stu-id="81077-116">Rename hello **index.js** file too**app.js**.</span></span> <span data-ttu-id="81077-117">In questo modo toodetect Azure che si tratta di un'applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="81077-117">This allows Azure toodetect that this is a Node.js application.</span></span>
2. <span data-ttu-id="81077-118">Aprire hello **app.js** file in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="81077-118">Open hello **app.js** file in a text editor.</span></span> <span data-ttu-id="81077-119">Modifica hello riga contenente `var io = require('../..')(server);` come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="81077-119">Change hello line containing `var io = require('../..')(server);` as shown below:</span></span>
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. <span data-ttu-id="81077-120">Aprire hello **package. JSON** file e aggiungere un riferimento toosocket.io in `dependencies`, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="81077-120">Open hello **package.json** file and add a reference toosocket.io under `dependencies`, as shown below:</span></span>
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. <span data-ttu-id="81077-121">Hello della riga di comando, modificare toohello  **\\nodo\\chat** directory e utilizzare npm tooinstall hello i moduli necessari per questa applicazione:</span><span class="sxs-lookup"><span data-stu-id="81077-121">From hello command-line, change toohello **\\node\\chat** directory and use npm tooinstall hello modules required by this application:</span></span>
   
        npm install
   
    <span data-ttu-id="81077-122">I moduli di hello verrà installato in una sottocartella denominata **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="81077-122">This will install hello modules into a subfolder named **node_modules**.</span></span>

## <a name="create-an-azure-web-app"></a><span data-ttu-id="81077-123">Creare un'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="81077-123">Create an Azure Web App</span></span>
<span data-ttu-id="81077-124">Seguire questi toocreate passaggi un'app web di Azure, abilitare la pubblicazione Git e quindi abilitare il supporto di WebSocket per l'app web hello.</span><span class="sxs-lookup"><span data-stu-id="81077-124">Follow these steps toocreate an Azure web app, enable Git publishing, and then enable WebSocket support for hello web app.</span></span>

> [!NOTE]
> <span data-ttu-id="81077-125">toocomplete questa esercitazione, è necessario un account di Azure.</span><span class="sxs-lookup"><span data-stu-id="81077-125">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="81077-126">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="81077-126">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="81077-127">Per informazioni dettagliate, vedere la pagina relativa alla <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">versione di valutazione gratuita di Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="81077-127">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

1. <span data-ttu-id="81077-128">Installare l'interfaccia della riga di comando di Azure (Azure CLI) hello e connettersi tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="81077-128">Install hello Azure Command-Line Interface (Azure CLI) and connect tooyour Azure subscription.</span></span> <span data-ttu-id="81077-129">Vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="81077-129">See [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="81077-130">Se questa è la prima impostazione del tempo di un archivio in Azure, è necessario toocreate le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="81077-130">If this is your first time setting up a repository in Azure, you need toocreate login credentials.</span></span> <span data-ttu-id="81077-131">Hello CLI di Azure, digitare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="81077-131">From hello Azure CLI, enter hello following command:</span></span>
   
        azure site deployment user set [username] [password]
3. <span data-ttu-id="81077-132">Modificare toohello  **\\node\chat** directory e seguente hello utilizzare comandi toocreate una nuova app web di Azure e un archivio Git locale.</span><span class="sxs-lookup"><span data-stu-id="81077-132">Change toohello **\\node\chat** directory and use hello following command toocreate a new Azure web app and a local Git repository.</span></span> <span data-ttu-id="81077-133">Verrà inoltre creato un repository Git remoto denominato .</span><span class="sxs-lookup"><span data-stu-id="81077-133">This command also creates a Git remote named 'azure'.</span></span>
   
        azure site create mysitename --git
   
    <span data-ttu-id="81077-134">Sostituire "mysitename" con un nome univoco per il sito Web.</span><span class="sxs-lookup"><span data-stu-id="81077-134">You must replace 'mysitename' with a unique name for your web app.</span></span>
4. <span data-ttu-id="81077-135">Eseguire il commit repository locale di hello esistente file toohello utilizzando hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="81077-135">Commit hello existing files toohello local repository by using hello following commands:</span></span>
   
        git add .
        git commit -m "Initial commit"
5. <span data-ttu-id="81077-136">Esegui il push del repository di hello file toohello App Web di Azure con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="81077-136">Push hello files toohello Azure Web Apps repository with hello following command:</span></span>
   
        git push azure master
   
    <span data-ttu-id="81077-137">Quando richiesto, immettere le credenziali dal passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="81077-137">When prompted, enter your credentials from step 2.</span></span> <span data-ttu-id="81077-138">Come i moduli vengono importati nel server di hello, si riceverà i messaggi di stato.</span><span class="sxs-lookup"><span data-stu-id="81077-138">You will receive status messages as modules are imported on hello server.</span></span> <span data-ttu-id="81077-139">Al termine di questo processo, un'applicazione hello verrà ospitata in un'applicazione web di Azure.</span><span class="sxs-lookup"><span data-stu-id="81077-139">Once this process has completed, hello application will be hosted on your Azure web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="81077-140">Durante l'installazione del modulo, è possibile riscontrare errori che ' hello progetto importato non è stato trovato '.</span><span class="sxs-lookup"><span data-stu-id="81077-140">During module installation, you may notice errors that 'hello imported project ... was not found'.</span></span> <span data-ttu-id="81077-141">Tali errori possono essere ignorati.</span><span class="sxs-lookup"><span data-stu-id="81077-141">These can safely be ignored.</span></span>
   > 
   > 
6. <span data-ttu-id="81077-142">Socket.IO utilizza i WebSocket che non sono abilitati per impostazione predefinita in Azure.</span><span class="sxs-lookup"><span data-stu-id="81077-142">Socket.IO uses WebSockets, which are not enabled by default on Azure.</span></span> <span data-ttu-id="81077-143">i socket web tooenable utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="81077-143">tooenable web sockets, use hello following command:</span></span>
   
        azure site set -w
   
    <span data-ttu-id="81077-144">Se richiesto, immettere il nome di hello dell'app web hello.</span><span class="sxs-lookup"><span data-stu-id="81077-144">If prompted, enter hello name of hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="81077-145">Hello 'set -w sito azure' verrà comando funziona solo con versione 0.7.4 o successiva di hello interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="81077-145">hello 'azure site set -w' command will work only with version 0.7.4 or higher of hello Azure Command-Line Interface.</span></span> <span data-ttu-id="81077-146">È inoltre possibile abilitare il supporto di WebSocket con hello [portale Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="81077-146">You can also enable WebSocket support using hello [Azure Portal](https://portal.azure.com).</span></span>
   > 
   > <span data-ttu-id="81077-147">utilizzo di WebSockets tooenable hello portale di Azure, fare clic su app web hello dal pannello App Web hello, fare clic su **tutte le impostazioni** > **le impostazioni dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="81077-147">tooenable WebSockets using hello Azure Portal, click hello web app from hello Web Apps blade, click **All settings** > **Application settings**.</span></span> <span data-ttu-id="81077-148">In **Web Socket** fare clic su **Attivato**.</span><span class="sxs-lookup"><span data-stu-id="81077-148">Under **Web Sockets**, click **On**.</span></span> <span data-ttu-id="81077-149">Fare quindi clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="81077-149">Then click **Save**.</span></span>
   > 
   > 
7. <span data-ttu-id="81077-150">tooview hello app web seguenti di hello Azure, utilizzare comando toolaunch web browser e passare l'app web toohello ospitato:</span><span class="sxs-lookup"><span data-stu-id="81077-150">tooview hello web app on Azure, use hello following command toolaunch your web browser and navigate toohello hosted web app:</span></span>
   
        azure site browse

<span data-ttu-id="81077-151">L'app ora è in esecuzione in Azure ed è in grado di inoltrare i messaggi di chat tra diversi client tramite Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="81077-151">Your app is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

## <a name="scale-out"></a><span data-ttu-id="81077-152">Scalabilità orizzontale</span><span class="sxs-lookup"><span data-stu-id="81077-152">Scale out</span></span>
<span data-ttu-id="81077-153">Applicazioni Socket.IO possono essere scalate orizzontalmente con un **adapter** toodistribute messaggi e gli eventi tra più istanze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="81077-153">Socket.IO applications can be scaled out by using an **adapter** toodistribute messages and events between multiple application instances.</span></span> <span data-ttu-id="81077-154">Anche se sono presenti più schede, hello [socket.io redis] adapter può essere utilizzato con funzionalità di Cache Redis di Azure hello facilmente.</span><span class="sxs-lookup"><span data-stu-id="81077-154">While there are several adapters available, hello [socket.io-redis] adapter can be easily used with hello Azure Redis Cache feature.</span></span>

> [!NOTE]
> <span data-ttu-id="81077-155">Un ulteriore requisito per la scalabilità orizzontale di una soluzione Socket.IO è il supporto di sessioni permanenti.</span><span class="sxs-lookup"><span data-stu-id="81077-155">An additional requirement for scaling out a Socket.IO solution is support for sticky sessions.</span></span> <span data-ttu-id="81077-156">Le sessioni permanenti sono abilitate per impostazione predefinita per le app Web di Azure tramite il routing delle richieste di Azure.</span><span class="sxs-lookup"><span data-stu-id="81077-156">Sticky sessions are enabled by default for Azure Web Apps through Azure Request Routing.</span></span> <span data-ttu-id="81077-157">Per altre informazioni, vedere il blog relativo all' [affinità delle istanze in Siti Web di Azure]</span><span class="sxs-lookup"><span data-stu-id="81077-157">For more information, see [Instance Affinity in Azure Web Sites].</span></span>
> 
> 

### <a name="create-a-redis-cache"></a><span data-ttu-id="81077-158">Creare una cache Redis</span><span class="sxs-lookup"><span data-stu-id="81077-158">Create a Redis cache</span></span>
<span data-ttu-id="81077-159">Eseguire i passaggi di hello in [creare una cache in Cache Redis di Azure] toocreate una nuova cache.</span><span class="sxs-lookup"><span data-stu-id="81077-159">Perform hello steps in [Create a cache in Azure Redis Cache] toocreate a new cache.</span></span>

> [!NOTE]
> <span data-ttu-id="81077-160">Salvare hello **nome Host** e **chiave primaria** per la cache, come queste saranno necessarie hello passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="81077-160">Save hello **Host name** and **Primary key** for your cache, as these will be needed in hello next steps.</span></span>
> 
> 

### <a name="add-hello-redis-and-socketio-redis-modules"></a><span data-ttu-id="81077-161">Aggiungere redis hello e moduli socket.io redis</span><span class="sxs-lookup"><span data-stu-id="81077-161">Add hello redis and socket.io-redis modules</span></span>
1. <span data-ttu-id="81077-162">Dalla riga di comando, modificare toohello  **\\nodo\\chat** directory e utilizzare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="81077-162">From a command-line, change toohello **\\node\\chat** directory and use hello following command.</span></span>
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > <span data-ttu-id="81077-163">versioni di Hello specificate in questo comando sono versioni hello utilizzate per la verifica di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="81077-163">hello versions specified in this command are hello versions used when testing this article.</span></span>
   > 
   > 
2. <span data-ttu-id="81077-164">Modificare hello **app.js** seguenti di hello tooadd file righe immediatamente dopo`var io = require('socket.io')(server);`</span><span class="sxs-lookup"><span data-stu-id="81077-164">Modify hello **app.js** file tooadd hello following lines immediately after `var io = require('socket.io')(server);`</span></span>
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    <span data-ttu-id="81077-165">Sostituire **redishostname** e **rediskey** con nome host hello e la chiave per la cache Redis.</span><span class="sxs-lookup"><span data-stu-id="81077-165">Replace **redishostname** and **rediskey** with hello host name and key for your Redis cache.</span></span>
   
    <span data-ttu-id="81077-166">Verrà creata una pubblicazione e sottoscrizione toohello client della cache Redis creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="81077-166">This will create a publish and subscribe client toohello Redis cache created previously.</span></span> <span data-ttu-id="81077-167">i client Hello vengono quindi utilizzati con hello adapter tooconfigure cache Redis di Socket.IO toouse hello per il passaggio di messaggi e gli eventi tra le istanze dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="81077-167">hello clients are then used with hello adapter tooconfigure Socket.IO toouse hello Redis cache for passing messages and events between instances of your application</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="81077-168">Durante la hello **socket.io redis** adapter può comunicare direttamente tooRedis, la versione corrente di hello non supporta l'autenticazione di hello richiesto dalla cache Redis di Azure.</span><span class="sxs-lookup"><span data-stu-id="81077-168">While hello **socket.io-redis** adapter can communicate directly tooRedis, hello current version does not support hello authentication required by Azure Redis cache.</span></span> <span data-ttu-id="81077-169">La connessione iniziale hello viene creato utilizzando hello **redis** modulo, quindi client hello viene passato toohello **socket.io redis** adapter.</span><span class="sxs-lookup"><span data-stu-id="81077-169">So hello initial connection is created using hello **redis** module, then hello client is passed toohello **socket.io-redis** adapter.</span></span>
   > 
   > <span data-ttu-id="81077-170">Durante la Cache Redis di Azure supporta connessioni protette tramite la porta 6380, moduli hello utilizzati in questo esempio non supportano le connessioni protette a partire da 14/7/2014.</span><span class="sxs-lookup"><span data-stu-id="81077-170">While Azure Redis Cache supports secure connections using port 6380, hello modules used in this example do not support secure connections as of 7/14/2014.</span></span> <span data-ttu-id="81077-171">Hello sopra codice utilizza hello predefinito, la porta non protetta di 6379.</span><span class="sxs-lookup"><span data-stu-id="81077-171">hello above code uses hello default, unsecure port of 6379.</span></span>
   > 
   > 
3. <span data-ttu-id="81077-172">Salva hello modificato **app.js**</span><span class="sxs-lookup"><span data-stu-id="81077-172">Save hello modified **app.js**</span></span>

### <a name="commit-changes-and-redeploy"></a><span data-ttu-id="81077-173">Eseguire il commit delle modifiche ed effettuare la ridistribuzione</span><span class="sxs-lookup"><span data-stu-id="81077-173">Commit changes and redeploy</span></span>
<span data-ttu-id="81077-174">Dalla riga di comando in hello hello  **\\nodo\\chat** directory, utilizzare hello modifiche toocommit i comandi seguenti e ridistribuire l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="81077-174">From hello command-line in hello **\\node\\chat** directory, use hello following commands toocommit changes and redeploy hello application.</span></span>

    git add .
    git commit -m "implementing scale out"
    git push azure master

<span data-ttu-id="81077-175">Una volta modifiche hello sono state inserite toohello server, è possibile ridimensionare il sito tra più istanze tramite hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="81077-175">Once hello changes have been pushed toohello server, you can scale your site across multiple instances by using hello following command.</span></span>

    azure site scale instances --instances #

<span data-ttu-id="81077-176">Dove  **#**  hello numero di istanze toocreate.</span><span class="sxs-lookup"><span data-stu-id="81077-176">Where **#** is hello number of instances toocreate.</span></span>

<span data-ttu-id="81077-177">È possibile connettersi app web tooyour da più computer o browser tooverify che i messaggi vengono inviati correttamente tooall client.</span><span class="sxs-lookup"><span data-stu-id="81077-177">You can connect tooyour web app from multiple browsers or computers tooverify that messages are correctly sent tooall clients.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="81077-178">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="81077-178">Troubleshooting</span></span>
### <a name="connection-limits"></a><span data-ttu-id="81077-179">Limiti di connessione</span><span class="sxs-lookup"><span data-stu-id="81077-179">Connection limits</span></span>
<span data-ttu-id="81077-180">Le app Web di Azure è disponibile in più SKU, che determinano sito tooyour disponibili risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="81077-180">Azure Web Apps is available in multiple SKUs, which determine hello resources available tooyour site.</span></span> <span data-ttu-id="81077-181">Ciò include il numero di hello di connessioni WebSocket consentite.</span><span class="sxs-lookup"><span data-stu-id="81077-181">This includes hello number of allowed WebSocket connections.</span></span> <span data-ttu-id="81077-182">Per ulteriori informazioni, vedere hello [pagina prezzi App Web].</span><span class="sxs-lookup"><span data-stu-id="81077-182">For more information, see hello [Web Apps Pricing page].</span></span>

### <a name="messages-arent-being-sent-using-websockets"></a><span data-ttu-id="81077-183">I messaggi non vengono inviati usando WebSocket</span><span class="sxs-lookup"><span data-stu-id="81077-183">Messages aren't being sent using WebSockets</span></span>
<span data-ttu-id="81077-184">Se il browser client mantenga fallback toolong polling anziché WebSocket, è possibile a causa di uno dei seguenti hello.</span><span class="sxs-lookup"><span data-stu-id="81077-184">If client browsers keep falling back toolong polling instead of using WebSockets, it may be because of one of hello following.</span></span>

* <span data-ttu-id="81077-185">**È possibile limitare hello trasporto toojust WebSocket**</span><span class="sxs-lookup"><span data-stu-id="81077-185">**Try limiting hello transport toojust WebSockets**</span></span>
  
    <span data-ttu-id="81077-186">Affinché Socket.IO toouse WebSocket come hello trasporto di messaggistica, hello server e client deve supportare WebSocket.</span><span class="sxs-lookup"><span data-stu-id="81077-186">In order for Socket.IO toouse WebSockets as hello messaging transport, both hello server and client must support WebSockets.</span></span> <span data-ttu-id="81077-187">Se uno o altri hello, non Socket.IO negozierà un altro trasporto, ad esempio di polling lungo.</span><span class="sxs-lookup"><span data-stu-id="81077-187">If one or hello other does not, Socket.IO will negotiate another transport, such as long polling.</span></span> <span data-ttu-id="81077-188">elenco predefinito di Hello dei trasporti utilizzati Socket.IO ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span><span class="sxs-lookup"><span data-stu-id="81077-188">hello default list of transports used by Socket.IO is ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span></span> <span data-ttu-id="81077-189">È possibile imporre l'uso tooonly WebSocket aggiungendo hello seguente codice toohello **app.js** file, dopo la riga hello contenente `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="81077-189">You can force it tooonly use WebSockets by adding hello following code toohello **app.js** file, after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > <span data-ttu-id="81077-190">Si noti che browser meno recenti che non supportano WebSocket non saranno in grado di tooconnect toohello sito mentre hello di sopra di codice è attiva, in quanto limita solo tooWebSockets di comunicazione.</span><span class="sxs-lookup"><span data-stu-id="81077-190">Note that older browsers that do not support WebSockets will not be able tooconnect toohello site while hello above code is active, as it restricts communication tooWebSockets only.</span></span>
  > 
  > 
* <span data-ttu-id="81077-191">**Usa SSL**</span><span class="sxs-lookup"><span data-stu-id="81077-191">**Use SSL**</span></span>
  
    <span data-ttu-id="81077-192">WebSocket si basano su alcuni meno intestazioni HTTP utilizzate, ad esempio hello **aggiornamento** intestazione.</span><span class="sxs-lookup"><span data-stu-id="81077-192">WebSockets relies on some lesser used HTTP headers, such as hello **Upgrade** header.</span></span> <span data-ttu-id="81077-193">Alcuni dispositivi di rete intermedi, come i proxy Web, possono rimuovere tali intestazioni.</span><span class="sxs-lookup"><span data-stu-id="81077-193">Some intermediate network devices, such as web proxies, may remove these headers.</span></span> <span data-ttu-id="81077-194">tooavoid questo problema, è possibile stabilire una connessione WebSocket hello tramite SSL.</span><span class="sxs-lookup"><span data-stu-id="81077-194">tooavoid this problem, you can establish hello WebSocket connection over SSL.</span></span>
  
    <span data-ttu-id="81077-195">Un modo semplice di tooaccomplish tratta tooconfigure Socket.IO troppo`match origin protocol`.</span><span class="sxs-lookup"><span data-stu-id="81077-195">An easy way tooaccomplish this is tooconfigure Socket.IO too`match origin protocol`.</span></span> <span data-ttu-id="81077-196">Questo indica hello comunicazione WebSocket toosecure di Socket.IO identico hello originari HTTP/HTTPS richiesta per la pagina web hello.</span><span class="sxs-lookup"><span data-stu-id="81077-196">This instructs Socket.IO toosecure WebSockets communication hello same as hello originating HTTP/HTTPS request for hello web page.</span></span> <span data-ttu-id="81077-197">Se un browser, viene utilizzato per il sito Web toovisit un URL HTTPS, le comunicazioni WebSocket successive tramite Socket.IO saranno protetti tramite SSL.</span><span class="sxs-lookup"><span data-stu-id="81077-197">If a browser uses an HTTPS URL toovisit your website, subsequent WebSocket communications through Socket.IO will be secured over SSL.</span></span>
  
    <span data-ttu-id="81077-198">toomodify tooenable in questo esempio questa configurazione, aggiungere hello seguente codice toohello **app.js** file dopo la riga hello contenente `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="81077-198">toomodify this example tooenable this configuration, add hello following code toohello **app.js** file after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* <span data-ttu-id="81077-199">**Verificare le impostazioni del file web.config**</span><span class="sxs-lookup"><span data-stu-id="81077-199">**Verify web.config settings**</span></span>
  
    <span data-ttu-id="81077-200">App web di Azure che ospitano applicazioni Node.js utilizzare hello **Web. config** tooroute file in ingresso richieste applicazione Node.js toohello.</span><span class="sxs-lookup"><span data-stu-id="81077-200">Azure web apps that host Node.js applications use hello **web.config** file tooroute incoming requests toohello Node.js application.</span></span> <span data-ttu-id="81077-201">Per WebSocket toofunction correttamente con le applicazioni Node.js, hello **Web. config** deve contenere hello entrata.</span><span class="sxs-lookup"><span data-stu-id="81077-201">For WebSockets toofunction correctly with Node.js applications, hello **web.config** must contain hello following entry.</span></span>
  
        <webSocket enabled="false"/>
  
    <span data-ttu-id="81077-202">Disabilita il modulo IIS WebSocket hello, che include la propria implementazione di WebSocket e in conflitto con WebSocket moduli Node.js specifici, ad esempio Socket.IO.</span><span class="sxs-lookup"><span data-stu-id="81077-202">This disables hello IIS WebSockets module, which includes its own implementation of WebSockets and conflicts with Node.js specific WebSocket modules such as Socket.IO.</span></span> <span data-ttu-id="81077-203">Se questa riga non è presente o è troppo`true`, è possibile motivo hello trasporto WebSocket hello non funzionante per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="81077-203">If this line is not present, or is set too`true`, this may be hello reason that hello WebSocket transport is not working for your application.</span></span>
  
    <span data-ttu-id="81077-204">Di norma le applicazioni Node.js non includono un file **web.config** , pertanto Siti Web di Azure ne genererà automaticamente uno per le applicazioni Node.js quando queste vengono distribuite.</span><span class="sxs-lookup"><span data-stu-id="81077-204">Normally, Node.js applications do not include a **web.config** file, so Azure Websites will automatically generate one for Node.js applications when they are deployed.</span></span> <span data-ttu-id="81077-205">Poiché questo file viene automaticamente generato sul server hello, è necessario utilizzare hello FTP o FTPS URL per il sito Web tooview questo file.</span><span class="sxs-lookup"><span data-stu-id="81077-205">Since this file is automatically generated on hello server, you must use hello FTP or FTPS URL for your website tooview this file.</span></span> <span data-ttu-id="81077-206">È possibile trovare hello FTP e FTPS URL per il sito nel portale classico hello selezionando l'app web e quindi hello **Dashboard** collegamento.</span><span class="sxs-lookup"><span data-stu-id="81077-206">You can find hello FTP and FTPS URLs for your site in hello classic portal by selecting your web app, and then hello **Dashboard** link.</span></span> <span data-ttu-id="81077-207">Hello gli URL vengono visualizzati in hello **riepilogo rapido** sezione.</span><span class="sxs-lookup"><span data-stu-id="81077-207">hello URLs are displayed in hello **quick glance** section.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="81077-208">Hello **Web. config** file viene generato solo per siti Web di Azure, se l'applicazione non ne fornisce uno.</span><span class="sxs-lookup"><span data-stu-id="81077-208">hello **web.config** file is only generated by Azure Websites if your application does not provide one.</span></span> <span data-ttu-id="81077-209">Se si fornisce un **Web. config** file nella radice del progetto di applicazione hello da utilizzare per le app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="81077-209">If you provide a **web.config** file in hello root of your application project, it will be used by Azure Web Apps.</span></span>
  > 
  > 
  
    <span data-ttu-id="81077-210">Se la voce hello non è presente o è impostata un valore di tooa `true`, sarà necessario creare un **Web. config** nella radice dell'applicazione Node.js hello e specificare un valore di `false`.</span><span class="sxs-lookup"><span data-stu-id="81077-210">If hello entry is not present, or is set tooa value of `true`, then you should create a **web.config** in hello root of your Node.js application and specify a value of `false`.</span></span>  <span data-ttu-id="81077-211">Per riferimento, hello seguente è un valore predefinito **Web. config** per un'applicazione che utilizza **app.js** come punto di ingresso hello.</span><span class="sxs-lookup"><span data-stu-id="81077-211">For reference, hello below is a default **web.config** for an application that uses **app.js** as hello entry point.</span></span>
  
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
  
    <span data-ttu-id="81077-212">Se l'applicazione utilizza un punto di ingresso diverso da **app.js**, è necessario sostituire tutte le occorrenze di **app.js** con hello correggere punto di ingresso.</span><span class="sxs-lookup"><span data-stu-id="81077-212">If your application uses an entry point other than **app.js**, you must replace all occurrences of **app.js** with hello correct entry point.</span></span> <span data-ttu-id="81077-213">ad esempio, la sostituzione di **app.js** con **server.js**.</span><span class="sxs-lookup"><span data-stu-id="81077-213">For example, replacing **app.js** with **server.js**.</span></span>

> [!NOTE]
> <span data-ttu-id="81077-214">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App], in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="81077-214">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="81077-215">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="81077-215">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="81077-216">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="81077-216">Next steps</span></span>
<span data-ttu-id="81077-217">In questa esercitazione è stato descritto come toocreate un'applicazione di chat ospitato in un'applicazione web di Azure.</span><span class="sxs-lookup"><span data-stu-id="81077-217">In this tutorial you learned how toocreate a chat application hosted in an Azure web app.</span></span> <span data-ttu-id="81077-218">È inoltre possibile ospitare l'applicazione come un servizio cloud di Azure.</span><span class="sxs-lookup"><span data-stu-id="81077-218">You can also host this application as an Azure Cloud Service.</span></span> <span data-ttu-id="81077-219">Per la procedura tooaccomplish questa operazione, vedere [compilare un'applicazione di Chat Node.js con Socket.IO su un servizio Cloud Azure].</span><span class="sxs-lookup"><span data-stu-id="81077-219">For steps on how tooaccomplish this, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>

<span data-ttu-id="81077-220">Per ulteriori informazioni, vedere anche hello [Centro per sviluppatori di Node.js].</span><span class="sxs-lookup"><span data-stu-id="81077-220">For more information, see also hello [Node.js Developer Center].</span></span>

## <a name="whats-changed"></a><span data-ttu-id="81077-221">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="81077-221">What's changed</span></span>
* <span data-ttu-id="81077-222">Per una Guida toohello modifica da siti Web tooApp servizio vedere: [servizio App di Azure e relativo impatto sui servizi di Azure esistente].</span><span class="sxs-lookup"><span data-stu-id="81077-222">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services].</span></span>

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
