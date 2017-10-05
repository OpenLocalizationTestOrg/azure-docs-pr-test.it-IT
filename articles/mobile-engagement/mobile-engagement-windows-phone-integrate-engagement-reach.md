---
title: Integrazione dell'SDK di Reach per Windows Phone Silverlight
description: Come integrare il servizio Reach di Azure Mobile Engagement con le app per Windows Phone Silverlight
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
ms.openlocfilehash: 0738f33df94d14fbb393bfaaf09e94c6560213cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a><span data-ttu-id="573c6-103">Integrazione dell'SDK di Reach per Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="573c6-103">Windows Phone Silverlight Reach SDK Integration</span></span>
<span data-ttu-id="573c6-104">Prima di usare questa guida, è necessario eseguire la procedura di integrazione descritta nel documento [Integrazione di Mobile Engagement SDK per Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) .</span><span class="sxs-lookup"><span data-stu-id="573c6-104">You must follow the integration procedure described in the [Windows Phone Silverlight Engagement SDK Integration](mobile-engagement-windows-phone-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-the-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a><span data-ttu-id="573c6-105">Incorporare l'SDK del servizio Reach di Engagement nel progetto Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="573c6-105">Embed the Engagement Reach SDK into your Windows Phone Silverlight project</span></span>
<span data-ttu-id="573c6-106">Nessun elemento da aggiungere.</span><span class="sxs-lookup"><span data-stu-id="573c6-106">You do not have anything to add.</span></span> <span data-ttu-id="573c6-107">`EngagementReach` sono già presenti nel progetto.</span><span class="sxs-lookup"><span data-stu-id="573c6-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="573c6-108">È possibile personalizzare le immagini incluse nella cartella `Resources` del progetto, soprattutto l'icona del marchio, che per impostazione predefinita è l'icona di Engagement.</span><span class="sxs-lookup"><span data-stu-id="573c6-108">You can customize images located in the `Resources` folder of your project, especially the brand icon (that default to the Engagement icon).</span></span>
> 
> 

## <a name="add-the-capabilities"></a><span data-ttu-id="573c6-109">Aggiungere le funzionalità</span><span class="sxs-lookup"><span data-stu-id="573c6-109">Add the capabilities</span></span>
<span data-ttu-id="573c6-110">L'SDK del servizio Reach di Engagement richiede alcune funzionalità aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="573c6-110">The Engagement Reach SDK needs some additional capabilities.</span></span>

<span data-ttu-id="573c6-111">Aprire il file `WMAppManifest.xml` e assicurarsi che le seguenti funzionalità siano dichiarate:</span><span class="sxs-lookup"><span data-stu-id="573c6-111">Open your `WMAppManifest.xml` file and be sure that the following capabilities are declared:</span></span>

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

<span data-ttu-id="573c6-112">La prima viene usata dal servizio MPNS per consentire la visualizzazione di notifiche popup.</span><span class="sxs-lookup"><span data-stu-id="573c6-112">The first one is used by the MPNS service to allow the display of toast notification.</span></span> <span data-ttu-id="573c6-113">La seconda viene usata per incorporare un'attività del browser nell'SDK.</span><span class="sxs-lookup"><span data-stu-id="573c6-113">The second one is used to embed a browser task into the SDK.</span></span>

<span data-ttu-id="573c6-114">Modificare il file `WMAppManifest.xml` e aggiungere il tag `<Capabilities />` all'interno:</span><span class="sxs-lookup"><span data-stu-id="573c6-114">Edit the `WMAppManifest.xml` file and add inside the `<Capabilities />` tag :</span></span>

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-the-microsoft-push-notification-service"></a><span data-ttu-id="573c6-115">Abilitare il Servizio notifica push Microsoft</span><span class="sxs-lookup"><span data-stu-id="573c6-115">Enable the Microsoft Push Notification Service</span></span>
<span data-ttu-id="573c6-116">Per usare il **Servizio notifica push Microsoft** (indicato come MPNS), il file `WMAppManifest.xml` deve avere un tag `<App />` con un attributo `Publisher` impostato sul nome del progetto.</span><span class="sxs-lookup"><span data-stu-id="573c6-116">In order to use the **Microsoft Push Notification Service** (referred as MPNS) your `WMAppManifest.xml` file must have an `<App />` tag with a `Publisher` attribute set to the name of your project.</span></span>

## <a name="initialize-the-engagement-reach-sdk"></a><span data-ttu-id="573c6-117">Inizializzare Engagement Reach SDK</span><span class="sxs-lookup"><span data-stu-id="573c6-117">Initialize the Engagement Reach SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="573c6-118">Configurazione di Engagement</span><span class="sxs-lookup"><span data-stu-id="573c6-118">Engagement configuration</span></span>
<span data-ttu-id="573c6-119">La configurazione di Engagement è centralizzata nel file `Resources\EngagementConfiguration.xml` del progetto.</span><span class="sxs-lookup"><span data-stu-id="573c6-119">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="573c6-120">Modificare questo file per specificare la configurazione di Reach:</span><span class="sxs-lookup"><span data-stu-id="573c6-120">Edit this file to specify reach configuration :</span></span>

* <span data-ttu-id="573c6-121">*Facoltativo*: indicare se il push nativo (MPNS) è attivato tra i tag `<enableNativePush>` e `</enableNativePush>`. L'impostazione predefinita è `true`.</span><span class="sxs-lookup"><span data-stu-id="573c6-121">*Optional*, indicate whether the native push (MPNS) is activated or not between `<enableNativePush>` and `</enableNativePush>` tags, (`true` by default).</span></span>
* <span data-ttu-id="573c6-122">*Facoltativo*: indicare il nome del canale di push tra i tag `<channelName>` e `</channelName>`. Fornire quello che potrebbe essere in uso nell'applicazione o lasciare vuoto il campo.</span><span class="sxs-lookup"><span data-stu-id="573c6-122">*Optional*, indicate the name of the push channel between `<channelName>` and `</channelName>` tags, provide the same that your application may currently use or leave it empty.</span></span>

<span data-ttu-id="573c6-123">Se si desidera specificarlo in fase di esecuzione, è possibile chiamare il metodo seguente prima dell'inizializzazione dell'agente di Engagement:</span><span class="sxs-lookup"><span data-stu-id="573c6-123">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization :</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether the native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide the same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> <span data-ttu-id="573c6-124">È possibile specificare il nome del canale di push MPNS dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="573c6-124">You can specify the name of the MPNS push channel of your application.</span></span> <span data-ttu-id="573c6-125">Per impostazione predefinita, Engagement crea un nome basato su appId.</span><span class="sxs-lookup"><span data-stu-id="573c6-125">By default, Engagement creates a name based on the appId.</span></span> <span data-ttu-id="573c6-126">Non è necessario specificare il nome manualmente, a meno che non si preveda di utilizzare il canale di push fuori da Engagement.</span><span class="sxs-lookup"><span data-stu-id="573c6-126">You have no need to specify the name yourself, except if you plan to use the push channel outside of Engagement.</span></span>
> 
> 

### <a name="engagement-initialization"></a><span data-ttu-id="573c6-127">Inizializzazione di Engagement</span><span class="sxs-lookup"><span data-stu-id="573c6-127">Engagement initialization</span></span>
<span data-ttu-id="573c6-128">Modificare il file `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="573c6-128">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="573c6-129">Aggiungere quanto segue alle istruzioni `using`:</span><span class="sxs-lookup"><span data-stu-id="573c6-129">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="573c6-130">Inserire `EngagementReach.Instance.Init` subito dopo `EngagementAgent.Instance.Init` in `Application_Launching`:</span><span class="sxs-lookup"><span data-stu-id="573c6-130">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in `Application_Launching` :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* <span data-ttu-id="573c6-131">Inserire `EngagementReach.Instance.OnActivated` nel metodo `Application_Activated`:</span><span class="sxs-lookup"><span data-stu-id="573c6-131">Insert `EngagementReach.Instance.OnActivated` in the `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> <span data-ttu-id="573c6-132">`EngagementReach.Instance.Init` viene eseguito in un thread dedicato.</span><span class="sxs-lookup"><span data-stu-id="573c6-132">The `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="573c6-133">Non è necessario eseguirlo manualmente.</span><span class="sxs-lookup"><span data-stu-id="573c6-133">You do not have to do it yourself.</span></span>
> 
> 

## <a name="app-store-submission-considerations"></a><span data-ttu-id="573c6-134">Considerazioni sull'invio di notifiche di App Store</span><span class="sxs-lookup"><span data-stu-id="573c6-134">App store submission considerations</span></span>
<span data-ttu-id="573c6-135">Microsoft impone alcune regole relative all'uso delle notifiche push.</span><span class="sxs-lookup"><span data-stu-id="573c6-135">Microsoft imposes some rules when using the push notifications:</span></span>

<span data-ttu-id="573c6-136">Come definito nella documentazione di Microsoft sui [criteri relativi alle applicazioni] , sezione 2.9:</span><span class="sxs-lookup"><span data-stu-id="573c6-136">From the Microsoft [Application Policies] documentation, section 2.9:</span></span>

1) <span data-ttu-id="573c6-137">È necessario chiedere all'utente di accettare la ricezione delle notifiche push.</span><span class="sxs-lookup"><span data-stu-id="573c6-137">You must ask the user to accept to receive push notifications.</span></span> <span data-ttu-id="573c6-138">Aggiungere quindi nelle impostazioni un modo per disattivare le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="573c6-138">Then, in your settings, add a way to disable the push notifications.</span></span>

<span data-ttu-id="573c6-139">L'oggetto EngagementReach fornisce due metodi per gestire il consenso/rifiuto, `EnableNativePush()` e `DisableNativePush()`.</span><span class="sxs-lookup"><span data-stu-id="573c6-139">The EngagementReach object provides two methods to manage the opt-in/opt-out, `EnableNativePush()` and `DisableNativePush()`.</span></span> <span data-ttu-id="573c6-140">È possibile, ad esempio, creare nelle impostazioni un'opzione che consente di disabilitare o abilitare MPNS.</span><span class="sxs-lookup"><span data-stu-id="573c6-140">You could, for example, create an option in the settings with a toggle to disable or enable MPNS.</span></span>

<span data-ttu-id="573c6-141">È possibile anche decidere di disattivare MPNS tramite la configurazione di Engagement \<windows-phone-sdk-reach-configuration\>.</span><span class="sxs-lookup"><span data-stu-id="573c6-141">You can also decide to deactivate MPNS through the Engagement configuration\<windows-phone-sdk-reach-configuration\>.</span></span>

> <span data-ttu-id="573c6-142">2.9.1) L'applicazione deve descrivere prima le notifiche da fornire e **ottenere l'autorizzazione esplicita dell'utente (consenso)** e **deve fornire un meccanismo attraverso il quale l'utente può rifiutare esplicitamente la ricezione di notifiche push**.</span><span class="sxs-lookup"><span data-stu-id="573c6-142">2.9.1) The application must first describe the notifications to be provided and **obtain the user’s express permission (opt-in)**, and **must provide a mechanism through which the user can opt out of receiving push notifications**.</span></span> <span data-ttu-id="573c6-143">Tutte le notifiche fornite tramite il Servizio notifica push Microsoft devono essere coerenti con la descrizione fornita all'utente e conformi a tutti i [criteri applicazione][Content Policies] e a tutti i [requisiti aggiuntivi per tipi di applicazione specifici] applicabili.</span><span class="sxs-lookup"><span data-stu-id="573c6-143">All notifications provided using the Microsoft Push Notification Service must be consistent with the description provided to the user and must comply with all applicable [Application Policies][Content Policies] and [Additional Requirements for Specific Application Types].</span></span>
> 
> 

2) <span data-ttu-id="573c6-144">Non fare un uso eccessivo delle notifiche push.</span><span class="sxs-lookup"><span data-stu-id="573c6-144">You should not use too many push notifications.</span></span> <span data-ttu-id="573c6-145">Engagement gestisce le notifiche in modo automatico.</span><span class="sxs-lookup"><span data-stu-id="573c6-145">Engagement will handle notifications for you.</span></span>

> <span data-ttu-id="573c6-146">2.9.2) L'applicazione che usa il Servizio notifica push Microsoft non deve sfruttare in modo eccessivo la capacità di rete o la larghezza di banda del Servizio notifica push Microsoft o sovraccaricare inutilmente un dispositivo Windows Phone o altro dispositivo o servizio Microsoft con un numero eccessivo di notifiche push, come stabilito da Microsoft a sua ragionevole discrezione, e non deve danneggiare o interferire con le reti o i server Microsoft o i server e le reti di terze parti connesse al Servizio notifica push Microsoft.</span><span class="sxs-lookup"><span data-stu-id="573c6-146">2.9.2) The application and its use of the Microsoft Push Notification Service must not excessively use network capacity or bandwidth of the Microsoft Push Notification Service, or otherwise unduly burden a Windows Phone or other Microsoft device or service with excessive push notifications, as determined by Microsoft in its reasonable discretion, and must not harm or interfere with any Microsoft networks or servers or any third party servers or networks connected to the Microsoft Push Notification Service.</span></span>
> 
> 

3) <span data-ttu-id="573c6-147">Non fare affidamento su MPNS per inviare informazioni critiche.</span><span class="sxs-lookup"><span data-stu-id="573c6-147">Do not rely on MPNS to send criticals information.</span></span> <span data-ttu-id="573c6-148">Engagement usa MPNS, pertanto questa regola è valida anche per le campagne create all'interno del front-end di Engagement.</span><span class="sxs-lookup"><span data-stu-id="573c6-148">Engagement uses MPNS, so this rule also applies for the campaigns created inside the Engagement front-end.</span></span>

> <span data-ttu-id="573c6-149">2.9.3) Il Servizio notifica push Microsoft non può essere usato per inviare notifiche di importanza cruciale o che possono influire su questioni di vita o di morte, incluse, senza alcuna limitazione, notifiche correlate a una condizione o a un dispositivo medico.</span><span class="sxs-lookup"><span data-stu-id="573c6-149">2.9.3) The Microsoft Push Notification Service may not be used to send notifications that are mission critical or otherwise could affect matters of life or death, including without limitation critical notifications related to a medical device or condition.</span></span> <span data-ttu-id="573c6-150">MICROSOFT RIFIUTA ESPRESSAMENTE QUALSIASI GARANZIA CHE L'UTILIZZO DEL SERVIZIO DI NOTIFICA PUSH DI MICROSOFT O CHE IL RECAPITO DELLE NOTIFICHE DEL SERVIZIO NOTIFICA PUSH MICROSOFT SARÀ ININTERROTTO, PRIVO DI ERRORI O CHE SARÀ ESEGUITO IN TEMPO REALE.</span><span class="sxs-lookup"><span data-stu-id="573c6-150">MICROSOFT EXPRESSLY DISCLAIMS ANY WARRANTIES THAT THE USE OF THE MICROSOFT PUSH NOTIFICATION SERVICE OR DELIVERY OF MICROSOFT PUSH NOTIFICATION SERVICE NOTIFICATIONS WILL BE UNINTERRUPTED, ERROR FREE, OR OTHERWISE GUARANTEED TO OCCUR ON A REAL-TIME BASIS.</span></span>
> 
> 

<span data-ttu-id="573c6-151">**Non è possibile garantire che l'applicazione supererà il processo di convalida se non si rispettano queste indicazioni.**</span><span class="sxs-lookup"><span data-stu-id="573c6-151">**We cannot guarantee that your application will pass the validation process if you do not respect these recommendations.**</span></span>

## <a name="handle-data-push-optional"></a><span data-ttu-id="573c6-152">Gestire il push di dati (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="573c6-152">Handle data push (optional)</span></span>
<span data-ttu-id="573c6-153">Se si desidera che l'applicazione sia in grado di ricevere push di dati Reach, è necessario implementare due eventi della classe EngagementReach:</span><span class="sxs-lookup"><span data-stu-id="573c6-153">If you want your application to be able to receive Reach data pushes, you have to implement two events of the EngagementReach class:</span></span>

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

<span data-ttu-id="573c6-154">È possibile notare che il callback di ogni metodo restituisce un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="573c6-154">You can see that the callback of each method returns a boolean.</span></span> <span data-ttu-id="573c6-155">Engagement invia un feedback per il back-end dopo l'invio del push di dati.</span><span class="sxs-lookup"><span data-stu-id="573c6-155">Engagement sends a feedback to its back-end after dispatching the data push.</span></span> <span data-ttu-id="573c6-156">Se il callback restituisce false, verrà inviato il feedback `exit` .</span><span class="sxs-lookup"><span data-stu-id="573c6-156">If the callback returns false, the `exit` feedback will be send.</span></span> <span data-ttu-id="573c6-157">In caso contrario, il feedback sarà `action`.</span><span class="sxs-lookup"><span data-stu-id="573c6-157">Otherwise, it will be `action`.</span></span> <span data-ttu-id="573c6-158">Se non è impostato alcun callback per gli eventi, il feedback `drop` verrà restituito a Engagement.</span><span class="sxs-lookup"><span data-stu-id="573c6-158">If no callback is set for the events, the `drop` feedback will be returned to Engagement.</span></span>

> [!WARNING]
> <span data-ttu-id="573c6-159">Engagement non è in grado di ricevere più feedback per un push di dati.</span><span class="sxs-lookup"><span data-stu-id="573c6-159">Engagement is not able to receive multiples feedbacks for a data push.</span></span> <span data-ttu-id="573c6-160">Se si prevede di impostare diversi gestori su un evento, tenere presente che il feedback corrisponderà all'ultimo inviato.</span><span class="sxs-lookup"><span data-stu-id="573c6-160">If you plan to set several handlers on an event, be aware that the feedback will correspond to the last one sent.</span></span> <span data-ttu-id="573c6-161">In questo caso, è consigliabile restituire sempre lo stesso valore per evitare confusione di feedback sul front-end.</span><span class="sxs-lookup"><span data-stu-id="573c6-161">In this case, we recommend to always returns the same value to avoid having confusing feedback on the front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="573c6-162">Personalizzare l'interfaccia utente (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="573c6-162">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="573c6-163">Primo passaggio</span><span class="sxs-lookup"><span data-stu-id="573c6-163">First step</span></span>
<span data-ttu-id="573c6-164">È possibile personalizzare l'interfaccia utente di Reach.</span><span class="sxs-lookup"><span data-stu-id="573c6-164">We allow you to customize the reach UI.</span></span>

<span data-ttu-id="573c6-165">A tale scopo, è necessario creare una sottoclasse della classe `EngagementReachHandler` .</span><span class="sxs-lookup"><span data-stu-id="573c6-165">To do so, you have to create a subclass of the `EngagementReachHandler` class.</span></span>

<span data-ttu-id="573c6-166">**Codice di esempio:**</span><span class="sxs-lookup"><span data-stu-id="573c6-166">**Sample Code :**</span></span>

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

<span data-ttu-id="573c6-167">Impostare quindi il contenuto del campo `EngagementReach.Instance.Handler` con l'oggetto personalizzato nella classe `App.xaml.cs` all'interno del metodo `Application_Launching`.</span><span class="sxs-lookup"><span data-stu-id="573c6-167">Then, set the content of the `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within the `Application_Launching` method.</span></span>

<span data-ttu-id="573c6-168">**Codice di esempio:**</span><span class="sxs-lookup"><span data-stu-id="573c6-168">**Sample Code :**</span></span>

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> <span data-ttu-id="573c6-169">Per impostazione predefinita, Engagement usa una specifica implementazione di `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="573c6-169">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span> <span data-ttu-id="573c6-170">Non è necessario crearne di proprie e, se ne viene creata una, non è necessario eseguire l'override di ogni metodo.</span><span class="sxs-lookup"><span data-stu-id="573c6-170">You don't have to create your own, and if you do so, you don't have to override every method.</span></span> <span data-ttu-id="573c6-171">Il comportamento predefinito consiste nel selezionare l'oggetto di base di Engagement.</span><span class="sxs-lookup"><span data-stu-id="573c6-171">The default behavior is to select the Engagement base object.</span></span>
> 
> 

### <a name="layouts"></a><span data-ttu-id="573c6-172">Layout</span><span class="sxs-lookup"><span data-stu-id="573c6-172">Layouts</span></span>
<span data-ttu-id="573c6-173">Per impostazione predefinita, Reach userà le risorse incorporate della DLL per visualizzare le pagine e le notifiche.</span><span class="sxs-lookup"><span data-stu-id="573c6-173">By default, Reach will use the embedded resources of the DLL to display the notifications and pages.</span></span>

<span data-ttu-id="573c6-174">Tuttavia, è possibile decidere di utilizzare le proprie risorse in modo da riflettere il marchio in questi componenti.</span><span class="sxs-lookup"><span data-stu-id="573c6-174">However, you can decide to use your own resources to reflect your brand in these components.</span></span>

<span data-ttu-id="573c6-175">È possibile eseguire l'override dei metodi `EngagementReachHandler` in una sottoclasse per indicare a Engagement di usare layout personalizzati:</span><span class="sxs-lookup"><span data-stu-id="573c6-175">You can override `EngagementReachHandler` methods in your subclass to tell Engagement to use your layouts :</span></span>

<span data-ttu-id="573c6-176">**Codice di esempio:**</span><span class="sxs-lookup"><span data-stu-id="573c6-176">**Sample Code :**</span></span>

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return the path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return the path of your own xaml
    }

    public override string GetPollUri()
    {
       // return the path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> <span data-ttu-id="573c6-177">Il metodo `CreateNotification` può restituire null.</span><span class="sxs-lookup"><span data-stu-id="573c6-177">The `CreateNotification` method can return null.</span></span> <span data-ttu-id="573c6-178">La notifica non verrà visualizzata e la campagna Reach verrà eliminata.</span><span class="sxs-lookup"><span data-stu-id="573c6-178">The notification won't be displayed and the reach campaign will be dropped.</span></span>
> 
> 

<span data-ttu-id="573c6-179">Per semplificare l'implementazione di layout, viene fornito anche un xaml che può essere utilizzato come base per il codice.</span><span class="sxs-lookup"><span data-stu-id="573c6-179">To simplify your layout implementation, we also provide our own xaml which can serve as a basis for your code.</span></span> <span data-ttu-id="573c6-180">Tale elemento si trova nell'archivio dell'SDK di Engagement (/src/reach/).</span><span class="sxs-lookup"><span data-stu-id="573c6-180">They are located in the Engagement SDK archive (/src/reach/).</span></span>

> [!WARNING]
> <span data-ttu-id="573c6-181">Le origini fornite da Microsoft sono le stesse.</span><span class="sxs-lookup"><span data-stu-id="573c6-181">The sources that we provide are the exact same ones that we use.</span></span> <span data-ttu-id="573c6-182">Pertanto, se si desidera modificarle direttamente, non dimenticare di modificare lo spazio dei nomi e il nome.</span><span class="sxs-lookup"><span data-stu-id="573c6-182">So if you want to modify them directly, don't forget to change the namespace and the name.</span></span>
> 
> 

### <a name="notification-position"></a><span data-ttu-id="573c6-183">Posizione di notifica</span><span class="sxs-lookup"><span data-stu-id="573c6-183">Notification position</span></span>
<span data-ttu-id="573c6-184">Per impostazione predefinita, una notifica in-app viene visualizzata nella parte inferiore sinistra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="573c6-184">By default, an in-app notification is displayed at the bottom left side of the application.</span></span> <span data-ttu-id="573c6-185">È possibile modificare questo comportamento eseguendo l'override del metodo `GetNotificationPosition` dell'oggetto `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="573c6-185">You can change this behavior by overriding the `GetNotificationPosition` method of the `EngagementReachHandler` object.</span></span>

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of the EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

<span data-ttu-id="573c6-186">Attualmente, è possibile scegliere tra le posizioni `BOTTOM` (impostazione predefinita) e `TOP`.</span><span class="sxs-lookup"><span data-stu-id="573c6-186">Currently, you can choose between the `BOTTOM` (default) and `TOP` positions.</span></span>

### <a name="launch-message"></a><span data-ttu-id="573c6-187">Messaggio di avvio</span><span class="sxs-lookup"><span data-stu-id="573c6-187">Launch message</span></span>
<span data-ttu-id="573c6-188">Quando un utente fa clic su una notifica del sistema (avviso popup), Engagement avvia l'app, carica il contenuto dei messaggi di push e visualizza la pagina per la campagna corrispondente.</span><span class="sxs-lookup"><span data-stu-id="573c6-188">When a user clicks on a system notification (a toast), Engagement launches the app, load the content of the push messages, and display the page for the corresponding campaign.</span></span>

<span data-ttu-id="573c6-189">Tra l'avvio dell'applicazione e la visualizzazione della pagina si verifica un ritardo (a seconda della velocità della rete).</span><span class="sxs-lookup"><span data-stu-id="573c6-189">There is a delay between the launch of the application and the display of the page (depending on the speed of your network).</span></span>

<span data-ttu-id="573c6-190">Per indicare all'utente che è in corso un caricamento, è necessario fornire un'indicazione visiva, ad esempio una barra o un indicatore di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="573c6-190">To indicate to the user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="573c6-191">Engagement non è in grado di gestire questa situazione, ma fornisce alcuni gestori.</span><span class="sxs-lookup"><span data-stu-id="573c6-191">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="573c6-192">Per implementare il callback:</span><span class="sxs-lookup"><span data-stu-id="573c6-192">To implement the callback, do:</span></span>

    /* The application has launched and the content is loading.
     * You should display an indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

    /* The application has finished loading the content and the page
     * is about to be displayed.
     * You should hide the indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

    /* The content has been loaded, but an error has occurred.
     * You can provide an information to the user.
     * You should hide the indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

<span data-ttu-id="573c6-193">È possibile impostare il callback nel metodo `Application_Launching` del file `App.xaml.cs`, preferibilmente prima della chiamata `EngagementReach.Instance.Init()`.</span><span class="sxs-lookup"><span data-stu-id="573c6-193">You can set the callback in your `Application_Launching` method of your `App.xaml.cs` file, preferably before the `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="573c6-194">Ogni gestore viene chiamato dal thread dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="573c6-194">Each handler is called by the UI Thread.</span></span> <span data-ttu-id="573c6-195">Non è necessario preoccuparsi quando si utilizza MessageBox o un elemento correlato all'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="573c6-195">You do not have to worry when using a MessageBox or something UI-related.</span></span>
> 
> 

<span data-ttu-id="573c6-196">[criteri relativi alle applicazioni]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="573c6-196">[Application Policies]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx</span></span>
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
<span data-ttu-id="573c6-197">[requisiti aggiuntivi per tipi di applicazione specifici]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="573c6-197">[Additional Requirements for Specific Application Types]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx</span></span>

