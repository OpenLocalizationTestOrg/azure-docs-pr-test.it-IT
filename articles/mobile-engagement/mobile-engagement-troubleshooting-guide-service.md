---
title: aaaAzure Mobile Engagement Troubleshooting Guide - servizio
description: Guide alla risoluzione dei problemi di Azure Mobile Engagement
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8b4275da-c0b4-4690-824a-48e9d7a1fc6e
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: cf48db323a873ccef95946f7bb26e8d7473c002f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a><span data-ttu-id="dfeef-103">Guida alla risoluzione dei problemi relativi al servizio</span><span class="sxs-lookup"><span data-stu-id="dfeef-103">Troubleshooting guide for Service issues</span></span>
<span data-ttu-id="dfeef-104">di seguito Hello sono possibili problemi che possono verificarsi con la modalità di esecuzione di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="dfeef-104">hello following are possible issues you may encounter with how Azure Mobile Engagement runs.</span></span>

## <a name="service-outages"></a><span data-ttu-id="dfeef-105">Interruzioni di servizio</span><span class="sxs-lookup"><span data-stu-id="dfeef-105">Service Outages</span></span>
### <a name="issue"></a><span data-ttu-id="dfeef-106">Problema</span><span class="sxs-lookup"><span data-stu-id="dfeef-106">Issue</span></span>
* <span data-ttu-id="dfeef-107">Problemi causati da interruzioni del servizio di Azure Mobile Engagement toobe visualizzati.</span><span class="sxs-lookup"><span data-stu-id="dfeef-107">Issues that appear toobe caused by Azure Mobile Engagement Service Outages.</span></span>

### <a name="causes"></a><span data-ttu-id="dfeef-108">Cause</span><span class="sxs-lookup"><span data-stu-id="dfeef-108">Causes</span></span>
* <span data-ttu-id="dfeef-109">I problemi causati da interruzioni del servizio di Azure Mobile Engagement toobe alle possono essere causati da diversi fattori:</span><span class="sxs-lookup"><span data-stu-id="dfeef-109">Issues that appear toobe caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span></span>
  * <span data-ttu-id="dfeef-110">Problemi isolati apparentemente originariamente tooall sistemica di Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="dfeef-110">Isolated issues that originally appear systemic tooall of Azure Mobile Engagement</span></span>
  * <span data-ttu-id="dfeef-111">Problemi noti causati da interruzioni del server (non sempre visualizzati nello stato del server).</span><span class="sxs-lookup"><span data-stu-id="dfeef-111">Known issues caused by server outages (not always shows in server status):</span></span>
  * <span data-ttu-id="dfeef-112">Pianificazione ritardi, gli errori di assegnazione, problemi di aggiornamento di Badge, arresto statistiche raccolgono, Push smette di funzionare, API smettono di funzionare, nuove app o gli utenti Impossibile creare, errori DNS e gli errori di Timeout in hello dell'interfaccia utente, l'API o App in un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dfeef-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in hello UI, API, or Apps on a device.</span></span>
  * <span data-ttu-id="dfeef-113">Interruzioni di dipendenza cloud [Stato del servizio Azure](http://status.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="dfeef-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span></span>
  * <span data-ttu-id="dfeef-114">Interruzione di dipendenza servizi di notifica push (PNS, Push Notification Services)</span><span class="sxs-lookup"><span data-stu-id="dfeef-114">Push Notification Services (PNS) Dependency Outages</span></span>
  * <span data-ttu-id="dfeef-115">Interruzioni di App Store</span><span class="sxs-lookup"><span data-stu-id="dfeef-115">App Store Outages</span></span>

1) <span data-ttu-id="dfeef-116">tootest toosee se il problema di hello dipende sistemico è possibile testare hello stessa funzione da un altro</span><span class="sxs-lookup"><span data-stu-id="dfeef-116">tootest toosee if hello problem is systemic you can test hello same function from a different</span></span>

