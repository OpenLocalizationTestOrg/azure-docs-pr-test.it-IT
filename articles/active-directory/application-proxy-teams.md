---
title: Accedere alle app del proxy app di Azure AD in Teams | Microsoft Docs
description: Usare il proxy applicazione di Azure AD per accedere all'applicazione locale tramite Microsoft Teams.
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
ms.openlocfilehash: 24e22d7314de536714a825cd7035d2cec2112278
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a><span data-ttu-id="19437-103">Accedere alle applicazioni locali tramite Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="19437-103">Access your on-premises applications through Microsoft Teams</span></span>

<span data-ttu-id="19437-104">Il proxy applicazione di Azure Active Directory consente l'accesso Single Sign-On alle applicazioni locali ovunque ci si trovi e Microsoft Teams ottimizza le attività di collaborazione in un'unica posizione.</span><span class="sxs-lookup"><span data-stu-id="19437-104">Azure Active Directory Application Proxy gives you single sign-on to on-premises applications no matter where you are, and Microsoft Teams streamlines your collaborative efforts in one place.</span></span> <span data-ttu-id="19437-105">Integrandoli, gli utenti e possono collaborare in modo produttivo con i colleghi in ogni situazione.</span><span class="sxs-lookup"><span data-stu-id="19437-105">Integrating the two together means that your users can be productive with their teammates in any situation.</span></span> 

<span data-ttu-id="19437-106">Gli utenti possono aggiungere le app per cloud ai canali di Teams [usando le schede](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), ma, nel caso in cui un sito di SharePoint o uno strumento di pianificazione usato da tutti sia ospitato in locale,</span><span class="sxs-lookup"><span data-stu-id="19437-106">Your users can add cloud apps to their Teams channels [using tabs](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), but what happens if that SharePoint site or planning tool they all use is hosted on-premises?</span></span> <span data-ttu-id="19437-107">il proxy di applicazione è la soluzione ideale.</span><span class="sxs-lookup"><span data-stu-id="19437-107">Application Proxy is the solution.</span></span> <span data-ttu-id="19437-108">Gli utenti possono aggiungere ai canali le app pubblicate tramite il proxy di applicazione usando gli stessi URL esterni che usano sempre per accedere alle app in remoto</span><span class="sxs-lookup"><span data-stu-id="19437-108">They can add apps published through Application Proxy to their channels using the same external URLs they always use to access their apps remotely.</span></span> <span data-ttu-id="19437-109">e, poiché il proxy di applicazione esegue l'autenticazione tramite Azure Active Directory, viene effettuato lo stesso accesso Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="19437-109">And because Application Proxy authenticates through Azure Active Directory, the same single sign-on experience carries through.</span></span>


## <a name="install-the-application-proxy-connector-and-publish-your-app"></a><span data-ttu-id="19437-110">Installare il connettore proxy applicazione e pubblicare l'app</span><span class="sxs-lookup"><span data-stu-id="19437-110">Install the Application Proxy connector and publish your app</span></span>

<span data-ttu-id="19437-111">Se necessario, [configurare il proxy di applicazione per il tenant e installare il connettore](active-directory-application-proxy-enable.md),</span><span class="sxs-lookup"><span data-stu-id="19437-111">If you haven't already, [configure Application Proxy for your tenant and install the connector](active-directory-application-proxy-enable.md).</span></span> <span data-ttu-id="19437-112">quindi [pubblicare l'applicazione locale](application-proxy-publish-azure-portal.md) per l'accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="19437-112">Then, [publish your on-premises application](application-proxy-publish-azure-portal.md) for remote access.</span></span> <span data-ttu-id="19437-113">Quando si pubblica l'app, prendere nota dell'URL esterno perché gli utenti finali hanno bisogno di questa informazione quando aggiungono l'app a Teams.</span><span class="sxs-lookup"><span data-stu-id="19437-113">When you're publishing the app, make note of the external URL because your end users need that information when they add the app to Teams.</span></span>

