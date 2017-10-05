---
title: Informazioni sulla verifica in due passaggi in Azure MFA | Documentazione Microsoft
description: "Cos'è Azure Multi-Factor Authentication (MFA) e perché usare questo servizio, informazioni sul client Multi-Factor Authentication e sui diversi metodi e versioni disponibili. "
keywords: "Introduzione a MFA, panoramica di mfa, che cos'è mfa"
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
ms.openlocfilehash: 7334ab5b278c3339fdbc2e363fd5c609604d3e14
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a><span data-ttu-id="4662d-104">Informazioni su Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="4662d-104">What is Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="4662d-105">La verifica in due passaggi è un metodo di autenticazione che richiede più di un metodo di verifica e con il quale viene aggiunto un secondo livello di sicurezza critico agli accessi e alle transazioni degli utenti.</span><span class="sxs-lookup"><span data-stu-id="4662d-105">Two-step verification is a method of authentication that requires more than one verification method and adds a critical second layer of security to user sign-ins and transactions.</span></span> <span data-ttu-id="4662d-106">In genere richiede due o più dei metodi di verifica seguenti:</span><span class="sxs-lookup"><span data-stu-id="4662d-106">It works by requiring any two or more of the following verification methods:</span></span>

* <span data-ttu-id="4662d-107">Un'informazione nota (in genere una password)</span><span class="sxs-lookup"><span data-stu-id="4662d-107">Something you know (typically a password)</span></span>
* <span data-ttu-id="4662d-108">Un oggetto che si possiede (un dispositivo attendibile non facile da duplicare, ad esempio un telefono)</span><span class="sxs-lookup"><span data-stu-id="4662d-108">Something you have (a trusted device that is not easily duplicated, like a phone)</span></span>
* <span data-ttu-id="4662d-109">Una caratteristica fisica dell'utente (biometrica)</span><span class="sxs-lookup"><span data-stu-id="4662d-109">Something you are (biometrics)</span></span>

<span data-ttu-id="4662d-110"><center>![Nome utente e password](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificati](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smartphone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart card](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart card virtuale](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Nome utente e password](./media/multi-factor-authentication/cert.png)</center></span><span class="sxs-lookup"><span data-stu-id="4662d-110"><center>![Username and Password](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificates](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Phone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Card](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Virtual Smart Card](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Username and Password](./media/multi-factor-authentication/cert.png)</center></span></span>

<span data-ttu-id="4662d-111">Azure Multi-Factor Authentication (MFA) è una soluzione di verifica in due passaggi di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4662d-111">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution.</span></span> <span data-ttu-id="4662d-112">Azure MFA consente di proteggere l'accesso ai dati e alle applicazioni dell'utente, garantendo al tempo stesso una procedura di accesso semplice.</span><span class="sxs-lookup"><span data-stu-id="4662d-112">Azure MFA helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="4662d-113">Offre autenticazione avanzata tramite una gamma di metodi di verifica, fra cui una telefonata, un SMS o una verifica dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="4662d-113">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a><span data-ttu-id="4662d-114">Vantaggi dell'uso di Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="4662d-114">Why use Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="4662d-115">Oggi più che mai le persone sono sempre più connesse.</span><span class="sxs-lookup"><span data-stu-id="4662d-115">Today, more than ever, people are increasingly connected.</span></span> <span data-ttu-id="4662d-116">Grazie a smartphone, tablet, portatili e computer, gli utenti possono contare su diverse opzioni per scegliere come connettersi e restare connessi in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="4662d-116">With smart phones, tablets, laptops, and PCs, people have several different options on how they are going to connect and stay connected at any time.</span></span> <span data-ttu-id="4662d-117">Le persone possono accedere ai propri account e alle applicazioni da qualsiasi luogo e questo significa poter svolgere più attività e servire meglio i clienti.</span><span class="sxs-lookup"><span data-stu-id="4662d-117">People can access their accounts and applications from anywhere, which means that they can get more work done and serve their customers better.</span></span>

<span data-ttu-id="4662d-118">Azure multi-Factor Authentication è una soluzione semplice da usare, scalabile e affidabile che offre un secondo metodo di autenticazione in modo che gli utenti siano sempre protetti.</span><span class="sxs-lookup"><span data-stu-id="4662d-118">Azure Multi-Factor Authentication is an easy to use, scalable, and reliable solution that provides a second method of authentication so your users are always protected.</span></span>

