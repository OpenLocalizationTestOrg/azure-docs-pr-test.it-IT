---
title: Proxy App di Azure AD App nei team aaaAccess | Documenti Microsoft
description: Utilizzare tooaccess Proxy dell'applicazione Azure Active Directory dell'applicazione locale tramite Teams Microsoft.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 13c36e43ae6349df09272e308ad4f40451cbbeb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a><span data-ttu-id="bea45-103">Accedere alle applicazioni locali tramite Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="bea45-103">Access your on-premises applications through Microsoft Teams</span></span>

<span data-ttu-id="bea45-104">Proxy di Active Directory dell'applicazione Azure offre applicazioni single sign-on tooon locale indipendentemente da dove si è e Microsoft Teams semplifica le attività di collaborazione in un'unica posizione.</span><span class="sxs-lookup"><span data-stu-id="bea45-104">Azure Active Directory Application Proxy gives you single sign-on tooon-premises applications no matter where you are, and Microsoft Teams streamlines your collaborative efforts in one place.</span></span> <span data-ttu-id="bea45-105">L'integrazione di hello due insieme significa che gli utenti possono essere produttivi con i propri colleghi in qualsiasi situazione.</span><span class="sxs-lookup"><span data-stu-id="bea45-105">Integrating hello two together means that your users can be productive with their teammates in any situation.</span></span> 

<span data-ttu-id="bea45-106">Gli utenti possono aggiungere cloud App tootheir team canali [utilizzando schede](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), ma cosa accade se il sito di SharePoint o un strumento di pianificazione tutte utilizzano è ospitato in locale?</span><span class="sxs-lookup"><span data-stu-id="bea45-106">Your users can add cloud apps tootheir Teams channels [using tabs](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), but what happens if that SharePoint site or planning tool they all use is hosted on-premises?</span></span> <span data-ttu-id="bea45-107">Proxy dell'applicazione è la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="bea45-107">Application Proxy is hello solution.</span></span> <span data-ttu-id="bea45-108">È possibile aggiungere le app pubblicate tramite il Proxy di applicazione tootheir canali utilizzando hello stesso URL esterni, essi utilizzano sempre tooaccess delle App in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="bea45-108">They can add apps published through Application Proxy tootheir channels using hello same external URLs they always use tooaccess their apps remotely.</span></span> <span data-ttu-id="bea45-109">E perché esegue l'autenticazione tramite Azure Active Directory, hello stesso esperienza single sign-on esegue tramite Proxy dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bea45-109">And because Application Proxy authenticates through Azure Active Directory, hello same single sign-on experience carries through.</span></span>


## <a name="install-hello-application-proxy-connector-and-publish-your-app"></a><span data-ttu-id="bea45-110">Installare il connettore Proxy dell'applicazione hello e pubblicare l'app</span><span class="sxs-lookup"><span data-stu-id="bea45-110">Install hello Application Proxy connector and publish your app</span></span>

<span data-ttu-id="bea45-111">Se hai già fatto, [configurare il Proxy di applicazione per il tenant e installare il connettore hello](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="bea45-111">If you haven't already, [configure Application Proxy for your tenant and install hello connector](active-directory-application-proxy-enable.md).</span></span> <span data-ttu-id="bea45-112">quindi [pubblicare l'applicazione locale](application-proxy-publish-azure-portal.md) per l'accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="bea45-112">Then, [publish your on-premises application](application-proxy-publish-azure-portal.md) for remote access.</span></span> <span data-ttu-id="bea45-113">Quando si pubblica l'applicazione hello, prendere nota dell'URL esterno hello perché gli utenti finali è necessario che tali informazioni durante l'aggiunta di hello app tooTeams.</span><span class="sxs-lookup"><span data-stu-id="bea45-113">When you're publishing hello app, make note of hello external URL because your end users need that information when they add hello app tooTeams.</span></span>

