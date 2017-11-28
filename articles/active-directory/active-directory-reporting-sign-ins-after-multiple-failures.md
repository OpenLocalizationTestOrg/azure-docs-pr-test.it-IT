---
title: "aaaSign aggiuntivi dopo più errori"
description: "Un report indica gli utenti che hanno eseguito correttamente l'accesso dopo più tentativi di accesso consecutivi non riusciti."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: femila
editor: 
ms.assetid: e4ec1a39-9c20-418f-8a75-6497d0117176
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 48d137dc3abf65287cb3b9ba8a6ff10340f6741f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sign-ins-after-multiple-failures"></a><span data-ttu-id="7770a-103">Accessi dopo più errori</span><span class="sxs-lookup"><span data-stu-id="7770a-103">Sign-ins after multiple failures</span></span>
<span data-ttu-id="7770a-104">Questo report indica gli utenti che hanno eseguito correttamente l'accesso dopo più tentativi di accesso consecutivi non riusciti.</span><span class="sxs-lookup"><span data-stu-id="7770a-104">This report indicates users who have successfully signed in after multiple consecutive failed sign in attempts.</span></span> <span data-ttu-id="7770a-105">Le possibili cause includono:</span><span class="sxs-lookup"><span data-stu-id="7770a-105">Possible causes include:</span></span>

* <span data-ttu-id="7770a-106">L'utente ha dimenticato la password</span><span class="sxs-lookup"><span data-stu-id="7770a-106">User had forgotten their password</span></span></li><li><span data-ttu-id="7770a-107">Utente è vittima hello di una password ha esito positivo di un'ipotesi di attacco di forza bruta</span><span class="sxs-lookup"><span data-stu-id="7770a-107">User is hello victim of a successful password guessing brute force attack</span></span>

<span data-ttu-id="7770a-108">Nei risultati del report verranno mostrati hello numero di tentativi consecutivi non accedi apportati toohello precedente ha esito positivo Accedi e un timestamp associato hello primo ha esito positivo Accedi.</span><span class="sxs-lookup"><span data-stu-id="7770a-108">Results from this report will show you hello number of consecutive failed sign-in attempts made prior toohello successful sign-in and a timestamp associated with hello first successful sign-in.</span></span>

<span data-ttu-id="7770a-109">**Report impostazioni**: È possibile configurare il numero minimo di hello di accesso non riusciti consecutivi tentativi che devono verificarsi prima che possono essere visualizzato nel report hello.</span><span class="sxs-lookup"><span data-stu-id="7770a-109">**Report Settings**: You can configure hello minimum number of consecutive failed sign in attempts that must occur before it can be displayed in hello report.</span></span> <span data-ttu-id="7770a-110">Quando si apportano modifiche toothis impostarlo è toonote importante che tali modifiche non verranno applicati tooany esistente non riuscita accessi che attualmente visualizzati nel rapporto.</span><span class="sxs-lookup"><span data-stu-id="7770a-110">When you make changes toothis setting it is important toonote that these changes will not be applied tooany existing failed sign ins that currently show up in your existing report.</span></span> <span data-ttu-id="7770a-111">Tuttavia, saranno applicati tooall future-accessi. Le modifiche toothis report può essere apportata esclusivamente dagli amministratori autorizzati.</span><span class="sxs-lookup"><span data-stu-id="7770a-111">However, they will be applied tooall future sign-ins. Changes toothis report can only be made by licensed admins.</span></span>

![Accessi dopo più errori](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

