---
title: Statistiche in tempo reale nella rete CDN di Azure | Documentazione Microsoft
description: Le statistiche in tempo reale forniscono i dati in tempo reale sulle prestazioni della rete CDN durante la distribuzione di contenuto ai client.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c7989340-1172-4315-acbb-186ba34dd52a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e9b9522de6b2c54dc794b00100ffe358296ecfdd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a><span data-ttu-id="f73f6-103">Statistiche in tempo reale nella rete CDN di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f73f6-103">Real-time stats in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="f73f6-104">Overview</span><span class="sxs-lookup"><span data-stu-id="f73f6-104">Overview</span></span>
<span data-ttu-id="f73f6-105">Questo documento illustra le statistiche in tempo reale nella rete CDN di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f73f6-105">This document explains real-time stats in Microsoft Azure CDN.</span></span>  <span data-ttu-id="f73f6-106">Questa funzionalità fornisce dati in tempo reale, ad esempio la larghezza di banda, gli stati della cache e le connessioni simultanee al profilo della rete CDN per il recapito di contenuto ai client.</span><span class="sxs-lookup"><span data-stu-id="f73f6-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections to your CDN profile when delivering content to your clients.</span></span> <span data-ttu-id="f73f6-107">In questo modo viene abilitato il monitoraggio continuo dell'integrità del servizio in qualsiasi momento, inclusi gli eventi di go-live.</span><span class="sxs-lookup"><span data-stu-id="f73f6-107">This enables continuous monitoring of the health of your service at any time, including go-live events.</span></span>

<span data-ttu-id="f73f6-108">Sono disponibili i grafici seguenti:</span><span class="sxs-lookup"><span data-stu-id="f73f6-108">The following graphs are available:</span></span>

