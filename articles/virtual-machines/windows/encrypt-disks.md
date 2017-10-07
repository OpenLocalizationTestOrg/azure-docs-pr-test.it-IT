---
title: aaaEncrypt dischi in una macchina virtuale Windows in Azure | Documenti Microsoft
description: "Con Azure PowerShell di protezione avanzata di tooencrypt dischi virtuali in una macchina virtuale di Windows per la modalità"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/10/2017
ms.author: iainfou
ms.openlocfilehash: 77c42a67cb57a9dc5fe3159fce0be75e3a965be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a>Come tooencrypt dischi virtuali in una macchina virtuale Windows
Per migliorare gli aspetti di sicurezza e conformità delle macchine virtuali (VM), i dischi virtuali in Azure possono essere crittografati. I dischi vengono crittografati usando chiavi di crittografia protette in un insieme di credenziali delle chiavi di Azure. È possibile controllare queste chiavi di crittografia e il loro uso. Questo articolo dettagli come i dischi virtuali tooencrypt in una macchina virtuale Windows usando Azure PowerShell. È anche possibile [crittografare una VM Linux di hello Azure CLI 2.0](../linux/encrypt-disks.md).

## <a name="overview-of-disk-encryption"></a>Panoramica della crittografia dei dischi
I dischi virtuali delle VM di Windows vengono crittografati a riposo mediante Bitlocker. Non è previsto alcun addebito per la crittografia dei dischi virtuali in Azure. Chiavi di crittografia vengono archiviate nell'insieme di credenziali di Azure chiave tramite software di protezione oppure è possibile importare o generare le chiavi in moduli di protezione Hardware (HSM) Certificate tooFIPS standard di livello 2 di 140-2. Queste chiavi di crittografia sono utilizzati tooencrypt e decrittografare i dischi virtuali collegati tooyour macchina virtuale. È possibile esercitare il controllo su queste chiavi di crittografia e sul loro uso. Un'entità servizio di Azure Active Directory offre un meccanismo protetto per il rilascio delle chiavi di crittografia all'accensione e allo spegnimento delle VM.

il processo di Hello per la crittografia di una macchina virtuale è il seguente:

1. Creare una chiave di crittografia in un insieme di credenziali delle chiavi di Azure.
2. Configurare hello crittografia chiave toobe utilizzabile per la crittografia dei dischi.
3. chiave di crittografia hello tooread dall'hello insieme di credenziali chiave di Azure, creare un servizio di Azure Active Directory principale con le autorizzazioni appropriate di hello.
4. Eseguire hello comando tooencrypt i dischi virtuali, specifica dell'entità servizio di Azure Active Directory hello e appropriato toobe chiave crittografica utilizzata.
5. le entità richieste di servizio Azure Active Directory Hello hello chiave di crittografia richiesto dall'insieme di credenziali chiave di Azure.
6. i dischi virtuali Hello vengono crittografati tramite la chiave crittografica hello fornito.

## <a name="encryption-process"></a>Processo di crittografia
Crittografia del disco si basa su hello i componenti aggiuntivi seguenti:

* **Insieme di credenziali chiave di Azure** -utilizzate le chiavi di crittografia toosafeguard e segreti utilizzati per il processo di crittografia/decrittografia hello disco. 
  * Se disponibile, è possibile usare un insieme di credenziali delle chiavi di Azure esistente. Non si dispone toodedicate i dischi tooencrypting un insieme di credenziali chiave.
  * limiti amministrativi tooseparate e visibilità chiave, è possibile creare un insieme di credenziali chiave dedicato.
* **Azure Active Directory** : handle hello lo scambio sicuro di chiavi di crittografia necessarie e richiesta l'autenticazione per le azioni. 
  * In genere, è possibile inserire l'applicazione in un'istanza esistente di Azure Active Directory.
  * entità servizio Hello fornisce un meccanismo protetto di toorequest e generato le chiavi di crittografia appropriato hello. Non si sta procedendo a sviluppare un'applicazione reale integrata con Azure Active Directory.

## <a name="requirements-and-limitations"></a>Requisiti e limitazioni
Requisiti relativi alla crittografia dei dischi e scenari supportati:

* Abilitazione della crittografia in nuove macchine virtuali di Windows da immagini di Azure Marketplace o da un'immagine del disco rigido virtuale personalizzata.
* Abilitazione della crittografia nelle macchine virtuali esistenti di Windows in Azure.
* Abilitazione della crittografia nelle macchine virtuali di Windows configurate usando spazi di archiviazione.
* Disabilitazione della crittografia nel sistema operativo e nelle unità dati per le VM di Windows.
* Tutte le risorse (ad esempio l'insieme di credenziali chiave, l'account di archiviazione e macchina virtuale) devono essere in hello stessa regione di Azure e sottoscrizione.
* Macchine virtuali di livello standard, ad esempio macchine virtuali di serie A, D, DS, G e GS.

Crittografia del disco non è attualmente supportata nei seguenti scenari hello:

* VM di base.
* Macchine virtuali create con modello di distribuzione classica hello.
* Aggiornamento delle chiavi di crittografia in una VM già crittografata hello.
* Integrazione con il Servizio di gestione delle chiavi locale.

## <a name="create-azure-key-vault-and-keys"></a>Creare le chiavi e l'insieme di credenziali delle chiavi di Azure
Prima di iniziare, verificare che la versione più recente di hello di hello Azure PowerShell modulo è stato installato. Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview). Nel corso di esempi di comandi hello, sostituire tutti i parametri di esempio con i nomi, percorso e i valori di chiave. Negli esempi seguenti Hello utilizzano una convenzione di *myResourceGroup*, *myKeyVault*, *myVM*e così via.

