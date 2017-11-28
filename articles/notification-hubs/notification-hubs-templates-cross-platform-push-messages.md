---
title: aaaTemplates
description: In questo argomento vengono illustrati i modelli per Hub di notifica di Azure.
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: a41897bb-5b4b-48b2-bfd5-2e3c65edc37e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0149f0c7473e5a4b952905bc8217582b58db2a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="templates"></a><span data-ttu-id="eead8-103">Modelli</span><span class="sxs-lookup"><span data-stu-id="eead8-103">Templates</span></span>
## <a name="overview"></a><span data-ttu-id="eead8-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="eead8-104">Overview</span></span>
<span data-ttu-id="eead8-105">I modelli consentono un client applicazione toospecify hello formato esatto delle notifiche di hello che tooreceive desiderati.</span><span class="sxs-lookup"><span data-stu-id="eead8-105">Templates enable a client application toospecify hello exact format of hello notifications it wants tooreceive.</span></span> <span data-ttu-id="eead8-106">Utilizzo di modelli, un'app consentono di realizzare diversi diversi vantaggi, tra cui hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="eead8-106">Using templates, an app can realize several different benefits, including hello following :</span></span>

* <span data-ttu-id="eead8-107">Un back-end indipendente dalla piattaforma</span><span class="sxs-lookup"><span data-stu-id="eead8-107">A platform-agnostic backend</span></span>
* <span data-ttu-id="eead8-108">Notifiche personalizzate</span><span class="sxs-lookup"><span data-stu-id="eead8-108">Personalized notifications</span></span>
* <span data-ttu-id="eead8-109">Indipendenza dalla versione del client</span><span class="sxs-lookup"><span data-stu-id="eead8-109">Client-version independence</span></span>
* <span data-ttu-id="eead8-110">Localizzazione semplice</span><span class="sxs-lookup"><span data-stu-id="eead8-110">Easy localization</span></span>

<span data-ttu-id="eead8-111">In questa sezione vengono forniti due esempi approfonditi come le notifiche indipendente dalla piattaforma toosend modelli toouse tutti i dispositivi di destinazione su piattaforme e toopersonalize broadcast dispositivo tooeach di notifica.</span><span class="sxs-lookup"><span data-stu-id="eead8-111">This section provides two in-depth examples of how toouse templates toosend platform-agnostic notifications targeting all your devices across platforms, and toopersonalize broadcast notification tooeach device.</span></span>

## <a name="using-templates-cross-platform"></a><span data-ttu-id="eead8-112">Utilizzo di modelli multipiattaforma</span><span class="sxs-lookup"><span data-stu-id="eead8-112">Using templates cross-platform</span></span>
<span data-ttu-id="eead8-113">le notifiche push in modo standard toosend Hello è toosend, per ogni notifica che viene inviato, toobe un payload specifico tooplatform notifica di servizi (WNS, APN).</span><span class="sxs-lookup"><span data-stu-id="eead8-113">hello standard way toosend push notifications is toosend, for each notification that is toobe sent, a specific payload tooplatform notification services (WNS, APNS).</span></span> <span data-ttu-id="eead8-114">Ad esempio, un avviso tooAPNS, toosend payload hello è un oggetto Json di hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="eead8-114">For example, toosend an alert tooAPNS, hello payload is a Json object of hello following form:</span></span>

    {"aps": {"alert" : "Hello!" }}

<span data-ttu-id="eead8-115">toosend un messaggio di tipo avviso popup simile in un'applicazione Windows Store, payload XML hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="eead8-115">toosend a similar toast message on a Windows Store application, hello XML payload is as follows:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

<span data-ttu-id="eead8-116">È possibile creare payload simili per MPNS (Windows Phone) e piattaforme GCM (Android).</span><span class="sxs-lookup"><span data-stu-id="eead8-116">You can create similar payloads for MPNS (Windows Phone) and GCM (Android) platforms.</span></span>

