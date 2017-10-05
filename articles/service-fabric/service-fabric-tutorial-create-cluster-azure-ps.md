---
title: Creare un cluster di Service Fabric in Azure | Microsoft Docs
description: Informazioni su come creare un cluster di Service Fabric per Windows o Linux in Azure usando PowerShell.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi
ms.openlocfilehash: f62249417552b9cf840bfac3b94c27f63bd7064e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a><span data-ttu-id="8c208-103">Creare un cluster sicuro in Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c208-103">Create a secure cluster on Azure using PowerShell</span></span>
<span data-ttu-id="8c208-104">Questa esercitazione illustra come creare un cluster di Service Fabric (Windows o Linux) in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="8c208-104">This tutorial shows you how to create a Service Fabric cluster (Windows or Linux) running in Azure.</span></span> <span data-ttu-id="8c208-105">Al termine, si ottiene un cluster in esecuzione nel cloud nel quale è possibile distribuire applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8c208-105">When you're finished, you have a cluster running in the cloud that you can deploy applications to.</span></span>

<span data-ttu-id="8c208-106">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="8c208-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8c208-107">Creare un cluster sicuro di Service Fabric in Azure tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c208-107">Create a secure Service Fabric cluster in Azure using PowerShell</span></span>
> * <span data-ttu-id="8c208-108">Proteggere il cluster con un certificato X.509</span><span class="sxs-lookup"><span data-stu-id="8c208-108">Secure the cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="8c208-109">Connessione al cluster mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c208-109">Connect to the cluster using PowerShell</span></span>
> * <span data-ttu-id="8c208-110">Rimuovere un cluster</span><span class="sxs-lookup"><span data-stu-id="8c208-110">Remove a cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c208-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8c208-111">Prerequisites</span></span>
<span data-ttu-id="8c208-112">Prima di iniziare questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="8c208-112">Before you begin this tutorial:</span></span>
- <span data-ttu-id="8c208-113">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="8c208-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="8c208-114">Installare [Service Fabric SDK e il modulo PowerShell](service-fabric-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="8c208-114">Install the [Service Fabric SDK and PowerShell module](service-fabric-get-started.md)</span></span>
- <span data-ttu-id="8c208-115">Installare il [modulo Azure PowerShell 4.1 o versioni successive](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span><span class="sxs-lookup"><span data-stu-id="8c208-115">Install the [Azure Powershell module version 4.1 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span></span>

<span data-ttu-id="8c208-116">La procedura seguente consente di creare un cluster di Service Fabric a nodo singolo, con una sola macchina virtuale,</span><span class="sxs-lookup"><span data-stu-id="8c208-116">The following procedure creates a single-node (single virtual machine) preview Service Fabric cluster.</span></span> <span data-ttu-id="8c208-117">protetto da un certificato autofirmato creato insieme al cluster e posizionato in un insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="8c208-117">The cluster is secured by a self-signed certificate that gets created along with the cluster and then placed in a key vault.</span></span> <span data-ttu-id="8c208-118">I cluster a nodo singolo non possono essere ridimensionati per più di una macchina virtuale e i cluster di anteprima non possono essere aggiornati a versioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="8c208-118">Single-node clusters cannot be scaled beyond one virtual machine and preview clusters cannot be upgraded to newer versions.</span></span>

<span data-ttu-id="8c208-119">Per calcolare i costi sostenuti per l'esecuzione di un cluster di Service Fabric in Azure, usare il [calcolatore dei prezzi di Azure](https://azure.microsoft.com/pricing/calculator/).</span><span class="sxs-lookup"><span data-stu-id="8c208-119">To calculate cost incurred by running a Service Fabric cluster in Azure use the [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/).</span></span>
<span data-ttu-id="8c208-120">Per altre informazioni sulla creazione di cluster di Service Fabric, vedere [Creare un cluster di Service Fabric usando Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="8c208-120">For more information on creating Service Fabric clusters, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="create-the-cluster-using-azure-powershell"></a><span data-ttu-id="8c208-121">Creare il cluster con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c208-121">Create the cluster using Azure PowerShell</span></span>
1. <span data-ttu-id="8c208-122">Scaricare una copia locale del modello di Azure Resource Manager e del file del parametri dal repository GitHub [Azure Resource Manager template for Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) (Modello di Azure Resource Manager per Service Fabric).</span><span class="sxs-lookup"><span data-stu-id="8c208-122">Download a local copy of the Azure Resource Manager template and the parameter file from the [Azure Resource Manager template for Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) GitHub repository.</span></span>  <span data-ttu-id="8c208-123">*azuredeploy.json* è il modello di Azure Resource Manager che definisce un cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8c208-123">*azuredeploy.json* is the Azure Resource Manager template that defines a Service Fabric cluster.</span></span> <span data-ttu-id="8c208-124">*azuredeploy.parameters.json* è il file di parametri per la personalizzazione della distribuzione del cluster.</span><span class="sxs-lookup"><span data-stu-id="8c208-124">*azuredeploy.parameters.json* is a parameters file for you to customize the cluster deployment.</span></span>

2. <span data-ttu-id="8c208-125">Personalizzare i parametri seguenti nel file di parametri *azuredeploy.parameters.json*:</span><span class="sxs-lookup"><span data-stu-id="8c208-125">Customize the following parameters in the *azuredeploy.parameters.json* parameters file:</span></span>

   | <span data-ttu-id="8c208-126">Parametro</span><span class="sxs-lookup"><span data-stu-id="8c208-126">Parameter</span></span>       | <span data-ttu-id="8c208-127">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8c208-127">Description</span></span> | <span data-ttu-id="8c208-128">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="8c208-128">Suggested Value</span></span> |
   | --------------- | ----------- | --------------- |
   | <span data-ttu-id="8c208-129">clusterLocation</span><span class="sxs-lookup"><span data-stu-id="8c208-129">clusterLocation</span></span> | <span data-ttu-id="8c208-130">Area di Azure per la distribuzione del cluster.</span><span class="sxs-lookup"><span data-stu-id="8c208-130">The Azure region to which to deploy the cluster.</span></span> | <span data-ttu-id="8c208-131">*ad esempio westeurope, eastasia, eastus*</span><span class="sxs-lookup"><span data-stu-id="8c208-131">*for example, westeurope, eastasia, eastus*</span></span> |
   | <span data-ttu-id="8c208-132">clusterName</span><span class="sxs-lookup"><span data-stu-id="8c208-132">clusterName</span></span>     | <span data-ttu-id="8c208-133">Nome del cluster che si desidera creare.</span><span class="sxs-lookup"><span data-stu-id="8c208-133">Name of the cluster you want to create.</span></span> | <span data-ttu-id="8c208-134">*ad esempio bobs-sfpreviewcluster*</span><span class="sxs-lookup"><span data-stu-id="8c208-134">*for example, bobs-sfpreviewcluster*</span></span> |
   | <span data-ttu-id="8c208-135">adminUserName</span><span class="sxs-lookup"><span data-stu-id="8c208-135">adminUserName</span></span>   | <span data-ttu-id="8c208-136">Account dell'amministratore locale nelle macchine virtuali del cluster.</span><span class="sxs-lookup"><span data-stu-id="8c208-136">The local admin account on the cluster virtual machines.</span></span> | <span data-ttu-id="8c208-137">*Qualsiasi nome utente di Windows Server valido*</span><span class="sxs-lookup"><span data-stu-id="8c208-137">*Any valid Windows Server username*</span></span> |
   | <span data-ttu-id="8c208-138">adminPassword</span><span class="sxs-lookup"><span data-stu-id="8c208-138">adminPassword</span></span>   | <span data-ttu-id="8c208-139">Password dell'amministratore locale nelle macchine virtuali del cluster.</span><span class="sxs-lookup"><span data-stu-id="8c208-139">Password of the local admin account on the cluster virtual machines.</span></span> | <span data-ttu-id="8c208-140">*Qualsiasi password di Windows Server valido*</span><span class="sxs-lookup"><span data-stu-id="8c208-140">*Any valid Windows Server password*</span></span> |
   | <span data-ttu-id="8c208-141">clusterCodeVersion</span><span class="sxs-lookup"><span data-stu-id="8c208-141">clusterCodeVersion</span></span> | <span data-ttu-id="8c208-142">La versione di Service Fabric da eseguire.</span><span class="sxs-lookup"><span data-stu-id="8c208-142">The Service Fabric version to run.</span></span> <span data-ttu-id="8c208-143">255.255.X.255 sono versioni di anteprima.</span><span class="sxs-lookup"><span data-stu-id="8c208-143">(255.255.X.255 are preview versions).</span></span> | <span data-ttu-id="8c208-144">**255.255.5718.255**</span><span class="sxs-lookup"><span data-stu-id="8c208-144">**255.255.5718.255**</span></span> |
   | <span data-ttu-id="8c208-145">vmInstanceCount</span><span class="sxs-lookup"><span data-stu-id="8c208-145">vmInstanceCount</span></span> | <span data-ttu-id="8c208-146">Il numero di macchine virtuali del cluster, può essere 1 o variare da 3 a 99.</span><span class="sxs-lookup"><span data-stu-id="8c208-146">The number of virtual machines in your cluster (can be 1 or 3-99).</span></span> | <span data-ttu-id="8c208-147">**1**</span><span class="sxs-lookup"><span data-stu-id="8c208-147">**1**</span></span> | <span data-ttu-id="8c208-148">*Per un cluster di anteprima, specificare solo una macchina virtuale*</span><span class="sxs-lookup"><span data-stu-id="8c208-148">*For a preview cluster specify only one virtual machine*</span></span> |

3. <span data-ttu-id="8c208-149">Aprire una console di PowerShell, accedere ad Azure e selezionare la sottoscrizione in cui si vuole distribuire il cluster:</span><span class="sxs-lookup"><span data-stu-id="8c208-149">Open a PowerShell console, login to Azure, and select the subscription you want to deploy the cluster in:</span></span>

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. <span data-ttu-id="8c208-150">Creare e crittografare una password per il certificato che Service Fabric deve usare.</span><span class="sxs-lookup"><span data-stu-id="8c208-150">Create and encrypt a password for the certificate to be used by Service Fabric.</span></span>

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. <span data-ttu-id="8c208-151">Creare il cluster e il relativo certificato eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8c208-151">Create the cluster and its certificate by running the following command:</span></span>

   ```powershell
      New-AzureRmServiceFabricCluster
          -TemplateFile C:\Users\me\Desktop\azuredeploy.json `
          -ParameterFile C:\Users\me\Desktop\azuredeploy.parameters.json `
          -CertificateOutputFolder C:\Users\me\Desktop\ `
          -CertificatePassword $pwd `
          -CertificateSubjectName "mycluster.westeurope.cloudapp.azure.com" `
          -ResourceGroupName myclusterRG
   ```

   >[!NOTE]
   ><span data-ttu-id="8c208-152">Il parametro `-CertificateSubjectName` deve essere allineato al parametro clusterName specificato nel file dei parametri, così come il dominio associato all'area di Azure scelta, ad esempio: `clustername.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="8c208-152">The `-CertificateSubjectName` parameter should align with the clusterName parameter specified in the parameters file, as well as the domain tied to the Azure region you chose, such as: `clustername.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="8c208-153">Al termine della configurazione, vengono generate informazioni relative al cluster creato in Azure.</span><span class="sxs-lookup"><span data-stu-id="8c208-153">Once the configuration finishes, it outputs information about the cluster created in Azure.</span></span> <span data-ttu-id="8c208-154">La configurazione copia anche il certificato del cluster nella directory CertificateOutputFolder nel percorso specificato per questo parametro.</span><span class="sxs-lookup"><span data-stu-id="8c208-154">It also copies the cluster certificate to the -CertificateOutputFolder directory on the path you specified for this parameter.</span></span> <span data-ttu-id="8c208-155">È necessario questo certificato per accedere a Service Fabric Explorer e visualizzare l'integrità del cluster.</span><span class="sxs-lookup"><span data-stu-id="8c208-155">You need this certificate to access Service Fabric Explorer and view the health of your cluster.</span></span>

<span data-ttu-id="8c208-156">Prendere nota dell'URL per il cluster, che potrebbe essere simile al seguente: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span><span class="sxs-lookup"><span data-stu-id="8c208-156">Take note of the URL for your cluster, which may be similar to the following URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span></span>

## <a name="modify-the-certificate--access-service-fabric-explorer"></a><span data-ttu-id="8c208-157">Modificare il certificato e accedere a Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="8c208-157">Modify the certificate & access Service Fabric Explorer</span></span> ##

1. <span data-ttu-id="8c208-158">Fare doppio clic sul certificato per aprire l'Importazione guidata certificati.</span><span class="sxs-lookup"><span data-stu-id="8c208-158">Double-click the certificate to open the Certificate Import Wizard.</span></span>

2. <span data-ttu-id="8c208-159">Usare le impostazioni predefinite, ma assicurarsi di spuntare la casella di testo **Mark this key as exportable.** (Contrassegnare questa chiave come esportabile.)</span><span class="sxs-lookup"><span data-stu-id="8c208-159">Use default settings, but make sure to check the **Mark this key as exportable.**</span></span> <span data-ttu-id="8c208-160">nel passaggio **Protezione della chiave privata**.</span><span class="sxs-lookup"><span data-stu-id="8c208-160">check box, in the **private key protection** step.</span></span> <span data-ttu-id="8c208-161">Visual Studio deve esportare il certificato durante la configurazione del Registro contenitori di Azure per l'autenticazione del cluster di Service Fabric in seguito in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8c208-161">Visual Studio needs to export the certificate when configuring Azure Container Registry to Service Fabric Cluster authentication later in this tutorial.</span></span>

3. <span data-ttu-id="8c208-162">È ora possibile aprire Service Fabric Explorer in un browser.</span><span class="sxs-lookup"><span data-stu-id="8c208-162">You can now open Service Fabric Explorer in a browser.</span></span> <span data-ttu-id="8c208-163">A tale scopo, passare all'URL **ManagementEndpoint** per il cluster tramite un web browser e selezionare il certificato salvato nel computer.</span><span class="sxs-lookup"><span data-stu-id="8c208-163">To do so, navigate to the **ManagementEndpoint** URL for your cluster using a web browser, and select the certificate that was saved on your machine.</span></span>

>[!NOTE]
><span data-ttu-id="8c208-164">Quando si apre Service Fabric Explorer, viene visualizzato un errore di certificato, poiché si usa un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="8c208-164">When opening Service Fabric Explorer, you see a certificate error, as you are using a self-signed certificate.</span></span> <span data-ttu-id="8c208-165">In Edge, è necessario fare clic su *Dettagli* e quindi sul collegamento *Continua per la pagina Web*.</span><span class="sxs-lookup"><span data-stu-id="8c208-165">In Edge, you have to click *Details* and then the *Go on to the webpage* link.</span></span> <span data-ttu-id="8c208-166">In Chrome, è necessario fare clic su *Advanced* (Impostazioni avanzate)e quindi sul collegamento *Procedi*.</span><span class="sxs-lookup"><span data-stu-id="8c208-166">In Chrome, you have to click *Advanced* and then the *proceed* link.</span></span>

>[!NOTE]
><span data-ttu-id="8c208-167">Se la creazione del cluster non riesce, è sempre possibile rieseguire il comando che aggiorna le risorse già distribuite.</span><span class="sxs-lookup"><span data-stu-id="8c208-167">If the cluster creation fails, you can always rerun the command, which updates the resources already deployed.</span></span> <span data-ttu-id="8c208-168">Se un certificato è stato creato come parte della distribuzione non riuscita, ne viene generato uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="8c208-168">If a certificate was created as part of the failed deployment, a new one is generated.</span></span> <span data-ttu-id="8c208-169">Per risolvere i problemi di creazione del cluster, vedere [Creare un cluster di Service Fabric usando Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="8c208-169">To troubleshoot cluster creation, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="connect-to-the-secure-cluster"></a><span data-ttu-id="8c208-170">Connettersi al cluster sicuro</span><span class="sxs-lookup"><span data-stu-id="8c208-170">Connect to the secure cluster</span></span>
<span data-ttu-id="8c208-171">Connettersi al cluster usando il modulo di PowerShell Service Fabric installato con Service Fabric SDK.</span><span class="sxs-lookup"><span data-stu-id="8c208-171">Connect to the cluster using the Service Fabric PowerShell module installed with the Service Fabric SDK.</span></span>  <span data-ttu-id="8c208-172">Installare prima di tutto il certificato nell'archivio personale (My) dell'utente corrente nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="8c208-172">First, install the certificate into the Personal (My) store of the current user on your computer.</span></span>  <span data-ttu-id="8c208-173">Eseguire il seguente comando PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8c208-173">Run the following PowerShell command:</span></span>

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

<span data-ttu-id="8c208-174">È ora possibile connettersi al cluster sicuro.</span><span class="sxs-lookup"><span data-stu-id="8c208-174">You are now ready to connect to your secure cluster.</span></span>

<span data-ttu-id="8c208-175">Il modulo di PowerShell **Service Fabric** include molti cmdlet per la gestione di cluster, applicazioni e servizi di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8c208-175">The **Service Fabric** PowerShell module provides many cmdlets for managing Service Fabric clusters, applications, and services.</span></span>  <span data-ttu-id="8c208-176">Usare il cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) per connettersi al cluster sicuro.</span><span class="sxs-lookup"><span data-stu-id="8c208-176">Use the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet to connect to the secure cluster.</span></span> <span data-ttu-id="8c208-177">L'identificazione personale del certificato e i dettagli dell'endpoint della connessione sono disponibili nell'output di un passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="8c208-177">The certificate thumbprint and connection endpoint details are found in the output from a previous step.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="8c208-178">Verificare di essere connessi e che il cluster sia integro usando il cmdlet [Get ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth).</span><span class="sxs-lookup"><span data-stu-id="8c208-178">Check that you are connected and the cluster is healthy using the [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.</span></span>

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a><span data-ttu-id="8c208-179">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="8c208-179">Clean up resources</span></span>

<span data-ttu-id="8c208-180">Un cluster è costituito da altre risorse di Azure oltre alla risorsa cluster stessa.</span><span class="sxs-lookup"><span data-stu-id="8c208-180">A cluster is made up of other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="8c208-181">Il modo più semplice per eliminare il cluster e tutte le risorse che utilizza consiste nell'eliminare il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="8c208-181">The simplest way to delete the cluster and all the resources it consumes is to delete the resource group.</span></span>

<span data-ttu-id="8c208-182">Accedere ad Azure e selezionare l'ID della sottoscrizione da usare per rimuovere il cluster.</span><span class="sxs-lookup"><span data-stu-id="8c208-182">Log in to Azure and select the subscription ID with which you want to remove the cluster.</span></span>  <span data-ttu-id="8c208-183">È possibile trovare l'ID della sottoscrizione accedendo al [portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8c208-183">You can find your subscription ID by logging in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="8c208-184">Eliminare il gruppo di risorse e tutte le risorse del cluster con il [cmdlet Remove-AzureRmResourceGroup](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="8c208-184">Delete the resource group and all the cluster resources using the [Remove-AzureRMResourceGroup cmdlet](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a><span data-ttu-id="8c208-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8c208-185">Next steps</span></span>
<span data-ttu-id="8c208-186">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="8c208-186">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8c208-187">Creare un cluster di Service Fabric in Azure</span><span class="sxs-lookup"><span data-stu-id="8c208-187">Create a Service Fabric cluster in Azure</span></span>
> * <span data-ttu-id="8c208-188">Proteggere il cluster con un certificato X.509</span><span class="sxs-lookup"><span data-stu-id="8c208-188">Secure the cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="8c208-189">Connessione al cluster mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c208-189">Connect to the cluster using PowerShell</span></span>
> * <span data-ttu-id="8c208-190">Rimuovere un cluster</span><span class="sxs-lookup"><span data-stu-id="8c208-190">Remove a cluster</span></span>

<span data-ttu-id="8c208-191">Procedere con l'esercitazione seguente per scoprire come distribuire un'applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="8c208-191">Next, advance to the following tutorial to learn how to deploy an existing application.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="8c208-192">Distribuire un'app .NET tramite Docker Compose</span><span class="sxs-lookup"><span data-stu-id="8c208-192">Deploy an existing .NET application with Docker Compose</span></span>](service-fabric-host-app-in-a-container.md)
