---
title: "Imposta aaaDeploy un'app su scalabilità della macchina virtuale"
description: "Utilizzare le estensioni toodepoy un'app nel set di scalabilità di macchine virtuali di Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8892199-f2e2-4b82-988a-28ca8a7fd1eb
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: 5f3988b9511d80370a8be1fc042c21fee212506e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a>Distribuire l'applicazione nei set di scalabilità delle macchine virtuali

In questo articolo descrive diversi modi di impostazione software tooinstall hello hello scala viene eseguito il provisioning.

È opportuno hello tooreview [Panoramica sulla progettazione di Set di scalabilità](virtual-machine-scale-sets-design-overview.md) articolo vengono descritti alcuni dei limiti di hello imposti dal set di scalabilità di macchine virtuali.

## <a name="capture-and-reuse-an-image"></a>Acquisire e riusare un'immagine

È possibile utilizzare una macchina virtuale che in Azure tooprepare un'immagine di base per la scala impostate. Questo processo crea un disco gestito nell'account di archiviazione, è possibile fare riferimento come immagine di base hello per il set di scalabilità. 

Hello i passaggi seguenti:

1. Creare una macchina virtuale di Azure
   * [Linux][linux-vm-create]
   * [Windows][windows-vm-create]

2. Remoto in hello macchina virtuale e personalizzare desiderato di tooyour sistema hello.

   Se lo si desidera, a questo punto è possibile installare l'applicazione. Può tuttavia sapere che con l'installazione dell'applicazione a questo punto, è possibile effettuare l'aggiornamento, l'applicazione più complessa poiché potrebbe essere necessario tooremove il primo. In alternativa, è possibile utilizzare tooinstall questo passaggio gli eventuali prerequisiti che dell'applicazione potrebbe essere necessario, ad esempio una funzionalità di runtime o del sistema operativo specifica.

3. Seguire l'esercitazione "acquisire una macchina" hello per uno [Linux] [ linux-vm-capture] o [Windows][windows-vm-capture].

4. Creare un [Set di scalabilità della macchina virtuale] [ vmss-create] con hello immagine acquisita nel passaggio precedente hello URI.

Per altre informazioni sui dischi, vedere [Panoramica di Managed Disks](../virtual-machines/windows/managed-disks-overview.md) e [Usare dischi dati collegati](virtual-machine-scale-sets-attached-disks.md).

## <a name="install-when-hello-scale-set-is-provisioned"></a>Installare quando viene eseguito il provisioning di set di scalabilità hello

Le estensioni di macchina virtuale possono essere applicato tooa set di scalabilità della macchina virtuale. Con un'estensione della macchina virtuale, è possibile personalizzare hello le macchine virtuali in un set come un intero gruppo di scalabilità. Per altre informazioni sulle estensioni, vedere [Estensioni della macchina virtuale](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

È possibile usare tre principali estensioni, a seconda che il sistema operativo si basi su Windows o Linux.

### <a name="windows"></a>Windows

Per un sistema operativo basato su Windows, utilizzare uno hello **v 1.8 Custom Script** estensione o hello **PowerShell DSC** estensione.

#### <a name="custom-script"></a>Custom Script

estensione Script personalizzata Hello esegue uno script in ogni istanza di macchina virtuale nel set di scalabilità hello. Un file di configurazione o una variabile indica quali file sono macchina virtuale toohello scaricato, quindi viene eseguito il comando. È possibile utilizzare ad esempio un programma di installazione questo toorun, uno script, un file batch, qualsiasi file eseguibile.

PowerShell utilizza una tabella hash per le impostazioni di hello. In questo esempio Configura toorun di estensione script personalizzata hello uno script di PowerShell che consente di installare IIS.

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
>Hello utilizzare `-ProtectedSetting` passare per tutte le impostazioni che potrebbero contenere informazioni riservate.

---------


CLI di Azure Usa un file json per le impostazioni di hello. In questo esempio Configura toorun di estensione script personalizzata hello uno script di PowerShell che consente di installare IIS. Salvare i seguenti file json come hello _Settings_.

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

Quindi, eseguire questo comando dell'interfaccia della riga di comando di Azure.

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Hello utilizzare `--protected-settings` passare per tutte le impostazioni che potrebbero contenere informazioni riservate.

### <a name="powershell-dsc"></a>PowerShell DSC

È possibile utilizzare le istanze di macchina virtuale di PowerShell DSC toocustomize hello scala set. Hello **DSC** estensione pubblicato da **PowerShell** distribuisce ed esegue configurazione DSC hello fornito in ogni istanza di macchina virtuale. Estensione hello indica a un file di configurazione o una variabile in cui *zip* pacchetto è e quali _funzione di script_ toorun combinazione.

PowerShell utilizza una tabella hash per le impostazioni di hello. Questo esempio distribuisce un pacchetto DSC che consente di installare IIS.

