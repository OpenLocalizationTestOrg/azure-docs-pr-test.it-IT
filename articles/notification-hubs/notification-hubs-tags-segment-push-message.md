---
title: aaaRouting ed espressioni Tag
description: Questo argomento illustra le espressioni di routing e tag per gli hub di notifica di Azure.
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: 0fffb3bb-8ed8-4e0f-89e8-0de24a47f644
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c2c60500f7469f1cb1a73a5cf63c221a9ad6cbb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="routing-and-tag-expressions"></a><span data-ttu-id="fc1d4-103">Espressioni di routing e tag</span><span class="sxs-lookup"><span data-stu-id="fc1d4-103">Routing and tag expressions</span></span>
## <a name="overview"></a><span data-ttu-id="fc1d4-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="fc1d4-104">Overview</span></span>
<span data-ttu-id="fc1d4-105">Espressioni tag consentono di tootarget set specifici di dispositivi o più specificamente registrazioni, quando si invia una notifica push tramite hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-105">Tag expressions enable you tootarget specific sets of devices, or more specifically registrations, when sending a push notification through Notification Hubs.</span></span>

## <a name="targeting-specific-registrations"></a><span data-ttu-id="fc1d4-106">Destinazione su registrazioni specifiche</span><span class="sxs-lookup"><span data-stu-id="fc1d4-106">Targeting specific registrations</span></span>
<span data-ttu-id="fc1d4-107">Hello solo modo tootarget notifica specifica registrazioni è tooassociate tag con essi, quindi come destinazione tali tag.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-107">hello only way tootarget specific notification registrations is tooassociate tags with them, then target those tags.</span></span> <span data-ttu-id="fc1d4-108">Come descritto in [gestione registrazione](notification-hubs-push-notification-registration-management.md), in push tooreceive ordine notifiche tooregister un dispositivo dispone di un'app di gestire in un hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-108">As discussed in [Registration Management](notification-hubs-push-notification-registration-management.md), in order tooreceive push notifications an app has tooregister a device handle on a notification hub.</span></span> <span data-ttu-id="fc1d4-109">Dopo aver creata una registrazione in un hub di notifica, back-end dell'applicazione hello può inviare tooit le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-109">Once a registration is created on a notification hub, hello application backend can send push notifications tooit.</span></span>
<span data-ttu-id="fc1d4-110">back-end dell'applicazione Hello è possibile scegliere hello registrazioni tootarget con una notifica specifica hello seguenti modi:</span><span class="sxs-lookup"><span data-stu-id="fc1d4-110">hello application backend can choose hello registrations tootarget with a specific notification in hello following ways:</span></span>

1. <span data-ttu-id="fc1d4-111">**Trasmissione**: tutte le registrazioni nell'hub di notifica hello ricevano una notifica di hello.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-111">**Broadcast**: all registrations in hello notification hub receive hello notification.</span></span>
2. <span data-ttu-id="fc1d4-112">**Tag**: tutte le registrazioni contenenti hello specificato tag ricevere una notifica di hello.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-112">**Tag**: all registrations that contain hello specified tag receive hello notification.</span></span>
3. <span data-ttu-id="fc1d4-113">**Espressione tag**: tutte le registrazioni il cui set di tag corrispondenza hello espressione specificata ricevono la notifica hello.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-113">**Tag expression**: all registrations whose set of tags match hello specified expression receive hello notification.</span></span>

## <a name="tags"></a><span data-ttu-id="fc1d4-114">Tag</span><span class="sxs-lookup"><span data-stu-id="fc1d4-114">Tags</span></span>
<span data-ttu-id="fc1d4-115">Un tag può essere qualsiasi stringa, i caratteri too120, contenente caratteri alfanumerici e hello seguenti caratteri non alfanumerici: '_', ' @', '#', '. ',':', '-'.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-115">A tag can be any string, up too120 characters, containing alphanumeric and hello following non-alphanumeric characters: ‘_’, ‘@’, ‘#’, ‘.’, ‘:’, ‘-’.</span></span> <span data-ttu-id="fc1d4-116">Hello esempio seguente viene illustrata un'applicazione da cui è possibile ricevere notifiche di tipo avviso popup su gruppi musicali specifici.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-116">hello following example shows an application from which you can receive toast notifications about specific music groups.</span></span> <span data-ttu-id="fc1d4-117">In questo scenario, le notifiche tooroute un modo semplice è toolabel registrazioni con tag che rappresentano gruppi musicali diversi hello, come illustrato di seguito immagine hello.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-117">In this scenario, a simple way tooroute notifications is toolabel registrations with tags that represent hello different bands, as in hello following picture.</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

