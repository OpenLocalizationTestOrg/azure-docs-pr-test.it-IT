---
title: aaaAzure multi-Factor Authentication - funzionamento
description: "Azure multi-Factor Authentication consente di salvaguardare accesso toodata e applicazioni rispettando richiesta dell'utente per un semplice processo. Offre ulteriore sicurezza richiedendo una seconda forma di autenticazione nonché un'autenticazione avanzata tramite una gamma di opzioni di verifica semplice."
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
ms.openlocfilehash: 82f234fb86f145c42e8e56b8bdd2d61720c9ff2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-multi-factor-authentication-works"></a><span data-ttu-id="05259-104">Come funziona Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="05259-104">How Azure Multi-Factor Authentication works</span></span>
<span data-ttu-id="05259-105">sicurezza di Hello di verifica in due passaggi è compresa nel suo approccio a più livelli.</span><span class="sxs-lookup"><span data-stu-id="05259-105">hello security of two-step verification lies in its layered approach.</span></span> <span data-ttu-id="05259-106">La manomissione di più fattori rappresenta una sfida significativa per gli autori di attacchi.</span><span class="sxs-lookup"><span data-stu-id="05259-106">Compromising multiple authentication factors presents a significant challenge for attackers.</span></span> <span data-ttu-id="05259-107">Anche se un utente malintenzionato riesce toolearn hello password utente, è inutile senza anche in possesso del dispositivo attendibile hello.</span><span class="sxs-lookup"><span data-stu-id="05259-107">Even if an attacker manages toolearn hello user's password, it is useless without also having possession of hello trusted device.</span></span> 

![Verifica](./media/multi-factor-authentication-how-it-works/howitworks.png)

<span data-ttu-id="05259-109">Azure multi-Factor Authentication consente di salvaguardare accesso toodata e applicazioni rispettando richiesta dell'utente per un semplice processo.</span><span class="sxs-lookup"><span data-stu-id="05259-109">Azure Multi-Factor Authentication helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span>  <span data-ttu-id="05259-110">Offre ulteriore sicurezza richiedendo una seconda forma di autenticazione nonché un'autenticazione avanzata tramite una gamma di opzioni di verifica semplice.</span><span class="sxs-lookup"><span data-stu-id="05259-110">It provides additional security by requiring a second form of authentication and delivers strong authentication via a range of easy verification options.</span></span>


## <a name="methods-available-for-two-step-verification"></a><span data-ttu-id="05259-111">Metodi disponibili per la verifica in due passaggi</span><span class="sxs-lookup"><span data-stu-id="05259-111">Methods available for two-step verification</span></span>
<span data-ttu-id="05259-112">Quando un utente accede, una verifica aggiuntiva viene inviata toohello utente.</span><span class="sxs-lookup"><span data-stu-id="05259-112">When a user signs in, an additional verification is sent toohello user.</span></span>  <span data-ttu-id="05259-113">di seguito Hello sono un elenco di metodi che può essere utilizzato per la verifica di secondo.</span><span class="sxs-lookup"><span data-stu-id="05259-113">hello following are a list of methods that can be used for this second verification.</span></span>

