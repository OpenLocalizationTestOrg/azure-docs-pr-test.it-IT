---
title: aaaCreate una macchina virtuale di SQL Server in Azure PowerShell (versione classica) | Documenti Microsoft
description: "Fornisce procedure e script di PowerShell per la creazione di una macchina virtuale di Azure con le immagini della galleria di macchine virtuali SQL Server. In questo argomento Usa la modalità di distribuzione classica hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: b14d5d9bc192fa0a21126395ee20ffd06b3bf47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a>Effettuare il provisioning di una macchina virtuale di SQL Server con Azure PowerShell (classico)

In questo articolo viene descritta la procedura per la modalità toocreate una macchina virtuale di SQL Server in Azure utilizzando hello i cmdlet di PowerShell.

> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

Per la versione di hello Gestione risorse di questo argomento, vedere [il provisioning di una macchina virtuale di SQL Server tramite Gestione risorse di Azure PowerShell](../sql/virtual-machines-windows-ps-sql-create.md).

### <a name="install-and-configure-powershell"></a>Installare e configurare PowerShell:
1. Se non si dispone di un account Azure, provare la [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
2. [Scaricare e installare i comandi di PowerShell di Azure più recenti hello](/powershell/azure/overview).
3. Avviare Windows PowerShell e connetterla tooyour sottoscrizione di Azure con hello **Add-AzureAccount** comando.

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a>Determinare l'area di destinazione di Azure

La macchina virtuale di SQL Server verrà ospitata in un servizio cloud che si trova un'area di Azure specifica. Hello seguente procedura consente di toodetermine è l'area geografica, un account di archiviazione e un servizio cloud che verrà utilizzato per il resto di hello di esercitazione hello.

1. Determinare i data center di hello che si desidera toouse toohost la macchina virtuale di SQL Server. il comando PowerShell seguente viene visualizzato un elenco di nomi delle aree disponibili.

   ```powershell
   (Get-AzureLocation).Name
   ```

2. Dopo aver identificato il percorso desiderato, impostare una variabile denominata **$dcLocation** toothat area. Ad esempio, hello comando set hello area troppo seguente "Stati Uniti orientali":

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a>Impostare l'account di archiviazione e la sottoscrizione

1. Determinare hello sottoscrizione Azure, si utilizzerà per hello nuova macchina virtuale.

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. Assegnare il toohello di sottoscrizione di Azure di destinazione **$subscr** variabile. Quindi, impostarla come la sottoscrizione di Azure corrente.

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. Verificare la presenza di account di archiviazione esistenti. Hello lo script seguente consente di visualizzare tutti gli account di archiviazione presenti nel proprio paese scelto:

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > Se è necessario un nuovo account di archiviazione, creare innanzitutto un nome di account di archiviazione tutto minuscolo con il comando New-AzureStorageAccount hello come hello di esempio seguente:`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`

4. Assegnare hello destinazione storage account name toohello **$staccount**. Utilizzare quindi **Set-AzureSubscription** tooset hello sottoscrizione e l'account di archiviazione corrente.

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a>Selezionare un'immagine di macchina virtuale di SQL Server

1. Individuare l'elenco di hello di immagini di macchine virtuali di SQL Server disponibili dalla raccolta hello. Queste immagini hanno la proprietà **ImageFamily** che inizia con "SQL". esempio Hello query consente di visualizzare hello immagine famiglia disponibili tooyou che SQL Server è preinstallato.

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. Quando si individua una famiglia di immagine di macchina virtuale hello, in questo gruppo possono essere più immagini pubblicate. Lo script seguente hello utilizzare viene toofind hello più recente pubblicata immagine nome della macchina virtuale per l'intera famiglia di immagine selezionata (ad esempio **SQL Server 2016 RTM Enterprise in Windows Server 2012 R2**):

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-hello-virtual-machine"></a>Creare una macchina virtuale hello

Infine, creare macchine virtuali hello con PowerShell:

1. Creare un cloud servizio toohost hello nuova macchina virtuale. Si noti che è anche possibile toouse un servizio cloud esistente. Creare una nuova variabile **$svcname** nome breve di hello del servizio cloud hello.

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. Specificare il nome di macchina virtuale hello e una dimensione. Per altre informazioni sulle dimensioni della macchina virtuale, vedere [Dimensioni delle macchine virtuali in Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see hello link toohello other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. Specificare la password e account di amministratore locale hello.

   ```powershell
   $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. Eseguire hello seguente macchina virtuale di script toocreate hello.

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> Per informazioni aggiuntive e le opzioni di configurazione, vedere hello **compilare il set di comandi** sezione [toocreate usare Azure PowerShell e preconfigurare macchine virtuali basate su Windows](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="example-powershell-script"></a>Script di PowerShell di esempio

Hello script riportato di seguito viene fornito un esempio di uno script completo che consente di creare un **SQL Server 2016 RTM Enterprise in Windows Server 2012 R2** macchina virtuale. Se si usa questo script, è necessario personalizzare le variabili di hello iniziale in base ai passaggi precedenti di hello in questo argomento.

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set hello current subscription and storage account
# Comment out hello New-AzureStorageAccount line if hello account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select hello most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create hello new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create hello VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create hello SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a>Connettersi a Desktop remoto

1. Creare i file RDP hello toolaunch di cartella documenti dell'utente corrente hello il programma di installazione toocomplete queste macchine virtuali:

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. Nella directory documenti hello, avviare il file RDP hello. La connessione con nome utente dell'amministratore hello e la password specificati in precedenza (ad esempio, se il nome utente è stato VMAdmin, specificare "\VMAdmin" come utente hello e fornire la password di hello).

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-hello-configuration-of-hello-sql-server-machine-for-remote-access"></a>Configurazione di hello completo di hello macchina di SQL Server per l'accesso remoto

Dopo l'accesso toohello computer con desktop remoto, configurare SQL Server in base alle istruzioni hello [passaggi per la configurazione della connettività di SQL Server in una macchina virtuale di Azure](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).

## <a name="next-steps"></a>Passaggi successivi

È possibile trovare istruzioni aggiuntive per il provisioning di macchine virtuali con PowerShell in hello [macchine virtuali-documentazione](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

In molti casi, la fase successiva hello è toomigrate toothis il database nuova VM SQL Server. Per istruzioni sulla migrazione di database, vedere [la migrazione di un Server in una macchina virtuale Azure di tooSQL Database](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).

Se inoltre si è interessati all'uso hello toocreate portale Azure macchine virtuali di SQL, vedere [Provisioning di una macchina virtuale di SQL Server in Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md). Si noti che esercitazione hello che tramite il portale di hello crea le macchine virtuali utilizzando percorsi hello modello consigliato di gestione risorse, anziché modello classico di hello utilizzato in questo argomento di PowerShell.

Inoltre le risorse toothese, che è consigliabile consultare [su altri argomenti relativi a SQL Server in macchine virtuali di Azure toorunning](../sql/virtual-machines-windows-sql-server-iaas-overview.md).
