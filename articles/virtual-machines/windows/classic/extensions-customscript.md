---
title: estensione dello Script in una macchina virtuale Windows aaaCustom | Documenti Microsoft
description: "Automatizzare le attività di configurazione macchina virtuale di Azure tramite script di PowerShell toorun estensione Custom Script hello in una VM Windows remoto"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: ebb7340a-8f61-4d3c-a290-d7bf8de2d0bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: nepeters
ms.openlocfilehash: cf7bb895dd211f07fd010dc03b68cd77df1127b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows-using-hello-classic-deployment-model"></a>Script di estensione per Windows personalizzata utilizzando il modello di distribuzione classica hello

> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Informazioni su come troppo[eseguire questi passaggi tramite il modello di gestione risorse di hello](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Estensione dello Script personalizzata Hello Scarica ed esegue gli script in macchine virtuali di Azure. Questa estensione è utile per la configurazione post-distribuzione, l'installazione di software o qualsiasi altra attività di configurazione o gestione. Gli script possono essere scaricati da GitHub o di archiviazione di Azure o forniti toohello portale di Azure in fase di esecuzione di estensione. estensione Script personalizzata Hello si integra con i modelli di gestione risorse di Azure e può essere eseguito anche tramite hello Azure CLI, PowerShell, il portale di Azure o hello API REST di macchina virtuale di Azure.

Questo documento illustra in dettaglio come toouse hello estensione Script personalizzata utilizzando hello modulo Azure PowerShell, i modelli di gestione risorse di Azure e i dettagli di risoluzione dei problemi in sistemi Windows.

## <a name="prerequisites"></a>Prerequisiti

### <a name="operating-system"></a>Sistema operativo

Estensione dello Script personalizzata Hello per Windows possono essere eseguite in Windows Server 2008 R2, 2012 e 2012 R2 2016 rilascia.

### <a name="script-location"></a>Percorso dello script

script di Hello deve toobe archiviati in archiviazione di Azure o qualsiasi altro percorso accessibile tramite un URL valido.

### <a name="internet-connectivity"></a>Connettività Internet

Hello Custom Script di estensione per Windows richiede tale macchina virtuale di destinazione hello è connesso toohello internet. 

## <a name="extension-schema"></a>Schema dell'estensione

Hello JSON seguente viene illustrato lo schema di hello per hello estensione Script personalizzata. estensione di Hello richiede un percorso di script (archiviazione di Azure o in altre posizioni di URL valido) e tooexecute un comando. Se si utilizza l'archiviazione di Azure come origine script hello, una chiave account e nome dell'account di archiviazione di Azure è obbligatoria. Questi elementi devono essere considerati come dati sensibili e specificati nella configurazione di hello estensioni impostazione protetto. Dati impostazione protette dell'estensione di macchina virtuale di Azure sono crittografati e decrittografati solo nella macchina virtuale di destinazione hello.

```json
{
    "name": "config-app",
    "type": "Microsoft.ClassicCompute/virtualMachines/extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-01",
    "properties": {
        "publisher": "Microsoft.Compute",
        "extension": "CustomScriptExtension",
        "version": "1.8",
        "parameters": {
            "public": {
                "fileUris": "[myScriptLocation]"
            },
            "private": {
                "commandToExecute": "[myExecutionString]"
            }
        }
    }
}
```

### <a name="property-values"></a>Valori delle proprietà

| Nome | Valore/Esempio |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.Compute |
| estensione | CustomScriptExtension |
| typeHandlerVersion | 1.8 |
| fileUris (es.) | https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1 |
| commandToExecute (es.) | powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 |

## <a name="template-deployment"></a>Distribuzione del modello

Le estensioni macchina virtuale di Azure possono essere distribuite con i modelli di Azure Resource Manager. schema JSON Hello descritta in dettaglio nella sezione precedente hello è utilizzabile in un hello toorun modello di gestione risorse di Azure estensione Script personalizzata durante la distribuzione di un modello di gestione risorse di Azure. Un modello di esempio che include l'estensione dello Script personalizzata è reperibile qui, hello [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="powershell-deployment"></a>Distribuzione PowerShell

Hello `Set-AzureVMCustomScriptExtension` comando può essere utilizzato tooadd hello Custom Script estensione tooan macchina virtuale esistente. Per ulteriori informazioni, vedere [Set-AzureRmVMCustomScriptExtension](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a>Risoluzione dei problemi e supporto

### <a name="troubleshoot"></a>Risoluzione dei problemi

Dati sullo stato di hello delle distribuzioni di estensione possono essere recuperati dal portale di Azure hello e, utilizzando il modulo di Azure PowerShell hello. stato di distribuzione toosee hello delle estensioni per una macchina virtuale specificata, eseguire hello comando seguente.

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Esecuzione di estensione output ci toofiles connesso trovato nella seguente directory nella macchina virtuale di destinazione hello hello.

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

script Hello stesso viene scaricato nella seguente directory nella macchina virtuale di destinazione hello hello.

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a>Supporto

Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti hello [forum MSDN di Azure e di Overflow dello Stack](https://azure.microsoft.com/en-us/support/forums/). In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure. Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/en-us/support/options/) e scegliere supporto tecnico. Per informazioni sull'utilizzo di supporto di Azure, leggere hello [supporto tecnico di Microsoft Azure domande frequenti su](https://azure.microsoft.com/en-us/support/faq/).
