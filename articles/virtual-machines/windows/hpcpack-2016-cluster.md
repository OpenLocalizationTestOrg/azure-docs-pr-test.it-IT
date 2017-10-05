---
title: Cluster HPC Pack 2016 in Azure | Microsoft Docs
description: Informazioni su come distribuire un cluster HPC Pack 2016 in Azure
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
ms.openlocfilehash: 88d1f4e29f38ba1a6bef57c2da43bee205575eee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a><span data-ttu-id="48111-103">Distribuire un cluster HPC Pack 2016 in Azure</span><span class="sxs-lookup"><span data-stu-id="48111-103">Deploy an HPC Pack 2016 cluster in Azure</span></span>

<span data-ttu-id="48111-104">Seguire i passaggi descritti in questo articolo per distribuire un cluster [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) nelle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="48111-104">Follow the steps in this article to deploy a [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster in Azure virtual machines.</span></span> <span data-ttu-id="48111-105">HPC Pack è la soluzione HPC gratuita di Microsoft basata sulle tecnologie di Microsoft Azure e Windows Server e supporta un'ampia gamma di carichi di lavoro di HPC.</span><span class="sxs-lookup"><span data-stu-id="48111-105">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies and supports a wide range of HPC workloads.</span></span>

<span data-ttu-id="48111-106">Usare uno dei [modelli di Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) per distribuire il cluster HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="48111-106">Use one of the [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) to deploy the HPC Pack 2016 cluster.</span></span> <span data-ttu-id="48111-107">È possibile scegliere tra diverse topologie di cluster con numeri differenti di nodi head del cluster e con nodi di calcolo Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="48111-107">You have several choices of cluster topology with different numbers of cluster head nodes, and with either Linux or Windows compute nodes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48111-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="48111-108">Prerequisites</span></span>

### <a name="pfx-certificate"></a><span data-ttu-id="48111-109">Certificato PFX</span><span class="sxs-lookup"><span data-stu-id="48111-109">PFX certificate</span></span>

<span data-ttu-id="48111-110">Un cluster Microsoft HPC Pack 2016 richiede un certificato PFX (scambio di informazioni personali) per rendere sicura la comunicazione tra i nodi HPC.</span><span class="sxs-lookup"><span data-stu-id="48111-110">A Microsoft HPC Pack 2016 cluster requires a Personal Information Exchange (PFX) certificate to secure the communication between the HPC nodes.</span></span> <span data-ttu-id="48111-111">Il certificato deve soddisfare i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="48111-111">The certificate must meet the following requirements:</span></span>

* <span data-ttu-id="48111-112">Deve avere una chiave privata abilitata per lo scambio di chiave</span><span class="sxs-lookup"><span data-stu-id="48111-112">It must have a private key capable of key exchange</span></span>
* <span data-ttu-id="48111-113">L'uso di chiavi include la firma digitale e la crittografia a chiave</span><span class="sxs-lookup"><span data-stu-id="48111-113">Key usage includes Digital Signature and Key Encipherment</span></span>
* <span data-ttu-id="48111-114">L'uso di chiavi avanzato include l'autenticazione client e l'autenticazione server</span><span class="sxs-lookup"><span data-stu-id="48111-114">Enhanced key usage includes Client Authentication and Server Authentication</span></span>

<span data-ttu-id="48111-115">Se si dispone già di un certificato che soddisfa questi requisiti, è possibile richiedere il certificato a un'autorità di certificazione.</span><span class="sxs-lookup"><span data-stu-id="48111-115">If you don’t already have a certificate that meets these requirements, you can request the certificate from a certification authority.</span></span> <span data-ttu-id="48111-116">In alternativa, è possibile utilizzare i comandi seguenti per generare i certificati autofirmati in base al sistema operativo in cui si esegue il comando ed esportare il certificato di formato PFX con la chiave privata.</span><span class="sxs-lookup"><span data-stu-id="48111-116">Alternatively, you can use the following commands to generate the self-signed certificate based on the operating system on which you run the command, and export the PFX format certificate with private key.</span></span>

* <span data-ttu-id="48111-117">**Per Windows 10 o Windows Server 2016**, eseguire il cmdlet integrato di PowerShell **SelfSignedCertificate New** nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="48111-117">**For Windows 10 or Windows Server 2016**, run the built-in **New-SelfSignedCertificate** PowerShell cmdlet as follows:</span></span>

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* <span data-ttu-id="48111-118">**Per i sistemi operativi meno recenti di Windows 10 o Windows Server 2016**, scaricare il [generatore di certificati autofirmati](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) da Microsoft Script Center.</span><span class="sxs-lookup"><span data-stu-id="48111-118">**For operating systems earlier than Windows 10 or Windows Server 2016**, download the [self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from the Microsoft Script Center.</span></span> <span data-ttu-id="48111-119">Estrarne il contenuto ed eseguire i comandi seguenti al prompt dei comandi di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="48111-119">Extract its contents and run the following commands at a PowerShell prompt:</span></span>

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-to-an-azure-key-vault"></a><span data-ttu-id="48111-120">Caricare il certificato nell'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="48111-120">Upload certificate to an Azure key vault</span></span>

<span data-ttu-id="48111-121">Prima di distribuire il cluster HPC, caricare il certificato in un [insieme di credenziali delle chiavi di Azure](../../key-vault/index.md) come segreto e registrare le informazioni seguenti per l'uso durante la distribuzione: **Nome dell'insieme di credenziali**, **Gruppo di risorse dell'insieme di credenziali**, **URL certificato** e **identificazione personale certificato**.</span><span class="sxs-lookup"><span data-stu-id="48111-121">Before deploying the HPC cluster, upload the certificate to an [Azure key vault](../../key-vault/index.md) as a secret, and record the following information for use during the deployment: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

<span data-ttu-id="48111-122">Di seguito viene presentato un esempio di script di PowerShell per caricare il certificato.</span><span class="sxs-lookup"><span data-stu-id="48111-122">A sample PowerShell script to upload the certificate follows.</span></span> <span data-ttu-id="48111-123">Per altre informazioni sul caricamento di un certificato in un insieme di credenziali delle chiavi di Azure, vedere [Introduzione all'insieme di credenziali delle chiavi di Azure](../../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="48111-123">For more information about uploading a certificate to an Azure key vault, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span></span>

```powershell
#Give the following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate the pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode the JSON object
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
#Create an Azure key vault and upload the certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"The following Information will be used in the deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a><span data-ttu-id="48111-124">Topologie supportate</span><span class="sxs-lookup"><span data-stu-id="48111-124">Supported topologies</span></span>

<span data-ttu-id="48111-125">Scegliere uno dei [modelli di Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) per distribuire il cluster HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="48111-125">Choose one of the [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) to deploy the HPC Pack 2016 cluster.</span></span> <span data-ttu-id="48111-126">Di seguito vengono indicate le architetture di alto livello di tre topologie di cluster supportate.</span><span class="sxs-lookup"><span data-stu-id="48111-126">Following are high-level architectures of three supported cluster topologies.</span></span> <span data-ttu-id="48111-127">Le topologie a disponibilità elevata includono più nodi head del cluster.</span><span class="sxs-lookup"><span data-stu-id="48111-127">High-availability topologies include multiple cluster head nodes.</span></span>

1. <span data-ttu-id="48111-128">Il cluster a disponibilità elevata con dominio di Active Directory</span><span class="sxs-lookup"><span data-stu-id="48111-128">High-availability cluster with Active Directory domain</span></span>

    ![Il cluster a disponibilità elevata nel dominio AD](./media/hpcpack-2016-cluster/haad.png)



2. <span data-ttu-id="48111-130">Il cluster a disponibilità elevata senza dominio di Active Directory</span><span class="sxs-lookup"><span data-stu-id="48111-130">High-availability cluster without Active Directory domain</span></span>

    ![Il cluster a disponibilità elevata senza dominio AD](./media/hpcpack-2016-cluster/hanoad.png)

3. <span data-ttu-id="48111-132">Cluster con un singolo nodo head</span><span class="sxs-lookup"><span data-stu-id="48111-132">Cluster with a single head node</span></span>

   ![Cluster con nodo head singolo](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a><span data-ttu-id="48111-134">Distribuire un cluster</span><span class="sxs-lookup"><span data-stu-id="48111-134">Deploy a cluster</span></span>

<span data-ttu-id="48111-135">Per creare il cluster, scegliere un modello e fare clic su **Distribuisci in Azure**.</span><span class="sxs-lookup"><span data-stu-id="48111-135">To create the cluster, choose a template and click **Deploy to Azure**.</span></span> <span data-ttu-id="48111-136">Nel [portale di Azure](https://portal.azure.com) specificare i parametri per il modello come descritto nei passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="48111-136">In the [Azure portal](https://portal.azure.com), specify parameters for the template as described in the following steps.</span></span> <span data-ttu-id="48111-137">Ogni modello crea tutte le risorse di Azure necessarie per l'infrastruttura del cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="48111-137">Each template creates all Azure resources required for the HPC cluster infrastructure.</span></span> <span data-ttu-id="48111-138">Le risorse sono: rete virtuale di Azure, indirizzo IP pubblico, bilanciamento del carico (solo per un cluster a disponibilità elevata), interfacce di rete, set di disponibilità, account di archiviazione e macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="48111-138">Resources include an Azure virtual network, public IP address, load balancer (only for a high-availability cluster), network interfaces, availability sets, storage accounts, and virtual machines.</span></span>

### <a name="step-1-select-the-subscription-location-and-resource-group"></a><span data-ttu-id="48111-139">Passaggio 1: Selezionare la sottoscrizione, il percorso e il gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="48111-139">Step 1: Select the subscription, location, and resource group</span></span>

<span data-ttu-id="48111-140">La **sottoscrizione** e il **percorso** devono essere gli stessi specificati quando è stato caricato il certificato PFX (vedere la sezione Prerequisiti).</span><span class="sxs-lookup"><span data-stu-id="48111-140">The **Subscription** and the **Location** must be same that you specified when you uploaded your PFX certificate (see Prerequisites).</span></span> <span data-ttu-id="48111-141">È consigliabile creare un **gruppo di risorse** per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="48111-141">We recommend that you create a **Resource group** for the deployment.</span></span>

### <a name="step-2-specify-the-parameter-settings"></a><span data-ttu-id="48111-142">Passaggio 2: Specificare le impostazioni dei parametri</span><span class="sxs-lookup"><span data-stu-id="48111-142">Step 2: Specify the parameter settings</span></span>

<span data-ttu-id="48111-143">Immettere o modificare i valori dei parametri del modello.</span><span class="sxs-lookup"><span data-stu-id="48111-143">Enter or modify values for the template parameters.</span></span> <span data-ttu-id="48111-144">Per visualizzare le informazioni della Guida, fare clic sull'icona accanto a ciascun parametro.</span><span class="sxs-lookup"><span data-stu-id="48111-144">Click the icon next to each parameter for help information.</span></span> <span data-ttu-id="48111-145">Vedere anche le linee guida per le [dimensioni delle macchine virtuali disponibili](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="48111-145">Also see the guidance for [available VM sizes](sizes.md).</span></span>

<span data-ttu-id="48111-146">Specificare i valori registrati in Prerequisiti per i parametri seguenti: **Nome dell'insieme di credenziali**, **Gruppo di risorse dell'insieme di credenziali**, **URL certificato** e **Identificazione personale certificato**.</span><span class="sxs-lookup"><span data-stu-id="48111-146">Specify the values you recorded in the Prerequisites for the following parameters: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

### <a name="step-3-review-legal-terms-and-create"></a><span data-ttu-id="48111-147">Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="48111-147">Step 3.</span></span> <span data-ttu-id="48111-148">Rivedere le note legali e creare</span><span class="sxs-lookup"><span data-stu-id="48111-148">Review legal terms and create</span></span>
<span data-ttu-id="48111-149">Fare clic su **Rivedere le note legali** per esaminare le condizioni.</span><span class="sxs-lookup"><span data-stu-id="48111-149">Click **Review legal terms** to review the terms.</span></span> <span data-ttu-id="48111-150">Se si accetta, fare clic su **Acquista** e selezionare **Crea** per avviare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="48111-150">If you agree, click **Purchase**, and then click **Create** to start the deployment.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="48111-151">Connettersi al cluster</span><span class="sxs-lookup"><span data-stu-id="48111-151">Connect to the cluster</span></span>
1. <span data-ttu-id="48111-152">Dopo aver distribuito il cluster HPC Pack, accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="48111-152">After the HPC Pack cluster is deployed, go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="48111-153">Fare clic su **Gruppi di risorse** e individuare il gruppo di risorse in cui è stato distribuito il cluster.</span><span class="sxs-lookup"><span data-stu-id="48111-153">Click **Resource groups**, and find the resource group in which the cluster was deployed.</span></span> <span data-ttu-id="48111-154">È possibile cercare le macchine virtuali del nodo head.</span><span class="sxs-lookup"><span data-stu-id="48111-154">You can find the head node virtual machines.</span></span>

    ![Nodi head del cluster nel portale](./media/hpcpack-2016-cluster/clusterhns.png)

2. <span data-ttu-id="48111-156">Fare clic su un nodo head (in un cluster a disponibilità elevata, fare clic su uno qualsiasi dei nodi head).</span><span class="sxs-lookup"><span data-stu-id="48111-156">Click one head node (in a high-availability cluster, click any of the head nodes).</span></span> <span data-ttu-id="48111-157">In **Essentials** è possibile trovare l'indirizzo IP pubblico o il nome DNS completo del cluster.</span><span class="sxs-lookup"><span data-stu-id="48111-157">In **Essentials**, you can find the public IP address or full DNS name of the cluster.</span></span>

    ![Impostazioni di connessione del cluster](./media/hpcpack-2016-cluster/clusterconnect.png)

3. <span data-ttu-id="48111-159">Fare clic su **Connetti** per accedere a uno dei nodi head usando Desktop remoto con il nome utente amministratore specificato.</span><span class="sxs-lookup"><span data-stu-id="48111-159">Click **Connect** to log on to any of the head nodes using Remote Desktop with your specified administrator user name.</span></span> <span data-ttu-id="48111-160">Se il cluster distribuito si trova in un dominio di Active Directory, il nome utente sarà nel formato <privateDomainName>\<adminUsername> (ad esempio, hpc.local\hpcadmin).</span><span class="sxs-lookup"><span data-stu-id="48111-160">If the cluster you deployed is in an Active Directory Domain, the user name is of the form <privateDomainName>\<adminUsername> (for example, hpc.local\hpcadmin).</span></span>

## <a name="next-steps"></a><span data-ttu-id="48111-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="48111-161">Next steps</span></span>
* <span data-ttu-id="48111-162">Inviare i processi al cluster.</span><span class="sxs-lookup"><span data-stu-id="48111-162">Submit jobs to your cluster.</span></span> <span data-ttu-id="48111-163">Vedere [Inviare i processi a un cluster HPC e HPC Pack in Azure](hpcpack-cluster-submit-jobs.md) e [Gestire un cluster HPC Pack 2016 in Azure usando Azure Active Directory](hpcpack-cluster-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="48111-163">See [Submit jobs to HPC an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md) and [Manage an HPC Pack 2016 cluster in Azure using Azure Active Directory](hpcpack-cluster-active-directory.md).</span></span>

