---
title: "Accessi da più aree geografiche"
description: "Report che segnala agli utenti situazioni in cui due accessi sembrano provenire da diverse aree, ma dato il tempo intercorso tra gli accessi non è possibile che l'utente si sia spostato da un'area all'altra."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: 79259c8a-2388-4747-b41e-c07434ea9a02
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 1de57f64692ade442f9ef8d1e3b587ffee35d7cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-multiple-geographies"></a><span data-ttu-id="d7cce-103">Accessi da più aree geografiche</span><span class="sxs-lookup"><span data-stu-id="d7cce-103">Sign-ins from multiple geographies</span></span>
<span data-ttu-id="d7cce-104">Questo report mostra gli accessi effettuati da un utente e due di questi sembrano provenire da aree diverse. Dato il tempo intercorso tra gli accessi non è possibile che l'utente si sia spostato da un'area all'altra.</span><span class="sxs-lookup"><span data-stu-id="d7cce-104">This report includes successful sign-ins from a user where two sign-ins appeared to originate from different regions and the time between the sign-ins makes it impossible for the user to have traveled between those regions.</span></span> <span data-ttu-id="d7cce-105">Le possibili cause includono:</span><span class="sxs-lookup"><span data-stu-id="d7cce-105">Possible causes include:</span></span>

* <span data-ttu-id="d7cce-106">L'utente sta condividendo la password</span><span class="sxs-lookup"><span data-stu-id="d7cce-106">User is sharing their password with other users</span></span>
* <span data-ttu-id="d7cce-107">L'utente usa un desktop remoto per avviare un Web browser per l'accesso</span><span class="sxs-lookup"><span data-stu-id="d7cce-107">User is using a remote desktop to launch a web browser for sign-in</span></span>
* <span data-ttu-id="d7cce-108">Un pirata informatico ha effettuato l'accesso all'account di un utente da un altro paese</span><span class="sxs-lookup"><span data-stu-id="d7cce-108">A hacker has signed in to the account of a user from a different country</span></span>
* <span data-ttu-id="d7cce-109">L’utente sta usando una VPN o un proxy</span><span class="sxs-lookup"><span data-stu-id="d7cce-109">User is using a VPN or proxy</span></span>
* <span data-ttu-id="d7cce-110">L'utente ha eseguito l'accesso da più dispositivi contemporaneamente, ad esempio da un computer desktop e da un cellulare, e l'indirizzo IP del cellulare è insolito.</span><span class="sxs-lookup"><span data-stu-id="d7cce-110">User is signed in from multiple devices at the same time, such as a desktop and a mobile phone, and the IP address of the mobile phone is unusual.</span></span>

<span data-ttu-id="d7cce-111">Nei risultati del report verranno mostrati gli eventi di accesso riuscito, nonché il tempo tra gli accessi, le aree da cui gli accessi sembrano provenire e il tempo di spostamento stimato tra queste aree.</span><span class="sxs-lookup"><span data-stu-id="d7cce-111">Results from this report will show you the successful sign-in events, together with the time between the sign-ins, the regions where the sign-ins appeared to originate from, and the estimated travel time between those regions.</span></span> <span data-ttu-id="d7cce-112">Il tempo di spostamento mostrato è solo una stima e può essere diverso da quello effettivamente necessario per spostarsi da una posizione all’altra.</span><span class="sxs-lookup"><span data-stu-id="d7cce-112">The travel time shown is only an estimate and may be different from the actual travel time between the locations.</span></span>

![Accessi da più aree geografiche](./media/active-directory-reporting-sign-ins-from-multiple-geographies/signInsFromMultipleGeographies.PNG)

