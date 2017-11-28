---
title: aaaHow toouse gli hub di notifica con Java
description: Informazioni su come toouse gli hub di notifica di Azure da un linguaggio back-end.
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
ms.openlocfilehash: afcf305b1acd9ee28ee4889040ece59d9399d29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-java"></a><span data-ttu-id="50c2d-103">Come toouse gli hub di notifica da Java</span><span class="sxs-lookup"><span data-stu-id="50c2d-103">How toouse Notification Hubs from Java</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="50c2d-104">In questo argomento descrive le funzionalità principali di hello di ufficiale hello nuovo completamente supportata SDK per Java Hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="50c2d-104">This topic describes hello key features of hello new fully supported official Azure Notification Hub Java SDK.</span></span> <span data-ttu-id="50c2d-105">Si tratta di un progetto open source ed è possibile visualizzare l'intero codice SDK hello in [SDK per Java].</span><span class="sxs-lookup"><span data-stu-id="50c2d-105">This is an open source project and you can view hello entire SDK code at [Java SDK].</span></span> 

<span data-ttu-id="50c2d-106">In generale, è possibile accedere tutte le funzionalità di hub di notifica da un server back-end utilizzabile come Java, PHP, Python o Ruby utilizzando l'interfaccia REST di Hub di notifica di hello come descritto nell'argomento MSDN hello [API REST degli hub di notifica](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="50c2d-106">In general, you can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span> <span data-ttu-id="50c2d-107">L'SDK per Java fornisce un semplice wrapper per le interfacce REST in Java.</span><span class="sxs-lookup"><span data-stu-id="50c2d-107">This Java SDK provides a thin wrapper over these REST interfaces in Java.</span></span> 

<span data-ttu-id="50c2d-108">Hello SDK supporta attualmente:</span><span class="sxs-lookup"><span data-stu-id="50c2d-108">hello SDK supports currently:</span></span>

* <span data-ttu-id="50c2d-109">CRUD in Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="50c2d-109">CRUD on Notification Hubs</span></span> 
* <span data-ttu-id="50c2d-110">CRUD in Registrazioni</span><span class="sxs-lookup"><span data-stu-id="50c2d-110">CRUD on Registrations</span></span>
* <span data-ttu-id="50c2d-111">Gestione dell'installazione</span><span class="sxs-lookup"><span data-stu-id="50c2d-111">Installation Management</span></span>
* <span data-ttu-id="50c2d-112">Importazione/esportazione di registrazioni</span><span class="sxs-lookup"><span data-stu-id="50c2d-112">Import/Export Registrations</span></span>
* <span data-ttu-id="50c2d-113">Invii regolari</span><span class="sxs-lookup"><span data-stu-id="50c2d-113">Regular Sends</span></span>
* <span data-ttu-id="50c2d-114">Invii pianificati</span><span class="sxs-lookup"><span data-stu-id="50c2d-114">Scheduled Sends</span></span>
* <span data-ttu-id="50c2d-115">Operazioni asincrone tramite Java NIO</span><span class="sxs-lookup"><span data-stu-id="50c2d-115">Async operations via Java NIO</span></span>
* <span data-ttu-id="50c2d-116">Piattaforme supportate: APNS (iOS), GCM (Android), WNS (app di Windows Store), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android senza servizi Google)</span><span class="sxs-lookup"><span data-stu-id="50c2d-116">Supported platforms: APNS (iOS), GCM (Android), WNS (Windows Store apps), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android without Google services)</span></span> 

## <a name="sdk-usage"></a><span data-ttu-id="50c2d-117">Uso dell'SDK</span><span class="sxs-lookup"><span data-stu-id="50c2d-117">SDK Usage</span></span>
### <a name="compile-and-build"></a><span data-ttu-id="50c2d-118">Compilazione e creazione</span><span class="sxs-lookup"><span data-stu-id="50c2d-118">Compile and build</span></span>
<span data-ttu-id="50c2d-119">Usare [Maven]</span><span class="sxs-lookup"><span data-stu-id="50c2d-119">Use [Maven]</span></span>

<span data-ttu-id="50c2d-120">toobuild:</span><span class="sxs-lookup"><span data-stu-id="50c2d-120">toobuild:</span></span>

    mvn package

