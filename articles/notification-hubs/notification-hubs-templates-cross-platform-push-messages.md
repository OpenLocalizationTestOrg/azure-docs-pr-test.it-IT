---
title: Modelli
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
ms.openlocfilehash: 1ca24a4bf08ecdbe1c1e47a931613144309a04a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="templates"></a><span data-ttu-id="99414-103">Modelli</span><span class="sxs-lookup"><span data-stu-id="99414-103">Templates</span></span>
## <a name="overview"></a><span data-ttu-id="99414-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="99414-104">Overview</span></span>
<span data-ttu-id="99414-105">I modelli consentono alle applicazioni client di specificare il formato esatto delle notifiche da ricevere.</span><span class="sxs-lookup"><span data-stu-id="99414-105">Templates enable a client application to specify the exact format of the notifications it wants to receive.</span></span> <span data-ttu-id="99414-106">Mediante i modelli, le app possono ottenere diversi vantaggi, fra cui i seguenti:</span><span class="sxs-lookup"><span data-stu-id="99414-106">Using templates, an app can realize several different benefits, including the following :</span></span>

* <span data-ttu-id="99414-107">Un back-end indipendente dalla piattaforma</span><span class="sxs-lookup"><span data-stu-id="99414-107">A platform-agnostic backend</span></span>
* <span data-ttu-id="99414-108">Notifiche personalizzate</span><span class="sxs-lookup"><span data-stu-id="99414-108">Personalized notifications</span></span>
* <span data-ttu-id="99414-109">Indipendenza dalla versione del client</span><span class="sxs-lookup"><span data-stu-id="99414-109">Client-version independence</span></span>
* <span data-ttu-id="99414-110">Localizzazione semplice</span><span class="sxs-lookup"><span data-stu-id="99414-110">Easy localization</span></span>

<span data-ttu-id="99414-111">In questa sezione vengono forniti due esempi dettagliati di come utilizzare modelli per inviare notifiche indipendenti dalla piattaforma destinate a i dispositivi di tutte le piattaforme e per personalizzare la notifica di trasmissione per ciascun dispositivo.</span><span class="sxs-lookup"><span data-stu-id="99414-111">This section provides two in-depth examples of how to use templates to send platform-agnostic notifications targeting all your devices across platforms, and to personalize broadcast notification to each device.</span></span>

## <a name="using-templates-cross-platform"></a><span data-ttu-id="99414-112">Utilizzo di modelli multipiattaforma</span><span class="sxs-lookup"><span data-stu-id="99414-112">Using templates cross-platform</span></span>
<span data-ttu-id="99414-113">Il metodo standard per inviare notifiche push consiste nell'inviare, per ciascuna notifica, uno specifico payload dei servizi di notifica della piattaforma (WNS, servizio APN).</span><span class="sxs-lookup"><span data-stu-id="99414-113">The standard way to send push notifications is to send, for each notification that is to be sent, a specific payload to platform notification services (WNS, APNS).</span></span> <span data-ttu-id="99414-114">Per inviare un avviso al servizio APN, ad esempio, il payload è un oggetto Json nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="99414-114">For example, to send an alert to APNS, the payload is a Json object of the following form:</span></span>

    {"aps": {"alert" : "Hello!" }}

<span data-ttu-id="99414-115">Per inviare un messaggio di avviso popup simile in un'applicazione di Windows Store, il payload XML è il seguente:</span><span class="sxs-lookup"><span data-stu-id="99414-115">To send a similar toast message on a Windows Store application, the XML payload is as follows:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

<span data-ttu-id="99414-116">È possibile creare payload simili per MPNS (Windows Phone) e piattaforme GCM (Android).</span><span class="sxs-lookup"><span data-stu-id="99414-116">You can create similar payloads for MPNS (Windows Phone) and GCM (Android) platforms.</span></span>

