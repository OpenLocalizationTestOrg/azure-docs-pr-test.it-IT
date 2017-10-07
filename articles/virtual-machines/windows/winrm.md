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
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a>Configurare l'accesso WinRM per le macchine virtuali in Azure Resource Manager
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a>WinRM nella gestione del servizio Azure e Azure Resource Manager

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* Per una panoramica di hello Azure Resource Manager, consultare la [articolo](../../azure-resource-manager/resource-group-overview.md)
* Per conoscere le differenze tra la gestione del servizio Azure e Azure Resource Manager, consultare questo [articolo](../../resource-manager-deployment-model.md)

Hello differenza principale nell'impostazione di configurazione di gestione remota Windows tra due stack hello è come certificato hello viene installato e su hello macchina virtuale. Nello stack di gestione risorse di Azure hello, certificati hello vengono modellati come risorse gestite dal Provider di risorse dell'insieme di credenziali chiave hello. Pertanto, utente hello deve tooprovide il proprio certificato e caricarlo tooa insieme di credenziali chiave prima di utilizzarlo in una macchina virtuale.

Ecco i passaggi di hello è necessario tooset tootake una macchina virtuale con connettività di WinRM

1. Creare un insieme di credenziali delle chiavi
2. Creare un certificato autofirmato
3. Caricare il tooKey certificato autofirmato dell'insieme di credenziali
4. Ottenere hello URL per il certificato autofirmato nell'insieme di credenziali chiave hello
5. Fare riferimento all'URL del certificato autofirmato durante la creazione di una VM

## <a name="step-1-create-a-key-vault"></a>Passaggio 1: Creare un insieme di credenziali delle chiavi
È possibile utilizzare hello sotto comando toocreate hello insieme di credenziali chiave

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a>Passaggio 2: Creare un certificato autofirmato
Per creare un certificato autofirmato, è possibile utilizzare questo script PowerShell

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter hello certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-toohello-key-vault"></a>Passaggio 3: Caricare l'insieme di credenziali chiave di toohello certificato autofirmato
Prima di caricare hello certificato toohello insieme di credenziali chiave creata nel passaggio 1, è necessario che tooconverted in hello un formato di comprendere i provider di risorse di Microsoft. COMPUTE. Hello script PowerShell seguente consentirà di effettuare questa operazione

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

## <a name="step-4-get-hello-url-for-your-self-signed-certificate-in-hello-key-vault"></a>Passaggio 4: Ottenere hello URL per il certificato autofirmato nell'insieme di credenziali chiave hello
provider di risorse Microsoft. COMPUTE Hello è necessario un segreto toohello URL all'interno di hello insieme di credenziali chiave durante il provisioning hello macchina virtuale. Questo consente di chiave privata di hello toodownload provider risorse Microsoft. COMPUTE hello e creare certificati equivalente hello in hello macchina virtuale.

> [!NOTE]
> l'URL di Hello del segreto hello deve tooinclude hello versione. Di seguito è riportato un esempio di URL: https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve
> 
> 

#### <a name="templates"></a>Modelli
È possibile ottenere l'URL di toohello collegamento hello nel modello di hello utilizzando hello di codice riportato di seguito

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a>PowerShell
È possibile ottenere questo URL mediante hello comando PowerShell seguente

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a>Passaggio 5: Durante la creazione di una VM, fare riferimento all'URL dei certificati autofirmati
#### <a name="azure-resource-manager-templates"></a>Modelli di Azure Resource Manager
Durante la creazione di una macchina virtuale tramite modelli di certificato hello viene fatto riferimento nella sezione segreti hello e nella sezione gestione remota Windows hello come indicato di seguito:

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

Un modello di esempio per hello sopra è reperibile qui in [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)

Il codice sorgente di questo modello è reperibile in [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)

#### <a name="powershell"></a>PowerShell
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-toohello-vm"></a>Passaggio 6: Connessione toohello VM
Prima di poter connettere toohello macchina virtuale è necessario che il computer sia configurato per la gestione remota WinRM toomake. Avviare PowerShell come amministratore ed eseguire hello sotto toomake di comando che desidera configurare.

    Enable-PSRemoting -Force

> [!NOTE]
> Potrebbe essere necessario toomake che hello servizio Gestione remota Windows sia in esecuzione se hello sopra non funziona. Per farlo, utilizzare `Get-Service WinRM`
> 
> 

Al termine dell'installazione di hello, è possibile connettersi toohello VM utilizzando hello comando seguente

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