## <a name="code"></a><span data-ttu-id="50c2d-121">Codice</span><span class="sxs-lookup"><span data-stu-id="50c2d-121">Code</span></span>
### <a name="notification-hub-cruds"></a><span data-ttu-id="50c2d-122">CRUD di Hub di notifica</span><span class="sxs-lookup"><span data-stu-id="50c2d-122">Notification Hub CRUDs</span></span>
<span data-ttu-id="50c2d-123">**Creare un oggetto NamespaceManager:**</span><span class="sxs-lookup"><span data-stu-id="50c2d-123">**Create a NamespaceManager:**</span></span>

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

<span data-ttu-id="50c2d-124">**Creare un hub di notifica:**</span><span class="sxs-lookup"><span data-stu-id="50c2d-124">**Create Notification Hub:**</span></span>

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 <span data-ttu-id="50c2d-125">OPPURE</span><span class="sxs-lookup"><span data-stu-id="50c2d-125">OR</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="50c2d-126">**Ottenere un hub di notifica:**</span><span class="sxs-lookup"><span data-stu-id="50c2d-126">**Get Notification Hub:**</span></span>

    hub = namespaceManager.getNotificationHub("hubname");

<span data-ttu-id="50c2d-127">**Aggiornare un hub di notifica:**</span><span class="sxs-lookup"><span data-stu-id="50c2d-127">**Update Notification Hub:**</span></span>

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

<span data-ttu-id="50c2d-128">**Eliminare un hub di notifica:**</span><span class="sxs-lookup"><span data-stu-id="50c2d-128">**Delete Notification Hub:**</span></span>

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a><span data-ttu-id="50c2d-129">CRUD di registrazione</span><span class="sxs-lookup"><span data-stu-id="50c2d-129">Registration CRUDs</span></span>
<span data-ttu-id="50c2d-130">**Creare un client di Hub di notifica:**</span><span class="sxs-lookup"><span data-stu-id="50c2d-130">**Create a Notification Hub client:**</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="50c2d-131">**Creare una registrazione per Windows:**</span><span class="sxs-lookup"><span data-stu-id="50c2d-131">**Create Windows registration:**</span></span>

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

<span data-ttu-id="50c2d-132">**Creare una registrazione per iOS:**</span><span class="sxs-lookup"><span data-stu-id="50c2d-132">**Create iOS registration:**</span></span>

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

<span data-ttu-id="50c2d-133">Analogamente, è possibile creare registrazioni per Android (GCM), Windows Phone (MPNS) e Kindle Fire (ADM).</span><span class="sxs-lookup"><span data-stu-id="50c2d-133">Similarly you can create registrations for Android (GCM), Windows Phone (MPNS), and Kindle Fire (ADM).</span></span>

<span data-ttu-id="50c2d-134">**Creare registrazioni modello:**</span><span class="sxs-lookup"><span data-stu-id="50c2d-134">**Create template registrations:**</span></span>

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

<span data-ttu-id="50c2d-135">**Creare registrazioni usando il modello create registrationid + upsert**</span><span class="sxs-lookup"><span data-stu-id="50c2d-135">**Create registrations using create registrationid + upsert pattern**</span></span>

<span data-ttu-id="50c2d-136">Rimuove i duplicati a causa delle risposte tooany perdita se l'archiviazione degli ID di registrazione nel dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="50c2d-136">Removes duplicates due tooany lost responses if storing registration ids on hello device:</span></span>

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

<span data-ttu-id="50c2d-137">**Aggiornare registrazioni:**</span><span class="sxs-lookup"><span data-stu-id="50c2d-137">**Update registrations:**</span></span>

    hub.updateRegistration(reg);

<span data-ttu-id="50c2d-138">**Eliminare registrazioni:**</span><span class="sxs-lookup"><span data-stu-id="50c2d-138">**Delete registrations:**</span></span>

    hub.deleteRegistration(regid);

<span data-ttu-id="50c2d-139">**Effettuare query di registrazioni:**</span><span class="sxs-lookup"><span data-stu-id="50c2d-139">**Query registrations:**</span></span>

