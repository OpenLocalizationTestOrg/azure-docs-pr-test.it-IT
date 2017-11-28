---
title: Integrazione di Phone Silverlight raggiungere SDK aaaWindows
description: Come tooIntegrate Azure Mobile Engagement raggiunge con App di Windows Phone Silverlight
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d3516a6b-db9f-4cdb-a475-4148edf81af1
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 09c8767216e11963c5c600755ab8d4d11cd92034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a><span data-ttu-id="b0ea4-103">Integrazione dell'SDK di Reach per Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="b0ea4-103">Windows Phone Silverlight Reach SDK Integration</span></span>
<span data-ttu-id="b0ea4-104">Attenersi alla procedura di integrazione hello descritta in hello [integrazione SDK di Windows Phone Silverlight Engagement](mobile-engagement-windows-phone-integrate-engagement.md) prima di seguire questa Guida.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-104">You must follow hello integration procedure described in hello [Windows Phone Silverlight Engagement SDK Integration](mobile-engagement-windows-phone-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a><span data-ttu-id="b0ea4-105">Incorporare hello Engagement Reach SDK nel progetto Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="b0ea4-105">Embed hello Engagement Reach SDK into your Windows Phone Silverlight project</span></span>
<span data-ttu-id="b0ea4-106">Non è un valore tooadd.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-106">You do not have anything tooadd.</span></span> <span data-ttu-id="b0ea4-107">`EngagementReach` sono già presenti nel progetto.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="b0ea4-108">È possibile personalizzare le immagini si trova in hello `Resources` cartella del progetto, in particolare hello marchio icona (tale impostazione predefinita toohello Engagement).</span><span class="sxs-lookup"><span data-stu-id="b0ea4-108">You can customize images located in hello `Resources` folder of your project, especially hello brand icon (that default toohello Engagement icon).</span></span>
> 
> 

## <a name="add-hello-capabilities"></a><span data-ttu-id="b0ea4-109">Aggiungere le funzionalità di hello</span><span class="sxs-lookup"><span data-stu-id="b0ea4-109">Add hello capabilities</span></span>
<span data-ttu-id="b0ea4-110">Hello Engagement Reach SDK richiede alcune funzionalità aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-110">hello Engagement Reach SDK needs some additional capabilities.</span></span>

<span data-ttu-id="b0ea4-111">Aprire il `WMAppManifest.xml` file e assicurarsi che vengono dichiarati tale hello seguenti funzionalità:</span><span class="sxs-lookup"><span data-stu-id="b0ea4-111">Open your `WMAppManifest.xml` file and be sure that hello following capabilities are declared:</span></span>

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

<span data-ttu-id="b0ea4-112">Hello prima di tutto è utilizzato da visualizzazione hello MPNS servizio tooallow hello della notifica di tipo avviso popup.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-112">hello first one is used by hello MPNS service tooallow hello display of toast notification.</span></span> <span data-ttu-id="b0ea4-113">Hello secondo è tooembed usato un'attività di browser in hello SDK.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-113">hello second one is used tooembed a browser task into hello SDK.</span></span>

<span data-ttu-id="b0ea4-114">Modifica hello `WMAppManifest.xml` file e aggiungere all'interno di hello `<Capabilities />` tag:</span><span class="sxs-lookup"><span data-stu-id="b0ea4-114">Edit hello `WMAppManifest.xml` file and add inside hello `<Capabilities />` tag :</span></span>

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a><span data-ttu-id="b0ea4-115">Abilitare hello servizio notifica Push Microsoft</span><span class="sxs-lookup"><span data-stu-id="b0ea4-115">Enable hello Microsoft Push Notification Service</span></span>
<span data-ttu-id="b0ea4-116">In hello toouse ordine **servizio notifica Push Microsoft** (definito MPNS) il `WMAppManifest.xml` file deve avere un `<App />` tag con un `Publisher` attributo impostato toohello nome del progetto.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-116">In order toouse hello **Microsoft Push Notification Service** (referred as MPNS) your `WMAppManifest.xml` file must have an `<App />` tag with a `Publisher` attribute set toohello name of your project.</span></span>

