---
title: aaaSolution come destinazione di OMS | Documenti Microsoft
description: "Destinazioni di soluzione sono una funzionalità di Operations Management Suite (OMS) che consente di toolimit Gestione soluzioni tooa set specifico di agenti.  Questo articolo viene descritto come toocreate una configurazione di ambito e applicarlo tooa soluzione."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 6f8c8109e0d9e282e18724bf8b673b10de8e498a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-solution-targeting-in-operations-management-suite-oms-tooscope-management-solutions-toospecific-agents-preview"></a>Utilizzare Esplora targeting in Operations Management Suite (OMS) gli agenti toospecific soluzioni di gestione di tooscope (anteprima)
Quando si aggiunge un tooOMS soluzione, viene distribuito automaticamente da tooall Windows e Linux gli agenti connessi tooyour Log Analitica area di lavoro predefinita.  È opportuno toomanage i costi e limite hello della quantità di dati raccolti per una soluzione limitandolo tooa particolare set di agenti.  Questo articolo viene descritto come toouse **soluzione destinazione** che è una funzionalità OMS che consente a un ambito tooapply tooyour soluzioni.

## <a name="how-tootarget-a-solution"></a>Come tootarget una soluzione
Esistono tre passaggi tootargeting una soluzione come descritto in hello le sezioni seguenti.  Si noti che è necessario il portale di OMS hello sia hello portale di Azure per i diversi passaggi.


### <a name="1-create-a-computer-group"></a>1. Creare un gruppo di computer
Specificare i computer hello che si vuole tooinclude in un ambito, la creazione di un [gruppo di computer](../log-analytics/log-analytics-computer-groups.md) nel Log Analitica.  gruppo di computer Hello in base a una ricerca di log o importato da origini diverse, ad esempio Active Directory o gruppi WSUS. Come [descritto di seguito](#solutions-and-agents-that-cant-be-targeted), solo i computer che sono direttamente connessi tooLog Analitica verrà inclusi nell'ambito di hello.

Dopo aver creato il gruppo di computer hello creato nell'area di lavoro, è possibile includerlo in una configurazione di ambito che può essere applicati tooone o altre soluzioni.
 
 
 ### <a name="2-create-a-scope-configuration"></a>2. Creare una configurazione ambito
 Oggetto **configurazione dell'ambito** include uno o più gruppi di computer e possono essere applicati tooone o altre soluzioni. 
 
 Creare una configurazione di ambito utilizzando hello processo.  

 1. Nel portale di Azure hello, passare troppo**Analitica Log** e selezionare l'area di lavoro.
 2. Nelle proprietà dell'area di lavoro hello in hello **origini di dati dell'area di lavoro** selezionare **configurazioni ambito**.
 3. Fare clic su **Aggiungi** toocreate una nuova configurazione di ambito.
 4. Digitare un **nome** per la configurazione dell'ambito hello.
 5. Fare clic su **Selezionare i gruppi di computer**.
 6. Selezionare il gruppo di computer hello creato e, facoltativamente, qualsiasi altra tooadd toohello configurazione di gruppi.  Fare clic su **Seleziona**.  
 6. Fare clic su **OK** configurazione dell'ambito toocreate hello. 


 ### <a name="3-apply-hello-scope-configuration-tooa-solution"></a>3. Applicare hello ambito configurazione tooa soluzione.
Dopo aver creato una configurazione di ambito, quindi è possibile applicarlo tooone o altre soluzioni.  Si noti che è possibile usare una sola configurazione ambito con più soluzioni e che ogni soluzione può usare solo una configurazione ambito.

Applicare una configurazione di ambito mediante hello processo.  

 1. Nel portale di Azure hello, passare troppo**Analitica Log** e selezionare l'area di lavoro.
 2. Selezionare la proprietà hello per area di lavoro hello **soluzioni**.
 3. Fare clic sulla soluzione hello desiderato tooscope.
 4. Nelle proprietà hello per soluzione hello in **origini di dati dell'area di lavoro** selezionare **soluzione destinazione**.  Se non è disponibile l'opzione hello quindi [questa soluzione non può essere destinata](#solutions-and-agents-that-cant-be-targeted).
 5. Fare clic su **Aggiungi configurazione dell'ambito**.  Se si dispone già di una soluzione di toothis configurazione applicata questa opzione non sarà disponibile.  È necessario rimuovere una configurazione esistente di hello prima di aggiungere un altro.
 6. Fare clic su configurazione di ambito hello è stato creato.
 7. Hello Watch **stato** di tooensure configurazione hello che mostra **Succeeded**.  Se lo stato di hello indica un errore, quindi fare clic su hello ellisse toohello destra della configurazione hello e selezionare **configurazione dell'ambito di modifica** toomake modifiche.

## <a name="solutions-and-agents-that-cant-be-targeted"></a>Soluzioni e agenti di cui non è possibile eseguire il targeting
Di seguito sono criteri hello per gli agenti e non possono essere utilizzate con la destinazione di Esplora soluzioni.

- Soluzione è destinata solo toosolutions che distribuiscono tooagents.
- Soluzione è destinata solo toosolutions fornito da Microsoft.  Non è applicabile toosolutions [creati autonomamente o partner](operations-management-suite-solutions-creating.md).
- È possibile filtrare solo gli agenti che si connettono direttamente tooLog Analitica.  Soluzioni distribuirà automaticamente tooany agenti che fanno parte di un gruppo di gestione di Operations Manager connesso o meno vengono inclusi in una configurazione di ambito.

### <a name="exceptions"></a>Eccezioni
Soluzione di destinazione non può essere utilizzato con hello seguenti soluzioni anche se si adatta hello indicato criteri.

- Valutazione dell'integrità dell'agente

## <a name="next-steps"></a>Passaggi successivi
- Altre informazioni sulle soluzioni di gestione, ad esempio hello soluzioni che sono disponibili tooinstall nell'ambiente in uso in [dell'area di lavoro di aggiungere Azure Log Analitica Gestione soluzioni tooyour](../log-analytics/log-analytics-add-solutions.md).
- Altre informazioni sulla creazione di gruppi di computer sono riportate in [Gruppi di computer nelle ricerche log in Log Analytics](../log-analytics/log-analytics-computer-groups.md).