* [<span data-ttu-id="f73f6-109">Larghezza di banda</span><span class="sxs-lookup"><span data-stu-id="f73f6-109">Bandwidth</span></span>](#bandwidth)
* [<span data-ttu-id="f73f6-110">Codici di stato</span><span class="sxs-lookup"><span data-stu-id="f73f6-110">Status Codes</span></span>](#status-codes)
* [<span data-ttu-id="f73f6-111">Stati della cache</span><span class="sxs-lookup"><span data-stu-id="f73f6-111">Cache Statuses</span></span>](#cache-statuses)
* [<span data-ttu-id="f73f6-112">Connessioni</span><span class="sxs-lookup"><span data-stu-id="f73f6-112">Connections</span></span>](#connections)

## <a name="accessing-real-time-stats"></a><span data-ttu-id="f73f6-113">Accesso alle statistiche in tempo reale</span><span class="sxs-lookup"><span data-stu-id="f73f6-113">Accessing real-time stats</span></span>
1. <span data-ttu-id="f73f6-114">Nel [portale di Azure](https://portal.azure.com)passare al profilo della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="f73f6-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span></span>
   
    ![Pannello del profilo di rete CDN](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. <span data-ttu-id="f73f6-116">Dal pannello del profilo della rete CDN fare clic sul pulsante **Gestisci** .</span><span class="sxs-lookup"><span data-stu-id="f73f6-116">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    <span data-ttu-id="f73f6-118">Si aprirà il portale di gestione della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="f73f6-118">The CDN management portal opens.</span></span>
3. <span data-ttu-id="f73f6-119">Passare il puntatore sulla scheda **Analisi**, quindi sul riquadro a comparsa **Statistiche in tempo reale**.</span><span class="sxs-lookup"><span data-stu-id="f73f6-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="f73f6-120">Fare clic su **Oggetto di grandi dimensioni HTTP**.</span><span class="sxs-lookup"><span data-stu-id="f73f6-120">Click on **HTTP Large Object**.</span></span>
   
    ![Portale di gestione della rete CDN](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    <span data-ttu-id="f73f6-122">Vengono visualizzati i grafici delle statistiche in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="f73f6-122">The real-time stats graphs are displayed.</span></span>

<span data-ttu-id="f73f6-123">Ogni grafico visualizza le statistiche in tempo reale per l'intervallo di tempo selezionato, a partire dal momento del caricamento della pagina.</span><span class="sxs-lookup"><span data-stu-id="f73f6-123">Each of the graphs displays real-time statistics for the selected time span, starting when the page loads.</span></span>  <span data-ttu-id="f73f6-124">I grafici vengono aggiornati automaticamente a intervalli di pochi secondi.</span><span class="sxs-lookup"><span data-stu-id="f73f6-124">The graphs update automatically every few seconds.</span></span>  <span data-ttu-id="f73f6-125">Il pulsante **Aggiorna grafico** , se presente, consente di cancellare il grafico, dopodiché saranno visualizzati solo i dati selezionati.</span><span class="sxs-lookup"><span data-stu-id="f73f6-125">The **Refresh Graph** button, if present, will clear the graph, after which it will only display the selected data.</span></span>

## <a name="bandwidth"></a><span data-ttu-id="f73f6-126">Larghezza di banda</span><span class="sxs-lookup"><span data-stu-id="f73f6-126">Bandwidth</span></span>
![Grafico Larghezza di banda](./media/cdn-real-time-stats/cdn-bandwidth.png)

<span data-ttu-id="f73f6-128">Il grafico **Larghezza di banda** visualizza la quantità di larghezza di banda usata per la piattaforma corrente nel periodo di tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="f73f6-128">The **Bandwidth** graph displays the amount of bandwidth used for the current platform over the selected time span.</span></span> <span data-ttu-id="f73f6-129">La parte ombreggiata del grafico indica l'utilizzo della larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="f73f6-129">The shaded portion of the graph indicates bandwidth usage.</span></span> <span data-ttu-id="f73f6-130">La quantità esatta di larghezza di banda attualmente in uso viene visualizzata direttamente sotto il grafico a linee.</span><span class="sxs-lookup"><span data-stu-id="f73f6-130">The exact amount of bandwidth currently being used is displayed directly below the line graph.</span></span>

## <a name="status-codes"></a><span data-ttu-id="f73f6-131">Codici di stato</span><span class="sxs-lookup"><span data-stu-id="f73f6-131">Status Codes</span></span>
![Grafico Codici di stato](./media/cdn-real-time-stats/cdn-status-codes.png)

<span data-ttu-id="f73f6-133">Il grafico **Codici di stato** indica la frequenza con cui si verificano alcuni codici di risposta HTTP durante l'intervallo di tempo selezionato.</span><span class="sxs-lookup"><span data-stu-id="f73f6-133">The **Status Codes** graph indicates how often certain HTTP response codes are occurring over the selected time span.</span></span>

> [!TIP]
> <span data-ttu-id="f73f6-134">Per una descrizione di ogni opzione relativa ai codici di stato HTTP, vedere [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)(Codici di stato HTTP della rete CDN di Azure).</span><span class="sxs-lookup"><span data-stu-id="f73f6-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span></span>
> 
> 

<span data-ttu-id="f73f6-135">Direttamente sopra al grafico viene visualizzato un elenco dei codici di stato HTTP.</span><span class="sxs-lookup"><span data-stu-id="f73f6-135">A list of HTTP status codes is displayed directly above the graph.</span></span> <span data-ttu-id="f73f6-136">Questo elenco indica ogni codice di stato che può essere incluso nel grafico a linee e il numero di occorrenze correnti al secondo per ogni codice di stato.</span><span class="sxs-lookup"><span data-stu-id="f73f6-136">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="f73f6-137">Per impostazione predefinita, viene visualizzata una riga per ognuno di questi codici di stato nel grafico.</span><span class="sxs-lookup"><span data-stu-id="f73f6-137">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="f73f6-138">Tuttavia, è possibile scegliere di monitorare solo i codici di stato che hanno un significato speciale per la configurazione della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="f73f6-138">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="f73f6-139">A tale scopo, selezionare i codici di stato desiderati e deselezionare tutte le altre opzioni, quindi fare clic su **Aggiorna grafico**.</span><span class="sxs-lookup"><span data-stu-id="f73f6-139">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="f73f6-140">È possibile nascondere temporaneamente i dati registrati per un codice di stato specifico.</span><span class="sxs-lookup"><span data-stu-id="f73f6-140">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="f73f6-141">Nella legenda direttamente sotto il grafico selezionare il codice di stato che si vuole nascondere.</span><span class="sxs-lookup"><span data-stu-id="f73f6-141">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="f73f6-142">Il codice di stato verrà nascosto immediatamente nel grafico.</span><span class="sxs-lookup"><span data-stu-id="f73f6-142">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="f73f6-143">Se si seleziona di nuovo il codice di stato, l'opzione verrà visualizzata nuovamente.</span><span class="sxs-lookup"><span data-stu-id="f73f6-143">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="cache-statuses"></a><span data-ttu-id="f73f6-144">Stati della cache</span><span class="sxs-lookup"><span data-stu-id="f73f6-144">Cache Statuses</span></span>
![Grafico Stati della cache](./media/cdn-real-time-stats/cdn-cache-status.png)

<span data-ttu-id="f73f6-146">Il grafico **Stati della cache** indica la frequenza con cui si verificano alcuni tipi di stati della cache durante l'intervallo di tempo selezionato.</span><span class="sxs-lookup"><span data-stu-id="f73f6-146">The **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over the selected time span.</span></span> 

> [!TIP]
> <span data-ttu-id="f73f6-147">Per una descrizione di ogni opzione relativa agli stati della cache, vedere [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx)(Codici di stato della cache della rete CDN di Azure).</span><span class="sxs-lookup"><span data-stu-id="f73f6-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span></span>
> 
> 

<span data-ttu-id="f73f6-148">Direttamente sopra al grafico viene visualizzato un elenco di codici di stato della cache.</span><span class="sxs-lookup"><span data-stu-id="f73f6-148">A list of cache status codes is displayed directly above the graph.</span></span> <span data-ttu-id="f73f6-149">Questo elenco indica ogni codice di stato che può essere incluso nel grafico a linee e il numero di occorrenze correnti al secondo per ogni codice di stato.</span><span class="sxs-lookup"><span data-stu-id="f73f6-149">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="f73f6-150">Per impostazione predefinita, viene visualizzata una riga per ognuno di questi codici di stato nel grafico.</span><span class="sxs-lookup"><span data-stu-id="f73f6-150">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="f73f6-151">Tuttavia, è possibile scegliere di monitorare solo i codici di stato che hanno un significato speciale per la configurazione della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="f73f6-151">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="f73f6-152">A tale scopo, selezionare i codici di stato desiderati e deselezionare tutte le altre opzioni, quindi fare clic su **Aggiorna grafico**.</span><span class="sxs-lookup"><span data-stu-id="f73f6-152">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="f73f6-153">È possibile nascondere temporaneamente i dati registrati per un codice di stato specifico.</span><span class="sxs-lookup"><span data-stu-id="f73f6-153">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="f73f6-154">Nella legenda direttamente sotto il grafico selezionare il codice di stato che si vuole nascondere.</span><span class="sxs-lookup"><span data-stu-id="f73f6-154">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="f73f6-155">Il codice di stato verrà nascosto immediatamente nel grafico.</span><span class="sxs-lookup"><span data-stu-id="f73f6-155">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="f73f6-156">Se si seleziona di nuovo il codice di stato, l'opzione verrà visualizzata nuovamente.</span><span class="sxs-lookup"><span data-stu-id="f73f6-156">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="connections"></a><span data-ttu-id="f73f6-157">Connessioni</span><span class="sxs-lookup"><span data-stu-id="f73f6-157">Connections</span></span>
![Grafico Connessioni](./media/cdn-real-time-stats/cdn-connections.png)

<span data-ttu-id="f73f6-159">Questo grafico indica il numero di connessioni stabilite con i server perimetrali.</span><span class="sxs-lookup"><span data-stu-id="f73f6-159">This graph indicates how many connections have been established to your edge servers.</span></span> <span data-ttu-id="f73f6-160">Ogni richiesta per un asset che passa attraverso la rete CDN costituisce una connessione.</span><span class="sxs-lookup"><span data-stu-id="f73f6-160">Each request for an asset that passes through our CDN results in a connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f73f6-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f73f6-161">Next Steps</span></span>
* <span data-ttu-id="f73f6-162">Per impostare la ricezione di notifiche, vedere [Avvisi in tempo reale nella rete CDN di Microsoft Azure](cdn-real-time-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="f73f6-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span></span>
* <span data-ttu-id="f73f6-163">Per un'analisi più approfondita, vedere [Report HTTP avanzati nella rete CDN di Microsoft Azure](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="f73f6-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="f73f6-164">Vedere [Analizzare i modelli di utilizzo della rete CDN di Azure](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="f73f6-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

