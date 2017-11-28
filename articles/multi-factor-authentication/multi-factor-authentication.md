---
title: aaaLearn sulla verifica in due fasi in Azure MFA | Documenti Microsoft
description: "Che cos'è Azure multi-factor Authentication, motivo per cui utilizzare autenticazione a più fattori, informazioni sui client di multi-factor Authentication hello e diversi metodi di hello e le versioni disponibili. "
keywords: "Introduzione tooMFA, panoramica di autenticazione a più fattori, che cos'è mfa"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: c40d7a34-1274-4496-96b0-784850c06e9b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: kgremban
ms.openlocfilehash: a91b8d6941d2b6ce72a789a97c57e10e594e7ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a><span data-ttu-id="844b6-104">Informazioni su Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="844b6-104">What is Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="844b6-105">Verifica in due passaggi è un metodo di autenticazione che richiede più di un metodo di verifica e aggiunge un secondo livello critico di sicurezza toouser accessi e le transazioni.</span><span class="sxs-lookup"><span data-stu-id="844b6-105">Two-step verification is a method of authentication that requires more than one verification method and adds a critical second layer of security toouser sign-ins and transactions.</span></span> <span data-ttu-id="844b6-106">Funziona richiedendo due o più dei seguenti metodi di verifica hello:</span><span class="sxs-lookup"><span data-stu-id="844b6-106">It works by requiring any two or more of hello following verification methods:</span></span>

* <span data-ttu-id="844b6-107">Un'informazione nota (in genere una password)</span><span class="sxs-lookup"><span data-stu-id="844b6-107">Something you know (typically a password)</span></span>
* <span data-ttu-id="844b6-108">Un oggetto che si possiede (un dispositivo attendibile non facile da duplicare, ad esempio un telefono)</span><span class="sxs-lookup"><span data-stu-id="844b6-108">Something you have (a trusted device that is not easily duplicated, like a phone)</span></span>
* <span data-ttu-id="844b6-109">Una caratteristica fisica dell'utente (biometrica)</span><span class="sxs-lookup"><span data-stu-id="844b6-109">Something you are (biometrics)</span></span>

<span data-ttu-id="844b6-110"><center>![Nome utente e password](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificati](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smartphone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart card](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart card virtuale](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Nome utente e password](./media/multi-factor-authentication/cert.png)</center></span><span class="sxs-lookup"><span data-stu-id="844b6-110"><center>![Username and Password](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificates](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Phone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Card](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Virtual Smart Card](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Username and Password](./media/multi-factor-authentication/cert.png)</center></span></span>

<span data-ttu-id="844b6-111">Azure Multi-Factor Authentication (MFA) è una soluzione di verifica in due passaggi di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="844b6-111">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution.</span></span> <span data-ttu-id="844b6-112">Azure MFA consente di salvaguardare accesso toodata e applicazioni rispettando richiesta dell'utente per un semplice processo.</span><span class="sxs-lookup"><span data-stu-id="844b6-112">Azure MFA helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="844b6-113">Offre autenticazione avanzata tramite una gamma di metodi di verifica, fra cui una telefonata, un SMS o una verifica dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="844b6-113">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a><span data-ttu-id="844b6-114">Vantaggi dell'uso di Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="844b6-114">Why use Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="844b6-115">Oggi più che mai le persone sono sempre più connesse.</span><span class="sxs-lookup"><span data-stu-id="844b6-115">Today, more than ever, people are increasingly connected.</span></span> <span data-ttu-id="844b6-116">Con Smartphone, Tablet, laptop e PC, gli utenti sono disponibili varie opzioni in modalità sta tooconnect e rimanere connessi in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="844b6-116">With smart phones, tablets, laptops, and PCs, people have several different options on how they are going tooconnect and stay connected at any time.</span></span> <span data-ttu-id="844b6-117">Le persone possono accedere ai propri account e alle applicazioni da qualsiasi luogo e questo significa poter svolgere più attività e servire meglio i clienti.</span><span class="sxs-lookup"><span data-stu-id="844b6-117">People can access their accounts and applications from anywhere, which means that they can get more work done and serve their customers better.</span></span>