* <span data-ttu-id="50c2d-140">**Ottenere una singola registrazione:**</span><span class="sxs-lookup"><span data-stu-id="50c2d-140">**Get single registration:**</span></span>
  
    <span data-ttu-id="50c2d-141">hub.getRegistration(regid);</span><span class="sxs-lookup"><span data-stu-id="50c2d-141">hub.getRegistration(regid);</span></span>
* <span data-ttu-id="50c2d-142">**Ottenere tutte le registrazioni nell'hub:**</span><span class="sxs-lookup"><span data-stu-id="50c2d-142">**Get all registrations in hub:**</span></span>
  
    <span data-ttu-id="50c2d-143">hub.getRegistrations();</span><span class="sxs-lookup"><span data-stu-id="50c2d-143">hub.getRegistrations();</span></span>
* <span data-ttu-id="50c2d-144">**Ottenere registrazioni con tag:**</span><span class="sxs-lookup"><span data-stu-id="50c2d-144">**Get registrations with tag:**</span></span>
  
    <span data-ttu-id="50c2d-145">hub.getRegistrationsByTag("myTag");</span><span class="sxs-lookup"><span data-stu-id="50c2d-145">hub.getRegistrationsByTag("myTag");</span></span>
* <span data-ttu-id="50c2d-146">**Ottenere registrazioni per canale:**</span><span class="sxs-lookup"><span data-stu-id="50c2d-146">**Get registrations by channel:**</span></span>
  
    <span data-ttu-id="50c2d-147">hub.getRegistrationsByChannel("devicetoken");</span><span class="sxs-lookup"><span data-stu-id="50c2d-147">hub.getRegistrationsByChannel("devicetoken");</span></span>

<span data-ttu-id="50c2d-148">Tutte le query di raccolta supportano i token $top e di continuazione.</span><span class="sxs-lookup"><span data-stu-id="50c2d-148">All collection queries support $top and continuation tokens.</span></span>

### <a name="installation-api-usage"></a><span data-ttu-id="50c2d-149">Uso dell'API di installazione</span><span class="sxs-lookup"><span data-stu-id="50c2d-149">Installation API usage</span></span>
<span data-ttu-id="50c2d-150">L'API di installazione rappresenta un meccanismo alternativo per la gestione delle registrazioni.</span><span class="sxs-lookup"><span data-stu-id="50c2d-150">Installation API is an alternative mechanism for registration management.</span></span> <span data-ttu-id="50c2d-151">Anziché gestire più registrazioni che non è semplice e può essere eseguita facilmente in modo errato o uso inefficiente, è ora possibile toouse oggetto una singola installazione.</span><span class="sxs-lookup"><span data-stu-id="50c2d-151">Instead of maintaining multiple registrations which is not trivial and may be easily done wrongly or inefficiently, it is now possible toouse a SINGLE Installation object.</span></span> <span data-ttu-id="50c2d-152">L'installazione contiene tutti gli elementi necessari: il canale push (token del dispositivo), tag, modelli, riquadri secondari (per WNS e APN).</span><span class="sxs-lookup"><span data-stu-id="50c2d-152">Installation contains everything you need: push channel (device token), tags, templates, secondary tiles (for WNS and APNS).</span></span> <span data-ttu-id="50c2d-153">Non più necessario toocall hello servizio tooget Id - semplicemente generare GUID o qualsiasi altro identificatore, mantenerli nel dispositivo e inviano back-end tooyour insieme canale push (token del dispositivo).</span><span class="sxs-lookup"><span data-stu-id="50c2d-153">You don't need toocall hello service tooget Id anymore - just generate GUID or any other identifier, keep it on device and send tooyour backend together with push channel (device token).</span></span> <span data-ttu-id="50c2d-154">Nel back-end hello deve eseguire solo una singola chiamata:, quindi CreateOrUpdateInstallation, è completamente idempotente, è disponibile tooretry se necessario.</span><span class="sxs-lookup"><span data-stu-id="50c2d-154">On hello backend you should only do a single call: CreateOrUpdateInstallation, it is fully idempotent, so feel free tooretry if needed.</span></span>

