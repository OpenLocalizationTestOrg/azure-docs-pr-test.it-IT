---
title: ripristino aaaDisaster per account di integrazione B2B - App Azure per la logica | Documenti Microsoft
description: Ripristino di emergenza delle app per la logica B2B
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e86564a3c5a2607d22514936c606e2843cba0416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a>Ripristino di emergenza tra più aree delle app per la logica B2B

I carichi di lavoro B2B coinvolgono le transazioni di denaro, come ad esempio gli ordini e le fatture. Durante un evento di emergenza, è fondamentale per un hello toomeet di business tooquickly Ripristina che i contratti di servizio a livello aziendale concordati con i partner. In questo articolo viene illustrato come toobuild continuità aziendale un piano per i carichi di lavoro B2B. 

* Preparazione al ripristino di emergenza 
* Eseguire il failover toosecondary area durante un evento di emergenza 
* Eseguire il fallback tooprimary area dopo un evento di emergenza

## <a name="disaster-recovery-readiness"></a>Preparazione al ripristino di emergenza  

1. Identifica un'area secondaria e creare un [account integrazione](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) nell'area secondaria hello.

2. Aggiungere partner, schemi e accordi per i flussi dei messaggi hello necessarie in cui hello stato esecuzione deve toobe replicati toosecondary area integrazione account.

   > [!TIP]
   > Assicurarsi che sia la coerenza nella convenzione di denominazione dell'elemento di hello integrazione account in aree geografiche. 

3. hello toopull stato di esecuzione dall'area primaria hello, creare un'app logica nell'area secondaria hello. 

   che deve avere un *trigger* e un'*azione*. 
   trigger Hello deve connettersi tooprimary account di integrazione di area e azione hello debba connettersi toosecondary account di integrazione di area. 
   Trigger hello basato su intervallo di tempo hello, esegue il polling tabella dello stato di area primaria eseguire hello ed effettua il pull dei nuovi record hello, se presente. azione di Hello li aggiorna account di integrazione toosecondary area. 
   In questo modo lo stato di runtime incrementale tooget dall'area toosecondary area primaria.

4. Continuità aziendale in App per la logica integrazione account è progettato toosupport basato su protocolli B2B - X12, EDIFACT e AS2. passaggi dettagliati toofind, selezionare hello rispettivi collegamenti.

5. Hello raccomandazione è troppo toodeploy tutte le risorse area primaria in un'area secondaria. 

   Risorse di area primaria includono Database SQL di Azure o Azure Cosmos DB, Azure Service Bus e hub di eventi di Azure utilizzata per la messaggistica, gestione API di Azure e funzionalità di Azure logica App hello in Azure App Service.   

6. Stabilire una connessione da un'area secondaria di tooa area primaria. hello toopull stato di esecuzione da un'area primaria, creare un'app logica in un'area secondaria. 

   app per la logica Hello devono avere un trigger e un'azione. 
   trigger Hello deve connettersi l'account di integrazione tooa area primaria. 
   azione Hello deve connettersi l'account di integrazione tooa area secondaria. 
   Trigger hello basato su intervallo di tempo hello, esegue il polling tabella dello stato di area primaria eseguire hello ed effettua il pull dei nuovi record hello, se presente. 
   azione di Hello li aggiorna account di integrazione tooa area secondaria. 
   Questo processo consente di stato di runtime incrementale tooget dall'area secondaria toohello di hello area primaria.

Continuità aziendale in un account di integrazione di App per la logica fornisce supporto basato su protocolli B2B hello X12, AS2 ed EDIFACT. Per informazioni dettagliate sull'uso di X12 e AS2, vedere [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) e [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in questo articolo.

## <a name="fail-over-tooa-secondary-region-during-a-disaster-event"></a>Eseguire il failover area secondaria tooa durante un evento di emergenza

Durante un evento di emergenza, quando l'area primaria hello non è disponibile per la continuità aziendale, area secondaria toohello di traffico diretto. Consente di area secondaria toorecover un business rapidamente funzioni hello toomeet RPO/RTO concordato dai relativi partner. Inoltre riduce al minimo gli sforzi toofail dall'area tooanother un'area. 

È presente una latenza prevista durante la copia di numeri di controllo da un'area secondaria di tooa area primaria. invio controllo generato duplicati tooavoid numeri toopartners durante un evento di emergenza, hello consiglia di numeri di controllo tooincrement hello nei contratti di hello area secondaria utilizzando [i cmdlet di PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).

## <a name="fall-back-tooa-primary-region-post-disaster-event"></a>Eseguire il fallback evento di post-emergenza tooa area primaria

toofall tooa indietro primario area quando è disponibile, seguire questi passaggi:

1. Interrompere l'accettazione dei messaggi dei partner nell'area secondaria hello.  

