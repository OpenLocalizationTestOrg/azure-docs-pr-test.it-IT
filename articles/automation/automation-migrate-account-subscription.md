---
title: aaaMigrate risorse e Account di automazione | Documenti Microsoft
description: In questo articolo viene descritto come toomove un'automazione dell'Account di automazione di Azure e le risorse associate da tooanother una sottoscrizione.
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9c2db4a2-f324-48dc-8ce7-3343bf7230d5
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte
ms.openlocfilehash: 201c9091cd2d78d7ea407c1e5fb27f366bb4fa8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-automation-account-and-resources"></a>Eseguire la migrazione delle risorse e dell’account di Automazione
Per gli account di automazione e le risorse associate (ad esempio asset, i runbook, moduli, e così via) che sono stati creati nel portale di Azure hello e desidera toomigrate da una risorsa gruppo tooanother o da una sottoscrizione tooanother, è possibile farlo facilmente con Hello [lo spostamento di risorse](../azure-resource-manager/resource-group-move-resources.md) funzionalità disponibile in hello portale di Azure. Tuttavia, prima di procedere con questa azione, è necessario vedere seguente hello [elenco di controllo prima di spostare risorse](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) e inoltre hello elenco sotto tooAutomation specifico.   

1. gruppo di risorse di sottoscrizione/destinazione Hello deve essere nella stessa area come origine di hello.  Pertanto, gli account di Automazione non possono essere spostati tra le aree.
2. Quando lo spostamento delle risorse (ad esempio, i runbook, processi, e così via), sia il gruppo di origine hello e il gruppo di destinazione hello sono bloccati per la durata di hello dell'operazione di hello. Scrivere e le operazioni di eliminazione sono bloccati in gruppi di hello fino al completamento di spostamento hello.  
3. Qualsiasi runbook o variabili che fanno riferimento a un ID di risorsa o sottoscrizione dalla sottoscrizione esistente hello necessario toobe aggiornato dopo il completamento della migrazione.   

> [!NOTE]
> Questa funzionalità non supporta lo spostamento delle risorse di automazione classica.
>
>

## <a name="toomove-hello-automation-account-using-hello-portal"></a>toomove hello tramite hello portale Account di automazione
1. Scegliere l'account di automazione, **spostare** nella parte superiore di hello del pannello hello.<br> ![Opzione Sposta](media/automation-migrate-account-subscription/automation-menu-move.png)<br>
2. In hello **lo spostamento di risorse** blade, si noti che presenta le risorse correlate tooboth l'account di automazione e i gruppi di risorse.  Seleziona hello **sottoscrizione** e **gruppo di risorse** da elenchi a discesa hello o opzione hello selezionare **creare un nuovo gruppo di risorse** e immettere un nuovo nome gruppo di risorse in campo Hello fornito.  
3. Revisione e hello selezionare la casella di controllo tooacknowledge è *comprendere strumenti e script sarà necessario toobe aggiornato toouse nuovi ID di risorsa dopo aver spostate le risorse* e quindi fare clic su **OK**.<br> ![Pannello Sposta risorse](media/automation-migrate-account-subscription/automation-move-resources-blade.png)<br>   

Questa operazione richiederà diverse toocomplete minuti.  In **Notifiche**verrà visualizzato lo stato di ciascuna operazione eseguita: convalida, migrazione e completa.     

## <a name="toomove-hello-automation-account-using-powershell"></a>toomove hello Account di automazione con PowerShell
esistente toomove gruppo di risorse di automazione risorse tooanother o sottoscrizione, utilizzare hello **Get-AzureRmResource** cmdlet tooget hello specifico account di automazione e quindi **Move-AzureRmResource** spostamento di hello tooperform cmdlet.

Hello primo esempio viene illustrato come un'automazione toomove account tooa nuovo gruppo di risorse.

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

Dopo aver eseguito hello esempio di codice precedente, sarà richiesta tooverify tooperform si desidera che questa azione.  Quando si fa clic su **Sì** e consentire hello tooproceed script, non si ricevano le notifiche durante l'esecuzione della migrazione hello.  

toomove tooa nuova sottoscrizione, includere un valore per hello *DestinationSubscriptionId* parametro.

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

Come con hello esempio precedente, sarà richiesta tooconfirm hello move.  

## <a name="next-steps"></a>Passaggi successivi
* Per ulteriori informazioni sul gruppo di risorse toonew risorse mobile o una sottoscrizione, vedere [spostare sottoscrizione o il gruppo di risorse toonew risorse](../azure-resource-manager/resource-group-move-resources.md)
* Per ulteriori informazioni sul controllo di accesso basato sui ruoli in automazione di Azure, vedere troppo[controllo di accesso basato sui ruoli in automazione di Azure](automation-role-based-access-control.md).
* toolearn sui cmdlet di PowerShell per gestire la sottoscrizione, vedere [tramite Azure PowerShell con Gestione risorse](../azure-resource-manager/powershell-azure-resource-manager.md)
* toolearn sulle funzionalità del portale per gestire la sottoscrizione, vedere [utilizzando le risorse di hello Azure Portal toomanage](../azure-resource-manager/resource-group-portal.md).