<span data-ttu-id="99414-117">Tale requisito impone al back-end dell'app la produzione di payload diversi per ciascuna piattaforma e di fatto rende il back-end responsabile di parte del livello di presentazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="99414-117">This requirement forces the app backend to produce different payloads for each platform, and effectively makes the backend responsible for part of the presentation layer of the app.</span></span> <span data-ttu-id="99414-118">Alcuni dei problemi riguardano la localizzazione e i layout grafici (soprattutto per applicazioni di Windows Store che comprendono notifiche per vari tipi di riquadri).</span><span class="sxs-lookup"><span data-stu-id="99414-118">Some concerns include localization and graphical layouts (especially for Windows Store apps that include notifications for various types of tiles).</span></span>

<span data-ttu-id="99414-119">La funzionalità del modello degli Hub di notifica consente a un'app client di creare registrazioni speciali, denominate registrazioni con modello, comprendenti un modello, oltre al set di tag.</span><span class="sxs-lookup"><span data-stu-id="99414-119">The Notification Hubs template feature enables a client app to create special registrations, called template registrations, which include, in addition to the set of tags, a template.</span></span> <span data-ttu-id="99414-120">La funzionalità del modello Hub di notifica consente a un'app client di associare i dispositivi con i modelli, indipendentemente dall'utilizzo di installazioni (scelta consigliata) o di registrazioni.</span><span class="sxs-lookup"><span data-stu-id="99414-120">The Notification Hubs template feature enables a client app to associate devices with templates whether you are working with Installations (preferred) or Registrations.</span></span> <span data-ttu-id="99414-121">Dati gli esempi di payload precedenti, le sole informazioni indipendenti dalla piattaforma consistono nel messaggio di avviso effettivo (Hello!).</span><span class="sxs-lookup"><span data-stu-id="99414-121">Given the preceding payload examples, the only platform-independent information is the actual alert message (Hello!).</span></span> <span data-ttu-id="99414-122">Un modello è un set di istruzioni per l'Hub di notifica circa la modalità di formattazione di un messaggio indipendente dalla piattaforma per la registrazione di una determinata app client.</span><span class="sxs-lookup"><span data-stu-id="99414-122">A template is a set of instructions for the Notification Hub on how to format a platform-independent message for the registration of that specific client app.</span></span> <span data-ttu-id="99414-123">Nell'esempio precedente, il messaggio indipendente dalla piattaforma consiste in una singola proprietà: **message = Hello!**.</span><span class="sxs-lookup"><span data-stu-id="99414-123">In the preceding example, the platform independent message is a single property: **message = Hello!**.</span></span>

<span data-ttu-id="99414-124">Nell'immagine seguente viene illustrato il processo indicato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="99414-124">The following picture illustrates the above process:</span></span>

![](./media/notification-hubs-templates/notification-hubs-hello.png)

<span data-ttu-id="99414-125">Il modello per la registrazione dell'app client iOS è il seguente:</span><span class="sxs-lookup"><span data-stu-id="99414-125">The template for the iOS client app registration is as follows:</span></span>

    {"aps": {"alert": "$(message)"}}

<span data-ttu-id="99414-126">Il modello corrispondente per l'applicazione client di Windows Store è:</span><span class="sxs-lookup"><span data-stu-id="99414-126">The corresponding template for the Windows Store client app is:</span></span>

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

<span data-ttu-id="99414-127">Si noti che il messaggio effettivo viene sostituito dall'espressione $(message).</span><span class="sxs-lookup"><span data-stu-id="99414-127">Notice that the actual message is substituted for the expression $(message).</span></span> <span data-ttu-id="99414-128">Tale espressione indica all'Hub di notifica, ogni volta che viene inviato un messaggio a quella particolare registrazione, di creare un messaggio successivo, commutandolo nel valore comune.</span><span class="sxs-lookup"><span data-stu-id="99414-128">This expression instructs the Notification Hub, whenever it sends a message to this particular registration, to build a message that follows it and switches in the common value.</span></span>