<span data-ttu-id="eead8-117">Questo requisito forza hello app back-end tooproduce diversi payload per ogni piattaforma e rende effettivamente responsabile della parte del livello di presentazione hello di hello app back-end hello.</span><span class="sxs-lookup"><span data-stu-id="eead8-117">This requirement forces hello app backend tooproduce different payloads for each platform, and effectively makes hello backend responsible for part of hello presentation layer of hello app.</span></span> <span data-ttu-id="eead8-118">Alcuni dei problemi riguardano la localizzazione e i layout grafici (soprattutto per applicazioni di Windows Store che comprendono notifiche per vari tipi di riquadri).</span><span class="sxs-lookup"><span data-stu-id="eead8-118">Some concerns include localization and graphical layouts (especially for Windows Store apps that include notifications for various types of tiles).</span></span>

<span data-ttu-id="eead8-119">funzionalità del modello di hub di notifica Hello consente un app toocreate speciali registrazioni client, le registrazioni del modello, che includono inoltre toohello set di tag, un modello di chiamata.</span><span class="sxs-lookup"><span data-stu-id="eead8-119">hello Notification Hubs template feature enables a client app toocreate special registrations, called template registrations, which include, in addition toohello set of tags, a template.</span></span> <span data-ttu-id="eead8-120">funzionalità del modello di hub di notifica Hello consente dispositivi tooassociate app client con i modelli se si lavora con installazioni (scelta consigliate) o registrazioni.</span><span class="sxs-lookup"><span data-stu-id="eead8-120">hello Notification Hubs template feature enables a client app tooassociate devices with templates whether you are working with Installations (preferred) or Registrations.</span></span> <span data-ttu-id="eead8-121">Dato hello precedenti esempi di payload, hello solo le informazioni indipendente dalla piattaforma sono hello effettivo messaggio di avviso (Hello!).</span><span class="sxs-lookup"><span data-stu-id="eead8-121">Given hello preceding payload examples, hello only platform-independent information is hello actual alert message (Hello!).</span></span> <span data-ttu-id="eead8-122">Un modello è un set di istruzioni per l'Hub di notifica di hello in modalità tooformat un indipendente dalla piattaforma dei messaggi per la registrazione di hello di app client specifico.</span><span class="sxs-lookup"><span data-stu-id="eead8-122">A template is a set of instructions for hello Notification Hub on how tooformat a platform-independent message for hello registration of that specific client app.</span></span> <span data-ttu-id="eead8-123">In hello sopra riportato, messaggio indipendente dalla piattaforma di hello è una singola proprietà: **messaggio = Hello!**.</span><span class="sxs-lookup"><span data-stu-id="eead8-123">In hello preceding example, hello platform independent message is a single property: **message = Hello!**.</span></span>

<span data-ttu-id="eead8-124">Hello seguente immagine illustra hello sopra processo:</span><span class="sxs-lookup"><span data-stu-id="eead8-124">hello following picture illustrates hello above process:</span></span>

![](./media/notification-hubs-templates/notification-hubs-hello.png)

<span data-ttu-id="eead8-125">modello di Hello per la registrazione dell'app client iOS hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="eead8-125">hello template for hello iOS client app registration is as follows:</span></span>

    {"aps": {"alert": "$(message)"}}

<span data-ttu-id="eead8-126">modello di Hello corrispondente per l'applicazione client di Windows Store hello è:</span><span class="sxs-lookup"><span data-stu-id="eead8-126">hello corresponding template for hello Windows Store client app is:</span></span>

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

<span data-ttu-id="eead8-127">Si noti che hello effettivo del messaggio viene sostituito per hello espressione $(messaggio).</span><span class="sxs-lookup"><span data-stu-id="eead8-127">Notice that hello actual message is substituted for hello expression $(message).</span></span> <span data-ttu-id="eead8-128">Questa espressione indica hello Hub di notifica, ogni volta che invia un messaggio toothis registrazione particolare, un messaggio che segue viene switch in valore comune hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="eead8-128">This expression instructs hello Notification Hub, whenever it sends a message toothis particular registration, toobuild a message that follows it and switches in hello common value.</span></span>

