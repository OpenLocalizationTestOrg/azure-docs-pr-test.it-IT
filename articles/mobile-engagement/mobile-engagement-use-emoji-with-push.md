---
title: aaaUse Emoji emoticon all'interno di Azure Mobile Engagement
description: Come le emoticon Emoji toouse entro le notifiche push
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 663317d7-3c93-4e8f-b13d-c6fb342124ee
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 63bfc59ef472e9fe9aa28b5ac8761017b9250e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-emoji-emoticon-within-push-notifications"></a><span data-ttu-id="34e3f-103">Usare emoticon Emoji nelle notifiche push</span><span class="sxs-lookup"><span data-stu-id="34e3f-103">Use Emoji emoticon within Push Notifications</span></span>
<span data-ttu-id="34e3f-104">È possibile includere emoticon Emoji nelle notifiche push con pochi e semplici passaggi:</span><span class="sxs-lookup"><span data-stu-id="34e3f-104">You can include Emoji emoticons in you push notification in a few easy steps:</span></span> 

1. <span data-ttu-id="34e3f-105">Prima di tutto è necessario toofind hello Emoji desiderato toosend nel messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="34e3f-105">First of all you need toofind hello Emoji you want toosend in hello message.</span></span> <span data-ttu-id="34e3f-106">Verificare che hello sarà supportato dal dispositivo di destinazione hello Emoji si seleziona come dispositivo produce accettano alcuni tooadd ora piattaforme per dispositivi toohello Emojis appena approvate.</span><span class="sxs-lookup"><span data-stu-id="34e3f-106">Please ensure that hello Emoji you are selecting will be supported by hello target device as device manufactures take some time tooadd newly approved Emojis toohello device platforms.</span></span> 
2. <span data-ttu-id="34e3f-107">In **Windows** -è possibile passare toothis [collegamento](http://apps.timwhitlock.info/emoji/tables/unicode) e l'icona di copia hello 'Native'.</span><span class="sxs-lookup"><span data-stu-id="34e3f-107">On **Windows** - you can navigate toothis [link](http://apps.timwhitlock.info/emoji/tables/unicode) and copy hello 'Native' icon.</span></span>
   
    ![][7] 
3. <span data-ttu-id="34e3f-108">In **Mac** -è possibile trovare hello Emojis nell'applicazione di dizionario, scegliere Modifica -> Emoji & simboli.</span><span class="sxs-lookup"><span data-stu-id="34e3f-108">On **Mac** - you can find hello Emojis in Dictionary application under Edit -> Emoji & Symbols.</span></span>
   
    ![][6] 
4. <span data-ttu-id="34e3f-109">A questo punto, passare toohello **raggiungere** scheda nel portale di Azure Mobile Engagement hello hello.</span><span class="sxs-lookup"><span data-stu-id="34e3f-109">Now, go toohello **Reach** tab on hello hello Azure Mobile Engagement portal.</span></span> <span data-ttu-id="34e3f-110">Selezionare il tipo di hello della notifica push (annuncio, viene eseguito il polling e così via).</span><span class="sxs-lookup"><span data-stu-id="34e3f-110">Select hello type of your push notification (Announcement, polls etc).</span></span> <span data-ttu-id="34e3f-111">Per questo esempio è stata scelta una notifica push di tipo annuncio.</span><span class="sxs-lookup"><span data-stu-id="34e3f-111">For this example we choose an announcement push.</span></span>
5. <span data-ttu-id="34e3f-112">Specificare i campi di diversi hello della notifica hello fino a raggiungere il testo hello della notifica hello.</span><span class="sxs-lookup"><span data-stu-id="34e3f-112">Specify hello different fields of hello notification until you reach hello text of hello notification.</span></span> <span data-ttu-id="34e3f-113">in cui verrà aggiunto l'emoticon Emoji.</span><span class="sxs-lookup"><span data-stu-id="34e3f-113">This is where you will add your Emoji Emoticon.</span></span> <span data-ttu-id="34e3f-114">È possibile scegliere tooput nel titolo hello, il messaggio hello o entrambi.</span><span class="sxs-lookup"><span data-stu-id="34e3f-114">You can choose tooput it in hello title, hello message, or both.</span></span> <span data-ttu-id="34e3f-115">Si sarà necessario toodrag e drop o copiare hello Emoji che trova da posizioni di hello precedente.</span><span class="sxs-lookup"><span data-stu-id="34e3f-115">You will need toodrag and drop or copy hello Emoji that you find from hello locations above.</span></span> 
   
    ![][1]
6. <span data-ttu-id="34e3f-116">Completa hello altri campi per la notifica di hello e salvarlo.</span><span class="sxs-lookup"><span data-stu-id="34e3f-116">Complete hello other fields for hello notification and save it.</span></span> 
7. <span data-ttu-id="34e3f-117">Quando si esegue un test o attiva annuncio hello si vedrà una notifica con emoticon hello come specificato.</span><span class="sxs-lookup"><span data-stu-id="34e3f-117">When you run a test or activate hello announcement you will see a notification with hello emoticon as specified.</span></span>   
   
    <span data-ttu-id="34e3f-118">![][3] ![][4] ![][5]</span><span class="sxs-lookup"><span data-stu-id="34e3f-118">![][3] ![][4] ![][5]</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-use-emoji-with-push/notification_input.png
[3]: ./media/mobile-engagement-use-emoji-with-push/iOS_Emoji.png
[4]: ./media/mobile-engagement-use-emoji-with-push/Android_Emoji.png
[5]: ./media/mobile-engagement-use-emoji-with-push/WindowsPhone_Emoji.png
[6]: ./media/mobile-engagement-use-emoji-with-push/Mac_SelectEmoji.png
[7]: ./media/mobile-engagement-use-emoji-with-push/Windows_SelectEmoji.png

