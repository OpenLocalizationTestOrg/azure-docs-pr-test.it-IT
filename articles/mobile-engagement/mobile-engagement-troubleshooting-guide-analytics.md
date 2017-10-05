---
title: Guida alla risoluzione dei problemi di Azure Mobile Engagement - Analytics
description: Risoluzione dei problemi relativi ad analisi, monitoraggio, segmentazione e dashboard in Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04a7020a-ad74-4491-be69-0bd574890029
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: e30c9ac0a8421ffcf4fc3e2548cfd7ac49701900
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a><span data-ttu-id="cc492-103">Guida alla risoluzione dei problemi relativi ad analisi, monitoraggio, segmentazione e dashboard</span><span class="sxs-lookup"><span data-stu-id="cc492-103">Troubleshooting guide for Analytics, Monitoring, Segmentation, and Dashboard issues</span></span>
<span data-ttu-id="cc492-104">Di seguito sono indicati possibili problemi che relativi al modo in cui Azure Mobile Engagement raccoglie informazioni su applicazioni, dispositivi e utenti.</span><span class="sxs-lookup"><span data-stu-id="cc492-104">The following are possible issues you may encounter with how Azure Mobile Engagement gathers information about your applications, devices, and users.</span></span>

## <a name="missingdelayed-information"></a><span data-ttu-id="cc492-105">Informazioni mancanti o in ritardo</span><span class="sxs-lookup"><span data-stu-id="cc492-105">Missing/Delayed information</span></span>
### <a name="issue"></a><span data-ttu-id="cc492-106">Problema</span><span class="sxs-lookup"><span data-stu-id="cc492-106">Issue</span></span>
* <span data-ttu-id="cc492-107">Informazioni visualizzate in ritardo nell'analisi, nella segmentazione o nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="cc492-107">Information is delayed in appearing in Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="cc492-108">Informazioni mancanti nel monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="cc492-108">Information is missing from Monitoring.</span></span>
* <span data-ttu-id="cc492-109">Informazioni mancanti nell'analisi, nella segmentazione o nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="cc492-109">Information is missing from Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="cc492-110">Raggiungimento dei limiti di segmentazione.</span><span class="sxs-lookup"><span data-stu-id="cc492-110">Hitting segmentation limits.</span></span>

### <a name="causes"></a><span data-ttu-id="cc492-111">Cause</span><span class="sxs-lookup"><span data-stu-id="cc492-111">Causes</span></span>
* <span data-ttu-id="cc492-112">È possibile usare le API Analytics, Monitor e Segments per verificare se i dati che non vengono visualizzati nell'interfaccia utente sono visibili tramite le API.</span><span class="sxs-lookup"><span data-stu-id="cc492-112">You can use the Analytics API, Monitor API, and Segments API to see if any data you are missing from the UI is visible through the APIs.</span></span>
* <span data-ttu-id="cc492-113">Se Azure Mobile Engagement SDK non è stato integrato correttamente nell'app, non sarà possibile visualizzare le informazioni nell'analisi, nella segmentazione, nel monitoraggio o nei dashboard.</span><span class="sxs-lookup"><span data-stu-id="cc492-113">If the Azure Mobile Engagement SDK is not correctly integrated into your app then you won't be able to see information in the Analytics, Segmentation, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="cc492-114">Una volta creati, i segmenti possono essere soltanto "clonati" (copiati) o "distrutti" (eliminati).</span><span class="sxs-lookup"><span data-stu-id="cc492-114">Segments can't be changed once they are created, segments can only be "cloned" (copied) or "destroyed" (deleted).</span></span> <span data-ttu-id="cc492-115">I segmenti possono contenere solo 10 criteri.</span><span class="sxs-lookup"><span data-stu-id="cc492-115">Segments can only contain 10 criteria.</span></span>
* <span data-ttu-id="cc492-116">Il modo migliore per verificare le informazioni non visualizzate nel monitoraggio consiste nel configurare un dispositivo di test, disinstallare l'app dal dispositivo e/o reinstallarla.</span><span class="sxs-lookup"><span data-stu-id="cc492-116">The best way to test missing information from monitoring is to setup a test device, uninstall and/or reinstall the app on the test device.</span></span>
* <span data-ttu-id="cc492-117">Le informazioni vengono aggiornate ogni 24 ore per l'analisi, la segmentazione o i dashboard.</span><span class="sxs-lookup"><span data-stu-id="cc492-117">Information is refreshed every 24 hours for Analytics, Segmentation, or Dashboards.</span></span>
* <span data-ttu-id="cc492-118">È possibile che le informazioni nei nuovi segmenti vengano visualizzate solo dopo 24 ore dal momento della creazione, anche se il segmento si basa su informazioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="cc492-118">Information in new segments may not be displayed until 24 hours after they are created even if the segment is based on previous information.</span></span>
* <span data-ttu-id="cc492-119">Se i dati di analisi presenti nell'interfaccia utente vengono filtrati, è possibile visualizzare tutti gli esempi di questo tipo, indipendentemente dalla versione dell'app. Ad esempio, se si filtrano gli "arresti anomali" in base al nome, verranno visualizzati quelli delle versioni 1 e 2 dell'app.</span><span class="sxs-lookup"><span data-stu-id="cc492-119">Filtering your analytics data in the UI will show all examples of this type regardless of the version of your app (e.g. "Crashes" filtered by name will show from version 1 and version 2 of your app).</span></span>
* <span data-ttu-id="cc492-120">Il periodo per l'analisi si basa sulla data presente nelle impostazioni del dispositivo dell'utente. Pertanto, se nel telefono di un utente la data è impostata in modo errato, è possibile che venga visualizzato il periodo errato.</span><span class="sxs-lookup"><span data-stu-id="cc492-120">The time period for Analytics is based on the date from the users' device settings, so a user whose phone has the date incorrectly set could show up in the wrong time period.</span></span>
* <span data-ttu-id="cc492-121">Non vengono registrati dati sul lato server quando si usa il pulsante per "testare" i push, vengono registrati solo i dati per le campagne di push reali.</span><span class="sxs-lookup"><span data-stu-id="cc492-121">No server side data is logged when you use the button to "test" pushes, data is only logged for real push campaigns.</span></span>