<span data-ttu-id="50c2d-155">Un esempio per Amazon Kindle Fire è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="50c2d-155">As example for Amazon Kindle Fire it looks like this:</span></span>

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="50c2d-156">Se si desidera tooupdate è:</span><span class="sxs-lookup"><span data-stu-id="50c2d-156">If you want tooupdate it:</span></span> 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="50c2d-157">Per scenari avanzati si dispone di funzionalità di aggiornamento parziale che consente di toomodify solo determinate proprietà degli oggetti installazione hello.</span><span class="sxs-lookup"><span data-stu-id="50c2d-157">For advanced scenarios we have partial update capability which allows toomodify only particular properties of hello installation object.</span></span> <span data-ttu-id="50c2d-158">L'aggiornamento parziale è essenzialmente un subset di operazioni Patch JSON che è possibile eseguire in un oggetto di installazione.</span><span class="sxs-lookup"><span data-stu-id="50c2d-158">Basically partial update is subset of JSON Patch operations you can run against Installation object.</span></span>

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

<span data-ttu-id="50c2d-159">Eliminare l'installazione:</span><span class="sxs-lookup"><span data-stu-id="50c2d-159">Delete Installation:</span></span>

    hub.deleteInstallation(installation.getInstallationId());

<span data-ttu-id="50c2d-160">Le operazioni CreateOrUpdate, Patch e Delete saranno coerenti con l'operazione Get.</span><span class="sxs-lookup"><span data-stu-id="50c2d-160">CreateOrUpdate, Patch and Delete are eventually consistent with Get.</span></span> <span data-ttu-id="50c2d-161">L'operazione richiesta appena diventa toohello coda di sistema durante la chiamata di hello e verrà eseguito in background.</span><span class="sxs-lookup"><span data-stu-id="50c2d-161">Your requested operation just goes toohello system queue during hello call and will be executed in background.</span></span> <span data-ttu-id="50c2d-162">Si noti che Get non è progettato per uno scenario di runtime principale, ma solo per il debug e risoluzione dei problemi è strettamente limitato dal servizio hello.</span><span class="sxs-lookup"><span data-stu-id="50c2d-162">Note that Get is not designed for main runtime scenario but just for debug and troubleshooting purposes, it is tightly throttled by hello service.</span></span>

<span data-ttu-id="50c2d-163">Flusso di trasmissione per le installazioni è hello come per le registrazioni.</span><span class="sxs-lookup"><span data-stu-id="50c2d-163">Send flow for Installations is hello same as for Registrations.</span></span> <span data-ttu-id="50c2d-164">È stato introdotto solo toohello di notifica tootarget un'opzione particolare installazione - utilizza solo tag "InstallationId: {desired-id}".</span><span class="sxs-lookup"><span data-stu-id="50c2d-164">We've just introduced an option tootarget notification toohello particular Installation - just use tag "InstallationId:{desired-id}".</span></span> <span data-ttu-id="50c2d-165">Nel caso riportato sopra l'aspetto dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="50c2d-165">For case above it would look like this:</span></span>

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

<span data-ttu-id="50c2d-166">Per uno dei diversi modelli:</span><span class="sxs-lookup"><span data-stu-id="50c2d-166">For one of several templates:</span></span>

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a><span data-ttu-id="50c2d-167">Pianificare le notifiche (disponibile per il livello STANDARD)</span><span class="sxs-lookup"><span data-stu-id="50c2d-167">Schedule Notifications (available for STANDARD Tier)</span></span>
<span data-ttu-id="50c2d-168">Hello stesso trasmissione regolare ma con un parametro aggiuntivo - scheduledTime che indica quando deve essere recapitata la notifica.</span><span class="sxs-lookup"><span data-stu-id="50c2d-168">hello same as regular send but with one additional parameter - scheduledTime which says when notification should be delivered.</span></span> <span data-ttu-id="50c2d-169">Il servizio accetta qualsiasi data e ora da 5 minuti a sette giorni a partire dalla data e ora correnti.</span><span class="sxs-lookup"><span data-stu-id="50c2d-169">Service accepts any point of time between now + 5 minutes and now + 7 days.</span></span>

