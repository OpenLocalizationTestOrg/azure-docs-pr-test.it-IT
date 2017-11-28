---
title: aaaSet di accesso di gestione remota Windows per una macchina virtuale di Azure | Documenti Microsoft
description: Configurare WinRM l'accesso per l'utilizzo con una macchina virtuale Azure creata nel modello di distribuzione di gestione risorse di hello.
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9718e85b-d360-4621-90b8-0b0b84a21208
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/16/2016
ms.author: kasing
ms.openlocfilehash: 23d1d3a3065cbd8e4036be085c6d835cae36caae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="d62a9-103">Configurare l'accesso WinRM per le macchine virtuali in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d62a9-103">Setting up WinRM access for Virtual Machines in Azure Resource Manager</span></span>
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a><span data-ttu-id="d62a9-104">WinRM nella gestione del servizio Azure e Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d62a9-104">WinRM in Azure Service Management vs Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* <span data-ttu-id="d62a9-105">Per una panoramica di hello Azure Resource Manager, consultare la [articolo](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d62a9-105">For an overview of hello Azure Resource Manager, please see this [article](../../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="d62a9-106">Per conoscere le differenze tra la gestione del servizio Azure e Azure Resource Manager, consultare questo [articolo](../../resource-manager-deployment-model.md)</span><span class="sxs-lookup"><span data-stu-id="d62a9-106">For differences between Azure Service Management and Azure Resource Manager, please see this [article](../../resource-manager-deployment-model.md)</span></span>

<span data-ttu-id="d62a9-107">Hello differenza principale nell'impostazione di configurazione di gestione remota Windows tra due stack hello è come certificato hello viene installato e su hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d62a9-107">hello key difference in setting up WinRM configuration between hello two stacks is how hello certificate gets installed on hello VM.</span></span> <span data-ttu-id="d62a9-108">Nello stack di gestione risorse di Azure hello, certificati hello vengono modellati come risorse gestite dal Provider di risorse dell'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="d62a9-108">In hello Azure Resource Manager stack, hello certificates are modeled as resources managed by hello Key Vault Resource Provider.</span></span> <span data-ttu-id="d62a9-109">Pertanto, utente hello deve tooprovide il proprio certificato e caricarlo tooa insieme di credenziali chiave prima di utilizzarlo in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d62a9-109">Therefore, hello user needs tooprovide their own certificate and upload it tooa Key Vault before using it in a VM.</span></span>

<span data-ttu-id="d62a9-110">Ecco i passaggi di hello è necessario tooset tootake una macchina virtuale con connettività di WinRM</span><span class="sxs-lookup"><span data-stu-id="d62a9-110">Here are hello steps you need tootake tooset up a VM with WinRM connectivity</span></span>

1. <span data-ttu-id="d62a9-111">Creare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="d62a9-111">Create a Key Vault</span></span>
2. <span data-ttu-id="d62a9-112">Creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="d62a9-112">Create a self-signed certificate</span></span>
3. <span data-ttu-id="d62a9-113">Caricare il tooKey certificato autofirmato dell'insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="d62a9-113">Upload your self-signed certificate tooKey Vault</span></span>
4. <span data-ttu-id="d62a9-114">Ottenere hello URL per il certificato autofirmato nell'insieme di credenziali chiave hello</span><span class="sxs-lookup"><span data-stu-id="d62a9-114">Get hello URL for your self-signed certificate in hello Key Vault</span></span>
5. <span data-ttu-id="d62a9-115">Fare riferimento all'URL del certificato autofirmato durante la creazione di una VM</span><span class="sxs-lookup"><span data-stu-id="d62a9-115">Reference your self-signed certificates URL while creating a VM</span></span>

## <a name="step-1-create-a-key-vault"></a><span data-ttu-id="d62a9-116">Passaggio 1: Creare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="d62a9-116">Step 1: Create a Key Vault</span></span>
<span data-ttu-id="d62a9-117">È possibile utilizzare hello sotto comando toocreate hello insieme di credenziali chiave</span><span class="sxs-lookup"><span data-stu-id="d62a9-117">You can use hello below command toocreate hello Key Vault</span></span>

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a><span data-ttu-id="d62a9-118">Passaggio 2: Creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="d62a9-118">Step 2: Create a self-signed certificate</span></span>
<span data-ttu-id="d62a9-119">Per creare un certificato autofirmato, è possibile utilizzare questo script PowerShell</span><span class="sxs-lookup"><span data-stu-id="d62a9-119">You can create a self-signed certificate using this PowerShell script</span></span>

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter hello certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-toohello-key-vault"></a><span data-ttu-id="d62a9-120">Passaggio 3: Caricare l'insieme di credenziali chiave di toohello certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="d62a9-120">Step 3: Upload your self-signed certificate toohello Key Vault</span></span>
<span data-ttu-id="d62a9-121">Prima di caricare hello certificato toohello insieme di credenziali chiave creata nel passaggio 1, è necessario che tooconverted in hello un formato di comprendere i provider di risorse di Microsoft. COMPUTE.</span><span class="sxs-lookup"><span data-stu-id="d62a9-121">Before uploading hello certificate toohello Key Vault created in step 1, it needs tooconverted into a format hello Microsoft.Compute resource provider will understand.</span></span> <span data-ttu-id="d62a9-122">Hello script PowerShell seguente consentirà di effettuare questa operazione</span><span class="sxs-lookup"><span data-stu-id="d62a9-122">hello below PowerShell script will allow you do that</span></span>

```
$fileName = "<Path toohello .pfx file>"
$fileContentBytes = Get-Content $fileName -Encoding Byte
$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

$jsonObject = @"
{
  "data": "$filecontentencoded",
  "dataType" :"pfx",
  "password": "<password>"
}
"@

$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText –Force
Set-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>" -SecretValue $secret
```

## <a name="step-4-get-hello-url-for-your-self-signed-certificate-in-hello-key-vault"></a><span data-ttu-id="d62a9-123">Passaggio 4: Ottenere hello URL per il certificato autofirmato nell'insieme di credenziali chiave hello</span><span class="sxs-lookup"><span data-stu-id="d62a9-123">Step 4: Get hello URL for your self-signed certificate in hello Key Vault</span></span>
<span data-ttu-id="d62a9-124">provider di risorse Microsoft. COMPUTE Hello è necessario un segreto toohello URL all'interno di hello insieme di credenziali chiave durante il provisioning hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d62a9-124">hello Microsoft.Compute resource provider needs a URL toohello secret inside hello Key Vault while provisioning hello VM.</span></span> <span data-ttu-id="d62a9-125">Questo consente di chiave privata di hello toodownload provider risorse Microsoft. COMPUTE hello e creare certificati equivalente hello in hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d62a9-125">This enables hello Microsoft.Compute resource provider toodownload hello secret and create hello equivalent certificate on hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="d62a9-126">l'URL di Hello del segreto hello deve tooinclude hello versione.</span><span class="sxs-lookup"><span data-stu-id="d62a9-126">hello URL of hello secret needs tooinclude hello version as well.</span></span> <span data-ttu-id="d62a9-127">Di seguito è riportato un esempio di URL: https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span><span class="sxs-lookup"><span data-stu-id="d62a9-127">An example URL looks like below https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span></span>
> 
> 

#### <a name="templates"></a><span data-ttu-id="d62a9-128">Modelli</span><span class="sxs-lookup"><span data-stu-id="d62a9-128">Templates</span></span>
<span data-ttu-id="d62a9-129">È possibile ottenere l'URL di toohello collegamento hello nel modello di hello utilizzando hello di codice riportato di seguito</span><span class="sxs-lookup"><span data-stu-id="d62a9-129">You can get hello link toohello URL in hello template using hello below code</span></span>

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a><span data-ttu-id="d62a9-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d62a9-130">PowerShell</span></span>
<span data-ttu-id="d62a9-131">È possibile ottenere questo URL mediante hello comando PowerShell seguente</span><span class="sxs-lookup"><span data-stu-id="d62a9-131">You can get this URL using hello below PowerShell command</span></span>

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a><span data-ttu-id="d62a9-132">Passaggio 5: Durante la creazione di una VM, fare riferimento all'URL dei certificati autofirmati</span><span class="sxs-lookup"><span data-stu-id="d62a9-132">Step 5: Reference your self-signed certificates URL while creating a VM</span></span>
#### <a name="azure-resource-manager-templates"></a><span data-ttu-id="d62a9-133">Modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d62a9-133">Azure Resource Manager Templates</span></span>
<span data-ttu-id="d62a9-134">Durante la creazione di una macchina virtuale tramite modelli di certificato hello viene fatto riferimento nella sezione segreti hello e nella sezione gestione remota Windows hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="d62a9-134">While creating a VM through templates, hello certificate gets referenced in hello secrets section and hello winRM section as below:</span></span>

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of hello Key Vault containing hello secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for hello certificate you got in Step 4>",
                  "certificateStore": "<Name of hello certificate store on hello VM>"
                }
              ]
            }
          ],
          "windowsConfiguration": {
            ...
            "winRM": {
              "listeners": [
                {
                  "protocol": "http"
                },
                {
                  "protocol": "https",
                  "certificateUrl": "<URL for hello certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

<span data-ttu-id="d62a9-135">Un modello di esempio per hello sopra è reperibile qui in [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="d62a9-135">A sample template for hello above can be found here at [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span></span>

<span data-ttu-id="d62a9-136">Il codice sorgente di questo modello è reperibile in [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="d62a9-136">Source code for this template can be found on [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span></span>

#### <a name="powershell"></a><span data-ttu-id="d62a9-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d62a9-137">PowerShell</span></span>
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-toohello-vm"></a><span data-ttu-id="d62a9-138">Passaggio 6: Connessione toohello VM</span><span class="sxs-lookup"><span data-stu-id="d62a9-138">Step 6: Connecting toohello VM</span></span>
<span data-ttu-id="d62a9-139">Prima di poter connettere toohello macchina virtuale è necessario che il computer sia configurato per la gestione remota WinRM toomake.</span><span class="sxs-lookup"><span data-stu-id="d62a9-139">Before you can connect toohello VM you'll need toomake sure your machine is configured for WinRM remote management.</span></span> <span data-ttu-id="d62a9-140">Avviare PowerShell come amministratore ed eseguire hello sotto toomake di comando che desidera configurare.</span><span class="sxs-lookup"><span data-stu-id="d62a9-140">Start PowerShell as an administrator and execute hello below command toomake sure you're set up.</span></span>

    Enable-PSRemoting -Force

> [!NOTE]
> <span data-ttu-id="d62a9-141">Potrebbe essere necessario toomake che hello servizio Gestione remota Windows sia in esecuzione se hello sopra non funziona.</span><span class="sxs-lookup"><span data-stu-id="d62a9-141">You might need toomake sure hello WinRM service is running if hello above does not work.</span></span> <span data-ttu-id="d62a9-142">Per farlo, utilizzare `Get-Service WinRM`</span><span class="sxs-lookup"><span data-stu-id="d62a9-142">You can do that using `Get-Service WinRM`</span></span>
> 
> 

<span data-ttu-id="d62a9-143">Al termine dell'installazione di hello, è possibile connettersi toohello VM utilizzando hello comando seguente</span><span class="sxs-lookup"><span data-stu-id="d62a9-143">Once hello setup is done, you can connect toohello VM using hello below command</span></span>

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
