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
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a><span data-ttu-id="43140-103">Ripristino di emergenza tra più aree delle app per la logica B2B</span><span class="sxs-lookup"><span data-stu-id="43140-103">Logic Apps B2B cross-region disaster recovery</span></span>

<span data-ttu-id="43140-104">I carichi di lavoro B2B coinvolgono le transazioni di denaro, come ad esempio gli ordini e le fatture.</span><span class="sxs-lookup"><span data-stu-id="43140-104">B2B workloads involve money transactions like orders and invoices.</span></span> <span data-ttu-id="43140-105">Durante un evento di emergenza, è fondamentale per un hello toomeet di business tooquickly Ripristina che i contratti di servizio a livello aziendale concordati con i partner.</span><span class="sxs-lookup"><span data-stu-id="43140-105">During a disaster event, it's critical for a business tooquickly recover toomeet hello business-level SLAs agreed upon with their partners.</span></span> <span data-ttu-id="43140-106">In questo articolo viene illustrato come toobuild continuità aziendale un piano per i carichi di lavoro B2B.</span><span class="sxs-lookup"><span data-stu-id="43140-106">This article demonstrates how toobuild a business continuity plan for B2B workloads.</span></span> 

* <span data-ttu-id="43140-107">Preparazione al ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="43140-107">Disaster Recovery readiness</span></span> 
* <span data-ttu-id="43140-108">Eseguire il failover toosecondary area durante un evento di emergenza</span><span class="sxs-lookup"><span data-stu-id="43140-108">Fail over toosecondary region during a disaster event</span></span> 
* <span data-ttu-id="43140-109">Eseguire il fallback tooprimary area dopo un evento di emergenza</span><span class="sxs-lookup"><span data-stu-id="43140-109">Fall back tooprimary region after a disaster event</span></span>

## <a name="disaster-recovery-readiness"></a><span data-ttu-id="43140-110">Preparazione al ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="43140-110">Disaster Recovery readiness</span></span>  

1. <span data-ttu-id="43140-111">Identifica un'area secondaria e creare un [account integrazione](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) nell'area secondaria hello.</span><span class="sxs-lookup"><span data-stu-id="43140-111">Identify a secondary region and create an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) in hello secondary region.</span></span>

2. <span data-ttu-id="43140-112">Aggiungere partner, schemi e accordi per i flussi dei messaggi hello necessarie in cui hello stato esecuzione deve toobe replicati toosecondary area integrazione account.</span><span class="sxs-lookup"><span data-stu-id="43140-112">Add partners, schemas, and agreements for hello required message flows where hello run status needs toobe replicated toosecondary region integration account.</span></span>

   > [!TIP]
   > <span data-ttu-id="43140-113">Assicurarsi che sia la coerenza nella convenzione di denominazione dell'elemento di hello integrazione account in aree geografiche.</span><span class="sxs-lookup"><span data-stu-id="43140-113">Make sure there's consistency in hello integration account artifact's naming convention across regions.</span></span> 

3. <span data-ttu-id="43140-114">hello toopull stato di esecuzione dall'area primaria hello, creare un'app logica nell'area secondaria hello.</span><span class="sxs-lookup"><span data-stu-id="43140-114">toopull hello run status from hello primary region, create a logic app in hello secondary region.</span></span> 

   <span data-ttu-id="43140-115">che deve avere un *trigger* e un'*azione*.</span><span class="sxs-lookup"><span data-stu-id="43140-115">This logic app should have a *trigger* and an *action*.</span></span> 
   <span data-ttu-id="43140-116">trigger Hello deve connettersi tooprimary account di integrazione di area e azione hello debba connettersi toosecondary account di integrazione di area.</span><span class="sxs-lookup"><span data-stu-id="43140-116">hello trigger should connect tooprimary region integration account, and hello action should connect toosecondary region integration account.</span></span> 
   <span data-ttu-id="43140-117">Trigger hello basato su intervallo di tempo hello, esegue il polling tabella dello stato di area primaria eseguire hello ed effettua il pull dei nuovi record hello, se presente.</span><span class="sxs-lookup"><span data-stu-id="43140-117">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> <span data-ttu-id="43140-118">azione di Hello li aggiorna account di integrazione toosecondary area.</span><span class="sxs-lookup"><span data-stu-id="43140-118">hello action updates them toosecondary region integration account.</span></span> 
   <span data-ttu-id="43140-119">In questo modo lo stato di runtime incrementale tooget dall'area toosecondary area primaria.</span><span class="sxs-lookup"><span data-stu-id="43140-119">This helps tooget incremental runtime status from primary region toosecondary region.</span></span>