| ![Facile da usare](./media/multi-factor-authentication/simple.png) | ![Scalabile](./media/multi-factor-authentication/scalable.png) | ![Sempre protetti](./media/multi-factor-authentication/protected.png) | ![Affidabile](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| <span data-ttu-id="4662d-123">**Facile da usare**</span><span class="sxs-lookup"><span data-stu-id="4662d-123">**Easy to use**</span></span> |<span data-ttu-id="4662d-124">**Scalabile**</span><span class="sxs-lookup"><span data-stu-id="4662d-124">**Scalable**</span></span> |<span data-ttu-id="4662d-125">**Sempre protetti**</span><span class="sxs-lookup"><span data-stu-id="4662d-125">**Always Protected**</span></span> |<span data-ttu-id="4662d-126">**Affidabile**</span><span class="sxs-lookup"><span data-stu-id="4662d-126">**Reliable**</span></span> |

* <span data-ttu-id="4662d-127">**Facile da usare** : Azure Multi-Factor Authentication è semplice da configurare e usare.</span><span class="sxs-lookup"><span data-stu-id="4662d-127">**Easy to Use** - Azure Multi-Factor Authentication is simple to set up and use.</span></span> <span data-ttu-id="4662d-128">La protezione aggiuntiva offerta da Azure Multi-Factor Authentication consente agli utenti di usare e gestire i propri dispositivi.</span><span class="sxs-lookup"><span data-stu-id="4662d-128">The extra protection that comes with Azure Multi-Factor Authentication allows users to manage their own devices.</span></span> <span data-ttu-id="4662d-129">L'aspetto più importante è che in molti casi può essere configurata con pochi semplici clic.</span><span class="sxs-lookup"><span data-stu-id="4662d-129">Best of all, in many instances it can be set up with just a few simple clicks.</span></span>
* <span data-ttu-id="4662d-130">**Scalabile** : Azure Multi-Factor Authentication usa le potenzialità del cloud e si integra con Active Directory locale e con le app personalizzate.</span><span class="sxs-lookup"><span data-stu-id="4662d-130">**Scalable** - Azure Multi-Factor Authentication uses the power of the cloud and integrates with your on-premises AD and custom apps.</span></span> <span data-ttu-id="4662d-131">Questa protezione viene estesa anche agli scenari di importanza strategica con volumi elevati.</span><span class="sxs-lookup"><span data-stu-id="4662d-131">This protection is even extended to your high-volume, mission-critical scenarios.</span></span>
* <span data-ttu-id="4662d-132">**Sempre protetti** : Azure multi-Factor Authentication fornisce autenticazione avanzata grazie all'uso dei più elevati standard di settore.</span><span class="sxs-lookup"><span data-stu-id="4662d-132">**Always Protected** - Azure Multi-Factor Authentication provides strong authentication using the highest industry standards.</span></span>
* <span data-ttu-id="4662d-133">**Affidabile** : la disponibilità di Azure Multi-Factor Authentication è garantita al 99,9%.</span><span class="sxs-lookup"><span data-stu-id="4662d-133">**Reliable** - We guarantee 99.9% availability of Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="4662d-134">Il servizio viene considerato non disponibile quando non è in grado di ricevere o elaborare le richieste di verifica per la verifica in due passaggi.</span><span class="sxs-lookup"><span data-stu-id="4662d-134">The service is considered unavailable when it is unable to receive or process verification requests for the two-step verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a><span data-ttu-id="4662d-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4662d-135">Next steps</span></span>

- <span data-ttu-id="4662d-136">Informazioni su [come funziona Azure Multi-Factor Authentication](multi-factor-authentication-how-it-works.md)</span><span class="sxs-lookup"><span data-stu-id="4662d-136">Learn about [how Azure Multi-Factor Authentication works](multi-factor-authentication-how-it-works.md)</span></span>

- <span data-ttu-id="4662d-137">Informazioni sulle diverse [versioni e i metodi di utilizzo per Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="4662d-137">Read about the different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>
