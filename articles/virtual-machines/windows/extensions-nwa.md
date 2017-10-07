---
title: estensione della macchina virtuale dell'agente di controllo di rete per Windows aaaAzure | Documenti Microsoft
description: Distribuire hello agente di controllo di rete nella macchina virtuale Windows usando un'estensione della macchina virtuale.
services: virtual-machines-windows
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 27e46af7-2150-45e8-b084-ba33de8c5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 21298706e462ff32c4d314f9a1ad127074ddf481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a>Estensione macchina virtuale agente Network Watcher per Windows

## <a name="overview"></a>Panoramica

[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) è un servizio di monitoraggio delle prestazioni di rete, diagnostica e analisi che consente di monitorare le reti di Azure. Hello estensione della macchina virtuale dell'agente di controllo di rete è un requisito per alcune delle funzionalità di hello Watcher di rete in macchine virtuali di Azure. Include l'acquisizione del traffico di rete su richiesta e altre funzionalità avanzate.

Questo hello dettagli di documento supportato piattaforme e le opzioni di distribuzione per hello estensione della macchina virtuale dell'agente di controllo di rete per Windows.

## <a name="prerequisites"></a>Prerequisiti

### <a name="operating-system"></a>Sistema operativo

Hello estensione rete Watcher agente per Windows possono essere eseguite in Windows Server 2008 R2, 2012 e 2012 R2 2016 rilascia. Si noti che hello Nano Server non sono supportato in questo momento.

### <a name="internet-connectivity"></a>Connettività Internet

Alcune delle funzionalità dell'agente di controllo rete hello richiede tale macchina virtuale di destinazione hello connesso toohello Internet. Senza connessioni in uscita di hello possibilità tooestablish alcune delle funzionalità dell'agente di controllo rete hello malfunzionamento o non sono più disponibili. Per ulteriori informazioni, vedere hello [documentazione Watcher di rete](../../network-watcher/network-watcher-monitoring-overview.md).

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
        "type": "NetworkWatcherAgentWindows",
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
| type | NetworkWatcherAgentWindows |
| typeHandlerVersion | 1.4 |


## <a name="template-deployment"></a>Distribuzione del modello

Le estensioni macchina virtuale di Azure possono essere distribuite con i modelli di Azure Resource Manager. schema JSON Hello descritta in dettaglio nella sezione precedente hello è utilizzabile in un hello toorun modello di gestione risorse di Azure estensione Agent Watcher di rete durante la distribuzione di un modello di gestione risorse di Azure.

## <a name="powershell-deployment"></a>Distribuzione PowerShell

Hello `Set-AzureRmVMExtension` comando può essere utilizzato toodeploy hello agente di controllo di rete macchina virtuale estensione tooan macchina virtuale esistente.

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a>Risoluzione dei problemi e supporto

### <a name="troubleshooting"></a>Risoluzione dei problemi

Dati sullo stato di hello delle distribuzioni di estensione possono essere recuperati dal portale di Azure hello e, utilizzando il modulo di Azure PowerShell hello. lo stato di distribuzione hello toosee delle estensioni per una macchina virtuale specificata, hello esecuzione seguente comando utilizzando hello modulo Azure PowerShell.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

Esecuzione di estensione di output è toofiles registrati nell'hello seguente directory:

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a>Supporto

Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile consultare la documentazione di toohello Guida utente Watcher di rete o contattare hello Azure esperti hello [forum MSDN di Azure e di Overflow dello Stack](https://azure.microsoft.com/en-us/support/forums/). In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure. Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/en-us/support/options/) e scegliere supporto tecnico. Per informazioni sull'utilizzo di supporto di Azure, leggere hello [supporto tecnico di Microsoft Azure domande frequenti su](https://azure.microsoft.com/en-us/support/faq/).
