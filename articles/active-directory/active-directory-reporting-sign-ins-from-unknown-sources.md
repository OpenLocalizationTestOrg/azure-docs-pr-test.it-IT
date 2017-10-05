---
title: Accessi da origini sconosciute
description: Un report che indica gli utenti che hanno effettuato correttamente l'accesso alla directory da un indirizzo IP proxy anonimo.
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: femila
editor: 
ms.assetid: 2f045543-1578-4972-bf70-b35310f23110
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 90006121e4b3392f6e3ecffb4a56aca330feb02f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-unknown-sources"></a><span data-ttu-id="76a8d-103">Accessi da origini sconosciute</span><span class="sxs-lookup"><span data-stu-id="76a8d-103">Sign ins from unknown sources</span></span>
<span data-ttu-id="76a8d-104">Questo report indica gli utenti che hanno eseguito correttamente l'accesso alla directory mentre era loro assegnato un indirizzo IP client riconosciuto da Microsoft come indirizzo IP proxy anonimo (ad esempio un indirizzo Tor IP).</span><span class="sxs-lookup"><span data-stu-id="76a8d-104">This report indicates users who have successfully signed in to your directory while assigned a client IP address that has been recognized by Microsoft as an anonymous proxy IP address (for example, a Tor IP address).</span></span> <span data-ttu-id="76a8d-105">Questi proxy vengono spesso usati dagli utenti che vogliono nascondere l'indirizzo IP del computer e possono essere usati per attacchi dannosi.</span><span class="sxs-lookup"><span data-stu-id="76a8d-105">These proxies are often used by users that want to hide their computer’s IP address, and may be used for malicious intent.</span></span>

<span data-ttu-id="76a8d-106">I risultati del report mostreranno il numero di volte in cui un utente ha effettuato correttamente l'accesso alla directory da quell'indirizzo e l'indirizzo IP del proxy.</span><span class="sxs-lookup"><span data-stu-id="76a8d-106">Results from this report will show the number of times a user successfully signed in to your directory from that address and the proxy’s IP address.</span></span>

![Accessi da origini sconosciute](./media/active-directory-reporting-sign-ins-from-unknown-sources/signInsFromUnknownSources.PNG)

