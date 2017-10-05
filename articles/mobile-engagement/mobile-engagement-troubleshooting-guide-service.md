---
title: Guida alla risoluzione dei problemi di Azure Mobile Engagement - Servizio
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
ms.openlocfilehash: f13fd0540b783120014b3a8d4e41f78808c7fade
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a><span data-ttu-id="431ae-103">Guida alla risoluzione dei problemi relativi al servizio</span><span class="sxs-lookup"><span data-stu-id="431ae-103">Troubleshooting guide for Service issues</span></span>
<span data-ttu-id="431ae-104">Di seguito sono indicati possibili problemi relativi all'esecuzione di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="431ae-104">The following are possible issues you may encounter with how Azure Mobile Engagement runs.</span></span>

## <a name="service-outages"></a><span data-ttu-id="431ae-105">Interruzioni di servizio</span><span class="sxs-lookup"><span data-stu-id="431ae-105">Service Outages</span></span>
### <a name="issue"></a><span data-ttu-id="431ae-106">Problema</span><span class="sxs-lookup"><span data-stu-id="431ae-106">Issue</span></span>
* <span data-ttu-id="431ae-107">Problemi che sembrano essere causati da interruzioni del servizio Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="431ae-107">Issues that appear to be caused by Azure Mobile Engagement Service Outages.</span></span>

### <a name="causes"></a><span data-ttu-id="431ae-108">Cause</span><span class="sxs-lookup"><span data-stu-id="431ae-108">Causes</span></span>
* <span data-ttu-id="431ae-109">I problemi che sembrano dovuti a interruzioni del servizio Azure Mobile Engagement possono avere diverse cause:</span><span class="sxs-lookup"><span data-stu-id="431ae-109">Issues that appear to be caused by Azure Mobile Engagement Service Outages can be caused by several different issues:</span></span>
  * <span data-ttu-id="431ae-110">Problemi isolati visualizzati originariamente come sistemici in Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="431ae-110">Isolated issues that originally appear systemic to all of Azure Mobile Engagement</span></span>
  * <span data-ttu-id="431ae-111">Problemi noti causati da interruzioni del server (non sempre visualizzati nello stato del server).</span><span class="sxs-lookup"><span data-stu-id="431ae-111">Known issues caused by server outages (not always shows in server status):</span></span>
  * <span data-ttu-id="431ae-112">Ritardi di pianificazione, errori di destinazione, problemi nell'aggiornamento del badge, interruzione della raccolta dei dati da parte dei sistemi statistici, interruzione del funzionamento delle notifiche push e delle API, impossibilità di creazione di nuovi utenti o app, errori DNS e di timeout nell'interfaccia utente, nell'API o nelle app del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="431ae-112">Scheduling delays, Targeting errors, Badge update issues, Statistics stop collecting, Push stops working, API's stop working, New apps or users can't be created, DNS errors, and Timeout errors in the UI, API, or Apps on a device.</span></span>
  * <span data-ttu-id="431ae-113">Interruzioni di dipendenza cloud [Stato del servizio Azure](http://status.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="431ae-113">Cloud Dependency Outages [Azure Service Status](http://status.azure.com/)</span></span>
  * <span data-ttu-id="431ae-114">Interruzione di dipendenza servizi di notifica push (PNS, Push Notification Services)</span><span class="sxs-lookup"><span data-stu-id="431ae-114">Push Notification Services (PNS) Dependency Outages</span></span>
  * <span data-ttu-id="431ae-115">Interruzioni di App Store</span><span class="sxs-lookup"><span data-stu-id="431ae-115">App Store Outages</span></span>

1) <span data-ttu-id="431ae-116">Per verificare se il problema è sistemico, eseguire il test della stessa funzione da un elemento differente</span><span class="sxs-lookup"><span data-stu-id="431ae-116">To test to see if the problem is systemic you can test the same function from a different</span></span>

