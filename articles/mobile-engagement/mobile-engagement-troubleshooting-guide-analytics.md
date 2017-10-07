---
title: aaaAzure Mobile Engagement Troubleshooting Guide - Analitica
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
ms.openlocfilehash: 69c6ff8f5c8540f8ba8b85b9ffec55acc59329fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a><span data-ttu-id="37b55-103">Guida alla risoluzione dei problemi relativi ad analisi, monitoraggio, segmentazione e dashboard</span><span class="sxs-lookup"><span data-stu-id="37b55-103">Troubleshooting guide for Analytics, Monitoring, Segmentation, and Dashboard issues</span></span>
<span data-ttu-id="37b55-104">di seguito Hello sono possibili problemi che possono verificarsi con Azure Mobile Engagement come raccoglie le informazioni sulle applicazioni e dispositivi e utenti.</span><span class="sxs-lookup"><span data-stu-id="37b55-104">hello following are possible issues you may encounter with how Azure Mobile Engagement gathers information about your applications, devices, and users.</span></span>

## <a name="missingdelayed-information"></a><span data-ttu-id="37b55-105">Informazioni mancanti o in ritardo</span><span class="sxs-lookup"><span data-stu-id="37b55-105">Missing/Delayed information</span></span>
### <a name="issue"></a><span data-ttu-id="37b55-106">Problema</span><span class="sxs-lookup"><span data-stu-id="37b55-106">Issue</span></span>
* <span data-ttu-id="37b55-107">Informazioni visualizzate in ritardo nell'analisi, nella segmentazione o nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="37b55-107">Information is delayed in appearing in Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="37b55-108">Informazioni mancanti nel monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="37b55-108">Information is missing from Monitoring.</span></span>
* <span data-ttu-id="37b55-109">Informazioni mancanti nell'analisi, nella segmentazione o nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="37b55-109">Information is missing from Analytics, Segmentation, or Dashboard.</span></span>
* <span data-ttu-id="37b55-110">Raggiungimento dei limiti di segmentazione.</span><span class="sxs-lookup"><span data-stu-id="37b55-110">Hitting segmentation limits.</span></span>