| <span data-ttu-id="05259-114">Metodo di verifica</span><span class="sxs-lookup"><span data-stu-id="05259-114">Verification Method</span></span> | <span data-ttu-id="05259-115">Descrizione</span><span class="sxs-lookup"><span data-stu-id="05259-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="05259-116">Chiamata telefonica</span><span class="sxs-lookup"><span data-stu-id="05259-116">Phone call</span></span> |<span data-ttu-id="05259-117">Telefono registrato tooa dell'utente viene effettuata una chiamata.</span><span class="sxs-lookup"><span data-stu-id="05259-117">A call is placed tooa user’s registered phone.</span></span> <span data-ttu-id="05259-118">utente Hello immette un PIN, se necessario, quindi preme # hello.</span><span class="sxs-lookup"><span data-stu-id="05259-118">hello user enters a PIN if necessary then presses hello # key.</span></span> |
| <span data-ttu-id="05259-119">SMS</span><span class="sxs-lookup"><span data-stu-id="05259-119">Text message</span></span> |<span data-ttu-id="05259-120">Il telefono cellulare dell'utente tooa con un codice a sei cifre viene inviato un messaggio di testo.</span><span class="sxs-lookup"><span data-stu-id="05259-120">A text message is sent tooa user’s mobile phone with a six-digit code.</span></span> <span data-ttu-id="05259-121">Questo codice Hello immessi nella pagina di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="05259-121">hello user enters this code on hello sign-in page.</span></span> |
| <span data-ttu-id="05259-122">Notifica dell'app per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="05259-122">Mobile app notification</span></span> |<span data-ttu-id="05259-123">Smartphone dell'utente tooa viene inviata una richiesta di verifica.</span><span class="sxs-lookup"><span data-stu-id="05259-123">A verification request is sent tooa user’s smart phone.</span></span> <span data-ttu-id="05259-124">Hello utente immette il PIN, se necessario, quindi seleziona **verificare** su hello app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="05259-124">hello user enters a PIN if necessary then selects **Verify** on hello mobile app.</span></span> |
| <span data-ttu-id="05259-125">Codice di verifica dell'app per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="05259-125">Mobile app verification code</span></span> |<span data-ttu-id="05259-126">Hello app per dispositivi mobili, che è in esecuzione Smartphone dell'utente, viene visualizzato un codice di verifica che le modifiche apportate a ogni 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="05259-126">hello mobile app, which is running on a user’s smart phone, displays a verification code that changes every 30 seconds.</span></span> <span data-ttu-id="05259-127">utente Hello Trova codice più recente di hello e lo inserisce nella pagina di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="05259-127">hello user finds hello most recent code and enters it on hello sign-in page.</span></span> |
| <span data-ttu-id="05259-128">Token OATH di terze parti</span><span class="sxs-lookup"><span data-stu-id="05259-128">Third-party OATH tokens</span></span> | <span data-ttu-id="05259-129">Server di Azure multi-Factor Authentication può essere configurato tooaccept metodi di verifica di terze parti.</span><span class="sxs-lookup"><span data-stu-id="05259-129">Azure Multi-Factor Authentication Server can be configured tooaccept third-party verification methods.</span></span> |

<span data-ttu-id="05259-130">Azure multi-Factor Authentication fornisce metodi di verifica selezionabili per cloud e server.</span><span class="sxs-lookup"><span data-stu-id="05259-130">Azure Multi-Factor Authentication provides selectable verification methods for both cloud and server.</span></span> <span data-ttu-id="05259-131">È possibile scegliere i metodi disponibili per gli utenti: telefonata, SMS, notifica dell'app o codici dell'app.</span><span class="sxs-lookup"><span data-stu-id="05259-131">You can choose which methods are available for your users: phone call, text, app notification, or app codes.</span></span> <span data-ttu-id="05259-132">Per altre informazioni, vedere i [metodi di verifica selezionabili](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span><span class="sxs-lookup"><span data-stu-id="05259-132">For more information, see [selectable verification methods](multi-factor-authentication-whats-next.md#selectable-verification-methods).</span></span>

## <a name="next-steps"></a><span data-ttu-id="05259-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="05259-133">Next steps</span></span>

- <span data-ttu-id="05259-134">Informazioni sulle diversa hello [versioni e i metodi di utilizzo per Azure multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="05259-134">Read about hello different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>

- <span data-ttu-id="05259-135">Scegliere se toodeploy Azure MFA [in locale o cloud hello](multi-factor-authentication-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="05259-135">Choose whether toodeploy Azure MFA [in hello cloud or on-premises](multi-factor-authentication-get-started.md)</span></span>

- <span data-ttu-id="05259-136">Risposte alle [Domande frequenti](multi-factor-authentication-faq.md)</span><span class="sxs-lookup"><span data-stu-id="05259-136">Read answers for [Frequently asked questions](multi-factor-authentication-faq.md)</span></span>