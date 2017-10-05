---
title: Azure Multi-Factor Authentication - Come funziona
description: "Azure multi-Factor Authentication contribuisce a salvaguardare l'accesso a dati e applicazioni rispondendo alla richiesta degli utenti di poter usare un processo di accesso semplice. Offre ulteriore sicurezza richiedendo una seconda forma di autenticazione nonché un'autenticazione avanzata tramite una gamma di opzioni di verifica semplice."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d14db902-9afe-4fca-b3a5-4bd54b3d8ec5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 6fee02885cc76b3a4fdad11e8702f623d6fe6597
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a><span data-ttu-id="9bd73-104">Come funziona Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="9bd73-104">How Azure Multi-Factor Authentication works</span></span>
<span data-ttu-id="9bd73-105">La sicurezza della verifica in due passaggi sta nel suo approccio a livelli.</span><span class="sxs-lookup"><span data-stu-id="9bd73-105">The security of two-step verification lies in its layered approach.</span></span> <span data-ttu-id="9bd73-106">La manomissione di più fattori rappresenta una sfida significativa per gli autori di attacchi.</span><span class="sxs-lookup"><span data-stu-id="9bd73-106">Compromising multiple authentication factors presents a significant challenge for attackers.</span></span> <span data-ttu-id="9bd73-107">Tuttavia, anche se un autore di attacco riesce a ottenere la password dell'utente, questa risulta inutile se non è in possesso del dispositivo attendibile.</span><span class="sxs-lookup"><span data-stu-id="9bd73-107">Even if an attacker manages to learn the user's password, it is useless without also having possession of the trusted device.</span></span> 

![Verifica](./media/multi-factor-authentication-how-it-works/howitworks.png)

<span data-ttu-id="9bd73-109">Azure multi-Factor Authentication contribuisce a salvaguardare l'accesso a dati e applicazioni rispondendo alla richiesta degli utenti di poter usare un processo di accesso semplice.</span><span class="sxs-lookup"><span data-stu-id="9bd73-109">Azure Multi-Factor Authentication helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span>  <span data-ttu-id="9bd73-110">Offre ulteriore sicurezza richiedendo una seconda forma di autenticazione nonché un'autenticazione avanzata tramite una gamma di opzioni di verifica semplice.</span><span class="sxs-lookup"><span data-stu-id="9bd73-110">It provides additional security by requiring a second form of authentication and delivers strong authentication via a range of easy verification options.</span></span>


## <a name="methods-available-for-two-step-verification"></a><span data-ttu-id="9bd73-111">Metodi disponibili per la verifica in due passaggi</span><span class="sxs-lookup"><span data-stu-id="9bd73-111">Methods available for two-step verification</span></span>
<span data-ttu-id="9bd73-112">Quando un utente accede, una verifica aggiuntiva viene inviata all'utente.</span><span class="sxs-lookup"><span data-stu-id="9bd73-112">When a user signs in, an additional verification is sent to the user.</span></span>  <span data-ttu-id="9bd73-113">Di seguito è riportato un elenco di metodi che possono essere utilizzati per la seconda verifica.</span><span class="sxs-lookup"><span data-stu-id="9bd73-113">The following are a list of methods that can be used for this second verification.</span></span>

