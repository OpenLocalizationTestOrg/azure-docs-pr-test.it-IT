---
title: Come usare Hub di notifica con Java
description: Informazioni su come usare Hub di notifica di Azure da un back-end Java.
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 4c3f966d-0158-4a48-b949-9fa3666cb7e4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: java
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 41f978750ddef9f7e878c65b0017e909720154aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-notification-hubs-from-java"></a><span data-ttu-id="d77e7-103">Come usare Hub di notifica da Java</span><span class="sxs-lookup"><span data-stu-id="d77e7-103">How to use Notification Hubs from Java</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="d77e7-104">Questo argomento descrive le funzionalità principali del nuovo ufficiale SDK per Java di Hub di notifica di Azure, completamente supportato.</span><span class="sxs-lookup"><span data-stu-id="d77e7-104">This topic describes the key features of the new fully supported official Azure Notification Hub Java SDK.</span></span> <span data-ttu-id="d77e7-105">Si tratta di un progetto open source ed è possibile visualizzare il codice SDK completo nell'articolo relativo all' [SDK per Java].</span><span class="sxs-lookup"><span data-stu-id="d77e7-105">This is an open source project and you can view the entire SDK code at [Java SDK].</span></span> 

<span data-ttu-id="d77e7-106">In generale, è possibile accedere a tutte le funzionalità di Hub di notifica da un back-end Java/PHP/Python/Ruby tramite l'interfaccia REST di Hub di notifica, come descritto nell'argomento [API REST degli hub di notifica](http://msdn.microsoft.com/library/dn223264.aspx)di MSDN.</span><span class="sxs-lookup"><span data-stu-id="d77e7-106">In general, you can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span> <span data-ttu-id="d77e7-107">L'SDK per Java fornisce un semplice wrapper per le interfacce REST in Java.</span><span class="sxs-lookup"><span data-stu-id="d77e7-107">This Java SDK provides a thin wrapper over these REST interfaces in Java.</span></span> 

<span data-ttu-id="d77e7-108">L'SDK attualmente supporta:</span><span class="sxs-lookup"><span data-stu-id="d77e7-108">The SDK supports currently:</span></span>

* <span data-ttu-id="d77e7-109">CRUD in Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="d77e7-109">CRUD on Notification Hubs</span></span> 
* <span data-ttu-id="d77e7-110">CRUD in Registrazioni</span><span class="sxs-lookup"><span data-stu-id="d77e7-110">CRUD on Registrations</span></span>
* <span data-ttu-id="d77e7-111">Gestione dell'installazione</span><span class="sxs-lookup"><span data-stu-id="d77e7-111">Installation Management</span></span>
* <span data-ttu-id="d77e7-112">Importazione/esportazione di registrazioni</span><span class="sxs-lookup"><span data-stu-id="d77e7-112">Import/Export Registrations</span></span>
* <span data-ttu-id="d77e7-113">Invii regolari</span><span class="sxs-lookup"><span data-stu-id="d77e7-113">Regular Sends</span></span>
* <span data-ttu-id="d77e7-114">Invii pianificati</span><span class="sxs-lookup"><span data-stu-id="d77e7-114">Scheduled Sends</span></span>
* <span data-ttu-id="d77e7-115">Operazioni asincrone tramite Java NIO</span><span class="sxs-lookup"><span data-stu-id="d77e7-115">Async operations via Java NIO</span></span>
* <span data-ttu-id="d77e7-116">Piattaforme supportate: APNS (iOS), GCM (Android), WNS (app di Windows Store), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android senza servizi Google)</span><span class="sxs-lookup"><span data-stu-id="d77e7-116">Supported platforms: APNS (iOS), GCM (Android), WNS (Windows Store apps), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android without Google services)</span></span> 

## <a name="sdk-usage"></a><span data-ttu-id="d77e7-117">Uso dell'SDK</span><span class="sxs-lookup"><span data-stu-id="d77e7-117">SDK Usage</span></span>
### <a name="compile-and-build"></a><span data-ttu-id="d77e7-118">Compilazione e creazione</span><span class="sxs-lookup"><span data-stu-id="d77e7-118">Compile and build</span></span>
<span data-ttu-id="d77e7-119">Usare [Maven]</span><span class="sxs-lookup"><span data-stu-id="d77e7-119">Use [Maven]</span></span>

<span data-ttu-id="d77e7-120">Per creare:</span><span class="sxs-lookup"><span data-stu-id="d77e7-120">To build:</span></span>

    mvn package

