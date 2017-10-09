---
title: Esempio di Script di PowerShell - aaaAzure ridimensionare un'app web manualmente | Documenti Microsoft
description: Esempio di script di Azure PowerShell - Ridimensionare un'app Web manualmente
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: de5d4285-9c7d-4735-a695-288264047375
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: c749031fbe6c6bcbb25395387b4f32b2ba75cef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a>Ridimensionare un'App Web manualmente

In questo scenario si apprenderà toocreate un gruppo di risorse, app web e il piano di servizio app. È quindi verrà ridimensionato hello piano di servizio App dalle istanze di toomultiple singola istanza.

Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](/powershell/azure/overview), quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.

## <a name="sample-script"></a>Script di esempio

[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]

## <a name="clean-up-deployment"></a>Pulire la distribuzione 

Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove gruppo di risorse hello, app web e tutte le relative risorse.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza hello i comandi seguenti. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [New-AzureRmAppServicePlan](/powershell/module/azurerm.websites/new-azurermappserviceplan) | Consente di creare un piano di servizio app. |
| [New-AzureRmWebApp](/powershell/module/azurerm.websites/new-azurermwebapp) | Crea un'App Web. |
| [Set-AzureRmWebApp](/powershell/module/azurerm.websites/set-azurermwebapp) | Modifica la configurazione di un'app Web. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).

Esempi aggiuntivi di Azure Powershell per App Web di servizio App di Azure sono reperibile in hello [esempi di Azure PowerShell](../app-service-powershell-samples.md).