* <span data-ttu-id="dfeef-117">Applicazione integrata di Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="dfeef-117">Azure Mobile Engagement integrated application</span></span>
* <span data-ttu-id="dfeef-118">Dispositivo di test</span><span class="sxs-lookup"><span data-stu-id="dfeef-118">Test device</span></span>
* <span data-ttu-id="dfeef-119">Versione del sistema operativo del dispositivo di test</span><span class="sxs-lookup"><span data-stu-id="dfeef-119">Test device OS version</span></span>
* <span data-ttu-id="dfeef-120">Campagna</span><span class="sxs-lookup"><span data-stu-id="dfeef-120">Campaign</span></span>
* <span data-ttu-id="dfeef-121">Account utente dell'amministratore</span><span class="sxs-lookup"><span data-stu-id="dfeef-121">Administrator user account</span></span>
* <span data-ttu-id="dfeef-122">Browser (Internet Explorer, Firefox, Chrome, ecc.)</span><span class="sxs-lookup"><span data-stu-id="dfeef-122">Browser (IE, Firefox, Chrome, etc.)</span></span>
* <span data-ttu-id="dfeef-123">Computer</span><span class="sxs-lookup"><span data-stu-id="dfeef-123">Computer</span></span>

2) <span data-ttu-id="dfeef-124">tootest se hello problema solo hello dell'interfaccia utente o hello dell'API:</span><span class="sxs-lookup"><span data-stu-id="dfeef-124">tootest if hello problem only affects hello UI or hello API's:</span></span>

* <span data-ttu-id="dfeef-125">Test hello stessa funzione dell'interfaccia utente di Azure Mobile Engagement entrambi hello e hello dell'API di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="dfeef-125">Test hello same function from both hello Azure Mobile Engagement UI and hello Azure Mobile Engagement API's.</span></span>

3) <span data-ttu-id="dfeef-126">tootest se hello problema con la rete cellulare:</span><span class="sxs-lookup"><span data-stu-id="dfeef-126">tootest if hello problem is with your Cellular Phone Network:</span></span>

* <span data-ttu-id="dfeef-127">Eseguire test durante toohello connesso Internet tramite Wi-Fi e durante la connessione tramite la rete cellulare 3G.</span><span class="sxs-lookup"><span data-stu-id="dfeef-127">Test while connected toohello Internet via WIFI and while connected via your 3G cellular phone network.</span></span>
* <span data-ttu-id="dfeef-128">Verificare che il firewall non blocchi le porte o indirizzi IP di hello Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="dfeef-128">Confirm that your firewall is not blocking any of hello Azure Mobile Engagement IP Addresses or Ports.</span></span>

4) <span data-ttu-id="dfeef-129">tootest se hello problema con il dispositivo:</span><span class="sxs-lookup"><span data-stu-id="dfeef-129">tootest if hello problem is with your Device:</span></span>

* <span data-ttu-id="dfeef-130">Verificare se il dispositivo è in grado di tooconnect tooAzure Mobile Engagement con un'altra app integrata di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="dfeef-130">Test if your Device is able tooconnect tooAzure Mobile Engagement with another Azure Mobile Engagement integrated app.</span></span>
* <span data-ttu-id="dfeef-131">Verificare che è possibile generare eventi, i processi e arresti anomali del sistema dal telefono che può essere visualizzato nell'interfaccia utente di Azure Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="dfeef-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in hello Azure Mobile Engagement UI.</span></span> 
* <span data-ttu-id="dfeef-132">Verificare se è possibile inviare notifiche push dal dispositivo di tooyour dell'interfaccia utente di Azure Mobile Engagement hello in base all'ID la periferica.</span><span class="sxs-lookup"><span data-stu-id="dfeef-132">Test if you can send push notifications from hello Azure Mobile Engagement UI tooyour device based on its Device ID.</span></span> 

5) <span data-ttu-id="dfeef-133">tootest se hello problema con l'App:</span><span class="sxs-lookup"><span data-stu-id="dfeef-133">tootest if hello problem is with your App:</span></span>

* <span data-ttu-id="dfeef-134">Installare e testare l'applicazione da un emulatore anziché da un dispositivo fisico:</span><span class="sxs-lookup"><span data-stu-id="dfeef-134">Install and test your application from an emulator instead of from a physical device:</span></span>

6) <span data-ttu-id="dfeef-135">tootest se il problema di hello è un sistema operativo viene aggiornato tooend utente, dispositivi, che richiedono un tooresolve aggiornamento SDK:</span><span class="sxs-lookup"><span data-stu-id="dfeef-135">tootest if hello problem is with OS upgrades tooend user Devices, which require an SDK upgrade tooresolve:</span></span>