```powershell
# Setup extension configuration hashtable variable
$dscConfig = @{
  "wmfVersion" = "latest";
  "configuration" = @{
    "url" = "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip";
    "script" = "configure-http.ps1";
    "function" = "WebsiteTest";
  };
}

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
>Hello utilizzare `-ProtectedSetting` passare per tutte le impostazioni che potrebbero contenere informazioni riservate.

-----------

CLI di Azure Usa un formato json per le impostazioni di hello. Questo esempio distribuisce un pacchetto DSC che consente di installare IIS. Salvare i seguenti file json come hello _Settings_.

```json
{
  "wmfVersion": "latest",
  "configuration": {
    "url": "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip",
    "script": "configure-http.ps1",
    "function": "WebsiteTest"
  }
}
```

Quindi, eseguire questo comando dell'interfaccia della riga di comando di Azure.

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Hello utilizzare `--protected-settings` passare per tutte le impostazioni che potrebbero contenere informazioni riservate.

### <a name="linux"></a>Linux

Linux è possibile utilizzare entrambi hello **v 2.0 Custom Script** estensione oppure utilizzare **cloud init** durante la creazione.

Script personalizzato è un'estensione semplice che scarica istanze di macchine virtuali di file toohello ed esegue un comando.

#### <a name="custom-script"></a>Custom Script

Salvare i seguenti file json come hello _Settings_.

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

Utilizzare hello Azure CLI tooadd tooan questa estensione set di scalabilità della macchina virtuale esistente. Ogni macchina virtuale in scala di hello impostate automaticamente estensione hello viene eseguito.

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
>Hello utilizzare `--protected-settings` passare per tutte le impostazioni che potrebbero contenere informazioni riservate.

#### <a name="cloud-init"></a>cloud-init

Cloud-inizializzazione viene utilizzato quando viene creato il set di scalabilità di hello. Innanzitutto, creare un file locale denominato _cloud init.txt_ e aggiungere il tooit di configurazione. Ad esempio, vedere [questo gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)

Imposta hello utilizzare Azure CLI toocreate una scala. Hello `--custom-data` campo accetta il nome file hello di uno script di inizializzazione di cloud.

```azurecli
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image Canonical:UbuntuServer:14.04.4-LTS:latest \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

## <a name="how-do-i-manage-application-updates"></a>Gestione degli aggiornamenti dell'applicazione

Se è stata distribuita l'applicazione tramite un'estensione, è possibile modificare la definizione di estensione hello in qualche modo. Questa modifica impedisce a istanze di macchine virtuali tooall hello estensione toobe ridistribuita. Un elemento **deve** modificato sull'estensione hello, ad esempio la ridenominazione di un file di cui viene fatto riferimento, in caso contrario, Azure fa non vedere che hello estensione è stata modificata.

Se si baked applicazione hello nella propria immagine del sistema operativo, è possibile utilizzare una pipeline di distribuzione automatica degli aggiornamenti dell'applicazione. Progettare il toofacilitate architettura rapido la sostituzione di una scala di gestione temporanea impostata nell'ambiente di produzione. Un buon esempio di questo approccio è hello [lavoro driver Azure Spinnaker](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).

[Chi](https://www.packer.io/) e [Terraform](https://www.terraform.io/) supporto Azure Resource Manager, pertanto è possibile anche definire le immagini "come"codice e compilarle in Azure, quindi utilizzare hello disco rigido virtuale nel set di scalabilità. Tuttavia, tale approccio diventerebbe problematico per le immagini Marketplace, in cui gli script personalizzati/le estensioni acquistano importanza in quanto i bit non vengono modificati direttamente da Marketplace.

## <a name="what-happens-when-a-scale-set-scales-out"></a>Cosa accade in caso di aumento della capacità di un set di scalabilità
Quando si aggiunge uno o più set di scalabilità di tooa macchine virtuali, un'applicazione hello viene installata automaticamente. Per esempio se il set di scalabilità hello include le estensioni definite, eseguono in una nuova macchina virtuale ogni volta che viene creato. Se il set di scalabilità di hello è basato su un'immagine personalizzata, qualsiasi nuova macchina virtuale è una copia dell'immagine di hello origine personalizzata. Se le macchine virtuali di set di scalabilità di hello host contenitore, avere contenitori hello tooload codice di avvio in un'estensione Script personalizzata. In alternativa, un'estensione potrebbe installare un agente che esegue la registrazione con un agente di orchestrazione del cluster, ad esempio il servizio contenitore di Azure.


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a>Come distribuire un aggiornamento del sistema operativo nei domini di aggiornamento
Si supponga di che voler tooupdate l'immagine del sistema operativo mantenendo scalabilità della macchina virtuale hello impostata in esecuzione. PowerShell e hello CLI di Azure è possibile aggiornare le immagini di macchina virtuale hello, una macchina virtuale alla volta. Hello [aggiornare un Set di scalabilità della macchina virtuale](./virtual-machine-scale-sets-upgrade-scale-set.md) articolo inoltre fornisce ulteriori informazioni su quali opzioni sono disponibili tooperform l'aggiornamento di un sistema operativo in un set di scalabilità della macchina virtuale.

## <a name="next-steps"></a>Passaggi successivi

* [Utilizzare PowerShell toomanage il set di scalabilità.](virtual-machine-scale-sets-windows-manage.md)
* [Creare un modello del set di scalabilità.](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