## <a name="initialize-hello-engagement-reach-sdk"></a><span data-ttu-id="b0ea4-117">Inizializzare hello Engagement Reach SDK</span><span class="sxs-lookup"><span data-stu-id="b0ea4-117">Initialize hello Engagement Reach SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="b0ea4-118">Configurazione di Engagement</span><span class="sxs-lookup"><span data-stu-id="b0ea4-118">Engagement configuration</span></span>
<span data-ttu-id="b0ea4-119">configurazione di Engagement Hello è centralizzata in hello `Resources\EngagementConfiguration.xml` file del progetto.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-119">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="b0ea4-120">Modificare questa configurazione di copertura toospecify file:</span><span class="sxs-lookup"><span data-stu-id="b0ea4-120">Edit this file toospecify reach configuration :</span></span>

* <span data-ttu-id="b0ea4-121">*Parametro facoltativo*, indicare se è attivato il push nativo hello (MPNS) o non è compreso tra `<enableNativePush>` e `</enableNativePush>` tag, (`true` per impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="b0ea4-121">*Optional*, indicate whether hello native push (MPNS) is activated or not between `<enableNativePush>` and `</enableNativePush>` tags, (`true` by default).</span></span>
* <span data-ttu-id="b0ea4-122">*Parametro facoltativo*, indicare il nome del canale di push hello tra hello `<channelName>` e `</channelName>` tag, forniscono hello stesso che l'applicazione può utilizzare o lasciare vuoto il campo attualmente.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-122">*Optional*, indicate hello name of hello push channel between `<channelName>` and `</channelName>` tags, provide hello same that your application may currently use or leave it empty.</span></span>

<span data-ttu-id="b0ea4-123">Se si desidera che in fase di esecuzione, invece, si può chiamare seguente hello toospecify metodo prima dell'inizializzazione dell'agente di Engagement hello:</span><span class="sxs-lookup"><span data-stu-id="b0ea4-123">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization :</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether hello native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide hello same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> <span data-ttu-id="b0ea4-124">È possibile specificare il nome di hello di hello MPNS push canale dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-124">You can specify hello name of hello MPNS push channel of your application.</span></span> <span data-ttu-id="b0ea4-125">Per impostazione predefinita, Engagement crea un nome in base a appId hello.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-125">By default, Engagement creates a name based on hello appId.</span></span> <span data-ttu-id="b0ea4-126">Non si dispone di alcuna necessità toospecify hello nome manualmente, tranne se si prevede di canale di push toouse hello di fuori di Engagement.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-126">You have no need toospecify hello name yourself, except if you plan toouse hello push channel outside of Engagement.</span></span>
> 
> 

### <a name="engagement-initialization"></a><span data-ttu-id="b0ea4-127">Inizializzazione di Engagement</span><span class="sxs-lookup"><span data-stu-id="b0ea4-127">Engagement initialization</span></span>
<span data-ttu-id="b0ea4-128">Modificare hello `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="b0ea4-128">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="b0ea4-129">Aggiungere tooyour `using` istruzioni:</span><span class="sxs-lookup"><span data-stu-id="b0ea4-129">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="b0ea4-130">Inserire `EngagementReach.Instance.Init` subito dopo `EngagementAgent.Instance.Init` in `Application_Launching`:</span><span class="sxs-lookup"><span data-stu-id="b0ea4-130">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in `Application_Launching` :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* <span data-ttu-id="b0ea4-131">Inserisci `EngagementReach.Instance.OnActivated` in hello `Application_Activated` metodo:</span><span class="sxs-lookup"><span data-stu-id="b0ea4-131">Insert `EngagementReach.Instance.OnActivated` in hello `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> <span data-ttu-id="b0ea4-132">Hello `EngagementReach.Instance.Init` viene eseguito in un thread dedicato.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-132">hello `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="b0ea4-133">Non è toodo è manualmente.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-133">You do not have toodo it yourself.</span></span>
> 
> 

## <a name="app-store-submission-considerations"></a><span data-ttu-id="b0ea4-134">Considerazioni sull'invio di notifiche di App Store</span><span class="sxs-lookup"><span data-stu-id="b0ea4-134">App store submission considerations</span></span>
<span data-ttu-id="b0ea4-135">Microsoft impone alcune regole quando si usano le notifiche push hello:</span><span class="sxs-lookup"><span data-stu-id="b0ea4-135">Microsoft imposes some rules when using hello push notifications:</span></span>

<span data-ttu-id="b0ea4-136">Da Microsoft hello [criteri di applicazione] documentazione, sezione 2.9:</span><span class="sxs-lookup"><span data-stu-id="b0ea4-136">From hello Microsoft [Application Policies] documentation, section 2.9:</span></span>

1) <span data-ttu-id="b0ea4-137">È necessario richiedere le notifiche push hello utente tooaccept tooreceive.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-137">You must ask hello user tooaccept tooreceive push notifications.</span></span> <span data-ttu-id="b0ea4-138">Nelle impostazioni, quindi aggiungere le notifiche push hello toodisable un modo.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-138">Then, in your settings, add a way toodisable hello push notifications.</span></span>