2. Incrementare i numeri di controllo hello generato per tutti i contratti di area primaria hello utilizzando [i cmdlet di PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).  

3. Traffico diretto dall'area primaria toohello di hello area secondaria.

4. Verificare che app logica hello creato in hello area secondaria per il pull di stato di esecuzione dall'area primaria hello è abilitata.

## <a name="x12"></a>X12 

La continuità aziendale per i documenti EDI X12 si basa sui numeri di controllo:

> [!TIP]
> È inoltre possibile utilizzare hello [X12 quick start modello](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate logica app. Creazione account di integrazione primario e secondario sono prerequisiti toouse hello al modello. Hello modello consente di toocreate due logica App, uno per i numeri di controllo ricevuti e un altro per i numeri di controllo generato. Azioni e i rispettivi trigger vengono create in applicazioni logica hello, connessione hello trigger toohello integrazione primario account e hello azione toohello integrazione secondario.

**Prerequisiti**

tooenable il ripristino di emergenza per i messaggi in ingresso, selezionare le impostazioni di controllo duplicati hello in impostazioni di ricezione dell'accordo X12 hello.

![Selezionare le impostazioni per la verifica dei duplicati](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. Creare un'[app per la logica](../logic-apps/logic-apps-create-a-logic-app.md) nell'area secondaria.    

2. Cercare in **X12** e selezionare **X12 - Quando viene modificato un numero di controllo**.   

   ![Cercare X12](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   trigger Hello richiesto è tooestablish un account di integrazione tooan di connessione. 
   Hello trigger deve essere connesso l'account di integrazione tooa area primaria.

3. Immettere un nome di connessione, selezionare il *account integrazione area primaria* da hello elenco e scegliere **crea**.   

   ![Nome dell'account di integrazione dell'area primaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. Hello **numero sincronizzazione di data/ora toostart controllo** impostazione è facoltativa. Hello **frequenza** può essere impostato troppo**giorno**, **ora**, **minuto**, o **secondo** con un intervallo.   

   ![DateTime e Frequenza](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. Selezionare **Nuovo passaggio** > **Aggiungi un'azione**.

   ![Nuovo passaggio, Aggiungi un'azione](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. Cercare in **X12** e selezionare **X12 - Aggiungi o aggiorna numeri di controllo**.   

   ![Aggiungi o aggiorna numeri di controllo](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. Selezionare un account di integrazione azione tooa area secondaria, tooconnect **Cambia connessione** > **Aggiungi nuova connessione** per un elenco di account di integrazione disponibile in hello. Immettere un nome di connessione, selezionare il *account integrazione area secondaria* da hello elenco e scegliere **crea**. 

   ![Nome dell'account di integrazione dell'area secondaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. Passare tooraw input facendo clic sull'icona di hello in alto a destra.

   ![Input tooraw commutatore](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. Selezionare corpo dalla selezione di contenuto dinamico hello e salvare hello logica app.

   ![Campi per il contenuto dinamico](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   Trigger hello basato su intervallo di tempo hello, esegue il polling hello area primaria ricevuto controllo tabella ed effettua il pull dei nuovi record hello. 
   azione di Hello Aggiorna i record di hello nell'account di integrazione di hello area secondaria. 
   Se non sono disponibili aggiornamenti, come verrà visualizzato lo stato di trigger hello **ignorati**.   

   ![Tabella dei numeri di controllo](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

Basato su intervallo di tempo hello, lo stato di runtime incrementale hello replica da un'area secondaria di tooa area primaria. Durante un evento di emergenza, quando l'area primaria hello non area secondaria di toohello il traffico diretto disponibili per la continuità aziendale. 

## <a name="edifact"></a>EDIFACT 

La continuità aziendale per i documenti EDI EDIFACT si basa sui numeri di controllo.

**Prerequisiti**

tooenable il ripristino di emergenza per i messaggi in ingresso, selezionare le impostazioni di controllo duplicati hello in impostazioni di ricezione del contratto EDIFACT.

![Selezionare le impostazioni per la verifica dei duplicati](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. Creare un'[app per la logica](../logic-apps/logic-apps-create-a-logic-app.md) nell'area secondaria.    

2. Cercare in **EDIFACT** e selezionare **EDIFACT - Quando viene modificato un numero di controllo**.

   ![Cercare EDIFACT](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   trigger Hello richiesto è tooestablish un account di integrazione tooan di connessione. 
   Hello trigger deve essere connesso l'account di integrazione tooa area primaria. 

3. Immettere un nome di connessione, selezionare il *account integrazione area primaria* da hello elenco e scegliere **crea**.    

   ![Nome dell'account di integrazione dell'area primaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. Hello **numero sincronizzazione di data/ora toostart controllo** impostazione è facoltativa. Hello **frequenza** può essere impostato troppo**giorno**, **ora**, **minuto**, o **secondo** con un intervallo.    

   ![DateTime e Frequenza](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. Selezionare **Nuovo passaggio** > **Aggiungi un'azione**.    

   ![Nuovo passaggio, Aggiungi un'azione](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. Cercare in **EDIFACT** e selezionare **EDIFACT - Aggiungi o aggiorna numeri di controllo**.   

   ![Aggiungi o aggiorna numeri di controllo](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. Selezionare un account di integrazione azione tooa area secondaria, tooconnect **Cambia connessione** > **Aggiungi nuova connessione** per un elenco di account di integrazione disponibile in hello. Immettere un nome di connessione, selezionare il *account integrazione area secondaria* da hello elenco e scegliere **crea**.

   ![Nome dell'account di integrazione dell'area secondaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. Passare tooraw input facendo clic sull'icona di hello in alto a destra.

   ![Input tooraw commutatore](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. Selezionare corpo dalla selezione di contenuto dinamico hello e salvare hello logica app.   

   ![Campi per il contenuto dinamico](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   Trigger hello basato su intervallo di tempo hello, esegue il polling hello area primaria ricevuto controllo tabella ed effettua il pull dei nuovi record hello.
   azione di Hello Aggiorna account di integrazione di hello record toohello area secondaria. 
   Se non sono disponibili aggiornamenti, come verrà visualizzato lo stato di trigger hello **ignorati**.

   ![Tabella dei numeri di controllo](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

Basato su intervallo di tempo hello, lo stato di runtime incrementale hello replica da un'area secondaria di tooa area primaria. Durante un evento di emergenza, quando l'area primaria hello non area secondaria di toohello il traffico diretto disponibili per la continuità aziendale. 

## <a name="as2"></a>AS2 

Continuità aziendale per i documenti che usano il protocollo di AS2 hello è basata sull'ID di messaggio hello e valore MIC hello.

> [!TIP]
> È inoltre possibile utilizzare hello [il modello di avvio rapido AS2](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate logica app. Creazione account di integrazione primario e secondario sono prerequisiti toouse hello al modello. modello Hello consente di creare un'applicazione di logica che dispone di un trigger e un'azione. app per la logica Hello crea una connessione da un account di integrazione primario tooa trigger e un account di azione tooa integrazione secondario.

1. Creare un [logica app](../logic-apps/logic-apps-create-a-logic-app.md) nell'area secondaria hello.  

2. Cercare in **AS2** e selezionare **AS2 -When a MIC value is created** (AS2 - Quando viene creato un valore MIC).   

   ![Cercare AS2](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   Un trigger viene richiesto un account di integrazione tooan tooestablish. 
   Hello trigger deve essere connesso l'account di integrazione tooa area primaria. 
   
3. Immettere un nome di connessione, selezionare il *account integrazione area primaria* da hello elenco e scegliere **crea**.

   ![Nome dell'account di integrazione dell'area primaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. Hello **sincronizzazione di valore DateTime toostart MIC** impostazione è facoltativa. Hello **frequenza** può essere impostato troppo**giorno**, **ora**, **minuto**, o **secondo** con un intervallo.   

   ![DateTime e Frequenza](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. Selezionare **Nuovo passaggio** > **Aggiungi un'azione**.  

   ![Nuovo passaggio, Aggiungi un'azione](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. Cercare in **AS2** e selezionare **AS2 - Add or update MIC contents** (AS2 - Aggiungi o aggiorna contenuti MIC).  

   ![Aggiunta o aggiornamento MIC](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. tooconnect account azione tooa integrazione secondario, selezionare **Cambia connessione** > **Aggiungi nuova connessione** per un elenco di account di integrazione disponibile in hello. Immettere un nome di connessione, selezionare il *account integrazione area secondaria* da hello elenco e scegliere **crea**.

   ![Nome dell'account di integrazione dell'area secondaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. Passare tooraw input facendo clic sull'icona di hello in alto a destra.

   ![Input tooraw commutatore](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. Selezionare corpo dalla selezione di contenuto dinamico hello e salvare hello logica app.   

   ![Contenuto dinamico](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   Trigger hello basato su intervallo di tempo hello, esegue il polling tabella area primaria hello ed effettua il pull dei nuovi record hello. azione di Hello li aggiorna account di integrazione toohello area secondaria. 
   Se non sono disponibili aggiornamenti, come verrà visualizzato lo stato di trigger hello **ignorati**.  

   ![Tabella dell'area primaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

Basato su intervallo di tempo hello, lo stato di runtime incrementale hello replica dall'area secondaria toohello di hello area primaria. Durante un evento di emergenza, quando l'area primaria hello non area secondaria di toohello il traffico diretto disponibili per la continuità aziendale. 

## <a name="next-steps"></a>Passaggi successivi

[Monitorare i messaggi B2B](logic-apps-monitor-b2b-message.md)