## <a name="code"></a><span data-ttu-id="d77e7-121">Codice</span><span class="sxs-lookup"><span data-stu-id="d77e7-121">Code</span></span>
### <a name="notification-hub-cruds"></a><span data-ttu-id="d77e7-122">CRUD di Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="d77e7-122">Notification Hub CRUDs</span></span>
<span data-ttu-id="d77e7-123">**Creare un oggetto NamespaceManager:**</span><span class="sxs-lookup"><span data-stu-id="d77e7-123">**Create a NamespaceManager:**</span></span>

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

<span data-ttu-id="d77e7-124">**Creare un hub di notifica:**</span><span class="sxs-lookup"><span data-stu-id="d77e7-124">**Create Notification Hub:**</span></span>

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 <span data-ttu-id="d77e7-125">OPPURE</span><span class="sxs-lookup"><span data-stu-id="d77e7-125">OR</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="d77e7-126">**Ottenere un hub di notifica:**</span><span class="sxs-lookup"><span data-stu-id="d77e7-126">**Get Notification Hub:**</span></span>

    hub = namespaceManager.getNotificationHub("hubname");

<span data-ttu-id="d77e7-127">**Aggiornare un hub di notifica:**</span><span class="sxs-lookup"><span data-stu-id="d77e7-127">**Update Notification Hub:**</span></span>

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

<span data-ttu-id="d77e7-128">**Eliminare un hub di notifica:**</span><span class="sxs-lookup"><span data-stu-id="d77e7-128">**Delete Notification Hub:**</span></span>

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a><span data-ttu-id="d77e7-129">CRUD di registrazione</span><span class="sxs-lookup"><span data-stu-id="d77e7-129">Registration CRUDs</span></span>
<span data-ttu-id="d77e7-130">**Creare un client di Hub di notifica:**</span><span class="sxs-lookup"><span data-stu-id="d77e7-130">**Create a Notification Hub client:**</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="d77e7-131">**Creare una registrazione per Windows:**</span><span class="sxs-lookup"><span data-stu-id="d77e7-131">**Create Windows registration:**</span></span>

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

<span data-ttu-id="d77e7-132">**Creare una registrazione per iOS:**</span><span class="sxs-lookup"><span data-stu-id="d77e7-132">**Create iOS registration:**</span></span>

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

<span data-ttu-id="d77e7-133">Analogamente, è possibile creare registrazioni per Android (GCM), Windows Phone (MPNS) e Kindle Fire (ADM).</span><span class="sxs-lookup"><span data-stu-id="d77e7-133">Similarly you can create registrations for Android (GCM), Windows Phone (MPNS), and Kindle Fire (ADM).</span></span>

<span data-ttu-id="d77e7-134">**Creare registrazioni modello:**</span><span class="sxs-lookup"><span data-stu-id="d77e7-134">**Create template registrations:**</span></span>

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

<span data-ttu-id="d77e7-135">**Creare registrazioni usando il modello create registrationid + upsert**</span><span class="sxs-lookup"><span data-stu-id="d77e7-135">**Create registrations using create registrationid + upsert pattern**</span></span>

<span data-ttu-id="d77e7-136">Rimuove i duplicati causati dalle risposte perse se gli ID di registrazione sono stati archiviati nel dispositivo:</span><span class="sxs-lookup"><span data-stu-id="d77e7-136">Removes duplicates due to any lost responses if storing registration ids on the device:</span></span>

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

<span data-ttu-id="d77e7-137">**Aggiornare registrazioni:**</span><span class="sxs-lookup"><span data-stu-id="d77e7-137">**Update registrations:**</span></span>

    hub.updateRegistration(reg);

<span data-ttu-id="d77e7-138">**Eliminare registrazioni:**</span><span class="sxs-lookup"><span data-stu-id="d77e7-138">**Delete registrations:**</span></span>

    hub.deleteRegistration(regid);

<span data-ttu-id="d77e7-139">**Effettuare query di registrazioni:**</span><span class="sxs-lookup"><span data-stu-id="d77e7-139">**Query registrations:**</span></span>

* <span data-ttu-id="d77e7-140">**Ottenere una singola registrazione:**</span><span class="sxs-lookup"><span data-stu-id="d77e7-140">**Get single registration:**</span></span>
  
    <span data-ttu-id="d77e7-141">hub.getRegistration(regid);</span><span class="sxs-lookup"><span data-stu-id="d77e7-141">hub.getRegistration(regid);</span></span>
