---
title: aaaAzure notifiche dei report di Active Directory
description: Come toouse hello notifiche reporting di Azure Active Directory per l'accesso sospetti aggiuntivi.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ae6d4b0e-5931-4cb3-98bf-9be91b381c92
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.custom: oldportal
ms.reviewer: dhanyahk
ms.openlocfilehash: 3843c45eaf9d68e671943bfdbc7ab68933f38fbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-notifications"></a><span data-ttu-id="45c19-103">Notifiche di Report di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="45c19-103">Azure Active Directory Reporting Notifications</span></span>
## <a name="what-reports-generate-email-notifications"></a><span data-ttu-id="45c19-104">Quali report generano notifiche tramite posta elettronica</span><span class="sxs-lookup"><span data-stu-id="45c19-104">What reports generate email notifications</span></span>
<span data-ttu-id="45c19-105">In questo momento, notifiche tramite posta elettronica solo nei trigger report attività hello di accesso irregolare.</span><span class="sxs-lookup"><span data-stu-id="45c19-105">At this time, only hello Irregular Sign in Activity report triggers email notifications.</span></span>

## <a name="what-is-an-irregular-sign-in"></a><span data-ttu-id="45c19-106">Che cos'è un "Accesso irregolare"?</span><span class="sxs-lookup"><span data-stu-id="45c19-106">What is an "Irregular Sign in"?</span></span>
<span data-ttu-id="45c19-107">Accessi irregolari sono quelli che sono stati identificati dagli algoritmi, su base hello di una condizione di "Impossibile viaggio" combinata con un percorso di accesso anomalo e dispositivo di apprendimento automatico.</span><span class="sxs-lookup"><span data-stu-id="45c19-107">Irregular sign-ins are those that have been identified by our machine learning algorithms, on hello basis of an "impossible travel" condition combined with an anomalous sign-in location and device.</span></span> <span data-ttu-id="45c19-108">Questo può indicare che un pirata informatico abbia tentato toosign utilizzando questo account.</span><span class="sxs-lookup"><span data-stu-id="45c19-108">This may indicate that a hacker has been trying toosign in using this account.</span></span>

## <a name="who-receives-hello-email-notifications"></a><span data-ttu-id="45c19-109">Chi riceverà le notifiche di posta elettronica hello?</span><span class="sxs-lookup"><span data-stu-id="45c19-109">Who receives hello email notifications?</span></span>
<span data-ttu-id="45c19-110">messaggio di posta elettronica Hello viene inviato tooall gli amministratori globali che sono stati assegnati una licenza di Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="45c19-110">hello email is sent tooall global admins who have been assigned an Active Directory Premium license.</span></span> <span data-ttu-id="45c19-111">tooensure che viene recapitato, inviato anche toohello admins indirizzo di posta elettronica alternativo.</span><span class="sxs-lookup"><span data-stu-id="45c19-111">tooensure it is delivered, we send it toohello admins Alternate Email Address as well.</span></span> <span data-ttu-id="45c19-112">Gli amministratori devono includere aad-alerts-noreply@mail.windowsazure.com nel proprio elenco Mittenti attendibili in modo che non perdere il messaggio di posta elettronica hello.</span><span class="sxs-lookup"><span data-stu-id="45c19-112">Admins should include aad-alerts-noreply@mail.windowsazure.com in their safe senders list so they don’t miss hello email.</span></span>

## <a name="how-often-are-these-emails-sent"></a><span data-ttu-id="45c19-113">Con quale frequenza vengono inviati i messaggi di posta elettronica?</span><span class="sxs-lookup"><span data-stu-id="45c19-113">How often are these emails sent?</span></span>
<span data-ttu-id="45c19-114">messaggio di posta elettronica Hello viene inviato se 10 nuove irregolari Accedi attività si verificano in hello ultimi 30 giorni, oppure perché è stato inviato l'ultimo messaggio di posta hello, qualunque sia inferiore.</span><span class="sxs-lookup"><span data-stu-id="45c19-114">hello email is sent if 10 new irregular sign-in activities occur in hello last 30 days, or since hello last email was sent, whichever is less.</span></span>

## <a name="how-do-i-access-hello-report-mentioned-in-hello-email"></a><span data-ttu-id="45c19-115">La modalità di accesso di report hello indicato nel messaggio di posta elettronica hello?</span><span class="sxs-lookup"><span data-stu-id="45c19-115">How do I access hello report mentioned in hello email?</span></span>
<span data-ttu-id="45c19-116">Quando si fa clic sul collegamento hello, sarà reindirizzato toohello pagina del report all'interno di hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="45c19-116">When you click on hello link, you will be redirected toohello report page within hello Azure classic portal.</span></span> <span data-ttu-id="45c19-117">In ordine tooaccess hello report, è necessario toobe entrambi:</span><span class="sxs-lookup"><span data-stu-id="45c19-117">In order tooaccess hello report, you need toobe both:</span></span>

* <span data-ttu-id="45c19-118">Un amministratore o un coamministratore della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="45c19-118">An admin or co-admin of your Azure subscription</span></span>
* <span data-ttu-id="45c19-119">Un amministratore globale nella directory di hello e assegnata una licenza di Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="45c19-119">A global administrator in hello directory, and assigned an Active Directory Premium license.</span></span> <span data-ttu-id="45c19-120">Per altre informazioni, vedere [Edizioni di Azure Active Directory](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="45c19-120">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="can-i-turn-off-these-emails"></a><span data-ttu-id="45c19-121">È possibile disattivare questi messaggi di posta elettronica?</span><span class="sxs-lookup"><span data-stu-id="45c19-121">Can I turn off these emails?</span></span>
<span data-ttu-id="45c19-122">Sì, tooturn le notifiche correlate tooanomalous accessi all'interno di hello portale di Azure classico, fare clic su **configura**, quindi selezionare **disabilitato** in hello **notifiche**sezione.</span><span class="sxs-lookup"><span data-stu-id="45c19-122">Yes, tooturn off notifications related tooanomalous sign-ins within hello Azure classic portal, click **Configure**, and then select **Disabled** under hello **Notifications** section.</span></span>

## <a name="whats-next"></a><span data-ttu-id="45c19-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="45c19-123">What's next</span></span>
* <span data-ttu-id="45c19-124">Per informazioni sui report di sicurezza, controllo e attività disponibili,</span><span class="sxs-lookup"><span data-stu-id="45c19-124">Curious about what security, audit, and activity reports are available?</span></span> <span data-ttu-id="45c19-125">Vedere [Report di sicurezza, controllo e attività di Azure AD](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="45c19-125">Check out [Azure AD Security, Audit, and Activity Reports](active-directory-view-access-usage-reports.md)</span></span>
* [<span data-ttu-id="45c19-126">Introduzione ad Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="45c19-126">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="45c19-127">Aggiungere personalizzazione delle pagine di accesso e il pannello di accesso tooyour della società</span><span class="sxs-lookup"><span data-stu-id="45c19-127">Add company branding tooyour Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

