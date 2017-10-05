---
title: 'Ripristino di emergenza per l''account di integrazione B2B: App per la logica di Azure | Microsoft Docs'
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
ms.openlocfilehash: 4896d9da456bcc17b1a4d92259ef3d57f8575d8b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a><span data-ttu-id="31bd9-103">Ripristino di emergenza tra più aree delle app per la logica B2B</span><span class="sxs-lookup"><span data-stu-id="31bd9-103">Logic Apps B2B cross-region disaster recovery</span></span>

<span data-ttu-id="31bd9-104">I carichi di lavoro B2B coinvolgono le transazioni di denaro, come ad esempio gli ordini e le fatture.</span><span class="sxs-lookup"><span data-stu-id="31bd9-104">B2B workloads involve money transactions like orders and invoices.</span></span> <span data-ttu-id="31bd9-105">In caso di un evento di emergenza, per un'azienda è essenziale eseguire rapidamente un ripristino per soddisfare i contratti di servizio a livello di business secondo gli accordi presi con i partner.</span><span class="sxs-lookup"><span data-stu-id="31bd9-105">During a disaster event, it's critical for a business to quickly recover to meet the business-level SLAs agreed upon with their partners.</span></span> <span data-ttu-id="31bd9-106">In questo articolo viene illustrato come creare un piano di continuità aziendale per i carichi di lavoro B2B.</span><span class="sxs-lookup"><span data-stu-id="31bd9-106">This article demonstrates how to build a business continuity plan for B2B workloads.</span></span> 

* <span data-ttu-id="31bd9-107">Preparazione al ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="31bd9-107">Disaster Recovery readiness</span></span> 
* <span data-ttu-id="31bd9-108">Eseguire il failover all'area secondaria durante un evento di emergenza</span><span class="sxs-lookup"><span data-stu-id="31bd9-108">Fail over to secondary region during a disaster event</span></span> 
* <span data-ttu-id="31bd9-109">Eseguire il failover all'area primaria dopo un evento di emergenza</span><span class="sxs-lookup"><span data-stu-id="31bd9-109">Fall back to primary region after a disaster event</span></span>

## <a name="disaster-recovery-readiness"></a><span data-ttu-id="31bd9-110">Preparazione al ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="31bd9-110">Disaster Recovery readiness</span></span>  

1. <span data-ttu-id="31bd9-111">Identificare un'area secondaria e crearvi un [account di integrazione](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md).</span><span class="sxs-lookup"><span data-stu-id="31bd9-111">Identify a secondary region and create an [integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) in the secondary region.</span></span>

2. <span data-ttu-id="31bd9-112">Aggiungere partner, schemi e contratti per i flussi di messaggi richiesti dove lo stato di esecuzione deve essere replicato nell'account di integrazione dell'area secondaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-112">Add partners, schemas, and agreements for the required message flows where the run status needs to be replicated to secondary region integration account.</span></span>

   > [!TIP]
   > <span data-ttu-id="31bd9-113">Assicurare la coerenza degli elementi dell'account di integrazione secondo la convenzione di denominazione nelle aree.</span><span class="sxs-lookup"><span data-stu-id="31bd9-113">Make sure there's consistency in the integration account artifact's naming convention across regions.</span></span> 

3. <span data-ttu-id="31bd9-114">Per eseguire il pull dello stato di esecuzione dall'area primaria, creare un'app per la logica nell'area secondaria,</span><span class="sxs-lookup"><span data-stu-id="31bd9-114">To pull the run status from the primary region, create a logic app in the secondary region.</span></span> 

   <span data-ttu-id="31bd9-115">che deve avere un *trigger* e un'*azione*.</span><span class="sxs-lookup"><span data-stu-id="31bd9-115">This logic app should have a *trigger* and an *action*.</span></span> 
   <span data-ttu-id="31bd9-116">Il trigger deve connettersi all'account di integrazione dell'area primaria, mentre l'azione deve connettersi all'account di integrazione dell'area secondaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-116">The trigger should connect to primary region integration account, and the action should connect to secondary region integration account.</span></span> 
   <span data-ttu-id="31bd9-117">In base all'intervallo di tempo, il trigger esegue il sondaggio della tabella sullo stato di esecuzione dell'area primaria ed esegue il pull dei nuovi record, se presenti.</span><span class="sxs-lookup"><span data-stu-id="31bd9-117">Based on the time interval, the trigger polls the primary region run status table and pulls the new records, if any.</span></span> <span data-ttu-id="31bd9-118">L'azione li aggiorna nell'account di integrazione dell'area secondaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-118">The action updates them to secondary region integration account.</span></span> 
   <span data-ttu-id="31bd9-119">Questa operazione consente di ottenere lo stato di runtime incrementale dall'area primaria a quella secondaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-119">This helps to get incremental runtime status from primary region to secondary region.</span></span>

