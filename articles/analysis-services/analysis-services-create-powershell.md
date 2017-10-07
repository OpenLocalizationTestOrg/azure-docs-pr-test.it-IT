---
title: un server di Azure Analysis Services utilizzando PowerShell aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate un Azure Analysis Services server utilizzando PowerShell
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/01/2017
ms.author: owend
ms.custom: mvc
ms.openlocfilehash: 269b78983410f773d47c4cea34d6d353b19f9e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a>Creare un server di Azure Analysis Services tramite PowerShell

Questa Guida introduttiva viene illustrato l'utilizzo di PowerShell da hello riga di comando toocreate un server di Azure Analysis Services in un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) nella sottoscrizione di Azure.

Questa attività richiede il modulo Azure PowerShell 4.0 o versioni successive. versione di hello toofind, eseguire ` Get-Module -ListAvailable AzureRM`. tooinstall o l'aggiornamento, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps). 

> [!NOTE]
> La creazione di un server può avere come risultato un nuovo servizio fatturabile. vedere, più toolearn [dei prezzi di Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).

## <a name="prerequisites"></a>Prerequisiti
toocomplete questa Guida rapida, è necessario:

* **Sottoscrizione di Azure**: visitare [versione di valutazione gratuita di Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate un account.
* **Azure Active Directory**: la sottoscrizione deve essere associata a un tenant Azure Active Directory ed è necessario avere un account in tale directory. vedere, più toolearn [l'autenticazione e le autorizzazioni utente](analysis-services-manage-users.md).

## <a name="import-azurermanalysisservices-module"></a>Importare il modulo AzureRm.AnalysisServices
toocreate un server nella sottoscrizione, utilizzare hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) modulo componente. Caricare il modulo di AzureRm.AnalysisServices hello nella sessione di PowerShell.

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-tooazure"></a>Accedi tooAzure

Accedi tooyour sottoscrizione di Azure tramite hello [Aggiungi AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) comando. Seguire hello le direzioni.

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse
 
Un [gruppo di risorse di Azure](../azure-resource-manager/resource-group-overview.md) è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite come gruppo. Quando si crea il server, è necessario specificare un gruppo di risorse nella sottoscrizione. Se si dispone già di un gruppo di risorse, è possibile creare una nuova istanza utilizzando hello [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) comando. esempio Hello crea un gruppo di risorse denominato `myResourceGroup` nell'area Stati Uniti occidentali hello.

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a>Creare un server

Creare un nuovo server tramite hello [New AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) comando. Hello esempio seguente viene creato un server denominato Server1 in myResourceGroup, nell'area Stati Uniti occidentali hello, a livello di hello D1 e philipc@adventureworks.com come un amministratore del server.

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a>Pulire le risorse

È possibile rimuovere il server di hello dalla sottoscrizione utilizzando hello [Remove AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) comando. Se si prevede di passare ad altre esercitazioni introduttive ed esercitazioni in questa raccolta, non rimuovere il server. Hello esempio seguente rimuove il server di hello creato nel passaggio precedente hello.


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a>Passaggi successivi
[Gestire Azure Analysis Services con PowerShell](analysis-services-powershell.md)   
[Distribuire un modello da SSDT](analysis-services-deploy.md)   
[Creare un modello nel portale di Azure](analysis-services-create-model-portal.md)