* <span data-ttu-id="431ae-117">Applicazione integrata di Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="431ae-117">Azure Mobile Engagement integrated application</span></span>
* <span data-ttu-id="431ae-118">Dispositivo di test</span><span class="sxs-lookup"><span data-stu-id="431ae-118">Test device</span></span>
* <span data-ttu-id="431ae-119">Versione del sistema operativo del dispositivo di test</span><span class="sxs-lookup"><span data-stu-id="431ae-119">Test device OS version</span></span>
* <span data-ttu-id="431ae-120">Campagna</span><span class="sxs-lookup"><span data-stu-id="431ae-120">Campaign</span></span>
* <span data-ttu-id="431ae-121">Account utente dell'amministratore</span><span class="sxs-lookup"><span data-stu-id="431ae-121">Administrator user account</span></span>
* <span data-ttu-id="431ae-122">Browser (Internet Explorer, Firefox, Chrome, ecc.)</span><span class="sxs-lookup"><span data-stu-id="431ae-122">Browser (IE, Firefox, Chrome, etc.)</span></span>
* <span data-ttu-id="431ae-123">Computer</span><span class="sxs-lookup"><span data-stu-id="431ae-123">Computer</span></span>

2) <span data-ttu-id="431ae-124">Per verificare se il problema riguarda soltanto l'interfaccia utente o l'API:</span><span class="sxs-lookup"><span data-stu-id="431ae-124">To test if the problem only affects the UI or the API's:</span></span>

* <span data-ttu-id="431ae-125">Verificare la stessa funzione dall'interfaccia utente di Azure Mobile Engagement e dell'API di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="431ae-125">Test the same function from both the Azure Mobile Engagement UI and the Azure Mobile Engagement API's.</span></span>

3) <span data-ttu-id="431ae-126">Per verificare se il problema riguarda la rete dati:</span><span class="sxs-lookup"><span data-stu-id="431ae-126">To test if the problem is with your Cellular Phone Network:</span></span>

* <span data-ttu-id="431ae-127">Eseguire il test mentre si è connessi a Internet tramite Wi-Fi e mentre si è connessi tramite la rete dati 3G.</span><span class="sxs-lookup"><span data-stu-id="431ae-127">Test while connected to the Internet via WIFI and while connected via your 3G cellular phone network.</span></span>
* <span data-ttu-id="431ae-128">Verificare che il firewall non blocchi porte o indirizzi IP di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="431ae-128">Confirm that your firewall is not blocking any of the Azure Mobile Engagement IP Addresses or Ports.</span></span>

4) <span data-ttu-id="431ae-129">Per verificare se il problema riguarda il dispositivo:</span><span class="sxs-lookup"><span data-stu-id="431ae-129">To test if the problem is with your Device:</span></span>

* <span data-ttu-id="431ae-130">Verificare se il dispositivo è in grado di connettersi a Azure Mobile Engagement con un'altra app integrata di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="431ae-130">Test if your Device is able to connect to Azure Mobile Engagement with another Azure Mobile Engagement integrated app.</span></span>
* <span data-ttu-id="431ae-131">Verificare che sia possibile generare eventi, processi e arresti anomali del sistema dal telefono che può essere visualizzato nell'interfaccia utente di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="431ae-131">Test that you can generate Events, Jobs, and Crashes from your phone that can be seen in the Azure Mobile Engagement UI.</span></span> 
* <span data-ttu-id="431ae-132">Verificare se è possibile inviare notifiche push dall'interfaccia utente di Azure Mobile Engagement sul dispositivo in base al relativo ID dispositivo.</span><span class="sxs-lookup"><span data-stu-id="431ae-132">Test if you can send push notifications from the Azure Mobile Engagement UI to your device based on its Device ID.</span></span> 

5) <span data-ttu-id="431ae-133">Per verificare se il problema riguarda l'app:</span><span class="sxs-lookup"><span data-stu-id="431ae-133">To test if the problem is with your App:</span></span>

* <span data-ttu-id="431ae-134">Installare e testare l'applicazione da un emulatore anziché da un dispositivo fisico:</span><span class="sxs-lookup"><span data-stu-id="431ae-134">Install and test your application from an emulator instead of from a physical device:</span></span>

6) <span data-ttu-id="431ae-135">Per verificare se il problema riguarda gli aggiornamenti relativi al sistema operativo del dispositivo dell'utente finale ed è necessario aggiornare l'SDK per risolvere:</span><span class="sxs-lookup"><span data-stu-id="431ae-135">To test if the problem is with OS upgrades to end user Devices, which require an SDK upgrade to resolve:</span></span>

* <span data-ttu-id="431ae-136">Verificare l'applicazione in dispositivi diversi con diverse versioni del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="431ae-136">Test your application on different devices with different versions of the OS.</span></span>
* <span data-ttu-id="431ae-137">Confermare che si utilizza la versione più recente dell’SDK.</span><span class="sxs-lookup"><span data-stu-id="431ae-137">Confirm that you are using the most recent version of the SDK.</span></span>

## <a name="connectivity-and-incorrect-information-issues"></a><span data-ttu-id="431ae-138">Problemi di connettività e di informazioni non corrette</span><span class="sxs-lookup"><span data-stu-id="431ae-138">Connectivity and Incorrect Information Issues</span></span>
### <a name="issue"></a><span data-ttu-id="431ae-139">Problema</span><span class="sxs-lookup"><span data-stu-id="431ae-139">Issue</span></span>
* <span data-ttu-id="431ae-140">Problemi di accesso all'interfaccia utente di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="431ae-140">Problems logging into the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="431ae-141">Errori di connessione relativi alle API di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="431ae-141">Connection errors with the Azure Mobile Engagement API's.</span></span>
* <span data-ttu-id="431ae-142">Problemi relativi al caricamento dei tag sulle informazioni dell'app usando l'API del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="431ae-142">Problems uploading App Info Tags via the Device API.</span></span>
* <span data-ttu-id="431ae-143">Problemi relativi al download di registri o di dati esportati da Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="431ae-143">Problems downloading logs or exported data from Azure Mobile Engagement.</span></span>
* <span data-ttu-id="431ae-144">Informazioni non corrette visualizzate nell'interfaccia utente di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="431ae-144">Incorrect information shown in the Azure Mobile Engagement UI.</span></span>
* <span data-ttu-id="431ae-145">Informazioni non corrette visualizzate nei registri di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="431ae-145">Incorrect information shown in Azure Mobile Engagement logs.</span></span>

### <a name="causes"></a><span data-ttu-id="431ae-146">Cause</span><span class="sxs-lookup"><span data-stu-id="431ae-146">Causes</span></span>
* <span data-ttu-id="431ae-147">Confermare che l'account dispone delle autorizzazioni necessarie a eseguire l'attività.</span><span class="sxs-lookup"><span data-stu-id="431ae-147">Confirm your user account has sufficient permissions to perform the task.</span></span>
* <span data-ttu-id="431ae-148">Confermare che il problema non è relativo a un solo computer o alla propria rete locale.</span><span class="sxs-lookup"><span data-stu-id="431ae-148">Confirm that the problem is not isolated to one computer or your local network.</span></span>
* <span data-ttu-id="431ae-149">Confermare che il servizio Azure Mobile Engagement non ha riportato interruzioni.</span><span class="sxs-lookup"><span data-stu-id="431ae-149">Confirm that that the Azure Mobile Engagement service has no reported outages.</span></span>
* <span data-ttu-id="431ae-150">Confermare che i file relativi al tag di informazioni sull'app seguono tutte le regole seguenti:</span><span class="sxs-lookup"><span data-stu-id="431ae-150">Confirm that your App Info Tag files follow all of these rules:</span></span>
  * <span data-ttu-id="431ae-151">Usare solo il set di caratteri UTF8 (set di caratteri ANSI non supportato).</span><span class="sxs-lookup"><span data-stu-id="431ae-151">Use only the UTF8 character set (the ANSI character set is not supported).</span></span>
  * <span data-ttu-id="431ae-152">Usare la virgola "," come separatore. È possibile aprire una richiesta di assistenza per richiedere di non usare la virgola "," come separatore, ma un altro carattere, ad esempio il punto e virgola ";".</span><span class="sxs-lookup"><span data-stu-id="431ae-152">Use a comma "," as the separator character (you can open a service request to request to change the .csv separator character from a comma "," to another character such as a semi-colon ";").</span></span>
  * <span data-ttu-id="431ae-153">Usare tutte le lettere minuscole per i valori Boolean "true" e "false".</span><span class="sxs-lookup"><span data-stu-id="431ae-153">Use all lower case for Boolean values "true" and "false".</span></span>
  * <span data-ttu-id="431ae-154">Usare un file di dimensioni inferiori a 35 MB (limite consentito).</span><span class="sxs-lookup"><span data-stu-id="431ae-154">Use a file that is smaller than the maximum file size of 35MB.</span></span>