### <a name="causes"></a><span data-ttu-id="37b55-111">Cause</span><span class="sxs-lookup"><span data-stu-id="37b55-111">Causes</span></span>
* <span data-ttu-id="37b55-112">È possibile utilizzare hello API Analitica, API di monitoraggio, e API segmenti toosee se tutti i dati mancano hello dell'interfaccia utente è visibile attraverso le API di hello.</span><span class="sxs-lookup"><span data-stu-id="37b55-112">You can use hello Analytics API, Monitor API, and Segments API toosee if any data you are missing from hello UI is visible through hello APIs.</span></span>
* <span data-ttu-id="37b55-113">Se correttamente hello Azure Mobile Engagement SDK non è integrato nell'app quindi non sarà in grado di toosee informazioni in hello Analitica, segmentazione, monitoraggio o dashboard.</span><span class="sxs-lookup"><span data-stu-id="37b55-113">If hello Azure Mobile Engagement SDK is not correctly integrated into your app then you won't be able toosee information in hello Analytics, Segmentation, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="37b55-114">Una volta creati, i segmenti possono essere soltanto "clonati" (copiati) o "distrutti" (eliminati).</span><span class="sxs-lookup"><span data-stu-id="37b55-114">Segments can't be changed once they are created, segments can only be "cloned" (copied) or "destroyed" (deleted).</span></span> <span data-ttu-id="37b55-115">I segmenti possono contenere solo 10 criteri.</span><span class="sxs-lookup"><span data-stu-id="37b55-115">Segments can only contain 10 criteria.</span></span>
* <span data-ttu-id="37b55-116">tootest modo migliore di Hello mancano le informazioni di monitoraggio è un dispositivo di test toosetup, disinstallare e/o reinstallare hello app sul dispositivo di test hello.</span><span class="sxs-lookup"><span data-stu-id="37b55-116">hello best way tootest missing information from monitoring is toosetup a test device, uninstall and/or reinstall hello app on hello test device.</span></span>
* <span data-ttu-id="37b55-117">Le informazioni vengono aggiornate ogni 24 ore per l'analisi, la segmentazione o i dashboard.</span><span class="sxs-lookup"><span data-stu-id="37b55-117">Information is refreshed every 24 hours for Analytics, Segmentation, or Dashboards.</span></span>
* <span data-ttu-id="37b55-118">Informazioni contenute in nuovi segmenti potrebbe non essere visualizzati fino a 24 ore dopo averli creati, anche se il segmento hello è in base alle informazioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="37b55-118">Information in new segments may not be displayed until 24 hours after they are created even if hello segment is based on previous information.</span></span>
* <span data-ttu-id="37b55-119">Filtrare i dati analitica in hello dell'interfaccia utente visualizzerà tutti gli esempi di questo tipo, indipendentemente dalla versione di hello dell'app (ad esempio Ad esempio, se si filtrano gli "arresti anomali" in base al nome, verranno visualizzati quelli delle versioni 1 e 2 dell'app.</span><span class="sxs-lookup"><span data-stu-id="37b55-119">Filtering your analytics data in hello UI will show all examples of this type regardless of hello version of your app (e.g. "Crashes" filtered by name will show from version 1 and version 2 of your app).</span></span>
* <span data-ttu-id="37b55-120">Hello periodo di tempo per Analitica è basato sulla data hello dalle impostazioni del dispositivo degli utenti hello, pertanto un utente il cui telefono è data hello impostato in modo errato può visualizzati nella hello errato periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="37b55-120">hello time period for Analytics is based on hello date from hello users' device settings, so a user whose phone has hello date incorrectly set could show up in hello wrong time period.</span></span>
* <span data-ttu-id="37b55-121">Inserisce alcun lato server vengono registrati i dati quando si utilizza il pulsante hello troppo "non test", i dati vengono registrati solo per le campagne push reale.</span><span class="sxs-lookup"><span data-stu-id="37b55-121">No server side data is logged when you use hello button too"test" pushes, data is only logged for real push campaigns.</span></span>

## <a name="cant-locate-items-in-ui"></a><span data-ttu-id="37b55-122">Impossibile individuare elementi nell'interfaccia utente</span><span class="sxs-lookup"><span data-stu-id="37b55-122">Can't locate items in UI</span></span>
### <a name="issue"></a><span data-ttu-id="37b55-123">Problema</span><span class="sxs-lookup"><span data-stu-id="37b55-123">Issue</span></span>
* <span data-ttu-id="37b55-124">Impossibile creare segmenti in base a determinati criteri di tag sulle informazioni dell'app integrati o personalizzati.</span><span class="sxs-lookup"><span data-stu-id="37b55-124">Can't create segments based on certain built in or custom app info tag criteria.</span></span>
* <span data-ttu-id="37b55-125">Impossibile trovare criteri di tag sulle informazioni dell'app integrati o personalizzati nell'analisi, nel monitoraggio o nei dashboard.</span><span class="sxs-lookup"><span data-stu-id="37b55-125">Can't find certain built in or custom app info tag criteria in Analytics, Monitoring, or Dashboards.</span></span>
* <span data-ttu-id="37b55-126">Impossibile interpretare i dati di hello in Analitica, il monitoraggio, segmentazione o dashboard.</span><span class="sxs-lookup"><span data-stu-id="37b55-126">Can't interpret hello data in Analytics, Monitoring, Segmentation, or Dashboards.</span></span>

### <a name="causes"></a><span data-ttu-id="37b55-127">Cause</span><span class="sxs-lookup"><span data-stu-id="37b55-127">Causes</span></span>
* <span data-ttu-id="37b55-128">Alcuni compilati negli elementi e informazioni sull'app tag sono disponibili solo come criteri di push, ma non possono essere aggiunti tooa segmento o visibili da Analitica, monitoraggio o Dashboard.</span><span class="sxs-lookup"><span data-stu-id="37b55-128">Some built in items and app info tags are only available as push criteria but may not be added tooa segment or visible from Analytics, Monitoring, or Dashboard.</span></span> 
* <span data-ttu-id="37b55-129">Per incorporate negli elementi e informazioni sull'app tag che non può essere aggiunto tooa segmento, sarà necessario toosetup elenco di criteri di ogni hello tooperform campagna stessa funzione come destinazione in base a un segmento di destinazione.</span><span class="sxs-lookup"><span data-stu-id="37b55-129">For built in items and app info tags that can't be added tooa segment, you will need toosetup list of targeting criteria in each campaign tooperform hello same function as targeting based on a segment.</span></span>
* <span data-ttu-id="37b55-130">Vedere i menu di scelta rapida hello nelle sezioni Analitica, monitoraggio, segmentazione e i dashboard di hello di hello dell'interfaccia utente di Azure Mobile Engagement per ulteriori informazioni e come tooinformation.</span><span class="sxs-lookup"><span data-stu-id="37b55-130">See hello context menus in hello Analytics, Monitoring, Segmentation, and Dashboards sections of hello Azure Mobile Engagement UI for more help and how tooinformation.</span></span>

## <a name="crash-troubleshooting"></a><span data-ttu-id="37b55-131">Risoluzione dei problemi di arresto anomalo</span><span class="sxs-lookup"><span data-stu-id="37b55-131">Crash troubleshooting</span></span>
### <a name="issue"></a><span data-ttu-id="37b55-132">Problema</span><span class="sxs-lookup"><span data-stu-id="37b55-132">Issue</span></span>
* <span data-ttu-id="37b55-133">Gli arresti anomali dell'applicazione vengono visualizzati nelle sezioni di analisi, monitoraggio o dashboard.</span><span class="sxs-lookup"><span data-stu-id="37b55-133">Application Crashes appearing in Analytics, Monitoring, or Dashboard.</span></span>

### <a name="causes"></a><span data-ttu-id="37b55-134">Cause</span><span class="sxs-lookup"><span data-stu-id="37b55-134">Causes</span></span>
* <span data-ttu-id="37b55-135">Blocchi applicazione tootroubleshoot visualizzati nel Dashboard, monitoraggio o Analitica rendere note sulla versione di hello toocheck che per i problemi noti con le versioni precedenti di hello SDK.</span><span class="sxs-lookup"><span data-stu-id="37b55-135">tootroubleshoot Application Crashes seen in Analytics, Monitoring, or Dashboard make sure toocheck hello release notes for known issues with previous versions of hello SDK.</span></span>
* <span data-ttu-id="37b55-136">toofurther di risolvere i problemi applicazione arresti anomali del sistema esegue un evento da un dispositivo di test con l'applicazione installata e cercare l'ID dispositivo nella sezione hello "eventi – monitoraggio" hello dell'interfaccia utente di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="37b55-136">toofurther troubleshoot application crashes perform an event from a test device with your application installed and look up your device ID in hello “Monitor – Events” section of hello Azure Mobile Engagement UI.</span></span> <span data-ttu-id="37b55-137">Quindi eseguire hello evento che causa l'applicazione toocrash e cercare informazioni aggiuntive in hello "Monitoraggio – Crash" sezione di hello dell'interfaccia utente di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="37b55-137">Then perform hello event that is causing your application toocrash and look up additional information in hello “Monitor – Crash” section of hello Azure Mobile Engagement UI.</span></span> 

