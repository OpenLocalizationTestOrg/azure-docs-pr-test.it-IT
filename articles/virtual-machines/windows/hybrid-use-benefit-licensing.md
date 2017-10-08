---
title: aaaAzure vantaggio di utilizzare ibrida per Windows Server e Client Windows | Documenti Microsoft
description: Informazioni su come toomaximize il toobring vantaggi Windows Software Assurance locale tooAzure le licenze
services: virtual-machines-windows
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 332583b6-15a3-4efb-80c3-9082587828b0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 5/26/2017
ms.author: xujing
ms.openlocfilehash: f24487320a60132aaf766a31f3e6f3726d4a3bd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a>Azure Hybrid Use Benefit per Windows Server e Client Windows
Per i clienti con Software Assurance, vantaggio di utilizzare ibrida di Azure consente toouse le licenze di Windows Server e Client di Windows locale e l'esecuzione macchine virtuali di Windows in Azure a un costo ridotto. Azure Hybrid Use Benefit per Windows Server include Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2 e Windows Server 2016. Azure Hybrid Use Benefit per Client Windows include Windows 10. Per ulteriori informazioni, vedere hello [pagina di gestione delle licenze vantaggio di utilizzare Azure ibrida](https://azure.microsoft.com/pricing/hybrid-use-benefit/).

>[!IMPORTANT]
>Azure ibrida utilizzare vantaggi per Client Windows è attualmente in anteprima utilizzando l'immagine di Windows 10 hello in hello Azure Marketplace. Solo i clienti Enterprise con Windows 10 Enterprise E3/E5 per utente o Windows VDA per utente (licenze di sottoscrizione utente o le licenze di sottoscrizione utente per i componenti aggiuntivi) idonei ("Licenze di qualificazione") sono idonei.
>
>

## <a name="ways-toouse-azure-hybrid-use-benefit"></a>Modi toouse vantaggio di utilizzare ibrida di Azure
Esistono un paio di modi toodeploy macchine virtuali di Windows con hello vantaggio di utilizzare ibrida di Azure:

1. È possibile distribuire le macchine virtuali da [immagini specifiche del Marketplace](#deploy-a-vm-using-the-azure-marketplace) preconfigurate con Azure Hybrid Use Benefit: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008SP1.
2. È possibile [caricare una macchina virtuale personalizzata](#upload-a-windows-vhd) e [distribuirla usando un modello di Resource Manager](#deploy-a-vm-via-resource-manager) o [Azure PowerShell](#detailed-powershell-deployment-walkthrough).

## <a name="deploy-a-vm-using-hello-azure-marketplace"></a>Distribuire una macchina virtuale utilizzando hello Azure Marketplace
Le immagini seguenti sono disponibili in hello preconfigurata con vantaggio di utilizzare ibrida di Azure Marketplace: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008SP1. Queste immagini possono essere distribuite direttamente dal portale di Azure hello, modelli di gestione risorse o Azure PowerShell.

È possibile distribuire queste immagini direttamente dal portale di Azure hello. Per l'utilizzo in modelli di gestione risorse e con Azure PowerShell, visualizzare elenco hello delle immagini come segue:

Per Windows Server:
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- 2016-Datacenter versione 2016.127.20170406 o versione successiva

- 2012-R2-Datacenter versione 4.127.20170406 o versione successiva

- 2012-Datacenter versione 3.127.20170406 o versione successiva

- 2008 R2-SP1 versione 2.127.20170406 o versione successiva

Per Client Windows:
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a>Caricare un disco rigido virtuale di Windows Server
toodeploy una VM di Windows Server in Azure, è innanzitutto necessario toocreate un disco rigido virtuale che contiene la build di Windows di base. Questo disco rigido virtuale è necessario preparare adeguatamente tramite Sysprep prima di caricarla tooAzure. È possibile [altre informazioni sui requisiti di disco rigido virtuale hello e processo Sysprep](upload-generalized-managed.md) e [supporto Sysprep per i ruoli Server](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles). Eseguire il backup hello VM prima di eseguire Sysprep. 

Assicurarsi di avere [installato e configurato in hello più recente di Azure PowerShell](/powershell/azure/overview). Dopo aver preparato il disco rigido virtuale, caricare hello VHD tooyour account di archiviazione Azure tramite hello `Add-AzureRmVhd` cmdlet come segue:

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> Microsoft SQL Server, SharePoint Server e Dynamics possono usare anche le licenza di Software Assurance. Immagine di Windows Server tooprepare hello è comunque necessario installare i componenti dell'applicazione e fornendo di conseguenza le chiavi di licenza, quindi caricare tooAzure di immagine disco hello. Esaminare hello documentazione appropriata per l'esecuzione di Sysprep con l'applicazione, ad esempio [considerazioni per l'installazione di SQL Server tramite Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) o [compilare un'immagine di riferimento di SharePoint Server 2016 (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).
>
>

È inoltre possibile leggere informazioni sui [hello VHD tooAzure processo di caricamento](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)


## <a name="deploy-a-vm-via-resource-manager-template"></a>Distribuire una macchina virtuale con il modello di Resource Manager
Nei modelli di Resource Manager è possibile specificare un parametro aggiuntivo per `licenseType`. Altre informazioni sulla [creazione di modelli di Azure Resource Manager](../../resource-group-authoring-templates.md). Dopo aver creato il disco rigido virtuale caricato di tooAzure, modificare è tipo di licenza di gestione risorse modello tooinclude hello come parte di hello provider di calcolo e distribuire il modello come di consueto:

Per Windows Server:
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

Per solo toouse di Client Windows con un'immagine del Marketplace Azure:
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a>Distribuire una macchina virtuale con l'avvio rapido di PowerShell
Quando si distribuisce la macchina virtuale Windows Server con PowerShell è presente un parametro aggiuntivo per `-LicenseType`. Dopo aver creato il disco rigido virtuale caricato di tooAzure, creare una macchina virtuale utilizzando `New-AzureRmVM` e specificare tipo di licenza hello come segue:

Per Windows Server:
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

Per solo toouse di Client Windows con un'immagine del Marketplace Azure:
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

È possibile [leggere una descrizione più dettagliata sulla distribuzione di una macchina virtuale in Azure tramite PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) seguente o lettura una Guida più descrittiva in hello diversi passaggi troppo[creare una macchina virtuale Windows usando Gestione risorse e PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


## <a name="verify-your-vm-is-utilizing-hello-licensing-benefit"></a>Verificare che la macchina virtuale utilizza vantaggio licenze hello
Dopo avere distribuito la macchina virtuale mediante PowerShell hello o il metodo di distribuzione di gestione delle risorse, verificare il tipo di licenza hello con `Get-AzureRmVM` come indicato di seguito:

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

Hello l'output è simile toohello seguente esempio per Windows Server:

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

Questo output è in contrasto con hello che seguente macchina virtuale distribuita senza licenze vantaggio di utilizzare ibrida di Azure, ad esempio una macchina virtuale distribuita direttamente dalla raccolta di Azure hello:

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a>Procedura dettagliata per la distribuzione con PowerShell
esempio Hello dettagliate Mostra i passaggi di PowerShell di una distribuzione completa di una macchina virtuale. È possibile leggere ulteriori informazioni di contesto come toohello effettivo cmdlet e i diversi componenti viene creati [creare una macchina virtuale Windows usando Gestione risorse e PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Verranno creati il gruppo di risorse, l'account di archiviazione e la rete virtuale, quindi verrà definita e creata la VM.

Ottenere prima le credenziali in modo sicuro, specificare una località e definire un nome per il gruppo di risorse:

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

Creare un IP pubblico:

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

Definire la subnet, la scheda di interfaccia di rete e la rete virtuale:

```powershell
$subnetName = "mySubnet"
$nicName = "myNIC"
$vnetName = "myVnet"
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/8
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location `
    -AddressPrefix 10.0.0.0/8 -Subnet $subnetconfig
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroupName -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $publicIP.Id
```

Assegnare un nome alla macchina virtuale e creare una configurazione:

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

Definire il sistema operativo:

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

Aggiungere il toohello NIC VM:

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

Definire toouse account di archiviazione hello:

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

Caricare il disco rigido virtuale, adeguatamente preparato e collegare tooyour macchina virtuale per l'utilizzo:

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

Infine, creare la macchina virtuale e definire hello licenze tipo tooutilize vantaggio di utilizzare ibrida di Azure:

Per Windows Server:
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a>Distribuire un set di scalabilità di macchine virtuali tramite un modello di Resource Manager
Nei modelli di Resource Manager del set di scalabilità di macchine virtuali è necessario specificare un parametro aggiuntivo per `licenseType`. Altre informazioni sulla [creazione di modelli di Azure Resource Manager](../../resource-group-authoring-templates.md). Modificare la proprietà di gestione risorse modello tooinclude hello licenseType come parte di virtualMachineProfile del set di scalabilità di hello e distribuire il modello come di consueto: vedere l'esempio seguente utilizzando l'immagine di Windows Server 2016:


```json
"virtualMachineProfile": {
    "storageProfile": {
        "osDisk": {
            "createOption": "FromImage"
        },
        "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2016-Datacenter",
            "version": "latest"
        }
    },
    "licenseType": "Windows_Server",
    "osProfile": {
            "computerNamePrefix": "[parameters('vmssName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
    }
```

> [!NOTE]
> Il supporto per la distribuzione di un set di scalabilità di macchine virtuali con vantaggi AHUB tramite PowerShell e altri strumenti SDK sarà presto disponibile.
>

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni sul [Vantaggio Microsoft Azure Hybrid Use](https://azure.microsoft.com/pricing/hybrid-use-benefit/).

Altre informazioni sull' [uso dei modelli di Resource Manager](../../azure-resource-manager/resource-group-overview.md).

Altre informazioni, vedere [vantaggio di utilizzare ibrida di Azure e Azure Site Recovery rendere ancora più economica tooAzure la migrazione di applicazioni](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).
