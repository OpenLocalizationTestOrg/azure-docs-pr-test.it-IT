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
# <a name="routing-and-tag-expressions"></a>Espressioni di routing e tag
## <a name="overview"></a>Panoramica
Espressioni tag consentono di tootarget set specifici di dispositivi o più specificamente registrazioni, quando si invia una notifica push tramite hub di notifica.

## <a name="targeting-specific-registrations"></a>Destinazione su registrazioni specifiche
Hello solo modo tootarget notifica specifica registrazioni è tooassociate tag con essi, quindi come destinazione tali tag. Come descritto in [gestione registrazione](notification-hubs-push-notification-registration-management.md), in push tooreceive ordine notifiche tooregister un dispositivo dispone di un'app di gestire in un hub di notifica. Dopo aver creata una registrazione in un hub di notifica, back-end dell'applicazione hello può inviare tooit le notifiche push.
back-end dell'applicazione Hello è possibile scegliere hello registrazioni tootarget con una notifica specifica hello seguenti modi:

1. **Trasmissione**: tutte le registrazioni nell'hub di notifica hello ricevano una notifica di hello.
2. **Tag**: tutte le registrazioni contenenti hello specificato tag ricevere una notifica di hello.
3. **Espressione tag**: tutte le registrazioni il cui set di tag corrispondenza hello espressione specificata ricevono la notifica hello.

## <a name="tags"></a>Tag
Un tag può essere qualsiasi stringa, i caratteri too120, contenente caratteri alfanumerici e hello seguenti caratteri non alfanumerici: '_', ' @', '#', '. ',':', '-'. Hello esempio seguente viene illustrata un'applicazione da cui è possibile ricevere notifiche di tipo avviso popup su gruppi musicali specifici. In questo scenario, le notifiche tooroute un modo semplice è toolabel registrazioni con tag che rappresentano gruppi musicali diversi hello, come illustrato di seguito immagine hello.

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

In questa immagine, tag messaggio hello **Beatles** raggiunge solo hello tablet registrato con il tag di hello **Beatles**.

Per ulteriori informazioni sulla creazione di registrazioni per i tag, vedere [Gestione delle registrazioni](notification-hubs-push-notification-registration-management.md).

È possibile inviare notifiche tootags utilizzando hello inviare metodi di notifiche di hello `Microsoft.Azure.NotificationHubs.NotificationHubClient` classe hello [gli hub di notifica di Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK. È anche possibile usare Node.js o hello API REST di notifiche Push.  Di seguito è riportato un esempio di utilizzo hello SDK.

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




Tag non è necessario pre-provisioning toobe e possono fare riferimento a concetti specifici dell'app toomultiple. In questo modo gli utenti di questa applicazione di esempio possono ad esempio, commentare le bande e desidera avvisi popup tooreceive, non solo per i commenti di hello sui propri gruppi Preferiti, ma anche per tutti i commenti degli amici, indipendentemente dalla banda hello in cui si sta Commentando. Hello seguente immagine mostra un esempio di questo scenario:

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

In questa immagine, Alice è interessata a ricevere aggiornamenti per hello Beatles e Bob è interessato a ricevere aggiornamenti per hello Wailers. Bob è anche interessato ai commenti di Charlie e Charlie è interessato hello Wailers. Quando viene inviata una notifica per commento di Charlie sui Beatles hello, sia Alice sia Bob la ricevono.

Sebbene sia possibile codificare più aspetti nei tag (ad esempio, "gruppo_Beatles" o "segue_Charlie"), i tag sono semplici stringhe e non proprietà con valori. La registrazione viene stabilita la corrispondenza solo hello presenza o assenza di un tag specifico.

Per un'esercitazione dettagliata su come i tag per l'invio di gruppi toointerest toouse, vedere [delle ultime notizie](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).

## <a name="using-tags-tootarget-users"></a>Tag tootarget utenti
Un altro modo toouse tag è tooidentify tutti i dispositivi di hello di un determinato utente. Le registrazioni possono essere contrassegnate con un tag che contiene un id utente, come in hello seguente immagine:

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

In questa immagine, UID: Alice tag messaggio hello raggiunge tutte le registrazioni con tag UID: Alice; di conseguenza, tutti i dispositivi di Alice.

## <a name="tag-expressions"></a>Espressioni tag
Vi sono casi in cui una notifica ha tootarget un set di registrazioni identificato non da un singolo tag, ma con un'espressione booleana su tag.

Si consideri un'applicazione sportiva che invia un promemoria tooeveryone Boston su una partita tra hello Red Sox e Cardinals. Se l'applicazione client hello registra i tag relativi all'interesse per squadre e località, notifica hello deve essere tooeveryone destinazione Boston interessati hello Red Sox o hello Cardinals. Questa condizione può essere espresso con hello espressione booleana seguente:

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

Le espressioni tag possono contenere tutti gli operatori booleani, quali AND (&&), OR (||) e NOT (!). Possono inoltre contenere parentesi. Espressioni tag sono tag too20 limitato se contengono solo OR; in caso contrario sono tag too6 limitato.

Di seguito è riportato un esempio per l'invio di notifiche con espressioni tag usando hello SDK.

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
