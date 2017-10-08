---
title: modello di hello aaaDownload per una macchina virtuale di Azure | Documenti Microsoft
description: Scaricare hello templatefor toohelp una macchina virtuale con l'automazione delle distribuzioni nel modello di distribuzione di gestione risorse di hello
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 51ef4f51-0942-4249-afea-4a3f87ce1ff8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 86fd05f67409019b5e5c9023881745047860eee1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-template-for-a-vm"></a>Scaricare il modello di hello per una macchina virtuale
Quando si crea una macchina virtuale in Azure mediante portale hello o PowerShell, gestione delle risorse di modello viene creato automaticamente. È possibile utilizzare questo duplicato di tooquickly una distribuzione modello. modello di Hello contiene informazioni su tutte le risorse di hello in un gruppo di risorse. Per una macchina virtuale, ciò significa modello hello contiene tutto ciò che viene creato per supportare hello macchina virtuale in tale gruppo di risorse, tra cui le risorse di rete hello.

## <a name="download-hello-template-using-hello-portal"></a>Scaricare il modello di hello tramite il portale di hello
1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Un hello hub dal menu **macchine virtuali**.
3. Selezionare macchina virtuale hello hello elenco.
4. Selezionare **Script di automazione**.
5. Selezionare **scaricare** e salvare computer tooyour di file con estensione zip hello locale.
6. Aprire il file con estensione zip hello ed estrarre cartella tooa hello. file con estensione zip Hello conterrà:
   
   * deploy.ps1
   * deploy.sh 
   * deployer.rb
   * DeploymentHelper.cs
   * parameters.json
   * template.json

file template.json Hello è il modello di hello.

## <a name="download-hello-template-using-powershell"></a>Scaricare il modello di hello tramite PowerShell
È inoltre possibile scaricare i file di modello con estensione JSON hello utilizzando hello [esportazione AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet. È possibile utilizzare hello `-path` parametro tooprovide hello filename e il percorso di file con estensione JSON hello. Questo esempio viene illustrato come modello hello toodownload per il gruppo di risorse hello denominati **myResourceGroup** toohello **C:\users\public\downloads** cartella nel computer locale.

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a>Passaggi successivi
toolearn più sulla distribuzione di risorse utilizzando i modelli, vedere [procedura dettagliata di modello di gestione risorse](../../azure-resource-manager/resource-manager-template-walkthrough.md).