## <a name="cant-locate-items-in-ui"></a><span data-ttu-id="cc492-122">Impossibile individuare elementi nell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="cc492-122">Can't locate items in UI</span></span>
### <a name="issue"></a><span data-ttu-id="cc492-123">Problema</span><span class="sxs-lookup"><span data-stu-id="cc492-123">Issue</span></span>
* <span data-ttu-id="cc492-124">Impossibile creare segmenti in base a determinati criteri di tag sulle informazioni dell'app integrati o personalizzati.</span><span class="sxs-lookup"><span data-stu-id="cc492-124">Can't create segments based on certain built in or custom app info tag criteria.</span></span>
* <span data-ttu-id="cc492-125">Impossibile trovare criteri di tag sulle informazioni dell'app integrati o personalizzati nell'analisi, nel monitoraggio o nei dashboard.</span><span class="sxs-lookup"><span data-stu-id="cc492-125">Can't find certain built in or custom app info tag criteria in Analytics, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="cc492-126">Impossibile interpretare i dati presenti nell'analisi, nel monitoraggio, nella segmentazione o nei dashboard.</span><span class="sxs-lookup"><span data-stu-id="cc492-126">Can't interpret the data in Analytics, Monitoring, Segmentation, or Dashboards.</span></span>

### <a name="causes"></a><span data-ttu-id="cc492-127">Cause</span><span class="sxs-lookup"><span data-stu-id="cc492-127">Causes</span></span>
* <span data-ttu-id="cc492-128">Alcuni elementi integrati e tag sulle informazioni dell'app sono disponibili soltanto come criteri di inserimento, ma non possono essere aggiunti a un segmento o essere visibili nell'analisi, nel monitoraggio o nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="cc492-128">Some built in items and app info tags are only available as push criteria but may not be added to a segment or visible from Analytics, Monitoring, or Dashboard.</span></span> 
* <span data-ttu-id="cc492-129">Nel caso di elementi integrati e tag sulle informazioni dell'app che non possono essere aggiunti a un segmento, sarà necessario impostare un elenco di criteri di destinazione per ogni campagna, in modo che eseguano la stessa funzione di selezione della destinazione basata su un segmento.</span><span class="sxs-lookup"><span data-stu-id="cc492-129">For built in items and app info tags that can't be added to a segment, you will need to setup list of targeting criteria in each campaign to perform the same function as targeting based on a segment.</span></span>
* <span data-ttu-id="cc492-130">Visualizzare i menu di scelta rapida nelle sezioni di analisi, monitoraggio e dashboard dell'interfaccia utente di Azure Mobile Engagement per altre informazioni di supporto e procedure.</span><span class="sxs-lookup"><span data-stu-id="cc492-130">See the context menus in the Analytics, Monitoring, Segmentation, and Dashboards sections of the Azure Mobile Engagement UI for more help and how to information.</span></span>

## <a name="crash-troubleshooting"></a><span data-ttu-id="cc492-131">Risoluzione dei problemi di arresto anomalo</span><span class="sxs-lookup"><span data-stu-id="cc492-131">Crash troubleshooting</span></span>
### <a name="issue"></a><span data-ttu-id="cc492-132">Problema</span><span class="sxs-lookup"><span data-stu-id="cc492-132">Issue</span></span>
* <span data-ttu-id="cc492-133">Gli arresti anomali dell'applicazione vengono visualizzati nelle sezioni di analisi, monitoraggio o dashboard.</span><span class="sxs-lookup"><span data-stu-id="cc492-133">Application Crashes appearing in Analytics, Monitoring, or Dashboard.</span></span>

### <a name="causes"></a><span data-ttu-id="cc492-134">Cause</span><span class="sxs-lookup"><span data-stu-id="cc492-134">Causes</span></span>
* <span data-ttu-id="cc492-135">Per risolvere i problemi di arresto anomalo dell'applicazione visualizzati nelle sezioni di analisi, monitoraggio o dashboard, controllare le note sulla versione e verificare la presenza di problemi noti nelle versioni precedenti dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="cc492-135">To troubleshoot Application Crashes seen in Analytics, Monitoring, or Dashboard make sure to check the release notes for known issues with previous versions of the SDK.</span></span>
* <span data-ttu-id="cc492-136">Per risolvere altri problemi di arresto anomalo dell'app, eseguire un evento da un dispositivo di test su cui è installata l'app, quindi cercare l'ID dispositivo nella sezione "Monitor - Eventi" dell'interfaccia utente di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="cc492-136">To further troubleshoot application crashes perform an event from a test device with your application installed and look up your device ID in the “Monitor – Events” section of the Azure Mobile Engagement UI.</span></span> <span data-ttu-id="cc492-137">Quindi, eseguire l'evento che causa l'arresto anomalo dell'applicazione e cercare altre informazioni nella sezione "Monitor - Arresto anomalo" dell'interfaccia utente di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="cc492-137">Then perform the event that is causing your application to crash and look up additional information in the “Monitor – Crash” section of the Azure Mobile Engagement UI.</span></span> 