* <span data-ttu-id="d77e7-142">**Ottenere tutte le registrazioni nell'hub:**</span><span class="sxs-lookup"><span data-stu-id="d77e7-142">**Get all registrations in hub:**</span></span>
  
    <span data-ttu-id="d77e7-143">hub.getRegistrations();</span><span class="sxs-lookup"><span data-stu-id="d77e7-143">hub.getRegistrations();</span></span>
* <span data-ttu-id="d77e7-144">**Ottenere registrazioni con tag:**</span><span class="sxs-lookup"><span data-stu-id="d77e7-144">**Get registrations with tag:**</span></span>
  
    <span data-ttu-id="d77e7-145">hub.getRegistrationsByTag("myTag");</span><span class="sxs-lookup"><span data-stu-id="d77e7-145">hub.getRegistrationsByTag("myTag");</span></span>
* <span data-ttu-id="d77e7-146">**Ottenere registrazioni per canale:**</span><span class="sxs-lookup"><span data-stu-id="d77e7-146">**Get registrations by channel:**</span></span>
  
    <span data-ttu-id="d77e7-147">hub.getRegistrationsByChannel("devicetoken");</span><span class="sxs-lookup"><span data-stu-id="d77e7-147">hub.getRegistrationsByChannel("devicetoken");</span></span>

<span data-ttu-id="d77e7-148">Tutte le query di raccolta supportano i token $top e di continuazione.</span><span class="sxs-lookup"><span data-stu-id="d77e7-148">All collection queries support $top and continuation tokens.</span></span>

### <a name="installation-api-usage"></a><span data-ttu-id="d77e7-149">Uso dell'API di installazione</span><span class="sxs-lookup"><span data-stu-id="d77e7-149">Installation API usage</span></span>
<span data-ttu-id="d77e7-150">L'API di installazione rappresenta un meccanismo alternativo per la gestione delle registrazioni.</span><span class="sxs-lookup"><span data-stu-id="d77e7-150">Installation API is an alternative mechanism for registration management.</span></span> <span data-ttu-id="d77e7-151">Il mantenimento di più registrazioni non è semplice e può facilmente essere eseguito in maniera errata o inefficace, pertanto ora è possibile usare un SINGOLO oggetto di installazione.</span><span class="sxs-lookup"><span data-stu-id="d77e7-151">Instead of maintaining multiple registrations which is not trivial and may be easily done wrongly or inefficiently, it is now possible to use a SINGLE Installation object.</span></span> <span data-ttu-id="d77e7-152">L'installazione contiene tutti gli elementi necessari: il canale push (token del dispositivo), tag, modelli, riquadri secondari (per WNS e APN).</span><span class="sxs-lookup"><span data-stu-id="d77e7-152">Installation contains everything you need: push channel (device token), tags, templates, secondary tiles (for WNS and APNS).</span></span> <span data-ttu-id="d77e7-153">Non è più necessario chiamare il servizio per ottenere l'Id. È sufficiente generare un GUID o qualsiasi altro identificatore, mantenerlo nel dispositivo e inviarlo al back-end con il canale push (token del dispositivo).</span><span class="sxs-lookup"><span data-stu-id="d77e7-153">You don't need to call the service to get Id anymore - just generate GUID or any other identifier, keep it on device and send to your backend together with push channel (device token).</span></span> <span data-ttu-id="d77e7-154">Nel back-end, effettuare una singola chiamata: CreateOrUpdateInstallation, del tutto idempotente, per cui se necessario è possibile ritentare.</span><span class="sxs-lookup"><span data-stu-id="d77e7-154">On the backend you should only do a single call: CreateOrUpdateInstallation, it is fully idempotent, so feel free to retry if needed.</span></span>

<span data-ttu-id="d77e7-155">Un esempio per Amazon Kindle Fire è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="d77e7-155">As example for Amazon Kindle Fire it looks like this:</span></span>

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="d77e7-156">Per aggiornarlo:</span><span class="sxs-lookup"><span data-stu-id="d77e7-156">If you want to update it:</span></span> 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="d77e7-157">Per scenari avanzati è possibile usare la funzionalità di aggiornamento parziale, che consente di modificare solo determinate proprietà dell'oggetto di installazione.</span><span class="sxs-lookup"><span data-stu-id="d77e7-157">For advanced scenarios we have partial update capability which allows to modify only particular properties of the installation object.</span></span> <span data-ttu-id="d77e7-158">L'aggiornamento parziale è essenzialmente un subset di operazioni Patch JSON che è possibile eseguire in un oggetto di installazione.</span><span class="sxs-lookup"><span data-stu-id="d77e7-158">Basically partial update is subset of JSON Patch operations you can run against Installation object.</span></span>

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