<span data-ttu-id="844b6-118">Azure multi-Factor Authentication è un semplice toouse, scalabile e soluzione affidabile che offre un secondo metodo di autenticazione in modo gli utenti sono sempre protetti.</span><span class="sxs-lookup"><span data-stu-id="844b6-118">Azure Multi-Factor Authentication is an easy toouse, scalable, and reliable solution that provides a second method of authentication so your users are always protected.</span></span>

| ![TooUse semplice](./media/multi-factor-authentication/simple.png) | ![Scalabile](./media/multi-factor-authentication/scalable.png) | ![Sempre protetti](./media/multi-factor-authentication/protected.png) | ![Affidabile](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| <span data-ttu-id="844b6-123">**Toouse semplice**</span><span class="sxs-lookup"><span data-stu-id="844b6-123">**Easy toouse**</span></span> |<span data-ttu-id="844b6-124">**Scalabile**</span><span class="sxs-lookup"><span data-stu-id="844b6-124">**Scalable**</span></span> |<span data-ttu-id="844b6-125">**Sempre protetti**</span><span class="sxs-lookup"><span data-stu-id="844b6-125">**Always Protected**</span></span> |<span data-ttu-id="844b6-126">**Affidabile**</span><span class="sxs-lookup"><span data-stu-id="844b6-126">**Reliable**</span></span> |

* <span data-ttu-id="844b6-127">**Facile tooUse** -Azure multi-Factor Authentication è semplice tooset backup e usare.</span><span class="sxs-lookup"><span data-stu-id="844b6-127">**Easy tooUse** - Azure Multi-Factor Authentication is simple tooset up and use.</span></span> <span data-ttu-id="844b6-128">Hello protezione aggiuntiva fornita con Azure multi-Factor Authentication consente agli utenti toomanage i propri dispositivi.</span><span class="sxs-lookup"><span data-stu-id="844b6-128">hello extra protection that comes with Azure Multi-Factor Authentication allows users toomanage their own devices.</span></span> <span data-ttu-id="844b6-129">L'aspetto più importante è che in molti casi può essere configurata con pochi semplici clic.</span><span class="sxs-lookup"><span data-stu-id="844b6-129">Best of all, in many instances it can be set up with just a few simple clicks.</span></span>
* <span data-ttu-id="844b6-130">**Scalabile** -Azure multi-Factor Authentication Usa power hello del cloud hello e si integra con locale Active Directory e le applicazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="844b6-130">**Scalable** - Azure Multi-Factor Authentication uses hello power of hello cloud and integrates with your on-premises AD and custom apps.</span></span> <span data-ttu-id="844b6-131">Questa protezione viene estesa anche tooyour scenari di volumi elevati di importanza critica.</span><span class="sxs-lookup"><span data-stu-id="844b6-131">This protection is even extended tooyour high-volume, mission-critical scenarios.</span></span>
* <span data-ttu-id="844b6-132">**Sempre protetti** -Azure multi-Factor Authentication fornisce autenticazione avanzata mediante massimi standard del settore di hello.</span><span class="sxs-lookup"><span data-stu-id="844b6-132">**Always Protected** - Azure Multi-Factor Authentication provides strong authentication using hello highest industry standards.</span></span>
* <span data-ttu-id="844b6-133">**Affidabile** : la disponibilità di Azure Multi-Factor Authentication è garantita al 99,9%.</span><span class="sxs-lookup"><span data-stu-id="844b6-133">**Reliable** - We guarantee 99.9% availability of Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="844b6-134">Hello servizio verrà considerato non disponibile quando è in grado di richieste di verifica tooreceive o un processo di verifica in due passaggi hello.</span><span class="sxs-lookup"><span data-stu-id="844b6-134">hello service is considered unavailable when it is unable tooreceive or process verification requests for hello two-step verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a><span data-ttu-id="844b6-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="844b6-135">Next steps</span></span>

- <span data-ttu-id="844b6-136">Informazioni su [come funziona Azure Multi-Factor Authentication](multi-factor-authentication-how-it-works.md)</span><span class="sxs-lookup"><span data-stu-id="844b6-136">Learn about [how Azure Multi-Factor Authentication works](multi-factor-authentication-how-it-works.md)</span></span>

- <span data-ttu-id="844b6-137">Informazioni sulle diversa hello [versioni e i metodi di utilizzo per Azure multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="844b6-137">Read about hello different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>