| <span data-ttu-id="9bd73-114">Metodo di verifica</span><span class="sxs-lookup"><span data-stu-id="9bd73-114">Verification Method</span></span> | <span data-ttu-id="9bd73-115">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9bd73-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9bd73-116">Chiamata telefonica</span><span class="sxs-lookup"><span data-stu-id="9bd73-116">Phone call</span></span> |<span data-ttu-id="9bd73-117">Viene eseguita una chiamata al telefono registrato di un utente.</span><span class="sxs-lookup"><span data-stu-id="9bd73-117">A call is placed to a user’s registered phone.</span></span> <span data-ttu-id="9bd73-118">Se è necessario l'utente immette un PIN, quindi preme il tasto #.</span><span class="sxs-lookup"><span data-stu-id="9bd73-118">The user enters a PIN if necessary then presses the # key.</span></span> |
| <span data-ttu-id="9bd73-119">SMS</span><span class="sxs-lookup"><span data-stu-id="9bd73-119">Text message</span></span> |<span data-ttu-id="9bd73-120">Viene inviato un SMS al cellulare dell'utente con un codice di sei cifre.</span><span class="sxs-lookup"><span data-stu-id="9bd73-120">A text message is sent to a user’s mobile phone with a six-digit code.</span></span> <span data-ttu-id="9bd73-121">L'utente immette il codice nella pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="9bd73-121">The user enters this code on the sign-in page.</span></span> |
| <span data-ttu-id="9bd73-122">Notifica dell'app per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="9bd73-122">Mobile app notification</span></span> |<span data-ttu-id="9bd73-123">Viene inviata una richiesta di verifica allo smartphone dell'utente.</span><span class="sxs-lookup"><span data-stu-id="9bd73-123">A verification request is sent to a user’s smart phone.</span></span> <span data-ttu-id="9bd73-124">L'utente immette il PIN, se necessario, quindi seleziona **Verifica** nell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="9bd73-124">The user enters a PIN if necessary then selects **Verify** on the mobile app.</span></span> |
| <span data-ttu-id="9bd73-125">Codice di verifica dell'app per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="9bd73-125">Mobile app verification code</span></span> |<span data-ttu-id="9bd73-126">L'app per dispositivi mobili, che è in esecuzione sullo smartphone dell'utente, mostra un codice di verifica che cambia ogni 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="9bd73-126">The mobile app, which is running on a user’s smart phone, displays a verification code that changes every 30 seconds.</span></span> <span data-ttu-id="9bd73-127">L'utente individua il codice più recente e lo inserisce nella pagina di accesso.</span><span class="sxs-lookup"><span data-stu-id="9bd73-127">The user finds the most recent code and enters it on the sign-in page.</span></span> |
| <span data-ttu-id="9bd73-128">Token OATH di terze parti</span><span class="sxs-lookup"><span data-stu-id="9bd73-128">Third-party OATH tokens</span></span> | <span data-ttu-id="9bd73-129">Il server Azure Multi-Factor Authentication può essere configurato per accettare metodi di verifica di terze parti.</span><span class="sxs-lookup"><span data-stu-id="9bd73-129">Azure Multi-Factor Authentication Server can be configured to accept third-party verification methods.</span></span> |

<span data-ttu-id="9bd73-130">Azure multi-Factor Authentication fornisce metodi di verifica selezionabili per cloud e server.</span><span class="sxs-lookup"><span data-stu-id="9bd73-130">Azure Multi-Factor Authentication provides selectable verification methods for both cloud and server.</span></span> <span data-ttu-id="9bd73-131">È possibile scegliere i metodi disponibili per gli utenti: telefonata, SMS, notifica dell'app o codici dell'app.</span><span class="sxs-lookup"><span data-stu-id="9bd73-131">You can choose which methods are available for your users: phone call, text, app notification, or app codes.</span></span> <span data-ttu-id="9bd73-132">Per altre informazioni, vedere i [metodi di verifica selezionabili](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span><span class="sxs-lookup"><span data-stu-id="9bd73-132">For more information, see [selectable verification methods](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9bd73-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9bd73-133">Next steps</span></span>

- <span data-ttu-id="9bd73-134">Informazioni sulle diverse [versioni e i metodi di utilizzo per Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="9bd73-134">Read about the different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>

- <span data-ttu-id="9bd73-135">Scegliere se distribuire Azure MFA [nel cloud o in locale](multi-factor-authentication-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="9bd73-135">Choose whether to deploy Azure MFA [in the cloud or on-premises](multi-factor-authentication-get-started.md)</span></span>

- <span data-ttu-id="9bd73-136">Risposte alle [Domande frequenti](multi-factor-authentication-faq.md)</span><span class="sxs-lookup"><span data-stu-id="9bd73-136">Read answers for [Frequently asked questions](multi-factor-authentication-faq.md)</span></span>