<span data-ttu-id="d77e7-159">Eliminare l'installazione:</span><span class="sxs-lookup"><span data-stu-id="d77e7-159">Delete Installation:</span></span>

    hub.deleteInstallation(installation.getInstallationId());

<span data-ttu-id="d77e7-160">Le operazioni CreateOrUpdate, Patch e Delete saranno coerenti con l'operazione Get.</span><span class="sxs-lookup"><span data-stu-id="d77e7-160">CreateOrUpdate, Patch and Delete are eventually consistent with Get.</span></span> <span data-ttu-id="d77e7-161">L'operazione richiesta passa alla coda di sistema durante la chiamata e verrà eseguita in background.</span><span class="sxs-lookup"><span data-stu-id="d77e7-161">Your requested operation just goes to the system queue during the call and will be executed in background.</span></span> <span data-ttu-id="d77e7-162">Si noti che l'operazione Get non è progettata per lo scenario di runtime principale, ma solo per il debug e la risoluzione dei problemi ed è strettamente limitata dal servizio.</span><span class="sxs-lookup"><span data-stu-id="d77e7-162">Note that Get is not designed for main runtime scenario but just for debug and troubleshooting purposes, it is tightly throttled by the service.</span></span>

<span data-ttu-id="d77e7-163">Il flusso di invio per le installazioni è identico a quello delle registrazioni.</span><span class="sxs-lookup"><span data-stu-id="d77e7-163">Send flow for Installations is the same as for Registrations.</span></span> <span data-ttu-id="d77e7-164">È stata introdotta un'opzione per indirizzare la notifica all'installazione specifica: per farlo, usare il tag "InstallationId: {desired-id}".</span><span class="sxs-lookup"><span data-stu-id="d77e7-164">We've just introduced an option to target notification to the particular Installation - just use tag "InstallationId:{desired-id}".</span></span> <span data-ttu-id="d77e7-165">Nel caso riportato sopra l'aspetto dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="d77e7-165">For case above it would look like this:</span></span>

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

<span data-ttu-id="d77e7-166">Per uno dei diversi modelli:</span><span class="sxs-lookup"><span data-stu-id="d77e7-166">For one of several templates:</span></span>

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a><span data-ttu-id="d77e7-167">Pianificare le notifiche (disponibile per il livello STANDARD)</span><span class="sxs-lookup"><span data-stu-id="d77e7-167">Schedule Notifications (available for STANDARD Tier)</span></span>
<span data-ttu-id="d77e7-168">Si tratta di un invio normale ma con un parametro aggiuntivo, scheduledTime, che indica quando deve essere recapitata la notifica.</span><span class="sxs-lookup"><span data-stu-id="d77e7-168">The same as regular send but with one additional parameter - scheduledTime which says when notification should be delivered.</span></span> <span data-ttu-id="d77e7-169">Il servizio accetta qualsiasi data e ora da 5 minuti a sette giorni a partire dalla data e ora correnti.</span><span class="sxs-lookup"><span data-stu-id="d77e7-169">Service accepts any point of time between now + 5 minutes and now + 7 days.</span></span>

<span data-ttu-id="d77e7-170">**Pianificare una notifica nativa di Windows:**</span><span class="sxs-lookup"><span data-stu-id="d77e7-170">**Schedule a Windows native notification:**</span></span>

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a><span data-ttu-id="d77e7-171">Importazione/esportazione (disponibile per il livello STANDARD)</span><span class="sxs-lookup"><span data-stu-id="d77e7-171">Import/Export (available for STANDARD Tier)</span></span>
<span data-ttu-id="d77e7-172">Talvolta è necessario eseguire un'operazione di massa nelle registrazioni.</span><span class="sxs-lookup"><span data-stu-id="d77e7-172">Sometimes it is required to perform bulk operation against registrations.</span></span> <span data-ttu-id="d77e7-173">In genere si tratta dell'integrazione con un altro sistema o di una correzione di grandi dimensioni, ad esempio per l'aggiornamento di tag.</span><span class="sxs-lookup"><span data-stu-id="d77e7-173">Usually it is for integration with another system or just a massive fix to say update the tags.</span></span> <span data-ttu-id="d77e7-174">Se si ha a che fare con migliaia di registrazioni, non è consigliabile usare il flusso Get/Update.</span><span class="sxs-lookup"><span data-stu-id="d77e7-174">It is strongly not recommended to use Get/Update flow if we are talking about thousands of registrations.</span></span> <span data-ttu-id="d77e7-175">La soluzione appropriata per tale scenario è la funzionalità di importazione/esportazione.</span><span class="sxs-lookup"><span data-stu-id="d77e7-175">Import/Export capability is designed to cover the scenario.</span></span> <span data-ttu-id="d77e7-176">Essenzialmente è necessario fornire un accesso a un contenitore BLOB dell'account di archiviazione come origine dei dati in ingresso e come percorso per l'output.</span><span class="sxs-lookup"><span data-stu-id="d77e7-176">Basically you provide an access to some blob container under your storage account as a source of incoming data and location for output.</span></span>