<span data-ttu-id="bea45-114">Se già App pubblicata ma non memorizza i relativi URL esterni, cercarli in hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bea45-114">If you already have your apps published but don't remember their external URLs, look them up in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="bea45-115">Eseguire l'accesso, quindi passare troppo**Azure Active Directory** > **applicazioni aziendali** > **tutte le applicazioni** > selezionare l'app > **Proxy dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="bea45-115">Sign in, then navigate too**Azure Active Directory** > **Enterprise applications** > **All applications** > select your app > **Application proxy**.</span></span>

## <a name="add-your-app-tooteams"></a><span data-ttu-id="bea45-116">Aggiungere il tooTeams app</span><span class="sxs-lookup"><span data-stu-id="bea45-116">Add your app tooTeams</span></span>

<span data-ttu-id="bea45-117">Dopo avere pubblicato l'applicazione hello mediante il Proxy di applicazione, informare gli utenti che è possibile aggiungere sotto forma di una scheda direttamente i canali del team.</span><span class="sxs-lookup"><span data-stu-id="bea45-117">Once you publish hello app through Application Proxy, let your users know that they can add it as a tab directly in their Teams channels.</span></span> <span data-ttu-id="bea45-118">Far eseguire questi tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="bea45-118">Have them follow these three steps:</span></span>

1. <span data-ttu-id="bea45-119">Passare toohello team del canale in cui si desidera tooadd questa app e selezionare  **+**  tooadd una scheda.</span><span class="sxs-lookup"><span data-stu-id="bea45-119">Navigate toohello Teams channel where you want tooadd this app and select **+** tooadd a tab.</span></span>

   ![Selezionare l'opzione per aggiungere una scheda](./media/application-proxy-teams/add-tab.png)

2. <span data-ttu-id="bea45-121">Selezionare **sito Web** da opzioni della scheda hello.</span><span class="sxs-lookup"><span data-stu-id="bea45-121">Select **Website** from hello tab options.</span></span>

   ![Aggiungere un sito Web](./media/application-proxy-teams/website.png)

3. <span data-ttu-id="bea45-123">Assegnare un nome di scheda hello e impostare l'URL esterno di hello URL toohello Proxy dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bea45-123">Give hello tab a name and set hello URL toohello Application Proxy external URL.</span></span> 

   ![Configurare il nome della scheda e l'URL](./media/application-proxy-teams/tab-name-url.png)

<span data-ttu-id="bea45-125">Una volta che un membro di un team aggiunge una scheda di hello, viene visualizzato per tutti gli utenti nel canale hello.</span><span class="sxs-lookup"><span data-stu-id="bea45-125">Once one member of a team adds hello tab, it shows up for everyone in hello channel.</span></span> <span data-ttu-id="bea45-126">Tutti gli utenti che dispongono di accesso toohello app ottengono l'accesso single sign-on con credenziali hello che usano per Teams Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bea45-126">Any users who have access toohello app get single sign-on access with hello credentials they use for Microsoft Teams.</span></span> <span data-ttu-id="bea45-127">Tutti gli utenti non dispongono di accesso toohello app verranno visualizzata la scheda hello in team, ma vengono bloccati finché non si assegnare loro autorizzazioni toohello locale app e hello Azure versione pubblicata del portale di app hello.</span><span class="sxs-lookup"><span data-stu-id="bea45-127">Any users who don't have access toohello app will see hello tab in Teams, but are blocked until you give them permissions toohello on-premises app and hello Azure portal published version of hello app.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bea45-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bea45-128">Next steps</span></span>

- <span data-ttu-id="bea45-129">Informazioni su come troppo[pubblicare i siti SharePoint locali](application-proxy-enable-remote-access-sharepoint.md) con Proxy dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bea45-129">Learn how too[publish on-premises SharePoint sites](application-proxy-enable-remote-access-sharepoint.md) with Application Proxy.</span></span>
- <span data-ttu-id="bea45-130">Configurare il toouse app [domini personalizzati](active-directory-application-proxy-custom-domains.md) per i relativi URL esterni.</span><span class="sxs-lookup"><span data-stu-id="bea45-130">Configure your apps toouse [custom domains](active-directory-application-proxy-custom-domains.md) for their external URL.</span></span> 