primo passaggio Hello è toocreate toostore un insieme di credenziali chiave Azure le chiavi di crittografia. Insieme di credenziali chiave di Azure è possibile archiviare le chiavi, i segreti, o le password che consentono di toosecurely implementano nelle applicazioni e servizi. Per la crittografia del disco virtuale, si crea un insieme di credenziali chiave di toostore una chiave di crittografia che viene utilizzato tooencrypt o decrittografare i dischi virtuali. 

Abilitare il provider di credenziali chiave hello nella sottoscrizione di Azure con [registro AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), quindi creare un gruppo di risorse con [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). esempio Hello crea il nome di un gruppo di risorse *myResourceGroup* in hello *Stati Uniti orientali* percorso:

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

Hello insieme credenziali chiavi Azure contenente hello le chiavi di crittografia e calcolo associato risorse, ad esempio hello macchina virtuale stessa e di archiviazione devono trovarsi nella hello stessa area. Creare un insieme di credenziali chiave di Azure con [New AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) e abilitare hello insieme di credenziali chiave per l'utilizzo con crittografia del disco. Specificare un nome univoco di Key Vault per *keyVaultName* come indicato di seguito:

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

È possibile archiviare le chiavi di crittografia usando il software o il modulo di protezione hardware. L'uso di un modulo di protezione hardware richiede un insieme di credenziali delle chiavi premium. È un toocreating costi aggiuntivi premium insieme di credenziali chiave anziché standard insieme di credenziali chiave che archivia le chiavi protette tramite software. un insieme di credenziali chiave premium nel precedente passaggio hello toocreate aggiungere hello *- Sku "Premium"* parametri. Hello esempio seguente usa le chiavi protette tramite software poiché è stato creato un insieme di credenziali chiave standard. 

Per entrambi i modelli di protezione, hello piattaforma Azure deve toobe concesso accesso toorequest hello chiavi di crittografia quando si avvia i dischi virtuali hello toodecrypt hello macchina virtuale. Creare una chiave crittografica in Key Vault con [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey). esempio Hello crea una chiave denominata *myKey*:

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a>Creare hello dell'entità servizio di Azure Active Directory
Quando i dischi virtuali vengono crittografati o decrittografati, specificare l'autenticazione di account toohandle hello e lo scambio delle chiavi di crittografia dall'insieme di credenziali chiave. Questo account, un'entità di servizio di Azure Active Directory consente hello piattaforma Azure toorequest hello appropriato le chiavi di crittografia per conto di hello macchina virtuale. Un'istanza di Azure Active Directory predefinita è già disponibile nella sottoscrizione, anche se molte organizzazioni hanno directory di Azure Active Directory dedicate.

Creare un'entità servizio in Azure Active Directory con [New AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal). toospecify una password sicura, seguire hello [restrizioni in Azure Active Directory e criteri Password](../../active-directory/active-directory-passwords-policy.md):

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

toosuccessfully crittografare o decrittografare i dischi virtuali, le autorizzazioni sulla chiave di crittografia hello archiviati nell'insieme di credenziali chiave devono essere principale tooread hello chiavi del set toopermit hello Azure Active Directory del servizio. Impostare le autorizzazioni per Key Vault con [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a>Crea macchina virtuale
tootest hello processo di crittografia, creare una macchina virtuale. esempio Hello crea una macchina virtuale denominata *myVM* utilizzando un *Data Center di Windows Server 2016* immagine:

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "mypublicdns$(Get-Random)"

$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$cred = Get-Credential

$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```


## <a name="encrypt-virtual-machine"></a>Crittografare una macchina virtuale
tooencrypt hello i dischi virtuali, riunire tutti i componenti precedenti hello:

1. Specificare hello entità servizio di Azure Active Directory e una password.
2. Specificare hello insieme di credenziali chiave toostore hello metadati per i dischi crittografati.
3. Specificare hello toouse di chiavi di crittografia per hello effettivo crittografia e decrittografia.
4. Specificare se si desidera tooencrypt hello del sistema operativo disco, i dischi dati hello o tutti.

Crittografare la macchina virtuale con [Set AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) utilizzando la chiave di insieme credenziali chiavi Azure hello e le credenziali dell'entità servizio di Azure Active Directory. Recupera tutte le informazioni chiave hello Hello esempio seguente viene quindi crittografa hello macchina virtuale denominata *myVM*:

```powershell
$keyVault = Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $rgName;
$diskEncryptionKeyVaultUrl = $keyVault.VaultUri;
$keyVaultResourceId = $keyVault.ResourceId;
$keyEncryptionKeyUrl = (Get-AzureKeyVaultKey -VaultName $keyVaultName -Name myKey).Key.kid;

Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $rgName `
    -VMName $vmName `
    -AadClientID $app.ApplicationId `
    -AadClientSecret $securePassword `
    -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl `
    -DiskEncryptionKeyVaultId $keyVaultResourceId `
    -KeyEncryptionKeyUrl $keyEncryptionKeyUrl `
    -KeyEncryptionKeyVaultId $keyVaultResourceId
```

Accettare hello toocontinue prompt dei comandi con la crittografia di VM hello. Hello VM viene riavviato durante il processo di hello. Una volta completato il processo di crittografia hello e hello VM è stato riavviato, verificare lo stato di crittografia hello con [Get AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

Hello l'output è simile toohello seguente esempio:

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a>Passaggi successivi
* Per altre informazioni sulla gestione di Azure Key Vault, vedere [Configurare il Key Vault per le macchine virtuali](key-vault-setup.md).
* Per ulteriori informazioni sulla crittografia del disco, ad esempio la preparazione di un tooAzure di tooupload macchina virtuale personalizzata crittografato, vedere [crittografia del disco Azure](../../security/azure-security-disk-encryption.md).