<span data-ttu-id="b0ea4-139">oggetto EngagementReach Hello fornisce due metodi toomanage hello opt-in/opt-out, `EnableNativePush()` e `DisableNativePush()`.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-139">hello EngagementReach object provides two methods toomanage hello opt-in/opt-out, `EnableNativePush()` and `DisableNativePush()`.</span></span> <span data-ttu-id="b0ea4-140">Potrebbe, ad esempio, creare un'opzione nelle impostazioni di hello con un elemento toggle di toodisable o abilitare MPNS.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-140">You could, for example, create an option in hello settings with a toggle toodisable or enable MPNS.</span></span>

<span data-ttu-id="b0ea4-141">È inoltre possibile decidere toodeactivate MPNS tramite la configurazione di Engagement hello\<windows-phone-sdk-reach-configurazione\>.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-141">You can also decide toodeactivate MPNS through hello Engagement configuration\<windows-phone-sdk-reach-configuration\>.</span></span>

> <span data-ttu-id="b0ea4-142">2.9.1) applicazione hello innanzitutto deve descrivere hello notifiche toobe fornito e **ottenere l'autorizzazione dell'utente hello (acconsentire esplicitamente)**, e **deve fornire un meccanismo tramite cui hello utente può rifiutare esplicitamente la ricezione le notifiche push**.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-142">2.9.1) hello application must first describe hello notifications toobe provided and **obtain hello user’s express permission (opt-in)**, and **must provide a mechanism through which hello user can opt out of receiving push notifications**.</span></span> <span data-ttu-id="b0ea4-143">Tutte le notifiche fornite tramite servizio notifica Push Microsoft hello devono essere coerenti con l'utente di toohello descrizione fornita hello e devono conformarsi a tutte applicabile [criteri di applicazione] [ Content Policies]e [requisiti aggiuntivi per i tipi di applicazione specifico].</span><span class="sxs-lookup"><span data-stu-id="b0ea4-143">All notifications provided using hello Microsoft Push Notification Service must be consistent with hello description provided toohello user and must comply with all applicable [Application Policies][Content Policies] and [Additional Requirements for Specific Application Types].</span></span>
> 
> 

2) <span data-ttu-id="b0ea4-144">Non fare un uso eccessivo delle notifiche push.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-144">You should not use too many push notifications.</span></span> <span data-ttu-id="b0ea4-145">Engagement gestisce le notifiche in modo automatico.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-145">Engagement will handle notifications for you.</span></span>

> <span data-ttu-id="b0ea4-146">2.9.2) applicazione hello e l'utilizzo del servizio notifica Push Microsoft hello deve essere non eccessivamente utilizzare capacità di rete o della larghezza di banda di servizio notifica Push Microsoft hello, o in caso contrario eccessivamente sovraccarica un Windows Phone o altro dispositivo di Microsoft o un servizio con un numero eccessivo push delle notifiche, come stabilito da Microsoft a propria discrezione e non deve compromettere o interferire con le reti di Microsoft Server o qualsiasi server di terze parti o reti connesse toohello servizio notifica Push Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-146">2.9.2) hello application and its use of hello Microsoft Push Notification Service must not excessively use network capacity or bandwidth of hello Microsoft Push Notification Service, or otherwise unduly burden a Windows Phone or other Microsoft device or service with excessive push notifications, as determined by Microsoft in its reasonable discretion, and must not harm or interfere with any Microsoft networks or servers or any third party servers or networks connected toohello Microsoft Push Notification Service.</span></span>
> 
> 

