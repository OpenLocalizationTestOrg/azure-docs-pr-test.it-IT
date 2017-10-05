---
title: Configurazione di un cluster di Service Fabric tramite Visual Studio | Microsoft Docs
description: Descrive come configurare un cluster di Service Fabric usando il modello di Azure Resource Manager creato da un progetto di Gruppo di risorse di Azure in Visual Studio
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: adegeo
editor: 
ms.assetid: bd2c0511-36c9-4828-8dc3-69e4b6a70567
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/21/2017
ms.author: mikhegn
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: c43145b96cdbdfaa7e1893e50d027321fe4c0510
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a><span data-ttu-id="d74b8-103">Configurare un cluster di Service Fabric tramite Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d74b8-103">Set up a Service Fabric cluster by using Visual Studio</span></span>
<span data-ttu-id="d74b8-104">Questo articolo descrive come configurare un cluster di Azure Service Fabric usando Visual Studio e un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d74b8-104">This article describes how to set up an Azure Service Fabric cluster by using Visual Studio and an Azure Resource Manager template.</span></span> <span data-ttu-id="d74b8-105">Per creare il modello, si userà un progetto Gruppo di risorse di Azure di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d74b8-105">We will use a Visual Studio Azure resource group project to create the template.</span></span> <span data-ttu-id="d74b8-106">Dopo aver creato il modello, è possibile distribuirlo direttamente in Azure da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d74b8-106">After the template has been created, it can be deployed directly to Azure from Visual Studio.</span></span> <span data-ttu-id="d74b8-107">Può anche essere usato da uno script o come parte della funzionalità di integrazione continuata (CI).</span><span class="sxs-lookup"><span data-stu-id="d74b8-107">It can also be used from a script, or as part of continuous integration (CI) facility.</span></span>

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a><span data-ttu-id="d74b8-108">Creare un modello di cluster di Service Fabric con un progetto Gruppo di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="d74b8-108">Create a Service Fabric cluster template by using an Azure resource group project</span></span>
<span data-ttu-id="d74b8-109">Per iniziare, aprire Visual Studio e creare un progetto Gruppo di risorse di Azure, disponibile nella cartella **Cloud** :</span><span class="sxs-lookup"><span data-stu-id="d74b8-109">To get started, open Visual Studio and create an Azure resource group project (it is available in the **Cloud** folder):</span></span>

![Finestra di dialogo Nuovo progetto con il progetto Gruppo di risorse di Azure selezionato][1]

<span data-ttu-id="d74b8-111">È possibile creare una nuova soluzione di Visual Studio per il progetto oppure aggiungerlo a una soluzione esistente.</span><span class="sxs-lookup"><span data-stu-id="d74b8-111">You can create a new Visual Studio solution for this project or add it to an existing solution.</span></span>

