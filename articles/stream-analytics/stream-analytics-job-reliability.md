---
title: Evitare interruzioni del servizio con i processi di Analisi di flusso di Azure | Microsoft Docs
description: Indicazioni per ottenere la resilienza nell'aggiornamento dei processi di Analisi di flusso.
services: stream-analytics
documentationCenter: 
authors: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 8dc19e1b37082c87d2990ad910d1af786f8b9280
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a><span data-ttu-id="e5052-103">Garantire l'affidabilità dei processi di Analisi di flusso durante gli aggiornamenti del servizio</span><span class="sxs-lookup"><span data-stu-id="e5052-103">Guarantee Stream Analytics job reliability during service updates</span></span>

<span data-ttu-id="e5052-104">Perché un servizio sia completamente gestito, deve includere anche la possibilità di introdurre rapidamente nuove funzionalità e miglioramenti.</span><span class="sxs-lookup"><span data-stu-id="e5052-104">Part of being a fully managed service is the capability to introduce new service functionality and improvements at a rapid pace.</span></span> <span data-ttu-id="e5052-105">La distribuzione di aggiornamenti del servizio in Analisi di flusso può quindi essere eseguita con frequenza settimanale o superiore.</span><span class="sxs-lookup"><span data-stu-id="e5052-105">As a result, Stream Analytics can have a service update deploy on a weekly (or more frequent) basis.</span></span> <span data-ttu-id="e5052-106">Indipendentemente dalla quantità di test effettuati, esiste comunque il rischio che un processo esistente in esecuzione subisca un'interruzione a causa dell'introduzione di un bug.</span><span class="sxs-lookup"><span data-stu-id="e5052-106">No matter how much testing is done there is still a risk that an existing, running job may break due to the introduction of a bug.</span></span> <span data-ttu-id="e5052-107">I clienti che eseguono processi di elaborazione in streaming critici devono evitare tali rischi.</span><span class="sxs-lookup"><span data-stu-id="e5052-107">For customers who run critical streaming processing jobs these risks need to be avoided.</span></span> <span data-ttu-id="e5052-108">Come meccanismo per ridurli, possono usare il modello delle **[aree abbinate](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** di Azure.</span><span class="sxs-lookup"><span data-stu-id="e5052-108">A mechanism customers can use to reduce this risk is Azure’s **[paired region](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** model.</span></span> 

## <a name="how-do-azure-paired-regions-address-this-concern"></a><span data-ttu-id="e5052-109">Vantaggi delle aree abbinate di Azure per la risoluzione del problema</span><span class="sxs-lookup"><span data-stu-id="e5052-109">How do Azure paired regions address this concern?</span></span>

<span data-ttu-id="e5052-110">Analisi di flusso garantisce che i processi nelle aree abbinate vengano aggiornati in batch separati.</span><span class="sxs-lookup"><span data-stu-id="e5052-110">Stream Analytics guarantees jobs in paired regions are updated in separate batches.</span></span> <span data-ttu-id="e5052-111">Di conseguenza, tra gli aggiornamenti intercorre un intervallo di tempo sufficiente a identificare e risolvere i bug che potrebbero causare interruzioni.</span><span class="sxs-lookup"><span data-stu-id="e5052-111">As a result there is a sufficient time gap between the updates to identify potential breaking bugs and remediate them.</span></span>

<span data-ttu-id="e5052-112">_Con l'eccezione dell'India centrale_ (nella cui area abbinata, India meridionale, non è presente Analisi di flusso), la distribuzione di un aggiornamento in Analisi di flusso non viene eseguita contemporaneamente in un set di aree abbinate.</span><span class="sxs-lookup"><span data-stu-id="e5052-112">_With the exception of Central India_ (whose paired region, South India, does not have Stream Analytics presence), the deployment of an update to Stream Analytics would not occur at the same time in a set of paired regions.</span></span> <span data-ttu-id="e5052-113">Le distribuzioni in più aree **dello stesso gruppo** possono essere eseguite **contemporaneamente**.</span><span class="sxs-lookup"><span data-stu-id="e5052-113">Deployments in multiple regions **in the same group** may occur **at the same time**.</span></span>

<span data-ttu-id="e5052-114">L'articolo su **[disponibilità e aree abbinate](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** contiene le informazioni più aggiornate su quali aree sono abbinate.</span><span class="sxs-lookup"><span data-stu-id="e5052-114">The article on **[availability and paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** has the most up-to-date information on which regions are paired.</span></span>

<span data-ttu-id="e5052-115">Per i clienti è consigliabile distribuire processi identici in entrambe le aree abbinate.</span><span class="sxs-lookup"><span data-stu-id="e5052-115">Customers are advised to deploy identical jobs to both paired regions.</span></span> <span data-ttu-id="e5052-116">In aggiunta alle funzionalità di monitoraggio interno di Analisi di flusso, è anche consigliabile monitorare i processi come se fossero **entrambi** processi di produzione.</span><span class="sxs-lookup"><span data-stu-id="e5052-116">In addition to Stream Analytics internal monitoring capabilities, customers are also advised to monitor the jobs as if **both** are production jobs.</span></span> <span data-ttu-id="e5052-117">Se la causa identificata di un'interruzione è l'aggiornamento del servizio Analisi di flusso, eseguire l'escalation appropriata e il failover degli utenti downstream all'output del processo integro.</span><span class="sxs-lookup"><span data-stu-id="e5052-117">If a break is identified to be a result of the Stream Analytics service update, escalate appropriately and fail over any downstream consumers to the healthy job output.</span></span> <span data-ttu-id="e5052-118">L'escalation al supporto tecnico impedirà che l'area abbinata sia interessata dalla nuova distribuzione, in modo da mantenere l'integrità dei processi abbinati.</span><span class="sxs-lookup"><span data-stu-id="e5052-118">Escalation to support will prevent the paired region from being affected by the new deployment and maintain the integrity of the paired jobs.</span></span>