<span data-ttu-id="99414-129">Se si utilizza il modello di installazione, la chiave dei "modelli" di installazione contiene un JSON composto da più modelli.</span><span class="sxs-lookup"><span data-stu-id="99414-129">If you are working with Installation model, the installation “templates” key holds a JSON of multiple templates.</span></span> <span data-ttu-id="99414-130">Se si utilizza il modello di registrazione, l'applicazione client può creare più registrazioni per poter utilizzare più modelli: ad esempio, un modello per i messaggi di avviso e un modello per gli aggiornamenti dei riquadri.</span><span class="sxs-lookup"><span data-stu-id="99414-130">If you are working with Registration model, the client application can create multiple registrations in order to use multiple templates; for example, a template for alert messages and a template for tile updates.</span></span> <span data-ttu-id="99414-131">Inoltre, le applicazioni client possono unire registrazioni native (registrazioni senza modello) e registrazioni con modello.</span><span class="sxs-lookup"><span data-stu-id="99414-131">Client applications can also mix native registrations (registrations with no template) and template registrations.</span></span>

<span data-ttu-id="99414-132">L'Hub di notifica invia una notifica per ciascun modello senza considerare se appartengono alla stessa app client.</span><span class="sxs-lookup"><span data-stu-id="99414-132">The Notification Hub sends one notification for each template without considering whether they belong to the same client app.</span></span> <span data-ttu-id="99414-133">Questo comportamento può essere utilizzato per convertire notifiche indipendenti dalla piattaforma in più notifiche.</span><span class="sxs-lookup"><span data-stu-id="99414-133">This behavior can be used to translate platform-independent notifications into more notifications.</span></span> <span data-ttu-id="99414-134">Ad esempio, lo stesso messaggio indipendente dalla piattaforma all'Hub di notifica può essere facilmente convertito in un avviso popup e in un aggiornamento del riquadro, senza essere rilevato dal back-end.</span><span class="sxs-lookup"><span data-stu-id="99414-134">For example, the same platform independent message to the Notification Hub can be seamlessly translated in a toast alert and a tile update, without requiring the backend to be aware of it.</span></span> <span data-ttu-id="99414-135">Si noti che alcune piattaforme (ad esempio, iOS) potrebbero comprimere più notifiche allo stesso dispositivo se queste vengono inviate in un breve periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="99414-135">Note that some platforms (for example, iOS) might collapse multiple notifications to the same device if they are sent in a short period of time.</span></span>

## <a name="using-templates-for-personalization"></a><span data-ttu-id="99414-136">Utilizzo di modelli per la personalizzazione</span><span class="sxs-lookup"><span data-stu-id="99414-136">Using templates for personalization</span></span>
<span data-ttu-id="99414-137">Un altro vantaggio derivante dall'utilizzo di modelli è la possibilità di utilizzare gli Hub di notifica per eseguire la personalizzazione delle notifiche per registrazione.</span><span class="sxs-lookup"><span data-stu-id="99414-137">Another advantage to using templates is the ability to use Notification Hubs to perform per-registration personalization of notifications.</span></span> <span data-ttu-id="99414-138">Si consideri ad esempio un'app meteo che visualizza un riquadro sulle condizioni meteorologiche relative a un luogo specifico.</span><span class="sxs-lookup"><span data-stu-id="99414-138">For example, consider a weather app that displays a tile with the weather conditions at a specific location.</span></span> <span data-ttu-id="99414-139">Un utente può scegliere tra gradi Celsius o Fahrenheit e una previsione singola o di cinque giorni.</span><span class="sxs-lookup"><span data-stu-id="99414-139">A user can choose between Celsius or Fahrenheit degrees, and a single or five-day forecast.</span></span> <span data-ttu-id="99414-140">Mediante i modelli, ciascuna installazione dell'app client può registrare il formato richiesto (1 giorno in gradi Celsius 1 giorno in gradi Fahrenheit, 5 giorni in gradi Celsius, 5 giorni in gradi Fahrenheit), e far sì che il back-end invii un unico messaggio contenente tutte le informazioni necessarie per compilare i modelli (ad esempio una previsione di cinque giorni con gradi Celsius e Fahrenheit).</span><span class="sxs-lookup"><span data-stu-id="99414-140">Using templates, each client app installation can register for the format required (1-day Celsius, 1-day Fahrenheit, 5-days Celsius, 5-days Fahrenheit), and have the backend send a single message that contains all the information required to fill those templates (for example, a five-day forecast with Celsius and Fahrenheit degrees).</span></span>

