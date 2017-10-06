---
title: errori di estensione di macchina virtuale Windows aaaTroubleshooting | Documenti Microsoft
description: Informazioni sulla risoluzione degli errori delle estensioni della macchina virtuale Windows di Azure
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: 878ab9b6-c3e6-40be-82d4-d77fecd5030f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: d24544743d9e0cb1a68ec9ab7718716f918054f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a>Risoluzione degli errori delle estensioni di macchina virtuale Windows di Azure
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>Visualizzazione dello stato dell'estensione
I modelli di Azure Resource Manager possono essere eseguiti da Azure PowerShell. Quando viene eseguita modello hello, lo stato dell'estensione hello può essere visualizzato da Esplora inventario risorse di Azure o hello strumenti da riga di comando.

Di seguito è fornito un esempio:

Azure PowerShell:

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

Ecco l'output di esempio hello:

      Extensions:  {
      "ExtensionType": "Microsoft.Compute.CustomScriptExtension",
      "Name": "myCustomScriptExtension",
      "SubStatuses": [
        {
          "Code": "ComponentStatus/StdOut/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "    Directory: C:\\temp\\n\\n\\nMode                LastWriteTime     Length Name
              \\n----                -------------     ------ ----                              \\n-a---          9/1/2015   2:03 AM         11
              test.txt                          \\n\\n",
                      "Time": null
          },
        {
          "Code": "ComponentStatus/StdErr/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "",
          "Time": null
        }
    }
  ]

## <a name="troubleshooting-extension-failures"></a>Risoluzione degli errori delle estensioni
### <a name="re-running-hello-extension-on-hello-vm"></a>Eseguire nuovamente l'estensione hello in hello VM
Se si eseguono gli script nella macchina virtuale utilizzando l'estensione dello Script personalizzata hello, in alcuni casi è possibile eseguire un errore in cui VM è stato creato ma script hello non è riuscita. In queste condizioni, hello consigliato modo toorecover da questo errore è tooremove hello estensione e nuovamente il modello di hello.
Nota: In futuro, questa funzionalità sarebbe tooremove avanzata hello necessità di disinstallazione dell'estensione hello.

#### <a name="remove-hello-extension-from-azure-powershell"></a>Rimuovere l'estensione hello da Azure PowerShell
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

Una volta hello estensione è stata rimossa, il modello di hello può essere rieseguita toorun hello gli script hello VM.

