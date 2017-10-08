---
title: estensione dell'agente di controllo di rete della macchina virtuale per Linux aaaAzure | Documenti Microsoft
description: Distribuire hello agente di controllo di rete nella macchina virtuale di Linux mediante un'estensione di macchina virtuale.
services: virtual-machines-linux
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 84bed132cbda83d0917be490f9a50914578952a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a>Estensione macchina virtuale Network Watcher Agent per Linux

## <a name="overview"></a>Panoramica

[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) è un servizio di monitoraggio delle prestazioni di rete, diagnostica e analisi che consente di monitorare le reti di Azure. Hello estensione della macchina virtuale dell'agente di controllo di rete è un requisito per alcune delle funzionalità di hello Watcher di rete in macchine virtuali di Azure. Include l'acquisizione del traffico di rete su richiesta e altre funzionalità avanzate.

Per Linux, hello di dettagli in questo documento supporta piattaforme e le opzioni di distribuzione per hello estensione della macchina virtuale dell'agente di controllo di rete.

## <a name="prerequisites"></a>Prerequisiti

### <a name="operating-system"></a>Sistema operativo

Hello estensione Agent Watcher di rete può essere eseguita su queste distribuzioni Linux:

| Distribuzione | Versione |
|---|---|
| Ubuntu | 16.04 LTS, 14.04 LTS e 12.04 LTS |
| Debian | 7 e 8 |
| RedHat | 6.x e 7.x |
| Oracle Linux | 7x |
| SUSE | 11 e 12 |
| OpenSUSE | 7.0 |
| CentOS | 7.0 |

Si noti che CoreOS non è attualmente supportato.

### <a name="internet-connectivity"></a>Connettività Internet

Alcune delle funzionalità dell'agente di controllo rete hello richiede tale macchina virtuale di destinazione hello connesso toohello Internet. Senza connessioni in uscita di hello possibilità tooestablish alcune delle funzionalità dell'agente di controllo rete hello malfunzionamento o non sono più disponibili. Per ulteriori informazioni, vedere hello [documentazione Watcher di rete](https://review.docs.microsoft.com/en-us/azure/network-watcher/).

## <a name="extension-schema"></a>Schema dell'estensione

Hello JSON seguente mostra lo schema di hello per hello estensione Agent Watcher di rete. estensione di Hello non richiede né supporta le impostazioni fornite dall'utente in questo momento e si basa sulla configurazione predefinita.

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentLinux",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a>Valori delle proprietà

| Nome | Valore/Esempio |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.Azure.NetworkWatcher |
| type | NetworkWatcherAgentLinux |
| typeHandlerVersion | 1.4 |

## <a name="template-deployment"></a>Distribuzione del modello

Le estensioni macchina virtuale di Azure possono essere distribuite con i modelli di Azure Resource Manager. schema JSON Hello descritta in dettaglio nella sezione precedente hello è utilizzabile in un hello toorun modello di gestione risorse di Azure estensione Agent Watcher di rete durante la distribuzione di un modello di gestione risorse di Azure.

## <a name="azure-cli-deployment"></a>Distribuzione dell'interfaccia della riga di comando di Azure

Hello CLI di Azure può essere utilizzato toodeploy hello rete Watcher agente VM estensione tooan macchina virtuale esistente.

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a>Risoluzione dei problemi e supporto

### <a name="troubleshooting"></a>Risoluzione dei problemi

Dati sullo stato di hello delle distribuzioni di estensione possono essere recuperati dal portale di Azure hello e, utilizzando hello CLI di Azure. lo stato di distribuzione hello toosee delle estensioni per una macchina virtuale specificata, eseguire hello seguente comando utilizzando hello CLI di Azure.

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

Esecuzione di estensione di output è toofiles registrati nell'hello seguente directory:

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a>Supporto

Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile consultare la documentazione di toohello Watcher di rete o contattare hello Azure esperti hello [forum MSDN di Azure e di Overflow dello Stack](https://azure.microsoft.com/en-us/support/forums/). In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure. Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/en-us/support/options/) e scegliere supporto tecnico. Per informazioni sull'utilizzo di supporto di Azure, leggere hello [supporto tecnico di Microsoft Azure domande frequenti su](https://azure.microsoft.com/en-us/support/faq/).
