---
title: aaaConnect tooDynamics 365 (online) da Azure logica App | Documenti Microsoft
description: "Creare la logica di flussi di lavoro app per la gestione di entità (online) di Dynamics 365 tramite API fornita da connettore hello Dynamics 365 hello"
services: logic-apps
cloud: Azure Stack
author: Mattp123
manager: anneta
documentationcenter: 
tags: connectors
ms.assetid: 0dc2abef-7d2c-4a2d-87ca-fad21367d135
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: matp; LADocs
ms.openlocfilehash: 183d7a6b8e5d2c0eecc70da0da3806e06c382df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toodynamics-365-from-logic-app-workflows"></a><span data-ttu-id="1c99c-103">Connettersi tooDynamics 365 da flussi di lavoro logica app</span><span class="sxs-lookup"><span data-stu-id="1c99c-103">Connect tooDynamics 365 from logic app workflows</span></span>

<span data-ttu-id="1c99c-104">Con la logica App, è possibile connettersi tooDynamics 365 (online) e creare flussi di business utile creano record, aggiornare gli elementi o restituiscono un elenco di record.</span><span class="sxs-lookup"><span data-stu-id="1c99c-104">With Logic Apps, you can connect tooDynamics 365 (online) and create useful business flows that create records, update items, or return a list of records.</span></span> <span data-ttu-id="1c99c-105">Con il connettore di Dynamics 365 hello, è possibile:</span><span class="sxs-lookup"><span data-stu-id="1c99c-105">With hello Dynamics 365 connector, you can:</span></span>

* <span data-ttu-id="1c99c-106">Compilare il flusso di business in base ai dati hello che si ottiene da Dynamics 365 (online).</span><span class="sxs-lookup"><span data-stu-id="1c99c-106">Build your business flow based on hello data you get from Dynamics 365 (online).</span></span>
* <span data-ttu-id="1c99c-107">Usare le azioni che ottengono una risposta e l'output di hello rendono disponibili per le altre azioni.</span><span class="sxs-lookup"><span data-stu-id="1c99c-107">Use actions that get a response and then make hello output available for other actions.</span></span> <span data-ttu-id="1c99c-108">Ad esempio, quando viene aggiornato un elemento in Dynamics 365 (online), è possibile inviare un messaggio di posta elettronica con Office 365.</span><span class="sxs-lookup"><span data-stu-id="1c99c-108">For example, when an item is updated in Dynamics 365 (online), you can send an email using Office 365.</span></span>

<span data-ttu-id="1c99c-109">Questo argomento viene illustrato come toocreate un'app di logica che crea un'attività in Dynamics 365 ogni volta che un nuovo cliente potenziale viene creato in Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="1c99c-109">This topic shows you how toocreate a logic app that creates a task in Dynamics 365 whenever a new lead is created in Dynamics 365.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c99c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1c99c-110">Prerequisites</span></span>
* <span data-ttu-id="1c99c-111">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="1c99c-111">An Azure account.</span></span>
* <span data-ttu-id="1c99c-112">Un account Dynamics 365 (online).</span><span class="sxs-lookup"><span data-stu-id="1c99c-112">A Dynamics 365 (online) account.</span></span>

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a><span data-ttu-id="1c99c-113">Creare un'attività quando viene creato un nuovo lead in Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="1c99c-113">Create a task when a new lead is created in Dynamics 365</span></span>

