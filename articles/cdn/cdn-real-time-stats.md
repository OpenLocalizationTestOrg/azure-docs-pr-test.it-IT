---
title: fase aaaReal statistiche nella rete CDN di Azure | Documenti Microsoft
description: Statistiche in tempo reale fornisce in tempo reale dati sulle prestazioni di hello della rete CDN di Azure per il recapito di contenuto tooyour client.
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
ms.openlocfilehash: 68900a5092b767e45c1fdf9cef2cd03f55f38a6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a><span data-ttu-id="89073-103">Statistiche in tempo reale nella rete CDN di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="89073-103">Real-time stats in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="89073-104">Overview</span><span class="sxs-lookup"><span data-stu-id="89073-104">Overview</span></span>
<span data-ttu-id="89073-105">Questo documento illustra le statistiche in tempo reale nella rete CDN di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="89073-105">This document explains real-time stats in Microsoft Azure CDN.</span></span>  <span data-ttu-id="89073-106">Questa funzionalità fornisce i dati in tempo reale, ad esempio larghezza di banda, gli stati di cache e connessioni simultanee tooyour CDN profilo per il recapito di contenuto tooyour client.</span><span class="sxs-lookup"><span data-stu-id="89073-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections tooyour CDN profile when delivering content tooyour clients.</span></span> <span data-ttu-id="89073-107">In questo modo, il monitoraggio continuo dell'integrità di hello del servizio in qualsiasi momento, inclusi gli eventi di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="89073-107">This enables continuous monitoring of hello health of your service at any time, including go-live events.</span></span>

<span data-ttu-id="89073-108">sono disponibile i seguenti grafici Hello:</span><span class="sxs-lookup"><span data-stu-id="89073-108">hello following graphs are available:</span></span>