4. <span data-ttu-id="43140-120">Continuità aziendale in App per la logica integrazione account è progettato toosupport basato su protocolli B2B - X12, EDIFACT e AS2.</span><span class="sxs-lookup"><span data-stu-id="43140-120">Business continuity in Logic Apps integration account is designed toosupport based on B2B protocols - X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="43140-121">passaggi dettagliati toofind, selezionare hello rispettivi collegamenti.</span><span class="sxs-lookup"><span data-stu-id="43140-121">toofind detailed steps, select hello respective links.</span></span>

5. <span data-ttu-id="43140-122">Hello raccomandazione è troppo toodeploy tutte le risorse area primaria in un'area secondaria.</span><span class="sxs-lookup"><span data-stu-id="43140-122">hello recommendation is toodeploy all primary region resources in a secondary region too.</span></span> 

   <span data-ttu-id="43140-123">Risorse di area primaria includono Database SQL di Azure o Azure Cosmos DB, Azure Service Bus e hub di eventi di Azure utilizzata per la messaggistica, gestione API di Azure e funzionalità di Azure logica App hello in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="43140-123">Primary region resources include Azure SQL Database or Azure Cosmos DB, Azure Service Bus and Azure Event Hubs used for messaging, Azure API Management, and hello Azure Logic Apps feature in Azure App Service.</span></span>   

6. <span data-ttu-id="43140-124">Stabilire una connessione da un'area secondaria di tooa area primaria.</span><span class="sxs-lookup"><span data-stu-id="43140-124">Establish a connection from a primary region tooa secondary region.</span></span> <span data-ttu-id="43140-125">hello toopull stato di esecuzione da un'area primaria, creare un'app logica in un'area secondaria.</span><span class="sxs-lookup"><span data-stu-id="43140-125">toopull hello run status from a primary region, create a logic app in a secondary region.</span></span> 

   <span data-ttu-id="43140-126">app per la logica Hello devono avere un trigger e un'azione.</span><span class="sxs-lookup"><span data-stu-id="43140-126">hello logic app should have a trigger and an action.</span></span> 
   <span data-ttu-id="43140-127">trigger Hello deve connettersi l'account di integrazione tooa area primaria.</span><span class="sxs-lookup"><span data-stu-id="43140-127">hello trigger should connect tooa primary region integration account.</span></span> 
   <span data-ttu-id="43140-128">azione Hello deve connettersi l'account di integrazione tooa area secondaria.</span><span class="sxs-lookup"><span data-stu-id="43140-128">hello action should connect tooa secondary region integration account.</span></span> 
   <span data-ttu-id="43140-129">Trigger hello basato su intervallo di tempo hello, esegue il polling tabella dello stato di area primaria eseguire hello ed effettua il pull dei nuovi record hello, se presente.</span><span class="sxs-lookup"><span data-stu-id="43140-129">Based on hello time interval, hello trigger polls hello primary region run status table and pulls hello new records, if any.</span></span> 
   <span data-ttu-id="43140-130">azione di Hello li aggiorna account di integrazione tooa area secondaria.</span><span class="sxs-lookup"><span data-stu-id="43140-130">hello action updates them tooa secondary region integration account.</span></span> 
   <span data-ttu-id="43140-131">Questo processo consente di stato di runtime incrementale tooget dall'area secondaria toohello di hello area primaria.</span><span class="sxs-lookup"><span data-stu-id="43140-131">This process helps tooget incremental runtime status from hello primary region toohello secondary region.</span></span>

