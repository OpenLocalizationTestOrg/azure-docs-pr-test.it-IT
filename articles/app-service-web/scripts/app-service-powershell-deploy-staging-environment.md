---
title: aaaAzure Script di PowerShell di esempio - creare un'app web e distribuire codice tooa ambiente di gestione temporanea | Documenti Microsoft
description: Esempio di Script di PowerShell Azure - creare un'app web e distribuire codice tooa ambiente di gestione temporanea
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 27cf0680-c3a9-4a58-9f71-6dec09f6b874
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 5c74b962955770637173f1fd4f49342fec54ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a>Creare un'app web e distribuire codice tooa ambiente di gestione temporanea

Questo script di esempio crea un'app web nel servizio App con uno slot di distribuzione aggiuntivo denominato "gestione temporanea" e quindi distribuisce un toohello di app di esempio "gestione temporanea" slot.

Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](/powershell/azure/overview), quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.

## <a name="sample-script"></a>Script di esempio

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code tooa staging environment")]

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
| [Set-AzureRmAppServicePlan](/powershell/module/azurerm.websites/set-azurermappserviceplan) | Modifica il livello di prezzo di un toochange piano di servizio App. |
| [New-AzureRmWebAppSlot](/powershell/module/azurerm.websites/new-azurermwebappslot) | Crea uno slot di distribuzione per un'app Web. |
| [Set-AzureRmResource](/powershell/module/azurerm.resources/set-azurermresource) | Modifica una risorsa in un gruppo di risorse. |
| [Swap-AzureRmWebAppSlot](/powershell/module/azurerm.websites/swap-azurermwebappslot) | Trasferisce uno slot di distribuzione dell'app Web nell'ambiente di produzione. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sul modulo di Azure PowerShell hello, vedere [documentazione di Azure PowerShell](/powershell/azure/overview).

Esempi aggiuntivi di Azure Powershell per App Web di servizio App di Azure sono reperibile in hello [esempi di Azure PowerShell](../app-service-powershell-samples.md).