3) <span data-ttu-id="b0ea4-147">Non basarsi sulle informazioni di criticals toosend MPNS.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-147">Do not rely on MPNS toosend criticals information.</span></span> <span data-ttu-id="b0ea4-148">Engagement Usa MPNS, in modo da questa regola si applica anche per le campagne hello create all'interno di hello Engagement front-end.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-148">Engagement uses MPNS, so this rule also applies for hello campaigns created inside hello Engagement front-end.</span></span>

> <span data-ttu-id="b0ea4-149">2.9.3) hello servizio notifica Push Microsoft potrebbe non essere notifiche toosend utilizzati che vengono mission-critical o in caso contrario potrebbe incidere sulle questioni della priorità, inclusi, a condizione o dispositivo medico di limitazione le notifiche critiche tooa correlati.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-149">2.9.3) hello Microsoft Push Notification Service may not be used toosend notifications that are mission critical or otherwise could affect matters of life or death, including without limitation critical notifications related tooa medical device or condition.</span></span> <span data-ttu-id="b0ea4-150">MICROSOFT espressamente declina qualsiasi garanzia che hello uso di hello MICROSOFT PUSH NOTIFICATION servizio o recapito di MICROSOFT PUSH notifica servizio notifiche verrà essere senza interruzioni, errore disponibile, o in caso contrario garantito tooOCCUR ON A in tempo reale base.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-150">MICROSOFT EXPRESSLY DISCLAIMS ANY WARRANTIES THAT hello USE OF hello MICROSOFT PUSH NOTIFICATION SERVICE OR DELIVERY OF MICROSOFT PUSH NOTIFICATION SERVICE NOTIFICATIONS WILL BE UNINTERRUPTED, ERROR FREE, OR OTHERWISE GUARANTEED tooOCCUR ON A REAL-TIME BASIS.</span></span>
> 
> 

<span data-ttu-id="b0ea4-151">**È possibile garantire che l'applicazione passerà il processo di convalida hello se non si rispettano questi suggerimenti.**</span><span class="sxs-lookup"><span data-stu-id="b0ea4-151">**We cannot guarantee that your application will pass hello validation process if you do not respect these recommendations.**</span></span>

## <a name="handle-data-push-optional"></a><span data-ttu-id="b0ea4-152">Gestire il push di dati (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="b0ea4-152">Handle data push (optional)</span></span>
<span data-ttu-id="b0ea4-153">Se si desidera il push di dati applicazione toobe tooreceive in grado di raggiungere, è necessario tooimplement due eventi di classe EngagementReach hello:</span><span class="sxs-lookup"><span data-stu-id="b0ea4-153">If you want your application toobe able tooreceive Reach data pushes, you have tooimplement two events of hello EngagementReach class:</span></span>

    EngagementReach.Instance.DataPushStringReceived += (body) =>
    {
       Debug.WriteLine("String data push message received: " + body);
       return true;
    };

    EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
    {
       Debug.WriteLine("Base64 data push message received: " + encodedBody);
       // Do something useful with decodedBody like updating an image view
       return true;
    };

<span data-ttu-id="b0ea4-154">È possibile visualizzare il callback di hello di ogni metodo restituisce un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-154">You can see that hello callback of each method returns a boolean.</span></span> <span data-ttu-id="b0ea4-155">Engagement invia un feedback tooits back-end dopo l'invio di push di dati hello.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-155">Engagement sends a feedback tooits back-end after dispatching hello data push.</span></span> <span data-ttu-id="b0ea4-156">Se il callback di hello restituisce false, hello `exit` feedback verrà inviato.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-156">If hello callback returns false, hello `exit` feedback will be send.</span></span> <span data-ttu-id="b0ea4-157">In caso contrario, il feedback sarà `action`.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-157">Otherwise, it will be `action`.</span></span> <span data-ttu-id="b0ea4-158">Se il callback non è impostato per gli eventi di hello, hello `drop` commenti e suggerimenti verranno restituiti tooEngagement.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-158">If no callback is set for hello events, hello `drop` feedback will be returned tooEngagement.</span></span>