<span data-ttu-id="99414-141">Il modello per la previsione di un giorno in gradi Celsius è il seguente:</span><span class="sxs-lookup"><span data-stu-id="99414-141">The template for the one-day forecast with Celsius temperatures is as follows:</span></span>

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

<span data-ttu-id="99414-142">Il messaggio inviato all'Hub di notifica contiene tutte le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="99414-142">The message sent to the Notification Hub contains all the following properties:</span></span>

<table border="1">

<tr><td><span data-ttu-id="99414-143">day1_image</span><span class="sxs-lookup"><span data-stu-id="99414-143">day1_image</span></span></td><td><span data-ttu-id="99414-144">day2_image</span><span class="sxs-lookup"><span data-stu-id="99414-144">day2_image</span></span></td><td><span data-ttu-id="99414-145">day3_image</span><span class="sxs-lookup"><span data-stu-id="99414-145">day3_image</span></span></td><td><span data-ttu-id="99414-146">day4_image</span><span class="sxs-lookup"><span data-stu-id="99414-146">day4_image</span></span></td><td><span data-ttu-id="99414-147">day5_image</span><span class="sxs-lookup"><span data-stu-id="99414-147">day5_image</span></span></td></tr>

<tr><td><span data-ttu-id="99414-148">day1_tempC</span><span class="sxs-lookup"><span data-stu-id="99414-148">day1_tempC</span></span></td><td><span data-ttu-id="99414-149">day2_tempC</span><span class="sxs-lookup"><span data-stu-id="99414-149">day2_tempC</span></span></td><td><span data-ttu-id="99414-150">day3_tempC</span><span class="sxs-lookup"><span data-stu-id="99414-150">day3_tempC</span></span></td><td><span data-ttu-id="99414-151">day4_tempC</span><span class="sxs-lookup"><span data-stu-id="99414-151">day4_tempC</span></span></td><td><span data-ttu-id="99414-152">day5_tempC</span><span class="sxs-lookup"><span data-stu-id="99414-152">day5_tempC</span></span></td></tr>

<tr><td><span data-ttu-id="99414-153">day1_tempF</span><span class="sxs-lookup"><span data-stu-id="99414-153">day1_tempF</span></span></td><td><span data-ttu-id="99414-154">day2_tempF</span><span class="sxs-lookup"><span data-stu-id="99414-154">day2_tempF</span></span></td><td><span data-ttu-id="99414-155">day3_tempF</span><span class="sxs-lookup"><span data-stu-id="99414-155">day3_tempF</span></span></td><td><span data-ttu-id="99414-156">day4_tempF</span><span class="sxs-lookup"><span data-stu-id="99414-156">day4_tempF</span></span></td><td><span data-ttu-id="99414-157">day5_tempF</span><span class="sxs-lookup"><span data-stu-id="99414-157">day5_tempF</span></span></td></tr>
</table><br/>