4. <span data-ttu-id="31bd9-120">La continuità aziendale nell'account di integrazione delle app per la logica è pensata per il supporto basato sui protocolli B2B - X12, AS2 ed EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="31bd9-120">Business continuity in Logic Apps integration account is designed to support based on B2B protocols - X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="31bd9-121">Per trovare la procedura dettagliata, selezionare i rispettivi collegamenti.</span><span class="sxs-lookup"><span data-stu-id="31bd9-121">To find detailed steps, select the respective links.</span></span>

5. <span data-ttu-id="31bd9-122">Si consiglia di distribuire tutte le risorse dell'area primaria anche in un'area secondaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-122">The recommendation is to deploy all primary region resources in a secondary region too.</span></span> 

   <span data-ttu-id="31bd9-123">Le risorse dell'area primaria includono il database SQL di Azure o Azure Cosmos DB, il bus di servizio di Azure e Hub eventi di Azure usati per la messaggistica, Gestione API di Azure e la funzionalità App per la logica di Azure di Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="31bd9-123">Primary region resources include Azure SQL Database or Azure Cosmos DB, Azure Service Bus and Azure Event Hubs used for messaging, Azure API Management, and the Azure Logic Apps feature in Azure App Service.</span></span>   

6. <span data-ttu-id="31bd9-124">Stabilire una connessione dall'area primaria a quella secondaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-124">Establish a connection from a primary region to a secondary region.</span></span> <span data-ttu-id="31bd9-125">Per eseguire il pull dello stato di esecuzione dall'area primaria, creare un'app per la logica nell'area secondaria,</span><span class="sxs-lookup"><span data-stu-id="31bd9-125">To pull the run status from a primary region, create a logic app in a secondary region.</span></span> 

   <span data-ttu-id="31bd9-126">che deve avere un trigger e un'azione.</span><span class="sxs-lookup"><span data-stu-id="31bd9-126">The logic app should have a trigger and an action.</span></span> 
   <span data-ttu-id="31bd9-127">Il trigger deve connettersi all'account di integrazione dell'area primaria, mentre</span><span class="sxs-lookup"><span data-stu-id="31bd9-127">The trigger should connect to a primary region integration account.</span></span> 
   <span data-ttu-id="31bd9-128">l'azione deve connettersi all'account di integrazione dell'area secondaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-128">The action should connect to a secondary region integration account.</span></span> 
   <span data-ttu-id="31bd9-129">In base all'intervallo di tempo, il trigger esegue il sondaggio della tabella sullo stato di esecuzione dell'area primaria ed esegue il pull dei nuovi record, se presenti.</span><span class="sxs-lookup"><span data-stu-id="31bd9-129">Based on the time interval, the trigger polls the primary region run status table and pulls the new records, if any.</span></span> 
   <span data-ttu-id="31bd9-130">L'azione li aggiorna nell'account di integrazione dell'area secondaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-130">The action updates them to a secondary region integration account.</span></span> 
   <span data-ttu-id="31bd9-131">Questa operazione consente di ottenere lo stato di runtime incrementale dall'area primaria a quella secondaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-131">This process helps to get incremental runtime status from the primary region to the secondary region.</span></span>