> [!WARNING]
> <span data-ttu-id="b0ea4-159">Engagement non è in grado di tooreceive feedback multipli per il push di dati.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-159">Engagement is not able tooreceive multiples feedbacks for a data push.</span></span> <span data-ttu-id="b0ea4-160">Se si intende tooset diversi gestori di un evento, tenere presente che il feedback hello corrisponderà toohello ultimo quello inviato.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-160">If you plan tooset several handlers on an event, be aware that hello feedback will correspond toohello last one sent.</span></span> <span data-ttu-id="b0ea4-161">In questo caso, è consigliabile tooalways restituisce hello stesso tooavoid valore determinato confusione commenti e suggerimenti su hello front-end.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-161">In this case, we recommend tooalways returns hello same value tooavoid having confusing feedback on hello front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="b0ea4-162">Personalizzare l'interfaccia utente (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="b0ea4-162">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="b0ea4-163">Primo passaggio</span><span class="sxs-lookup"><span data-stu-id="b0ea4-163">First step</span></span>
<span data-ttu-id="b0ea4-164">Abbiamo consentono di raggiungere hello toocustomize dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-164">We allow you toocustomize hello reach UI.</span></span>

<span data-ttu-id="b0ea4-165">toodo, è necessario toocreate una sottoclasse di hello `EngagementReachHandler` classe.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-165">toodo so, you have toocreate a subclass of hello `EngagementReachHandler` class.</span></span>

<span data-ttu-id="b0ea4-166">**Codice di esempio:**</span><span class="sxs-lookup"><span data-stu-id="b0ea4-166">**Sample Code :**</span></span>

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

<span data-ttu-id="b0ea4-167">Quindi, impostare il contenuto di hello di hello `EngagementReach.Instance.Handler` campo con l'oggetto personalizzato nel `App.xaml.cs` classe all'interno di hello `Application_Launching` metodo.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-167">Then, set hello content of hello `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within hello `Application_Launching` method.</span></span>

