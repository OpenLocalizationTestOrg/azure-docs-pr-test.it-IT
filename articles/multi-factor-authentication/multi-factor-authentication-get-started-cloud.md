---
title: aaaGet avviato Azure MFA nel cloud hello | Documenti Microsoft
description: "Si tratta di pagina di autenticazione di Microsoft Azure multi-Factor hello che descrive la modalità di avvio tooget con Azure MFA nel cloud hello."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 6b2e6549-1a26-4666-9c4a-cbe5d64c4e66
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/24/2017
ms.author: kgremban
ms.openlocfilehash: a4aaf44bf08d96f2baad155072fdd6e0e727ce8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-in-hello-cloud"></a><span data-ttu-id="9ef70-103">Introduzione ad Azure multi-Factor Authentication nel cloud hello</span><span class="sxs-lookup"><span data-stu-id="9ef70-103">Getting started with Azure Multi-Factor Authentication in hello cloud</span></span>
<span data-ttu-id="9ef70-104">Questo articolo descrive la modalità di avvio tramite Azure multi-Factor Authentication nel cloud hello tooget.</span><span class="sxs-lookup"><span data-stu-id="9ef70-104">This article walks through how tooget started using Azure Multi-Factor Authentication in hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="9ef70-105">Hello documentazione riportata di seguito vengono fornite informazioni su come gli utenti tooenable utilizzando hello **portale di Azure classico**.</span><span class="sxs-lookup"><span data-stu-id="9ef70-105">hello following documentation provides information on how tooenable users using hello **Azure Classic Portal**.</span></span> <span data-ttu-id="9ef70-106">Se si cercano informazioni su come tooset di Azure multi-Factor Authentication per gli utenti di Office 365, vedere [configurare multi-factor authentication per Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span><span class="sxs-lookup"><span data-stu-id="9ef70-106">If you are looking for information on how tooset up Azure Multi-Factor Authentication for O365 users, see [Set up multi-factor authentication for Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span></span>

![Autenticazione a più fattori in hello Cloud](./media/multi-factor-authentication-get-started-cloud/mfa_in_cloud.png)

## <a name="prerequisite"></a><span data-ttu-id="9ef70-108">Prerequisito</span><span class="sxs-lookup"><span data-stu-id="9ef70-108">Prerequisite</span></span>
<span data-ttu-id="9ef70-109">[Iscriversi per una sottoscrizione di Azure](https://azure.microsoft.com/pricing/free-trial/) -se si dispone già di una sottoscrizione di Azure, è necessario toosign-up per uno.</span><span class="sxs-lookup"><span data-stu-id="9ef70-109">[Sign up for an Azure subscription](https://azure.microsoft.com/pricing/free-trial/) - If you do not already have an Azure subscription, you need toosign-up for one.</span></span> <span data-ttu-id="9ef70-110">Se si è appena iniziato a usare il servizio Azure MFA, è possibile usare una sottoscrizione di valutazione</span><span class="sxs-lookup"><span data-stu-id="9ef70-110">If you are just starting out and using Azure MFA you can use a trial subscription</span></span>

## <a name="enable-azure-multi-factor-authentication"></a><span data-ttu-id="9ef70-111">Abilitare Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="9ef70-111">Enable Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="9ef70-112">Fino a quando gli utenti hanno le licenze che includono Azure multi-Factor Authentication, non è che occorre tooturn toodo su Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="9ef70-112">As long as your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="9ef70-113">È possibile iniziare a richiedere la verifica in due passaggi per i singoli utenti.</span><span class="sxs-lookup"><span data-stu-id="9ef70-113">You can start requiring two-step verification on an individual user basis.</span></span> <span data-ttu-id="9ef70-114">licenze di Hello che consentono l'autenticazione a più fattori di Azure sono:</span><span class="sxs-lookup"><span data-stu-id="9ef70-114">hello licenses that enable Azure MFA are:</span></span>
- <span data-ttu-id="9ef70-115">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="9ef70-115">Azure Multi-Factor Authentication</span></span>
- <span data-ttu-id="9ef70-116">Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="9ef70-116">Azure Active Directory Premium</span></span>
- <span data-ttu-id="9ef70-117">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="9ef70-117">Enterprise Mobility + Security</span></span>

<span data-ttu-id="9ef70-118">Se non si dispone di una di queste tre licenze, o non è sufficiente toocover licenze tutti gli utenti che ok troppo.</span><span class="sxs-lookup"><span data-stu-id="9ef70-118">If you don't have one of these three licenses, or you don't have enough licenses toocover all of your users, that's ok too.</span></span> <span data-ttu-id="9ef70-119">È sufficiente toodo un passaggio aggiuntivo e [creare un Provider multi-Factor Authentication](multi-factor-authentication-get-started-auth-provider.md) nella directory.</span><span class="sxs-lookup"><span data-stu-id="9ef70-119">You just have toodo an extra step and [Create a Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md) in your directory.</span></span>

## <a name="turn-on-two-step-verification-for-users"></a><span data-ttu-id="9ef70-120">Attivare la verifica in due passaggi per gli utenti</span><span class="sxs-lookup"><span data-stu-id="9ef70-120">Turn on two-step verification for users</span></span>

<span data-ttu-id="9ef70-121">Utilizzare una delle procedure hello elencate in [come toorequire di verifica in due passaggi per un utente o gruppo](multi-factor-authentication-get-started-user-states.md) toostart tramite Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="9ef70-121">Use one of hello procedures listed in [How toorequire two-step verification for a user or group](multi-factor-authentication-get-started-user-states.md) toostart using Azure MFA.</span></span> <span data-ttu-id="9ef70-122">È possibile scegliere di verifica in due passaggi tooenforce per tutti gli accessi, oppure è possibile creare verifica in due passaggi toorequire criteri di accesso condizionale solo quando è importante tooyou.</span><span class="sxs-lookup"><span data-stu-id="9ef70-122">You can choose tooenforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when it matters tooyou.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ef70-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9ef70-123">Next Steps</span></span>
<span data-ttu-id="9ef70-124">Ora che impostati Azure multi-Factor Authentication nel cloud hello, è possibile configurare e impostare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="9ef70-124">Now that you have set up Azure Multi-Factor Authentication in hello cloud, you can configure and set up your deployment.</span></span> <span data-ttu-id="9ef70-125">Per altri dettagli, vedere [Configurazione di Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md).</span><span class="sxs-lookup"><span data-stu-id="9ef70-125">See [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) for more details.</span></span>

