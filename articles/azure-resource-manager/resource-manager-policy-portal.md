---
title: aaaAzure portale per i criteri di risorse | Documenti Microsoft
description: Viene descritto come toouse toocreate portale Azure e gestire i criteri di gestione risorse. I criteri possono essere applicati a hello sottoscrizione o gruppi di risorse.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: ce6413386317e532b63761a24458b85c996af4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-tooassign-and-manage-resource-policies"></a>Utilizzare tooassign portale Azure e gestire i criteri di risorse
portale di Azure Hello consente le sottoscrizioni e si tooassign criteri tooresource gruppi di risorse. interfaccia utente di Hello rende i criteri di hello tooselect semplice che si desidera tooassign e specificano i valori dei parametri per tale criterio impostazioni dei criteri toocustomize hello. 

tooassign criteri tramite il portale di hello, definizione dei criteri hello deve esistere già nella sottoscrizione. La sottoscrizione ha diverse definizioni di criteri predefiniti che sono pronte per si tooassign tooresource gruppi o le sottoscrizioni. Vengono visualizzati questi criteri predefiniti e i criteri personalizzati definiti quando si utilizza criteri tooassign portale hello. Per un'introduzione toopolicies e come toodefine personalizzare criteri, vedere [Panoramica criteri delle risorse](resource-manager-policy.md).

I criteri vengono ereditati da tutte le risorse figlio. Se il criterio viene applicato tooa gruppo di risorse, è pertanto applicabile tooall risorse di hello in tale gruppo di risorse. In questo articolo, termini hello **ambito** fa riferimento il gruppo di risorse toohello o una sottoscrizione che viene assegnato il criterio di hello. 

I criteri vengono valutati durante la creazione e l'aggiornamento delle risorse (operazioni PUT e PATCH).

## <a name="assign-a-policy"></a>Assegnare i criteri

1. tooassign un tooeither criteri un gruppo di risorse o una sottoscrizione, selezionare il gruppo di risorse o di una sottoscrizione. Nelle impostazioni di hello, selezionare **criteri**.

   ![selezionare i criteri](./media/resource-manager-policy-portal/select-policies.png)

2. Selezionare un'assegnazione di criteri per questo ambito, toocreate **aggiungere assegnazione**.

   ![aggiungere un'assegnazione](./media/resource-manager-policy-portal/add-assignment.png)

3. Selezionare i criteri di hello da tooassign. Anche se non sono state aggiunte sottoscrizioni di tooyour le definizioni dei criteri, vedrai i criteri predefiniti hello che sono disponibili per l'assegnazione. I criteri predefiniti sono applicabili a numerosi scenari comuni.

   ![selezionare la definizione](./media/resource-manager-policy-portal/select-definition.png)

4. Dopo aver selezionato un criterio, vedere una descrizione dei criteri di hello e i parametri per tale criterio. Ad esempio, hello seguente immagine Mostra hello **consentiti percorsi** parametro, è necessario per i criteri di hello che limitano i percorsi disponibili hello.

   ![visualizzazione dei parametri](./media/resource-manager-policy-portal/show-parameters.png)

5. Tramite l'interfaccia utente di hello, selezionare hello toospecify di valori per i parametri dei criteri hello (ad esempio i percorsi di hello che possono essere usati per la distribuzione).

   ![selezionare i valori dei parametri](./media/resource-manager-policy-portal/select-parameters.png)

6. Fornire valori per hello altri parametri. ambito Hello viene assegnato automaticamente nel pannello hello selezionato quando si avvia l'assegnazione dei criteri hello. Selezionare **OK** al termine dell'operazione.

   ![definire i parametri](./media/resource-manager-policy-portal/define-parameters.png)

  È stato assegnato il criterio di hello toohello specificato ambito.

## <a name="view-policy-assignments"></a>Visualizzare le assegnazioni di criteri

Dopo l'assegnazione di un criterio, è visualizzata nell'elenco di hello dei criteri per tale ambito. Hello **dettagli** scheda Mostra un riepilogo dell'assegnazione di criteri hello.

![visualizzare i dettagli](./media/resource-manager-policy-portal/show-details.png)

Hello **regola di assegnazione** scheda Mostra hello JSON per la definizione dei criteri hello.

![visualizzare la regola di assegnazione](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a>Modificare un'assegnazione di criteri esistente

Selezionare un criterio, toochange **modifica assegnazione** o **eliminare**

![modificare o eliminare l'assegnazione](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a>Assegnare criteri personalizzati

Se sono stati definiti criteri personalizzati nella sottoscrizione, sono disponibili per l'assegnazione tramite il portale di hello tali criteri. I criteri personalizzati sono preceduti da **[Personalizzato]**

![criteri personalizzati](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a>Passaggi successivi
* toolearn sulla sintassi di hello JSON per la definizione di criteri, vedere [Panoramica criteri delle risorse](resource-manager-policy.md).
* Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).
* schema dei criteri di Hello è pubblicato nella [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json). 