<span data-ttu-id="b0ea4-168">**Codice di esempio:**</span><span class="sxs-lookup"><span data-stu-id="b0ea4-168">**Sample Code :**</span></span>

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> <span data-ttu-id="b0ea4-169">Per impostazione predefinita, Engagement usa una specifica implementazione di `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-169">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span> <span data-ttu-id="b0ea4-170">Non è toocreate personalizzata, e se in tal caso, non è necessario toooverride ogni metodo.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-170">You don't have toocreate your own, and if you do so, you don't have toooverride every method.</span></span> <span data-ttu-id="b0ea4-171">comportamento predefinito di Hello è oggetto di base di tooselect hello Engagement.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-171">hello default behavior is tooselect hello Engagement base object.</span></span>
> 
> 

### <a name="layouts"></a><span data-ttu-id="b0ea4-172">Layout</span><span class="sxs-lookup"><span data-stu-id="b0ea4-172">Layouts</span></span>
<span data-ttu-id="b0ea4-173">Per impostazione predefinita, Reach utilizzerà hello incorporato di risorse di notifiche di hello DLL toodisplay hello e pagine.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-173">By default, Reach will use hello embedded resources of hello DLL toodisplay hello notifications and pages.</span></span>

<span data-ttu-id="b0ea4-174">Tuttavia, è possibile decidere toouse tooreflect proprie risorse il marchio in questi componenti.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-174">However, you can decide toouse your own resources tooreflect your brand in these components.</span></span>

<span data-ttu-id="b0ea4-175">È possibile eseguire l'override `EngagementReachHandler` metodi toouse di Engagement tootell la sottoclasse i layout:</span><span class="sxs-lookup"><span data-stu-id="b0ea4-175">You can override `EngagementReachHandler` methods in your subclass tootell Engagement toouse your layouts :</span></span>

<span data-ttu-id="b0ea4-176">**Codice di esempio:**</span><span class="sxs-lookup"><span data-stu-id="b0ea4-176">**Sample Code :**</span></span>

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetPollUri()
    {
       // return hello path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> <span data-ttu-id="b0ea4-177">Hello `CreateNotification` metodo può restituire null.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-177">hello `CreateNotification` method can return null.</span></span> <span data-ttu-id="b0ea4-178">non verrà visualizzata la notifica Hello e campagna di copertura hello verrà eliminata.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-178">hello notification won't be displayed and hello reach campaign will be dropped.</span></span>
> 
> 

<span data-ttu-id="b0ea4-179">toosimplify l'implementazione del layout, è inoltre possibile usare nostro xaml che può essere utilizzato come base per il codice.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-179">toosimplify your layout implementation, we also provide our own xaml which can serve as a basis for your code.</span></span> <span data-ttu-id="b0ea4-180">Si trovano nell'archivio di Engagement SDK hello (o src/reach /).</span><span class="sxs-lookup"><span data-stu-id="b0ea4-180">They are located in hello Engagement SDK archive (/src/reach/).</span></span>

> [!WARNING]
> <span data-ttu-id="b0ea4-181">origini di Hello fornito da Microsoft sono hello utilizziamo esatte stesse.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-181">hello sources that we provide are hello exact same ones that we use.</span></span> <span data-ttu-id="b0ea4-182">Pertanto, se si desidera toomodify li direttamente, non dimenticare dello spazio dei nomi di toochange hello e hello nome.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-182">So if you want toomodify them directly, don't forget toochange hello namespace and hello name.</span></span>
> 
> 

### <a name="notification-position"></a><span data-ttu-id="b0ea4-183">Posizione di notifica</span><span class="sxs-lookup"><span data-stu-id="b0ea4-183">Notification position</span></span>
<span data-ttu-id="b0ea4-184">Per impostazione predefinita, viene visualizzata una notifica di nell'applicazione in hello sul lato inferiore sinistro di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-184">By default, an in-app notification is displayed at hello bottom left side of hello application.</span></span> <span data-ttu-id="b0ea4-185">È possibile modificare questo comportamento eseguendo l'override di hello `GetNotificationPosition` metodo hello `EngagementReachHandler` oggetto.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-185">You can change this behavior by overriding hello `GetNotificationPosition` method of hello `EngagementReachHandler` object.</span></span>

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

<span data-ttu-id="b0ea4-186">Attualmente, è possibile scegliere tra hello `BOTTOM` (impostazione predefinita) e `TOP` posizioni.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-186">Currently, you can choose between hello `BOTTOM` (default) and `TOP` positions.</span></span>

### <a name="launch-message"></a><span data-ttu-id="b0ea4-187">Messaggio di avvio</span><span class="sxs-lookup"><span data-stu-id="b0ea4-187">Launch message</span></span>
<span data-ttu-id="b0ea4-188">Quando un utente fa clic su una notifica di sistema (un tipo di avviso popup), avvia Engagement hello app, carico hello contenuto di hello il push dei messaggi e visualizzare la pagina hello per hello corrispondente della campagna.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-188">When a user clicks on a system notification (a toast), Engagement launches hello app, load hello content of hello push messages, and display hello page for hello corresponding campaign.</span></span>

<span data-ttu-id="b0ea4-189">Si verifica un ritardo tra l'avvio di hello del display di applicazione e hello hello della pagina hello (a seconda della velocità di hello della rete).</span><span class="sxs-lookup"><span data-stu-id="b0ea4-189">There is a delay between hello launch of hello application and hello display of hello page (depending on hello speed of your network).</span></span>

<span data-ttu-id="b0ea4-190">utente di toohello tooindicate che si sta caricando, è necessario fornire un informazioni visive, ad esempio una barra di stato o un indicatore di stato.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-190">tooindicate toohello user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="b0ea4-191">Engagement non è in grado di gestire questa situazione, ma fornisce alcuni gestori.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-191">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="b0ea4-192">tooimplement hello callback, eseguire:</span><span class="sxs-lookup"><span data-stu-id="b0ea4-192">tooimplement hello callback, do:</span></span>

    /* hello application has launched and hello content is loading.
     * You should display an indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

    /* hello application has finished loading hello content and hello page
     * is about toobe displayed.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

    /* hello content has been loaded, but an error has occurred.
     * You can provide an information toohello user.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

<span data-ttu-id="b0ea4-193">È possibile impostare il callback di hello nel `Application_Launching` metodo i `App.xaml.cs` file, preferibilmente prima hello `EngagementReach.Instance.Init()` chiamare.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-193">You can set hello callback in your `Application_Launching` method of your `App.xaml.cs` file, preferably before hello `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="b0ea4-194">Ogni gestore viene chiamato dal Thread UI hello.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-194">Each handler is called by hello UI Thread.</span></span> <span data-ttu-id="b0ea4-195">Non si dispone tooworry quando si utilizza un MessageBox o qualcosa correlate all'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="b0ea4-195">You do not have tooworry when using a MessageBox or something UI-related.</span></span>
> 
> 

[criteri di applicazione]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[requisiti aggiuntivi per i tipi di applicazione specifico]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx

