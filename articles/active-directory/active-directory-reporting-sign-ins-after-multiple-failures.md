---
title: "Accessi dopo più errori"
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
ms.openlocfilehash: e55e0145adbdb1f41a8b8753d5555f20e96bf161
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-after-multiple-failures"></a><span data-ttu-id="0417c-103">Accessi dopo più errori</span><span class="sxs-lookup"><span data-stu-id="0417c-103">Sign-ins after multiple failures</span></span>
<span data-ttu-id="0417c-104">Questo report indica gli utenti che hanno eseguito correttamente l'accesso dopo più tentativi di accesso consecutivi non riusciti.</span><span class="sxs-lookup"><span data-stu-id="0417c-104">This report indicates users who have successfully signed in after multiple consecutive failed sign in attempts.</span></span> <span data-ttu-id="0417c-105">Le possibili cause includono:</span><span class="sxs-lookup"><span data-stu-id="0417c-105">Possible causes include:</span></span>

* <span data-ttu-id="0417c-106">L'utente ha dimenticato la password</span><span class="sxs-lookup"><span data-stu-id="0417c-106">User had forgotten their password</span></span></li><li><span data-ttu-id="0417c-107">L’utente è vittima di un attacco di forza bruta per l’individuazione della password riuscito</span><span class="sxs-lookup"><span data-stu-id="0417c-107">User is the victim of a successful password guessing brute force attack</span></span>

<span data-ttu-id="0417c-108">I risultati di questo report mostreranno il numero di tentativi di accesso consecutivi non riusciti effettuati prima dell’accesso riuscito e un timestamp associato con il primo accesso riuscito.</span><span class="sxs-lookup"><span data-stu-id="0417c-108">Results from this report will show you the number of consecutive failed sign-in attempts made prior to the successful sign-in and a timestamp associated with the first successful sign-in.</span></span>

<span data-ttu-id="0417c-109">**Impostazioni report**: è possibile configurare il numero minimo di tentativi di accesso consecutivi non riusciti che devono verificarsi affinché l’informazione sia segnalata nel report.</span><span class="sxs-lookup"><span data-stu-id="0417c-109">**Report Settings**: You can configure the minimum number of consecutive failed sign in attempts that must occur before it can be displayed in the report.</span></span> <span data-ttu-id="0417c-110">Quando si apportano modifiche a questa impostazione si noti che le modifiche non si applicano a eventuali accessi non riusciti attualmente visualizzati nel report.</span><span class="sxs-lookup"><span data-stu-id="0417c-110">When you make changes to this setting it is important to note that these changes will not be applied to any existing failed sign ins that currently show up in your existing report.</span></span> <span data-ttu-id="0417c-111">Verranno tuttavia applicate a tutti gli accessi successivi.</span><span class="sxs-lookup"><span data-stu-id="0417c-111">However, they will be applied to all future sign-ins.</span></span> <span data-ttu-id="0417c-112">Le modifiche a questo report possono essere apportate solo dagli amministratori autorizzati.</span><span class="sxs-lookup"><span data-stu-id="0417c-112">Changes to this report can only be made by licensed admins.</span></span>

![Accessi dopo più errori](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