<span data-ttu-id="eead8-129">Se utilizza il modello di installazione, chiave "modelli" installazione di hello contiene un formato JSON di più modelli.</span><span class="sxs-lookup"><span data-stu-id="eead8-129">If you are working with Installation model, hello installation “templates” key holds a JSON of multiple templates.</span></span> <span data-ttu-id="eead8-130">Se si lavora con modello di registrazione, hello applicazione client può creare più registrazioni in ordine toouse più modelli. ad esempio, un modello per i messaggi di avviso e un modello di riquadro aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="eead8-130">If you are working with Registration model, hello client application can create multiple registrations in order toouse multiple templates; for example, a template for alert messages and a template for tile updates.</span></span> <span data-ttu-id="eead8-131">Inoltre, le applicazioni client possono unire registrazioni native (registrazioni senza modello) e registrazioni con modello.</span><span class="sxs-lookup"><span data-stu-id="eead8-131">Client applications can also mix native registrations (registrations with no template) and template registrations.</span></span>

<span data-ttu-id="eead8-132">Hub di notifica Hello invia una notifica per ogni modello, senza considerare se appartengono toohello app client stesso.</span><span class="sxs-lookup"><span data-stu-id="eead8-132">hello Notification Hub sends one notification for each template without considering whether they belong toohello same client app.</span></span> <span data-ttu-id="eead8-133">Questo comportamento può essere notifiche indipendente dalla piattaforma tootranslate utilizzati in altre notifiche.</span><span class="sxs-lookup"><span data-stu-id="eead8-133">This behavior can be used tootranslate platform-independent notifications into more notifications.</span></span> <span data-ttu-id="eead8-134">Ad esempio, hello toohello di messaggi indipendenti dalla piattaforma stessa che hub di notifica possono essere convertiti perfettamente in un avviso di tipo avviso popup e un aggiornamento del riquadro, senza richiedere hello informati toobe di back-end.</span><span class="sxs-lookup"><span data-stu-id="eead8-134">For example, hello same platform independent message toohello Notification Hub can be seamlessly translated in a toast alert and a tile update, without requiring hello backend toobe aware of it.</span></span> <span data-ttu-id="eead8-135">Si noti che alcune piattaforme (ad esempio, iOS) potrebbero comprime più notifiche toohello stesso dispositivo, se vengono inviati in un breve periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="eead8-135">Note that some platforms (for example, iOS) might collapse multiple notifications toohello same device if they are sent in a short period of time.</span></span>

## <a name="using-templates-for-personalization"></a><span data-ttu-id="eead8-136">Utilizzo di modelli per la personalizzazione</span><span class="sxs-lookup"><span data-stu-id="eead8-136">Using templates for personalization</span></span>
<span data-ttu-id="eead8-137">Modelli di toousing un altro vantaggio è hello possibilità toouse sulla personalizzazione di hub di notifica tooperform per la registrazione delle notifiche.</span><span class="sxs-lookup"><span data-stu-id="eead8-137">Another advantage toousing templates is hello ability toouse Notification Hubs tooperform per-registration personalization of notifications.</span></span> <span data-ttu-id="eead8-138">Si consideri ad esempio un'app meteo che consente di visualizzare un riquadro con condizioni climatiche hello in una posizione specifica.</span><span class="sxs-lookup"><span data-stu-id="eead8-138">For example, consider a weather app that displays a tile with hello weather conditions at a specific location.</span></span> <span data-ttu-id="eead8-139">Un utente può scegliere tra gradi Celsius o Fahrenheit e una previsione singola o di cinque giorni.</span><span class="sxs-lookup"><span data-stu-id="eead8-139">A user can choose between Celsius or Fahrenheit degrees, and a single or five-day forecast.</span></span> <span data-ttu-id="eead8-140">Utilizzo di modelli, ogni installazione di app client può registrare per formato hello richiesto (1 giorno Celsius, 1 giorno Fahrenheit, 5 giorni Celsius, 5 giorni Fahrenheit), e back-end hello invia un messaggio singolo che contiene tutte le informazioni di hello obbligatoria toofill quelli modelli (ad esempio, cinque giorni previsione con gradi Celsius e Fahrenheit).</span><span class="sxs-lookup"><span data-stu-id="eead8-140">Using templates, each client app installation can register for hello format required (1-day Celsius, 1-day Fahrenheit, 5-days Celsius, 5-days Fahrenheit), and have hello backend send a single message that contains all hello information required toofill those templates (for example, a five-day forecast with Celsius and Fahrenheit degrees).</span></span>