1.  <span data-ttu-id="1c99c-114">[Accedi tooAzure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1c99c-114">[Sign in tooAzure](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="1c99c-115">Nella casella di ricerca di Azure hello, digitare `Logic apps`, e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="1c99c-115">In hello Azure search box, type `Logic apps`, and press ENTER.</span></span>

      ![Trovare App per la logica](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  <span data-ttu-id="1c99c-117">In **App per la logica** fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-117">Under **Logic apps**, click **Add**.</span></span>

      ![Aggiungere un'app per la logica](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  <span data-ttu-id="1c99c-119">app per la logica hello toocreate, hello completo **nome**, **sottoscrizione**, **gruppo di risorse**, e **percorso** campi e quindi fare clic su  **Creare**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-119">toocreate hello logic app, complete hello **Name**, **Subscription**, **Resource Group**, and **Location** fields, and then click **Create**.</span></span>

5.  <span data-ttu-id="1c99c-120">Selezionare hello nuova logica app.</span><span class="sxs-lookup"><span data-stu-id="1c99c-120">Select hello new logic app.</span></span> <span data-ttu-id="1c99c-121">Quando si riceve hello **distribuzione ha avuto esito positivo** notifica, fare clic su **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-121">When you receive hello **Deployment Succeeded** notification, click **Refresh**.</span></span>

6.  <span data-ttu-id="1c99c-122">In **Strumenti di sviluppo** fare clic su **Progettazione app per la logica**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-122">Under **Development Tools**, click **Logic App Designer**.</span></span> <span data-ttu-id="1c99c-123">Nell'elenco di modelli di hello, fare clic su **App vuota per la logica**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-123">In hello template list, click **Blank Logic App**.</span></span>

7.  <span data-ttu-id="1c99c-124">Nella casella di ricerca hello, digitare `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="1c99c-124">In hello search box, type `Dynamics 365`.</span></span> <span data-ttu-id="1c99c-125">Da hello Dynamics 365 attiva l'elenco, selezionare **Dynamics 365: quando viene creato un record**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-125">From hello Dynamics 365 triggers list, select **Dynamics 365 – When a record is created**.</span></span>

8.  <span data-ttu-id="1c99c-126">Nel caso di richiesta toosign in tooDynamics 365, farlo ora.</span><span class="sxs-lookup"><span data-stu-id="1c99c-126">If you are prompted toosign in tooDynamics 365, do so now.</span></span>

9.  <span data-ttu-id="1c99c-127">Nei dettagli trigger hello, immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="1c99c-127">In hello trigger details, enter hello following information:</span></span>

  * <span data-ttu-id="1c99c-128">**Nome organizzazione**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-128">**Organization Name**.</span></span> <span data-ttu-id="1c99c-129">Selezionare l'istanza di Dynamics 365 di hello che si desidera hello logica app toolisten per.</span><span class="sxs-lookup"><span data-stu-id="1c99c-129">Select hello Dynamics 365 instance that you want hello logic app toolisten to.</span></span>

  * <span data-ttu-id="1c99c-130">**Nome entità**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-130">**Entity Name**.</span></span> <span data-ttu-id="1c99c-131">Selezionare entità hello che si desidera toolisten per.</span><span class="sxs-lookup"><span data-stu-id="1c99c-131">Select hello entity that you want toolisten to.</span></span> <span data-ttu-id="1c99c-132">Questo evento viene utilizzato come un'app di logica di trigger toostart hello.</span><span class="sxs-lookup"><span data-stu-id="1c99c-132">This event acts as a trigger toostart hello logic app.</span></span> 
  <span data-ttu-id="1c99c-133">In questa procedura guidata si seleziona **Lead**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-133">In this walkthrough, **Leads** is selected.</span></span>

  * <span data-ttu-id="1c99c-134">**La frequenza desiderata toocheck per gli elementi?**</span><span class="sxs-lookup"><span data-stu-id="1c99c-134">**How often do you want toocheck for items?**</span></span> <span data-ttu-id="1c99c-135">Impostare la frequenza di questi valori hello logica app verifica la presenza di trigger toohello correlati gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="1c99c-135">These values set how often hello logic app checks for updates related toohello trigger.</span></span> <span data-ttu-id="1c99c-136">impostazione predefinita Hello è toocheck per gli aggiornamenti ogni tre minuti.</span><span class="sxs-lookup"><span data-stu-id="1c99c-136">hello default setting is toocheck for updates every three minutes.</span></span>

    * <span data-ttu-id="1c99c-137">**Frequenza**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-137">**Frequency**.</span></span> <span data-ttu-id="1c99c-138">Selezionare secondi, minuti, ore o giorni.</span><span class="sxs-lookup"><span data-stu-id="1c99c-138">Select seconds, minutes, hours, or days.</span></span>

    * <span data-ttu-id="1c99c-139">**Intervallo**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-139">**Interval**.</span></span> <span data-ttu-id="1c99c-140">Immettere il numero di hello di secondi, minuti, ore o giorni che si desidera toopass prima hello della successiva archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1c99c-140">Enter hello number of seconds, minutes, hours, or days that you want toopass before hello next check.</span></span>

      ![Dettagli del trigger dell'app per la logica](./media/connectors-create-api-crmonline/trigger-details.png)

10. <span data-ttu-id="1c99c-142">Fare clic su **Nuovo passaggio** e quindi su **Aggiungi un'azione**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-142">Click **New step**, and then click **Add an action**.</span></span>

11. <span data-ttu-id="1c99c-143">Nella casella di ricerca hello, digitare `Dynamics 365`.</span><span class="sxs-lookup"><span data-stu-id="1c99c-143">In hello search box, type `Dynamics 365`.</span></span> <span data-ttu-id="1c99c-144">Selezionare nell'elenco di azioni hello **Dynamics 365: creare un nuovo record**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-144">From hello actions list, select **Dynamics 365 – Create a new record**.</span></span>

12. <span data-ttu-id="1c99c-145">Immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="1c99c-145">Enter hello following information:</span></span>

    * <span data-ttu-id="1c99c-146">**Nome organizzazione**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-146">**Organization Name**.</span></span> <span data-ttu-id="1c99c-147">Selezionare l'istanza di Dynamics 365 hello in cui si desidera registrazione hello toocreate di hello del flusso.</span><span class="sxs-lookup"><span data-stu-id="1c99c-147">Select hello Dynamics 365 instance where you want hello flow toocreate hello record.</span></span> 
    <span data-ttu-id="1c99c-148">Si noti che questa istanza non dispone di toobe hello stesso in cui hello evento dall'istanza.</span><span class="sxs-lookup"><span data-stu-id="1c99c-148">Notice that this instance doesn’t have toobe hello same instance where hello event is triggered from.</span></span>

    * <span data-ttu-id="1c99c-149">**Nome entità**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-149">**Entity Name**.</span></span> <span data-ttu-id="1c99c-150">Selezionare entità hello che si desidera toocreate un record quando viene attivato l'evento hello.</span><span class="sxs-lookup"><span data-stu-id="1c99c-150">Select hello entity that you want toocreate a record when hello event is triggered.</span></span> 
    <span data-ttu-id="1c99c-151">In questa procedura guidata si seleziona **Attività**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-151">In this walkthrough, **Tasks** is selected.</span></span>

13. <span data-ttu-id="1c99c-152">Fare clic nella hello **soggetto** visualizzata.</span><span class="sxs-lookup"><span data-stu-id="1c99c-152">Click in hello **Subject** box that appears.</span></span> <span data-ttu-id="1c99c-153">Hello dinamica contenuto elenco visualizzato, è possibile selezionare uno di questi campi:</span><span class="sxs-lookup"><span data-stu-id="1c99c-153">From hello dynamic content list that appears, you can select either of these fields:</span></span>

    * <span data-ttu-id="1c99c-154">**Cognome**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-154">**Last Name**.</span></span> <span data-ttu-id="1c99c-155">Selezione di questo campo inserisce hello cognome hello lead campo Subject hello per le attività di hello, quando viene creato il record di attività hello.</span><span class="sxs-lookup"><span data-stu-id="1c99c-155">Selecting this field inserts hello last name for hello lead into hello Subject field for hello task, when hello task record is created.</span></span>
    * <span data-ttu-id="1c99c-156">**Argomento**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-156">**Topic**.</span></span> <span data-ttu-id="1c99c-157">Selezionando questa inserimenti hello argomento campo lead hello nel campo soggetto hello per attività di hello, quando i record di attività hello viene creato.</span><span class="sxs-lookup"><span data-stu-id="1c99c-157">Selecting this field inserts hello Topic field for hello lead into hello Subject field for hello task, when hello task record is created.</span></span> 
    <span data-ttu-id="1c99c-158">Fare clic su **argomento** tooadd che toohello **soggetto** casella.</span><span class="sxs-lookup"><span data-stu-id="1c99c-158">Click **Topic** tooadd that toohello **Subject** box.</span></span>

      ![Dettagli per la creazione di un nuovo record nell'app per la logica](./media/connectors-create-api-crmonline/create-record-details.png)

14. <span data-ttu-id="1c99c-160">Sulla barra degli strumenti Progettazione applicazione logica hello, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-160">On hello Logic App Designer toolbar, click **Save**.</span></span>

    ![Salva nella barra degli strumenti di Progettazione app per la logica](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. <span data-ttu-id="1c99c-162">hello toostart logica App, fare clic su **eseguire**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-162">toostart hello Logic App, click **Run**.</span></span>

    ![Salva nella barra degli strumenti di Progettazione app per la logica](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. <span data-ttu-id="1c99c-164">Creare ora un record lead in Dynamics 365 for Sales e verificare il funzionamento del flusso.</span><span class="sxs-lookup"><span data-stu-id="1c99c-164">Now create a lead record in Dynamics 365 for Sales and see your flow in action!</span></span>

## <a name="set-advanced-options-for-a-logic-app-step"></a><span data-ttu-id="1c99c-165">Impostare le opzioni avanzate per un passaggio dell'app per la logica</span><span class="sxs-lookup"><span data-stu-id="1c99c-165">Set advanced options for a logic app step</span></span>

<span data-ttu-id="1c99c-166">toospecify come toofilter dati in un passaggio di app di logica, fare clic su **Visualizza le opzioni avanzate** in questo passaggio, quindi aggiungere un filtro o un ordine dalla query.</span><span class="sxs-lookup"><span data-stu-id="1c99c-166">toospecify how toofilter data in a logic app step, click **Show advanced options** in that step, then add a filter or order by query.</span></span>

<span data-ttu-id="1c99c-167">Ad esempio, è possibile utilizzare un filtro query tooget solo gli account attivi e ordinare per nome account hello.</span><span class="sxs-lookup"><span data-stu-id="1c99c-167">For example, you can use a filter query tooget only active accounts and order by hello account name.</span></span> <span data-ttu-id="1c99c-168">tooperform questa attività, immettere una query di filtro OData hello `statuscode eq 1`e selezionare **nome Account** dall'elenco di contenuto dinamico hello.</span><span class="sxs-lookup"><span data-stu-id="1c99c-168">tooperform this task, enter hello OData filter query `statuscode eq 1`, and select **Account Name** from hello dynamic content list.</span></span> <span data-ttu-id="1c99c-169">Per altre informazioni, vedere [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) e [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span><span class="sxs-lookup"><span data-stu-id="1c99c-169">More information: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) and [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2).</span></span>

![Opzioni avanzate delle app per la logica](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a><span data-ttu-id="1c99c-171">Procedure consigliate per l'uso delle opzioni avanzate</span><span class="sxs-lookup"><span data-stu-id="1c99c-171">Best practices when using advanced options</span></span>

<span data-ttu-id="1c99c-172">Quando si aggiunge un campo del valore tooa, è necessario rispettare il tipo di campo hello digitare un valore o selezionare un valore dall'elenco di contenuto dinamico hello.</span><span class="sxs-lookup"><span data-stu-id="1c99c-172">When you add a value tooa field, you must match hello field type whether you type a value or select a value from hello dynamic content list.</span></span>

<span data-ttu-id="1c99c-173">Tipo di campo</span><span class="sxs-lookup"><span data-stu-id="1c99c-173">Field type</span></span>  |<span data-ttu-id="1c99c-174">Come toouse</span><span class="sxs-lookup"><span data-stu-id="1c99c-174">How toouse</span></span>  |<span data-ttu-id="1c99c-175">Dove toofind</span><span class="sxs-lookup"><span data-stu-id="1c99c-175">Where toofind</span></span>  |<span data-ttu-id="1c99c-176">Nome</span><span class="sxs-lookup"><span data-stu-id="1c99c-176">Name</span></span>  |<span data-ttu-id="1c99c-177">Tipo di dati</span><span class="sxs-lookup"><span data-stu-id="1c99c-177">Data type</span></span>  
---------|---------|---------|---------|---------
<span data-ttu-id="1c99c-178">Campi di testo</span><span class="sxs-lookup"><span data-stu-id="1c99c-178">Text fields</span></span>|<span data-ttu-id="1c99c-179">I campi di testo richiedono una singola riga di testo oppure contenuto dinamico costituito da un campo di tipo testo.</span><span class="sxs-lookup"><span data-stu-id="1c99c-179">Text fields require a single line of text or dynamic content that is a text type field.</span></span> <span data-ttu-id="1c99c-180">Esempi includono i campi categoria e sottocategoria hello.</span><span class="sxs-lookup"><span data-stu-id="1c99c-180">Examples include hello Category and Sub-Category fields.</span></span>|<span data-ttu-id="1c99c-181">Impostazioni > personalizzazioni > Personalizza hello sistema > entità > attività > campi</span><span class="sxs-lookup"><span data-stu-id="1c99c-181">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="1c99c-182">category</span><span class="sxs-lookup"><span data-stu-id="1c99c-182">category</span></span> |<span data-ttu-id="1c99c-183">Riga di testo singola</span><span class="sxs-lookup"><span data-stu-id="1c99c-183">Single Line of Text</span></span>        
<span data-ttu-id="1c99c-184">Campi di tipo Integer</span><span class="sxs-lookup"><span data-stu-id="1c99c-184">Integer fields</span></span> | <span data-ttu-id="1c99c-185">Alcuni campi richiedono Integer oppure contenuto dinamico costituito da un campo di tipo Integer.</span><span class="sxs-lookup"><span data-stu-id="1c99c-185">Some fields require integer or dynamic content that is an integer type field.</span></span> <span data-ttu-id="1c99c-186">Ad esempio, Percentuale completamento e Durata.</span><span class="sxs-lookup"><span data-stu-id="1c99c-186">Examples include Percent Complete and Duration.</span></span> |<span data-ttu-id="1c99c-187">Impostazioni > personalizzazioni > Personalizza hello sistema > entità > attività > campi</span><span class="sxs-lookup"><span data-stu-id="1c99c-187">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="1c99c-188">percentcomplete</span><span class="sxs-lookup"><span data-stu-id="1c99c-188">percentcomplete</span></span> |<span data-ttu-id="1c99c-189">Numero intero</span><span class="sxs-lookup"><span data-stu-id="1c99c-189">Whole Number</span></span>         
<span data-ttu-id="1c99c-190">Campi di data</span><span class="sxs-lookup"><span data-stu-id="1c99c-190">Date fields</span></span> | <span data-ttu-id="1c99c-191">Alcuni campi richiedono una data immessa nel formato mm/gg/aaaa oppure contenuto dinamico costituito da un campo di tipo data.</span><span class="sxs-lookup"><span data-stu-id="1c99c-191">Some fields require a date entered in mm/dd/yyyy format or dynamic content that is a date type field.</span></span> <span data-ttu-id="1c99c-192">Ad esempio, Data creazione, Data di inizio, Inizio effettivo, Ultimo periodo sospensione, Fine effettiva e Scadenza.</span><span class="sxs-lookup"><span data-stu-id="1c99c-192">Examples include Created On, Start Date, Actual Start, Last on Hold Time, Actual End, and Due Date.</span></span> | <span data-ttu-id="1c99c-193">Impostazioni > personalizzazioni > Personalizza hello sistema > entità > attività > campi</span><span class="sxs-lookup"><span data-stu-id="1c99c-193">Settings > Customizations > Customize hello System > Entities > Task > Fields</span></span> |<span data-ttu-id="1c99c-194">createdon</span><span class="sxs-lookup"><span data-stu-id="1c99c-194">createdon</span></span> |<span data-ttu-id="1c99c-195">Data e ora</span><span class="sxs-lookup"><span data-stu-id="1c99c-195">Date and Time</span></span>
<span data-ttu-id="1c99c-196">Campi che richiedono sia ID record che tipo di ricerca</span><span class="sxs-lookup"><span data-stu-id="1c99c-196">Fields that require both a record ID and lookup type</span></span> |<span data-ttu-id="1c99c-197">Alcuni campi che fanno riferimento a un altro record di entità richiedono l'ID record hello e il tipo di ricerca di hello.</span><span class="sxs-lookup"><span data-stu-id="1c99c-197">Some fields that reference another entity record require both hello record ID and hello lookup type.</span></span> |<span data-ttu-id="1c99c-198">Impostazioni > personalizzazioni > Personalizza hello sistema > entità > Account > campi</span><span class="sxs-lookup"><span data-stu-id="1c99c-198">Settings > Customizations > Customize hello System > Entities > Account > Fields</span></span>  | <span data-ttu-id="1c99c-199">accountid</span><span class="sxs-lookup"><span data-stu-id="1c99c-199">accountid</span></span>  | <span data-ttu-id="1c99c-200">Chiave primaria</span><span class="sxs-lookup"><span data-stu-id="1c99c-200">Primary Key</span></span>

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a><span data-ttu-id="1c99c-201">Alcuni esempi di campi che richiedono sia ID record che tipo di ricerca</span><span class="sxs-lookup"><span data-stu-id="1c99c-201">More examples of fields that require both a record ID and lookup type</span></span>
<span data-ttu-id="1c99c-202">Nella tabella precedente hello l'espansione, ecco alcuni esempi di campi che non funzionano con i valori selezionati dall'elenco di contenuto dinamico hello.</span><span class="sxs-lookup"><span data-stu-id="1c99c-202">Expanding on hello previous table, here are more examples of fields that don't work with values selected from hello dynamic content list.</span></span> <span data-ttu-id="1c99c-203">Al contrario, questi campi richiedono entrambi una ricerca e l'ID tipo di record immesso nei campi hello in PowerApps.</span><span class="sxs-lookup"><span data-stu-id="1c99c-203">Instead, these fields require both a record ID and lookup type entered into hello fields in PowerApps.</span></span>  
* <span data-ttu-id="1c99c-204">Proprietario e Tipo di proprietario.</span><span class="sxs-lookup"><span data-stu-id="1c99c-204">Owner and Owner Type.</span></span> <span data-ttu-id="1c99c-205">campo proprietario Hello deve essere un ID di record utente o del team valido</span><span class="sxs-lookup"><span data-stu-id="1c99c-205">hello Owner field must be a valid user or team record ID.</span></span> <span data-ttu-id="1c99c-206">deve essere il tipo di proprietario Hello **systemusers** o **Team**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-206">hello Owner Type must be either **systemusers** or **teams**.</span></span>
* <span data-ttu-id="1c99c-207">Cliente e Tipo di cliente.</span><span class="sxs-lookup"><span data-stu-id="1c99c-207">Customer and Customer Type.</span></span> <span data-ttu-id="1c99c-208">campo Customer Hello deve essere un account valido o record ID contatto.</span><span class="sxs-lookup"><span data-stu-id="1c99c-208">hello Customer field must be a valid account or contact record ID.</span></span> <span data-ttu-id="1c99c-209">deve essere il tipo di proprietario Hello **account** o **contatti**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-209">hello Owner Type must be either **accounts** or **contacts**.</span></span>
* <span data-ttu-id="1c99c-210">Tema e Tipo relativo.</span><span class="sxs-lookup"><span data-stu-id="1c99c-210">Regarding and Regarding Type.</span></span> <span data-ttu-id="1c99c-211">Hello relativi campi deve essere un ID record valido, ad esempio un account o record ID contatto.</span><span class="sxs-lookup"><span data-stu-id="1c99c-211">hello Regarding field must be a valid record ID, such as an account or contact record ID.</span></span> <span data-ttu-id="1c99c-212">Hello per quanto riguarda tipo deve essere il tipo di ricerca hello per record hello, ad esempio **account** o **contatti**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-212">hello Regarding Type must be hello lookup type for hello record, such as **accounts** or **contacts**.</span></span>

<span data-ttu-id="1c99c-213">Hello seguente esempio di azione di creazione di attività aggiunge un account corrispondente di ID di record toohello aggiungerlo toohello riguardanti campo dell'attività hello.</span><span class="sxs-lookup"><span data-stu-id="1c99c-213">hello following task creation action example adds an account record that corresponds toohello record ID adding it toohello regarding field of hello task.</span></span>

![ID record e tipo account nel flusso](./media/connectors-create-api-crmonline/recordid-type-account.png)

<span data-ttu-id="1c99c-215">In questo esempio viene inoltre assegnato hello attività tooa utente specifico in base a ID del record. dell'utente hello</span><span class="sxs-lookup"><span data-stu-id="1c99c-215">This example also assigns hello task tooa specific user based on hello user's record ID.</span></span>

![ID record e tipo account nel flusso](./media/connectors-create-api-crmonline/recordid-type-user.png)

<span data-ttu-id="1c99c-217">toofind un record dell'ID, vedere hello seguente sezione: *trovare l'ID record hello*</span><span class="sxs-lookup"><span data-stu-id="1c99c-217">toofind a record's ID, see hello following section: *Find hello record ID*</span></span>

## <a name="find-hello-record-id"></a><span data-ttu-id="1c99c-218">Trovare l'ID record hello</span><span class="sxs-lookup"><span data-stu-id="1c99c-218">Find hello record ID</span></span>

1. <span data-ttu-id="1c99c-219">Aprire un record, ad esempio un record account.</span><span class="sxs-lookup"><span data-stu-id="1c99c-219">Open a record, such as an account record.</span></span>

2. <span data-ttu-id="1c99c-220">Sulla barra degli strumenti Azioni hello, fare clic su **Pop Out** ![record popout](./media/connectors-create-api-crmonline/popout-record.png).</span><span class="sxs-lookup"><span data-stu-id="1c99c-220">On hello actions toolbar, click **Pop Out** ![popout record](./media/connectors-create-api-crmonline/popout-record.png).</span></span>
<span data-ttu-id="1c99c-221">In alternativa, sulla barra degli strumenti Azioni hello, toocopy hello l'URL completo nel programma di posta elettronica predefinito, fare clic su **posta elettronica un collegamento**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-221">Alternatively, on hello actions toolbar, toocopy hello full URL into your default email program, click **EMAIL A LINK**.</span></span>

   <span data-ttu-id="1c99c-222">ID record Hello viene visualizzato tra hello % 7b e 7 di % d la codifica dei caratteri dell'URL hello.</span><span class="sxs-lookup"><span data-stu-id="1c99c-222">hello record ID is displayed in between hello %7b and %7d encoding characters of hello URL.</span></span>

   ![ID record e tipo account nel flusso](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a><span data-ttu-id="1c99c-224">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="1c99c-224">Troubleshooting</span></span>
<span data-ttu-id="1c99c-225">un passaggio non riuscito in un'app di logica, lo stato hello di visualizzare i dettagli dell'evento hello tootroubleshoot.</span><span class="sxs-lookup"><span data-stu-id="1c99c-225">tootroubleshoot a failed step in a logic app, view hello status details of hello event.</span></span>

1. <span data-ttu-id="1c99c-226">In **App per la logica**, selezionare l'app per la logica e quindi fare clic su **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="1c99c-226">Under **Logic Apps**, select your logic app, and then click **Overview**.</span></span> 

   <span data-ttu-id="1c99c-227">Hello area di riepilogo viene visualizzato e fornisce lo stato di esecuzione hello per hello logica app.</span><span class="sxs-lookup"><span data-stu-id="1c99c-227">hello Summary area is shown and provides hello run status for hello logic app.</span></span> 

   ![Stato di esecuzione dell'app per la logica](./media/connectors-create-api-crmonline/tshoot1.png)

2. <span data-ttu-id="1c99c-229">tooview ulteriori informazioni su qualsiasi esecuzioni non riuscite, fare clic su hello Impossibile evento.</span><span class="sxs-lookup"><span data-stu-id="1c99c-229">tooview more information about any failed runs, click hello failed event.</span></span> <span data-ttu-id="1c99c-230">tooexpand un passaggio non riuscito, fare clic su tale passaggio.</span><span class="sxs-lookup"><span data-stu-id="1c99c-230">tooexpand a failed step, click that step.</span></span>

   ![Espandere un passaggio non riuscito](./media/connectors-create-api-crmonline/tshoot2.png)

   <span data-ttu-id="1c99c-232">Dettagli Hello vengono visualizzati e consentono di risolvere problemi che causano hello dell'errore hello.</span><span class="sxs-lookup"><span data-stu-id="1c99c-232">hello step details appear and can help troubleshoot hello cause of hello failure.</span></span>

   ![Dettagli del passaggio non riuscito](./media/connectors-create-api-crmonline/tshoot3.png)

<span data-ttu-id="1c99c-234">Per altre informazioni sulla risoluzione dei problemi delle app per la logica, vedere [Diagnosi degli errori delle app per la logica](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="1c99c-234">For more information about troubleshooting logic apps, see [Diagnosing logic app failures](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="1c99c-235">Dettagli specifici del connettore</span><span class="sxs-lookup"><span data-stu-id="1c99c-235">Connector-specific details</span></span>

<span data-ttu-id="1c99c-236">Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/crm/).</span><span class="sxs-lookup"><span data-stu-id="1c99c-236">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/crm/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1c99c-237">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1c99c-237">Next steps</span></span>
<span data-ttu-id="1c99c-238">Esplorare hello altri connettori disponibile in App per la logica nel nostro [elenco API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="1c99c-238">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