<span data-ttu-id="d77e7-177">**Inviare il processo di esportazione:**</span><span class="sxs-lookup"><span data-stu-id="d77e7-177">**Submit export job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


<span data-ttu-id="d77e7-178">**Inviare il processo di importazione:**</span><span class="sxs-lookup"><span data-stu-id="d77e7-178">**Submit import job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

<span data-ttu-id="d77e7-179">**Attendere fino al completamento del processo:**</span><span class="sxs-lookup"><span data-stu-id="d77e7-179">**Wait until job is done:**</span></span>

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

<span data-ttu-id="d77e7-180">**Ottenere tutti i processi:**</span><span class="sxs-lookup"><span data-stu-id="d77e7-180">**Get all jobs:**</span></span>

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

<span data-ttu-id="d77e7-181">**URI con firma SAS** : l'URL di un file BLOB o di un contenitore BLOB con un insieme di parametri come le autorizzazioni e l'ora di scadenza e con la firma di tutti questi elementi effettuata usando la chiave della firma di accesso condiviso dell'account.</span><span class="sxs-lookup"><span data-stu-id="d77e7-181">**URI with SAS signature:** This is the URL of some blob file or blob container plus set of parameters like permissions and expiration time plus signature of all these things made using account's SAS key.</span></span> <span data-ttu-id="d77e7-182">L'SDK per Java di Archiviazione di Azure dispone di funzionalità avanzate, compresa la creazione di tale tipo di URI.</span><span class="sxs-lookup"><span data-stu-id="d77e7-182">Azure Storage Java SDK has rich capabilities including creation of such kind of URIs.</span></span> <span data-ttu-id="d77e7-183">In alternativa è possibile esaminare la classe di test ImportExportE2E (dal percorso Github) che include un'implementazione molto semplice e compatta dell'algoritmo di firma.</span><span class="sxs-lookup"><span data-stu-id="d77e7-183">As simple alternative you can take a look at ImportExportE2E test class (from the github location) which has very basic and compact implementation of signing algorithm.</span></span>

### <a name="send-notifications"></a><span data-ttu-id="d77e7-184">Inviare notifiche</span><span class="sxs-lookup"><span data-stu-id="d77e7-184">Send Notifications</span></span>
<span data-ttu-id="d77e7-185">L'oggetto notifica è semplicemente un corpo con intestazioni ed esistono alcuni metodi di utilità che consentono la creazione di notifiche modello e notifiche native.</span><span class="sxs-lookup"><span data-stu-id="d77e7-185">The Notification object is simply a body with headers, some utility methods help in building the native and template notifications objects.</span></span>

* <span data-ttu-id="d77e7-186">**Windows Store e Windows Phone 8.1 (non Silverlight)**</span><span class="sxs-lookup"><span data-stu-id="d77e7-186">**Windows Store and Windows Phone 8.1 (non-Silverlight)**</span></span>
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="d77e7-187">**iOS**</span><span class="sxs-lookup"><span data-stu-id="d77e7-187">**iOS**</span></span>
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* <span data-ttu-id="d77e7-188">**Android**</span><span class="sxs-lookup"><span data-stu-id="d77e7-188">**Android**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="d77e7-189">**Windows Phone 8.0 e 8.1 Silverlight**</span><span class="sxs-lookup"><span data-stu-id="d77e7-189">**Windows Phone 8.0 and 8.1 Silverlight**</span></span>
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="d77e7-190">**Kindle Fire**</span><span class="sxs-lookup"><span data-stu-id="d77e7-190">**Kindle Fire**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="d77e7-191">**Inviare a tag**</span><span class="sxs-lookup"><span data-stu-id="d77e7-191">**Send to Tags**</span></span>
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* <span data-ttu-id="d77e7-192">**Inviare a espressione tag**</span><span class="sxs-lookup"><span data-stu-id="d77e7-192">**Send to tag expression**</span></span>       
  
        hub.sendNotification(n, "foo && ! bar");
