---
title: "aaaVirtual computer estensioni e funzionalità per Linux | Documenti Microsoft"
description: "Informazioni sulle estensioni disponibili per le macchine virtuali di Azure, raggruppate in base a ciò che forniscono o migliorano."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 52f5d0ec-8f75-49e7-9e15-88d46b420e63
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: e0d2ce794c76815ccc6743e8788ee5d9d931e9a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a>Estensioni della macchina virtuale e funzionalità per Linux

Le estensioni della macchina virtuale di Azure sono piccole applicazioni che eseguono attività di configurazione e automazione post-distribuzione sulle macchine virtuali di Azure. Ad esempio, se una macchina virtuale richiede l'installazione del software, protezione antivirus o configurazione di Docker, un'estensione della macchina virtuale può essere utilizzato toocomplete queste attività. Le estensioni VM di Azure possono essere eseguite tramite hello CLI di Azure PowerShell, i modelli, Gestione risorse di Azure e hello portale di Azure. Le estensioni possono essere unite in bundle con una nuova distribuzione di macchina virtuale o eseguite su un sistema esistente.

Questo documento fornisce una panoramica delle estensioni di macchina virtuale, i prerequisiti per l'utilizzo di estensioni di macchina virtuale di Azure e indicazioni su come gestire toodetect e rimuovere estensioni di macchina virtuale. Questo documento fornisce informazioni generali perché sono disponibili molte estensioni della macchina virtuale, ognuna con una configurazione potenzialmente univoca. Dettagli specifici dell'estensione sono disponibili in ogni estensione singoli toohello specifico di documento.

## <a name="use-cases-and-samples"></a>Casi d'uso ed esempi

Sono disponibili numerose estensioni della macchina virtuale di Azure, ognuna con uno specifico caso d'uso. Di seguito sono riportati alcuni esempi:

- Applicare una macchina virtuale tooa configurazioni dello stato desiderato di PowerShell utilizzando hello estensione DSC per Linux. Per altre informazioni, vedere l'argomento relativo all'[Estensione DSC (Desired State Configuration) di Azure](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).
- Configurare il monitoraggio di una macchina virtuale con hello estensione di macchina virtuale di Microsoft Monitoring Agent. Per ulteriori informazioni, vedere [come toomonitor una VM Linux](tutorial-monitoring.md).
- Configurare il monitoraggio dell'infrastruttura di Azure con estensione Datadog hello. Per ulteriori informazioni, vedere hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).
- Configurare un host Docker nella macchina virtuale di Azure utilizzando l'estensione della macchina virtuale Docker hello. Per altre informazioni, vedere [Estensione macchina virtuale per Docker](dockerextension.md).

Inoltre estensioni specifiche di tooprocess, un'estensione Script personalizzato è disponibile per le macchine virtuali Windows e Linux. estensione Script personalizzato per Linux Hello consente qualsiasi toobe script Bash eseguire in una macchina virtuale. Gli script personalizzati sono utili per la progettazione di distribuzioni di Azure che richiedono una configurazione in aggiunta a quella offerta dagli strumenti nativi di Azure. Per altre informazioni, vedere [Estensione di script personalizzata per le VM Linux](extensions-customscript.md).


## <a name="prerequisites"></a>Prerequisiti

Ogni estensione macchina virtuale può avere un insieme specifico di prerequisiti. Ad esempio, hello estensione della macchina virtuale Docker è un prerequisito di una distribuzione di Linux supportata. Requisiti di singole estensioni vengono descritti in dettaglio nella documentazione di hello specifiche dell'estensione.

### <a name="azure-vm-agent"></a>Agente VM di Azure

agente VM di Azure Hello gestisce le interazioni tra una macchina virtuale di Azure e il controller di infrastruttura di Azure hello. agente VM Hello è responsabile per molti aspetti funzionali di distribuzione e gestione di macchine virtuali di Azure, incluse l'esecuzione di estensioni di macchina virtuale. agente VM di Azure Hello è preinstallato in immagini di Azure Marketplace e può essere installato manualmente su sistemi operativi supportati.

Per informazioni sui sistemi operativi supportati e per le istruzioni di installazione, vedere [Agente delle macchine virtuali di Azure](../windows/classic/agents-and-extensions.md).

## <a name="discover-vm-extensions"></a>Individuare le estensioni della macchina virtuale

Molte estensioni delle macchine virtuali di diverso tipo sono disponibili per l'uso con macchine virtuali di Azure. toosee un elenco completo, eseguire hello comando con hello CLI di Azure seguente, sostituendo il percorso di esempio hello con hello nel percorso desiderato.

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a>Eseguire le estensioni della macchina virtuale

Estensioni di macchina virtuale di Azure possono essere eseguite nelle macchine virtuali esistenti, sono utili quando è necessario toomake modifiche di configurazione o ripristinare la connessione in una macchina virtuale già distribuita. Le estensioni della macchina virtuale possono essere anche unite in bundle con le distribuzioni del modello di Azure Resource Manager. L'uso delle estensioni con i modelli di Resource Manager consente di distribuire e configurare le macchine virtuali di Azure senza l'intervento post-distribuzione.

Hello dei seguenti metodi può essere utilizzati toorun un'estensione in una macchina virtuale esistente.

### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

Estensioni di macchina virtuale di Azure possono essere eseguite su una macchina virtuale esistente con hello `az vm extension set` comando. In questo esempio esegue l'estensione script personalizzata hello su una macchina virtuale.

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