* <span data-ttu-id="dfeef-136">Testare l'applicazione in dispositivi diversi con versioni diverse di hello del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="dfeef-136">Test your application on different devices with different versions of hello OS.</span></span>
* <span data-ttu-id="dfeef-137">Confermare che si utilizza hello la versione più recente di hello SDK.</span><span class="sxs-lookup"><span data-stu-id="dfeef-137">Confirm that you are using hello most recent version of hello SDK.</span></span>

## <a name="connectivity-and-incorrect-information-issues"></a><span data-ttu-id="dfeef-138">Problemi di connettività e di informazioni non corrette</span><span class="sxs-lookup"><span data-stu-id="dfeef-138">Connectivity and Incorrect Information Issues</span></span>
### <a name="issue"></a><span data-ttu-id="dfeef-139">Problema</span><span class="sxs-lookup"><span data-stu-id="dfeef-139">Issue</span></span>
* <span data-ttu-id="dfeef-140">Problemi di accesso in hello dell'interfaccia utente di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="dfeef-140">Problems logging into hello Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="dfeef-141">Errori di connessione con l'API di Azure Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="dfeef-141">Connection errors with hello Azure Mobile Engagement API's.</span></span>
* <span data-ttu-id="dfeef-142">Problemi di caricamento dei tag Info App tramite hello Device API.</span><span class="sxs-lookup"><span data-stu-id="dfeef-142">Problems uploading App Info Tags via hello Device API.</span></span>
* <span data-ttu-id="dfeef-143">Problemi relativi al download di registri o di dati esportati da Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="dfeef-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span></span>
* <span data-ttu-id="dfeef-144">Informazioni non corrette nell'interfaccia utente di Azure Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="dfeef-144">Incorrect information shown in hello Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="dfeef-145">Informazioni non corrette visualizzate nei registri di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="dfeef-145">Incorrect information shown in Azure Mobile Engagement logs.</span></span>

### <a name="causes"></a><span data-ttu-id="dfeef-146">Cause</span><span class="sxs-lookup"><span data-stu-id="dfeef-146">Causes</span></span>
* <span data-ttu-id="dfeef-147">Confermare che l'account utente disponga di sufficienti attività hello tooperform di autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="dfeef-147">Confirm your user account has sufficient permissions tooperform hello task.</span></span>
* <span data-ttu-id="dfeef-148">Verificare che il problema di hello non è isolato tooone computer o la rete locale.</span><span class="sxs-lookup"><span data-stu-id="dfeef-148">Confirm that hello problem is not isolated tooone computer or your local network.</span></span>
* <span data-ttu-id="dfeef-149">Verificare che il servizio di Azure Mobile Engagement hello non ha le interruzioni segnalate.</span><span class="sxs-lookup"><span data-stu-id="dfeef-149">Confirm that that hello Azure Mobile Engagement service has no reported outages.</span></span>
* <span data-ttu-id="dfeef-150">Confermare che i file relativi al tag di informazioni sull'app seguono tutte le regole seguenti:</span><span class="sxs-lookup"><span data-stu-id="dfeef-150">Confirm that your App Info Tag files follow all of these rules:</span></span>
  * <span data-ttu-id="dfeef-151">Utilizzare hello solo set di caratteri UTF8 (set di caratteri ANSI hello non supportato).</span><span class="sxs-lookup"><span data-stu-id="dfeef-151">Use only hello UTF8 character set (hello ANSI character set is not supported).</span></span>
  * <span data-ttu-id="dfeef-152">Utilizzare la virgola "," come carattere separatore hello (è possibile aprire un carattere di separatore di servizio richiesta toorequest toochange hello CSV da una virgola carattere tooanother ",", ad esempio un punto e virgola ";").</span><span class="sxs-lookup"><span data-stu-id="dfeef-152">Use a comma "," as hello separator character (you can open a service request toorequest toochange hello .csv separator character from a comma "," tooanother character such as a semi-colon ";").</span></span>
  * <span data-ttu-id="dfeef-153">Usare tutte le lettere minuscole per i valori Boolean "true" e "false".</span><span class="sxs-lookup"><span data-stu-id="dfeef-153">Use all lower case for Boolean values "true" and "false".</span></span>
  * <span data-ttu-id="dfeef-154">Utilizzare un file di dimensioni inferiori a quelle delle dimensioni massime del file hello di 35MB.</span><span class="sxs-lookup"><span data-stu-id="dfeef-154">Use a file that is smaller than hello maximum file size of 35MB.</span></span>

