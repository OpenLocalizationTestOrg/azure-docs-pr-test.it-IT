---
title: aaaCreate un'infrastruttura del servizio cluster in Azure | Documenti Microsoft
description: Informazioni su come toocreate Windows o Linux Service Fabric cluster in Azure utilizzando PowerShell.
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
ms.openlocfilehash: e697e2a2e99f67cb02422efdb368c664c9fd5a97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a><span data-ttu-id="1f6ce-103">Creare un cluster sicuro in Azure con PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f6ce-103">Create a secure cluster on Azure using PowerShell</span></span>
<span data-ttu-id="1f6ce-104">Questa esercitazione viene illustrato come toocreate un'infrastruttura del servizio cluster (Windows o Linux) in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-104">This tutorial shows you how toocreate a Service Fabric cluster (Windows or Linux) running in Azure.</span></span> <span data-ttu-id="1f6ce-105">Al termine, si dispone di un cluster in esecuzione nel cloud hello che è possibile distribuire applicazioni.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-105">When you're finished, you have a cluster running in hello cloud that you can deploy applications to.</span></span>

<span data-ttu-id="1f6ce-106">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="1f6ce-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1f6ce-107">Creare un cluster sicuro di Service Fabric in Azure tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f6ce-107">Create a secure Service Fabric cluster in Azure using PowerShell</span></span>
> * <span data-ttu-id="1f6ce-108">Cluster hello protetta con un certificato x. 509</span><span class="sxs-lookup"><span data-stu-id="1f6ce-108">Secure hello cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="1f6ce-109">Connettere il cluster toohello tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f6ce-109">Connect toohello cluster using PowerShell</span></span>
> * <span data-ttu-id="1f6ce-110">Rimuovere un cluster</span><span class="sxs-lookup"><span data-stu-id="1f6ce-110">Remove a cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f6ce-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1f6ce-111">Prerequisites</span></span>
<span data-ttu-id="1f6ce-112">Prima di iniziare questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="1f6ce-112">Before you begin this tutorial:</span></span>
- <span data-ttu-id="1f6ce-113">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="1f6ce-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="1f6ce-114">Installare hello [modulo di Service Fabric SDK e PowerShell](service-fabric-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="1f6ce-114">Install hello [Service Fabric SDK and PowerShell module](service-fabric-get-started.md)</span></span>
- <span data-ttu-id="1f6ce-115">Installare hello [Azure Powershell versione del modulo 4.1 o versione successiva](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span><span class="sxs-lookup"><span data-stu-id="1f6ce-115">Install hello [Azure Powershell module version 4.1 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span></span>

<span data-ttu-id="1f6ce-116">Hello procedura crea una cluster di Service Fabric di anteprima (singola macchina virtuale) a nodo singolo.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-116">hello following procedure creates a single-node (single virtual machine) preview Service Fabric cluster.</span></span> <span data-ttu-id="1f6ce-117">cluster Hello è protetto da un certificato autofirmato creato insieme a cluster hello viene quindi inserito in un insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-117">hello cluster is secured by a self-signed certificate that gets created along with hello cluster and then placed in a key vault.</span></span> <span data-ttu-id="1f6ce-118">Cluster a nodo singolo non può essere scalato oltre una macchina virtuale e i cluster di anteprima non possono essere aggiornato toonewer versioni.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-118">Single-node clusters cannot be scaled beyond one virtual machine and preview clusters cannot be upgraded toonewer versions.</span></span>

<span data-ttu-id="1f6ce-119">costi toocalculate mediante l'esecuzione di un cluster di Service Fabric in Azure usare hello [calcolatore dei costi Azure](https://azure.microsoft.com/pricing/calculator/).</span><span class="sxs-lookup"><span data-stu-id="1f6ce-119">toocalculate cost incurred by running a Service Fabric cluster in Azure use hello [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/).</span></span>
<span data-ttu-id="1f6ce-120">Per altre informazioni sulla creazione di cluster di Service Fabric, vedere [Creare un cluster di Service Fabric usando Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="1f6ce-120">For more information on creating Service Fabric clusters, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="create-hello-cluster-using-azure-powershell"></a><span data-ttu-id="1f6ce-121">Creare cluster hello tramite Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f6ce-121">Create hello cluster using Azure PowerShell</span></span>
1. <span data-ttu-id="1f6ce-122">Scaricare una copia locale del file di parametro hello e al modello di Azure Resource Manager hello da hello [il modello di gestione risorse di Azure per Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-122">Download a local copy of hello Azure Resource Manager template and hello parameter file from hello [Azure Resource Manager template for Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) GitHub repository.</span></span>  <span data-ttu-id="1f6ce-123">*azuredeploy.JSON* hello Azure Resource Manager modello che definisce un cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-123">*azuredeploy.json* is hello Azure Resource Manager template that defines a Service Fabric cluster.</span></span> <span data-ttu-id="1f6ce-124">*azuredeploy.Parameters.JSON* è un file di parametri per la distribuzione di cluster toocustomize hello.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-124">*azuredeploy.parameters.json* is a parameters file for you toocustomize hello cluster deployment.</span></span>

2. <span data-ttu-id="1f6ce-125">Personalizzare i seguenti parametri in hello hello *azuredeploy.parameters.json* file dei parametri:</span><span class="sxs-lookup"><span data-stu-id="1f6ce-125">Customize hello following parameters in hello *azuredeploy.parameters.json* parameters file:</span></span>

   | <span data-ttu-id="1f6ce-126">.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-126">Parameter</span></span>       | <span data-ttu-id="1f6ce-127">Descrizione</span><span class="sxs-lookup"><span data-stu-id="1f6ce-127">Description</span></span> | <span data-ttu-id="1f6ce-128">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="1f6ce-128">Suggested Value</span></span> |
   | --------------- | ----------- | --------------- |
   | <span data-ttu-id="1f6ce-129">clusterLocation</span><span class="sxs-lookup"><span data-stu-id="1f6ce-129">clusterLocation</span></span> | <span data-ttu-id="1f6ce-130">cluster di hello toodeploy toowhich area Azure Hello.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-130">hello Azure region toowhich toodeploy hello cluster.</span></span> | <span data-ttu-id="1f6ce-131">*ad esempio westeurope, eastasia, eastus*</span><span class="sxs-lookup"><span data-stu-id="1f6ce-131">*for example, westeurope, eastasia, eastus*</span></span> |
   | <span data-ttu-id="1f6ce-132">clusterName</span><span class="sxs-lookup"><span data-stu-id="1f6ce-132">clusterName</span></span>     | <span data-ttu-id="1f6ce-133">Nome del cluster hello desiderato toocreate.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-133">Name of hello cluster you want toocreate.</span></span> | <span data-ttu-id="1f6ce-134">*ad esempio bobs-sfpreviewcluster*</span><span class="sxs-lookup"><span data-stu-id="1f6ce-134">*for example, bobs-sfpreviewcluster*</span></span> |
   | <span data-ttu-id="1f6ce-135">adminUserName</span><span class="sxs-lookup"><span data-stu-id="1f6ce-135">adminUserName</span></span>   | <span data-ttu-id="1f6ce-136">account di amministratore locale Hello in macchine virtuali del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-136">hello local admin account on hello cluster virtual machines.</span></span> | <span data-ttu-id="1f6ce-137">*Qualsiasi nome utente di Windows Server valido*</span><span class="sxs-lookup"><span data-stu-id="1f6ce-137">*Any valid Windows Server username*</span></span> |
   | <span data-ttu-id="1f6ce-138">adminPassword</span><span class="sxs-lookup"><span data-stu-id="1f6ce-138">adminPassword</span></span>   | <span data-ttu-id="1f6ce-139">Password dell'account di amministratore locale hello in macchine virtuali del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-139">Password of hello local admin account on hello cluster virtual machines.</span></span> | <span data-ttu-id="1f6ce-140">*Qualsiasi password di Windows Server valido*</span><span class="sxs-lookup"><span data-stu-id="1f6ce-140">*Any valid Windows Server password*</span></span> |
   | <span data-ttu-id="1f6ce-141">clusterCodeVersion</span><span class="sxs-lookup"><span data-stu-id="1f6ce-141">clusterCodeVersion</span></span> | <span data-ttu-id="1f6ce-142">toorun versione di Service Fabric Hello.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-142">hello Service Fabric version toorun.</span></span> <span data-ttu-id="1f6ce-143">255.255.X.255 sono versioni di anteprima.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-143">(255.255.X.255 are preview versions).</span></span> | <span data-ttu-id="1f6ce-144">**255.255.5718.255**</span><span class="sxs-lookup"><span data-stu-id="1f6ce-144">**255.255.5718.255**</span></span> |
   | <span data-ttu-id="1f6ce-145">vmInstanceCount</span><span class="sxs-lookup"><span data-stu-id="1f6ce-145">vmInstanceCount</span></span> | <span data-ttu-id="1f6ce-146">numero di Hello di macchine virtuali del cluster (può essere 1 o 3-99).</span><span class="sxs-lookup"><span data-stu-id="1f6ce-146">hello number of virtual machines in your cluster (can be 1 or 3-99).</span></span> | <span data-ttu-id="1f6ce-147">**1**</span><span class="sxs-lookup"><span data-stu-id="1f6ce-147">**1**</span></span> | <span data-ttu-id="1f6ce-148">*Per un cluster di anteprima, specificare solo una macchina virtuale*</span><span class="sxs-lookup"><span data-stu-id="1f6ce-148">*For a preview cluster specify only one virtual machine*</span></span> |

3. <span data-ttu-id="1f6ce-149">Aprire una console di PowerShell, account di accesso tooAzure e selezionare una sottoscrizione hello da cluster hello toodeploy in:</span><span class="sxs-lookup"><span data-stu-id="1f6ce-149">Open a PowerShell console, login tooAzure, and select hello subscription you want toodeploy hello cluster in:</span></span>

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. <span data-ttu-id="1f6ce-150">Creare e crittografare una password per hello certificato toobe utilizzata dall'infrastruttura del servizio.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-150">Create and encrypt a password for hello certificate toobe used by Service Fabric.</span></span>

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. <span data-ttu-id="1f6ce-151">Creare il cluster hello e il certificato eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1f6ce-151">Create hello cluster and its certificate by running hello following command:</span></span>

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
   ><span data-ttu-id="1f6ce-152">Hello `-CertificateSubjectName` parametro devono essere allineate con il parametro di clusterName hello specificata nel file dei parametri di hello, nonché come hello dominio associato toohello area di Azure si è scelto, ad esempio: `clustername.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-152">hello `-CertificateSubjectName` parameter should align with hello clusterName parameter specified in hello parameters file, as well as hello domain tied toohello Azure region you chose, such as: `clustername.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="1f6ce-153">Al termine della configurazione di hello, che genera informazioni sui cluster hello creato in Azure.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-153">Once hello configuration finishes, it outputs information about hello cluster created in Azure.</span></span> <span data-ttu-id="1f6ce-154">Copia anche hello cluster certificato toohello - CertificateOutputFolder directory nel percorso di hello che per questo parametro è specificato.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-154">It also copies hello cluster certificate toohello -CertificateOutputFolder directory on hello path you specified for this parameter.</span></span> <span data-ttu-id="1f6ce-155">È necessario questo tooaccess certificato Service Fabric Explorer e visualizzare l'integrità hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-155">You need this certificate tooaccess Service Fabric Explorer and view hello health of your cluster.</span></span>

<span data-ttu-id="1f6ce-156">Prendere nota dell'URL di hello per il cluster, che potrebbe essere simile toohello seguente URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span><span class="sxs-lookup"><span data-stu-id="1f6ce-156">Take note of hello URL for your cluster, which may be similar toohello following URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span></span>

## <a name="modify-hello-certificate--access-service-fabric-explorer"></a><span data-ttu-id="1f6ce-157">Modificare il certificato di hello & accedere Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="1f6ce-157">Modify hello certificate & access Service Fabric Explorer</span></span> ##

1. <span data-ttu-id="1f6ce-158">Fare doppio clic su hello tooopen tramite certificato hello importazione guidata certificati.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-158">Double-click hello certificate tooopen hello Certificate Import Wizard.</span></span>

2. <span data-ttu-id="1f6ce-159">Utilizzare le impostazioni predefinite, ma assicurarsi che toocheck hello **contrassegna questa chiave come esportabile.**</span><span class="sxs-lookup"><span data-stu-id="1f6ce-159">Use default settings, but make sure toocheck hello **Mark this key as exportable.**</span></span> <span data-ttu-id="1f6ce-160">casella di controllo, in hello **protezione della chiave privata** passaggio.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-160">check box, in hello **private key protection** step.</span></span> <span data-ttu-id="1f6ce-161">Visual Studio deve certificato hello tooexport quando si configura l'autenticazione di Azure del Registro di sistema contenitore tooService dell'infrastruttura Cluster più avanti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-161">Visual Studio needs tooexport hello certificate when configuring Azure Container Registry tooService Fabric Cluster authentication later in this tutorial.</span></span>

3. <span data-ttu-id="1f6ce-162">È ora possibile aprire Service Fabric Explorer in un browser.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-162">You can now open Service Fabric Explorer in a browser.</span></span> <span data-ttu-id="1f6ce-163">toodo in tal caso, passare toohello **ManagementEndpoint** URL per il cluster usando un web browser e certificato selezionare hello che è stato salvato nel computer.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-163">toodo so, navigate toohello **ManagementEndpoint** URL for your cluster using a web browser, and select hello certificate that was saved on your machine.</span></span>

>[!NOTE]
><span data-ttu-id="1f6ce-164">Quando si apre Service Fabric Explorer, viene visualizzato un errore di certificato, poiché si usa un certificato autofirmato.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-164">When opening Service Fabric Explorer, you see a certificate error, as you are using a self-signed certificate.</span></span> <span data-ttu-id="1f6ce-165">In Edge, è necessario tooclick *dettagli* e quindi hello *andare nella pagina Web toohello* collegamento.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-165">In Edge, you have tooclick *Details* and then hello *Go on toohello webpage* link.</span></span> <span data-ttu-id="1f6ce-166">In Chrome, è necessario tooclick *avanzate* e quindi hello *procedere* collegamento.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-166">In Chrome, you have tooclick *Advanced* and then hello *proceed* link.</span></span>

>[!NOTE]
><span data-ttu-id="1f6ce-167">Se la creazione del cluster di hello non riesce, è sempre possibile rieseguire comando hello, che aggiorna le risorse di hello già distribuite.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-167">If hello cluster creation fails, you can always rerun hello command, which updates hello resources already deployed.</span></span> <span data-ttu-id="1f6ce-168">Se un certificato è stato creato come parte della distribuzione di hello non è riuscita, viene generato uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-168">If a certificate was created as part of hello failed deployment, a new one is generated.</span></span> <span data-ttu-id="1f6ce-169">creazione del cluster tootroubleshoot, vedere [creare un cluster di Service Fabric usando Gestione risorse di Azure](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="1f6ce-169">tootroubleshoot cluster creation, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="connect-toohello-secure-cluster"></a><span data-ttu-id="1f6ce-170">Connettere il cluster protetto di toohello</span><span class="sxs-lookup"><span data-stu-id="1f6ce-170">Connect toohello secure cluster</span></span>
<span data-ttu-id="1f6ce-171">Connettere il cluster toohello utilizzando il modulo di PowerShell di Service Fabric hello installato con hello Service Fabric SDK.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-171">Connect toohello cluster using hello Service Fabric PowerShell module installed with hello Service Fabric SDK.</span></span>  <span data-ttu-id="1f6ce-172">In primo luogo, è possibile installare il certificato di hello nell'archivio personale (My) hello dell'utente corrente di hello nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-172">First, install hello certificate into hello Personal (My) store of hello current user on your computer.</span></span>  <span data-ttu-id="1f6ce-173">Eseguire il comando PowerShell seguente hello:</span><span class="sxs-lookup"><span data-stu-id="1f6ce-173">Run hello following PowerShell command:</span></span>

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

<span data-ttu-id="1f6ce-174">Si è ora pronto tooconnect tooyour sicura cluster.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-174">You are now ready tooconnect tooyour secure cluster.</span></span>

<span data-ttu-id="1f6ce-175">Hello **Service Fabric** modulo PowerShell fornisce molti cmdlet per la gestione di cluster, applicazioni e servizi di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-175">hello **Service Fabric** PowerShell module provides many cmdlets for managing Service Fabric clusters, applications, and services.</span></span>  <span data-ttu-id="1f6ce-176">Hello utilizzare [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet tooconnect toohello sicura cluster.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-176">Use hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet tooconnect toohello secure cluster.</span></span> <span data-ttu-id="1f6ce-177">Hello identificazione personale del certificato e i dettagli di endpoint di connessione vengono trovati nell'output di hello da un passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-177">hello certificate thumbprint and connection endpoint details are found in hello output from a previous step.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="1f6ce-178">Verificare che si è connessi e hello cluster è integro utilizzando hello [Get ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-178">Check that you are connected and hello cluster is healthy using hello [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.</span></span>

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a><span data-ttu-id="1f6ce-179">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="1f6ce-179">Clean up resources</span></span>

<span data-ttu-id="1f6ce-180">Un cluster è costituito da altre risorse di Azure inoltre toohello risorsa del cluster stesso.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-180">A cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="1f6ce-181">cluster di Hello più semplice modo toodelete hello e tutte le risorse di hello che consuma è gruppo di risorse toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-181">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span>

<span data-ttu-id="1f6ce-182">Accedi tooAzure e selezionare l'ID sottoscrizione hello con cui si desidera che il cluster di hello tooremove.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-182">Log in tooAzure and select hello subscription ID with which you want tooremove hello cluster.</span></span>  <span data-ttu-id="1f6ce-183">È possibile trovare l'ID sottoscrizione effettuando l'accesso toohello [portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1f6ce-183">You can find your subscription ID by logging in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="1f6ce-184">Eliminare il gruppo di risorse hello e tutte le risorse cluster hello utilizzando hello [cmdlet Remove-AzureRMResourceGroup](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="1f6ce-184">Delete hello resource group and all hello cluster resources using hello [Remove-AzureRMResourceGroup cmdlet](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a><span data-ttu-id="1f6ce-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1f6ce-185">Next steps</span></span>
<span data-ttu-id="1f6ce-186">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="1f6ce-186">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1f6ce-187">Creare un cluster di Service Fabric in Azure</span><span class="sxs-lookup"><span data-stu-id="1f6ce-187">Create a Service Fabric cluster in Azure</span></span>
> * <span data-ttu-id="1f6ce-188">Cluster hello protetta con un certificato x. 509</span><span class="sxs-lookup"><span data-stu-id="1f6ce-188">Secure hello cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="1f6ce-189">Connettere il cluster toohello tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f6ce-189">Connect toohello cluster using PowerShell</span></span>
> * <span data-ttu-id="1f6ce-190">Rimuovere un cluster</span><span class="sxs-lookup"><span data-stu-id="1f6ce-190">Remove a cluster</span></span>

<span data-ttu-id="1f6ce-191">Successivamente, spostare toohello successivo dell'esercitazione toolearn come toodeploy un'applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="1f6ce-191">Next, advance toohello following tutorial toolearn how toodeploy an existing application.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="1f6ce-192">Distribuire un'app .NET tramite Docker Compose</span><span class="sxs-lookup"><span data-stu-id="1f6ce-192">Deploy an existing .NET application with Docker Compose</span></span>](service-fabric-host-app-in-a-container.md)
