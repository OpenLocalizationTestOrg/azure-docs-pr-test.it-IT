---
title: "Attività di accesso irregolare"
description: Questo report include accessi identificati come anomali dagli algoritmi di Machine Learning.
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: a5a270a9-a0eb-4a99-b04c-ccde3829ffe4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 565321b6f3ad5988f383a701cb9d8bd5c9937795
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="irregular-sign-in-activity"></a><span data-ttu-id="a6cbc-103">Attività di accesso irregolare</span><span class="sxs-lookup"><span data-stu-id="a6cbc-103">Irregular sign-in activity</span></span>
<span data-ttu-id="a6cbc-104">Gli accessi irregolari sono quelli individuati dagli algoritmi di Machine Learning in base a una condizione di tipo "tempo di spostamento impossibile" combinata con una posizione e un dispositivo di accesso anomali.</span><span class="sxs-lookup"><span data-stu-id="a6cbc-104">Irregular sign-ins are those that have been identified by our machine learning algorithms, on the basis of an "impossible travel" condition combined with an anomalous sign in location and device.</span></span> <span data-ttu-id="a6cbc-105">È possibile che un pirata informatico abbia eseguito l'accesso con questo account.</span><span class="sxs-lookup"><span data-stu-id="a6cbc-105">This may indicate that a hacker has successfully signed in using this account.</span></span>
<span data-ttu-id="a6cbc-106">Microsoft invierà una notifica tramite posta elettronica agli amministratori globali se si verificano 10 o più eventi di accesso anomalo in un intervallo di 30 giorni o meno.</span><span class="sxs-lookup"><span data-stu-id="a6cbc-106">We will send an email notification to the global admins if we encounter 10 or more anomalous sign-in events within a span of 30 days or less.</span></span> <span data-ttu-id="a6cbc-107">Assicurarsi di includere aad-alerts-noreply@mail.windowsazure.com nell'elenco dei mittenti attendibili.</span><span class="sxs-lookup"><span data-stu-id="a6cbc-107">Please be sure to include aad-alerts-noreply@mail.windowsazure.com in your safe senders list.</span></span>

