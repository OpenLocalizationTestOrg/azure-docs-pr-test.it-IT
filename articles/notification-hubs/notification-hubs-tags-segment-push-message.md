---
title: Espressioni di routing e tag
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
ms.openlocfilehash: 18faa88641623e1248d6a33bc2d87099e1c9f624
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="routing-and-tag-expressions"></a><span data-ttu-id="1a700-103">Espressioni di routing e tag</span><span class="sxs-lookup"><span data-stu-id="1a700-103">Routing and tag expressions</span></span>
## <a name="overview"></a><span data-ttu-id="1a700-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="1a700-104">Overview</span></span>
<span data-ttu-id="1a700-105">Le espressioni tag consentono di avere come destinazione set specifici di dispositivi, o più specificamente registrazioni, quando si invia una notifica push tramite hub di notifica.</span><span class="sxs-lookup"><span data-stu-id="1a700-105">Tag expressions enable you to target specific sets of devices, or more specifically registrations, when sending a push notification through Notification Hubs.</span></span>

## <a name="targeting-specific-registrations"></a><span data-ttu-id="1a700-106">Destinazione su registrazioni specifiche</span><span class="sxs-lookup"><span data-stu-id="1a700-106">Targeting specific registrations</span></span>
<span data-ttu-id="1a700-107">L'unico modo per avere come destinazione registrazioni di notifiche specifiche consiste nell'associare tag ad esse, quindi utilizzare come destinazione tali tag.</span><span class="sxs-lookup"><span data-stu-id="1a700-107">The only way to target specific notification registrations is to associate tags with them, then target those tags.</span></span> <span data-ttu-id="1a700-108">Come descritto in [Gestione delle registrazioni](notification-hubs-push-notification-registration-management.md), per ricevere le notifiche push un'app deve registrare un handle di dispositivo in un hub di notifica push.</span><span class="sxs-lookup"><span data-stu-id="1a700-108">As discussed in [Registration Management](notification-hubs-push-notification-registration-management.md), in order to receive push notifications an app has to register a device handle on a notification hub.</span></span> <span data-ttu-id="1a700-109">Dopo aver creato una registrazione su un hub di notifica, il back-end dell'applicazione può inviare ad esso notifiche push.</span><span class="sxs-lookup"><span data-stu-id="1a700-109">Once a registration is created on a notification hub, the application backend can send push notifications to it.</span></span>
<span data-ttu-id="1a700-110">Il back-end dell'applicazione può scegliere le registrazioni da utilizzare come destinazione con una notifica specifica nei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1a700-110">The application backend can choose the registrations to target with a specific notification in the following ways:</span></span>

1. <span data-ttu-id="1a700-111">**Trasmissione**: tutte le registrazioni nell'hub di notifica ricevono la notifica.</span><span class="sxs-lookup"><span data-stu-id="1a700-111">**Broadcast**: all registrations in the notification hub receive the notification.</span></span>
2. <span data-ttu-id="1a700-112">**Tag**: tutte le registrazioni contenenti il tag specificato ricevono la notifica.</span><span class="sxs-lookup"><span data-stu-id="1a700-112">**Tag**: all registrations that contain the specified tag receive the notification.</span></span>
3. <span data-ttu-id="1a700-113">**Espressione tag**: tutte le registrazioni il cui set di tag corrisponde all'espressione specificata ricevono la notifica.</span><span class="sxs-lookup"><span data-stu-id="1a700-113">**Tag expression**: all registrations whose set of tags match the specified expression receive the notification.</span></span>

## <a name="tags"></a><span data-ttu-id="1a700-114">Tag</span><span class="sxs-lookup"><span data-stu-id="1a700-114">Tags</span></span>
<span data-ttu-id="1a700-115">Un tag può essere qualsiasi stringa, fino a 120 caratteri alfanumerici e i seguenti caratteri non alfanumerici: '_', ' @', '#', '. ',':', '-'.</span><span class="sxs-lookup"><span data-stu-id="1a700-115">A tag can be any string, up to 120 characters, containing alphanumeric and the following non-alphanumeric characters: ‘_’, ‘@’, ‘#’, ‘.’, ‘:’, ‘-’.</span></span> <span data-ttu-id="1a700-116">Nell'esempio seguente viene illustrata un'applicazione da cui è possibile ricevere notifiche di tipo avviso popup su gruppi musicali specifici.</span><span class="sxs-lookup"><span data-stu-id="1a700-116">The following example shows an application from which you can receive toast notifications about specific music groups.</span></span> <span data-ttu-id="1a700-117">In questo scenario, un modo semplice per instradare le notifiche è etichettare le registrazioni con tag che rappresentano i diversi gruppi musicali, come illustrato nell'immagine seguente.</span><span class="sxs-lookup"><span data-stu-id="1a700-117">In this scenario, a simple way to route notifications is to label registrations with tags that represent the different bands, as in the following picture.</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

