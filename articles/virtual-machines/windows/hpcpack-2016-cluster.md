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
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a>Distribuire un cluster HPC Pack 2016 in Azure

Seguire i passaggi hello in questo articolo di toodeploy un [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster di macchine virtuali di Azure. HPC Pack è la soluzione HPC gratuita di Microsoft basata sulle tecnologie di Microsoft Azure e Windows Server e supporta un'ampia gamma di carichi di lavoro di HPC.

Utilizzare uno dei hello [modelli di gestione risorse di Azure](https://github.com/MsHpcPack/HPCPack2016) cluster HPC Pack 2016 hello toodeploy. È possibile scegliere tra diverse topologie di cluster con numeri differenti di nodi head del cluster e con nodi di calcolo Linux o Windows.

## <a name="prerequisites"></a>Prerequisiti

### <a name="pfx-certificate"></a>Certificato PFX

Un cluster di Microsoft HPC Pack 2016 richiede una comunicazione di scambio di informazioni personali (PFX) certificato toosecure hello tra i nodi HPC hello. certificato Hello deve soddisfare i seguenti requisiti hello:

* Deve avere una chiave privata abilitata per lo scambio di chiave
* L'uso di chiavi include la firma digitale e la crittografia a chiave
* L'uso di chiavi avanzato include l'autenticazione client e l'autenticazione server

Se si dispone già di un certificato che soddisfa questi requisiti, è possibile richiedere il certificato di hello da un'autorità di certificazione. In alternativa, è possibile utilizzare i seguenti comandi toogenerate hello certificato autofirmato basata sul sistema operativo di hello su cui eseguire il comando hello ed esportare un certificato PFX formato hello con chiave privata hello.

* **Per Windows 10 o Windows Server 2016**, eseguire hello incorporato **New-SelfSignedCertificate** cmdlet di PowerShell come indicato di seguito:

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* **Per i sistemi operativi precedenti a Windows 10 o Windows Server 2016**, scaricare hello [generatore certificato autofirmato](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) da hello Microsoft Script Center. Estrarre il contenuto ed eseguire hello comandi al prompt di PowerShell seguente:

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a>Carica certificato tooan insieme di credenziali chiave di Azure

Prima di distribuire un cluster HPC hello, caricare hello certificato tooan [insieme di credenziali chiave Azure](../../key-vault/index.md) come un hello segreto e registrare le seguenti informazioni per l'utilizzo durante la distribuzione di hello: **nome insieme di credenziali**,  **Gruppo di risorse dell'insieme di credenziali**, **URL certificato**, e **identificazione personale del certificato**.

Segue un certificato hello di tooupload script di PowerShell di esempio. Per ulteriori informazioni sul caricamento di un insieme di credenziali chiave di Azure di tooan certificato, vedere [introduzione insieme credenziali chiavi Azure](../../key-vault/key-vault-get-started.md).

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


## <a name="supported-topologies"></a>Topologie supportate

Scegliere una delle hello [modelli di gestione risorse di Azure](https://github.com/MsHpcPack/HPCPack2016) cluster HPC Pack 2016 hello toodeploy. Di seguito vengono indicate le architetture di alto livello di tre topologie di cluster supportate. Le topologie a disponibilità elevata includono più nodi head del cluster.

1. Il cluster a disponibilità elevata con dominio di Active Directory

    ![Il cluster a disponibilità elevata nel dominio AD](./media/hpcpack-2016-cluster/haad.png)



2. Il cluster a disponibilità elevata senza dominio di Active Directory

    ![Il cluster a disponibilità elevata senza dominio AD](./media/hpcpack-2016-cluster/hanoad.png)

3. Cluster con un singolo nodo head

   ![Cluster con nodo head singolo](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a>Distribuire un cluster

cluster hello toocreate, scegliere un modello e fare clic su **distribuire tooAzure**. In hello [portale di Azure](https://portal.azure.com), specificare i parametri per il modello di hello, come descritto in hello alla procedura seguente. Ogni modello crea tutte le risorse di Azure necessari per l'infrastruttura di cluster HPC hello. Le risorse sono: rete virtuale di Azure, indirizzo IP pubblico, bilanciamento del carico (solo per un cluster a disponibilità elevata), interfacce di rete, set di disponibilità, account di archiviazione e macchine virtuali.

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a>Passaggio 1: Selezionare la sottoscrizione hello, il percorso e gruppo di risorse

Hello **sottoscrizione** hello e **percorso** deve essere specificato quando è stato caricato il certificato PFX stesso (vedere la sezione Prerequisiti). È consigliabile creare un **gruppo di risorse** per la distribuzione di hello.

### <a name="step-2-specify-hello-parameter-settings"></a>Passaggio 2: Specificare le impostazioni dei parametri hello

Immettere o modificare i valori per parametri modello hello. Fare clic su parametro successivo tooeach hello icona per le informazioni della Guida. Vedere anche informazioni aggiuntive hello per [dimensioni delle macchine Virtuali disponibili](sizes.md).

Specificare i valori hello registrato nei prerequisiti hello per hello seguenti parametri: **nome insieme di credenziali**, **gruppo di risorse dell'insieme di credenziali**, **URL certificato**e **Identificazione personale del certificato**.

### <a name="step-3-review-legal-terms-and-create"></a>Passaggio 3. Rivedere le note legali e creare
Fare clic su **esaminare le note legali** termini hello tooreview. Se si accetta, fare clic su **acquisto**, quindi fare clic su **crea** distribuzione hello toostart.

## <a name="connect-toohello-cluster"></a>Connettere il cluster toohello
1. Dopo la distribuzione di cluster HPC Pack hello, visitare toohello [portale di Azure](https://portal.azure.com). Fare clic su **gruppi di risorse**e gruppo di risorse hello individuare in quale hello cluster è stato distribuito. È possibile trovare hello macchine virtuali di un nodo head.

    ![Nodi head del cluster nel portale di hello](./media/hpcpack-2016-cluster/clusterhns.png)

2. Fare clic su un nodo head (in un cluster a disponibilità elevata, fare clic su uno qualsiasi dei nodi head hello). In **Essentials**, è possibile trovare l'indirizzo IP pubblico hello o nome DNS completo del cluster di hello.

    ![Impostazioni di connessione del cluster](./media/hpcpack-2016-cluster/clusterconnect.png)

3. Fare clic su **Connetti** toolog su tooany dei nodi head di hello tramite Desktop remoto con il nome utente amministratore specificato. Se il cluster hello è distribuito in un dominio Active Directory, nome utente hello è formato hello <privateDomainName> \<adminUsername > (ad esempio, hpc.local\hpcadmin).

## <a name="next-steps"></a>Passaggi successivi
* Inviare cluster tooyour processi. Vedere [inviare processi tooHPC un cluster HPC Pack in Azure](hpcpack-cluster-submit-jobs.md) e [gestire un cluster HPC Pack 2016 in Azure tramite Azure Active Directory](hpcpack-cluster-active-directory.md).

