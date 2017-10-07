---
title: aaaAzure Custom Script di estensione per Windows | Documenti Microsoft
description: "Automatizzare le attività di configurazione macchina virtuale di Windows con l'estensione Custom Script hello"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f4181fee-7a9d-4a1c-b517-52956f5b7fa1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/16/2017
ms.author: nepeters
ms.openlocfilehash: 97e065242e9fed116ee20b074f4e302a0cd10585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows"></a>Estensione Script personalizzato per Windows

Estensione dello Script personalizzata Hello Scarica ed esegue gli script in macchine virtuali di Azure. Questa estensione è utile per la configurazione post-distribuzione, l'installazione di software o qualsiasi altra attività di configurazione o gestione. Gli script possono essere scaricati da GitHub o di archiviazione di Azure o forniti toohello portale di Azure in fase di esecuzione di estensione. estensione Script personalizzata Hello si integra con i modelli di gestione risorse di Azure e può essere eseguito anche tramite hello Azure CLI, PowerShell, il portale di Azure o hello API REST di macchina virtuale di Azure.

Questo documento illustra in dettaglio come toouse hello estensione Script personalizzata utilizzando hello modulo Azure PowerShell, i modelli di gestione risorse di Azure e i dettagli di risoluzione dei problemi in sistemi Windows.

## <a name="prerequisites"></a>Prerequisiti

### <a name="operating-system"></a>Sistema operativo

Estensione dello Script personalizzata Hello per Windows possono essere eseguite in Windows Server 2008 R2, 2012 e 2012 R2 2016 rilascia.

### <a name="script-location"></a>Percorso dello script

script di Hello deve toobe archiviati in archiviazione Blob di Azure o qualsiasi altro percorso accessibile tramite un URL valido.

### <a name="internet-connectivity"></a>Connettività Internet

Hello Custom Script di estensione per Windows richiede tale macchina virtuale di destinazione hello è connesso toohello internet. 

## <a name="extension-schema"></a>Schema dell'estensione

Hello JSON seguente viene illustrato lo schema di hello per hello estensione Script personalizzata. estensione di Hello richiede un percorso di script (archiviazione di Azure o in altre posizioni di URL valido) e tooexecute un comando. Se si utilizza l'archiviazione di Azure come origine script hello, una chiave account e nome dell'account di archiviazione di Azure è obbligatoria. Questi elementi devono essere considerati come dati sensibili e specificati nella configurazione di hello estensioni impostazione protetto. Dati impostazione protette dell'estensione di macchina virtuale di Azure sono crittografati e decrittografati solo nella macchina virtuale di destinazione hello.

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
        "[variables('musicstoresqlName')]"
    ],
    "tags": {
        "displayName": "config-app"
    },
    "properties": {
        "publisher": "Microsoft.Compute",
        "type": "CustomScriptExtension",
        "typeHandlerVersion": "1.9",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "script location"
            ]
        },
        "protectedSettings": {
            "commandToExecute": "myExecutionCommand",
            "storageAccountName": "myStorageAccountName",
            "storageAccountKey": "myStorageAccountKey"
        }
    }
}
```

### <a name="property-values"></a>Valori delle proprietà

| Nome | Valore/Esempio |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.Compute |
| type | Estensioni |
| typeHandlerVersion | 1.9 |
| fileUris (es.) | https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1 |
| commandToExecute (es.) | powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 |
| storageAccountName (es.) | examplestorageacct |
| storageAccountKey (es.) | TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg== |

**Nota**: questi nomi di proprietà fanno distinzione tra maiuscole e minuscole. Nell'esempio precedente tooavoid problemi di distribuzione, utilizzare nomi di hello.

## <a name="template-deployment"></a>Distribuzione del modello

Le estensioni macchina virtuale di Azure possono essere distribuite con i modelli di Azure Resource Manager. schema JSON Hello descritta in dettaglio nella sezione precedente hello è utilizzabile in un hello toorun modello di gestione risorse di Azure estensione Script personalizzata durante la distribuzione di un modello di gestione risorse di Azure. Un modello di esempio che include l'estensione dello Script personalizzata è reperibile qui, hello [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="powershell-deployment"></a>Distribuzione PowerShell

Hello `Set-AzureRmVMCustomScriptExtension` comando può essere utilizzato tooadd hello Custom Script estensione tooan macchina virtuale esistente. Per ulteriori informazioni, vedere [Set-AzureRmVMCustomScriptExtension](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a>Risoluzione dei problemi e supporto

### <a name="troubleshoot"></a>Risoluzione dei problemi

Dati sullo stato di hello delle distribuzioni di estensione possono essere recuperati dal portale di Azure hello e, utilizzando il modulo di Azure PowerShell hello. stato di distribuzione toosee hello delle estensioni per una macchina virtuale specificata, eseguire hello comando seguente.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Esecuzione di estensione di output è toofiles registrati in hello seguenti directory nella macchina virtuale di destinazione hello.
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

Hello specificato i file vengono scaricati nella seguente directory nella macchina virtuale di destinazione hello hello.
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
dove `<n>` è un intero decimale che può cambiare tra le esecuzioni di estensione hello.  Hello `1.*` valore corrisponde a corrente effettivo, hello `typeHandlerVersion` valore dell'estensione hello.  Ad esempio, è possibile directory effettiva hello `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.  

Quando si esegue hello `commandToExecute` comando estensione hello verrà installata questa directory (ad esempio, `...\Downloads\2`) come directory di lavoro corrente hello. Questo utilizzo hello consente di file di percorsi relativi toolocate hello scaricati tramite hello `fileURIs` proprietà. Vedere la tabella hello seguente per gli esempi.

Poiché il percorso di download assoluto hello può variare nel tempo, è meglio tooopt per i percorsi relativi script/file hello `commandToExecute` stringa, laddove possibile. ad esempio:
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

Informazioni sul percorso dopo il primo segmento di URI hello viene mantenuto per i file scaricati tramite hello `fileUris` elenco di proprietà.  Come illustrato nella tabella hello riportata di seguito, vengono eseguito il mapping di file scaricati in download struttura hello tooreflect di sottodirectory di hello `fileUris` valori.  

#### <a name="examples-of-downloaded-files"></a>Esempi di file scaricati

| URI in fileUris | Percorso relativo scaricato | Percorso assoluto scaricato * |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

\*Come in precedenza, i percorsi di directory assoluta hello verranno modificato nel corso della durata hello di hello VM, ma non all'interno di una singola esecuzione dell'estensione CustomScript hello.

### <a name="support"></a>Supporto

Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti hello [forum MSDN di Azure e di Overflow dello Stack] (https://azure.microsoft.com/en-us/support/forums/). In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure. Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/en-us/support/options/) e scegliere supporto tecnico. Per informazioni sull'utilizzo di supporto di Azure, leggere hello [supporto tecnico di Microsoft Azure domande frequenti su](https://azure.microsoft.com/en-us/support/faq/).
