---
title: aaaCreate, collegamento, eliminare o spostare un account di integrazione in App per la logica di Azure | Documenti Microsoft
description: Come toocreate un'integrazione account, quindi collegarlo tooyour logica App
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a>Cos'è un account di integrazione?

Un account di integrazione consente enterprise integration App toomanage elementi, inclusi gli schemi, mappe, i certificati, partner e contratti. Qualsiasi applicazione di integrazione che è creare Usa un tooaccess account integrazione questi schemi, mappe, i certificati e così via.

## <a name="create-an-integration-account"></a>Creare un account di integrazione

1.  Accedi toohello [portale di Azure](http://portal.azure.com "portale di Azure"). Scegliere dal menu a sinistra hello **più servizi**.

    ![Selezionare "Altri servizi"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. Nella casella di ricerca hello, digitare "integrazione" per il filtro. Selezionare dall'elenco risultati hello **account di integrazione**.

    ![Filtro su "integrazione", selezionare "Account di integrazione"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. Nella parte superiore di hello della pagina hello, scegliere **Aggiungi**.

    ![Scegliere Aggiungi](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. Denominare l'account di integrazione e la sottoscrizione di Azure che si desidera toouse di hello Seleziona. È possibile creare un nuovo **Gruppo di risorse** o selezionarne uno esistente. Selezionare quindi la **località** in cui eseguire l'hosting dell'account di integrazione e un **piano tariffario**. 

    Al termine, scegliere **Crea**.

    ![Immettere i dettagli dell'account di integrazione](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    Provisioning tramite Azure l'account di integrazione nel percorso selezionato hello, che deve essere completato entro 1 minuto.

5. Aggiornare la pagina hello. Il nuovo account di integrazione verrà visualizzato nell'elenco.

    ![Visualizzazione del nuovo account di integrazione](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

Successivamente, creare collegamenti account integrazione hello è creato tooyour logica app. 

## <a name="link-an-integration-account-tooa-logic-app"></a>Collegare un'applicazione di integrazione account tooa logica

toogive App per la logica di accesso toomaps, schemi, contratti e altri elementi nell'account di integrazione, collegamento hello integrazione account tooyour logica app.

### <a name="prerequisites"></a>Prerequisiti

* Un account di integrazione
* App per la logica

> [!NOTE] 
> Verificare che l'applicazione di account e la logica di integrazione siano hello *nello stesso percorso Azure* prima di iniziare.


1. Nel portale di Azure hello, selezionare l'app per la logica e controllare la posizione logica dell'applicazione.

    ![Selezionare l'app per la logica, controllare la località](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. In **Impostazioni**, selezionare **Account di integrazione**.

    ![Selezionare "Account di integrazione"](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. Da hello **selezionare un account di integrazione** elencare, account di integrazione hello selezionare desiderato toolink tooyour logica app. Scegliere il collegamento, toofinish **salvare**.

    ![Selezionare l'account di integrazione](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    Si riceve una notifica che mostra l'integrazione di account è collegato tooyour logica app e che tutti gli elementi nell'account di integrazione sono ora disponibili tooyour logica app.

    ![Logica app è collegata tooyour account di integrazione](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

Ora che l'account di integrazione è collegato tooyour logica app, è possibile utilizzare i connettori di hello B2B nelle App logica. Alcuni connettori B2B comuni includono la convalida XML e la codifica e decodifica di file flat.  

## <a name="delete-your-integration-account"></a>Eliminare l'account di integrazione

1. Selezionare **Altri servizi**.

    ![Selezionare "Altri servizi"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. Nella casella di ricerca hello, digitare "integrazione" per il filtro. Selezionare dall'elenco risultati hello **account di integrazione**.

    ![Filtro su "integrazione", selezionare "Account di integrazione"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. Selezionare l'account di integrazione hello che si desidera toodelete.

    ![Selezionare toodelete account di integrazione](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. Scegliere dal menu hello **eliminare**.

    ![Scegliere "Elimina"](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. Confermare l'account di integrazione di hello toodelete scelte.

## <a name="move-your-integration-account"></a>Spostare l'account di integrazione

toomove un tooanother account integrazione gruppo sottoscrizione o la risorsa di Azure, seguire questi passaggi.

> [!IMPORTANT]
> Dopo aver spostato un account di integrazione, è necessario aggiornare tutti gli script toouse hello nuovi ID di risorsa.

1. Selezionare **Altri servizi**.

    ![Selezionare "Altri servizi"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. Nella casella di ricerca hello, digitare "integrazione" per il filtro. Selezionare dall'elenco risultati hello **account di integrazione**.

    ![Filtro su "integrazione", selezionare "Account di integrazione"](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. Selezionare l'account di integrazione hello che si desidera toomove. In **Impostazioni**, scegliere **Proprietà**.

    ![Selezionare toomove account di integrazione. In Impostazioni, scegliere Proprietà](./media/logic-apps-enterprise-integration-accounts/move.png)

5. Modificare il gruppo di risorse hello o sottoscrizione di Azure che è associato all'account di integrazione.

    ![Scegliere Cambia il gruppo di risorse o Cambia sottoscrizione](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a>Passaggi successivi
* [Altre informazioni sui contratti](../logic-apps/logic-apps-enterprise-integration-agreements.md "Informazioni sui contratti di Enterprise Integration")  