<span data-ttu-id="eead8-141">modello Hello per hello un giorno previsione con Celsius temperature è come segue:</span><span class="sxs-lookup"><span data-stu-id="eead8-141">hello template for hello one-day forecast with Celsius temperatures is as follows:</span></span>

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

<span data-ttu-id="eead8-142">toohello messaggio Hello Hub di notifica contiene hello tutte le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="eead8-142">hello message sent toohello Notification Hub contains all hello following properties:</span></span>

<table border="1">

<tr><td><span data-ttu-id="eead8-143">day1_image</span><span class="sxs-lookup"><span data-stu-id="eead8-143">day1_image</span></span></td><td><span data-ttu-id="eead8-144">day2_image</span><span class="sxs-lookup"><span data-stu-id="eead8-144">day2_image</span></span></td><td><span data-ttu-id="eead8-145">day3_image</span><span class="sxs-lookup"><span data-stu-id="eead8-145">day3_image</span></span></td><td><span data-ttu-id="eead8-146">day4_image</span><span class="sxs-lookup"><span data-stu-id="eead8-146">day4_image</span></span></td><td><span data-ttu-id="eead8-147">day5_image</span><span class="sxs-lookup"><span data-stu-id="eead8-147">day5_image</span></span></td></tr>

<tr><td><span data-ttu-id="eead8-148">day1_tempC</span><span class="sxs-lookup"><span data-stu-id="eead8-148">day1_tempC</span></span></td><td><span data-ttu-id="eead8-149">day2_tempC</span><span class="sxs-lookup"><span data-stu-id="eead8-149">day2_tempC</span></span></td><td><span data-ttu-id="eead8-150">day3_tempC</span><span class="sxs-lookup"><span data-stu-id="eead8-150">day3_tempC</span></span></td><td><span data-ttu-id="eead8-151">day4_tempC</span><span class="sxs-lookup"><span data-stu-id="eead8-151">day4_tempC</span></span></td><td><span data-ttu-id="eead8-152">day5_tempC</span><span class="sxs-lookup"><span data-stu-id="eead8-152">day5_tempC</span></span></td></tr>

<tr><td><span data-ttu-id="eead8-153">day1_tempF</span><span class="sxs-lookup"><span data-stu-id="eead8-153">day1_tempF</span></span></td><td><span data-ttu-id="eead8-154">day2_tempF</span><span class="sxs-lookup"><span data-stu-id="eead8-154">day2_tempF</span></span></td><td><span data-ttu-id="eead8-155">day3_tempF</span><span class="sxs-lookup"><span data-stu-id="eead8-155">day3_tempF</span></span></td><td><span data-ttu-id="eead8-156">day4_tempF</span><span class="sxs-lookup"><span data-stu-id="eead8-156">day4_tempF</span></span></td><td><span data-ttu-id="eead8-157">day5_tempF</span><span class="sxs-lookup"><span data-stu-id="eead8-157">day5_tempF</span></span></td></tr>
</table><br/>