* <span data-ttu-id="d77e7-193">**Inviare una notifica modello**</span><span class="sxs-lookup"><span data-stu-id="d77e7-193">**Send template notification**</span></span>
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

<span data-ttu-id="d77e7-194">Quando si esegue il codice Java, dovrebbe essere visualizzata una notifica sul dispositivo di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d77e7-194">Running your Java code should now produce a notification appearing on your target device.</span></span>

## <span data-ttu-id="d77e7-195"><a name="next-steps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d77e7-195"><a name="next-steps"></a>Next Steps</span></span>
<span data-ttu-id="d77e7-196">In questo argomento è stato illustrato come creare un semplice client REST Java per Hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="d77e7-196">In this topic we showed how to create a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="d77e7-197">A questo punto è possibile:</span><span class="sxs-lookup"><span data-stu-id="d77e7-197">From here you can:</span></span>

* <span data-ttu-id="d77e7-198">Scaricare la versione completa di [SDK per Java]contenente l'intero codice SDK.</span><span class="sxs-lookup"><span data-stu-id="d77e7-198">Download the full [Java SDK], which contains the entire SDK code.</span></span> 
* <span data-ttu-id="d77e7-199">Consultare gli esempi:</span><span class="sxs-lookup"><span data-stu-id="d77e7-199">Play with the samples:</span></span>
  * <span data-ttu-id="d77e7-200">[Introduzione ad Hub di notifica]</span><span class="sxs-lookup"><span data-stu-id="d77e7-200">[Get Started with Notification Hubs]</span></span>
  * <span data-ttu-id="d77e7-201">[Inviare le ultime notizie]</span><span class="sxs-lookup"><span data-stu-id="d77e7-201">[Send breaking news]</span></span>
  * <span data-ttu-id="d77e7-202">[Inviare le ultime notizie localizzate]</span><span class="sxs-lookup"><span data-stu-id="d77e7-202">[Send localized breaking news]</span></span>
  * <span data-ttu-id="d77e7-203">[Inviare notifiche agli utenti autenticati]</span><span class="sxs-lookup"><span data-stu-id="d77e7-203">[Send notifications to authenticated users]</span></span>
  * <span data-ttu-id="d77e7-204">[Inviare notifiche multipiattaforma agli utenti autenticati]</span><span class="sxs-lookup"><span data-stu-id="d77e7-204">[Send cross-platform notifications to authenticated users]</span></span>

<span data-ttu-id="d77e7-205">[SDK per Java]: https://github.com/Azure/azure-notificationhubs-java-backend</span><span class="sxs-lookup"><span data-stu-id="d77e7-205">[Java SDK]: https://github.com/Azure/azure-notificationhubs-java-backend</span></span>
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
<span data-ttu-id="d77e7-206">[Introduzione ad Hub di notifica]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/</span><span class="sxs-lookup"><span data-stu-id="d77e7-206">[Get Started with Notification Hubs]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/</span></span>
<span data-ttu-id="d77e7-207">[Inviare le ultime notizie]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/</span><span class="sxs-lookup"><span data-stu-id="d77e7-207">[Send breaking news]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/</span></span>
<span data-ttu-id="d77e7-208">[Inviare le ultime notizie localizzate]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/</span><span class="sxs-lookup"><span data-stu-id="d77e7-208">[Send localized breaking news]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/</span></span>
<span data-ttu-id="d77e7-209">[Inviare notifiche agli utenti autenticati]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/</span><span class="sxs-lookup"><span data-stu-id="d77e7-209">[Send notifications to authenticated users]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/</span></span>
<span data-ttu-id="d77e7-210">[Inviare notifiche multipiattaforma agli utenti autenticati]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/</span><span class="sxs-lookup"><span data-stu-id="d77e7-210">[Send cross-platform notifications to authenticated users]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/</span></span>
<span data-ttu-id="d77e7-211">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="d77e7-211">[Maven]: http://maven.apache.org/</span></span>

