---
title: aaaHPC 2016 Pack del cluster in Azure | Documenti Microsoft
description: Informazioni su come toodeploy un' 2016 Pack HPC cluster in Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3dde6a68-e4a6-4054-8b67-d6a90fdc5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/15/2016
ms.author: danlep
ms.openlocfilehash: 9e21ec70c822a783474b96da77ce925940279abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a><span data-ttu-id="8c19d-103">Distribuire un cluster HPC Pack 2016 in Azure</span><span class="sxs-lookup"><span data-stu-id="8c19d-103">Deploy an HPC Pack 2016 cluster in Azure</span></span>

<span data-ttu-id="8c19d-104">Seguire i passaggi hello in questo articolo di toodeploy un [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster di macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="8c19d-104">Follow hello steps in this article toodeploy a [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster in Azure virtual machines.</span></span> <span data-ttu-id="8c19d-105">HPC Pack è la soluzione HPC gratuita di Microsoft basata sulle tecnologie di Microsoft Azure e Windows Server e supporta un'ampia gamma di carichi di lavoro di HPC.</span><span class="sxs-lookup"><span data-stu-id="8c19d-105">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies and supports a wide range of HPC workloads.</span></span>

<span data-ttu-id="8c19d-106">Utilizzare uno dei hello [modelli di gestione risorse di Azure](https://github.com/MsHpcPack/HPCPack2016) cluster HPC Pack 2016 hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="8c19d-106">Use one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="8c19d-107">È possibile scegliere tra diverse topologie di cluster con numeri differenti di nodi head del cluster e con nodi di calcolo Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="8c19d-107">You have several choices of cluster topology with different numbers of cluster head nodes, and with either Linux or Windows compute nodes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c19d-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8c19d-108">Prerequisites</span></span>

### <a name="pfx-certificate"></a><span data-ttu-id="8c19d-109">Certificato PFX</span><span class="sxs-lookup"><span data-stu-id="8c19d-109">PFX certificate</span></span>

<span data-ttu-id="8c19d-110">Un cluster di Microsoft HPC Pack 2016 richiede una comunicazione di scambio di informazioni personali (PFX) certificato toosecure hello tra i nodi HPC hello.</span><span class="sxs-lookup"><span data-stu-id="8c19d-110">A Microsoft HPC Pack 2016 cluster requires a Personal Information Exchange (PFX) certificate toosecure hello communication between hello HPC nodes.</span></span> <span data-ttu-id="8c19d-111">certificato Hello deve soddisfare i seguenti requisiti hello:</span><span class="sxs-lookup"><span data-stu-id="8c19d-111">hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="8c19d-112">Deve avere una chiave privata abilitata per lo scambio di chiave</span><span class="sxs-lookup"><span data-stu-id="8c19d-112">It must have a private key capable of key exchange</span></span>
* <span data-ttu-id="8c19d-113">L'uso di chiavi include la firma digitale e la crittografia a chiave</span><span class="sxs-lookup"><span data-stu-id="8c19d-113">Key usage includes Digital Signature and Key Encipherment</span></span>
* <span data-ttu-id="8c19d-114">L'uso di chiavi avanzato include l'autenticazione client e l'autenticazione server</span><span class="sxs-lookup"><span data-stu-id="8c19d-114">Enhanced key usage includes Client Authentication and Server Authentication</span></span>

<span data-ttu-id="8c19d-115">Se si dispone già di un certificato che soddisfa questi requisiti, è possibile richiedere il certificato di hello da un'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="8c19d-115">If you don’t already have a certificate that meets these requirements, you can request hello certificate from a certification authority.</span></span> <span data-ttu-id="8c19d-116">In alternativa, è possibile utilizzare i seguenti comandi toogenerate hello certificato autofirmato basata sul sistema operativo di hello su cui eseguire il comando hello ed esportare un certificato PFX formato hello con chiave privata hello.</span><span class="sxs-lookup"><span data-stu-id="8c19d-116">Alternatively, you can use hello following commands toogenerate hello self-signed certificate based on hello operating system on which you run hello command, and export hello PFX format certificate with private key.</span></span>

* <span data-ttu-id="8c19d-117">**Per Windows 10 o Windows Server 2016**, eseguire hello incorporato **New-SelfSignedCertificate** cmdlet di PowerShell come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="8c19d-117">**For Windows 10 or Windows Server 2016**, run hello built-in **New-SelfSignedCertificate** PowerShell cmdlet as follows:</span></span>

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* <span data-ttu-id="8c19d-118">**Per i sistemi operativi precedenti a Windows 10 o Windows Server 2016**, scaricare hello [generatore certificato autofirmato](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) da hello Microsoft Script Center.</span><span class="sxs-lookup"><span data-stu-id="8c19d-118">**For operating systems earlier than Windows 10 or Windows Server 2016**, download hello [self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from hello Microsoft Script Center.</span></span> <span data-ttu-id="8c19d-119">Estrarre il contenuto ed eseguire hello comandi al prompt di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="8c19d-119">Extract its contents and run hello following commands at a PowerShell prompt:</span></span>

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a><span data-ttu-id="8c19d-120">Carica certificato tooan insieme di credenziali chiave di Azure</span><span class="sxs-lookup"><span data-stu-id="8c19d-120">Upload certificate tooan Azure key vault</span></span>

<span data-ttu-id="8c19d-121">Prima di distribuire un cluster HPC hello, caricare hello certificato tooan [insieme di credenziali chiave Azure](../../key-vault/index.md) come un hello segreto e registrare le seguenti informazioni per l'utilizzo durante la distribuzione di hello: **nome insieme di credenziali**,  **Gruppo di risorse dell'insieme di credenziali**, **URL certificato**, e **identificazione personale del certificato**.</span><span class="sxs-lookup"><span data-stu-id="8c19d-121">Before deploying hello HPC cluster, upload hello certificate tooan [Azure key vault](../../key-vault/index.md) as a secret, and record hello following information for use during hello deployment: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

<span data-ttu-id="8c19d-122">Segue un certificato hello di tooupload script di PowerShell di esempio.</span><span class="sxs-lookup"><span data-stu-id="8c19d-122">A sample PowerShell script tooupload hello certificate follows.</span></span> <span data-ttu-id="8c19d-123">Per ulteriori informazioni sul caricamento di un insieme di credenziali chiave di Azure di tooan certificato, vedere [introduzione insieme credenziali chiavi Azure](../../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8c19d-123">For more information about uploading a certificate tooan Azure key vault, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span></span>

```powershell
#Give hello following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate hello pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode hello JSON object
$pfxContentBytes = Get-Content $PfxFile -Encoding Byte
$pfxContentEncoded = [System.Convert]::ToBase64String($pfxContentBytes)
$jsonObject = @"
{
"data": "$pfxContentEncoded",
"dataType": "pfx",
"password": "$Password"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
#Create an Azure key vault and upload hello certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"hello following Information will be used in hello deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a><span data-ttu-id="8c19d-124">Topologie supportate</span><span class="sxs-lookup"><span data-stu-id="8c19d-124">Supported topologies</span></span>

<span data-ttu-id="8c19d-125">Scegliere una delle hello [modelli di gestione risorse di Azure](https://github.com/MsHpcPack/HPCPack2016) cluster HPC Pack 2016 hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="8c19d-125">Choose one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="8c19d-126">Di seguito vengono indicate le architetture di alto livello di tre topologie di cluster supportate.</span><span class="sxs-lookup"><span data-stu-id="8c19d-126">Following are high-level architectures of three supported cluster topologies.</span></span> <span data-ttu-id="8c19d-127">Le topologie a disponibilità elevata includono più nodi head del cluster.</span><span class="sxs-lookup"><span data-stu-id="8c19d-127">High-availability topologies include multiple cluster head nodes.</span></span>

1. <span data-ttu-id="8c19d-128">Il cluster a disponibilità elevata con dominio di Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c19d-128">High-availability cluster with Active Directory domain</span></span>

    ![Il cluster a disponibilità elevata nel dominio AD](./media/hpcpack-2016-cluster/haad.png)



2. <span data-ttu-id="8c19d-130">Il cluster a disponibilità elevata senza dominio di Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c19d-130">High-availability cluster without Active Directory domain</span></span>

    ![Il cluster a disponibilità elevata senza dominio AD](./media/hpcpack-2016-cluster/hanoad.png)

3. <span data-ttu-id="8c19d-132">Cluster con un singolo nodo head</span><span class="sxs-lookup"><span data-stu-id="8c19d-132">Cluster with a single head node</span></span>

   ![Cluster con nodo head singolo](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a><span data-ttu-id="8c19d-134">Distribuire un cluster</span><span class="sxs-lookup"><span data-stu-id="8c19d-134">Deploy a cluster</span></span>

<span data-ttu-id="8c19d-135">cluster hello toocreate, scegliere un modello e fare clic su **distribuire tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="8c19d-135">toocreate hello cluster, choose a template and click **Deploy tooAzure**.</span></span> <span data-ttu-id="8c19d-136">In hello [portale di Azure](https://portal.azure.com), specificare i parametri per il modello di hello, come descritto in hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="8c19d-136">In hello [Azure portal](https://portal.azure.com), specify parameters for hello template as described in hello following steps.</span></span> <span data-ttu-id="8c19d-137">Ogni modello crea tutte le risorse di Azure necessari per l'infrastruttura di cluster HPC hello.</span><span class="sxs-lookup"><span data-stu-id="8c19d-137">Each template creates all Azure resources required for hello HPC cluster infrastructure.</span></span> <span data-ttu-id="8c19d-138">Le risorse sono: rete virtuale di Azure, indirizzo IP pubblico, bilanciamento del carico (solo per un cluster a disponibilità elevata), interfacce di rete, set di disponibilità, account di archiviazione e macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="8c19d-138">Resources include an Azure virtual network, public IP address, load balancer (only for a high-availability cluster), network interfaces, availability sets, storage accounts, and virtual machines.</span></span>

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a><span data-ttu-id="8c19d-139">Passaggio 1: Selezionare la sottoscrizione hello, il percorso e gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="8c19d-139">Step 1: Select hello subscription, location, and resource group</span></span>

<span data-ttu-id="8c19d-140">Hello **sottoscrizione** hello e **percorso** deve essere specificato quando è stato caricato il certificato PFX stesso (vedere la sezione Prerequisiti).</span><span class="sxs-lookup"><span data-stu-id="8c19d-140">hello **Subscription** and hello **Location** must be same that you specified when you uploaded your PFX certificate (see Prerequisites).</span></span> <span data-ttu-id="8c19d-141">È consigliabile creare un **gruppo di risorse** per la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="8c19d-141">We recommend that you create a **Resource group** for hello deployment.</span></span>

### <a name="step-2-specify-hello-parameter-settings"></a><span data-ttu-id="8c19d-142">Passaggio 2: Specificare le impostazioni dei parametri hello</span><span class="sxs-lookup"><span data-stu-id="8c19d-142">Step 2: Specify hello parameter settings</span></span>

<span data-ttu-id="8c19d-143">Immettere o modificare i valori per parametri modello hello.</span><span class="sxs-lookup"><span data-stu-id="8c19d-143">Enter or modify values for hello template parameters.</span></span> <span data-ttu-id="8c19d-144">Fare clic su parametro successivo tooeach hello icona per le informazioni della Guida.</span><span class="sxs-lookup"><span data-stu-id="8c19d-144">Click hello icon next tooeach parameter for help information.</span></span> <span data-ttu-id="8c19d-145">Vedere anche informazioni aggiuntive hello per [dimensioni delle macchine Virtuali disponibili](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="8c19d-145">Also see hello guidance for [available VM sizes](sizes.md).</span></span>

<span data-ttu-id="8c19d-146">Specificare i valori hello registrato nei prerequisiti hello per hello seguenti parametri: **nome insieme di credenziali**, **gruppo di risorse dell'insieme di credenziali**, **URL certificato**e **Identificazione personale del certificato**.</span><span class="sxs-lookup"><span data-stu-id="8c19d-146">Specify hello values you recorded in hello Prerequisites for hello following parameters: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

### <a name="step-3-review-legal-terms-and-create"></a><span data-ttu-id="8c19d-147">Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="8c19d-147">Step 3.</span></span> <span data-ttu-id="8c19d-148">Rivedere le note legali e creare</span><span class="sxs-lookup"><span data-stu-id="8c19d-148">Review legal terms and create</span></span>
<span data-ttu-id="8c19d-149">Fare clic su **esaminare le note legali** termini hello tooreview.</span><span class="sxs-lookup"><span data-stu-id="8c19d-149">Click **Review legal terms** tooreview hello terms.</span></span> <span data-ttu-id="8c19d-150">Se si accetta, fare clic su **acquisto**, quindi fare clic su **crea** distribuzione hello toostart.</span><span class="sxs-lookup"><span data-stu-id="8c19d-150">If you agree, click **Purchase**, and then click **Create** toostart hello deployment.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="8c19d-151">Connettere il cluster toohello</span><span class="sxs-lookup"><span data-stu-id="8c19d-151">Connect toohello cluster</span></span>
1. <span data-ttu-id="8c19d-152">Dopo la distribuzione di cluster HPC Pack hello, visitare toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8c19d-152">After hello HPC Pack cluster is deployed, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8c19d-153">Fare clic su **gruppi di risorse**e gruppo di risorse hello individuare in quale hello cluster è stato distribuito.</span><span class="sxs-lookup"><span data-stu-id="8c19d-153">Click **Resource groups**, and find hello resource group in which hello cluster was deployed.</span></span> <span data-ttu-id="8c19d-154">È possibile trovare hello macchine virtuali di un nodo head.</span><span class="sxs-lookup"><span data-stu-id="8c19d-154">You can find hello head node virtual machines.</span></span>

    ![Nodi head del cluster nel portale di hello](./media/hpcpack-2016-cluster/clusterhns.png)

2. <span data-ttu-id="8c19d-156">Fare clic su un nodo head (in un cluster a disponibilità elevata, fare clic su uno qualsiasi dei nodi head hello).</span><span class="sxs-lookup"><span data-stu-id="8c19d-156">Click one head node (in a high-availability cluster, click any of hello head nodes).</span></span> <span data-ttu-id="8c19d-157">In **Essentials**, è possibile trovare l'indirizzo IP pubblico hello o nome DNS completo del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="8c19d-157">In **Essentials**, you can find hello public IP address or full DNS name of hello cluster.</span></span>

    ![Impostazioni di connessione del cluster](./media/hpcpack-2016-cluster/clusterconnect.png)

3. <span data-ttu-id="8c19d-159">Fare clic su **Connetti** toolog su tooany dei nodi head di hello tramite Desktop remoto con il nome utente amministratore specificato.</span><span class="sxs-lookup"><span data-stu-id="8c19d-159">Click **Connect** toolog on tooany of hello head nodes using Remote Desktop with your specified administrator user name.</span></span> <span data-ttu-id="8c19d-160">Se il cluster hello è distribuito in un dominio Active Directory, nome utente hello è formato hello <privateDomainName> \<adminUsername > (ad esempio, hpc.local\hpcadmin).</span><span class="sxs-lookup"><span data-stu-id="8c19d-160">If hello cluster you deployed is in an Active Directory Domain, hello user name is of hello form <privateDomainName>\<adminUsername> (for example, hpc.local\hpcadmin).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c19d-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8c19d-161">Next steps</span></span>
* <span data-ttu-id="8c19d-162">Inviare cluster tooyour processi.</span><span class="sxs-lookup"><span data-stu-id="8c19d-162">Submit jobs tooyour cluster.</span></span> <span data-ttu-id="8c19d-163">Vedere [inviare processi tooHPC un cluster HPC Pack in Azure](hpcpack-cluster-submit-jobs.md) e [gestire un cluster HPC Pack 2016 in Azure tramite Azure Active Directory](hpcpack-cluster-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="8c19d-163">See [Submit jobs tooHPC an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md) and [Manage an HPC Pack 2016 cluster in Azure using Azure Active Directory](hpcpack-cluster-active-directory.md).</span></span>

