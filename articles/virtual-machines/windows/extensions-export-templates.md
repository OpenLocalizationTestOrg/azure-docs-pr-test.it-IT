---
title: Gruppi di risorse di Azure che contiene le estensioni VM aaaExporting | Documenti Microsoft
description: Esportare modelli di Resource Manager che includono estensioni macchina virtuale.
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7f4e2ca6-f1c7-4f59-a2cc-8f63132de279
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: nepeters
ms.openlocfilehash: cdbc2030988a19fe68429e8733dc60536c264abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a>Esportazione di gruppi di risorse contenenti estensioni macchina virtuale

I gruppi di risorse di Azure possono essere esportati in un nuovo modello di Resource Manager ridistribuibile. Hello processo di esportazione interpreta le risorse esistenti e crea un modello di gestione risorse che, quando distribuito comporta un gruppo di risorse simili. Quando si utilizza l'opzione di esportazione hello gruppo di risorse rispetto a un gruppo di risorse contenente le estensioni di macchina virtuale, diversi elementi necessità toobe considerato, ad esempio compatibilità dell'estensione e protetti delle impostazioni.

Questo documento illustra il funzionamento hello il processo di esportazione di gruppo di risorse relative estensioni di macchine virtuali, incluso un elenco di estensioni supportate e i dettagli sulla gestione di dati protetti.

## <a name="supported-virtual-machine-extensions"></a>Estensioni macchina virtuale supportate

Sono disponibili molte estensioni macchina virtuale. Non tutte le estensioni possono essere esportate in un modello di gestione risorse utilizzo funzionalità "Script di automazione" hello. Se un'estensione della macchina virtuale non è supportata, è necessario toobe manualmente inserito nel modello esportato hello.

Hello estensioni seguenti possono essere esportate con funzionalità di script di automazione hello.

| Estensione ||||
|---|---|---|---|
| Acronis Backup | Datadog Windows Agent | OS Patching For Linux | VM Snapshot Linux
| Acronis Backup Linux | Estensione Docker | Puppet Agent |
| BGInfo | DSC Extension | Site 24x7 Apm Insight |
| BMC CTM Agent Linux | Dynatrace Linux | Site 24x7 Linux Server |
| BMC CTM Agent Windows | Dynatrace Windows | Site 24x7 Windows Server |
| Chef Client | HPE Security Application Defender | Trend Micro DSA |
| Custom Script | IaaS Antimalware | Trend Micro DSA Linux |
| Estensione di script personalizzati | IaaS Diagnostics | VM Access For Linux |
| Custom Script for Linux | Linux Chef Client | VM Access For Linux |
| Datadog Linux Agent | Linux Diagnostic | VM Snapshot |

## <a name="export-hello-resource-group"></a>Esportazione hello gruppo di risorse

tooexport un gruppo di risorse in un modello riutilizzabile, hello completo alla procedura seguente:

1. Accedi toohello portale di Azure
2. Nel Menu Hub hello, fare clic su gruppi di risorse
3. Selezionare il gruppo di risorse di hello destinazione dall'elenco di hello
4. Nel Pannello di hello gruppo di risorse, fare clic su Script di automazione

![Esportazione del modello](./media/extensions-export-templates/template-export.png)

Hello script dall'automazione di Azure Resource Manager genera un modello di gestione delle risorse e un file di parametri diversi esempi di script di distribuzione, ad esempio PowerShell e CLI di Azure. A questo punto, può essere scaricato modello esportato hello mediante il pulsante download hello, aggiunto come una libreria di modelli toohello modello nuovo o ridistribuito utilizzando hello pulsante di distribuzione.

## <a name="configure-protected-settings"></a>Configurare le impostazioni protette

Molte estensioni macchina virtuale di Azure includono una configurazione di impostazioni protette, che crittografa i dati sensibili come credenziali e stringhe di configurazione. Impostazioni protette non vengono esportate con script di automazione hello. Se le impostazioni necessarie, protette necessario toobe reinserito hello esportata basati su modelli.

### <a name="step-1---remove-template-parameter"></a>Passaggio 1 - Rimuovere il parametro del modello

Creazione di hello al che gruppo di risorse viene esportato, un parametro singolo modello tooprovide toohello un valore esportato impostazioni protette. Questo parametro può essere rimosso. parametro hello tooremove, esaminare l'elenco di parametri hello ed eliminare il parametro hello che controlla l'esempio JSON toothis simile.

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a>Passaggio 2 - Proteggere le proprietà delle impostazioni

Poiché ciascuna impostazione protetto ha un set di proprietà necessarie, un elenco di queste proprietà necessario toobe raccolte. È possibile trovare ogni parametro di configurazione delle impostazioni protette hello in hello [dello schema di gestione risorse di Azure su GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json). Questo schema include solo il set di parametri hello per le estensioni di hello elencati nella sezione Panoramica hello di questo documento. 

All'interno del repository di schema hello, cercare estensione hello desiderato, in questo esempio `IaaSDiagnostics`. Una volta hello estensioni `protectedSettings` oggetto è stato trovato, prendere nota di ogni parametro. Nell'esempio hello di hello `IaasDiagnostic` estensione, hello richiedono parametri sono `storageAccountName`, `storageAccountKey`, e `storageAccountEndPoint`.

```json
"protectedSettings": {
    "type": "object",
    "properties": {
        "storageAccountName": {
            "type": "string"
        },
        "storageAccountKey": {
            "type": "string"
        },
        "storageAccountEndPoint": {
            "type": "string"
        }
    },
    "required": [
        "storageAccountName",
        "storageAccountKey",
        "storageAccountEndPoint"
    ]
}
```

### <a name="step-3---re-create-hello-protected-configuration"></a>Passaggio 3: creare nuovamente configurazione hello protetto

Il modello esportato di hello, cercare `protectedSettings` e sostituire hello esportata protetto l'impostazione dell'oggetto con una nuova istanza che include i parametri di estensione hello necessarie e un valore per ciascuna di esse.

Nell'esempio hello di hello `IaasDiagnostic` estensione, nuova configurazione di impostazione protetto hello avrà un aspetto analogo hello di esempio seguente:

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

risorse di estensione finale Hello sono simile toohello esempio JSON seguente:

```json
{
    "name": "Microsoft.Insights.VMDiagnosticsSettings",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "[variables('apiVersion')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "tags": {
        "displayName": "AzureDiagnostics"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]",
            "storageAccountEndPoint": "https://core.windows.net"
        }
    }
}
```

Se si utilizza i valori delle proprietà tooprovide modello parametri, questi devono toobe creato. Durante la creazione di parametri di modello per protetto impostazione dei valori, assicurarsi che hello toouse `SecureString` tipo di parametro in modo che i valori sensibili vengono protetti. Per altre informazioni sull'utilizzo dei parametri, vedere [Creazione di modelli di Azure Resource Manager](../../resource-group-authoring-templates.md).

Nell'esempio hello di hello `IaasDiagnostic` estensione, verrebbe creato nella sezione parametri hello del modello di gestione risorse di hello hello seguenti parametri.

```json
"storageAccountName": {
    "defaultValue": null,
    "type": "SecureString"
},
"storageAccountKey": {
    "defaultValue": null,
    "type": "SecureString"
}
```

A questo punto, il modello di hello può essere distribuito utilizzando qualsiasi metodo di distribuzione del modello.
