---
title: Utilizzare le emoticon Emoji all'interno di Mobile Engagement di Azure
description: Informazioni su come usare emoticon Emoji nelle notifiche push
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
ms.openlocfilehash: bbb7ce5e95b229a7505c5e97b6866d5a302a1d27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-emoji-emoticon-within-push-notifications"></a><span data-ttu-id="cf63b-103">Usare emoticon Emoji nelle notifiche push</span><span class="sxs-lookup"><span data-stu-id="cf63b-103">Use Emoji emoticon within Push Notifications</span></span>
<span data-ttu-id="cf63b-104">È possibile includere emoticon Emoji nelle notifiche push con pochi e semplici passaggi:</span><span class="sxs-lookup"><span data-stu-id="cf63b-104">You can include Emoji emoticons in you push notification in a few easy steps:</span></span> 

1. <span data-ttu-id="cf63b-105">In primo luogo è necessario trovare l’Emoji che si desidera inviare nel messaggio.</span><span class="sxs-lookup"><span data-stu-id="cf63b-105">First of all you need to find the Emoji you want to send in the message.</span></span> <span data-ttu-id="cf63b-106">Assicurarsi che l’Emoji che si sta selezionando verrà supportata dal dispositivo di destinazione poiché i produttori del dispositivo impiegano del tempo per aggiungere gli Emojis appena approvati alle piattaforme del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cf63b-106">Please ensure that the Emoji you are selecting will be supported by the target device as device manufactures take some time to add newly approved Emojis to the device platforms.</span></span> 
2. <span data-ttu-id="cf63b-107">Su **Windows** -è possibile passare a questo [collegamento](http://apps.timwhitlock.info/emoji/tables/unicode) e copiare l'icona 'Native'.</span><span class="sxs-lookup"><span data-stu-id="cf63b-107">On **Windows** - you can navigate to this [link](http://apps.timwhitlock.info/emoji/tables/unicode) and copy the 'Native' icon.</span></span>
   
    ![][7] 
3. <span data-ttu-id="cf63b-108">Su **Mac** - è possibile trovare gli emoji nell'applicazione Dizionario in Modifica -> Emoji e simboli.</span><span class="sxs-lookup"><span data-stu-id="cf63b-108">On **Mac** - you can find the Emojis in Dictionary application under Edit -> Emoji & Symbols.</span></span>
   
    ![][6] 
4. <span data-ttu-id="cf63b-109">A questo punto, passare alla scheda **Copertura** del portale di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="cf63b-109">Now, go to the **Reach** tab on the the Azure Mobile Engagement portal.</span></span> <span data-ttu-id="cf63b-110">Selezionare il tipo di notifica push, ovvero annuncio, sondaggio e così via.</span><span class="sxs-lookup"><span data-stu-id="cf63b-110">Select the type of your push notification (Announcement, polls etc).</span></span> <span data-ttu-id="cf63b-111">Per questo esempio è stata scelta una notifica push di tipo annuncio.</span><span class="sxs-lookup"><span data-stu-id="cf63b-111">For this example we choose an announcement push.</span></span>
5. <span data-ttu-id="cf63b-112">Specificare i diversi campi della notifica fino a raggiungere il testo della notifica,</span><span class="sxs-lookup"><span data-stu-id="cf63b-112">Specify the different fields of the notification until you reach the text of the notification.</span></span> <span data-ttu-id="cf63b-113">in cui verrà aggiunto l'emoticon Emoji.</span><span class="sxs-lookup"><span data-stu-id="cf63b-113">This is where you will add your Emoji Emoticon.</span></span> <span data-ttu-id="cf63b-114">È possibile scegliere di inserirlo nel titolo, nel messaggio o in entrambi.</span><span class="sxs-lookup"><span data-stu-id="cf63b-114">You can choose to put it in the title, the message, or both.</span></span> <span data-ttu-id="cf63b-115">È necessario trascinare o copiare gli Emoji individuati dai percorsi precedenti.</span><span class="sxs-lookup"><span data-stu-id="cf63b-115">You will need to drag and drop or copy the Emoji that you find from the locations above.</span></span> 
   
    ![][1]
6. <span data-ttu-id="cf63b-116">Completare gli altri campi per la notifica e salvarla.</span><span class="sxs-lookup"><span data-stu-id="cf63b-116">Complete the other fields for the notification and save it.</span></span> 
7. <span data-ttu-id="cf63b-117">Quando si esegue un test o si attiva l'annuncio, verrà visualizzata una notifica con l'emoticon, in base a quanto specificato.</span><span class="sxs-lookup"><span data-stu-id="cf63b-117">When you run a test or activate the announcement you will see a notification with the emoticon as specified.</span></span>   
   
    <span data-ttu-id="cf63b-118">![][3] ![][4] ![][5]</span><span class="sxs-lookup"><span data-stu-id="cf63b-118">![][3] ![][4] ![][5]</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-use-emoji-with-push/notification_input.png
[3]: ./media/mobile-engagement-use-emoji-with-push/iOS_Emoji.png
[4]: ./media/mobile-engagement-use-emoji-with-push/Android_Emoji.png
[5]: ./media/mobile-engagement-use-emoji-with-push/WindowsPhone_Emoji.png
[6]: ./media/mobile-engagement-use-emoji-with-push/Mac_SelectEmoji.png
[7]: ./media/mobile-engagement-use-emoji-with-push/Windows_SelectEmoji.png

