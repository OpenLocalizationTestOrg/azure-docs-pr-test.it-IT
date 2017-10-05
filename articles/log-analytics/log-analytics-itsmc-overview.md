---
title: IT Service Management Connector in OMS | Microsoft Docs
description: Usare IT Service Management Connector per monitorare e gestire centralmente gli elementi di lavoro di ITSM in OMS e risolvere rapidamente eventuali problemi.
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
ms.openlocfilehash: 54974ef06efdae69ddbfa12b1ba9278b48b113d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a><span data-ttu-id="58442-103">Gestire centralmente gli elementi di lavoro ITSM con IT Service Management Connector (anteprima)</span><span class="sxs-lookup"><span data-stu-id="58442-103">Centrally manage ITSM work items using IT Service Management Connector (Preview)</span></span>

![Simbolo di IT Service Management Connector](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="58442-105">È possibile usare IT Service Management Connector (ITSMC) in Log Analytics di OMS per monitorare e gestire centralmente gli elementi di lavoro nei prodotti o servizi di ITSM.</span><span class="sxs-lookup"><span data-stu-id="58442-105">You can use the IT Service Management Connector (ITSMC) in OMS Log Analytics to centrally monitor and manage work items across your ITSM products/services.</span></span>

<span data-ttu-id="58442-106">IT Service Management Connector integra i prodotti e i servizi di gestione IT (ITSM) esistenti con Log Analytics di OMS.</span><span class="sxs-lookup"><span data-stu-id="58442-106">The IT Service Management Connector integrates your existing IT Service Management (ITSM) products and services with OMS Log Analytics.</span></span>  <span data-ttu-id="58442-107">La soluzione presenta un'integrazione bidirezionale con i prodotti e i servizi ITSM, in cui offre agli utenti OMS un'opzione per creare eventi imprevisti, avvisi o eventi nella soluzione ITSM.</span><span class="sxs-lookup"><span data-stu-id="58442-107">The solution has bidirectional integration with ITSM products/services, where it provides the OMS users an option to create incidents, alerts, or events in ITSM solution.</span></span> <span data-ttu-id="58442-108">Il connettore importa anche dati, ad esempio eventi imprevisti e richieste di modifica dalla soluzione ITSM in Log Analytics di OMS.</span><span class="sxs-lookup"><span data-stu-id="58442-108">The connector also  imports data such as incidents, and change requests from ITSM solution into OMS Log Analytics.</span></span>

<span data-ttu-id="58442-109">Con IT Service Management Connector è possibile:</span><span class="sxs-lookup"><span data-stu-id="58442-109">With IT Service Management Connector, you can:</span></span>

  - <span data-ttu-id="58442-110">Monitorare e gestire centralmente gli elementi di lavoro per i prodotti e i servizi ITSM usati nell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="58442-110">Centrally monitor and manage work items for ITSM products/services used across your organization.</span></span>
  - <span data-ttu-id="58442-111">Creare elementi di lavoro ITSM, ad esempio avvisi, eventi, eventi imprevisto, in ITSM dagli avvisi OMS e tramite la ricerca log.</span><span class="sxs-lookup"><span data-stu-id="58442-111">Create ITSM work items (like alert, event, incident) in ITSM from OMS alerts and through log search.</span></span>
  - <span data-ttu-id="58442-112">Leggere gli eventi imprevisti e richieste di modifica dalla soluzione ITSM e correlare i dati di log rilevanti nell'area di lavoro di Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="58442-112">Read incidents and change requests from your ITSM solution and correlate with relevant log data in Log Analytics workspace.</span></span>
  - <span data-ttu-id="58442-113">Trovare tutti gli eventi imprevisti e non comuni e risolverli, anche prima che gli utenti finali si rivolgano e li segnalino al supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="58442-113">Find any unexpected and unusual events and resolve them, even before the end users call and report them to the helpdesk.</span></span>
  - <span data-ttu-id="58442-114">Importare i dati degli elementi di lavoro in Log Analytics e creare report indicatori di prestazioni chiave.</span><span class="sxs-lookup"><span data-stu-id="58442-114">Import work items data into Log Analytics and create key performance indicator (KPI) reports.</span></span>  <span data-ttu-id="58442-115">Grazie all'uso di questi report, è possibile individuare, valutare e agire su diversi elementi importanti, ad esempio la valutazione della presenza di malware.</span><span class="sxs-lookup"><span data-stu-id="58442-115">Using these reports, you can identify, assess and act on several important items such as malware assessment.</span></span>
  - <span data-ttu-id="58442-116">Visualizzare i dashboard curati per ottenere informazioni approfondite su eventi imprevisti, richieste di modifica e sistemi interessati.</span><span class="sxs-lookup"><span data-stu-id="58442-116">View curated dashboards for deeper insights on incidents, change requests and impacted systems.</span></span>
  - <span data-ttu-id="58442-117">Risolvere i problemi più rapidamente tramite correlazione con altre soluzioni di gestione nell'area di lavoro Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="58442-117">Troubleshoot faster by correlating with other management solutions in the Log Analytics workspace.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="58442-118">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="58442-118">Prerequisites</span></span>

<span data-ttu-id="58442-119">Per importare gli elementi di lavoro ITSM in Log Analytics di OMS, la soluzione richiede una connessione tra IT Service Management Connector in OMS e i prodotti o i servizi ITSM da cui si importano gli elementi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="58442-119">To import the ITSM work items into OMS Log Analytics, the solution requires a connection between the IT Service Management Connector in the OMS and the IT SM product/service from which you import the work items.</span></span>


## <a name="configuration"></a><span data-ttu-id="58442-120">Configurazione</span><span class="sxs-lookup"><span data-stu-id="58442-120">Configuration</span></span>

<span data-ttu-id="58442-121">Aggiungere la soluzione IT Service Management Connector all'area di lavoro di OMS usando la procedura descritta in [Aggiungere soluzioni di Log Analytics dalla raccolta soluzioni](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="58442-121">Add the IT Service Management Connector solution to your OMS work space, using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="58442-122">Riquadro di IT Service Management Connector come appare nella raccolta soluzioni:</span><span class="sxs-lookup"><span data-stu-id="58442-122">IT Service Management Connector tile as you see in the Solutions gallery:</span></span>

![riquadro connettore](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

<span data-ttu-id="58442-124">Dopo averlo aggiunto correttamente, IT Service Management Connector viene visualizzato in **OMS** > **Impostazioni** > **Origini connesse.**</span><span class="sxs-lookup"><span data-stu-id="58442-124">After successful addition, you will see the IT Service Management Connector under **OMS** > **Settings** > **Connected Sources.**</span></span>

![ITSMC connessi](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> <span data-ttu-id="58442-126">Per impostazione predefinita, IT Service Management Connector aggiorna i dati della connession ogni 24 ore.</span><span class="sxs-lookup"><span data-stu-id="58442-126">By default, the IT Service Management Connector refreshes the connection's data once in every 24 hours.</span></span> <span data-ttu-id="58442-127">Per aggiornare i dati della connessione immediatamente in caso di eventuali modifiche o aggiornamenti del modello, fare clic sul pulsante di aggiornamento posto accanto alla connessione.</span><span class="sxs-lookup"><span data-stu-id="58442-127">To refresh your connection's data instantly for any edits or template updates that you make, click the refresh button displayed next to your connection.</span></span>

 ![Aggiornamento di ITSMC refresh](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a><span data-ttu-id="58442-129">Management Pack</span><span class="sxs-lookup"><span data-stu-id="58442-129">Management packs</span></span>
<span data-ttu-id="58442-130">Questa soluzione non richiede alcun pacchetto di gestione.</span><span class="sxs-lookup"><span data-stu-id="58442-130">This solution does not require any management packs.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="58442-131">Origini connesse</span><span class="sxs-lookup"><span data-stu-id="58442-131">Connected sources</span></span>

<span data-ttu-id="58442-132">I seguenti prodotti o servizi ITSM sono supportati da IT Service Management Connector:</span><span class="sxs-lookup"><span data-stu-id="58442-132">The following ITSM products/services are supported by the IT Service Management Connector:</span></span>

- [<span data-ttu-id="58442-133">System Center Service Manager (SCSM)</span><span class="sxs-lookup"><span data-stu-id="58442-133">System Center Service Manager (SCSM)</span></span>](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="58442-134">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="58442-134">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="58442-135">Provance</span><span class="sxs-lookup"><span data-stu-id="58442-135">Provance</span></span>](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [<span data-ttu-id="58442-136">Cherwell</span><span class="sxs-lookup"><span data-stu-id="58442-136">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-the-solution"></a><span data-ttu-id="58442-137">Uso della soluzione</span><span class="sxs-lookup"><span data-stu-id="58442-137">Using the solution</span></span>

<span data-ttu-id="58442-138">Dopo aver collegato OMS IT Service Management Connector al servizio ITSM, il servizio Log Analytics inizia a raccogliere i dati dal servizio/prodotto ITSM connesso.</span><span class="sxs-lookup"><span data-stu-id="58442-138">Once you connect the OMS IT Service Management Connector with your ITSM service, the Log Analytics services starts gathering the data from the connected ITSM products/service.</span></span>

> [!NOTE]
> - <span data-ttu-id="58442-139">I dati importati dalla soluzione IT Service Management Connector vengono visualizzati in Log Analytics come eventi denominati **ServiceDesk_CL**.</span><span class="sxs-lookup"><span data-stu-id="58442-139">Data imported by IT Service Management Connector solution appears in Log Analytics as events named **ServiceDesk_CL**.</span></span>
- <span data-ttu-id="58442-140">L'evento contiene un campo denominato **ServiceDeskWorkItemType_s**.</span><span class="sxs-lookup"><span data-stu-id="58442-140">Event contains a field named **ServiceDeskWorkItemType_s**.</span></span> <span data-ttu-id="58442-141">che può prendere il proprio valore come evento imprevisto o richiesta di modifica, a seconda dei dati dell'elemento di lavoro contenuti nell'evento **ServiceDesk_CL**.</span><span class="sxs-lookup"><span data-stu-id="58442-141">which can take its value as incident, or change request, depending on the work item data contained in the **ServiceDesk_CL** event.</span></span>

## <a name="input-data"></a><span data-ttu-id="58442-142">Dati di input</span><span class="sxs-lookup"><span data-stu-id="58442-142">Input data</span></span>
<span data-ttu-id="58442-143">Elementi di lavoro importati dai prodotti/servizi ITSM.</span><span class="sxs-lookup"><span data-stu-id="58442-143">Work items imported from the ITSM products/services.</span></span>

<span data-ttu-id="58442-144">Le informazioni seguenti mostrano esempi di dati raccolti da IT Service Management Connector:</span><span class="sxs-lookup"><span data-stu-id="58442-144">The following information shows examples of data gathered by the IT Service Management connector:</span></span>

> [!NOTE]
> <span data-ttu-id="58442-145">A seconda del tipo di elemento di lavoro importato in Log Analytics, **ServiceDesk_CL** contiene i campi seguenti:</span><span class="sxs-lookup"><span data-stu-id="58442-145">Depending on the work item type imported into Log Analytics, **ServiceDesk_CL** contains the following fields:</span></span>

<span data-ttu-id="58442-146">**Elemento di lavoro:** **Eventi imprevisti**</span><span class="sxs-lookup"><span data-stu-id="58442-146">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="58442-147">ServiceDeskWorkItemType_s="Incident"</span><span class="sxs-lookup"><span data-stu-id="58442-147">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="58442-148">**Fields**</span><span class="sxs-lookup"><span data-stu-id="58442-148">**Fields**</span></span>

- <span data-ttu-id="58442-149">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="58442-149">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="58442-150">ID Service Desk</span><span class="sxs-lookup"><span data-stu-id="58442-150">Service Desk ID</span></span>
- <span data-ttu-id="58442-151">Stato</span><span class="sxs-lookup"><span data-stu-id="58442-151">State</span></span>
- <span data-ttu-id="58442-152">Urgenza</span><span class="sxs-lookup"><span data-stu-id="58442-152">Urgency</span></span>
- <span data-ttu-id="58442-153">Impatto</span><span class="sxs-lookup"><span data-stu-id="58442-153">Impact</span></span>
- <span data-ttu-id="58442-154">Priorità</span><span class="sxs-lookup"><span data-stu-id="58442-154">Priority</span></span>
- <span data-ttu-id="58442-155">Riassegnazione</span><span class="sxs-lookup"><span data-stu-id="58442-155">Escalation</span></span>
- <span data-ttu-id="58442-156">Created By (Creato da)</span><span class="sxs-lookup"><span data-stu-id="58442-156">Created By</span></span>
- <span data-ttu-id="58442-157">Resolved By (Risolto da)</span><span class="sxs-lookup"><span data-stu-id="58442-157">Resolved By</span></span>
- <span data-ttu-id="58442-158">Closed By (Chiuso da)</span><span class="sxs-lookup"><span data-stu-id="58442-158">Closed By</span></span>
- <span data-ttu-id="58442-159">Sorgente</span><span class="sxs-lookup"><span data-stu-id="58442-159">Source</span></span>
- <span data-ttu-id="58442-160">Assegnato a </span><span class="sxs-lookup"><span data-stu-id="58442-160">Assigned To</span></span>
- <span data-ttu-id="58442-161">Categoria</span><span class="sxs-lookup"><span data-stu-id="58442-161">Category</span></span>
- <span data-ttu-id="58442-162">Titolo</span><span class="sxs-lookup"><span data-stu-id="58442-162">Title</span></span>
- <span data-ttu-id="58442-163">Descrizione</span><span class="sxs-lookup"><span data-stu-id="58442-163">Description</span></span>
- <span data-ttu-id="58442-164">Data di creazione</span><span class="sxs-lookup"><span data-stu-id="58442-164">Created Date</span></span>
- <span data-ttu-id="58442-165">Data di chiusura</span><span class="sxs-lookup"><span data-stu-id="58442-165">Closed Date</span></span>
- <span data-ttu-id="58442-166">Data di risoluzione</span><span class="sxs-lookup"><span data-stu-id="58442-166">Resolved Date</span></span>
- <span data-ttu-id="58442-167">Data ultima modifica</span><span class="sxs-lookup"><span data-stu-id="58442-167">Last Modified Date</span></span>
- <span data-ttu-id="58442-168">Computer</span><span class="sxs-lookup"><span data-stu-id="58442-168">Computer</span></span>


<span data-ttu-id="58442-169">**Elemento di lavoro:** **Richieste di modifica**</span><span class="sxs-lookup"><span data-stu-id="58442-169">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="58442-170">ServiceDeskWorkItemType_s="ChangeRequest"</span><span class="sxs-lookup"><span data-stu-id="58442-170">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="58442-171">**Fields**</span><span class="sxs-lookup"><span data-stu-id="58442-171">**Fields**</span></span>
- <span data-ttu-id="58442-172">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="58442-172">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="58442-173">ID Service Desk</span><span class="sxs-lookup"><span data-stu-id="58442-173">Service Desk ID</span></span>
- <span data-ttu-id="58442-174">Created By (Creato da)</span><span class="sxs-lookup"><span data-stu-id="58442-174">Created By</span></span>
- <span data-ttu-id="58442-175">Closed By (Chiuso da)</span><span class="sxs-lookup"><span data-stu-id="58442-175">Closed By</span></span>
- <span data-ttu-id="58442-176">Sorgente</span><span class="sxs-lookup"><span data-stu-id="58442-176">Source</span></span>
- <span data-ttu-id="58442-177">Assegnato a </span><span class="sxs-lookup"><span data-stu-id="58442-177">Assigned To</span></span>
- <span data-ttu-id="58442-178">Titolo</span><span class="sxs-lookup"><span data-stu-id="58442-178">Title</span></span>
- <span data-ttu-id="58442-179">Tipo</span><span class="sxs-lookup"><span data-stu-id="58442-179">Type</span></span>
- <span data-ttu-id="58442-180">Categoria</span><span class="sxs-lookup"><span data-stu-id="58442-180">Category</span></span>
- <span data-ttu-id="58442-181">Stato</span><span class="sxs-lookup"><span data-stu-id="58442-181">State</span></span>
- <span data-ttu-id="58442-182">Riassegnazione</span><span class="sxs-lookup"><span data-stu-id="58442-182">Escalation</span></span>
- <span data-ttu-id="58442-183">Conflict Status (Stato di conflitto)</span><span class="sxs-lookup"><span data-stu-id="58442-183">Conflict Status</span></span>
- <span data-ttu-id="58442-184">Urgenza</span><span class="sxs-lookup"><span data-stu-id="58442-184">Urgency</span></span>
- <span data-ttu-id="58442-185">Priorità</span><span class="sxs-lookup"><span data-stu-id="58442-185">Priority</span></span>
- <span data-ttu-id="58442-186">Rischio</span><span class="sxs-lookup"><span data-stu-id="58442-186">Risk</span></span>
- <span data-ttu-id="58442-187">Impatto</span><span class="sxs-lookup"><span data-stu-id="58442-187">Impact</span></span>
- <span data-ttu-id="58442-188">Assegnato a </span><span class="sxs-lookup"><span data-stu-id="58442-188">Assigned To</span></span>
- <span data-ttu-id="58442-189">Data di creazione</span><span class="sxs-lookup"><span data-stu-id="58442-189">Created Date</span></span>
- <span data-ttu-id="58442-190">Data di chiusura</span><span class="sxs-lookup"><span data-stu-id="58442-190">Closed Date</span></span>
- <span data-ttu-id="58442-191">Data ultima modifica</span><span class="sxs-lookup"><span data-stu-id="58442-191">Last Modified Date</span></span>
- <span data-ttu-id="58442-192">Data richiesta</span><span class="sxs-lookup"><span data-stu-id="58442-192">Requested Date</span></span>
- <span data-ttu-id="58442-193">Planned Start Date (Data di inizio pianificata)</span><span class="sxs-lookup"><span data-stu-id="58442-193">Planned Start Date</span></span>
- <span data-ttu-id="58442-194">Planned End Date (Data di fine pianificata)</span><span class="sxs-lookup"><span data-stu-id="58442-194">Planned End Date</span></span>
- <span data-ttu-id="58442-195">Work Start Date (Data di inizio lavoro)</span><span class="sxs-lookup"><span data-stu-id="58442-195">Work Start Date</span></span>
- <span data-ttu-id="58442-196">Work End Date (Data di fine pianificata)</span><span class="sxs-lookup"><span data-stu-id="58442-196">Work End Date</span></span>
- <span data-ttu-id="58442-197">Descrizione</span><span class="sxs-lookup"><span data-stu-id="58442-197">Description</span></span>
- <span data-ttu-id="58442-198">Computer</span><span class="sxs-lookup"><span data-stu-id="58442-198">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="58442-199">Dati di output per un evento imprevisto ServiceNow</span><span class="sxs-lookup"><span data-stu-id="58442-199">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="58442-200">Campo OMS</span><span class="sxs-lookup"><span data-stu-id="58442-200">OMS field</span></span> | <span data-ttu-id="58442-201">Campo ITSM</span><span class="sxs-lookup"><span data-stu-id="58442-201">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="58442-202">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="58442-202">ServiceDeskId_s</span></span>| <span data-ttu-id="58442-203">Number</span><span class="sxs-lookup"><span data-stu-id="58442-203">Number</span></span> |
| <span data-ttu-id="58442-204">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="58442-204">IncidentState_s</span></span> | <span data-ttu-id="58442-205">Stato</span><span class="sxs-lookup"><span data-stu-id="58442-205">State</span></span> |
| <span data-ttu-id="58442-206">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="58442-206">Urgency_s</span></span> |<span data-ttu-id="58442-207">Urgenza</span><span class="sxs-lookup"><span data-stu-id="58442-207">Urgency</span></span> |
| <span data-ttu-id="58442-208">Impact_s</span><span class="sxs-lookup"><span data-stu-id="58442-208">Impact_s</span></span> |<span data-ttu-id="58442-209">Impatto</span><span class="sxs-lookup"><span data-stu-id="58442-209">Impact</span></span>|
| <span data-ttu-id="58442-210">Priority_s</span><span class="sxs-lookup"><span data-stu-id="58442-210">Priority_s</span></span> | <span data-ttu-id="58442-211">Priorità</span><span class="sxs-lookup"><span data-stu-id="58442-211">Priority</span></span> |
| <span data-ttu-id="58442-212">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="58442-212">CreatedBy_s</span></span> | <span data-ttu-id="58442-213">Aperto da</span><span class="sxs-lookup"><span data-stu-id="58442-213">Opened by</span></span> |
| <span data-ttu-id="58442-214">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="58442-214">ResolvedBy_s</span></span> | <span data-ttu-id="58442-215">Risolto da</span><span class="sxs-lookup"><span data-stu-id="58442-215">Resolved by</span></span>|
| <span data-ttu-id="58442-216">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="58442-216">ClosedBy_s</span></span>  | <span data-ttu-id="58442-217">Chiuso da</span><span class="sxs-lookup"><span data-stu-id="58442-217">Closed by</span></span> |
| <span data-ttu-id="58442-218">Source_s</span><span class="sxs-lookup"><span data-stu-id="58442-218">Source_s</span></span>| <span data-ttu-id="58442-219">Tipo di contatto</span><span class="sxs-lookup"><span data-stu-id="58442-219">Contact type</span></span> |
| <span data-ttu-id="58442-220">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="58442-220">AssignedTo_s</span></span> | <span data-ttu-id="58442-221">Assegnato a</span><span class="sxs-lookup"><span data-stu-id="58442-221">Assigned to</span></span>  |
| <span data-ttu-id="58442-222">Category_s</span><span class="sxs-lookup"><span data-stu-id="58442-222">Category_s</span></span> | <span data-ttu-id="58442-223">Categoria</span><span class="sxs-lookup"><span data-stu-id="58442-223">Category</span></span> |
| <span data-ttu-id="58442-224">Title_s</span><span class="sxs-lookup"><span data-stu-id="58442-224">Title_s</span></span>|  <span data-ttu-id="58442-225">Breve descrizione</span><span class="sxs-lookup"><span data-stu-id="58442-225">Short description</span></span> |
| <span data-ttu-id="58442-226">Description_s</span><span class="sxs-lookup"><span data-stu-id="58442-226">Description_s</span></span>|  <span data-ttu-id="58442-227">Note</span><span class="sxs-lookup"><span data-stu-id="58442-227">Notes</span></span> |
| <span data-ttu-id="58442-228">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="58442-228">CreatedDate_t</span></span>|  <span data-ttu-id="58442-229">Aperto</span><span class="sxs-lookup"><span data-stu-id="58442-229">Opened</span></span> |
| <span data-ttu-id="58442-230">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="58442-230">ClosedDate_t</span></span>| <span data-ttu-id="58442-231">closed</span><span class="sxs-lookup"><span data-stu-id="58442-231">closed</span></span>|
| <span data-ttu-id="58442-232">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="58442-232">ResolvedDate_t</span></span>|<span data-ttu-id="58442-233">Risolto</span><span class="sxs-lookup"><span data-stu-id="58442-233">Resolved</span></span>|
| <span data-ttu-id="58442-234">Computer</span><span class="sxs-lookup"><span data-stu-id="58442-234">Computer</span></span>  | <span data-ttu-id="58442-235">Elemento di configurazione</span><span class="sxs-lookup"><span data-stu-id="58442-235">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="58442-236">Dati di output per una richiesta di modifica ServiceNow</span><span class="sxs-lookup"><span data-stu-id="58442-236">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="58442-237">Campo OMS</span><span class="sxs-lookup"><span data-stu-id="58442-237">OMS field</span></span> | <span data-ttu-id="58442-238">Campo ITSM</span><span class="sxs-lookup"><span data-stu-id="58442-238">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="58442-239">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="58442-239">ServiceDeskId_s</span></span>| <span data-ttu-id="58442-240">Number</span><span class="sxs-lookup"><span data-stu-id="58442-240">Number</span></span> |
| <span data-ttu-id="58442-241">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="58442-241">CreatedBy_s</span></span> | <span data-ttu-id="58442-242">Richiesto da</span><span class="sxs-lookup"><span data-stu-id="58442-242">Requested by</span></span> |
| <span data-ttu-id="58442-243">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="58442-243">ClosedBy_s</span></span> | <span data-ttu-id="58442-244">Chiuso da</span><span class="sxs-lookup"><span data-stu-id="58442-244">Closed by</span></span> |
| <span data-ttu-id="58442-245">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="58442-245">AssignedTo_s</span></span> | <span data-ttu-id="58442-246">Assegnato a</span><span class="sxs-lookup"><span data-stu-id="58442-246">Assigned to</span></span>  |
| <span data-ttu-id="58442-247">Title_s</span><span class="sxs-lookup"><span data-stu-id="58442-247">Title_s</span></span>|  <span data-ttu-id="58442-248">Breve descrizione</span><span class="sxs-lookup"><span data-stu-id="58442-248">Short description</span></span> |
| <span data-ttu-id="58442-249">Type_s</span><span class="sxs-lookup"><span data-stu-id="58442-249">Type_s</span></span>|  <span data-ttu-id="58442-250">Tipo</span><span class="sxs-lookup"><span data-stu-id="58442-250">Type</span></span> |
| <span data-ttu-id="58442-251">Category_s</span><span class="sxs-lookup"><span data-stu-id="58442-251">Category_s</span></span>|  <span data-ttu-id="58442-252">Categoria</span><span class="sxs-lookup"><span data-stu-id="58442-252">Catgory</span></span> |
| <span data-ttu-id="58442-253">CRState_s</span><span class="sxs-lookup"><span data-stu-id="58442-253">CRState_s</span></span>|  <span data-ttu-id="58442-254">Stato</span><span class="sxs-lookup"><span data-stu-id="58442-254">State</span></span>|
| <span data-ttu-id="58442-255">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="58442-255">Urgency_s</span></span>|  <span data-ttu-id="58442-256">Urgenza</span><span class="sxs-lookup"><span data-stu-id="58442-256">Urgency</span></span> |
| <span data-ttu-id="58442-257">Priority_s</span><span class="sxs-lookup"><span data-stu-id="58442-257">Priority_s</span></span>| <span data-ttu-id="58442-258">Priorità</span><span class="sxs-lookup"><span data-stu-id="58442-258">Priority</span></span>|
| <span data-ttu-id="58442-259">Risk_s</span><span class="sxs-lookup"><span data-stu-id="58442-259">Risk_s</span></span>| <span data-ttu-id="58442-260">Rischio</span><span class="sxs-lookup"><span data-stu-id="58442-260">Risk</span></span>|
| <span data-ttu-id="58442-261">Impact_s</span><span class="sxs-lookup"><span data-stu-id="58442-261">Impact_s</span></span>| <span data-ttu-id="58442-262">Impatto</span><span class="sxs-lookup"><span data-stu-id="58442-262">Impact</span></span>|
| <span data-ttu-id="58442-263">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="58442-263">RequestedDate_t</span></span>  | <span data-ttu-id="58442-264">Data richiesta</span><span class="sxs-lookup"><span data-stu-id="58442-264">Requested by date</span></span> |
| <span data-ttu-id="58442-265">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="58442-265">ClosedDate_t</span></span> | <span data-ttu-id="58442-266">Data di chiusura</span><span class="sxs-lookup"><span data-stu-id="58442-266">Closed date</span></span> |
| <span data-ttu-id="58442-267">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="58442-267">PlannedStartDate_t</span></span>  |     <span data-ttu-id="58442-268">Data di inizio pianificata</span><span class="sxs-lookup"><span data-stu-id="58442-268">Planned start date</span></span> |
| <span data-ttu-id="58442-269">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="58442-269">PlannedEndDate_t</span></span>  |   <span data-ttu-id="58442-270">Data di fine pianificata</span><span class="sxs-lookup"><span data-stu-id="58442-270">Planned end date</span></span> |
| <span data-ttu-id="58442-271">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="58442-271">WorkStartDate_t</span></span>  | <span data-ttu-id="58442-272">Data di inizio effettiva</span><span class="sxs-lookup"><span data-stu-id="58442-272">Actual start date</span></span> |
| <span data-ttu-id="58442-273">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="58442-273">WorkEndDate_t</span></span> | <span data-ttu-id="58442-274">Data di fine effettiva</span><span class="sxs-lookup"><span data-stu-id="58442-274">Actual end date</span></span>|
| <span data-ttu-id="58442-275">Description_s</span><span class="sxs-lookup"><span data-stu-id="58442-275">Description_s</span></span> | <span data-ttu-id="58442-276">Descrizione</span><span class="sxs-lookup"><span data-stu-id="58442-276">Description</span></span> |
| <span data-ttu-id="58442-277">Computer</span><span class="sxs-lookup"><span data-stu-id="58442-277">Computer</span></span>  | <span data-ttu-id="58442-278">Elemento di configurazione</span><span class="sxs-lookup"><span data-stu-id="58442-278">Configuration Item</span></span> |

<span data-ttu-id="58442-279">**Schermata di esempio di Log Analytics per i dati ITSM:**</span><span class="sxs-lookup"><span data-stu-id="58442-279">**Sample Log Analytics screen for ITSM data:**</span></span>

![Schermata di Log Analytics](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a><span data-ttu-id="58442-281">IT Service Management connector: integrazione con altre soluzioni OMS</span><span class="sxs-lookup"><span data-stu-id="58442-281">IT Service Management connector – integration with other OMS solutions</span></span>

<span data-ttu-id="58442-282">IT Service Management connector supporta attualmente l'integrazione con la soluzione Elenco dei servizi.</span><span class="sxs-lookup"><span data-stu-id="58442-282">IT Service Management Connector, currently supports integration with the Service Map solution.</span></span>

<span data-ttu-id="58442-283">Elenco dei servizi individua automaticamente i componenti delle applicazioni nei sistemi Windows e Linux ed esegue la mappatura della comunicazione fra i servizi.</span><span class="sxs-lookup"><span data-stu-id="58442-283">Service Map automatically discovers the application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="58442-284">Consente di visualizzare i server nel modo in cui si pensa a essi, ovvero come sistemi interconnessi che forniscono servizi critici.</span><span class="sxs-lookup"><span data-stu-id="58442-284">It allows you to view your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="58442-285">L'elenco dei servizi mostra le connessioni fra i server, i processi e le porte di tutte le architetture connesse via TCP senza il bisogno di alcuna configurazione a parte l'installazione di un agente.</span><span class="sxs-lookup"><span data-stu-id="58442-285">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="58442-286">Altre informazioni: [Elenco dei servizi](../operations-management-suite/operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="58442-286">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="58442-287">Con questa integrazione, è possibile visualizzare gli elementi del service desk creati nelle soluzioni ITSM come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="58442-287">With this integration, you can view the service desk items created in the ITSM solutions as shown in the following example:</span></span>

![<span data-ttu-id="58442-288">Soluzione integrata</span><span class="sxs-lookup"><span data-stu-id="58442-288">Integrated solution</span></span> ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a><span data-ttu-id="58442-289">Creare elementi di lavoro ITSM per avvisi di OMS</span><span class="sxs-lookup"><span data-stu-id="58442-289">Create ITSM work items for OMS alerts</span></span>

<span data-ttu-id="58442-290">Per gli avvisi OMS, è possibile creare elementi di lavoro associati nelle origini ITSM connesse.</span><span class="sxs-lookup"><span data-stu-id="58442-290">For the OMS alerts, you can create associated work items in the connected ITSM sources.</span></span>  <span data-ttu-id="58442-291">A tale scopo, usare la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="58442-291">To do this, use the following procedure:</span></span>

1. <span data-ttu-id="58442-292">Dalla finestra **Ricerca Log** eseguire una query di ricerca log per visualizzare i dati.</span><span class="sxs-lookup"><span data-stu-id="58442-292">From **Log Search** window, run a log search query to view data.</span></span> <span data-ttu-id="58442-293">I risultati della query sono l'origine degli elementi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="58442-293">Query results are the source for work items.</span></span>
2. <span data-ttu-id="58442-294">In **Ricerca Log** fare clic su **Avviso** per aprire la pagina **Aggiungi regola di avviso**.</span><span class="sxs-lookup"><span data-stu-id="58442-294">In **Log Search**, click **Alert** to open the **Add Alert Rule** page.</span></span>

    ![Schermata di Log Analytics](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. <span data-ttu-id="58442-296">Nella finestra **Aggiungi regola di avviso**, inserire i dettagli necessari per **Nome**, **Gravità**,  **Query di ricerca** e **Criteri avvisi** (misurazione dell'intervallo di tempo/metrica).</span><span class="sxs-lookup"><span data-stu-id="58442-296">On the **Add Alert Rule** window, provide the required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="58442-297">Selezionare **Sì** per **Azioni ITSM**.</span><span class="sxs-lookup"><span data-stu-id="58442-297">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="58442-298">Selezionare la connessione ITSM dall'elenco **Selezionare una connessione**.</span><span class="sxs-lookup"><span data-stu-id="58442-298">Select your ITSM connection from the **Select Connection** list.</span></span>
6. <span data-ttu-id="58442-299">Specificare i dettagli richiesti.</span><span class="sxs-lookup"><span data-stu-id="58442-299">Provide the details as required.</span></span>
7. <span data-ttu-id="58442-300">Per creare un elemento di lavoro separato per ogni voce di log dell'avviso, selezionare la casella di controllo **Crea elementi di lavoro singoli per ogni voce di log**.</span><span class="sxs-lookup"><span data-stu-id="58442-300">To create a separate work item for each log entry of this alert, select the **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="58442-301">oppure</span><span class="sxs-lookup"><span data-stu-id="58442-301">Or</span></span>

    <span data-ttu-id="58442-302">non selezionare questa casella di controllo per creare un solo elemento di lavoro per il numero di voci di log in questo avviso.</span><span class="sxs-lookup"><span data-stu-id="58442-302">leave this checkbox unselected to create only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="58442-303">Fare clic su **Save**.</span><span class="sxs-lookup"><span data-stu-id="58442-303">Click **Save**.</span></span>

<span data-ttu-id="58442-304">In **avvisi** verrà creato l'avviso OMS.</span><span class="sxs-lookup"><span data-stu-id="58442-304">The OMS alert will be created under **Alerts**.</span></span> <span data-ttu-id="58442-305">Gli elementi di lavoro della connessione ITSM corrispondente vengono creati quando viene soddisfatta la condizione dell'avviso specificata.</span><span class="sxs-lookup"><span data-stu-id="58442-305">The corresponding ITSM connection's work items are created when the specified alert's condition is met.</span></span>

## <a name="create-itsm-work-items-from-oms-logs"></a><span data-ttu-id="58442-306">Creare elementi di lavoro ITSM da log di OMS</span><span class="sxs-lookup"><span data-stu-id="58442-306">Create ITSM work items from OMS logs</span></span>

<span data-ttu-id="58442-307">È possibile creare elementi di lavoro nelle origini ITSM connesse tramite Ricerca log di OMS.</span><span class="sxs-lookup"><span data-stu-id="58442-307">You can create work items in the connected ITSM sources by using OMS Log Search.</span></span> <span data-ttu-id="58442-308">A tale scopo, usare la procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="58442-308">To do this, use the following procedure:</span></span>

1. <span data-ttu-id="58442-309">Da **Ricerca Log** cercare i dati richiesti, selezionare i dettagli e fare clic su **Crea elemento di lavoro**.</span><span class="sxs-lookup"><span data-stu-id="58442-309">From **Log Search**,  search the required data, select the detail, and click **Create work item**.</span></span>

    <span data-ttu-id="58442-310">Viene visualizzata la finestra **Crea elemento di lavoro ITSM**:</span><span class="sxs-lookup"><span data-stu-id="58442-310">The **Create ITSM Work item** window appears:</span></span>

    ![Schermata di Log Analytics](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   <span data-ttu-id="58442-312">Aggiungere i dettagli seguenti:</span><span class="sxs-lookup"><span data-stu-id="58442-312">Add the following details:</span></span>

  - <span data-ttu-id="58442-313">**Titolo elemento di lavoro**: il titolo dell'elemento di lavoro.</span><span class="sxs-lookup"><span data-stu-id="58442-313">**Work item Title**: Title for the work item.</span></span>
  - <span data-ttu-id="58442-314">**Descrizione elemento di lavoro**: descrizione per il nuovo elemento di lavoro.</span><span class="sxs-lookup"><span data-stu-id="58442-314">**Work item Description**: Description for the new work item.</span></span>
  - <span data-ttu-id="58442-315">**Computer interessato**: nome del computer in cui sono stati trovati i dati del log.</span><span class="sxs-lookup"><span data-stu-id="58442-315">**Affected Computer**: Name of the computer where this log data was found.</span></span>
  - <span data-ttu-id="58442-316">**Selezionare una connessione**: connessione ITSM in cui si desidera creare questo elemento di lavoro.</span><span class="sxs-lookup"><span data-stu-id="58442-316">**Select Connection**:  ITSM connection in which you want to create this work item.</span></span>
  - <span data-ttu-id="58442-317">**Elemento di lavoro**: tipo di elemento di lavoro.</span><span class="sxs-lookup"><span data-stu-id="58442-317">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="58442-318">Per usare un modello di elemento di lavoro esistente per un evento imprevisto, fare clic su **Sì** nell'opzione **Generate work item based on the template** (Genera elemento di lavoro in base al modello) e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="58442-318">To use an existing work item template for an incident, click **Yes** under **Generate work item based on the template** option and then click **Create**.</span></span>

    <span data-ttu-id="58442-319">Oppure</span><span class="sxs-lookup"><span data-stu-id="58442-319">Or,</span></span>

    <span data-ttu-id="58442-320">Fare clic su **No** se si desidera specificare valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="58442-320">Click **No** if you want to provide your customized values.</span></span>

4. <span data-ttu-id="58442-321">Inserire i valori appropriati nelle caselle di testo **Tipo di contatto**, **Impatto**, **Urgenza**, **Categoria** e **Sottocategoria** e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="58442-321">Provide the appropriate values in the **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>

<span data-ttu-id="58442-322">Verrà creato l'elemento di lavoro in ITSM, che può essere visualizzato anche in OMS.</span><span class="sxs-lookup"><span data-stu-id="58442-322">The work item will be created in the ITSM, which you can also view in OMS.</span></span>

## <a name="troubleshoot-itsm-connections-in-oms"></a><span data-ttu-id="58442-323">Risolvere i problemi delle connessioni ITSM in OMS</span><span class="sxs-lookup"><span data-stu-id="58442-323">Troubleshoot ITSM connections in OMS</span></span>
1.  <span data-ttu-id="58442-324">Se si verifica un errore di connessione nell'interfaccia utente dell'origine connessa e viene visualizzato il messaggio **Errore durante il salvataggio della connessione**, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="58442-324">If connection fails from connected source's UI and you get the **Error in saving connection** message, do the following:</span></span>
 - <span data-ttu-id="58442-325">In caso di connessioni ServiceNow, Cherwell e Provance, assicurarsi di immettere correttamente il nome utente e la password, nonché l'ID e il segreto client per ognuna delle connessioni.</span><span class="sxs-lookup"><span data-stu-id="58442-325">In case of ServiceNow, Cherwell and Provance connections, ensure you correctly entered  the username/password and  client ID/client secret  for each of the connections.</span></span> <span data-ttu-id="58442-326">Se l'errore persiste, controllare se si dispone di privilegi sufficienti all'interno del prodotto ITSM corrispondente per stabilire la connessione.</span><span class="sxs-lookup"><span data-stu-id="58442-326">If the error persists, check if you have sufficient privileges  in the corresponding ITSM product to make the connection.</span></span>
 - <span data-ttu-id="58442-327">In caso di Service Manager, verificare che l'app Web sia stata distribuita correttamente e che la connessione ibrida sia stata creata.</span><span class="sxs-lookup"><span data-stu-id="58442-327">In case of Service Manager, ensure that the Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="58442-328">Per verificare che la connessione sia stata stabilita con il computer Service Manager on-premises, visitare l'URL dell'app Web come descritto nella documentazione per la creazione della [connessione ibrida](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="58442-328">To verify the connection is successfully established with the on-prem Service Manager machine, visit the  Web app URL as detailed in the documentation for making the [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>

2.  <span data-ttu-id="58442-329">Se i dati provenienti da ServiceNow non vengono sincronizzati in OMS, assicurarsi che l'istanza del servizio ServiceNow non sia sospesa.</span><span class="sxs-lookup"><span data-stu-id="58442-329">If data from ServiceNow is not getting synced in OMS, ensure that the ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="58442-330">Questo potrebbe accadere nelle istanze di ServiceNow Dev, quando si trova nello stato inattivo.</span><span class="sxs-lookup"><span data-stu-id="58442-330">This might sometime happen in the ServiceNow Dev instances, when idle.</span></span> <span data-ttu-id="58442-331">In caso contrario, segnalare il problema.</span><span class="sxs-lookup"><span data-stu-id="58442-331">Else, report the issue.</span></span>
3.  <span data-ttu-id="58442-332">Se gli avvisi vengono generati da OMS, ma gli elementi di lavoro non vengono creati nel prodotto ITSM o gli elementi di configurazione non vengono creati/collegati a elementi di lavoro o per qualsiasi informazione generica, eseguire le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="58442-332">If Alerts are getting fired from OMS but work items are not getting created in ITSM product or configuration items are not getting created/linked to work items or for any generic information, do the following:</span></span>
 -  <span data-ttu-id="58442-333">La soluzione IT Service Management Connector nel portale OMS può essere usata per ottenere un riepilogo delle connessioni/elementi di lavoro/computer e così via. Fare clic sul messaggio di errore nel pannello di stato, passare a **Ricerca log** e visualizzare la connessione con l'errore usando i dettagli nel messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="58442-333">IT Service Management Connector solution in OMS portal could be used to get a summary of connections/work items/computers etc. Click the error message in the status blade, navigate to **Log Search** and view the connection that has the error by using the details in the error message.</span></span>
 - <span data-ttu-id="58442-334">È possibile visualizzare direttamente gli errori/le informazioni correlate nella pagina **Ricerca log** usando *Type = ServiceDeskLog_CL*.</span><span class="sxs-lookup"><span data-stu-id="58442-334">you can directly view the errors/related information in the **Log Search** page using *Type=ServiceDeskLog_CL*.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="58442-335">Risolvere i problemi di distribuzione dell’app Web Service Manager</span><span class="sxs-lookup"><span data-stu-id="58442-335">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="58442-336">In caso di problemi con la distribuzione dell’app Web, assicurarsi di disporre di autorizzazioni sufficienti nella sottoscrizione indicata per creare/distribuire risorse.</span><span class="sxs-lookup"><span data-stu-id="58442-336">In case of any trouble with web app deployment, ensure you have sufficient permissions in the subscription mentioned to create/deploy resources.</span></span>
2.  <span data-ttu-id="58442-337">Se viene visualizzato il messaggio di errore **Riferimento a oggetto non impostato sull’istanza di un oggetto** durante l’esecuzione dello [script](log-analytics-itsmc-service-manager-script.md), assicurarsi di aver immesso valori validi nella sezione **Configurazione utente**.</span><span class="sxs-lookup"><span data-stu-id="58442-337">If **Object reference not set to instance of an object** error message appears while running the [script](log-analytics-itsmc-service-manager-script.md) ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="58442-338">Se non è possibile creare lo spazio dei nomi di inoltro del bus di servizio, assicurarsi che il provider di risorse richiesto sia registrato nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="58442-338">If you fail to create service bus relay namespace, ensure that the required resource provider is registered in the subscription.</span></span> <span data-ttu-id="58442-339">Qualora non fosse registrato, crearlo manualmente dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="58442-339">If not registered, manually create it from the Azure portal.</span></span> <span data-ttu-id="58442-340">È inoltre possibile crearlo durante [la creazione della connessione ibrida](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="58442-340">You can also create it while [creating the hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from the Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="58442-341">Contatti</span><span class="sxs-lookup"><span data-stu-id="58442-341">Contact us</span></span>

<span data-ttu-id="58442-342">Per eventuali domande o commenti e suggerimenti su IT Service Management Connector, è possibile contattare [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="58442-342">For any queries or feedback on the IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="58442-343">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="58442-343">Next steps</span></span>
<span data-ttu-id="58442-344">[Aggiungere prodotti o servizi ITSM a IT Service Management Connector](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="58442-344">[Add ITSM products/services to IT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