> [!NOTE]
> <span data-ttu-id="d74b8-112">Se il progetto Gruppo di risorse di Azure non è visibile nel nodo Cloud, significa che Azure SDK non è installato.</span><span class="sxs-lookup"><span data-stu-id="d74b8-112">If you do not see the Azure resource group project under the Cloud node, you do not have the Azure SDK installed.</span></span> <span data-ttu-id="d74b8-113">Avviare Installazione guidata piattaforma Web ([eseguire ora l'installazione](http://www.microsoft.com/web/downloads/platform.aspx) , se necessario), quindi cercare "Azure SDK per .NET" e installare la versione compatibile con la versione di Visual Studio in uso.</span><span class="sxs-lookup"><span data-stu-id="d74b8-113">Launch Web Platform Installer ([install it now](http://www.microsoft.com/web/downloads/platform.aspx) if you have not already), and then search for "Azure SDK for .NET" and install the version that is compatible with your version of Visual Studio.</span></span>
> 
> 

<span data-ttu-id="d74b8-114">Dopo aver premuto il pulsante OK, Visual Studio chiederà di selezionare il modello di Gestione risorse da creare:</span><span class="sxs-lookup"><span data-stu-id="d74b8-114">After you hit the OK button, Visual Studio will ask you to select the Resource Manager template you want to create:</span></span>

![Finestra di dialogo Seleziona modello di Azure con il modello Service Fabric Cluster selezionato][2]

<span data-ttu-id="d74b8-116">Selezionare il modello "Service Fabric Cluster" e premere nuovamente il pulsante OK.</span><span class="sxs-lookup"><span data-stu-id="d74b8-116">Select the Service Fabric Cluster template and hit the OK button again.</span></span> <span data-ttu-id="d74b8-117">In questo modo, sono stati creati il progetto e il modello di Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="d74b8-117">The project and the Resource Manager template have now been created.</span></span>

## <a name="prepare-the-template-for-deployment"></a><span data-ttu-id="d74b8-118">Preparare il modello per la distribuzione</span><span class="sxs-lookup"><span data-stu-id="d74b8-118">Prepare the template for deployment</span></span>
<span data-ttu-id="d74b8-119">Prima di distribuire il modello per la creazione del cluster, è necessario specificare i valori per i parametri obbligatori del modello.</span><span class="sxs-lookup"><span data-stu-id="d74b8-119">Before the template is deployed to create the cluster, you must provide values for the required template parameters.</span></span> <span data-ttu-id="d74b8-120">Questi valori dei parametri vengono letti dal file `ServiceFabricCluster.parameters.json` che si trova nella cartella `Templates` del progetto del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="d74b8-120">These parameter values are read from the `ServiceFabricCluster.parameters.json` file, which is in the `Templates` folder of the resource group project.</span></span> <span data-ttu-id="d74b8-121">Aprire il file e specificare i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="d74b8-121">Open the file and provide the following values:</span></span>

| <span data-ttu-id="d74b8-122">Nome parametro</span><span class="sxs-lookup"><span data-stu-id="d74b8-122">Parameter name</span></span> | <span data-ttu-id="d74b8-123">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d74b8-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d74b8-124">adminUserName</span><span class="sxs-lookup"><span data-stu-id="d74b8-124">adminUserName</span></span> |<span data-ttu-id="d74b8-125">Nome dell'account amministratore per le macchine (nodi) di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d74b8-125">The name of the administrator account for Service Fabric machines (nodes).</span></span> |
| <span data-ttu-id="d74b8-126">certificateThumbprint</span><span class="sxs-lookup"><span data-stu-id="d74b8-126">certificateThumbprint</span></span> |<span data-ttu-id="d74b8-127">Identificazione personale del certificato che garantisce la sicurezza del cluster.</span><span class="sxs-lookup"><span data-stu-id="d74b8-127">The thumbprint of the certificate that secures the cluster.</span></span> |
| <span data-ttu-id="d74b8-128">sourceVaultResourceId</span><span class="sxs-lookup"><span data-stu-id="d74b8-128">sourceVaultResourceId</span></span> |<span data-ttu-id="d74b8-129">*ID risorsa* dell'insieme di credenziali delle chiavi in cui viene memorizzato il certificato che garantisce la sicurezza del cluster.</span><span class="sxs-lookup"><span data-stu-id="d74b8-129">The *resource ID* of the key vault where the certificate that secures the cluster is stored.</span></span> |
| <span data-ttu-id="d74b8-130">certificateUrlValue</span><span class="sxs-lookup"><span data-stu-id="d74b8-130">certificateUrlValue</span></span> |<span data-ttu-id="d74b8-131">URL del certificato di protezione del cluster.</span><span class="sxs-lookup"><span data-stu-id="d74b8-131">The URL of the cluster security certificate.</span></span> |

<span data-ttu-id="d74b8-132">Il modello di Gestione risorse di Service Fabric in Visual Studio crea un cluster sicuro, protetto da un certificato,</span><span class="sxs-lookup"><span data-stu-id="d74b8-132">The Visual Studio Service Fabric Resource Manager template creates a secure cluster that is protected by a certificate.</span></span> <span data-ttu-id="d74b8-133">identificato dagli ultimi tre parametri del modello (`certificateThumbprint`, `sourceVaultValue` e `certificateUrlValue`) e incluso in un **insieme di credenziali delle chiavi di Azure**.</span><span class="sxs-lookup"><span data-stu-id="d74b8-133">This certificate is identified by the last three template parameters (`certificateThumbprint`, `sourceVaultValue`, and `certificateUrlValue`), and it must exist in an **Azure Key Vault**.</span></span> <span data-ttu-id="d74b8-134">Per altre informazioni su come creare il certificato di sicurezza del cluster, vedere l'articolo [Scenari di sicurezza di un cluster di Service Fabric](service-fabric-cluster-security.md#x509-certificates-and-service-fabric).</span><span class="sxs-lookup"><span data-stu-id="d74b8-134">For more information on how to create the cluster security certificate, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) article.</span></span>

## <a name="optional-change-the-cluster-name"></a><span data-ttu-id="d74b8-135">Facoltativo: modificare il nome del cluster</span><span class="sxs-lookup"><span data-stu-id="d74b8-135">Optional: change the cluster name</span></span>
<span data-ttu-id="d74b8-136">Ogni cluster di Service Fabric ha un nome.</span><span class="sxs-lookup"><span data-stu-id="d74b8-136">Every Service Fabric cluster has a name.</span></span> <span data-ttu-id="d74b8-137">Quando viene creato un cluster di Fabric in Azure, il nome del cluster insieme all'area di Azure determina il nome DNS (Domain Name System) del cluster.</span><span class="sxs-lookup"><span data-stu-id="d74b8-137">When a Fabric cluster is created in Azure, cluster name determines (together with the Azure region) the Domain Name System (DNS) name for the cluster.</span></span> <span data-ttu-id="d74b8-138">Ad esempio, se il cluster viene denominato `myBigCluster` e il percorso (area di Azure) del gruppo di risorse che ospiterà il nuovo cluster è Stati Uniti orientali, il nome DNS del cluster sarà `myBigCluster.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="d74b8-138">For example, if you name your cluster `myBigCluster`, and the location (Azure region) of the resource group that will host the new cluster is East US, the DNS name of the cluster will be `myBigCluster.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="d74b8-139">Per impostazione predefinita il nome del cluster viene generato automaticamente in modo univoco aggiungendo un suffisso casuale al prefisso "cluster".</span><span class="sxs-lookup"><span data-stu-id="d74b8-139">By default the cluster name is generated automatically and made unique by attaching a random suffix to a "cluster" prefix.</span></span> <span data-ttu-id="d74b8-140">Questo metodo semplifica l'uso del modello nell'ambito di un sistema a **integrazione continua** .</span><span class="sxs-lookup"><span data-stu-id="d74b8-140">This makes it very easy to use the template as part of a **continuous integration** (CI) system.</span></span> <span data-ttu-id="d74b8-141">Se si vuole usare un nome specifico per il cluster con un particolare significato, impostare il valore della variabile `clusterName` nel file di modello di Resource Manager (`ServiceFabricCluster.json`) sul nome scelto.</span><span class="sxs-lookup"><span data-stu-id="d74b8-141">If you want to use a specific name for your cluster, one that is meaningful to you, set the value of the `clusterName` variable in the Resource Manager template file (`ServiceFabricCluster.json`) to your chosen name.</span></span> <span data-ttu-id="d74b8-142">Si tratta della prima variabile definita nel file.</span><span class="sxs-lookup"><span data-stu-id="d74b8-142">It is the first variable defined in that file.</span></span>

## <a name="optional-add-public-application-ports"></a><span data-ttu-id="d74b8-143">Facoltativo: aggiungere le porte pubbliche dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="d74b8-143">Optional: add public application ports</span></span>
<span data-ttu-id="d74b8-144">Prima di distribuire il cluster, è possibile anche modificare le porte pubbliche delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="d74b8-144">You may also want to change the public application ports for the cluster before you deploy it.</span></span> <span data-ttu-id="d74b8-145">Per impostazione predefinita, il modello apre solo due porte TCP pubbliche: 80 e 8081.</span><span class="sxs-lookup"><span data-stu-id="d74b8-145">By default, the template opens up just two public TCP ports (80 and 8081).</span></span> <span data-ttu-id="d74b8-146">Se per le applicazioni sono necessarie più porte, modificare la definizione del servizio di bilanciamento del carico di Azure nel modello.</span><span class="sxs-lookup"><span data-stu-id="d74b8-146">If you need more for your applications, modify the Azure Load Balancer definition in the template.</span></span> <span data-ttu-id="d74b8-147">La definizione viene archiviata nel file del modello principale (`ServiceFabricCluster.json`).</span><span class="sxs-lookup"><span data-stu-id="d74b8-147">The definition is stored in the main template file (`ServiceFabricCluster.json`).</span></span> <span data-ttu-id="d74b8-148">Aprire il file e cercare `loadBalancedAppPort`.</span><span class="sxs-lookup"><span data-stu-id="d74b8-148">Open that file and search for `loadBalancedAppPort`.</span></span> <span data-ttu-id="d74b8-149">Ogni porta è associata a tre elementi:</span><span class="sxs-lookup"><span data-stu-id="d74b8-149">Each port is associated with three artifacts:</span></span>

1. <span data-ttu-id="d74b8-150">Una variabile del modello che definisce il valore della porta TCP per la porta:</span><span class="sxs-lookup"><span data-stu-id="d74b8-150">A template variable that defines the TCP port value for the port:</span></span>
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. <span data-ttu-id="d74b8-151">Un *probe* che definisce la frequenza e per quanto tempo il servizio di bilanciamento del carico di Azure tenta di usare un nodo specifico dell'infrastruttura di servizi prima del failover a un altro nodo.</span><span class="sxs-lookup"><span data-stu-id="d74b8-151">A *probe* that defines how frequently and for how long the Azure load balancer attempts to use a specific Service Fabric node before failing over to another one.</span></span> <span data-ttu-id="d74b8-152">I probe fanno parte della risorsa del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="d74b8-152">The probes are part of the Load Balancer resource.</span></span> <span data-ttu-id="d74b8-153">Segue la definizione di probe per la prima porta dell'applicazione predefinita:</span><span class="sxs-lookup"><span data-stu-id="d74b8-153">Here is the probe definition for the first default application port:</span></span>
   
    ```json
    {
        "name": "AppPortProbe1",
        "properties": {
            "intervalInSeconds": 5,
            "numberOfProbes": 2,
            "port": "[variables('loadBalancedAppPort1')]",
            "protocol": "Tcp"
        }
    }
    ```
3. <span data-ttu-id="d74b8-154">Una *regola di bilanciamento del carico* che collega la porta e il probe e che consente il bilanciamento del carico in un set di nodi del cluster di Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="d74b8-154">A *load-balancing rule* that ties together the port and the probe, which enables load balancing across a set of Service Fabric cluster nodes:</span></span>
   
    ```json
    {
        "name": "AppPortLBRule1",
        "properties": {
            "backendAddressPool": {
                "id": "[variables('lbPoolID0')]"
            },
            "backendPort": "[variables('loadBalancedAppPort1')]",
            "enableFloatingIP": false,
            "frontendIPConfiguration": {
                "id": "[variables('lbIPConfig0')]"
            },
            "frontendPort": "[variables('loadBalancedAppPort1')]",
            "idleTimeoutInMinutes": 5,
            "probe": {
                "id": "[concat(variables('lbID0'),'/probes/AppPortProbe1')]"
            },
            "protocol": "Tcp"
        }
    }
    ```
   <span data-ttu-id="d74b8-155">Se le applicazioni che si intende distribuire nel cluster richiedono più porte, è possibile aggiungerle mediante la creazione di definizioni aggiuntive delle regole di bilanciamento del carico e di probe.</span><span class="sxs-lookup"><span data-stu-id="d74b8-155">If the applications that you plan to deploy to the cluster need more ports, you can add them by creating additional probe and load-balancing rule definitions.</span></span> <span data-ttu-id="d74b8-156">Per altre informazioni su come usare Azure Load Balancer con i modelli di Resource Manager, vedere [Introduzione alla creazione di un servizio di bilanciamento del carico interno tramite un modello](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="d74b8-156">For more information on how to work with Azure Load Balancer through Resource Manager templates, see [Get started creating an internal load balancer using a template](../load-balancer/load-balancer-get-started-ilb-arm-template.md).</span></span>

## <a name="deploy-the-template-by-using-visual-studio"></a><span data-ttu-id="d74b8-157">Distribuire il modello tramite Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d74b8-157">Deploy the template by using Visual Studio</span></span>
<span data-ttu-id="d74b8-158">Dopo aver salvato tutti i valori di parametro obbligatori nel file`ServiceFabricCluster.param.dev.json` , è possibile distribuire il modello e creare il cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d74b8-158">After you have saved all the required parameter values in the`ServiceFabricCluster.param.dev.json` file, you are ready to deploy the template and create your Service Fabric cluster.</span></span> <span data-ttu-id="d74b8-159">Fare clic con il pulsante destro del mouse sul progetto Gruppo di risorse in Esplora soluzioni di Visual Studio e scegliere **Distribuisci | Nuova distribuzione...**.</span><span class="sxs-lookup"><span data-stu-id="d74b8-159">Right-click the resource group project in Visual Studio Solution Explorer and choose **Deploy | New Deployment...**.</span></span> <span data-ttu-id="d74b8-160">Se necessario, verrà visualizzata la finestra di dialogo **Distribuisci in gruppo di risorse** che richiede l'autenticazione ad Azure:</span><span class="sxs-lookup"><span data-stu-id="d74b8-160">If necessary, Visual Studio will show the **Deploy to Resource Group** dialog box, asking you to authenticate to Azure:</span></span>

![Finestra di dialogo Distribuisci a Gruppo di risorse][3]

<span data-ttu-id="d74b8-162">La finestra di dialogo consente di scegliere se selezionare per il cluster un gruppo di risorse esistente oppure crearne uno nuovo in Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="d74b8-162">The dialog box lets you choose an existing Resource Manager resource group for the cluster and gives you the option to create a new one.</span></span> <span data-ttu-id="d74b8-163">In genere, è opportuno usare un gruppo di risorse distinto per un cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d74b8-163">It normally makes sense to use a separate resource group for a Service Fabric cluster.</span></span>

<span data-ttu-id="d74b8-164">Dopo aver premuto il pulsante Distribuisci, Visual Studio chiederà di confermare i valori di parametro del modello.</span><span class="sxs-lookup"><span data-stu-id="d74b8-164">After you hit the Deploy button, Visual Studio will prompt you to confirm the template parameter values.</span></span> <span data-ttu-id="d74b8-165">Premere il pulsante **Salva** .</span><span class="sxs-lookup"><span data-stu-id="d74b8-165">Hit the **Save** button.</span></span> <span data-ttu-id="d74b8-166">Uno dei parametri, tuttavia, non ha un valore persistente: la password dell'account amministrativo per il cluster.</span><span class="sxs-lookup"><span data-stu-id="d74b8-166">One parameter does not have a persisted value: the administrative account password for the cluster.</span></span> <span data-ttu-id="d74b8-167">È necessario specificare un valore di password ogni volta che Visual Studio lo richiede.</span><span class="sxs-lookup"><span data-stu-id="d74b8-167">You need to provide a password value when Visual Studio prompts you for one.</span></span>

> [!NOTE]
> <span data-ttu-id="d74b8-168">A partire da Azure SDK 2.9, Visual Studio supporta la lettura password dall'**insieme di credenziali delle chiavi di Azure** durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d74b8-168">Starting with Azure SDK 2.9, Visual Studio supports reading passwords from **Azure Key Vault** during deployment.</span></span> <span data-ttu-id="d74b8-169">Nella finestra di dialogo dei parametri modello la casella di testo del parametro `adminPassword` ha una piccola icona a forma di chiave sulla destra.</span><span class="sxs-lookup"><span data-stu-id="d74b8-169">In the template parameters dialog notice that the `adminPassword` parameter text box has a little "key" icon on the right.</span></span> <span data-ttu-id="d74b8-170">Questa icona consente di selezionare un segreto dell'insieme di credenziali delle chiavi come password amministrativa per il cluster.</span><span class="sxs-lookup"><span data-stu-id="d74b8-170">This icon allows you to select an existing key vault secret as the administrative password for the cluster.</span></span> <span data-ttu-id="d74b8-171">Assicurarsi di abilitare prima l'accesso di Azure Resource Manager per la distribuzione dei modelli nei criteri di accesso avanzato dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="d74b8-171">Just make sure to first enable Azure Resource Manager access for template deployment in the Advanced Access Policies of your key vault.</span></span> 
> 
> 

<span data-ttu-id="d74b8-172">È possibile monitorare lo stato di avanzamento del processo di distribuzione nella finestra di output di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d74b8-172">You can monitor the progress of the deployment process in the Visual Studio output window.</span></span> <span data-ttu-id="d74b8-173">Al termine della distribuzione del modello, è possibile usare il nuovo cluster.</span><span class="sxs-lookup"><span data-stu-id="d74b8-173">Once the template deployment is completed, your new cluster is ready to use!</span></span>

> [!NOTE]
> <span data-ttu-id="d74b8-174">Se PowerShell non è mai stato usato per amministrare Azure dal computer in uso, è necessario eseguire alcune attività di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="d74b8-174">If PowerShell was never used to administer Azure from the machine that you are using now, you need to do a little housekeeping.</span></span>
> 
> 1. <span data-ttu-id="d74b8-175">Abilitare gli script di PowerShell eseguendo il comando [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) .</span><span class="sxs-lookup"><span data-stu-id="d74b8-175">Enable PowerShell scripting by running the [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) command.</span></span> <span data-ttu-id="d74b8-176">Per i computer di sviluppo, i criteri "Unrestricted" sono in genere accettabili.</span><span class="sxs-lookup"><span data-stu-id="d74b8-176">For development machines, "unrestricted" policy is usually acceptable.</span></span>
> 2. <span data-ttu-id="d74b8-177">Decidere se consentire la raccolta dei dati di diagnostica dai comandi di Azure PowerShell ed eseguire [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) o [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx), in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="d74b8-177">Decide whether to allow diagnostic data collection from Azure PowerShell commands, and run [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) or [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx) as necessary.</span></span> <span data-ttu-id="d74b8-178">In questo modo, si eviteranno richieste non necessarie durante la distribuzione del modello.</span><span class="sxs-lookup"><span data-stu-id="d74b8-178">This will avoid unnecessary prompts during template deployment.</span></span>
> 
> 

<span data-ttu-id="d74b8-179">Se sono presenti errori, passare al [portale di Azure](https://portal.azure.com/) e aprire il gruppo di risorse in cui è stata eseguita la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d74b8-179">If there are any errors, go to the [Azure portal](https://portal.azure.com/) and open the resource group that you deployed to.</span></span> <span data-ttu-id="d74b8-180">Fare clic su **Tutte le impostazioni**, quindi fare clic su **Distribuzioni** nel pannello Impostazioni.</span><span class="sxs-lookup"><span data-stu-id="d74b8-180">Click **All settings**, then click **Deployments** on the settings blade.</span></span> <span data-ttu-id="d74b8-181">Nel caso in cui la distribuzione del gruppo di risorse non sia riuscita, in questa sezione saranno presenti informazioni di diagnostica dettagliate.</span><span class="sxs-lookup"><span data-stu-id="d74b8-181">A failed resource-group deployment leaves detailed diagnostic information there.</span></span>

> [!NOTE]
> <span data-ttu-id="d74b8-182">I cluster di Service Fabric richiedono che sia attivo un certo numero di nodi allo scopo di mantenere la disponibilità e lo stato, ossia per "mantenere il quorum".</span><span class="sxs-lookup"><span data-stu-id="d74b8-182">Service Fabric clusters require a certain number of nodes to be up to maintain availability and preserve state - referred to as "maintaining quorum."</span></span> <span data-ttu-id="d74b8-183">Di conseguenza, non è sicuro arrestare tutti i computer del cluster se prima non è stato eseguito un [backup completo dello stato](service-fabric-reliable-services-backup-restore.md).</span><span class="sxs-lookup"><span data-stu-id="d74b8-183">Therefore, it is not safe to shut down all of the machines in the cluster unless you have first performed a [full backup of your state](service-fabric-reliable-services-backup-restore.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d74b8-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d74b8-184">Next steps</span></span>
* [<span data-ttu-id="d74b8-185">Informazioni sulla configurazione di cluster di Service Fabric dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d74b8-185">Learn about setting up Service Fabric cluster using the Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="d74b8-186">Informazioni sulla gestione e la distribuzione di applicazioni di Service Fabric mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d74b8-186">Learn how to manage and deploy Service Fabric applications using Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
