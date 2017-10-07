---
title: "Esempio di Script di PowerShell - instradare il traffico per la disponibilità elevata delle applicazioni aaaAzure | Documenti Microsoft"
description: "Esempio di script di Azure PowerShell - Instradare il traffico per la disponibilità elevata delle applicazioni"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: georgewallace
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 11d15780403b4ed79e85d7b3495bc5d674bfdaee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a>Instradare il traffico per la disponibilità elevata delle applicazioni

In questo script viene creato un gruppo di risorse, due piani di servizio app, due app Web, un profilo di gestione traffico e due endpoint di gestione traffico. Gestione traffico indirizza applicazione toohello il traffico in un'area come area primaria hello e area secondaria toohello quando un'applicazione hello nell'area primaria hello è disponibile. Prima di eseguire script hello, è necessario modificare hello MyWebApp, MyWebAppL1 e MyWebAppL2 valori toounique valori in Azure. Dopo l'esecuzione di script hello, è possibile accedere app hello nell'area primaria di hello con mywebapp.trafficmanager.net URL hello.

Se necessario, installare Azure PowerShell utilizzando l'istruzione hello trovato in hello hello [Guida di Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), quindi eseguire `Login-AzureRmAccount` toocreate una connessione con Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script di esempio

[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]


Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a>Spiegazione dello script

Questo script utilizza i seguenti comandi toocreate un gruppo di risorse, app web, il profilo di gestione traffico hello e tutte risorse correlate. Ogni comando in documentazione specifica toocommand hello tabella collegamenti.

| Comando | Note |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse. |
| [New-AzureRmAppServicePlan](/powershell/module/azurerm.websites/new-azurermappserviceplan) | Consente di creare un piano di servizio app. Equivale a una server farm per l'App Web di Azure. |
| [New-AzureRmWebApp](/powershell/module/azurerm.websites/new-azurermwebapp) | Crea un'app web di Azure all'interno di hello piano di servizio App. |
| [Set-AzureRmResource](/powershell/module/azurerm.resources/new-azurermresource) | Crea un'app web di Azure all'interno di hello piano di servizio App. |
| [New-AzureRmTrafficManagerProfile](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | Crea un profilo di Gestione traffico di Azure. |
| [New-AzureRmTrafficManagerEndpoint](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | Aggiunge un tooan endpoint del profilo di Traffic Manager di Azure. |

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su hello Azure PowerShell, vedere [documentazione di Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

Ulteriori esempi di script di PowerShell remota sono reperibile in hello [documentazione Cenni preliminari sulle reti di Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