<span data-ttu-id="fc1d4-118">In questa immagine, tag messaggio hello **Beatles** raggiunge solo hello tablet registrato con il tag di hello **Beatles**.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-118">In this picture, hello message tagged **Beatles** reaches only hello tablet that registered with hello tag **Beatles**.</span></span>

<span data-ttu-id="fc1d4-119">Per ulteriori informazioni sulla creazione di registrazioni per i tag, vedere [Gestione delle registrazioni](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="fc1d4-119">For more information about creating registrations for tags, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

<span data-ttu-id="fc1d4-120">È possibile inviare notifiche tootags utilizzando hello inviare metodi di notifiche di hello `Microsoft.Azure.NotificationHubs.NotificationHubClient` classe hello [gli hub di notifica di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-120">You can send notifications tootags using hello send notifications methods of hello `Microsoft.Azure.NotificationHubs.NotificationHubClient` class in hello [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span></span> <span data-ttu-id="fc1d4-121">È anche possibile usare Node.js o hello API REST di notifiche Push.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-121">You can also use Node.js, or hello Push Notifications REST APIs.</span></span>  <span data-ttu-id="fc1d4-122">Di seguito è riportato un esempio di utilizzo hello SDK.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-122">Here's an example using hello SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




<span data-ttu-id="fc1d4-123">Tag non è necessario pre-provisioning toobe e possono fare riferimento a concetti specifici dell'app toomultiple.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-123">Tags do not have toobe pre-provisioned and can refer toomultiple app-specific concepts.</span></span> <span data-ttu-id="fc1d4-124">In questo modo gli utenti di questa applicazione di esempio possono ad esempio, commentare le bande e desidera avvisi popup tooreceive, non solo per i commenti di hello sui propri gruppi Preferiti, ma anche per tutti i commenti degli amici, indipendentemente dalla banda hello in cui si sta Commentando.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-124">For example, users of this example application can comment on bands and want tooreceive toasts, not only for hello comments on their favorite bands, but also for all comments from their friends, regardless of hello band on which they are commenting.</span></span> <span data-ttu-id="fc1d4-125">Hello seguente immagine mostra un esempio di questo scenario:</span><span class="sxs-lookup"><span data-stu-id="fc1d4-125">hello following picture shows an example of this scenario:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

<span data-ttu-id="fc1d4-126">In questa immagine, Alice è interessata a ricevere aggiornamenti per hello Beatles e Bob è interessato a ricevere aggiornamenti per hello Wailers.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-126">In this picture, Alice is interested in updates for hello Beatles, and Bob is interested in updates for hello Wailers.</span></span> <span data-ttu-id="fc1d4-127">Bob è anche interessato ai commenti di Charlie e Charlie è interessato hello Wailers.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-127">Bob is also interested in Charlie’s comments, and Charlie is in interested in hello Wailers.</span></span> <span data-ttu-id="fc1d4-128">Quando viene inviata una notifica per commento di Charlie sui Beatles hello, sia Alice sia Bob la ricevono.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-128">When a notification is sent for Charlie’s comment on hello Beatles, both Alice and Bob receive it.</span></span>

<span data-ttu-id="fc1d4-129">Sebbene sia possibile codificare più aspetti nei tag (ad esempio, "gruppo_Beatles" o "segue_Charlie"), i tag sono semplici stringhe e non proprietà con valori.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-129">While you can encode multiple concerns in tags (for example, “band_Beatles” or “follows_Charlie”), tags are simple strings and not properties with values.</span></span> <span data-ttu-id="fc1d4-130">La registrazione viene stabilita la corrispondenza solo hello presenza o assenza di un tag specifico.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-130">A registration is matched only on hello presence or absence of a specific tag.</span></span>

<span data-ttu-id="fc1d4-131">Per un'esercitazione dettagliata su come i tag per l'invio di gruppi toointerest toouse, vedere [delle ultime notizie](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span><span class="sxs-lookup"><span data-stu-id="fc1d4-131">For a full step-by-step tutorial on how toouse tags for sending toointerest groups, see [Breaking News](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span></span>

## <a name="using-tags-tootarget-users"></a><span data-ttu-id="fc1d4-132">Tag tootarget utenti</span><span class="sxs-lookup"><span data-stu-id="fc1d4-132">Using tags tootarget users</span></span>
<span data-ttu-id="fc1d4-133">Un altro modo toouse tag è tooidentify tutti i dispositivi di hello di un determinato utente.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-133">Another way toouse tags is tooidentify all hello devices of a particular user.</span></span> <span data-ttu-id="fc1d4-134">Le registrazioni possono essere contrassegnate con un tag che contiene un id utente, come in hello seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="fc1d4-134">Registrations can be tagged with a tag that contains a user id, as in hello following picture:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

<span data-ttu-id="fc1d4-135">In questa immagine, UID: Alice tag messaggio hello raggiunge tutte le registrazioni con tag UID: Alice; di conseguenza, tutti i dispositivi di Alice.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-135">In this picture, hello message tagged uid:Alice reaches all registrations tagged uid:Alice; hence, all of Alice’s devices.</span></span>

## <a name="tag-expressions"></a><span data-ttu-id="fc1d4-136">Espressioni tag</span><span class="sxs-lookup"><span data-stu-id="fc1d4-136">Tag expressions</span></span>
<span data-ttu-id="fc1d4-137">Vi sono casi in cui una notifica ha tootarget un set di registrazioni identificato non da un singolo tag, ma con un'espressione booleana su tag.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-137">There are cases in which a notification has tootarget a set of registrations that is identified not by a single tag, but by a Boolean expression on tags.</span></span>

<span data-ttu-id="fc1d4-138">Si consideri un'applicazione sportiva che invia un promemoria tooeveryone Boston su una partita tra hello Red Sox e Cardinals.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-138">Consider a sports application that sends a reminder tooeveryone in Boston about a game between hello Red Sox and Cardinals.</span></span> <span data-ttu-id="fc1d4-139">Se l'applicazione client hello registra i tag relativi all'interesse per squadre e località, notifica hello deve essere tooeveryone destinazione Boston interessati hello Red Sox o hello Cardinals.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-139">If hello client app registers tags about interest in teams and location, then hello notification should be targeted tooeveryone in Boston who is interested in either hello Red Sox or hello Cardinals.</span></span> <span data-ttu-id="fc1d4-140">Questa condizione può essere espresso con hello espressione booleana seguente:</span><span class="sxs-lookup"><span data-stu-id="fc1d4-140">This condition can be expressed with hello following Boolean expression:</span></span>

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

<span data-ttu-id="fc1d4-141">Le espressioni tag possono contenere tutti gli operatori booleani, quali AND (&&), OR (||) e NOT (!).</span><span class="sxs-lookup"><span data-stu-id="fc1d4-141">Tag expressions can contain all Boolean operators, such as AND (&&), OR (||), and NOT (!).</span></span> <span data-ttu-id="fc1d4-142">Possono inoltre contenere parentesi.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-142">They can also contain parentheses.</span></span> <span data-ttu-id="fc1d4-143">Espressioni tag sono tag too20 limitato se contengono solo OR; in caso contrario sono tag too6 limitato.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-143">Tag expressions are limited too20 tags if they contain only ORs; otherwise they are limited too6 tags.</span></span>

<span data-ttu-id="fc1d4-144">Di seguito è riportato un esempio per l'invio di notifiche con espressioni tag usando hello SDK.</span><span class="sxs-lookup"><span data-stu-id="fc1d4-144">Here's an example for sending notifications with tag expressions using hello SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    String userTag = "(location_Boston && !follows_Cardinals)";    

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You want info on hello Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You want info on hello Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
