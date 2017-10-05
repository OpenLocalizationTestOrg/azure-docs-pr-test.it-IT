---
title: Configurare l'accesso WinRM per una macchina virtuale di Azure | Documentazione Microsoft
description: Configurare l'accesso WinRM per l'uso con una macchina virtuale di Azure creata con il modello di distribuzione Resource Manager.
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
ms.openlocfilehash: 2d6533462400bc1d93d0d3b0227769784e2658a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="3a265-103">Configurare l'accesso WinRM per le macchine virtuali in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3a265-103">Setting up WinRM access for Virtual Machines in Azure Resource Manager</span></span>
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a><span data-ttu-id="3a265-104">WinRM nella gestione del servizio Azure e Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3a265-104">WinRM in Azure Service Management vs Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* <span data-ttu-id="3a265-105">Per una panoramica di Azure Resource Manager, vedere questo [articolo](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3a265-105">For an overview of the Azure Resource Manager, please see this [article](../../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="3a265-106">Per conoscere le differenze tra la gestione del servizio Azure e Azure Resource Manager, consultare questo [articolo](../../resource-manager-deployment-model.md)</span><span class="sxs-lookup"><span data-stu-id="3a265-106">For differences between Azure Service Management and Azure Resource Manager, please see this [article](../../resource-manager-deployment-model.md)</span></span>

<span data-ttu-id="3a265-107">La differenza principale nell'impostazione della configurazione di WinRM tra i due stack consiste nelle modalità di installazione del certificato nella VM.</span><span class="sxs-lookup"><span data-stu-id="3a265-107">The key difference in setting up WinRM configuration between the two stacks is how the certificate gets installed on the VM.</span></span> <span data-ttu-id="3a265-108">Nello stack di Azure Resource Manager, i certificati vengono modellati come risorse gestite dal provider di risorse dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="3a265-108">In the Azure Resource Manager stack, the certificates are modeled as resources managed by the Key Vault Resource Provider.</span></span> <span data-ttu-id="3a265-109">Pertanto, l'utente deve fornire il proprio certificato e caricarlo in un insieme di credenziali delle chiavi per poterlo utilizzare in una VM.</span><span class="sxs-lookup"><span data-stu-id="3a265-109">Therefore, the user needs to provide their own certificate and upload it to a Key Vault before using it in a VM.</span></span>

<span data-ttu-id="3a265-110">Di seguito è descritta la procedura per configurare una VM con connettività WinRM</span><span class="sxs-lookup"><span data-stu-id="3a265-110">Here are the steps you need to take to set up a VM with WinRM connectivity</span></span>

1. <span data-ttu-id="3a265-111">Creare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="3a265-111">Create a Key Vault</span></span>
2. <span data-ttu-id="3a265-112">Creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="3a265-112">Create a self-signed certificate</span></span>
3. <span data-ttu-id="3a265-113">Caricare il certificato autofirmato per l'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="3a265-113">Upload your self-signed certificate to Key Vault</span></span>
4. <span data-ttu-id="3a265-114">Ottenere l'URL del certificato autofirmato nell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="3a265-114">Get the URL for your self-signed certificate in the Key Vault</span></span>
5. <span data-ttu-id="3a265-115">Fare riferimento all'URL del certificato autofirmato durante la creazione di una VM</span><span class="sxs-lookup"><span data-stu-id="3a265-115">Reference your self-signed certificates URL while creating a VM</span></span>

## <a name="step-1-create-a-key-vault"></a><span data-ttu-id="3a265-116">Passaggio 1: Creare un insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="3a265-116">Step 1: Create a Key Vault</span></span>
<span data-ttu-id="3a265-117">Il seguente comando consente di creare l'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="3a265-117">You can use the below command to create the Key Vault</span></span>

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a><span data-ttu-id="3a265-118">Passaggio 2: Creare un certificato autofirmato</span><span class="sxs-lookup"><span data-stu-id="3a265-118">Step 2: Create a self-signed certificate</span></span>
<span data-ttu-id="3a265-119">Per creare un certificato autofirmato, è possibile utilizzare questo script PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a265-119">You can create a self-signed certificate using this PowerShell script</span></span>

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter the certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-to-the-key-vault"></a><span data-ttu-id="3a265-120">Passaggio 3: Caricare il certificato autofirmato per l'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="3a265-120">Step 3: Upload your self-signed certificate to the Key Vault</span></span>
<span data-ttu-id="3a265-121">Prima di caricare il certificato nell'insieme di credenziali delle chiavi creato al Passaggio 1, è necessario convertirlo in un formato comprensibile per il provider di risorse Microsoft.Compute.</span><span class="sxs-lookup"><span data-stu-id="3a265-121">Before uploading the certificate to the Key Vault created in step 1, it needs to converted into a format the Microsoft.Compute resource provider will understand.</span></span> <span data-ttu-id="3a265-122">Per farlo, utilizzare lo script PowerShell qui di seguito</span><span class="sxs-lookup"><span data-stu-id="3a265-122">The below PowerShell script will allow you do that</span></span>

```
$fileName = "<Path to the .pfx file>"
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

## <a name="step-4-get-the-url-for-your-self-signed-certificate-in-the-key-vault"></a><span data-ttu-id="3a265-123">Passaggio 4: Ottenere l'URL del certificato autofirmato nell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="3a265-123">Step 4: Get the URL for your self-signed certificate in the Key Vault</span></span>
<span data-ttu-id="3a265-124">Durante il provisioning della VM, il provider di risorse Microsoft.Compute necessita dell'URL della chiave privata all'interno dell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="3a265-124">The Microsoft.Compute resource provider needs a URL to the secret inside the Key Vault while provisioning the VM.</span></span> <span data-ttu-id="3a265-125">Ciò consente al provider di risorse Microsoft.Compute di scaricare la chiave privata e creare il certificato equivalente nella VM.</span><span class="sxs-lookup"><span data-stu-id="3a265-125">This enables the Microsoft.Compute resource provider to download the secret and create the equivalent certificate on the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="3a265-126">L'URL della chiave privata deve includerne anche la versione.</span><span class="sxs-lookup"><span data-stu-id="3a265-126">The URL of the secret needs to include the version as well.</span></span> <span data-ttu-id="3a265-127">Di seguito è riportato un esempio di URL: https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span><span class="sxs-lookup"><span data-stu-id="3a265-127">An example URL looks like below https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span></span>
> 
> 

#### <a name="templates"></a><span data-ttu-id="3a265-128">Modelli</span><span class="sxs-lookup"><span data-stu-id="3a265-128">Templates</span></span>
<span data-ttu-id="3a265-129">Per ottenere il collegamento all'URL nel modello, è possibile utilizzre il codice seguente</span><span class="sxs-lookup"><span data-stu-id="3a265-129">You can get the link to the URL in the template using the below code</span></span>

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a><span data-ttu-id="3a265-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a265-130">PowerShell</span></span>
<span data-ttu-id="3a265-131">Questo URL può essere ottenuto utilizzando il seguente comando PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a265-131">You can get this URL using the below PowerShell command</span></span>

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a><span data-ttu-id="3a265-132">Passaggio 5: Durante la creazione di una VM, fare riferimento all'URL dei certificati autofirmati</span><span class="sxs-lookup"><span data-stu-id="3a265-132">Step 5: Reference your self-signed certificates URL while creating a VM</span></span>
#### <a name="azure-resource-manager-templates"></a><span data-ttu-id="3a265-133">Modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3a265-133">Azure Resource Manager Templates</span></span>
<span data-ttu-id="3a265-134">Quando si crea una VM tramite modelli, viene fatto riferimento al certificato nelle sezioni delle chiavi private e di WinRM, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3a265-134">While creating a VM through templates, the certificate gets referenced in the secrets section and the winRM section as below:</span></span>

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of the Key Vault containing the secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for the certificate you got in Step 4>",
                  "certificateStore": "<Name of the certificate store on the VM>"
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
                  "certificateUrl": "<URL for the certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

<span data-ttu-id="3a265-135">Un modello di esempio per quanto detto sopra è disponibile qui: [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="3a265-135">A sample template for the above can be found here at [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span></span>

<span data-ttu-id="3a265-136">Il codice sorgente di questo modello è reperibile in [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="3a265-136">Source code for this template can be found on [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span></span>

#### <a name="powershell"></a><span data-ttu-id="3a265-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a265-137">PowerShell</span></span>
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-to-the-vm"></a><span data-ttu-id="3a265-138">Passaggio 6: Connettersi alla VM</span><span class="sxs-lookup"><span data-stu-id="3a265-138">Step 6: Connecting to the VM</span></span>
<span data-ttu-id="3a265-139">Per potersi connettere alla VM è necessario controllare di aver configurato il computer per la gestione remota di WinRM.</span><span class="sxs-lookup"><span data-stu-id="3a265-139">Before you can connect to the VM you'll need to make sure your machine is configured for WinRM remote management.</span></span> <span data-ttu-id="3a265-140">Avviare PowerShell come amministratore ed eseguire il comando seguente per verificare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="3a265-140">Start PowerShell as an administrator and execute the below command to make sure you're set up.</span></span>

    Enable-PSRemoting -Force

> [!NOTE]
> <span data-ttu-id="3a265-141">Se non si riesce, potrebbe essere necessario verificare che il servizio WinRM sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3a265-141">You might need to make sure the WinRM service is running if the above does not work.</span></span> <span data-ttu-id="3a265-142">Per farlo, utilizzare `Get-Service WinRM`</span><span class="sxs-lookup"><span data-stu-id="3a265-142">You can do that using `Get-Service WinRM`</span></span>
> 
> 

<span data-ttu-id="3a265-143">Dopo avere completato l'installazione, è possibile connettersi alla VM utilizzando il comando seguente</span><span class="sxs-lookup"><span data-stu-id="3a265-143">Once the setup is done, you can connect to the VM using the below command</span></span>

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
