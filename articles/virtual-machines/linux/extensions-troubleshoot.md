---
title: VM Linux aaaTroubleshooting errori estensione | Documenti Microsoft
description: Informazioni sulla risoluzione degli errori delle estensioni della macchina virtuale di Azure
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: f05d93f3-42fc-4a09-9798-d92f7929c417
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 29a0ca34207421e0014380000a313d3c44e7e594
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a>Risoluzione degli errori delle estensioni della macchina virtuale Linux di Azure
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>Visualizzazione dello stato dell'estensione
Modelli di gestione risorse di Azure possono essere eseguiti da hello CLI di Azure. Quando viene eseguita modello hello, lo stato dell'estensione hello può essere visualizzato da Esplora inventario risorse di Azure o hello strumenti da riga di comando.

Di seguito è fornito un esempio:

Interfaccia della riga di comando di Azure:

      azure vm get-instance-view


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

## <a name="troubleshooting-extenson-failures"></a>Risoluzione degli errori delle Estensioni:
### <a name="re-running-hello-extension-on-hello-vm"></a>Eseguire nuovamente l'estensione hello in hello VM
Se si eseguono gli script nella macchina virtuale utilizzando l'estensione dello Script personalizzata hello, in alcuni casi è possibile eseguire un errore in cui VM è stato creato ma script hello non è riuscita. In queste condizioni, hello consigliato modo toorecover da questo errore è tooremove hello estensione e nuovamente il modello di hello.
Nota: In futuro, questa funzionalità sarebbe tooremove avanzata hello necessità di disinstallazione dell'estensione hello.

#### <a name="remove-hello-extension-from-azure-cli"></a>Rimuovi estensione hello dalla CLI di Azure
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

Dove "nome-per Publisher" corrispondente tipo di estensione toohello dall'output di hello di "get-istanza-view macchina virtuale di azure" e hello nome della risorsa di estensione hello dal modello hello

Una volta hello estensione è stata rimossa, il modello di hello può essere rieseguita toorun hello gli script hello VM.

