---
title: Connettore del servizio di gestione in OMS aaaIT | Documenti Microsoft
description: Utilizzare monitor di toocentrally hello connettore di gestione del servizio IT e gestire gli elementi di lavoro ITSM hello in OMS e risolvere rapidamente eventuali problemi.
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: v-jysur
ms.openlocfilehash: 33ed5d432591b836eb41ba982c66c96f22879444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a><span data-ttu-id="8ac20-103">Gestire centralmente gli elementi di lavoro ITSM con IT Service Management Connector (anteprima)</span><span class="sxs-lookup"><span data-stu-id="8ac20-103">Centrally manage ITSM work items using IT Service Management Connector (Preview)</span></span>

![Simbolo di IT Service Management Connector](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="8ac20-105">È possibile utilizzare hello IT servizio Gestione connettore (ITSMC) in OMS Log Analitica toocentrally monitoraggio e gestione degli elementi di lavoro tra i prodotti o servizi ITSM.</span><span class="sxs-lookup"><span data-stu-id="8ac20-105">You can use hello IT Service Management Connector (ITSMC) in OMS Log Analytics toocentrally monitor and manage work items across your ITSM products/services.</span></span>

<span data-ttu-id="8ac20-106">Connettore di gestione del servizio IT Hello integra i prodotti di Gestione servizio IT (ITSM) esistente e i servizi con Analitica di Log di OMS.</span><span class="sxs-lookup"><span data-stu-id="8ac20-106">hello IT Service Management Connector integrates your existing IT Service Management (ITSM) products and services with OMS Log Analytics.</span></span>  <span data-ttu-id="8ac20-107">soluzione hello è bidirezionale l'integrazione con prodotti e servizi ITSM, dove fornisce hello gli utenti di OMS eventi imprevisti toocreate un'opzione, gli avvisi o eventi nella soluzione ITSM.</span><span class="sxs-lookup"><span data-stu-id="8ac20-107">hello solution has bidirectional integration with ITSM products/services, where it provides hello OMS users an option toocreate incidents, alerts, or events in ITSM solution.</span></span> <span data-ttu-id="8ac20-108">connettore Hello Importa anche i dati, ad esempio eventi imprevisti e richieste di modifica da soluzione ITSM in OMS Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="8ac20-108">hello connector also  imports data such as incidents, and change requests from ITSM solution into OMS Log Analytics.</span></span>

<span data-ttu-id="8ac20-109">Con IT Service Management Connector è possibile:</span><span class="sxs-lookup"><span data-stu-id="8ac20-109">With IT Service Management Connector, you can:</span></span>

  - <span data-ttu-id="8ac20-110">Monitorare e gestire centralmente gli elementi di lavoro per i prodotti e i servizi ITSM usati nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="8ac20-110">Centrally monitor and manage work items for ITSM products/services used across your organization.</span></span>
  - <span data-ttu-id="8ac20-111">Creare elementi di lavoro ITSM, ad esempio avvisi, eventi, eventi imprevisto, in ITSM dagli avvisi OMS e tramite la ricerca log.</span><span class="sxs-lookup"><span data-stu-id="8ac20-111">Create ITSM work items (like alert, event, incident) in ITSM from OMS alerts and through log search.</span></span>
  - <span data-ttu-id="8ac20-112">Leggere gli eventi imprevisti e richieste di modifica dalla soluzione ITSM e correlare i dati di log rilevanti nell'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8ac20-112">Read incidents and change requests from your ITSM solution and correlate with relevant log data in Log Analytics workspace.</span></span>
  - <span data-ttu-id="8ac20-113">Individuare eventuali eventi imprevisti e non comuni e risolverli, anche prima che gli utenti finali di hello chiamare e li segnala toohello helpdesk.</span><span class="sxs-lookup"><span data-stu-id="8ac20-113">Find any unexpected and unusual events and resolve them, even before hello end users call and report them toohello helpdesk.</span></span>
  - <span data-ttu-id="8ac20-114">Importare i dati degli elementi di lavoro in Log Analytics e creare report indicatori di prestazioni chiave.</span><span class="sxs-lookup"><span data-stu-id="8ac20-114">Import work items data into Log Analytics and create key performance indicator (KPI) reports.</span></span>  <span data-ttu-id="8ac20-115">Grazie all'uso di questi report, è possibile individuare, valutare e agire su diversi elementi importanti, ad esempio la valutazione della presenza di malware.</span><span class="sxs-lookup"><span data-stu-id="8ac20-115">Using these reports, you can identify, assess and act on several important items such as malware assessment.</span></span>
  - <span data-ttu-id="8ac20-116">Visualizzare i dashboard curati per ottenere informazioni approfondite su eventi imprevisti, richieste di modifica e sistemi interessati.</span><span class="sxs-lookup"><span data-stu-id="8ac20-116">View curated dashboards for deeper insights on incidents, change requests and impacted systems.</span></span>
  - <span data-ttu-id="8ac20-117">Risolvere i problemi più velocemente, è possibile correlare con altre soluzioni di gestione nell'area di lavoro Log Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="8ac20-117">Troubleshoot faster by correlating with other management solutions in hello Log Analytics workspace.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="8ac20-118">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8ac20-118">Prerequisites</span></span>

<span data-ttu-id="8ac20-119">tooimport hello ITSM gli elementi di lavoro in OMS Log Analitica soluzione hello richiede una connessione tra hello connettore di gestione del servizio IT in OMS hello e hello SM IT prodotti o servizi da cui importare gli elementi di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="8ac20-119">tooimport hello ITSM work items into OMS Log Analytics, hello solution requires a connection between hello IT Service Management Connector in hello OMS and hello IT SM product/service from which you import hello work items.</span></span>


## <a name="configuration"></a><span data-ttu-id="8ac20-120">Configurazione</span><span class="sxs-lookup"><span data-stu-id="8ac20-120">Configuration</span></span>

<span data-ttu-id="8ac20-121">Aggiungi hello area di lavoro OMS tooyour soluzione connettore di gestione del servizio IT, hello processo descritto in [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="8ac20-121">Add hello IT Service Management Connector solution tooyour OMS work space, using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="8ac20-122">Connettore di gestione del servizio IT riquadro come può vedere nella raccolta di soluzioni hello:</span><span class="sxs-lookup"><span data-stu-id="8ac20-122">IT Service Management Connector tile as you see in hello Solutions gallery:</span></span>

![riquadro connettore](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

<span data-ttu-id="8ac20-124">Dopo l'aggiunta di esito positivo, verrà visualizzato hello connettore di gestione del servizio IT in **OMS** > **impostazioni** > **Connected Sources.**</span><span class="sxs-lookup"><span data-stu-id="8ac20-124">After successful addition, you will see hello IT Service Management Connector under **OMS** > **Settings** > **Connected Sources.**</span></span>

![ITSMC connessi](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> <span data-ttu-id="8ac20-126">Per impostazione predefinita, hello connettore di gestione del servizio IT Aggiorna i dati della connessione hello una volta in ogni 24 ore.</span><span class="sxs-lookup"><span data-stu-id="8ac20-126">By default, hello IT Service Management Connector refreshes hello connection's data once in every 24 hours.</span></span> <span data-ttu-id="8ac20-127">toorefresh immediatamente per qualsiasi modello di modifiche o gli della connessione aggiornamenti dei dati apportate, fare clic su connessione tooyour avanti di hello aggiornamento pulsante visualizzato.</span><span class="sxs-lookup"><span data-stu-id="8ac20-127">toorefresh your connection's data instantly for any edits or template updates that you make, click hello refresh button displayed next tooyour connection.</span></span>

 ![Aggiornamento di ITSMC refresh](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a><span data-ttu-id="8ac20-129">Management Pack</span><span class="sxs-lookup"><span data-stu-id="8ac20-129">Management packs</span></span>
<span data-ttu-id="8ac20-130">Questa soluzione non richiede alcun pacchetto di gestione.</span><span class="sxs-lookup"><span data-stu-id="8ac20-130">This solution does not require any management packs.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="8ac20-131">Origini connesse</span><span class="sxs-lookup"><span data-stu-id="8ac20-131">Connected sources</span></span>

<span data-ttu-id="8ac20-132">Hello ITSM seguenti prodotti e servizi sono supportati dal connettore di gestione del servizio IT hello:</span><span class="sxs-lookup"><span data-stu-id="8ac20-132">hello following ITSM products/services are supported by hello IT Service Management Connector:</span></span>

- [<span data-ttu-id="8ac20-133">System Center Service Manager (SCSM)</span><span class="sxs-lookup"><span data-stu-id="8ac20-133">System Center Service Manager (SCSM)</span></span>](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="8ac20-134">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="8ac20-134">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="8ac20-135">Provance</span><span class="sxs-lookup"><span data-stu-id="8ac20-135">Provance</span></span>](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [<span data-ttu-id="8ac20-136">Cherwell</span><span class="sxs-lookup"><span data-stu-id="8ac20-136">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-hello-solution"></a><span data-ttu-id="8ac20-137">Utilizzo di soluzione hello</span><span class="sxs-lookup"><span data-stu-id="8ac20-137">Using hello solution</span></span>

<span data-ttu-id="8ac20-138">Una volta che ci si connette hello connettore di gestione del servizio IT OMS con il servizio ITSM, servizi Log Analitica hello avvia la raccolta dati hello da hello connesso ITSM prodotti o servizi.</span><span class="sxs-lookup"><span data-stu-id="8ac20-138">Once you connect hello OMS IT Service Management Connector with your ITSM service, hello Log Analytics services starts gathering hello data from hello connected ITSM products/service.</span></span>

> [!NOTE]
> - <span data-ttu-id="8ac20-139">I dati importati dalla soluzione IT Service Management Connector vengono visualizzati in Log Analytics come eventi denominati **ServiceDesk_CL**.</span><span class="sxs-lookup"><span data-stu-id="8ac20-139">Data imported by IT Service Management Connector solution appears in Log Analytics as events named **ServiceDesk_CL**.</span></span>
- <span data-ttu-id="8ac20-140">L'evento contiene un campo denominato **ServiceDeskWorkItemType_s**.</span><span class="sxs-lookup"><span data-stu-id="8ac20-140">Event contains a field named **ServiceDeskWorkItemType_s**.</span></span> <span data-ttu-id="8ac20-141">che il relativo valore come eventi imprevisti, richiedere o richiesta di modifica, a seconda di hello di elemento di lavoro dati contenuti in hello **ServiceDesk_CL** evento.</span><span class="sxs-lookup"><span data-stu-id="8ac20-141">which can take its value as incident, or change request, depending on hello work item data contained in hello **ServiceDesk_CL** event.</span></span>

## <a name="input-data"></a><span data-ttu-id="8ac20-142">Dati di input</span><span class="sxs-lookup"><span data-stu-id="8ac20-142">Input data</span></span>
<span data-ttu-id="8ac20-143">Gli elementi di lavoro importati da hello ITSM prodotti e servizi.</span><span class="sxs-lookup"><span data-stu-id="8ac20-143">Work items imported from hello ITSM products/services.</span></span>

<span data-ttu-id="8ac20-144">Hello informazioni riportate di seguito vengono illustrati esempi di dati raccolti dal connettore di gestione dei servizi IT hello:</span><span class="sxs-lookup"><span data-stu-id="8ac20-144">hello following information shows examples of data gathered by hello IT Service Management connector:</span></span>

> [!NOTE]
> <span data-ttu-id="8ac20-145">A seconda di hello tipo elemento di lavoro importato nel Log Analitica, **ServiceDesk_CL** contiene hello seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="8ac20-145">Depending on hello work item type imported into Log Analytics, **ServiceDesk_CL** contains hello following fields:</span></span>

<span data-ttu-id="8ac20-146">**Elemento di lavoro:** **Eventi imprevisti**</span><span class="sxs-lookup"><span data-stu-id="8ac20-146">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="8ac20-147">ServiceDeskWorkItemType_s="Incident"</span><span class="sxs-lookup"><span data-stu-id="8ac20-147">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="8ac20-148">**Fields**</span><span class="sxs-lookup"><span data-stu-id="8ac20-148">**Fields**</span></span>

- <span data-ttu-id="8ac20-149">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="8ac20-149">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="8ac20-150">ID Service Desk</span><span class="sxs-lookup"><span data-stu-id="8ac20-150">Service Desk ID</span></span>
- <span data-ttu-id="8ac20-151">Stato</span><span class="sxs-lookup"><span data-stu-id="8ac20-151">State</span></span>
- <span data-ttu-id="8ac20-152">Urgenza</span><span class="sxs-lookup"><span data-stu-id="8ac20-152">Urgency</span></span>
- <span data-ttu-id="8ac20-153">Impatto</span><span class="sxs-lookup"><span data-stu-id="8ac20-153">Impact</span></span>
- <span data-ttu-id="8ac20-154">Priorità</span><span class="sxs-lookup"><span data-stu-id="8ac20-154">Priority</span></span>
- <span data-ttu-id="8ac20-155">Riassegnazione</span><span class="sxs-lookup"><span data-stu-id="8ac20-155">Escalation</span></span>
- <span data-ttu-id="8ac20-156">Created By (Creato da)</span><span class="sxs-lookup"><span data-stu-id="8ac20-156">Created By</span></span>
- <span data-ttu-id="8ac20-157">Resolved By (Risolto da)</span><span class="sxs-lookup"><span data-stu-id="8ac20-157">Resolved By</span></span>
- <span data-ttu-id="8ac20-158">Closed By (Chiuso da)</span><span class="sxs-lookup"><span data-stu-id="8ac20-158">Closed By</span></span>
- <span data-ttu-id="8ac20-159">Sorgente</span><span class="sxs-lookup"><span data-stu-id="8ac20-159">Source</span></span>
- <span data-ttu-id="8ac20-160">Assegnato a </span><span class="sxs-lookup"><span data-stu-id="8ac20-160">Assigned To</span></span>
- <span data-ttu-id="8ac20-161">Categoria</span><span class="sxs-lookup"><span data-stu-id="8ac20-161">Category</span></span>
- <span data-ttu-id="8ac20-162">Titolo</span><span class="sxs-lookup"><span data-stu-id="8ac20-162">Title</span></span>
- <span data-ttu-id="8ac20-163">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8ac20-163">Description</span></span>
- <span data-ttu-id="8ac20-164">Data di creazione</span><span class="sxs-lookup"><span data-stu-id="8ac20-164">Created Date</span></span>
- <span data-ttu-id="8ac20-165">Data di chiusura</span><span class="sxs-lookup"><span data-stu-id="8ac20-165">Closed Date</span></span>
- <span data-ttu-id="8ac20-166">Data di risoluzione</span><span class="sxs-lookup"><span data-stu-id="8ac20-166">Resolved Date</span></span>
- <span data-ttu-id="8ac20-167">Data ultima modifica</span><span class="sxs-lookup"><span data-stu-id="8ac20-167">Last Modified Date</span></span>
- <span data-ttu-id="8ac20-168">Computer</span><span class="sxs-lookup"><span data-stu-id="8ac20-168">Computer</span></span>


<span data-ttu-id="8ac20-169">**Elemento di lavoro:****Richieste di modifica**</span><span class="sxs-lookup"><span data-stu-id="8ac20-169">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="8ac20-170">ServiceDeskWorkItemType_s="ChangeRequest"</span><span class="sxs-lookup"><span data-stu-id="8ac20-170">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="8ac20-171">**Fields**</span><span class="sxs-lookup"><span data-stu-id="8ac20-171">**Fields**</span></span>
- <span data-ttu-id="8ac20-172">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="8ac20-172">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="8ac20-173">ID Service Desk</span><span class="sxs-lookup"><span data-stu-id="8ac20-173">Service Desk ID</span></span>
- <span data-ttu-id="8ac20-174">Created By (Creato da)</span><span class="sxs-lookup"><span data-stu-id="8ac20-174">Created By</span></span>
- <span data-ttu-id="8ac20-175">Closed By (Chiuso da)</span><span class="sxs-lookup"><span data-stu-id="8ac20-175">Closed By</span></span>
- <span data-ttu-id="8ac20-176">Sorgente</span><span class="sxs-lookup"><span data-stu-id="8ac20-176">Source</span></span>
- <span data-ttu-id="8ac20-177">Assegnato a </span><span class="sxs-lookup"><span data-stu-id="8ac20-177">Assigned To</span></span>
- <span data-ttu-id="8ac20-178">Titolo</span><span class="sxs-lookup"><span data-stu-id="8ac20-178">Title</span></span>
- <span data-ttu-id="8ac20-179">Tipo</span><span class="sxs-lookup"><span data-stu-id="8ac20-179">Type</span></span>
- <span data-ttu-id="8ac20-180">Categoria</span><span class="sxs-lookup"><span data-stu-id="8ac20-180">Category</span></span>
- <span data-ttu-id="8ac20-181">Stato</span><span class="sxs-lookup"><span data-stu-id="8ac20-181">State</span></span>
- <span data-ttu-id="8ac20-182">Riassegnazione</span><span class="sxs-lookup"><span data-stu-id="8ac20-182">Escalation</span></span>
- <span data-ttu-id="8ac20-183">Conflict Status (Stato di conflitto)</span><span class="sxs-lookup"><span data-stu-id="8ac20-183">Conflict Status</span></span>
- <span data-ttu-id="8ac20-184">Urgenza</span><span class="sxs-lookup"><span data-stu-id="8ac20-184">Urgency</span></span>
- <span data-ttu-id="8ac20-185">Priorità</span><span class="sxs-lookup"><span data-stu-id="8ac20-185">Priority</span></span>
- <span data-ttu-id="8ac20-186">Rischio</span><span class="sxs-lookup"><span data-stu-id="8ac20-186">Risk</span></span>
- <span data-ttu-id="8ac20-187">Impatto</span><span class="sxs-lookup"><span data-stu-id="8ac20-187">Impact</span></span>
- <span data-ttu-id="8ac20-188">Assegnato a </span><span class="sxs-lookup"><span data-stu-id="8ac20-188">Assigned To</span></span>
- <span data-ttu-id="8ac20-189">Data di creazione</span><span class="sxs-lookup"><span data-stu-id="8ac20-189">Created Date</span></span>
- <span data-ttu-id="8ac20-190">Data di chiusura</span><span class="sxs-lookup"><span data-stu-id="8ac20-190">Closed Date</span></span>
- <span data-ttu-id="8ac20-191">Data ultima modifica</span><span class="sxs-lookup"><span data-stu-id="8ac20-191">Last Modified Date</span></span>
- <span data-ttu-id="8ac20-192">Data richiesta</span><span class="sxs-lookup"><span data-stu-id="8ac20-192">Requested Date</span></span>
- <span data-ttu-id="8ac20-193">Planned Start Date (Data di inizio pianificata)</span><span class="sxs-lookup"><span data-stu-id="8ac20-193">Planned Start Date</span></span>
- <span data-ttu-id="8ac20-194">Planned End Date (Data di fine pianificata)</span><span class="sxs-lookup"><span data-stu-id="8ac20-194">Planned End Date</span></span>
- <span data-ttu-id="8ac20-195">Work Start Date (Data di inizio lavoro)</span><span class="sxs-lookup"><span data-stu-id="8ac20-195">Work Start Date</span></span>
- <span data-ttu-id="8ac20-196">Work End Date (Data di fine pianificata)</span><span class="sxs-lookup"><span data-stu-id="8ac20-196">Work End Date</span></span>
- <span data-ttu-id="8ac20-197">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8ac20-197">Description</span></span>
- <span data-ttu-id="8ac20-198">Computer</span><span class="sxs-lookup"><span data-stu-id="8ac20-198">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="8ac20-199">Dati di output per un evento imprevisto ServiceNow</span><span class="sxs-lookup"><span data-stu-id="8ac20-199">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="8ac20-200">Campo OMS</span><span class="sxs-lookup"><span data-stu-id="8ac20-200">OMS field</span></span> | <span data-ttu-id="8ac20-201">Campo ITSM</span><span class="sxs-lookup"><span data-stu-id="8ac20-201">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="8ac20-202">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-202">ServiceDeskId_s</span></span>| <span data-ttu-id="8ac20-203">Number</span><span class="sxs-lookup"><span data-stu-id="8ac20-203">Number</span></span> |
| <span data-ttu-id="8ac20-204">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-204">IncidentState_s</span></span> | <span data-ttu-id="8ac20-205">Stato</span><span class="sxs-lookup"><span data-stu-id="8ac20-205">State</span></span> |
| <span data-ttu-id="8ac20-206">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-206">Urgency_s</span></span> |<span data-ttu-id="8ac20-207">Urgenza</span><span class="sxs-lookup"><span data-stu-id="8ac20-207">Urgency</span></span> |
| <span data-ttu-id="8ac20-208">Impact_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-208">Impact_s</span></span> |<span data-ttu-id="8ac20-209">Impatto</span><span class="sxs-lookup"><span data-stu-id="8ac20-209">Impact</span></span>|
| <span data-ttu-id="8ac20-210">Priority_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-210">Priority_s</span></span> | <span data-ttu-id="8ac20-211">Priorità</span><span class="sxs-lookup"><span data-stu-id="8ac20-211">Priority</span></span> |
| <span data-ttu-id="8ac20-212">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-212">CreatedBy_s</span></span> | <span data-ttu-id="8ac20-213">Aperto da</span><span class="sxs-lookup"><span data-stu-id="8ac20-213">Opened by</span></span> |
| <span data-ttu-id="8ac20-214">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-214">ResolvedBy_s</span></span> | <span data-ttu-id="8ac20-215">Risolto da</span><span class="sxs-lookup"><span data-stu-id="8ac20-215">Resolved by</span></span>|
| <span data-ttu-id="8ac20-216">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-216">ClosedBy_s</span></span>  | <span data-ttu-id="8ac20-217">Chiuso da</span><span class="sxs-lookup"><span data-stu-id="8ac20-217">Closed by</span></span> |
| <span data-ttu-id="8ac20-218">Source_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-218">Source_s</span></span>| <span data-ttu-id="8ac20-219">Tipo di contatto</span><span class="sxs-lookup"><span data-stu-id="8ac20-219">Contact type</span></span> |
| <span data-ttu-id="8ac20-220">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-220">AssignedTo_s</span></span> | <span data-ttu-id="8ac20-221">Troppo assegnato</span><span class="sxs-lookup"><span data-stu-id="8ac20-221">Assigned too</span></span> |
| <span data-ttu-id="8ac20-222">Category_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-222">Category_s</span></span> | <span data-ttu-id="8ac20-223">Categoria</span><span class="sxs-lookup"><span data-stu-id="8ac20-223">Category</span></span> |
| <span data-ttu-id="8ac20-224">Title_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-224">Title_s</span></span>|  <span data-ttu-id="8ac20-225">Breve descrizione</span><span class="sxs-lookup"><span data-stu-id="8ac20-225">Short description</span></span> |
| <span data-ttu-id="8ac20-226">Description_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-226">Description_s</span></span>|  <span data-ttu-id="8ac20-227">Note</span><span class="sxs-lookup"><span data-stu-id="8ac20-227">Notes</span></span> |
| <span data-ttu-id="8ac20-228">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="8ac20-228">CreatedDate_t</span></span>|  <span data-ttu-id="8ac20-229">Aperto</span><span class="sxs-lookup"><span data-stu-id="8ac20-229">Opened</span></span> |
| <span data-ttu-id="8ac20-230">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="8ac20-230">ClosedDate_t</span></span>| <span data-ttu-id="8ac20-231">closed</span><span class="sxs-lookup"><span data-stu-id="8ac20-231">closed</span></span>|
| <span data-ttu-id="8ac20-232">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="8ac20-232">ResolvedDate_t</span></span>|<span data-ttu-id="8ac20-233">Risolto</span><span class="sxs-lookup"><span data-stu-id="8ac20-233">Resolved</span></span>|
| <span data-ttu-id="8ac20-234">Computer</span><span class="sxs-lookup"><span data-stu-id="8ac20-234">Computer</span></span>  | <span data-ttu-id="8ac20-235">Elemento di configurazione</span><span class="sxs-lookup"><span data-stu-id="8ac20-235">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="8ac20-236">Dati di output per una richiesta di modifica ServiceNow</span><span class="sxs-lookup"><span data-stu-id="8ac20-236">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="8ac20-237">Campo OMS</span><span class="sxs-lookup"><span data-stu-id="8ac20-237">OMS field</span></span> | <span data-ttu-id="8ac20-238">Campo ITSM</span><span class="sxs-lookup"><span data-stu-id="8ac20-238">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="8ac20-239">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-239">ServiceDeskId_s</span></span>| <span data-ttu-id="8ac20-240">Number</span><span class="sxs-lookup"><span data-stu-id="8ac20-240">Number</span></span> |
| <span data-ttu-id="8ac20-241">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-241">CreatedBy_s</span></span> | <span data-ttu-id="8ac20-242">Richiesto da</span><span class="sxs-lookup"><span data-stu-id="8ac20-242">Requested by</span></span> |
| <span data-ttu-id="8ac20-243">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-243">ClosedBy_s</span></span> | <span data-ttu-id="8ac20-244">Chiuso da</span><span class="sxs-lookup"><span data-stu-id="8ac20-244">Closed by</span></span> |
| <span data-ttu-id="8ac20-245">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-245">AssignedTo_s</span></span> | <span data-ttu-id="8ac20-246">Troppo assegnato</span><span class="sxs-lookup"><span data-stu-id="8ac20-246">Assigned too</span></span> |
| <span data-ttu-id="8ac20-247">Title_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-247">Title_s</span></span>|  <span data-ttu-id="8ac20-248">Breve descrizione</span><span class="sxs-lookup"><span data-stu-id="8ac20-248">Short description</span></span> |
| <span data-ttu-id="8ac20-249">Type_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-249">Type_s</span></span>|  <span data-ttu-id="8ac20-250">Tipo</span><span class="sxs-lookup"><span data-stu-id="8ac20-250">Type</span></span> |
| <span data-ttu-id="8ac20-251">Category_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-251">Category_s</span></span>|  <span data-ttu-id="8ac20-252">Categoria</span><span class="sxs-lookup"><span data-stu-id="8ac20-252">Catgory</span></span> |
| <span data-ttu-id="8ac20-253">CRState_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-253">CRState_s</span></span>|  <span data-ttu-id="8ac20-254">Stato</span><span class="sxs-lookup"><span data-stu-id="8ac20-254">State</span></span>|
| <span data-ttu-id="8ac20-255">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-255">Urgency_s</span></span>|  <span data-ttu-id="8ac20-256">Urgenza</span><span class="sxs-lookup"><span data-stu-id="8ac20-256">Urgency</span></span> |
| <span data-ttu-id="8ac20-257">Priority_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-257">Priority_s</span></span>| <span data-ttu-id="8ac20-258">Priorità</span><span class="sxs-lookup"><span data-stu-id="8ac20-258">Priority</span></span>|
| <span data-ttu-id="8ac20-259">Risk_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-259">Risk_s</span></span>| <span data-ttu-id="8ac20-260">Rischio</span><span class="sxs-lookup"><span data-stu-id="8ac20-260">Risk</span></span>|
| <span data-ttu-id="8ac20-261">Impact_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-261">Impact_s</span></span>| <span data-ttu-id="8ac20-262">Impatto</span><span class="sxs-lookup"><span data-stu-id="8ac20-262">Impact</span></span>|
| <span data-ttu-id="8ac20-263">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="8ac20-263">RequestedDate_t</span></span>  | <span data-ttu-id="8ac20-264">Data richiesta</span><span class="sxs-lookup"><span data-stu-id="8ac20-264">Requested by date</span></span> |
| <span data-ttu-id="8ac20-265">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="8ac20-265">ClosedDate_t</span></span> | <span data-ttu-id="8ac20-266">Data di chiusura</span><span class="sxs-lookup"><span data-stu-id="8ac20-266">Closed date</span></span> |
| <span data-ttu-id="8ac20-267">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="8ac20-267">PlannedStartDate_t</span></span>  |     <span data-ttu-id="8ac20-268">Data di inizio pianificata</span><span class="sxs-lookup"><span data-stu-id="8ac20-268">Planned start date</span></span> |
| <span data-ttu-id="8ac20-269">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="8ac20-269">PlannedEndDate_t</span></span>  |   <span data-ttu-id="8ac20-270">Data di fine pianificata</span><span class="sxs-lookup"><span data-stu-id="8ac20-270">Planned end date</span></span> |
| <span data-ttu-id="8ac20-271">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="8ac20-271">WorkStartDate_t</span></span>  | <span data-ttu-id="8ac20-272">Data di inizio effettiva</span><span class="sxs-lookup"><span data-stu-id="8ac20-272">Actual start date</span></span> |
| <span data-ttu-id="8ac20-273">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="8ac20-273">WorkEndDate_t</span></span> | <span data-ttu-id="8ac20-274">Data di fine effettiva</span><span class="sxs-lookup"><span data-stu-id="8ac20-274">Actual end date</span></span>|
| <span data-ttu-id="8ac20-275">Description_s</span><span class="sxs-lookup"><span data-stu-id="8ac20-275">Description_s</span></span> | <span data-ttu-id="8ac20-276">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8ac20-276">Description</span></span> |
| <span data-ttu-id="8ac20-277">Computer</span><span class="sxs-lookup"><span data-stu-id="8ac20-277">Computer</span></span>  | <span data-ttu-id="8ac20-278">Elemento di configurazione</span><span class="sxs-lookup"><span data-stu-id="8ac20-278">Configuration Item</span></span> |

<span data-ttu-id="8ac20-279">**Schermata di esempio di Log Analytics per i dati ITSM:**</span><span class="sxs-lookup"><span data-stu-id="8ac20-279">**Sample Log Analytics screen for ITSM data:**</span></span>

![Schermata di Log Analytics](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a><span data-ttu-id="8ac20-281">IT Service Management connector: integrazione con altre soluzioni OMS</span><span class="sxs-lookup"><span data-stu-id="8ac20-281">IT Service Management connector – integration with other OMS solutions</span></span>

<span data-ttu-id="8ac20-282">Connettore di gestione del servizio IT, attualmente supporta l'integrazione con hello soluzione mappa del servizio.</span><span class="sxs-lookup"><span data-stu-id="8ac20-282">IT Service Management Connector, currently supports integration with hello Service Map solution.</span></span>

<span data-ttu-id="8ac20-283">Mappa del servizio individua automaticamente i componenti dell'applicazione in Windows hello e mappe e i sistemi Linux hello la comunicazione tra servizi.</span><span class="sxs-lookup"><span data-stu-id="8ac20-283">Service Map automatically discovers hello application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="8ac20-284">Consente di tooview i server come si immaginano – come sistemi interconnessi che offrono servizi critici.</span><span class="sxs-lookup"><span data-stu-id="8ac20-284">It allows you tooview your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="8ac20-285">L'elenco dei servizi mostra le connessioni fra i server, i processi e le porte di tutte le architetture connesse via TCP senza il bisogno di alcuna configurazione a parte l'installazione di un agente.</span><span class="sxs-lookup"><span data-stu-id="8ac20-285">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="8ac20-286">Altre informazioni: [Elenco dei servizi](../operations-management-suite/operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="8ac20-286">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="8ac20-287">L'integrazione, è possibile visualizzare hello service desk gli elementi creati in soluzioni ITSM hello come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="8ac20-287">With this integration, you can view hello service desk items created in hello ITSM solutions as shown in hello following example:</span></span>

![<span data-ttu-id="8ac20-288">Soluzione integrata</span><span class="sxs-lookup"><span data-stu-id="8ac20-288">Integrated solution</span></span> ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a><span data-ttu-id="8ac20-289">Creare elementi di lavoro ITSM per avvisi di OMS</span><span class="sxs-lookup"><span data-stu-id="8ac20-289">Create ITSM work items for OMS alerts</span></span>

<span data-ttu-id="8ac20-290">Per gli avvisi OMS hello, è possibile creare elementi di lavoro associati in origini ITSM hello connesso.</span><span class="sxs-lookup"><span data-stu-id="8ac20-290">For hello OMS alerts, you can create associated work items in hello connected ITSM sources.</span></span>  <span data-ttu-id="8ac20-291">toodo hello, questo uso seguente procedura:</span><span class="sxs-lookup"><span data-stu-id="8ac20-291">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="8ac20-292">Da **ricerca nei Log** finestra, eseguire una ricerca di log query tooview dati.</span><span class="sxs-lookup"><span data-stu-id="8ac20-292">From **Log Search** window, run a log search query tooview data.</span></span> <span data-ttu-id="8ac20-293">Risultati della query sono l'origine hello per gli elementi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8ac20-293">Query results are hello source for work items.</span></span>
2. <span data-ttu-id="8ac20-294">In **ricerca nei Log**, fare clic su **avviso** tooopen hello **Aggiungi regola di avviso** pagina.</span><span class="sxs-lookup"><span data-stu-id="8ac20-294">In **Log Search**, click **Alert** tooopen hello **Add Alert Rule** page.</span></span>

    ![Schermata di Log Analytics](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. <span data-ttu-id="8ac20-296">In hello **Aggiungi regola di avviso** finestra, fornire dettagli hello necessario per **nome**, **gravità**, **query di ricerca**, e  **Criteri di avviso** (misurazione finestra/metrica tempo).</span><span class="sxs-lookup"><span data-stu-id="8ac20-296">On hello **Add Alert Rule** window, provide hello required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="8ac20-297">Selezionare **Sì** per **Azioni ITSM**.</span><span class="sxs-lookup"><span data-stu-id="8ac20-297">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="8ac20-298">Selezionare la connessione ITSM hello **Seleziona connessione** elenco.</span><span class="sxs-lookup"><span data-stu-id="8ac20-298">Select your ITSM connection from hello **Select Connection** list.</span></span>
6. <span data-ttu-id="8ac20-299">Fornire dettagli hello come richiesto.</span><span class="sxs-lookup"><span data-stu-id="8ac20-299">Provide hello details as required.</span></span>
7. <span data-ttu-id="8ac20-300">un elemento di lavoro separata per ogni voce di log di hello questo avviso, seleziona toocreate **creare singoli elementi di lavoro per ogni voce di log** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="8ac20-300">toocreate a separate work item for each log entry of this alert, select hello **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="8ac20-301">Or</span><span class="sxs-lookup"><span data-stu-id="8ac20-301">Or</span></span>

    <span data-ttu-id="8ac20-302">lasciare questa casella di controllo deselezionata toocreate solo un elemento di lavoro per qualsiasi numero di voci di log in questo avviso.</span><span class="sxs-lookup"><span data-stu-id="8ac20-302">leave this checkbox unselected toocreate only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="8ac20-303">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8ac20-303">Click **Save**.</span></span>

<span data-ttu-id="8ac20-304">verrà creata nell'avviso OMS Hello **avvisi**.</span><span class="sxs-lookup"><span data-stu-id="8ac20-304">hello OMS alert will be created under **Alerts**.</span></span> <span data-ttu-id="8ac20-305">Hello lavoro della connessione corrispondente ITSM gli elementi vengono creati quando viene soddisfatta la condizione dell'avviso di hello specificato.</span><span class="sxs-lookup"><span data-stu-id="8ac20-305">hello corresponding ITSM connection's work items are created when hello specified alert's condition is met.</span></span>

## <a name="create-itsm-work-items-from-oms-logs"></a><span data-ttu-id="8ac20-306">Creare elementi di lavoro ITSM da log di OMS</span><span class="sxs-lookup"><span data-stu-id="8ac20-306">Create ITSM work items from OMS logs</span></span>

<span data-ttu-id="8ac20-307">È possibile creare elementi di lavoro nelle origini ITSM hello connesso tramite una ricerca nei Log di OMS.</span><span class="sxs-lookup"><span data-stu-id="8ac20-307">You can create work items in hello connected ITSM sources by using OMS Log Search.</span></span> <span data-ttu-id="8ac20-308">toodo hello, questo uso seguente procedura:</span><span class="sxs-lookup"><span data-stu-id="8ac20-308">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="8ac20-309">Da **ricerca nei Log**, cercare i dati di hello richiesto, selezionare dettagli hello e fare clic su **Crea elemento di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="8ac20-309">From **Log Search**,  search hello required data, select hello detail, and click **Create work item**.</span></span>

    <span data-ttu-id="8ac20-310">Hello **elemento di lavoro di ITSM creare** verrà visualizzata la finestra:</span><span class="sxs-lookup"><span data-stu-id="8ac20-310">hello **Create ITSM Work item** window appears:</span></span>

    ![Schermata di Log Analytics](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   <span data-ttu-id="8ac20-312">Aggiungere i seguenti dettagli hello:</span><span class="sxs-lookup"><span data-stu-id="8ac20-312">Add hello following details:</span></span>

  - <span data-ttu-id="8ac20-313">**Titolo elemento di lavoro**: titolo dell'elemento di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="8ac20-313">**Work item Title**: Title for hello work item.</span></span>
  - <span data-ttu-id="8ac20-314">**Descrizione elemento di lavoro**: descrizione per il nuovo elemento di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="8ac20-314">**Work item Description**: Description for hello new work item.</span></span>
  - <span data-ttu-id="8ac20-315">**Computer interessati**: nome del computer hello in cui è stati trovati i dati di log.</span><span class="sxs-lookup"><span data-stu-id="8ac20-315">**Affected Computer**: Name of hello computer where this log data was found.</span></span>
  - <span data-ttu-id="8ac20-316">**Selezionare connessione**: connessione ITSM in cui si desidera toocreate questo elemento di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8ac20-316">**Select Connection**:  ITSM connection in which you want toocreate this work item.</span></span>
  - <span data-ttu-id="8ac20-317">**Elemento di lavoro**: tipo di elemento di lavoro.</span><span class="sxs-lookup"><span data-stu-id="8ac20-317">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="8ac20-318">Fare clic su un modello di elemento di lavoro esistente per un evento imprevisto, toouse **Sì** in **elemento di lavoro genera basato sul modello di hello** opzione e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="8ac20-318">toouse an existing work item template for an incident, click **Yes** under **Generate work item based on hello template** option and then click **Create**.</span></span>

    <span data-ttu-id="8ac20-319">Oppure</span><span class="sxs-lookup"><span data-stu-id="8ac20-319">Or,</span></span>

    <span data-ttu-id="8ac20-320">Fare clic su **n** se si desiderano tooprovide i valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="8ac20-320">Click **No** if you want tooprovide your customized values.</span></span>

4. <span data-ttu-id="8ac20-321">Specificare i valori appropriati di hello in hello **tipo contatto**, **impatto**, **urgenza**, **categoria**, e **Sub Category**  caselle di testo e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="8ac20-321">Provide hello appropriate values in hello **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>

<span data-ttu-id="8ac20-322">verrà creato l'elemento di lavoro Hello in hello ITSM, che è anche possibile visualizzare in OMS.</span><span class="sxs-lookup"><span data-stu-id="8ac20-322">hello work item will be created in hello ITSM, which you can also view in OMS.</span></span>

## <a name="troubleshoot-itsm-connections-in-oms"></a><span data-ttu-id="8ac20-323">Risolvere i problemi delle connessioni ITSM in OMS</span><span class="sxs-lookup"><span data-stu-id="8ac20-323">Troubleshoot ITSM connections in OMS</span></span>
1.  <span data-ttu-id="8ac20-324">Se si verifica un errore di connessione nell'interfaccia utente dell'origine connesso e viene visualizzato hello **errore durante il salvataggio di connessione** dei messaggi, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8ac20-324">If connection fails from connected source's UI and you get hello **Error in saving connection** message, do hello following:</span></span>
 - <span data-ttu-id="8ac20-325">In caso di connessioni a ServiceNow, Cherwell e Provance, assicurarsi di segreto di hello correttamente immesso nome utente/password e il client ID e client per ciascuna delle connessioni hello.</span><span class="sxs-lookup"><span data-stu-id="8ac20-325">In case of ServiceNow, Cherwell and Provance connections, ensure you correctly entered  hello username/password and  client ID/client secret  for each of hello connections.</span></span> <span data-ttu-id="8ac20-326">Se l'errore hello persiste, controllare se si dispone di privilegi sufficienti nella connessione di hello corrispondente ITSM prodotto toomake hello.</span><span class="sxs-lookup"><span data-stu-id="8ac20-326">If hello error persists, check if you have sufficient privileges  in hello corresponding ITSM product toomake hello connection.</span></span>
 - <span data-ttu-id="8ac20-327">In caso di Service Manager, verificare che hello Web app è stata distribuita correttamente e viene creata la connessione ibrida.</span><span class="sxs-lookup"><span data-stu-id="8ac20-327">In case of Service Manager, ensure that hello Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="8ac20-328">connessione di hello tooverify è stata stabilita con il computer di Service Manager locale hello, visitare l'URL dell'app Web hello come descritto nella documentazione di hello per rendere hello [connessione ibrida](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="8ac20-328">tooverify hello connection is successfully established with hello on-prem Service Manager machine, visit hello  Web app URL as detailed in hello documentation for making hello [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>

2.  <span data-ttu-id="8ac20-329">Se i dati da ServiceNow non sono recupero sincronizzati in OMS, verificare che tale istanza di ServiceNow hello non è sospeso.</span><span class="sxs-lookup"><span data-stu-id="8ac20-329">If data from ServiceNow is not getting synced in OMS, ensure that hello ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="8ac20-330">In questo momento potrebbe verificarsi in hello ServiceNow Dev casi, quando è inattivo.</span><span class="sxs-lookup"><span data-stu-id="8ac20-330">This might sometime happen in hello ServiceNow Dev instances, when idle.</span></span> <span data-ttu-id="8ac20-331">Else, segnala un problema di hello.</span><span class="sxs-lookup"><span data-stu-id="8ac20-331">Else, report hello issue.</span></span>
3.  <span data-ttu-id="8ac20-332">Se gli avvisi vengono recupero generati da OMS ma non sono recupero creati elementi di lavoro nel prodotto ITSM o elementi di configurazione non ricevono gli elementi creati collegato toowork o per qualsiasi informazioni generiche, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="8ac20-332">If Alerts are getting fired from OMS but work items are not getting created in ITSM product or configuration items are not getting created/linked toowork items or for any generic information, do hello following:</span></span>
 -  <span data-ttu-id="8ac20-333">Soluzione di connettore di gestione del servizio IT nel portale OMS è possibile tooget usato un riepilogo delle connessioni/lavoro gli elementi e i computer e così via. Scegliere il messaggio di errore hello nel pannello stato hello, passare troppo**ricerca nei Log** e visualizzare connessione hello con errore hello utilizzando i dettagli di hello nel messaggio di errore hello.</span><span class="sxs-lookup"><span data-stu-id="8ac20-333">IT Service Management Connector solution in OMS portal could be used tooget a summary of connections/work items/computers etc. Click hello error message in hello status blade, navigate too**Log Search** and view hello connection that has hello error by using hello details in hello error message.</span></span>
 - <span data-ttu-id="8ac20-334">è possibile visualizzare direttamente le informazioni relative a errori/hello in hello **ricerca nei Log** pagina *tipo = ServiceDeskLog_CL*.</span><span class="sxs-lookup"><span data-stu-id="8ac20-334">you can directly view hello errors/related information in hello **Log Search** page using *Type=ServiceDeskLog_CL*.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="8ac20-335">Risolvere i problemi di distribuzione dell’app Web Service Manager</span><span class="sxs-lookup"><span data-stu-id="8ac20-335">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="8ac20-336">In caso di problemi con la distribuzione di app web, assicurarsi di disporre di autorizzazioni sufficienti nella sottoscrizione hello indicato toocreate/distribuire le risorse.</span><span class="sxs-lookup"><span data-stu-id="8ac20-336">In case of any trouble with web app deployment, ensure you have sufficient permissions in hello subscription mentioned toocreate/deploy resources.</span></span>
2.  <span data-ttu-id="8ac20-337">Se **riferimento all'oggetto non impostato tooinstance di un oggetto** viene visualizzato il messaggio di errore durante l'esecuzione di hello [script](log-analytics-itsmc-service-manager-script.md) verificare di avere immesso i valori validi in **configurazione utente**sezione.</span><span class="sxs-lookup"><span data-stu-id="8ac20-337">If **Object reference not set tooinstance of an object** error message appears while running hello [script](log-analytics-itsmc-service-manager-script.md) ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="8ac20-338">Se non si toocreate service bus inoltro dello spazio dei nomi, verificare che hello necessarie a provider di risorse è registrato nella sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="8ac20-338">If you fail toocreate service bus relay namespace, ensure that hello required resource provider is registered in hello subscription.</span></span> <span data-ttu-id="8ac20-339">Se non è registrato, crearla manualmente dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8ac20-339">If not registered, manually create it from hello Azure portal.</span></span> <span data-ttu-id="8ac20-340">È inoltre possibile creare mentre [creazione connessione ibrida hello](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ac20-340">You can also create it while [creating hello hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from hello Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="8ac20-341">Contatti</span><span class="sxs-lookup"><span data-stu-id="8ac20-341">Contact us</span></span>

<span data-ttu-id="8ac20-342">Per qualsiasi query o i commenti e suggerimenti su hello connettore di gestione del servizio IT, contattare Microsoft all'indirizzo [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="8ac20-342">For any queries or feedback on hello IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ac20-343">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8ac20-343">Next steps</span></span>
<span data-ttu-id="8ac20-344">[Aggiungere ITSM prodotti e servizi tooIT connettore del servizio di gestione](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="8ac20-344">[Add ITSM products/services tooIT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
