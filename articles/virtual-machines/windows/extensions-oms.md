---
title: estensione di macchina virtuale di Azure per Windows aaaOMS | Documenti Microsoft
description: Distribuire l'agente OMS hello nella macchina virtuale Windows usando un'estensione della macchina virtuale.
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: feae6176-2373-4034-b5d9-a32c6b4e1f10
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: nepeters
ms.openlocfilehash: 3000f66c0acdec1d1fad2125b8c6b72a92b1ec92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a>Estensione macchina virtuale OMS per Windows

In Operations Management Suite (OMS) sono disponibili funzionalità di monitoraggio, avviso e correzione tramite avvisi in risorse cloud e locali. estensione della macchina virtuale agente OMS per Windows Hello è pubblicato e supportato da Microsoft. estensione Hello installa l'agente OMS hello in macchine virtuali di Azure e registra le macchine virtuali in un'area di lavoro OMS. Opzioni di distribuzione, le configurazioni e piattaforme hello di dettagli in questo documento supportato per l'estensione della macchina virtuale OMS hello per Windows.

## <a name="prerequisites"></a>Prerequisiti

### <a name="operating-system"></a>Sistema operativo
Hello estensione OMS Agent per Windows possono essere eseguite in Windows Server 2008 R2, 2012 e 2012 R2 2016 rilascia.

### <a name="internet-connectivity"></a>Connettività Internet
estensione OMS Agent per Windows Hello richiede tale macchina virtuale di destinazione hello è connesso toohello internet. 

## <a name="extension-schema"></a>Schema dell'estensione

Hello JSON seguente viene illustrato lo schema di hello per hello estensione OMS Agent. estensione Hello richiede hello dell'area di lavoro area di lavoro e l'Id chiave dall'area di lavoro OMS destinazione hello, questi possono essere disponibili nel portale OMS hello. Poiché chiave dell'area di lavoro hello deve essere considerate come dati sensibili, devono essere archiviato in una configurazione di impostazione protetto. Dati impostazione protette dell'estensione di macchina virtuale di Azure sono crittografati e decrittografati solo nella macchina virtuale di destinazione hello. Tenere presente che **workspaceId** e **workspaceKey** distinguono tra maiuscole e minuscole.

```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```
### <a name="property-values"></a>Valori delle proprietà

| Nome | Valore/Esempio |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.EnterpriseCloud.Monitoring |
| type | MicrosoftMonitoringAgent |
| typeHandlerVersion | 1.0 |
| workspaceId (esempio) | 6f680a37-00c6-41c7-a93f-1437e3462574 |
| workspaceKey (esempio) | z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ== |

## <a name="template-deployment"></a>Distribuzione del modello

Le estensioni macchina virtuale di Azure possono essere distribuite con i modelli di Azure Resource Manager. schema JSON Hello descritta in dettaglio nella sezione precedente hello è utilizzabile in un hello toorun modello di gestione risorse di Azure estensione OMS Agent durante la distribuzione di un modello di gestione risorse di Azure. Un modello di esempio che include l'estensione della macchina virtuale di agente OMS hello è reperibile in hello [raccolta avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm). 

Hello JSON per un'estensione della macchina virtuale può essere annidata all'interno di risorsa di macchina virtuale hello o posizionato nella radice di hello o un livello superiore di un modello di gestione risorse di JSON. posizionamento di Hello di hello JSON influisce sul valore di hello del nome della risorsa hello e tipo. Per altre informazioni, vedere [Set name and type for child resources](../../azure-resource-manager/resource-manager-template-child-resource.md) (Impostare il nome e il tipo per le risorse figlio). 

Hello seguente si presuppone hello OMS estensione annidata all'interno di hello risorsa di macchina virtuale. Quando la nidificazione di risorse di estensione hello, hello JSON viene inserito nel hello `"resources": []` oggetto della macchina virtuale hello.


```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

Quando si inseriscono estensione hello JSON nella radice di hello del modello di hello, il nome di risorsa hello include una macchina virtuale di riferimento toohello padre e il tipo hello riflette configurazione annidati hello. 

```json
{
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "name": "<parentVmResource>/OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

## <a name="powershell-deployment"></a>Distribuzione PowerShell

Hello `Set-AzureRmVMExtension` comando può essere utilizzato toodeploy hello agente OMS macchina virtuale estensione tooan macchina virtuale esistente. Prima di eseguire il comando hello, configurazioni di hello pubbliche e private necessario toobe archiviati in una tabella hash di PowerShell. 

```powershell
$PublicSettings = @{"workspaceId" = "myWorkspaceId"}
$ProtectedSettings = @{"workspaceKey" = "myWorkspaceKey"}

Set-AzureRmVMExtension -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
    -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" `
    -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
    -ExtensionType "MicrosoftMonitoringAgent" `
    -TypeHandlerVersion 1.0 `
    -Settings $PublicSettings `
    -ProtectedSettings $ProtectedSettings `
    -Location WestUS ` 
```

## <a name="troubleshoot-and-support"></a>Risoluzione dei problemi e supporto

### <a name="troubleshoot"></a>Risoluzione dei problemi

Dati sullo stato di hello delle distribuzioni di estensione possono essere recuperati dal portale di Azure hello e, utilizzando il modulo di Azure PowerShell hello. lo stato di distribuzione hello toosee delle estensioni per una macchina virtuale specificata, hello esecuzione seguente comando utilizzando hello modulo Azure PowerShell.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Esecuzione di estensione di output è toofiles registrati nell'hello seguente directory:

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a>Supporto

Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti hello [forum MSDN di Azure e di Overflow dello Stack](https://azure.microsoft.com/en-us/support/forums/). In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure. Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/en-us/support/options/) e scegliere supporto tecnico. Per informazioni sull'utilizzo di supporto di Azure, leggere hello [supporto tecnico di Microsoft Azure domande frequenti su](https://azure.microsoft.com/en-us/support/faq/).