<span data-ttu-id="99414-158">Utilizzando questo modello, il back-end invia solo un unico messaggio senza dover memorizzare opzioni di personalizzazione specifiche per gli utenti dell'app.</span><span class="sxs-lookup"><span data-stu-id="99414-158">By using this pattern, the backend only sends a single message without having to store specific personalization options for the app users.</span></span> <span data-ttu-id="99414-159">Nell'immagine seguente viene illustrato tale scenario:</span><span class="sxs-lookup"><span data-stu-id="99414-159">The following picture illustrates this scenario:</span></span>

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-to-register-templates"></a><span data-ttu-id="99414-160">Come registrare i modelli</span><span class="sxs-lookup"><span data-stu-id="99414-160">How to register templates</span></span>
<span data-ttu-id="99414-161">Per la registrazione dei modelli mediante il modello di installazione (scelta consigliata) o il modello di registrazione, vedere [Gestione delle registrazioni](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="99414-161">To register with templates using the Installation model (preferred), or the Registration model, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

## <a name="template-expression-language"></a><span data-ttu-id="99414-162">Linguaggio di espressione dei modelli</span><span class="sxs-lookup"><span data-stu-id="99414-162">Template expression language</span></span>
<span data-ttu-id="99414-163">I modelli sono limitati ai formati di documento XML o JSON.</span><span class="sxs-lookup"><span data-stu-id="99414-163">Templates are limited to XML or JSON document formats.</span></span> <span data-ttu-id="99414-164">Inoltre, è possibile inserire solo le espressioni in particolari punti: ad esempio, attributi dei nodi o valori per il formato XML, valori delle proprietà di stringa per il formato JSON.</span><span class="sxs-lookup"><span data-stu-id="99414-164">Also, you can only place expressions in particular places; for example, node attributes or values for XML, string property values for JSON.</span></span>

<span data-ttu-id="99414-165">Nella tabella seguente viene descritto il linguaggio consentito nei modelli:</span><span class="sxs-lookup"><span data-stu-id="99414-165">The following table shows the language allowed in templates:</span></span>

| <span data-ttu-id="99414-166">Espressione</span><span class="sxs-lookup"><span data-stu-id="99414-166">Expression</span></span> | <span data-ttu-id="99414-167">Descrizione</span><span class="sxs-lookup"><span data-stu-id="99414-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="99414-168">$(prop)</span><span class="sxs-lookup"><span data-stu-id="99414-168">$(prop)</span></span> |<span data-ttu-id="99414-169">Riferimento a una proprietà di evento con il nome specificato.</span><span class="sxs-lookup"><span data-stu-id="99414-169">Reference to an event property with the given name.</span></span> <span data-ttu-id="99414-170">I nomi delle proprietà non distinguono tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="99414-170">Property names are not case-sensitive.</span></span> <span data-ttu-id="99414-171">Questa espressione viene risolta nel valore di testo della proprietà o in una stringa vuota se la proprietà non è presente.</span><span class="sxs-lookup"><span data-stu-id="99414-171">This expression resolves into the property’s text value or into an empty string if the property is not present.</span></span> |
| <span data-ttu-id="99414-172">$(prop, n)</span><span class="sxs-lookup"><span data-stu-id="99414-172">$(prop, n)</span></span> |<span data-ttu-id="99414-173">Come in precedenza, ma il testo viene esplicitamente troncato dopo n caratteri, ad esempio $(title, 20) tronca il contenuto della proprietà del riquadro dopo 20 caratteri.</span><span class="sxs-lookup"><span data-stu-id="99414-173">As above, but the text is explicitly clipped at n characters, for example $(title, 20) clips the contents of the title property at 20 characters.</span></span> |
| <span data-ttu-id="99414-174">.(prop, n)</span><span class="sxs-lookup"><span data-stu-id="99414-174">.(prop, n)</span></span> |<span data-ttu-id="99414-175">Come in precedenza, ma vengono aggiunti tre punti alla fine del testo troncato.</span><span class="sxs-lookup"><span data-stu-id="99414-175">As above, but the text is suffixed with three dots as it is clipped.</span></span> <span data-ttu-id="99414-176">La dimensione totale della stringa troncata e del suffisso non supera n caratteri.</span><span class="sxs-lookup"><span data-stu-id="99414-176">The total size of the clipped string and the suffix does not exceed n characters.</span></span> <span data-ttu-id="99414-177">.(title, 20) con una proprietà di input "Questa è la riga del titolo" restituisce **Questa è la riga...**</span><span class="sxs-lookup"><span data-stu-id="99414-177">.(title, 20) with an input property of “This is the title line” results in **This is the title...**</span></span> |
| <span data-ttu-id="99414-178">%(prop)</span><span class="sxs-lookup"><span data-stu-id="99414-178">%(prop)</span></span> |<span data-ttu-id="99414-179">È simile a $(name), a eccezione del fatto che l'output è codificato in formato URI.</span><span class="sxs-lookup"><span data-stu-id="99414-179">Similar to $(name) except that the output is URI-encoded.</span></span> |
| <span data-ttu-id="99414-180">#(prop)</span><span class="sxs-lookup"><span data-stu-id="99414-180">#(prop)</span></span> |<span data-ttu-id="99414-181">Utilizzata nei modelli JSON (ad esempio, per modelli iOS e Android).</span><span class="sxs-lookup"><span data-stu-id="99414-181">Used in JSON templates (for example, for iOS and Android templates).</span></span><br><br><span data-ttu-id="99414-182">Questa funzione opera esattamente come l'espressione $(prop) specificata in precedenza, salvo quando viene utilizzata nei modelli JSON (ad esempio, nei modelli Apple).</span><span class="sxs-lookup"><span data-stu-id="99414-182">This function works exactly the same as $(prop) previously specified, except when used in JSON templates (for example, Apple templates).</span></span> <span data-ttu-id="99414-183">In questo caso, se questa funzione non è racchiusa tra "{','}", ad esempio 'myJsonProperty' : '#(name)', e restituisce un numero in formato Javascript, ad esempio regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, l'output JSON sarà un numero.</span><span class="sxs-lookup"><span data-stu-id="99414-183">In this case, if this function is not surrounded by “{‘,’}” (for example, ‘myJsonProperty’ : ‘#(name)’), and it evaluates to a number in Javascript format, for example, regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, then the output JSON is a number.</span></span><br><br><span data-ttu-id="99414-184">Ad esempio, ' badge : '#(name)' diventa 'badge' : 40 (e non '40').</span><span class="sxs-lookup"><span data-stu-id="99414-184">For example, ‘badge : ‘#(name)’ becomes ‘badge’ : 40 (and not ‘40‘).</span></span> |
| <span data-ttu-id="99414-185">'text' o "text"</span><span class="sxs-lookup"><span data-stu-id="99414-185">‘text’ or “text”</span></span> |<span data-ttu-id="99414-186">Valore letterale.</span><span class="sxs-lookup"><span data-stu-id="99414-186">A literal.</span></span> <span data-ttu-id="99414-187">I valori letterali contengono testo arbitrario racchiuso tra virgolette singole o doppie.</span><span class="sxs-lookup"><span data-stu-id="99414-187">Literals contain arbitrary text enclosed in single or double quotes.</span></span> |
| <span data-ttu-id="99414-188">expr1 + expr2</span><span class="sxs-lookup"><span data-stu-id="99414-188">expr1 + expr2</span></span> |<span data-ttu-id="99414-189">Operatore di concatenazione che unisce due espressioni in una singola stringa.</span><span class="sxs-lookup"><span data-stu-id="99414-189">The concatenation operator joining two expressions into a single string.</span></span> |

<span data-ttu-id="99414-190">Il formato delle espressioni può essere uno dei precedenti.</span><span class="sxs-lookup"><span data-stu-id="99414-190">The expressions can be any of the preceding forms.</span></span>

<span data-ttu-id="99414-191">Quando si utilizza la concatenazione, l'intera espressione deve essere racchiusa tra parentesi graffe {}.</span><span class="sxs-lookup"><span data-stu-id="99414-191">When using concatenation, the entire expression must be surrounded with {}.</span></span> <span data-ttu-id="99414-192">Ad esempio, {$(prop) + ' - ' + $(prop2)}.</span><span class="sxs-lookup"><span data-stu-id="99414-192">For example, {$(prop) + ‘ - ’ + $(prop2)}.</span></span> |

<span data-ttu-id="99414-193">Ad esempio, il modello XML seguente non è valido:</span><span class="sxs-lookup"><span data-stu-id="99414-193">For example, the following is not a valid XML template:</span></span>

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


<span data-ttu-id="99414-194">Come spiegato in precedenza, quando si utilizza la concatenazione, le espressioni devono essere racchiuse tra parentesi graffe.</span><span class="sxs-lookup"><span data-stu-id="99414-194">As explained above, when using concatenation, expressions must be wrapped in curly brackets.</span></span> <span data-ttu-id="99414-195">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="99414-195">For example:</span></span>

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