<span data-ttu-id="1a700-118">In questa immagine il messaggio con tag **Beatles** raggiunge solo il tablet registrato con il tag **Beatles**.</span><span class="sxs-lookup"><span data-stu-id="1a700-118">In this picture, the message tagged **Beatles** reaches only the tablet that registered with the tag **Beatles**.</span></span>

<span data-ttu-id="1a700-119">Per ulteriori informazioni sulla creazione di registrazioni per i tag, vedere [Gestione delle registrazioni](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="1a700-119">For more information about creating registrations for tags, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

<span data-ttu-id="1a700-120">È possibile inviare notifiche ai tag usando i metodi di notifiche di invio della classe `Microsoft.Azure.NotificationHubs.NotificationHubClient` nell’SDK [hub di notifica di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) .</span><span class="sxs-lookup"><span data-stu-id="1a700-120">You can send notifications to tags using the send notifications methods of the `Microsoft.Azure.NotificationHubs.NotificationHubClient` class in the [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span></span> <span data-ttu-id="1a700-121">È inoltre possibile utilizzare Node.js o le API REST delle notifiche push.</span><span class="sxs-lookup"><span data-stu-id="1a700-121">You can also use Node.js, or the Push Notifications REST APIs.</span></span>  <span data-ttu-id="1a700-122">Di seguito è riportato un esempio con l’SDK.</span><span class="sxs-lookup"><span data-stu-id="1a700-122">Here's an example using the SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




<span data-ttu-id="1a700-123">Per tag non deve necessariamente essere eseguito il pre-provisioning e questi possono fare riferimento a più concetti specifici dell'app.</span><span class="sxs-lookup"><span data-stu-id="1a700-123">Tags do not have to be pre-provisioned and can refer to multiple app-specific concepts.</span></span> <span data-ttu-id="1a700-124">Ad esempio, gli utenti di questa applicazione di esempio possono commentare i gruppi e desiderano ricevere avvisi popup, non solo per i commenti sui propri gruppi preferiti, ma anche per tutti i commenti degli amici, indipendentemente dal gruppo che stanno commentando.</span><span class="sxs-lookup"><span data-stu-id="1a700-124">For example, users of this example application can comment on bands and want to receive toasts, not only for the comments on their favorite bands, but also for all comments from their friends, regardless of the band on which they are commenting.</span></span> <span data-ttu-id="1a700-125">Nell'immagine seguente viene illustrato un esempio di questo scenario:</span><span class="sxs-lookup"><span data-stu-id="1a700-125">The following picture shows an example of this scenario:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

<span data-ttu-id="1a700-126">In questa immagine, Alice è interessata a ricevere aggiornamenti sui Beatles e Bob è interessato a ricevere aggiornamenti sui Wailers.</span><span class="sxs-lookup"><span data-stu-id="1a700-126">In this picture, Alice is interested in updates for the Beatles, and Bob is interested in updates for the Wailers.</span></span> <span data-ttu-id="1a700-127">Bob è anche interessato ai commenti di Charlie e Charlie è interessato ai Wailers.</span><span class="sxs-lookup"><span data-stu-id="1a700-127">Bob is also interested in Charlie’s comments, and Charlie is in interested in the Wailers.</span></span> <span data-ttu-id="1a700-128">Quando viene inviata una notifica per un commento di Charlie sui Beatles, sia Alice che Bob la ricevono.</span><span class="sxs-lookup"><span data-stu-id="1a700-128">When a notification is sent for Charlie’s comment on the Beatles, both Alice and Bob receive it.</span></span>

<span data-ttu-id="1a700-129">Sebbene sia possibile codificare più aspetti nei tag (ad esempio, "gruppo_Beatles" o "segue_Charlie"), i tag sono semplici stringhe e non proprietà con valori.</span><span class="sxs-lookup"><span data-stu-id="1a700-129">While you can encode multiple concerns in tags (for example, “band_Beatles” or “follows_Charlie”), tags are simple strings and not properties with values.</span></span> <span data-ttu-id="1a700-130">Esiste una corrispondenza per la registrazione solo in presenza o assenza di un tag specifico.</span><span class="sxs-lookup"><span data-stu-id="1a700-130">A registration is matched only on the presence or absence of a specific tag.</span></span>

<span data-ttu-id="1a700-131">Per un'esercitazione completa dettagliata su come usare i tag per l'invio a gruppi di interesse, vedere [Ultime notizie](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span><span class="sxs-lookup"><span data-stu-id="1a700-131">For a full step-by-step tutorial on how to use tags for sending to interest groups, see [Breaking News](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span></span>

## <a name="using-tags-to-target-users"></a><span data-ttu-id="1a700-132">Uso dei tag per considerare come obiettivo gli utenti</span><span class="sxs-lookup"><span data-stu-id="1a700-132">Using tags to target users</span></span>
<span data-ttu-id="1a700-133">Un altro modo per utilizzare i tag consiste nell'identificare tutti i dispositivi di un particolare utente.</span><span class="sxs-lookup"><span data-stu-id="1a700-133">Another way to use tags is to identify all the devices of a particular user.</span></span> <span data-ttu-id="1a700-134">Le registrazioni possono essere contrassegnate con un tag che contiene un id utente, come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="1a700-134">Registrations can be tagged with a tag that contains a user id, as in the following picture:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

<span data-ttu-id="1a700-135">In questa immagine, il messaggio con tag uid:Alice raggiunge tutte le registrazioni con tag uid:Alice; di conseguenza, tutti i dispositivi di Alice.</span><span class="sxs-lookup"><span data-stu-id="1a700-135">In this picture, the message tagged uid:Alice reaches all registrations tagged uid:Alice; hence, all of Alice’s devices.</span></span>

## <a name="tag-expressions"></a><span data-ttu-id="1a700-136">Espressioni tag</span><span class="sxs-lookup"><span data-stu-id="1a700-136">Tag expressions</span></span>
<span data-ttu-id="1a700-137">Vi sono casi in cui una notifica ha come destinazione un set di registrazioni identificato non da un singolo tag, ma da un'espressione booleana su tag.</span><span class="sxs-lookup"><span data-stu-id="1a700-137">There are cases in which a notification has to target a set of registrations that is identified not by a single tag, but by a Boolean expression on tags.</span></span>

<span data-ttu-id="1a700-138">Si consideri un'applicazione sportiva che invia un promemoria su una partita tra Red Sox e Cardinals a tutte le persone di Boston.</span><span class="sxs-lookup"><span data-stu-id="1a700-138">Consider a sports application that sends a reminder to everyone in Boston about a game between the Red Sox and Cardinals.</span></span> <span data-ttu-id="1a700-139">Se l'app client registra i tag relativi all'interesse per squadre e località, la notifica deve essere destinata a tutte le persone di Boston interessate ai Red Sox o ai Cardinals.</span><span class="sxs-lookup"><span data-stu-id="1a700-139">If the client app registers tags about interest in teams and location, then the notification should be targeted to everyone in Boston who is interested in either the Red Sox or the Cardinals.</span></span> <span data-ttu-id="1a700-140">Questa condizione può essere espressa con l'espressione booleana seguente:</span><span class="sxs-lookup"><span data-stu-id="1a700-140">This condition can be expressed with the following Boolean expression:</span></span>

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

<span data-ttu-id="1a700-141">Le espressioni tag possono contenere tutti gli operatori booleani, quali AND (&&), OR (||) e NOT (!).</span><span class="sxs-lookup"><span data-stu-id="1a700-141">Tag expressions can contain all Boolean operators, such as AND (&&), OR (||), and NOT (!).</span></span> <span data-ttu-id="1a700-142">Possono inoltre contenere parentesi.</span><span class="sxs-lookup"><span data-stu-id="1a700-142">They can also contain parentheses.</span></span> <span data-ttu-id="1a700-143">Le espressioni tag sono limitate a 20 tag se contengono solo operatori OR; in caso contrario sono limitate a 6 tag.</span><span class="sxs-lookup"><span data-stu-id="1a700-143">Tag expressions are limited to 20 tags if they contain only ORs; otherwise they are limited to 6 tags.</span></span>

<span data-ttu-id="1a700-144">Di seguito è riportato un esempio per l'invio di notifiche con espressioni tag usando l’SDK.</span><span class="sxs-lookup"><span data-stu-id="1a700-144">Here's an example for sending notifications with tag expressions using the SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    String userTag = "(location_Boston && !follows_Cardinals)";    

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You want info on the Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You want info on the Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