* [<span data-ttu-id="89073-109">Larghezza di banda</span><span class="sxs-lookup"><span data-stu-id="89073-109">Bandwidth</span></span>](#bandwidth)
* [<span data-ttu-id="89073-110">Codici di stato</span><span class="sxs-lookup"><span data-stu-id="89073-110">Status Codes</span></span>](#status-codes)
* [<span data-ttu-id="89073-111">Stati della cache</span><span class="sxs-lookup"><span data-stu-id="89073-111">Cache Statuses</span></span>](#cache-statuses)
* [<span data-ttu-id="89073-112">Connessioni</span><span class="sxs-lookup"><span data-stu-id="89073-112">Connections</span></span>](#connections)

## <a name="accessing-real-time-stats"></a><span data-ttu-id="89073-113">Accesso alle statistiche in tempo reale</span><span class="sxs-lookup"><span data-stu-id="89073-113">Accessing real-time stats</span></span>
1. <span data-ttu-id="89073-114">In hello [portale Azure](https://portal.azure.com), selezionare il profilo CDN tooyour.</span><span class="sxs-lookup"><span data-stu-id="89073-114">In hello [Azure Portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>
   
    ![Pannello del profilo di rete CDN](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. <span data-ttu-id="89073-116">Dal Pannello di profilo CDN hello, fare clic su hello **Gestisci** pulsante.</span><span class="sxs-lookup"><span data-stu-id="89073-116">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Pulsante Gestisci pannello del profilo di rete CDN](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    <span data-ttu-id="89073-118">viene visualizzato il portale di gestione della rete CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="89073-118">hello CDN management portal opens.</span></span>
3. <span data-ttu-id="89073-119">Passare il mouse su hello **Analitica** scheda, quindi passare il mouse su hello **statistiche in tempo reale** riquadro a comparsa.</span><span class="sxs-lookup"><span data-stu-id="89073-119">Hover over hello **Analytics** tab, then hover over hello **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="89073-120">Fare clic su **Oggetto di grandi dimensioni HTTP**.</span><span class="sxs-lookup"><span data-stu-id="89073-120">Click on **HTTP Large Object**.</span></span>
   
    ![Portale di gestione della rete CDN](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    <span data-ttu-id="89073-122">vengono visualizzati i grafici di Hello statistiche in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="89073-122">hello real-time stats graphs are displayed.</span></span>

<span data-ttu-id="89073-123">Ognuno dei grafici hello Visualizza statistiche in tempo reale per l'intervallo di tempo selezionato hello, avvio durante il caricamento pagina hello.</span><span class="sxs-lookup"><span data-stu-id="89073-123">Each of hello graphs displays real-time statistics for hello selected time span, starting when hello page loads.</span></span>  <span data-ttu-id="89073-124">grafici di Hello aggiornati automaticamente ogni pochi secondi.</span><span class="sxs-lookup"><span data-stu-id="89073-124">hello graphs update automatically every few seconds.</span></span>  <span data-ttu-id="89073-125">Hello **aggiornare grafico** pulsante, se presente, verrà cancellato grafico hello, dopo il quale verranno visualizzate solo dati hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="89073-125">hello **Refresh Graph** button, if present, will clear hello graph, after which it will only display hello selected data.</span></span>

## <a name="bandwidth"></a><span data-ttu-id="89073-126">Larghezza di banda</span><span class="sxs-lookup"><span data-stu-id="89073-126">Bandwidth</span></span>
![Grafico Larghezza di banda](./media/cdn-real-time-stats/cdn-bandwidth.png)

<span data-ttu-id="89073-128">Hello **della larghezza di banda** grafico consente di visualizzare la quantità hello di larghezza di banda utilizzata per la piattaforma corrente hello tramite l'intervallo di tempo selezionato hello.</span><span class="sxs-lookup"><span data-stu-id="89073-128">hello **Bandwidth** graph displays hello amount of bandwidth used for hello current platform over hello selected time span.</span></span> <span data-ttu-id="89073-129">Hello ombreggiata parte grafico hello indica l'utilizzo della larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="89073-129">hello shaded portion of hello graph indicates bandwidth usage.</span></span> <span data-ttu-id="89073-130">quantità esatta di Hello di larghezza di banda attualmente in uso viene visualizzato sotto un grafico a linee hello.</span><span class="sxs-lookup"><span data-stu-id="89073-130">hello exact amount of bandwidth currently being used is displayed directly below hello line graph.</span></span>

## <a name="status-codes"></a><span data-ttu-id="89073-131">Codici di stato</span><span class="sxs-lookup"><span data-stu-id="89073-131">Status Codes</span></span>
![Grafico Codici di stato](./media/cdn-real-time-stats/cdn-status-codes.png)

<span data-ttu-id="89073-133">Hello **codici di stato** grafico indica la frequenza con cui si verificano alcuni codici di risposta HTTP su intervallo di tempo hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="89073-133">hello **Status Codes** graph indicates how often certain HTTP response codes are occurring over hello selected time span.</span></span>

> [!TIP]
> <span data-ttu-id="89073-134">Per una descrizione di ogni opzione relativa ai codici di stato HTTP, vedere [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx)(Codici di stato HTTP della rete CDN di Azure).</span><span class="sxs-lookup"><span data-stu-id="89073-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span></span>
> 
> 

<span data-ttu-id="89073-135">Direttamente sopra il grafico di hello viene visualizzato un elenco di codici di stato HTTP.</span><span class="sxs-lookup"><span data-stu-id="89073-135">A list of HTTP status codes is displayed directly above hello graph.</span></span> <span data-ttu-id="89073-136">Questo elenco indica ogni codice di stato che può essere incluso nel grafico a linee hello e numero corrente di hello di occorrenze al secondo per il codice di stato.</span><span class="sxs-lookup"><span data-stu-id="89073-136">This list indicates each status code that can be included in hello line graph and hello current number of occurrences per second for that status code.</span></span> <span data-ttu-id="89073-137">Per impostazione predefinita, viene visualizzata una riga per ognuno di questi codici di stato nel grafico hello.</span><span class="sxs-lookup"><span data-stu-id="89073-137">By default, a line is displayed for each of these status codes in hello graph.</span></span> <span data-ttu-id="89073-138">Tuttavia, è possibile scegliere tooonly i codici di stato hello monitor che hanno un significato speciale per la configurazione della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="89073-138">However, you can choose tooonly monitor hello status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="89073-139">toodo, controllare i codici di stato hello desiderato e deselezionare tutte le altre opzioni, quindi fare clic su **aggiornare grafico**.</span><span class="sxs-lookup"><span data-stu-id="89073-139">toodo this, check hello desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="89073-140">È possibile nascondere temporaneamente i dati registrati per un codice di stato specifico.</span><span class="sxs-lookup"><span data-stu-id="89073-140">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="89073-141">Legenda hello direttamente sotto il grafico di hello, selezionare il codice di stato hello desiderato toohide.</span><span class="sxs-lookup"><span data-stu-id="89073-141">From hello legend directly below hello graph, click hello status code you want toohide.</span></span> <span data-ttu-id="89073-142">codice di stato Hello verrà nascoste dal grafico hello immediatamente.</span><span class="sxs-lookup"><span data-stu-id="89073-142">hello status code will be immediately hidden from hello graph.</span></span> <span data-ttu-id="89073-143">Fare nuovamente clic su quel codice di stato causerà toobe tale opzione visualizzato di nuovo.</span><span class="sxs-lookup"><span data-stu-id="89073-143">Clicking that status code again will cause that option toobe displayed again.</span></span>

## <a name="cache-statuses"></a><span data-ttu-id="89073-144">Stati della cache</span><span class="sxs-lookup"><span data-stu-id="89073-144">Cache Statuses</span></span>
![Grafico Stati della cache](./media/cdn-real-time-stats/cdn-cache-status.png)

<span data-ttu-id="89073-146">Hello **Cache stati** grafico indica la frequenza con cui si verificano determinati tipi di stato della cache su intervallo di tempo selezionato hello.</span><span class="sxs-lookup"><span data-stu-id="89073-146">hello **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over hello selected time span.</span></span> 

> [!TIP]
> <span data-ttu-id="89073-147">Per una descrizione di ogni opzione relativa agli stati della cache, vedere [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx)(Codici di stato della cache della rete CDN di Azure).</span><span class="sxs-lookup"><span data-stu-id="89073-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span></span>
> 
> 

<span data-ttu-id="89073-148">Direttamente sopra il grafico di hello viene visualizzato un elenco dei codici di stato della cache.</span><span class="sxs-lookup"><span data-stu-id="89073-148">A list of cache status codes is displayed directly above hello graph.</span></span> <span data-ttu-id="89073-149">Questo elenco indica ogni codice di stato che può essere incluso nel grafico a linee hello e numero corrente di hello di occorrenze al secondo per il codice di stato.</span><span class="sxs-lookup"><span data-stu-id="89073-149">This list indicates each status code that can be included in hello line graph and hello current number of occurrences per second for that status code.</span></span> <span data-ttu-id="89073-150">Per impostazione predefinita, viene visualizzata una riga per ognuno di questi codici di stato nel grafico hello.</span><span class="sxs-lookup"><span data-stu-id="89073-150">By default, a line is displayed for each of these status codes in hello graph.</span></span> <span data-ttu-id="89073-151">Tuttavia, è possibile scegliere tooonly i codici di stato hello monitor che hanno un significato speciale per la configurazione della rete CDN.</span><span class="sxs-lookup"><span data-stu-id="89073-151">However, you can choose tooonly monitor hello status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="89073-152">toodo, controllare i codici di stato hello desiderato e deselezionare tutte le altre opzioni, quindi fare clic su **aggiornare grafico**.</span><span class="sxs-lookup"><span data-stu-id="89073-152">toodo this, check hello desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="89073-153">È possibile nascondere temporaneamente i dati registrati per un codice di stato specifico.</span><span class="sxs-lookup"><span data-stu-id="89073-153">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="89073-154">Legenda hello direttamente sotto il grafico di hello, selezionare il codice di stato hello desiderato toohide.</span><span class="sxs-lookup"><span data-stu-id="89073-154">From hello legend directly below hello graph, click hello status code you want toohide.</span></span> <span data-ttu-id="89073-155">codice di stato Hello verrà nascoste dal grafico hello immediatamente.</span><span class="sxs-lookup"><span data-stu-id="89073-155">hello status code will be immediately hidden from hello graph.</span></span> <span data-ttu-id="89073-156">Fare nuovamente clic su quel codice di stato causerà toobe tale opzione visualizzato di nuovo.</span><span class="sxs-lookup"><span data-stu-id="89073-156">Clicking that status code again will cause that option toobe displayed again.</span></span>

## <a name="connections"></a><span data-ttu-id="89073-157">Connessioni</span><span class="sxs-lookup"><span data-stu-id="89073-157">Connections</span></span>
![Grafico Connessioni](./media/cdn-real-time-stats/cdn-connections.png)

<span data-ttu-id="89073-159">Questo grafico indica il numero di connessioni sono state stabilite tooyour edge server.</span><span class="sxs-lookup"><span data-stu-id="89073-159">This graph indicates how many connections have been established tooyour edge servers.</span></span> <span data-ttu-id="89073-160">Ogni richiesta per un asset che passa attraverso la rete CDN costituisce una connessione.</span><span class="sxs-lookup"><span data-stu-id="89073-160">Each request for an asset that passes through our CDN results in a connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89073-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="89073-161">Next Steps</span></span>
* <span data-ttu-id="89073-162">Per impostare la ricezione di notifiche, vedere [Avvisi in tempo reale nella rete CDN di Microsoft Azure](cdn-real-time-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="89073-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span></span>
* <span data-ttu-id="89073-163">Per un'analisi più approfondita, vedere [Report HTTP avanzati nella rete CDN di Microsoft Azure](cdn-advanced-http-reports.md)</span><span class="sxs-lookup"><span data-stu-id="89073-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="89073-164">Vedere [Analizzare i modelli di utilizzo della rete CDN di Azure](cdn-analyze-usage-patterns.md)</span><span class="sxs-lookup"><span data-stu-id="89073-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