Hello script genera output simile toohello seguente testo:

```azurecli
info:    Executing command vm extension set
+ Looking up hello VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a>Portale di Azure

Estensioni di macchina virtuale possono essere applicato tooan macchina virtuale esistente tramite hello portale di Azure. toodo in tal caso, selezionare hello macchina virtuale, scegliere **estensioni**, fare clic su **Aggiungi**. Selezionare l'estensione di hello desiderato dall'elenco di hello delle estensioni disponibili e seguire le istruzioni di hello nella procedura guidata hello.

Hello immagine seguente mostra installazione hello di hello estensione Script personalizzato Linux da hello portale di Azure.

![Installare l'estensione di script personalizzata](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a>Modelli di Gestione risorse di Azure

Estensioni di macchina virtuale possono essere aggiunto tooan modello di gestione risorse di Azure ed eseguita con la distribuzione di hello del modello di hello. Quando si distribuisce un'estensione con un modello, è possibile creare distribuzioni di Azure completamente configurate. Ad esempio, hello che JSON seguente viene eseguita da un modello di gestione risorse. modello Hello distribuisce un insieme di macchine virtuali di bilanciamento del carico e un database SQL di Azure e quindi installa un'applicazione .NET Core su ogni macchina virtuale. estensione della macchina virtuale Hello occupa hello dell'installazione del software.

Per ulteriori informazioni, vedere hello completo [modello di gestione risorse](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
    }
}
```

Per altre informazioni, vedere [Creazione di modelli di Azure Resource Manager](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).

## <a name="secure-vm-extension-data"></a>Proteggere i dati dell'estensione della macchina virtuale

Quando si esegue un'estensione della macchina virtuale, potrebbe essere necessario tooinclude informazioni riservate, ad esempio le credenziali e i nomi degli account di archiviazione chiavi di accesso di account di archiviazione. Molte estensioni VM includono una configurazione protetta, che crittografa i dati e lo decrittografa solo all'interno di hello macchina virtuale di destinazione. Ogni estensione dispone di uno schema di configurazione protetta specifico, descritto in dettaglio nella documentazione specifica dell'estensione.

Hello di esempio seguente mostra un'istanza di hello estensione Script personalizzato per Linux. Si noti che tooexecute comando hello include un set di credenziali. In questo esempio hello comando tooexecute non verrà crittografati.


```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ],
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

Hello mobile **comando tooexecute** proprietà toohello **protetti** configurazione consente di proteggere la stringa di esecuzione hello.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

## <a name="troubleshoot-vm-extensions"></a>Risoluzione dei problemi relativi alle estensioni della macchina virtuale

Ogni estensione della macchina virtuale abbia estensione toohello specifici passaggi di risoluzione dei problemi. Ad esempio, quando si utilizza l'estensione Custom Script hello, dettagli sull'esecuzione di script è reperibile in locale nella macchina virtuale hello in cui è stata eseguita l'estensione hello. Tutti i passaggi per la risoluzione dei problemi specifici dell'estensione sono descritti in dettaglio nella documentazione specifica dell'estensione.

Hello risoluzione dei problemi relativi alla procedura seguente si applica tooall estensioni delle macchine virtuali.

### <a name="view-extension-status"></a>Visualizzare lo stato dell'estensione

Dopo l'esecuzione di un'estensione della macchina virtuale in una macchina virtuale, utilizzare hello seguente lo stato dell'estensione tooreturn comando CLI di Azure. Sostituire i nomi dei parametri di esempio con i valori desiderati.

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

output di Hello è simile hello seguente testo:

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

Lo stato dell'esecuzione di estensione può essere rilevata anche in hello portale di Azure. stato hello tooview di un'estensione, hello selezionare macchina virtuale, scegliere **estensioni**, e selezionare hello estensione desiderata.

### <a name="rerun-a-vm-extension"></a>Rieseguire un'estensione macchina virtuale

Potrebbero essere presenti i casi in cui un'estensione della macchina virtuale deve toobe eseguire di nuovo. È possibile eseguire nuovamente un'estensione rimuovendola e quindi eseguire nuovamente estensione hello con un metodo di esecuzione di propria scelta. tooremove un'estensione, eseguire hello comando con hello CLI di Azure seguente. Sostituire i nomi dei parametri di esempio con i valori desiderati.

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

È possibile rimuovere un'estensione tramite hello in hello portale di Azure come segue:

1. Selezionare una macchina virtuale.
2. Scegliere **Estensioni**.
3. Selezionare l'estensione hello desiderato.
4. Scegliere **Disinstalla**.

## <a name="common-vm-extension-reference"></a>Riferimento alle estensioni della macchina virtuale comuni
| Nome estensione | Descrizione | Altre informazioni |
| --- | --- | --- |
| Estensione script personalizzata per Linux |Eseguire gli script in una macchina virtuale di Azure |[Estensione script personalizzata per Linux](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| Estensione per Docker |Installare hello Docker daemon toosupport comandi Docker remoti. |[Estensione macchina virtuale per Docker](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| Estensione dell'accesso alle macchine virtuali |Ripristinare l'accesso tooan macchina virtuale di Azure |[Estensione dell'accesso alle macchine virtuali](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| Estensione di Diagnostica di Azure |Gestisce Diagnostica di Azure. |[Estensione di Diagnostica di Azure](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| Estensione dell'accesso alla VM di Azure |Gestire gli utenti e le credenziali |[Estensione dell'accesso alla VM per Linux](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
