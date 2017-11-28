---
title: Distribuire rapidamente un'app esistente in un cluster di Azure Service Fabric
description: Usare un cluster di Azure Service Fabric per ospitare un'applicazione Node.js esistente con Visual Studio.
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
ms.openlocfilehash: 3601b73872bbea4b4e5324382eb97b7384ca6e13
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a><span data-ttu-id="0566e-103">Ospitare un'applicazione Node.js in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0566e-103">Host a Node.js application on Azure Service Fabric</span></span>

<span data-ttu-id="0566e-104">Questa guida introduttiva illustra come distribuire un'applicazione esistente, in questo esempio Node.js, in un cluster di Service Fabric in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="0566e-104">This quickstart helps you deploy an existing application (Node.js in this example) to a Service Fabric cluster running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0566e-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0566e-105">Prerequisites</span></span>

<span data-ttu-id="0566e-106">Prima di iniziare, assicurarsi di avere [configurato l'ambiente di sviluppo](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0566e-106">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="0566e-107">Ciò include l'installazione di Service Fabric SDK e Visual Studio 2017 o 2015.</span><span class="sxs-lookup"><span data-stu-id="0566e-107">Which includes installing the Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

<span data-ttu-id="0566e-108">È anche necessaria un'applicazione Node.js esistente da distribuire.</span><span class="sxs-lookup"><span data-stu-id="0566e-108">You also need to have an existing Node.js application for deployment.</span></span> <span data-ttu-id="0566e-109">In questa guida introduttiva viene usato un semplice sito Web Node.js che può essere scaricato [qui][download-sample].</span><span class="sxs-lookup"><span data-stu-id="0566e-109">This quickstart uses a simple Node.js website that can be downloaded [here][download-sample].</span></span> <span data-ttu-id="0566e-110">Estrarre il file nella cartella `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` dopo aver creato il progetto nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="0566e-110">Extract this file to your `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` folder after you create the project in the next step.</span></span>

<span data-ttu-id="0566e-111">Se non si ha una sottoscrizione di Azure, creare un [account gratuito][create-account].</span><span class="sxs-lookup"><span data-stu-id="0566e-111">If you don't have an Azure subscription, create a [free account][create-account].</span></span>

## <a name="create-the-service"></a><span data-ttu-id="0566e-112">Creare il servizio</span><span class="sxs-lookup"><span data-stu-id="0566e-112">Create the service</span></span>

<span data-ttu-id="0566e-113">Avviare Visual Studio come **amministratore**.</span><span class="sxs-lookup"><span data-stu-id="0566e-113">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="0566e-114">Creare un progetto con `CTRL`+`SHIFT`+`N`.</span><span class="sxs-lookup"><span data-stu-id="0566e-114">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="0566e-115">Nella finestra di dialogo **Nuovo progetto** scegliere **Cloud > Applicazione di Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="0566e-115">In the **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="0566e-116">Assegnare all'applicazione il nome **MyGuestApp** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0566e-116">Name the application **MyGuestApp** and press **OK**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="0566e-117">Node.js può facilmente superare il limite di 260 caratteri per i percorsi presente in Windows.</span><span class="sxs-lookup"><span data-stu-id="0566e-117">Node.js can easily break the 260 character limit for paths that windows has.</span></span> <span data-ttu-id="0566e-118">Usare per il progetto un percorso breve, ad esempio **c:\code\svc1**.</span><span class="sxs-lookup"><span data-stu-id="0566e-118">Use a short path for the project itself such as **c:\code\svc1**.</span></span>
   
![Finestra di dialogo Nuovo progetto in Visual Studio][new-project]

<span data-ttu-id="0566e-120">Nella finestra di dialogo successiva è possibile creare qualsiasi tipo di servizio di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0566e-120">You can create any type of Service Fabric service from the next dialog.</span></span> <span data-ttu-id="0566e-121">Per questa guida introduttiva scegliere **Eseguibile guest**.</span><span class="sxs-lookup"><span data-stu-id="0566e-121">For this quickstart, choose **Guest Executable**.</span></span>

<span data-ttu-id="0566e-122">Assegnare al servizio il nome **MyGuestService** e impostare le opzioni a destra sui valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="0566e-122">Name the service **MyGuestService** and set the options on the right to the following values:</span></span>

| <span data-ttu-id="0566e-123">Impostazione</span><span class="sxs-lookup"><span data-stu-id="0566e-123">Setting</span></span>                   | <span data-ttu-id="0566e-124">Valore</span><span class="sxs-lookup"><span data-stu-id="0566e-124">Value</span></span> |
| ------------------------- | ------ |
| <span data-ttu-id="0566e-125">Cartella del pacchetto di codice</span><span class="sxs-lookup"><span data-stu-id="0566e-125">Code Package Folder</span></span>       | <span data-ttu-id="0566e-126">_&lt;cartella con l'app Node.js&gt;_</span><span class="sxs-lookup"><span data-stu-id="0566e-126">_&lt;the folder with your Node.js app&gt;_</span></span> |
| <span data-ttu-id="0566e-127">Comportamento del pacchetto di codice</span><span class="sxs-lookup"><span data-stu-id="0566e-127">Code Package Behavior</span></span>     | <span data-ttu-id="0566e-128">Copia il contenuto della cartella nel progetto</span><span class="sxs-lookup"><span data-stu-id="0566e-128">Copy folder contents to project</span></span> |
| <span data-ttu-id="0566e-129">Programma</span><span class="sxs-lookup"><span data-stu-id="0566e-129">Program</span></span>                   | <span data-ttu-id="0566e-130">node.exe</span><span class="sxs-lookup"><span data-stu-id="0566e-130">node.exe</span></span> |
| <span data-ttu-id="0566e-131">Argomenti</span><span class="sxs-lookup"><span data-stu-id="0566e-131">Arguments</span></span>                 | <span data-ttu-id="0566e-132">server.js</span><span class="sxs-lookup"><span data-stu-id="0566e-132">server.js</span></span> |
| <span data-ttu-id="0566e-133">Cartella di lavoro</span><span class="sxs-lookup"><span data-stu-id="0566e-133">Working Folder</span></span>            | <span data-ttu-id="0566e-134">CodePackage</span><span class="sxs-lookup"><span data-stu-id="0566e-134">CodePackage</span></span> |

<span data-ttu-id="0566e-135">Premere **OK**.</span><span class="sxs-lookup"><span data-stu-id="0566e-135">Press **OK**.</span></span>

![Finestra di dialogo Nuovo servizio in Visual Studio][new-service]

<span data-ttu-id="0566e-137">Visual Studio crea il progetto di applicazione e il progetto di servizio Actor e li visualizza in Esplora soluzioni.</span><span class="sxs-lookup"><span data-stu-id="0566e-137">Visual Studio creates the application project and the actor service project and displays them in Solution Explorer.</span></span>

<span data-ttu-id="0566e-138">Il progetto di applicazione (**MyGuestApp**) non contiene direttamente codice,</span><span class="sxs-lookup"><span data-stu-id="0566e-138">The application project (**MyGuestApp**) does not contain any code directly.</span></span> <span data-ttu-id="0566e-139">ma fa riferimento a un set di progetti di servizio.</span><span class="sxs-lookup"><span data-stu-id="0566e-139">Instead, it references a set of service projects.</span></span> <span data-ttu-id="0566e-140">Include inoltre altri tre tipi di contenuto:</span><span class="sxs-lookup"><span data-stu-id="0566e-140">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="0566e-141">**Profili di pubblicazione**</span><span class="sxs-lookup"><span data-stu-id="0566e-141">**Publish profiles**</span></span>  
<span data-ttu-id="0566e-142">Preferenze relative agli strumenti per diversi ambienti.</span><span class="sxs-lookup"><span data-stu-id="0566e-142">Tooling preferences for different environments.</span></span>

* <span data-ttu-id="0566e-143">**Script**</span><span class="sxs-lookup"><span data-stu-id="0566e-143">**Scripts**</span></span>  
<span data-ttu-id="0566e-144">Script di PowerShell per distribuire o aggiornare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0566e-144">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="0566e-145">**Definizione di applicazione**</span><span class="sxs-lookup"><span data-stu-id="0566e-145">**Application definition**</span></span>  
<span data-ttu-id="0566e-146">Include il manifesto dell'applicazione in *ApplicationPackageRoot*.</span><span class="sxs-lookup"><span data-stu-id="0566e-146">Includes the application manifest under *ApplicationPackageRoot*.</span></span> <span data-ttu-id="0566e-147">I file dei parametri dell'applicazione associati sono disponibili in *ApplicationParameters*, definiscono l'applicazione e consentono di configurarla appositamente per un ambiente specifico.</span><span class="sxs-lookup"><span data-stu-id="0566e-147">Associated application parameter files are under *ApplicationParameters*, which define the application and allow you to configure it specifically for a given environment.</span></span>
    
<span data-ttu-id="0566e-148">Per una panoramica del contenuto del progetto di servizio, vedere la [Guida introduttiva a Reliable Services](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="0566e-148">For an overview of the contents of the service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="set-up-networking"></a><span data-ttu-id="0566e-149">Configurare la rete</span><span class="sxs-lookup"><span data-stu-id="0566e-149">Set up networking</span></span>

<span data-ttu-id="0566e-150">L'app Node.js di esempio che viene distribuita usa la porta **80** ed è necessario indicare a Service Fabric che tale porta deve essere esposta.</span><span class="sxs-lookup"><span data-stu-id="0566e-150">The example Node.js app we're deploying uses port **80** and we need to tell Service Fabric that we need that port exposed.</span></span>

<span data-ttu-id="0566e-151">Aprire il file **ServiceManifest.xml** nel progetto.</span><span class="sxs-lookup"><span data-stu-id="0566e-151">Open the **ServiceManifest.xml** file in the project.</span></span> <span data-ttu-id="0566e-152">Nella parte inferiore del manifesto è presente `<Resources> \ <Endpoints>` con una voce già definita.</span><span class="sxs-lookup"><span data-stu-id="0566e-152">At the bottom of the manifest, there is a `<Resources> \ <Endpoints>` with an entry already defined.</span></span> <span data-ttu-id="0566e-153">Modificare la voce aggiungendo `Port`, `Protocol` e `Type`.</span><span class="sxs-lookup"><span data-stu-id="0566e-153">Modify that entry to add `Port`, `Protocol`, and `Type`.</span></span> 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-to-azure"></a><span data-ttu-id="0566e-154">Distribuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="0566e-154">Deploy to Azure</span></span>

<span data-ttu-id="0566e-155">Se si preme **F5** e si esegue il progetto, questo viene distribuito nel cluster locale.</span><span class="sxs-lookup"><span data-stu-id="0566e-155">If you press **F5** and run the project, it is deployed to the local cluster.</span></span> <span data-ttu-id="0566e-156">Si eseguirà invece la distribuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="0566e-156">However, let's deploy to Azure instead.</span></span>

<span data-ttu-id="0566e-157">Fare clic con il pulsante destro del mouse sul progetto e scegliere **Pubblica**. Verrà aperta una finestra di dialogo per la pubblicazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="0566e-157">Right-click on the project and choose **Publish...** which opens a dialog to publish to Azure.</span></span>

![Finestra di dialogo per la pubblicazione in Azure di un servizio di Service Fabric][publish]

<span data-ttu-id="0566e-159">Selezionare il profilo di destinazione **PublishProfiles\Cloud.xml**.</span><span class="sxs-lookup"><span data-stu-id="0566e-159">Select the **PublishProfiles\Cloud.xml** target profile.</span></span>

<span data-ttu-id="0566e-160">Se questa operazione non è stata eseguita in precedenza, scegliere un account Azure in cui effettuare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0566e-160">If you haven't previously, choose an Azure account to deploy to.</span></span> <span data-ttu-id="0566e-161">Se non si ha ancora un account, è possibile [iscriversi per ottenerne uno][create-account].</span><span class="sxs-lookup"><span data-stu-id="0566e-161">If you don't have one yet, [sign-up for one][create-account].</span></span>

<span data-ttu-id="0566e-162">In **Endpoint connessione** selezionare il cluster di Service Fabric in cui eseguire la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0566e-162">Under **Connection Endpoint**, select the Service Fabric cluster to deploy to.</span></span> <span data-ttu-id="0566e-163">Se non se ne ha uno, selezionare **&lt;Crea nuovo cluster&gt;**. Verrà aperta una finestra del Web browser con il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0566e-163">If you do not have one, select **&lt;Create New Cluster...&gt;** which opens up web browser window to the Azure portal.</span></span> <span data-ttu-id="0566e-164">Per altre informazioni, vedere [Creare un cluster nel portale](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="0566e-164">For more information, see [create a cluster in the portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span></span> 

<span data-ttu-id="0566e-165">Quando si crea il cluster di Service Fabric, assicurarsi di impostare **Endpoint personalizzati** su **80**.</span><span class="sxs-lookup"><span data-stu-id="0566e-165">When you create the Service Fabric cluster, make sure to set the **Custom endpoints** setting to **80**.</span></span>

![Configurazione del tipo di nodo di Service Fabric con endpoint personalizzato][custom-endpoint]

<span data-ttu-id="0566e-167">Il completamento della creazione di un nuovo cluster di Service Fabric richiede tempo.</span><span class="sxs-lookup"><span data-stu-id="0566e-167">Creating a new Service Fabric cluster takes some time to complete.</span></span> <span data-ttu-id="0566e-168">Al termine, tornare alla finestra di dialogo di pubblicazione e selezionare **&lt;Aggiorna&gt;**.</span><span class="sxs-lookup"><span data-stu-id="0566e-168">Once it has been created, go back to the publish dialog and select **&lt;Refresh&gt;**.</span></span> <span data-ttu-id="0566e-169">Il nuovo cluster sarà incluso nella casella di riepilogo a discesa. Selezionare il cluster.</span><span class="sxs-lookup"><span data-stu-id="0566e-169">The new cluster is listed in the drop-down box; select it.</span></span>

<span data-ttu-id="0566e-170">Fare clic su **Pubblica** e attendere il completamento della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0566e-170">Press **Publish** and wait for the deployment to finish.</span></span>

<span data-ttu-id="0566e-171">L'operazione potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="0566e-171">This may take a few minutes.</span></span> <span data-ttu-id="0566e-172">Al termine, potrebbero trascorrere ancora alcuni minuti prima che l'applicazione sia completamente disponibile.</span><span class="sxs-lookup"><span data-stu-id="0566e-172">After it completes, it may take a few more minutes for the application to be fully available.</span></span>

## <a name="test-the-website"></a><span data-ttu-id="0566e-173">Testare il sito Web</span><span class="sxs-lookup"><span data-stu-id="0566e-173">Test the website</span></span>

<span data-ttu-id="0566e-174">Dopo che è stato pubblicato, testare il servizio in un Web browser.</span><span class="sxs-lookup"><span data-stu-id="0566e-174">After your service has been published, test it in a web browser.</span></span> 

<span data-ttu-id="0566e-175">Prima di tutto, aprire il portale di Azure e trovare il servizio di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0566e-175">First, open the Azure portal and find your Service Fabric service.</span></span>

<span data-ttu-id="0566e-176">Controllare l'indirizzo del servizio nel pannello di panoramica.</span><span class="sxs-lookup"><span data-stu-id="0566e-176">Check the overview blade of the service address.</span></span> <span data-ttu-id="0566e-177">Usare il nome di dominio della proprietà _Endpoint di connessione client_.</span><span class="sxs-lookup"><span data-stu-id="0566e-177">Use the domain name from the _Client connection endpoint_ property.</span></span> <span data-ttu-id="0566e-178">Ad esempio, `http://mysvcfab1.westus2.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="0566e-178">For example, `http://mysvcfab1.westus2.cloudapp.azure.com`.</span></span>

![Pannello di panoramica di Service Fabric nel portale di Azure][overview]

<span data-ttu-id="0566e-180">Passare a tale indirizzo, in cui verrà visualizzata la risposta `HELLO WORLD`.</span><span class="sxs-lookup"><span data-stu-id="0566e-180">Navigate to this address where you will see the `HELLO WORLD` response.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="0566e-181">Eliminazione del cluster</span><span class="sxs-lookup"><span data-stu-id="0566e-181">Delete the cluster</span></span>

<span data-ttu-id="0566e-182">Non dimenticare di eliminare tutte le risorse create per questa guida introduttiva, perché verranno addebitate.</span><span class="sxs-lookup"><span data-stu-id="0566e-182">Do not forget to delete all of the resources you've created for this quickstart, as you are charged for those resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0566e-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0566e-183">Next steps</span></span>
<span data-ttu-id="0566e-184">Altre informazioni sugli [eseguibili guest](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="0566e-184">Read more about [guest executables](service-fabric-deploy-existing-app.md).</span></span>

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F