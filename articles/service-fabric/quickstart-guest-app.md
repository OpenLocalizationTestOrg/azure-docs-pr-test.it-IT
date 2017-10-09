---
title: aaaQuickly distribuire un cluster di Azure Service Fabric tooan app esistente
description: Usare un toohost di cluster di Azure Service Fabric un'applicazione Node.js esistente con Visual Studio.
services: service-fabric
documentationcenter: nodejs
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: adegeo
ms.openlocfilehash: 20a3eb4a9206ba465acf96d0976ba241b07158bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a><span data-ttu-id="0a359-103">Ospitare un'applicazione Node.js in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0a359-103">Host a Node.js application on Azure Service Fabric</span></span>

<span data-ttu-id="0a359-104">Questa Guida rapida consente di distribuire un cluster di Service Fabric tooa applicazione (Node.js in questo esempio) esistente in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="0a359-104">This quickstart helps you deploy an existing application (Node.js in this example) tooa Service Fabric cluster running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a359-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0a359-105">Prerequisites</span></span>

<span data-ttu-id="0a359-106">Prima di iniziare, assicurarsi di avere [configurato l'ambiente di sviluppo](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0a359-106">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="0a359-107">Che include l'installazione di Service Fabric SDK hello e Visual Studio 2017 o 2015.</span><span class="sxs-lookup"><span data-stu-id="0a359-107">Which includes installing hello Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

<span data-ttu-id="0a359-108">È inoltre necessario toohave un'applicazione Node.js esistente per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0a359-108">You also need toohave an existing Node.js application for deployment.</span></span> <span data-ttu-id="0a359-109">In questa guida introduttiva viene usato un semplice sito Web Node.js che può essere scaricato [qui][download-sample].</span><span class="sxs-lookup"><span data-stu-id="0a359-109">This quickstart uses a simple Node.js website that can be downloaded [here][download-sample].</span></span> <span data-ttu-id="0a359-110">Estrarre il file tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` cartella dopo aver creato il progetto di hello nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="0a359-110">Extract this file tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` folder after you create hello project in hello next step.</span></span>

<span data-ttu-id="0a359-111">Se non si ha una sottoscrizione di Azure, creare un [account gratuito][create-account].</span><span class="sxs-lookup"><span data-stu-id="0a359-111">If you don't have an Azure subscription, create a [free account][create-account].</span></span>

## <a name="create-hello-service"></a><span data-ttu-id="0a359-112">Creare il servizio hello</span><span class="sxs-lookup"><span data-stu-id="0a359-112">Create hello service</span></span>

<span data-ttu-id="0a359-113">Avviare Visual Studio come **amministratore**.</span><span class="sxs-lookup"><span data-stu-id="0a359-113">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="0a359-114">Creare un progetto con `CTRL`+`SHIFT`+`N`.</span><span class="sxs-lookup"><span data-stu-id="0a359-114">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="0a359-115">In hello **nuovo progetto** finestra di dialogo, scegliere **Cloud > applicazione di Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="0a359-115">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="0a359-116">Nome di un'applicazione hello **MyGuestApp** e premere **OK**.</span><span class="sxs-lookup"><span data-stu-id="0a359-116">Name hello application **MyGuestApp** and press **OK**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="0a359-117">Node.js corre il limite di caratteri per i percorsi di windows con 260 hello.</span><span class="sxs-lookup"><span data-stu-id="0a359-117">Node.js can easily break hello 260 character limit for paths that windows has.</span></span> <span data-ttu-id="0a359-118">Usare un percorso breve per il progetto hello stesso, ad esempio **c:\code\svc1**.</span><span class="sxs-lookup"><span data-stu-id="0a359-118">Use a short path for hello project itself such as **c:\code\svc1**.</span></span>
   
![Finestra di dialogo Nuovo progetto in Visual Studio][new-project]

<span data-ttu-id="0a359-120">È possibile creare qualsiasi tipo di servizio di Service Fabric dalla finestra di dialogo successiva hello.</span><span class="sxs-lookup"><span data-stu-id="0a359-120">You can create any type of Service Fabric service from hello next dialog.</span></span> <span data-ttu-id="0a359-121">Per questa guida introduttiva scegliere **Eseguibile guest**.</span><span class="sxs-lookup"><span data-stu-id="0a359-121">For this quickstart, choose **Guest Executable**.</span></span>

<span data-ttu-id="0a359-122">Nome servizio hello **MyGuestService** e impostare le opzioni di hello in toohello destra hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="0a359-122">Name hello service **MyGuestService** and set hello options on hello right toohello following values:</span></span>

| <span data-ttu-id="0a359-123">Impostazione</span><span class="sxs-lookup"><span data-stu-id="0a359-123">Setting</span></span>                   | <span data-ttu-id="0a359-124">Valore</span><span class="sxs-lookup"><span data-stu-id="0a359-124">Value</span></span> |
| ------------------------- | ------ |
| <span data-ttu-id="0a359-125">Cartella del pacchetto di codice</span><span class="sxs-lookup"><span data-stu-id="0a359-125">Code Package Folder</span></span>       | <span data-ttu-id="0a359-126">_&lt;cartella Hello con l'app Node.js&gt;_</span><span class="sxs-lookup"><span data-stu-id="0a359-126">_&lt;hello folder with your Node.js app&gt;_</span></span> |
| <span data-ttu-id="0a359-127">Comportamento del pacchetto di codice</span><span class="sxs-lookup"><span data-stu-id="0a359-127">Code Package Behavior</span></span>     | <span data-ttu-id="0a359-128">Copiare tooproject contenuto cartella</span><span class="sxs-lookup"><span data-stu-id="0a359-128">Copy folder contents tooproject</span></span> |
| <span data-ttu-id="0a359-129">Programma</span><span class="sxs-lookup"><span data-stu-id="0a359-129">Program</span></span>                   | <span data-ttu-id="0a359-130">node.exe</span><span class="sxs-lookup"><span data-stu-id="0a359-130">node.exe</span></span> |
| <span data-ttu-id="0a359-131">Argomenti</span><span class="sxs-lookup"><span data-stu-id="0a359-131">Arguments</span></span>                 | <span data-ttu-id="0a359-132">server.js</span><span class="sxs-lookup"><span data-stu-id="0a359-132">server.js</span></span> |
| <span data-ttu-id="0a359-133">Cartella di lavoro</span><span class="sxs-lookup"><span data-stu-id="0a359-133">Working Folder</span></span>            | <span data-ttu-id="0a359-134">CodePackage</span><span class="sxs-lookup"><span data-stu-id="0a359-134">CodePackage</span></span> |

<span data-ttu-id="0a359-135">Premere **OK**.</span><span class="sxs-lookup"><span data-stu-id="0a359-135">Press **OK**.</span></span>

![Finestra di dialogo Nuovo servizio in Visual Studio][new-service]

<span data-ttu-id="0a359-137">Visual Studio crea il progetto di applicazione hello e il progetto di servizio actor hello e li visualizza in Esplora soluzioni.</span><span class="sxs-lookup"><span data-stu-id="0a359-137">Visual Studio creates hello application project and hello actor service project and displays them in Solution Explorer.</span></span>

<span data-ttu-id="0a359-138">progetto di applicazione Hello (**MyGuestApp**) non contiene il codice direttamente.</span><span class="sxs-lookup"><span data-stu-id="0a359-138">hello application project (**MyGuestApp**) does not contain any code directly.</span></span> <span data-ttu-id="0a359-139">Fa invece riferimento a un set di progetti di servizio.</span><span class="sxs-lookup"><span data-stu-id="0a359-139">Instead, it references a set of service projects.</span></span> <span data-ttu-id="0a359-140">Include inoltre altri tre tipi di contenuto:</span><span class="sxs-lookup"><span data-stu-id="0a359-140">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="0a359-141">**Profili di pubblicazione**</span><span class="sxs-lookup"><span data-stu-id="0a359-141">**Publish profiles**</span></span>  
<span data-ttu-id="0a359-142">Preferenze relative agli strumenti per diversi ambienti.</span><span class="sxs-lookup"><span data-stu-id="0a359-142">Tooling preferences for different environments.</span></span>

* <span data-ttu-id="0a359-143">**Script**</span><span class="sxs-lookup"><span data-stu-id="0a359-143">**Scripts**</span></span>  
<span data-ttu-id="0a359-144">Script di PowerShell per distribuire o aggiornare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0a359-144">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="0a359-145">**Definizione di applicazione**</span><span class="sxs-lookup"><span data-stu-id="0a359-145">**Application definition**</span></span>  
<span data-ttu-id="0a359-146">Manifesto dell'applicazione hello in include *ApplicationPackageRoot*.</span><span class="sxs-lookup"><span data-stu-id="0a359-146">Includes hello application manifest under *ApplicationPackageRoot*.</span></span> <span data-ttu-id="0a359-147">I file dei parametri dell'applicazione associati sono in *ApplicationParameters*, che definiscono l'applicazione hello e consentono di tooconfigure in modo specifico per un determinato ambiente.</span><span class="sxs-lookup"><span data-stu-id="0a359-147">Associated application parameter files are under *ApplicationParameters*, which define hello application and allow you tooconfigure it specifically for a given environment.</span></span>
    
<span data-ttu-id="0a359-148">Per una panoramica del contenuto di hello hello del progetto di servizio, vedere [Introduzione a servizi affidabili](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="0a359-148">For an overview of hello contents of hello service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="set-up-networking"></a><span data-ttu-id="0a359-149">Configurare la rete</span><span class="sxs-lookup"><span data-stu-id="0a359-149">Set up networking</span></span>

<span data-ttu-id="0a359-150">esempio Hello app Node.js si sta distribuendo utilizza la porta **80** e dobbiamo tootell Service Fabric che è necessario che la porta esposti.</span><span class="sxs-lookup"><span data-stu-id="0a359-150">hello example Node.js app we're deploying uses port **80** and we need tootell Service Fabric that we need that port exposed.</span></span>

<span data-ttu-id="0a359-151">Aprire hello **ServiceManifest.xml** file nel progetto hello.</span><span class="sxs-lookup"><span data-stu-id="0a359-151">Open hello **ServiceManifest.xml** file in hello project.</span></span> <span data-ttu-id="0a359-152">Nella parte inferiore di hello del manifesto di hello, sussiste un `<Resources> \ <Endpoints>` con una voce già definita.</span><span class="sxs-lookup"><span data-stu-id="0a359-152">At hello bottom of hello manifest, there is a `<Resources> \ <Endpoints>` with an entry already defined.</span></span> <span data-ttu-id="0a359-153">Modificare tooadd tale voce `Port`, `Protocol`, e `Type`.</span><span class="sxs-lookup"><span data-stu-id="0a359-153">Modify that entry tooadd `Port`, `Protocol`, and `Type`.</span></span> 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-tooazure"></a><span data-ttu-id="0a359-154">Distribuire tooAzure</span><span class="sxs-lookup"><span data-stu-id="0a359-154">Deploy tooAzure</span></span>

<span data-ttu-id="0a359-155">Se si preme **F5** ed eseguire il progetto di hello, è cluster locale toohello distribuito.</span><span class="sxs-lookup"><span data-stu-id="0a359-155">If you press **F5** and run hello project, it is deployed toohello local cluster.</span></span> <span data-ttu-id="0a359-156">Tuttavia, consente di distribuire tooAzure invece.</span><span class="sxs-lookup"><span data-stu-id="0a359-156">However, let's deploy tooAzure instead.</span></span>

<span data-ttu-id="0a359-157">Fare clic sul progetto hello e scegliere **pubblica...**  che viene aperto un tooAzure toopublish finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="0a359-157">Right-click on hello project and choose **Publish...** which opens a dialog toopublish tooAzure.</span></span>

![Finestra di dialogo tooazure per un servizio di service fabric pubblicazione][publish]

<span data-ttu-id="0a359-159">Seleziona hello **PublishProfiles\Cloud.xml** profilo di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0a359-159">Select hello **PublishProfiles\Cloud.xml** target profile.</span></span>

<span data-ttu-id="0a359-160">Se non è stato in precedenza, scegliere un account di Azure di toodeploy per.</span><span class="sxs-lookup"><span data-stu-id="0a359-160">If you haven't previously, choose an Azure account toodeploy to.</span></span> <span data-ttu-id="0a359-161">Se non si ha ancora un account, è possibile [iscriversi per ottenerne uno][create-account].</span><span class="sxs-lookup"><span data-stu-id="0a359-161">If you don't have one yet, [sign-up for one][create-account].</span></span>

<span data-ttu-id="0a359-162">In **Endpoint della connessione**, selezionare hello toodeploy cluster Service Fabric per.</span><span class="sxs-lookup"><span data-stu-id="0a359-162">Under **Connection Endpoint**, select hello Service Fabric cluster toodeploy to.</span></span> <span data-ttu-id="0a359-163">Se non si dispone di uno, selezionare  **&lt;creare un nuovo Cluster... &gt;**  che apre toohello di finestra del browser web portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a359-163">If you do not have one, select **&lt;Create New Cluster...&gt;** which opens up web browser window toohello Azure portal.</span></span> <span data-ttu-id="0a359-164">Per ulteriori informazioni, vedere [creare un cluster nel portale di hello](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="0a359-164">For more information, see [create a cluster in hello portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span></span> 

<span data-ttu-id="0a359-165">Quando si crea il cluster di Service Fabric hello, assicurarsi che hello tooset **endpoint personalizzato** impostazione troppo**80**.</span><span class="sxs-lookup"><span data-stu-id="0a359-165">When you create hello Service Fabric cluster, make sure tooset hello **Custom endpoints** setting too**80**.</span></span>

![Configurazione del tipo di nodo di Service Fabric con endpoint personalizzato][custom-endpoint]

<span data-ttu-id="0a359-167">Creare un nuovo cluster di Service Fabric accetta alcuni toocomplete ora.</span><span class="sxs-lookup"><span data-stu-id="0a359-167">Creating a new Service Fabric cluster takes some time toocomplete.</span></span> <span data-ttu-id="0a359-168">Dopo che è stato creato, andare toohello back-finestra di dialogo pubblicazione e selezionare  **&lt;aggiornamento&gt;**.</span><span class="sxs-lookup"><span data-stu-id="0a359-168">Once it has been created, go back toohello publish dialog and select **&lt;Refresh&gt;**.</span></span> <span data-ttu-id="0a359-169">il nuovo cluster di Hello è elencato nella casella di riepilogo a discesa hello. selezionarla.</span><span class="sxs-lookup"><span data-stu-id="0a359-169">hello new cluster is listed in hello drop-down box; select it.</span></span>

<span data-ttu-id="0a359-170">Premere **pubblica** e attendere hello toofinish di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0a359-170">Press **Publish** and wait for hello deployment toofinish.</span></span>

<span data-ttu-id="0a359-171">L'operazione potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="0a359-171">This may take a few minutes.</span></span> <span data-ttu-id="0a359-172">Una volta completato, potrebbe richiedere alcuni minuti per toobe applicazione hello completamente disponibile.</span><span class="sxs-lookup"><span data-stu-id="0a359-172">After it completes, it may take a few more minutes for hello application toobe fully available.</span></span>

## <a name="test-hello-website"></a><span data-ttu-id="0a359-173">Sito Web hello di test</span><span class="sxs-lookup"><span data-stu-id="0a359-173">Test hello website</span></span>

<span data-ttu-id="0a359-174">Dopo che è stato pubblicato, testare il servizio in un Web browser.</span><span class="sxs-lookup"><span data-stu-id="0a359-174">After your service has been published, test it in a web browser.</span></span> 

<span data-ttu-id="0a359-175">Innanzitutto, aprire hello portale di Azure e trovare il servizio Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0a359-175">First, open hello Azure portal and find your Service Fabric service.</span></span>

<span data-ttu-id="0a359-176">Controllare il pannello Panoramica hello hello nell'indirizzo di assistenza.</span><span class="sxs-lookup"><span data-stu-id="0a359-176">Check hello overview blade of hello service address.</span></span> <span data-ttu-id="0a359-177">Utilizza il nome di dominio da hello hello _endpoint della connessione Client_ proprietà.</span><span class="sxs-lookup"><span data-stu-id="0a359-177">Use hello domain name from hello _Client connection endpoint_ property.</span></span> <span data-ttu-id="0a359-178">ad esempio `http://mysvcfab1.westus2.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="0a359-178">For example, `http://mysvcfab1.westus2.cloudapp.azure.com`.</span></span>

![Pannello della panoramica dell'infrastruttura del servizio nel portale di Azure hello][overview]

<span data-ttu-id="0a359-180">Passare l'indirizzo toothis in cui verrà visualizzato hello `HELLO WORLD` risposta.</span><span class="sxs-lookup"><span data-stu-id="0a359-180">Navigate toothis address where you will see hello `HELLO WORLD` response.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="0a359-181">Eliminare il cluster hello</span><span class="sxs-lookup"><span data-stu-id="0a359-181">Delete hello cluster</span></span>

<span data-ttu-id="0a359-182">Non dimenticare toodelete tutte le risorse di hello che hai creato per questa Guida rapida, come vengono addebitate per tali risorse.</span><span class="sxs-lookup"><span data-stu-id="0a359-182">Do not forget toodelete all of hello resources you've created for this quickstart, as you are charged for those resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a359-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0a359-183">Next steps</span></span>
<span data-ttu-id="0a359-184">Altre informazioni sugli [eseguibili guest](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="0a359-184">Read more about [guest executables](service-fabric-deploy-existing-app.md).</span></span>

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F