<span data-ttu-id="19437-114">Se le app sono già state pubblicate, ma non si ricordano gli URL esterni, cercarli nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="19437-114">If you already have your apps published but don't remember their external URLs, look them up in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="19437-115">Eseguire l'accesso, quindi passare ad **Azure Active Directory** > **Applicazioni aziendali** > **Tutte le applicazioni** > selezionare l'app > **Proxy dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="19437-115">Sign in, then navigate to **Azure Active Directory** > **Enterprise applications** > **All applications** > select your app > **Application proxy**.</span></span>

## <a name="add-your-app-to-teams"></a><span data-ttu-id="19437-116">Aggiungere l'app a Teams</span><span class="sxs-lookup"><span data-stu-id="19437-116">Add your app to Teams</span></span>

<span data-ttu-id="19437-117">Dopo avere pubblicato l'app tramite il proxy di applicazione, informare gli utenti che possono aggiungerla come scheda direttamente nei canali di Teams.</span><span class="sxs-lookup"><span data-stu-id="19437-117">Once you publish the app through Application Proxy, let your users know that they can add it as a tab directly in their Teams channels.</span></span> <span data-ttu-id="19437-118">Far eseguire questi tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="19437-118">Have them follow these three steps:</span></span>

1. <span data-ttu-id="19437-119">Passare al canale di Teams in cui si vuole aggiungere questa app e selezionare **+** per aggiungere una scheda.</span><span class="sxs-lookup"><span data-stu-id="19437-119">Navigate to the Teams channel where you want to add this app and select **+** to add a tab.</span></span>

   ![Selezionare l'opzione per aggiungere una scheda](./media/application-proxy-teams/add-tab.png)

2. <span data-ttu-id="19437-121">Selezionare **Sito Web** dalle opzioni della scheda.</span><span class="sxs-lookup"><span data-stu-id="19437-121">Select **Website** from the tab options.</span></span>

   ![Aggiungere un sito Web](./media/application-proxy-teams/website.png)

3. <span data-ttu-id="19437-123">Assegnare un nome alla scheda e impostare l'URL su quello esterno del proxy applicazione.</span><span class="sxs-lookup"><span data-stu-id="19437-123">Give the tab a name and set the URL to the Application Proxy external URL.</span></span> 

   ![Configurare il nome della scheda e l'URL](./media/application-proxy-teams/tab-name-url.png)

<span data-ttu-id="19437-125">La scheda, dopo che è stata aggiunta da un membro di un team, viene visualizzata da tutti nel canale.</span><span class="sxs-lookup"><span data-stu-id="19437-125">Once one member of a team adds the tab, it shows up for everyone in the channel.</span></span> <span data-ttu-id="19437-126">Tutti gli utenti che hanno accesso all'app ottengono l'accesso Single Sign-On con le credenziali usate per Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="19437-126">Any users who have access to the app get single sign-on access with the credentials they use for Microsoft Teams.</span></span> <span data-ttu-id="19437-127">Gli utenti che non hanno accesso all'app visualizzeranno la scheda in Teams, ma saranno bloccati finché non verranno concesse le autorizzazioni per l'app locale e la versione pubblicata nel portale di Azure dell'app.</span><span class="sxs-lookup"><span data-stu-id="19437-127">Any users who don't have access to the app will see the tab in Teams, but are blocked until you give them permissions to the on-premises app and the Azure portal published version of the app.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="19437-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="19437-128">Next steps</span></span>

- <span data-ttu-id="19437-129">Informazioni su come [pubblicare siti di SharePoint locali](application-proxy-enable-remote-access-sharepoint.md) con il proxy di applicazione.</span><span class="sxs-lookup"><span data-stu-id="19437-129">Learn how to [publish on-premises SharePoint sites](application-proxy-enable-remote-access-sharepoint.md) with Application Proxy.</span></span>
- <span data-ttu-id="19437-130">Configurare le app per usare i [domini personalizzati](active-directory-application-proxy-custom-domains.md) per l'URL esterno.</span><span class="sxs-lookup"><span data-stu-id="19437-130">Configure your apps to use [custom domains](active-directory-application-proxy-custom-domains.md) for their external URL.</span></span> 