<span data-ttu-id="31bd9-132">La continuità aziendale nell'account di integrazione delle app per la logica offre il supporto basato sui protocolli B2B X12, AS2 ed EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="31bd9-132">Business continuity in a Logic Apps integration account provides support based on the B2B protocols X12, AS2, and EDIFACT.</span></span> <span data-ttu-id="31bd9-133">Per informazioni dettagliate sull'uso di X12 e AS2, vedere [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) e [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="31bd9-133">For detailed steps on using X12 and AS2, see [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) and [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) in this article.</span></span>

## <a name="fail-over-to-a-secondary-region-during-a-disaster-event"></a><span data-ttu-id="31bd9-134">Eseguire il failover all'area secondaria durante un evento di emergenza</span><span class="sxs-lookup"><span data-stu-id="31bd9-134">Fail over to a secondary region during a disaster event</span></span>

<span data-ttu-id="31bd9-135">Durante un evento di emergenza, quando l'area primaria non è disponibile per la continuità aziendale, dirigere il traffico verso l'area secondaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-135">During a disaster event, when the primary region is not available for business continuity, direct traffic to the secondary region.</span></span> <span data-ttu-id="31bd9-136">Un'area secondaria consente a un'azienda di ripristinare rapidamente le funzioni per soddisfare gli RPO/RTO concordati con i partner.</span><span class="sxs-lookup"><span data-stu-id="31bd9-136">A secondary region helps a business to recover functions quickly to meet the RPO/RTO agreed upon by their partners.</span></span> <span data-ttu-id="31bd9-137">Riduce al minimo gli sforzi per il failover da un'area a un'altra.</span><span class="sxs-lookup"><span data-stu-id="31bd9-137">It also minimizes efforts to fail over from one region to another region.</span></span> 

<span data-ttu-id="31bd9-138">Esiste una latenza prevista durante la copia dei numeri di controllo dall'area primaria a quella secondaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-138">There is an expected latency while copying control numbers from a primary region to a secondary region.</span></span> <span data-ttu-id="31bd9-139">Per evitare l'invio ai partner di doppioni di numeri di controllo generati durante un evento di emergenza, è consigliabile incrementare i numeri di controllo negli accordi dell'area secondaria usando i [cmdlet di PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="31bd9-139">To avoid sending duplicate generated control numbers to partners during a disaster event, the recommendation is to increment the control numbers in the secondary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>

## <a name="fall-back-to-a-primary-region-post-disaster-event"></a><span data-ttu-id="31bd9-140">Eseguire il fallback all'area primaria dopo un evento di emergenza</span><span class="sxs-lookup"><span data-stu-id="31bd9-140">Fall back to a primary region post-disaster event</span></span>

<span data-ttu-id="31bd9-141">Per eseguire il fallback a un'area primaria quando è disponibile, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="31bd9-141">To fall back to a primary region when it is available, follow these steps:</span></span>

1. <span data-ttu-id="31bd9-142">Interrompere l'accettazione dei messaggi dai partner nell'area secondaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-142">Stop accepting messages from partners in the secondary region.</span></span>  

2. <span data-ttu-id="31bd9-143">Incrementare i numeri di controllo generati per tutti i contratti dell'area primaria usando i [cmdlet di PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span><span class="sxs-lookup"><span data-stu-id="31bd9-143">Increment the generated control numbers for all the primary region agreements by using [PowerShell cmdlets](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).</span></span>  

3. <span data-ttu-id="31bd9-144">Indirizzare il traffico dall'area secondaria all'area primaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-144">Direct traffic from the secondary region to the primary region.</span></span>

4. <span data-ttu-id="31bd9-145">Controllare che l'app per la logica creata nell'area secondaria per il pull dello stato di esecuzione dall'area primaria sia abilitata.</span><span class="sxs-lookup"><span data-stu-id="31bd9-145">Check that the logic app created in the secondary region for pulling run status from the primary region is enabled.</span></span>

## <a name="x12"></a><span data-ttu-id="31bd9-146">X12</span><span class="sxs-lookup"><span data-stu-id="31bd9-146">X12</span></span> 

<span data-ttu-id="31bd9-147">La continuità aziendale per i documenti EDI X12 si basa sui numeri di controllo:</span><span class="sxs-lookup"><span data-stu-id="31bd9-147">Business continuity for EDI X12 documents is based on control numbers:</span></span>

> [!TIP]
> <span data-ttu-id="31bd9-148">È anche possibile usare [il modello di avvio rapido X12](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) per creare app per la logica.</span><span class="sxs-lookup"><span data-stu-id="31bd9-148">You can also use the [X12 quick start template](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) to create logic apps.</span></span> <span data-ttu-id="31bd9-149">La creazione degli account di integrazione primari e secondari è un prerequisito per l'uso del modello.</span><span class="sxs-lookup"><span data-stu-id="31bd9-149">Creating primary and secondary integration accounts are prerequisites to use the template.</span></span> <span data-ttu-id="31bd9-150">Il modello consente di creare 2 app per la logica, una per i numeri di controllo ricevuti e l'altra per i numeri di controllo generati.</span><span class="sxs-lookup"><span data-stu-id="31bd9-150">The template helps to create two logic apps, one for received control numbers and another for generated control numbers.</span></span> <span data-ttu-id="31bd9-151">I trigger e le azioni corrispondenti vengono creati nelle app per la logica collegando il trigger all'account di integrazione primario e l'azione a quello secondario.</span><span class="sxs-lookup"><span data-stu-id="31bd9-151">Respective triggers and actions are created in the logic apps, connecting the trigger to the primary integration account and the action to the secondary integration account.</span></span>

<span data-ttu-id="31bd9-152">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="31bd9-152">**Prerequisites**</span></span>

<span data-ttu-id="31bd9-153">Per abilitare il ripristino di emergenza per i messaggi in ingresso, selezionare le impostazioni per la verifica dei duplicati nelle impostazioni di ricezione dell'accordo X12.</span><span class="sxs-lookup"><span data-stu-id="31bd9-153">To enable disaster recovery for inbound messages, select the duplicate check settings in the X12 agreement's Receive Settings.</span></span>

![Selezionare le impostazioni per la verifica dei duplicati](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. <span data-ttu-id="31bd9-155">Creare un'[app per la logica](../logic-apps/logic-apps-create-a-logic-app.md) nell'area secondaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-155">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="31bd9-156">Cercare in **X12** e selezionare **X12 - Quando viene modificato un numero di controllo**.</span><span class="sxs-lookup"><span data-stu-id="31bd9-156">Search on **X12**, and select **X12 - When a control number is modified**.</span></span>   

   ![Cercare X12](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   <span data-ttu-id="31bd9-158">Il trigger richiede di stabilire una connessione con l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="31bd9-158">The trigger prompts you to establish a connection to an integration account.</span></span> 
   <span data-ttu-id="31bd9-159">Il trigger deve connettersi all'account di integrazione dell'area primaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-159">The trigger should be connected to a primary region integration account.</span></span>

3. <span data-ttu-id="31bd9-160">Inserire un nome di connessione, selezionare l'*account di integrazione dell'area primaria* dall'elenco e scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="31bd9-160">Enter a connection name, select your *primary region integration account* from the list, and choose **Create**.</span></span>   

   ![Nome dell'account di integrazione dell'area primaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. <span data-ttu-id="31bd9-162">L'impostazione **DateTime per avviare la sincronizzazione dei numeri di controllo** è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="31bd9-162">The **DateTime to start control number sync** setting is optional.</span></span> <span data-ttu-id="31bd9-163">Il campo **Frequenza** può essere impostato su **Giorno**, **Ora**, **Minuto** o **Secondo** con un intervallo.</span><span class="sxs-lookup"><span data-stu-id="31bd9-163">The **Frequency** can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![DateTime e Frequenza](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. <span data-ttu-id="31bd9-165">Selezionare **Nuovo passaggio** > **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="31bd9-165">Select **New step** > **Add an action**.</span></span>

   ![Nuovo passaggio, Aggiungi un'azione](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. <span data-ttu-id="31bd9-167">Cercare in **X12** e selezionare **X12 - Aggiungi o aggiorna numeri di controllo**.</span><span class="sxs-lookup"><span data-stu-id="31bd9-167">Search on **X12**, and select **X12 - Add or update control numbers**.</span></span>   

   ![Aggiungi o aggiorna numeri di controllo](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. <span data-ttu-id="31bd9-169">Per collegare un'azione a un account di integrazione dell'area secondaria, selezionare **Modifica connessione** > **Aggiungi nuova connessione** per un elenco degli account di integrazione disponibili.</span><span class="sxs-lookup"><span data-stu-id="31bd9-169">To connect an action to a secondary region integration account, select **Change connection** > **Add new connection** for a list of the available integration accounts.</span></span> <span data-ttu-id="31bd9-170">Inserire un nome di connessione, selezionare l'*account di integrazione dell'area secondaria* dall'elenco e scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="31bd9-170">Enter a connection name, select your *secondary region integration account* from the list, and choose **Create**.</span></span> 

   ![Nome dell'account di integrazione dell'area secondaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. <span data-ttu-id="31bd9-172">Passare agli input non elaborati facendo clic sull'icona nell'angolo in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="31bd9-172">Switch to raw inputs by clicking on the icon in upper right corner.</span></span>

   ![Passare agli input non elaborati](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. <span data-ttu-id="31bd9-174">Selezionare Corpo nell'utilità di selezione del contenuto dinamico e salvare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="31bd9-174">Select Body from the dynamic content picker, and save the logic app.</span></span>

   ![Campi per il contenuto dinamico](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   <span data-ttu-id="31bd9-176">In base all'intervallo di tempo, il trigger esegue il sondaggio della tabella dei numeri di controllo ricevuti dell'area primaria ed esegue il pull dei nuovi record.</span><span class="sxs-lookup"><span data-stu-id="31bd9-176">Based on the time interval, the trigger polls the primary region received control number table and pulls the new records.</span></span> 
   <span data-ttu-id="31bd9-177">L'azione aggiorna i record nell'account di integrazione dell'area secondaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-177">The action updates the records in the secondary region integration account.</span></span> 
   <span data-ttu-id="31bd9-178">Se non ci sono aggiornamenti disponibili, lo stato del trigger appare come **Ignorato**.</span><span class="sxs-lookup"><span data-stu-id="31bd9-178">If there are no updates, the trigger status appears as **Skipped**.</span></span>   

   ![Tabella dei numeri di controllo](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="31bd9-180">In base all'intervallo di tempo, lo stato di runtime incrementale viene replicato dall'area primaria a quella secondaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-180">Based on the time interval, the incremental runtime status replicates from a primary region to a secondary region.</span></span> <span data-ttu-id="31bd9-181">Durante un evento di emergenza, quando l'area primaria non è disponibile, dirigere il traffico verso l'area secondaria per assicurare la continuità aziendale.</span><span class="sxs-lookup"><span data-stu-id="31bd9-181">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span></span> 

## <a name="edifact"></a><span data-ttu-id="31bd9-182">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="31bd9-182">EDIFACT</span></span> 

<span data-ttu-id="31bd9-183">La continuità aziendale per i documenti EDI EDIFACT si basa sui numeri di controllo.</span><span class="sxs-lookup"><span data-stu-id="31bd9-183">Business continuity for EDI EDIFACT documents is based on control numbers.</span></span>

<span data-ttu-id="31bd9-184">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="31bd9-184">**Prerequisites**</span></span>

<span data-ttu-id="31bd9-185">Per abilitare il ripristino di emergenza per i messaggi in ingresso, selezionare le impostazioni per la verifica dei duplicati nelle impostazioni di ricezione dell'accordo EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="31bd9-185">To enable disaster recovery for inbound messages, select the duplicate check settings in your EDIFACT agreement's Receive Settings.</span></span>

![Selezionare le impostazioni per la verifica dei duplicati](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. <span data-ttu-id="31bd9-187">Creare un'[app per la logica](../logic-apps/logic-apps-create-a-logic-app.md) nell'area secondaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-187">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in a secondary region.</span></span>    

2. <span data-ttu-id="31bd9-188">Cercare in **EDIFACT** e selezionare **EDIFACT - Quando viene modificato un numero di controllo**.</span><span class="sxs-lookup"><span data-stu-id="31bd9-188">Search on **EDIFACT**, and select **EDIFACT - When a control number is modified**.</span></span>

   ![Cercare EDIFACT](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   <span data-ttu-id="31bd9-190">Il trigger richiede di stabilire una connessione con l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="31bd9-190">The trigger prompts you to establish a connection to an integration account.</span></span> 
   <span data-ttu-id="31bd9-191">Il trigger deve connettersi all'account di integrazione dell'area primaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-191">The trigger should be connected to a primary region integration account.</span></span> 

3. <span data-ttu-id="31bd9-192">Inserire un nome di connessione, selezionare l'*account di integrazione dell'area primaria* dall'elenco e scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="31bd9-192">Enter a connection name, select your *primary region integration account* from the list, and choose **Create**.</span></span>    

   ![Nome dell'account di integrazione dell'area primaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. <span data-ttu-id="31bd9-194">L'impostazione **DateTime per avviare la sincronizzazione dei numeri di controllo** è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="31bd9-194">The **DateTime to start control number sync** setting is optional.</span></span> <span data-ttu-id="31bd9-195">Il campo **Frequenza** può essere impostato su **Giorno**, **Ora**, **Minuto** o **Secondo** con un intervallo.</span><span class="sxs-lookup"><span data-stu-id="31bd9-195">The **Frequency** can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>    

   ![DateTime e Frequenza](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. <span data-ttu-id="31bd9-197">Selezionare **Nuovo passaggio** > **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="31bd9-197">Select **New step** > **Add an action**.</span></span>    

   ![Nuovo passaggio, Aggiungi un'azione](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. <span data-ttu-id="31bd9-199">Cercare in **EDIFACT** e selezionare **EDIFACT - Aggiungi o aggiorna numeri di controllo**.</span><span class="sxs-lookup"><span data-stu-id="31bd9-199">Search on **EDIFACT**, and select **EDIFACT - Add or update control numbers**.</span></span>   

   ![Aggiungi o aggiorna numeri di controllo](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. <span data-ttu-id="31bd9-201">Per collegare un'azione a un account di integrazione dell'area secondaria, selezionare **Modifica connessione** > **Aggiungi nuova connessione** per un elenco degli account di integrazione disponibili.</span><span class="sxs-lookup"><span data-stu-id="31bd9-201">To connect an action to a secondary region integration account, select **Change connection** > **Add new connection** for a list of the available integration accounts.</span></span> <span data-ttu-id="31bd9-202">Inserire un nome di connessione, selezionare l'*account di integrazione dell'area secondaria* dall'elenco e scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="31bd9-202">Enter a connection name, select your *secondary region integration account* from the list, and choose **Create**.</span></span>

   ![Nome dell'account di integrazione dell'area secondaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. <span data-ttu-id="31bd9-204">Passare agli input non elaborati facendo clic sull'icona nell'angolo in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="31bd9-204">Switch to raw inputs by clicking on the icon in upper right corner.</span></span>

   ![Passare agli input non elaborati](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. <span data-ttu-id="31bd9-206">Selezionare Corpo nell'utilità di selezione del contenuto dinamico e salvare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="31bd9-206">Select Body from the dynamic content picker, and save the logic app.</span></span>   

   ![Campi per il contenuto dinamico](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   <span data-ttu-id="31bd9-208">In base all'intervallo di tempo, il trigger esegue il sondaggio della tabella dei numeri di controllo ricevuti dell'area primaria ed esegue il pull dei nuovi record.</span><span class="sxs-lookup"><span data-stu-id="31bd9-208">Based on the time interval, the trigger polls the primary region received control number table and pulls the new records.</span></span>
   <span data-ttu-id="31bd9-209">L'azione aggiorna i record per l'account di integrazione dell'area secondaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-209">The action updates the records to the secondary region integration account.</span></span> 
   <span data-ttu-id="31bd9-210">Se non ci sono aggiornamenti disponibili, lo stato del trigger appare come **Ignorato**.</span><span class="sxs-lookup"><span data-stu-id="31bd9-210">If there are no updates, the trigger status appears as **Skipped**.</span></span>

   ![Tabella dei numeri di controllo](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

<span data-ttu-id="31bd9-212">In base all'intervallo di tempo, lo stato di runtime incrementale viene replicato dall'area primaria a quella secondaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-212">Based on the time interval, the incremental runtime status replicates from a primary region to a secondary region.</span></span> <span data-ttu-id="31bd9-213">Durante un evento di emergenza, quando l'area primaria non è disponibile, dirigere il traffico verso l'area secondaria per assicurare la continuità aziendale.</span><span class="sxs-lookup"><span data-stu-id="31bd9-213">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span></span> 

## <a name="as2"></a><span data-ttu-id="31bd9-214">AS2</span><span class="sxs-lookup"><span data-stu-id="31bd9-214">AS2</span></span> 

<span data-ttu-id="31bd9-215">La continuità aziendale per i documenti che usano il protocollo AS2 si basai sull'ID di messaggio e sul valore MIC.</span><span class="sxs-lookup"><span data-stu-id="31bd9-215">Business continuity for documents that use the AS2 protocol is based on the message ID and the MIC value.</span></span>

> [!TIP]
> <span data-ttu-id="31bd9-216">È anche possibile usare [il modello di avvio rapido AS2](https://github.com/Azure/azure-quickstart-templates/pull/3302) per creare le app per la logica.</span><span class="sxs-lookup"><span data-stu-id="31bd9-216">You can also use the [AS2 quick start template](https://github.com/Azure/azure-quickstart-templates/pull/3302) to create logic apps.</span></span> <span data-ttu-id="31bd9-217">La creazione degli account di integrazione primari e secondari è un prerequisito per l'uso del modello.</span><span class="sxs-lookup"><span data-stu-id="31bd9-217">Creating primary and secondary integration accounts are prerequisites to use the template.</span></span> <span data-ttu-id="31bd9-218">Il modello consente di creare un'app per la logica, con un trigger e un'azione.</span><span class="sxs-lookup"><span data-stu-id="31bd9-218">The template helps create a logic app that has a trigger and an action.</span></span> <span data-ttu-id="31bd9-219">L'app per la logica crea una connessione tra il trigger e l'account di integrazione primario e tra l'azione e l'account di integrazione secondario.</span><span class="sxs-lookup"><span data-stu-id="31bd9-219">The logic app creates a connection from a trigger to a primary integration account and an action to a secondary integration account.</span></span>

1. <span data-ttu-id="31bd9-220">Creare un'[app per la logica](../logic-apps/logic-apps-create-a-logic-app.md) nell'area secondaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-220">Create a [logic app](../logic-apps/logic-apps-create-a-logic-app.md) in the secondary region.</span></span>  

2. <span data-ttu-id="31bd9-221">Cercare in **AS2** e selezionare **AS2 -When a MIC value is created** (AS2 - Quando viene creato un valore MIC).</span><span class="sxs-lookup"><span data-stu-id="31bd9-221">Search on **AS2**, and select **AS2 - When a MIC value is created**.</span></span>   

   ![Cercare AS2](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   <span data-ttu-id="31bd9-223">Il trigger richiede di stabilire una connessione con l'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="31bd9-223">A trigger prompts you to establish a connection to an integration account.</span></span> 
   <span data-ttu-id="31bd9-224">Il trigger deve connettersi all'account di integrazione dell'area primaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-224">The trigger should be connected to a primary region integration account.</span></span> 
   
3. <span data-ttu-id="31bd9-225">Inserire un nome di connessione, selezionare l'*account di integrazione dell'area primaria* dall'elenco e scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="31bd9-225">Enter a connection name, select your *primary region integration account* from the list, and choose **Create**.</span></span>

   ![Nome dell'account di integrazione dell'area primaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. <span data-ttu-id="31bd9-227">L'impostazione **DateTime per avviare la sincronizzazione del valore MIC** è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="31bd9-227">The **DateTime to start MIC value sync** setting is optional.</span></span> <span data-ttu-id="31bd9-228">Il campo **Frequenza** può essere impostato su **Giorno**, **Ora**, **Minuto** o **Secondo** con un intervallo.</span><span class="sxs-lookup"><span data-stu-id="31bd9-228">The **Frequency** can be set to **Day**, **Hour**, **Minute**, or **Second** with an interval.</span></span>   

   ![DateTime e Frequenza](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. <span data-ttu-id="31bd9-230">Selezionare **Nuovo passaggio** > **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="31bd9-230">Select **New step** > **Add an action**.</span></span>  

   ![Nuovo passaggio, Aggiungi un'azione](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. <span data-ttu-id="31bd9-232">Cercare in **AS2** e selezionare **AS2 - Add or update MIC contents** (AS2 - Aggiungi o aggiorna contenuti MIC).</span><span class="sxs-lookup"><span data-stu-id="31bd9-232">Search on **AS2**, and select **AS2 - Add or update MIC contents**.</span></span>  

   ![Aggiunta o aggiornamento MIC](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. <span data-ttu-id="31bd9-234">Per collegare un'azione a un account di integrazione secondario, selezionare **Modifica connessione** > **Aggiungi nuova connessione** per un elenco degli account di integrazione disponibili.</span><span class="sxs-lookup"><span data-stu-id="31bd9-234">To connect an action to a secondary integration account, select **Change connection** > **Add new connection** for a list of the available integration accounts.</span></span> <span data-ttu-id="31bd9-235">Inserire un nome di connessione, selezionare l'*account di integrazione dell'area secondaria* dall'elenco e scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="31bd9-235">Enter a connection name, select your *secondary region integration account* from the list, and choose **Create**.</span></span>

   ![Nome dell'account di integrazione dell'area secondaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. <span data-ttu-id="31bd9-237">Passare agli input non elaborati facendo clic sull'icona nell'angolo in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="31bd9-237">Switch to raw inputs by clicking on the icon in upper right corner.</span></span>

   ![Passare agli input non elaborati](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. <span data-ttu-id="31bd9-239">Selezionare Corpo nell'utilità di selezione del contenuto dinamico e salvare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="31bd9-239">Select Body from the dynamic content picker, and save the logic app.</span></span>   

   ![Contenuto dinamico](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   <span data-ttu-id="31bd9-241">In base all'intervallo di tempo, il trigger esegue il sondaggio della tabella dell'area primaria ed esegue il pull dei nuovi record.</span><span class="sxs-lookup"><span data-stu-id="31bd9-241">Based on the time interval, the trigger polls the primary region table and pulls the new records.</span></span> <span data-ttu-id="31bd9-242">L'azione li aggiorna nell'account di integrazione dell'area secondaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-242">The action updates them to the secondary region integration account.</span></span> 
   <span data-ttu-id="31bd9-243">Se non ci sono aggiornamenti disponibili, lo stato del trigger appare come **Ignorato**.</span><span class="sxs-lookup"><span data-stu-id="31bd9-243">If there are no updates, the trigger status appears as **Skipped**.</span></span>  

   ![Tabella dell'area primaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

<span data-ttu-id="31bd9-245">In base all'intervallo di tempo, lo stato di runtime incrementale viene replicato dall'area primaria a quella secondaria.</span><span class="sxs-lookup"><span data-stu-id="31bd9-245">Based on the time interval, the incremental runtime status replicates from the primary region to the secondary region.</span></span> <span data-ttu-id="31bd9-246">Durante un evento di emergenza, quando l'area primaria non è disponibile, dirigere il traffico verso l'area secondaria per assicurare la continuità aziendale.</span><span class="sxs-lookup"><span data-stu-id="31bd9-246">During a disaster event, when the primary region is not available, direct traffic to the secondary region for business continuity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="31bd9-247">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="31bd9-247">Next steps</span></span>

[<span data-ttu-id="31bd9-248">Monitorare i messaggi B2B</span><span class="sxs-lookup"><span data-stu-id="31bd9-248">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md)