<span data-ttu-id="50c2d-170">**Pianificare una notifica nativa di Windows:**</span><span class="sxs-lookup"><span data-stu-id="50c2d-170">**Schedule a Windows native notification:**</span></span>

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a><span data-ttu-id="50c2d-171">Importazione/esportazione (disponibile per il livello STANDARD)</span><span class="sxs-lookup"><span data-stu-id="50c2d-171">Import/Export (available for STANDARD Tier)</span></span>
<span data-ttu-id="50c2d-172">Talvolta è necessario tooperform massa contro le registrazioni.</span><span class="sxs-lookup"><span data-stu-id="50c2d-172">Sometimes it is required tooperform bulk operation against registrations.</span></span> <span data-ttu-id="50c2d-173">È in genere per l'integrazione con un altro sistema o solo una correzione massive toosay aggiornamento hello tag.</span><span class="sxs-lookup"><span data-stu-id="50c2d-173">Usually it is for integration with another system or just a massive fix toosay update hello tags.</span></span> <span data-ttu-id="50c2d-174">Non è fortemente consigliabile toouse flusso Get o l'aggiornamento se stiamo parlando migliaia di registrazioni.</span><span class="sxs-lookup"><span data-stu-id="50c2d-174">It is strongly not recommended toouse Get/Update flow if we are talking about thousands of registrations.</span></span> <span data-ttu-id="50c2d-175">Funzionalità di importazione/esportazione è uno scenario di hello toocover progettato.</span><span class="sxs-lookup"><span data-stu-id="50c2d-175">Import/Export capability is designed toocover hello scenario.</span></span> <span data-ttu-id="50c2d-176">Forniscono sostanzialmente un contenitore di blob toosome di accesso con l'account di archiviazione come origine di dati in arrivo e il percorso per l'output.</span><span class="sxs-lookup"><span data-stu-id="50c2d-176">Basically you provide an access toosome blob container under your storage account as a source of incoming data and location for output.</span></span>

<span data-ttu-id="50c2d-177">**Inviare il processo di esportazione:**</span><span class="sxs-lookup"><span data-stu-id="50c2d-177">**Submit export job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


<span data-ttu-id="50c2d-178">**Inviare il processo di importazione:**</span><span class="sxs-lookup"><span data-stu-id="50c2d-178">**Submit import job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

<span data-ttu-id="50c2d-179">**Attendere fino al completamento del processo:**</span><span class="sxs-lookup"><span data-stu-id="50c2d-179">**Wait until job is done:**</span></span>

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

<span data-ttu-id="50c2d-180">**Ottenere tutti i processi:**</span><span class="sxs-lookup"><span data-stu-id="50c2d-180">**Get all jobs:**</span></span>

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

<span data-ttu-id="50c2d-181">**URI con firma:** è hello URL di alcuni file blob o contenitore blob più set di parametri, quali le autorizzazioni e l'ora di scadenza e firma di tutte queste operazioni eseguite tramite la chiave di firma di accesso condiviso dell'account.</span><span class="sxs-lookup"><span data-stu-id="50c2d-181">**URI with SAS signature:** This is hello URL of some blob file or blob container plus set of parameters like permissions and expiration time plus signature of all these things made using account's SAS key.</span></span> <span data-ttu-id="50c2d-182">L'SDK per Java di Archiviazione di Azure dispone di funzionalità avanzate, compresa la creazione di tale tipo di URI.</span><span class="sxs-lookup"><span data-stu-id="50c2d-182">Azure Storage Java SDK has rich capabilities including creation of such kind of URIs.</span></span> <span data-ttu-id="50c2d-183">Come alternativa semplice è possibile dare un'occhiata ImportExportE2E classe di test (dal percorso di github hello) che è molto di base e compact implementazione dell'algoritmo di firma.</span><span class="sxs-lookup"><span data-stu-id="50c2d-183">As simple alternative you can take a look at ImportExportE2E test class (from hello github location) which has very basic and compact implementation of signing algorithm.</span></span>

### <a name="send-notifications"></a><span data-ttu-id="50c2d-184">Inviare notifiche</span><span class="sxs-lookup"><span data-stu-id="50c2d-184">Send Notifications</span></span>
<span data-ttu-id="50c2d-185">oggetto notifica Hello è semplicemente un corpo con intestazioni, alcuni metodi di utilità della Guida nella creazione di oggetti di notifiche hello nativo e modello.</span><span class="sxs-lookup"><span data-stu-id="50c2d-185">hello Notification object is simply a body with headers, some utility methods help in building hello native and template notifications objects.</span></span>