<span data-ttu-id="eead8-158">Utilizzando questo modello, back-end hello Invia solo un singolo messaggio senza opzioni di personalizzazione specifiche toostore per gli utenti di app hello.</span><span class="sxs-lookup"><span data-stu-id="eead8-158">By using this pattern, hello backend only sends a single message without having toostore specific personalization options for hello app users.</span></span> <span data-ttu-id="eead8-159">Hello seguente immagine illustra questo scenario:</span><span class="sxs-lookup"><span data-stu-id="eead8-159">hello following picture illustrates this scenario:</span></span>

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-tooregister-templates"></a><span data-ttu-id="eead8-160">Come modelli tooregister</span><span class="sxs-lookup"><span data-stu-id="eead8-160">How tooregister templates</span></span>
<span data-ttu-id="eead8-161">vedere tooregister con modelli utilizzando il modello di installazione hello (scelta consigliato) o il modello di registrazione, hello [gestione registrazione](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="eead8-161">tooregister with templates using hello Installation model (preferred), or hello Registration model, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

## <a name="template-expression-language"></a><span data-ttu-id="eead8-162">Linguaggio di espressione dei modelli</span><span class="sxs-lookup"><span data-stu-id="eead8-162">Template expression language</span></span>
<span data-ttu-id="eead8-163">I modelli sono tooXML limitato o formati di documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="eead8-163">Templates are limited tooXML or JSON document formats.</span></span> <span data-ttu-id="eead8-164">Inoltre, è possibile inserire solo le espressioni in particolari punti: ad esempio, attributi dei nodi o valori per il formato XML, valori delle proprietà di stringa per il formato JSON.</span><span class="sxs-lookup"><span data-stu-id="eead8-164">Also, you can only place expressions in particular places; for example, node attributes or values for XML, string property values for JSON.</span></span>

<span data-ttu-id="eead8-165">Hello nella tabella seguente mostra linguaggio hello consentita nei modelli:</span><span class="sxs-lookup"><span data-stu-id="eead8-165">hello following table shows hello language allowed in templates:</span></span>

| <span data-ttu-id="eead8-166">Expression</span><span class="sxs-lookup"><span data-stu-id="eead8-166">Expression</span></span> | <span data-ttu-id="eead8-167">Descrizione</span><span class="sxs-lookup"><span data-stu-id="eead8-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eead8-168">$(prop)</span><span class="sxs-lookup"><span data-stu-id="eead8-168">$(prop)</span></span> |<span data-ttu-id="eead8-169">Proprietà dell'evento tooan riferimento con il nome specificato hello.</span><span class="sxs-lookup"><span data-stu-id="eead8-169">Reference tooan event property with hello given name.</span></span> <span data-ttu-id="eead8-170">I nomi delle proprietà non distinguono tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="eead8-170">Property names are not case-sensitive.</span></span> <span data-ttu-id="eead8-171">Questa espressione viene risolta in valore di testo della proprietà hello o in una stringa vuota se hello proprietà non è presente.</span><span class="sxs-lookup"><span data-stu-id="eead8-171">This expression resolves into hello property’s text value or into an empty string if hello property is not present.</span></span> |
| <span data-ttu-id="eead8-172">$(prop, n)</span><span class="sxs-lookup"><span data-stu-id="eead8-172">$(prop, n)</span></span> |<span data-ttu-id="eead8-173">Come sopra, ma hello testo in modo esplicito troncato in corrispondenza di n caratteri, ad esempio $(titolo, 20) consente di ritagliare hello contenuto della proprietà title hello a 20 caratteri.</span><span class="sxs-lookup"><span data-stu-id="eead8-173">As above, but hello text is explicitly clipped at n characters, for example $(title, 20) clips hello contents of hello title property at 20 characters.</span></span> |
| <span data-ttu-id="eead8-174">.(prop, n)</span><span class="sxs-lookup"><span data-stu-id="eead8-174">.(prop, n)</span></span> |<span data-ttu-id="eead8-175">Come sopra, ma hello testo è Posposto con tre punti, come viene tagliato.</span><span class="sxs-lookup"><span data-stu-id="eead8-175">As above, but hello text is suffixed with three dots as it is clipped.</span></span> <span data-ttu-id="eead8-176">dimensioni totali di Hello di hello troncato stringa e il suffisso hello non superi i n caratteri.</span><span class="sxs-lookup"><span data-stu-id="eead8-176">hello total size of hello clipped string and hello suffix does not exceed n characters.</span></span> <span data-ttu-id="eead8-177">. (titolo, 20) con una proprietà di input dei risultati "This is a riga di titolo hello" in **tratta titolo hello...**</span><span class="sxs-lookup"><span data-stu-id="eead8-177">.(title, 20) with an input property of “This is hello title line” results in **This is hello title...**</span></span> |
| <span data-ttu-id="eead8-178">%(prop)</span><span class="sxs-lookup"><span data-stu-id="eead8-178">%(prop)</span></span> |<span data-ttu-id="eead8-179">Too$(name) simili, ad eccezione del fatto che l'output hello è con codifica URI.</span><span class="sxs-lookup"><span data-stu-id="eead8-179">Similar too$(name) except that hello output is URI-encoded.</span></span> |
| <span data-ttu-id="eead8-180">#(prop)</span><span class="sxs-lookup"><span data-stu-id="eead8-180">#(prop)</span></span> |<span data-ttu-id="eead8-181">Utilizzata nei modelli JSON (ad esempio, per modelli iOS e Android).</span><span class="sxs-lookup"><span data-stu-id="eead8-181">Used in JSON templates (for example, for iOS and Android templates).</span></span><br><br><span data-ttu-id="eead8-182">Questa funzione può essere utilizzata esattamente uguali hello come $(prop) specificata in precedenza, tranne quando sono usati nei modelli JSON (ad esempio, i modelli di Apple).</span><span class="sxs-lookup"><span data-stu-id="eead8-182">This function works exactly hello same as $(prop) previously specified, except when used in JSON templates (for example, Apple templates).</span></span> <span data-ttu-id="eead8-183">In questo caso, se questa funzione non racchiusi tra "{','}" (ad esempio, 'myJsonProperty': '(nome) #'), e restituisce il numero di tooa in formato Javascript, ad esempio, regexp: (0 &#124; (&#91; 1-9 &#93; &#91; 0-9 & #93 ;*))(\. &#91; 0-9 &#93; +)? ((a &#124; E) (+ &#124;-)? &#91; 0-9 &#93; +)?, quindi hello output JSON è un numero.</span><span class="sxs-lookup"><span data-stu-id="eead8-183">In this case, if this function is not surrounded by “{‘,’}” (for example, ‘myJsonProperty’ : ‘#(name)’), and it evaluates tooa number in Javascript format, for example, regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, then hello output JSON is a number.</span></span><br><br><span data-ttu-id="eead8-184">Ad esempio, ' badge : '#(name)' diventa 'badge' : 40 (e non '40').</span><span class="sxs-lookup"><span data-stu-id="eead8-184">For example, ‘badge : ‘#(name)’ becomes ‘badge’ : 40 (and not ‘40‘).</span></span> |
| <span data-ttu-id="eead8-185">'text' o "text"</span><span class="sxs-lookup"><span data-stu-id="eead8-185">‘text’ or “text”</span></span> |<span data-ttu-id="eead8-186">Valore letterale.</span><span class="sxs-lookup"><span data-stu-id="eead8-186">A literal.</span></span> <span data-ttu-id="eead8-187">I valori letterali contengono testo arbitrario racchiuso tra virgolette singole o doppie.</span><span class="sxs-lookup"><span data-stu-id="eead8-187">Literals contain arbitrary text enclosed in single or double quotes.</span></span> |
| <span data-ttu-id="eead8-188">expr1 + expr2</span><span class="sxs-lookup"><span data-stu-id="eead8-188">expr1 + expr2</span></span> |<span data-ttu-id="eead8-189">operatore di concatenazione Hello unione di due espressioni in un'unica stringa.</span><span class="sxs-lookup"><span data-stu-id="eead8-189">hello concatenation operator joining two expressions into a single string.</span></span> |

<span data-ttu-id="eead8-190">le espressioni di Hello possono essere qualsiasi di hello precedente form.</span><span class="sxs-lookup"><span data-stu-id="eead8-190">hello expressions can be any of hello preceding forms.</span></span>

<span data-ttu-id="eead8-191">Quando si usa la concatenazione, intera espressione hello deve essere racchiuso tra {}.</span><span class="sxs-lookup"><span data-stu-id="eead8-191">When using concatenation, hello entire expression must be surrounded with {}.</span></span> <span data-ttu-id="eead8-192">Ad esempio, {$(prop) + ' - ' + $(prop2)}.</span><span class="sxs-lookup"><span data-stu-id="eead8-192">For example, {$(prop) + ‘ - ’ + $(prop2)}.</span></span> |

<span data-ttu-id="eead8-193">Esempio hello non è ad esempio, un modello XML valido:</span><span class="sxs-lookup"><span data-stu-id="eead8-193">For example, hello following is not a valid XML template:</span></span>

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


<span data-ttu-id="eead8-194">Come spiegato in precedenza, quando si utilizza la concatenazione, le espressioni devono essere racchiuse tra parentesi graffe.</span><span class="sxs-lookup"><span data-stu-id="eead8-194">As explained above, when using concatenation, expressions must be wrapped in curly brackets.</span></span> <span data-ttu-id="eead8-195">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="eead8-195">For example:</span></span>

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