<span data-ttu-id="43140-132">Continuità aziendale in un account di integrazione di App per la logica fornisce supporto basato su protocolli B2B hello X12, AS2 ed EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="43140-132">Business continuity in a Logic Apps integration account provides support based on hello B2B protocols X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="43140-133">Per informazioni dettagliate sull'uso di X12 e AS2, vedere [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) e [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="43140-133">For detailed steps on using X12 and AS2, see [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) and [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in this article.</span></span>

## <a name="fail-over-tooa-secondary-region-during-a-disaster-event"></a><span data-ttu-id="43140-134">Eseguire il failover area secondaria tooa durante un evento di emergenza</span><span class="sxs-lookup"><span data-stu-id="43140-134">Fail over tooa secondary region during a disaster event</span></span>

<span data-ttu-id="43140-135">Durante un evento di emergenza, quando l'area primaria hello non è disponibile per la continuità aziendale, area secondaria toohello di traffico diretto.</span><span class="sxs-lookup"><span data-stu-id="43140-135">During a disaster event, when hello primary region is not available for business continuity, direct traffic toohello secondary region.</span></span> <span data-ttu-id="43140-136">Consente di area secondaria toorecover un business rapidamente funzioni hello toomeet RPO/RTO concordato dai relativi partner.</span><span class="sxs-lookup"><span data-stu-id="43140-136">A secondary region helps a business toorecover functions quickly toomeet hello RPO/RTO agreed upon by their partners.</span></span> <span data-ttu-id="43140-137">Inoltre riduce al minimo gli sforzi toofail dall'area tooanother un'area.</span><span class="sxs-lookup"><span data-stu-id="43140-137">It also minimizes efforts toofail over from one region tooanother region.</span></span> 

<span data-ttu-id="43140-138">È presente una latenza prevista durante la copia di numeri di controllo da un'area secondaria di tooa area primaria.</span><span class="sxs-lookup"><span data-stu-id="43140-138">There is an expected latency while copying control numbers from a primary region tooa secondary region.</span></span> <span data-ttu-id="43140-139">invio controllo generato duplicati tooavoid numeri toopartners durante un evento di emergenza, hello consiglia di numeri di controllo tooincrement hello nei contratti di hello area secondaria utilizzando [i cmdlet di PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="43140-139">tooavoid sending duplicate generated control numbers toopartners during a disaster event, hello recommendation is tooincrement hello control numbers in hello secondary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>

## <a name="fall-back-tooa-primary-region-post-disaster-event"></a><span data-ttu-id="43140-140">Eseguire il fallback evento di post-emergenza tooa area primaria</span><span class="sxs-lookup"><span data-stu-id="43140-140">Fall back tooa primary region post-disaster event</span></span>

<span data-ttu-id="43140-141">toofall tooa indietro primario area quando è disponibile, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="43140-141">toofall back tooa primary region when it is available, follow these steps:</span></span>

1. <span data-ttu-id="43140-142">Interrompere l'accettazione dei messaggi dei partner nell'area secondaria hello.</span><span class="sxs-lookup"><span data-stu-id="43140-142">Stop accepting messages from partners in hello secondary region.</span></span>  

2. <span data-ttu-id="43140-143">Incrementare i numeri di controllo hello generato per tutti i contratti di area primaria hello utilizzando [i cmdlet di PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="43140-143">Increment hello generated control numbers for all hello primary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>  

3. <span data-ttu-id="43140-144">Traffico diretto dall'area primaria toohello di hello area secondaria.</span><span class="sxs-lookup"><span data-stu-id="43140-144">Direct traffic from hello secondary region toohello primary region.</span></span>

4. <span data-ttu-id="43140-145">Verificare che app logica hello creato in hello area secondaria per il pull di stato di esecuzione dall'area primaria hello è abilitata.</span><span class="sxs-lookup"><span data-stu-id="43140-145">Check that hello logic app created in hello secondary region for pulling run status from hello primary region is enabled.</span></span>

## <a name="x12"></a><span data-ttu-id="43140-146">X12</span><span class="sxs-lookup"><span data-stu-id="43140-146">X12</span></span> 

<span data-ttu-id="43140-147">La continuità aziendale per i documenti EDI X12 si basa sui numeri di controllo:</span><span class="sxs-lookup"><span data-stu-id="43140-147">Business continuity for EDI X12 documents is based on control numbers:</span></span>

> [!TIP]
> <span data-ttu-id="43140-148">È inoltre possibile utilizzare hello [X12 quick start modello](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate logica app.</span><span class="sxs-lookup"><span data-stu-id="43140-148">You can also use hello [X12 quick start template](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate logic apps.</span></span> <span data-ttu-id="43140-149">Creazione account di integrazione primario e secondario sono prerequisiti toouse hello al modello.</span><span class="sxs-lookup"><span data-stu-id="43140-149">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="43140-150">Hello modello consente di toocreate due logica App, uno per i numeri di controllo ricevuti e un altro per i numeri di controllo generato.</span><span class="sxs-lookup"><span data-stu-id="43140-150">hello template helps toocreate two logic apps, one for received control numbers and another for generated control numbers.</span></span> <span data-ttu-id="43140-151">Azioni e i rispettivi trigger vengono create in applicazioni logica hello, connessione hello trigger toohello integrazione primario account e hello azione toohello integrazione secondario.</span><span class="sxs-lookup"><span data-stu-id="43140-151">Respective triggers and actions are created in hello logic apps, connecting hello trigger toohello primary integration account and hello action toohello secondary integration account.</span></span>

<span data-ttu-id="43140-152">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="43140-152">**Prerequisites**</span></span>

<span data-ttu-id="43140-153">tooenable il ripristino di emergenza per i messaggi in ingresso, selezionare le impostazioni di controllo duplicati hello in impostazioni di ricezione dell'accordo X12 hello.</span><span class="sxs-lookup"><span data-stu-id="43140-153">tooenable disaster recovery for inbound messages, select hello duplicate check settings in hello X12 agreement's Receive Settings.</span></span>

![Selezionare le impostazioni per la verifica dei duplicati](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. <span data-ttu-id="43140-155">Creare un'[app per la logica](../logic-apps/logic-apps-create-a-logic-app.md) nell'area secondaria.</span><span class="sxs-lookup"><span data-stu-id="43140-155">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="43140-156">Cercare in **X12** e selezionare **X12 - Quando viene modificato un numero di controllo**.</span><span class="sxs-lookup"><span data-stu-id="43140-156">Search on **X12**, and select **X12 - When a control number is modified**.</span></span>   

   ![Cercare X12](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   <span data-ttu-id="43140-158">trigger Hello richiesto è tooestablish un account di integrazione tooan di connessione.</span><span class="sxs-lookup"><span data-stu-id="43140-158">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="43140-159">Hello trigger deve essere connesso l'account di integrazione tooa area primaria.</span><span class="sxs-lookup"><span data-stu-id="43140-159">hello trigger should be connected tooa primary region integration account.</span></span>

3. <span data-ttu-id="43140-160">Immettere un nome di connessione, selezionare il *account integrazione area primaria* da hello elenco e scegliere **crea**.</span><span class="sxs-lookup"><span data-stu-id="43140-160">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>   

   ![Nome dell'account di integrazione dell'area primaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. <span data-ttu-id="43140-162">Hello **numero sincronizzazione di data/ora toostart controllo** impostazione è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="43140-162">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="43140-163">Hello **frequenza** può essere impostato troppo**giorno**, **ora**, **minuto**, o **secondo** con un intervallo.</span><span class="sxs-lookup"><span data-stu-id="43140-163">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![DateTime e Frequenza](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. <span data-ttu-id="43140-165">Selezionare **Nuovo passaggio** > **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="43140-165">Select **New step** > **Add an action**.</span></span>

   ![Nuovo passaggio, Aggiungi un'azione](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. <span data-ttu-id="43140-167">Cercare in **X12** e selezionare **X12 - Aggiungi o aggiorna numeri di controllo**.</span><span class="sxs-lookup"><span data-stu-id="43140-167">Search on **X12**, and select **X12 - Add or update control numbers**.</span></span>   

   ![Aggiungi o aggiorna numeri di controllo](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. <span data-ttu-id="43140-169">Selezionare un account di integrazione azione tooa area secondaria, tooconnect **Cambia connessione** > **Aggiungi nuova connessione** per un elenco di account di integrazione disponibile in hello.</span><span class="sxs-lookup"><span data-stu-id="43140-169">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="43140-170">Immettere un nome di connessione, selezionare il *account integrazione area secondaria* da hello elenco e scegliere **crea**.</span><span class="sxs-lookup"><span data-stu-id="43140-170">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span> 

   ![Nome dell'account di integrazione dell'area secondaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. <span data-ttu-id="43140-172">Passare tooraw input facendo clic sull'icona di hello in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="43140-172">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Input tooraw commutatore](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. <span data-ttu-id="43140-174">Selezionare corpo dalla selezione di contenuto dinamico hello e salvare hello logica app.</span><span class="sxs-lookup"><span data-stu-id="43140-174">Select Body from hello dynamic content picker, and save hello logic app.</span></span>

   ![Campi per il contenuto dinamico](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   <span data-ttu-id="43140-176">Trigger hello basato su intervallo di tempo hello, esegue il polling hello area primaria ricevuto controllo tabella ed effettua il pull dei nuovi record hello.</span><span class="sxs-lookup"><span data-stu-id="43140-176">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span> 
   <span data-ttu-id="43140-177">azione di Hello Aggiorna i record di hello nell'account di integrazione di hello area secondaria.</span><span class="sxs-lookup"><span data-stu-id="43140-177">hello action updates hello records in hello secondary region integration account.</span></span> 
   <span data-ttu-id="43140-178">Se non sono disponibili aggiornamenti, come verrà visualizzato lo stato di trigger hello **ignorati**.</span><span class="sxs-lookup"><span data-stu-id="43140-178">If there are no updates, hello trigger status appears as **Skipped**.</span></span>   

   ![Tabella dei numeri di controllo](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="43140-180">Basato su intervallo di tempo hello, lo stato di runtime incrementale hello replica da un'area secondaria di tooa area primaria.</span><span class="sxs-lookup"><span data-stu-id="43140-180">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="43140-181">Durante un evento di emergenza, quando l'area primaria hello non area secondaria di toohello il traffico diretto disponibili per la continuità aziendale.</span><span class="sxs-lookup"><span data-stu-id="43140-181">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="edifact"></a><span data-ttu-id="43140-182">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="43140-182">EDIFACT</span></span> 

<span data-ttu-id="43140-183">La continuità aziendale per i documenti EDI EDIFACT si basa sui numeri di controllo.</span><span class="sxs-lookup"><span data-stu-id="43140-183">Business continuity for EDI EDIFACT documents is based on control numbers.</span></span>

<span data-ttu-id="43140-184">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="43140-184">**Prerequisites**</span></span>

<span data-ttu-id="43140-185">tooenable il ripristino di emergenza per i messaggi in ingresso, selezionare le impostazioni di controllo duplicati hello in impostazioni di ricezione del contratto EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="43140-185">tooenable disaster recovery for inbound messages, select hello duplicate check settings in your EDIFACT agreement's Receive Settings.</span></span>

![Selezionare le impostazioni per la verifica dei duplicati](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. <span data-ttu-id="43140-187">Creare un'[app per la logica](../logic-apps/logic-apps-create-a-logic-app.md) nell'area secondaria.</span><span class="sxs-lookup"><span data-stu-id="43140-187">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="43140-188">Cercare in **EDIFACT** e selezionare **EDIFACT - Quando viene modificato un numero di controllo**.</span><span class="sxs-lookup"><span data-stu-id="43140-188">Search on **EDIFACT**, and select **EDIFACT - When a control number is modified**.</span></span>

   ![Cercare EDIFACT](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   <span data-ttu-id="43140-190">trigger Hello richiesto è tooestablish un account di integrazione tooan di connessione.</span><span class="sxs-lookup"><span data-stu-id="43140-190">hello trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="43140-191">Hello trigger deve essere connesso l'account di integrazione tooa area primaria.</span><span class="sxs-lookup"><span data-stu-id="43140-191">hello trigger should be connected tooa primary region integration account.</span></span> 

3. <span data-ttu-id="43140-192">Immettere un nome di connessione, selezionare il *account integrazione area primaria* da hello elenco e scegliere **crea**.</span><span class="sxs-lookup"><span data-stu-id="43140-192">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>    

   ![Nome dell'account di integrazione dell'area primaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. <span data-ttu-id="43140-194">Hello **numero sincronizzazione di data/ora toostart controllo** impostazione è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="43140-194">hello **DateTime toostart control number sync** setting is optional.</span></span> <span data-ttu-id="43140-195">Hello **frequenza** può essere impostato troppo**giorno**, **ora**, **minuto**, o **secondo** con un intervallo.</span><span class="sxs-lookup"><span data-stu-id="43140-195">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>    

   ![DateTime e Frequenza](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. <span data-ttu-id="43140-197">Selezionare **Nuovo passaggio** > **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="43140-197">Select **New step** > **Add an action**.</span></span>    

   ![Nuovo passaggio, Aggiungi un'azione](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. <span data-ttu-id="43140-199">Cercare in **EDIFACT** e selezionare **EDIFACT - Aggiungi o aggiorna numeri di controllo**.</span><span class="sxs-lookup"><span data-stu-id="43140-199">Search on **EDIFACT**, and select **EDIFACT - Add or update control numbers**.</span></span>   

   ![Aggiungi o aggiorna numeri di controllo](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. <span data-ttu-id="43140-201">Selezionare un account di integrazione azione tooa area secondaria, tooconnect **Cambia connessione** > **Aggiungi nuova connessione** per un elenco di account di integrazione disponibile in hello.</span><span class="sxs-lookup"><span data-stu-id="43140-201">tooconnect an action tooa secondary region integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="43140-202">Immettere un nome di connessione, selezionare il *account integrazione area secondaria* da hello elenco e scegliere **crea**.</span><span class="sxs-lookup"><span data-stu-id="43140-202">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![Nome dell'account di integrazione dell'area secondaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. <span data-ttu-id="43140-204">Passare tooraw input facendo clic sull'icona di hello in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="43140-204">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Input tooraw commutatore](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. <span data-ttu-id="43140-206">Selezionare corpo dalla selezione di contenuto dinamico hello e salvare hello logica app.</span><span class="sxs-lookup"><span data-stu-id="43140-206">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![Campi per il contenuto dinamico](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   <span data-ttu-id="43140-208">Trigger hello basato su intervallo di tempo hello, esegue il polling hello area primaria ricevuto controllo tabella ed effettua il pull dei nuovi record hello.</span><span class="sxs-lookup"><span data-stu-id="43140-208">Based on hello time interval, hello trigger polls hello primary region received control number table and pulls hello new records.</span></span>
   <span data-ttu-id="43140-209">azione di Hello Aggiorna account di integrazione di hello record toohello area secondaria.</span><span class="sxs-lookup"><span data-stu-id="43140-209">hello action updates hello records toohello secondary region integration account.</span></span> 
   <span data-ttu-id="43140-210">Se non sono disponibili aggiornamenti, come verrà visualizzato lo stato di trigger hello **ignorati**.</span><span class="sxs-lookup"><span data-stu-id="43140-210">If there are no updates, hello trigger status appears as **Skipped**.</span></span>

   ![Tabella dei numeri di controllo](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="43140-212">Basato su intervallo di tempo hello, lo stato di runtime incrementale hello replica da un'area secondaria di tooa area primaria.</span><span class="sxs-lookup"><span data-stu-id="43140-212">Based on hello time interval, hello incremental runtime status replicates from a primary region tooa secondary region.</span></span> <span data-ttu-id="43140-213">Durante un evento di emergenza, quando l'area primaria hello non area secondaria di toohello il traffico diretto disponibili per la continuità aziendale.</span><span class="sxs-lookup"><span data-stu-id="43140-213">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="as2"></a><span data-ttu-id="43140-214">AS2</span><span class="sxs-lookup"><span data-stu-id="43140-214">AS2</span></span> 

<span data-ttu-id="43140-215">Continuità aziendale per i documenti che usano il protocollo di AS2 hello è basata sull'ID di messaggio hello e valore MIC hello.</span><span class="sxs-lookup"><span data-stu-id="43140-215">Business continuity for documents that use hello AS2 protocol is based on hello message ID and hello MIC value.</span></span>

> [!TIP]
> <span data-ttu-id="43140-216">È inoltre possibile utilizzare hello [il modello di avvio rapido AS2](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate logica app.</span><span class="sxs-lookup"><span data-stu-id="43140-216">You can also use hello [AS2 quick start template](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate logic apps.</span></span> <span data-ttu-id="43140-217">Creazione account di integrazione primario e secondario sono prerequisiti toouse hello al modello.</span><span class="sxs-lookup"><span data-stu-id="43140-217">Creating primary and secondary integration accounts are prerequisites toouse hello template.</span></span> <span data-ttu-id="43140-218">modello Hello consente di creare un'applicazione di logica che dispone di un trigger e un'azione.</span><span class="sxs-lookup"><span data-stu-id="43140-218">hello template helps create a logic app that has a trigger and an action.</span></span> <span data-ttu-id="43140-219">app per la logica Hello crea una connessione da un account di integrazione primario tooa trigger e un account di azione tooa integrazione secondario.</span><span class="sxs-lookup"><span data-stu-id="43140-219">hello logic app creates a connection from a trigger tooa primary integration account and an action tooa secondary integration account.</span></span>

1. <span data-ttu-id="43140-220">Creare un [logica app](../logic-apps/logic-apps-create-a-logic-app.md) nell'area secondaria hello.</span><span class="sxs-lookup"><span data-stu-id="43140-220">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in hello secondary region.</span></span>  

2. <span data-ttu-id="43140-221">Cercare in **AS2** e selezionare **AS2 -When a MIC value is created** (AS2 - Quando viene creato un valore MIC).</span><span class="sxs-lookup"><span data-stu-id="43140-221">Search on **AS2**, and select **AS2 - When a MIC value is created**.</span></span>   

   ![Cercare AS2](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   <span data-ttu-id="43140-223">Un trigger viene richiesto un account di integrazione tooan tooestablish.</span><span class="sxs-lookup"><span data-stu-id="43140-223">A trigger prompts you tooestablish a connection tooan integration account.</span></span> 
   <span data-ttu-id="43140-224">Hello trigger deve essere connesso l'account di integrazione tooa area primaria.</span><span class="sxs-lookup"><span data-stu-id="43140-224">hello trigger should be connected tooa primary region integration account.</span></span> 
   
3. <span data-ttu-id="43140-225">Immettere un nome di connessione, selezionare il *account integrazione area primaria* da hello elenco e scegliere **crea**.</span><span class="sxs-lookup"><span data-stu-id="43140-225">Enter a connection name, select your *primary region integration account* from hello list, and choose **Create**.</span></span>

   ![Nome dell'account di integrazione dell'area primaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. <span data-ttu-id="43140-227">Hello **sincronizzazione di valore DateTime toostart MIC** impostazione è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="43140-227">hello **DateTime toostart MIC value sync** setting is optional.</span></span> <span data-ttu-id="43140-228">Hello **frequenza** può essere impostato troppo**giorno**, **ora**, **minuto**, o **secondo** con un intervallo.</span><span class="sxs-lookup"><span data-stu-id="43140-228">hello **Frequency** can be set too**Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![DateTime e Frequenza](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. <span data-ttu-id="43140-230">Selezionare **Nuovo passaggio** > **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="43140-230">Select **New step** > **Add an action**.</span></span>  

   ![Nuovo passaggio, Aggiungi un'azione](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. <span data-ttu-id="43140-232">Cercare in **AS2** e selezionare **AS2 - Add or update MIC contents** (AS2 - Aggiungi o aggiorna contenuti MIC).</span><span class="sxs-lookup"><span data-stu-id="43140-232">Search on **AS2**, and select **AS2 - Add or update MIC contents**.</span></span>  

   ![Aggiunta o aggiornamento MIC](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. <span data-ttu-id="43140-234">tooconnect account azione tooa integrazione secondario, selezionare **Cambia connessione** > **Aggiungi nuova connessione** per un elenco di account di integrazione disponibile in hello.</span><span class="sxs-lookup"><span data-stu-id="43140-234">tooconnect an action tooa secondary integration account, select **Change connection** > **Add new connection** for a list of hello available integration accounts.</span></span> <span data-ttu-id="43140-235">Immettere un nome di connessione, selezionare il *account integrazione area secondaria* da hello elenco e scegliere **crea**.</span><span class="sxs-lookup"><span data-stu-id="43140-235">Enter a connection name, select your *secondary region integration account* from hello list, and choose **Create**.</span></span>

   ![Nome dell'account di integrazione dell'area secondaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. <span data-ttu-id="43140-237">Passare tooraw input facendo clic sull'icona di hello in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="43140-237">Switch tooraw inputs by clicking on hello icon in upper right corner.</span></span>

   ![Input tooraw commutatore](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. <span data-ttu-id="43140-239">Selezionare corpo dalla selezione di contenuto dinamico hello e salvare hello logica app.</span><span class="sxs-lookup"><span data-stu-id="43140-239">Select Body from hello dynamic content picker, and save hello logic app.</span></span>   

   ![Contenuto dinamico](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   <span data-ttu-id="43140-241">Trigger hello basato su intervallo di tempo hello, esegue il polling tabella area primaria hello ed effettua il pull dei nuovi record hello.</span><span class="sxs-lookup"><span data-stu-id="43140-241">Based on hello time interval, hello trigger polls hello primary region table and pulls hello new records.</span></span> <span data-ttu-id="43140-242">azione di Hello li aggiorna account di integrazione toohello area secondaria.</span><span class="sxs-lookup"><span data-stu-id="43140-242">hello action updates them toohello secondary region integration account.</span></span> 
   <span data-ttu-id="43140-243">Se non sono disponibili aggiornamenti, come verrà visualizzato lo stato di trigger hello **ignorati**.</span><span class="sxs-lookup"><span data-stu-id="43140-243">If there are no updates, hello trigger status appears as **Skipped**.</span></span>  

   ![Tabella dell'area primaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

<span data-ttu-id="43140-245">Basato su intervallo di tempo hello, lo stato di runtime incrementale hello replica dall'area secondaria toohello di hello area primaria.</span><span class="sxs-lookup"><span data-stu-id="43140-245">Based on hello time interval, hello incremental runtime status replicates from hello primary region toohello secondary region.</span></span> <span data-ttu-id="43140-246">Durante un evento di emergenza, quando l'area primaria hello non area secondaria di toohello il traffico diretto disponibili per la continuità aziendale.</span><span class="sxs-lookup"><span data-stu-id="43140-246">During a disaster event, when hello primary region is not available, direct traffic toohello secondary region for business continuity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="43140-247">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="43140-247">Next steps</span></span>

[<span data-ttu-id="43140-248">Monitorare i messaggi B2B</span><span class="sxs-lookup"><span data-stu-id="43140-248">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md)