* <span data-ttu-id="50c2d-186">**Windows Store e Windows Phone 8.1 (non Silverlight)**</span><span class="sxs-lookup"><span data-stu-id="50c2d-186">**Windows Store and Windows Phone 8.1 (non-Silverlight)**</span></span>
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="50c2d-187">**iOS**</span><span class="sxs-lookup"><span data-stu-id="50c2d-187">**iOS**</span></span>
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* <span data-ttu-id="50c2d-188">**Android**</span><span class="sxs-lookup"><span data-stu-id="50c2d-188">**Android**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="50c2d-189">**Windows Phone 8.0 e 8.1 Silverlight**</span><span class="sxs-lookup"><span data-stu-id="50c2d-189">**Windows Phone 8.0 and 8.1 Silverlight**</span></span>
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="50c2d-190">**Kindle Fire**</span><span class="sxs-lookup"><span data-stu-id="50c2d-190">**Kindle Fire**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="50c2d-191">**Inviare tooTags**</span><span class="sxs-lookup"><span data-stu-id="50c2d-191">**Send tooTags**</span></span>
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* <span data-ttu-id="50c2d-192">**Inviare tootag espressione**</span><span class="sxs-lookup"><span data-stu-id="50c2d-192">**Send tootag expression**</span></span>       
  
        hub.sendNotification(n, "foo && ! bar");
* <span data-ttu-id="50c2d-193">**Inviare una notifica modello**</span><span class="sxs-lookup"><span data-stu-id="50c2d-193">**Send template notification**</span></span>
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

<span data-ttu-id="50c2d-194">Quando si esegue il codice Java, dovrebbe essere visualizzata una notifica sul dispositivo di destinazione.</span><span class="sxs-lookup"><span data-stu-id="50c2d-194">Running your Java code should now produce a notification appearing on your target device.</span></span>

## <span data-ttu-id="50c2d-195"><a name="next-steps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="50c2d-195"><a name="next-steps"></a>Next Steps</span></span>
<span data-ttu-id="50c2d-196">In questo argomento illustrato come toocreate un linguaggio semplice REST client per gli hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="50c2d-196">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="50c2d-197">A questo punto è possibile:</span><span class="sxs-lookup"><span data-stu-id="50c2d-197">From here you can:</span></span>

* <span data-ttu-id="50c2d-198">Scaricare hello completo [SDK per Java], che contiene tutto il codice SDK hello.</span><span class="sxs-lookup"><span data-stu-id="50c2d-198">Download hello full [Java SDK], which contains hello entire SDK code.</span></span> 
* <span data-ttu-id="50c2d-199">Provare a usare hello esempi:</span><span class="sxs-lookup"><span data-stu-id="50c2d-199">Play with hello samples:</span></span>
  * <span data-ttu-id="50c2d-200">[Introduzione ad Hub di notifica]</span><span class="sxs-lookup"><span data-stu-id="50c2d-200">[Get Started with Notification Hubs]</span></span>
  * <span data-ttu-id="50c2d-201">[Inviare le ultime notizie]</span><span class="sxs-lookup"><span data-stu-id="50c2d-201">[Send breaking news]</span></span>
  * <span data-ttu-id="50c2d-202">[Inviare le ultime notizie localizzate]</span><span class="sxs-lookup"><span data-stu-id="50c2d-202">[Send localized breaking news]</span></span>
  * <span data-ttu-id="50c2d-203">[Inviare notifiche agli utenti di tooauthenticated]</span><span class="sxs-lookup"><span data-stu-id="50c2d-203">[Send notifications tooauthenticated users]</span></span>
  * <span data-ttu-id="50c2d-204">[Inviare notifiche di multipiattaforma tooauthenticated utenti]</span><span class="sxs-lookup"><span data-stu-id="50c2d-204">[Send cross-platform notifications tooauthenticated users]</span></span>

[SDK per Java]: https://github.com/Azure/azure-notificationhubs-java-backend
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[Introduzione ad Hub di notifica]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/
[Inviare le ultime notizie]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/
[Inviare le ultime notizie localizzate]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/
[Inviare notifiche agli utenti di tooauthenticated]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/
[Inviare notifiche di multipiattaforma tooauthenticated utenti]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/
[Maven]: http://maven.apache.org/

