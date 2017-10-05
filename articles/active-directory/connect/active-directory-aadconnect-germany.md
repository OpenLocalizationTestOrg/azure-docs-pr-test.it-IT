---
title: Azure AD Connect in Microsoft Cloud per la Germania
description: "Azure AD Connect integra le directory locali con Azure Active Directory. Consente di fornire un'identità comune per le applicazioni di Office 365, Azure e SaaS integrate con Azure AD."
keywords: "introduzione ad Azure AD Connect, panoramica di Azure AD Connect, che cos'è Azure AD Connect, installare Active Directory, Germania, Foresta Nera"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 4c55b116c0dc080ae316caca873a7b693caa793b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a><span data-ttu-id="2cd05-105">Azure AD Connect in Microsoft Cloud per la Germania: anteprima pubblica</span><span class="sxs-lookup"><span data-stu-id="2cd05-105">Azure AD Connect in Microsoft Cloud Germany - Public Preview</span></span>
## <a name="introduction"></a><span data-ttu-id="2cd05-106">Introduzione</span><span class="sxs-lookup"><span data-stu-id="2cd05-106">Introduction</span></span>
<span data-ttu-id="2cd05-107">Azure AD Connect consente la sincronizzazione tra Active Directory locale e Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2cd05-107">Azure AD Connect provides synchronization between your on-premises Active Directory and Azure Active Directory.</span></span>
<span data-ttu-id="2cd05-108">Attualmente, molti scenari in [Microsoft Cloud per la Germania](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) devono essere gestiti dall'operatore.</span><span class="sxs-lookup"><span data-stu-id="2cd05-108">Currently, many of the scenarios in [Microsoft Cloud Germany](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) must be done by the operator.</span></span> <span data-ttu-id="2cd05-109">Quando si usa Microsoft Cloud per la Germania, è necessario tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="2cd05-109">When using Microsoft Cloud Germany, you must be aware of the following:</span></span>

* <span data-ttu-id="2cd05-110">Gli URL seguenti devono essere aperti su un server proxy per eseguire correttamente la sincronizzazione:</span><span class="sxs-lookup"><span data-stu-id="2cd05-110">The following URLs must be opened on a proxy server for synchronization to occur successfully:</span></span>
  
  * <span data-ttu-id="2cd05-111">*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="2cd05-111">*.microsoftonline.de</span></span>
  * <span data-ttu-id="2cd05-112">*.windows.net</span><span class="sxs-lookup"><span data-stu-id="2cd05-112">*.windows.net</span></span>
  * * <span data-ttu-id="2cd05-113">Elenchi di revoche dei certificati</span><span class="sxs-lookup"><span data-stu-id="2cd05-113">Certificate Revocation Lists</span></span>
* <span data-ttu-id="2cd05-114">Quando si accede alla directory di Azure AD, è necessario usare un account nel dominio onmicrosoft.de.</span><span class="sxs-lookup"><span data-stu-id="2cd05-114">When you sign in to your Azure AD directory, you must use an account in the onmicrosoft.de domain.</span></span>
* <span data-ttu-id="2cd05-115">Non sono disponibili le funzionalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="2cd05-115">The following features are not available:</span></span>
  * <span data-ttu-id="2cd05-116">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="2cd05-116">Azure AD Connect Health</span></span>
  * <span data-ttu-id="2cd05-117">Aggiornamenti automatici</span><span class="sxs-lookup"><span data-stu-id="2cd05-117">Automatic updates</span></span>
 
## <a name="download"></a><span data-ttu-id="2cd05-118">Scaricare</span><span class="sxs-lookup"><span data-stu-id="2cd05-118">Download</span></span>
<span data-ttu-id="2cd05-119">È possibile scaricare Azure AD Connect dal pannello Azure AD Connect nel portale.</span><span class="sxs-lookup"><span data-stu-id="2cd05-119">You can download Azure AD Connect from the Azure AD Connect blade within the portal.</span></span>  <span data-ttu-id="2cd05-120">Usare le istruzioni seguenti per trovare il pannello Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="2cd05-120">Use the instructions below to locate the Azure AD Connect blade.</span></span>

### <a name="the-azure-ad-connect-blade"></a><span data-ttu-id="2cd05-121">Pannello Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="2cd05-121">The Azure AD Connect Blade</span></span>
<span data-ttu-id="2cd05-122">Dopo l'accesso al portale di Azure, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2cd05-122">Once you have signed in to the Azure portal, do the following:</span></span>

1. <span data-ttu-id="2cd05-123">Andare a Esplora</span><span class="sxs-lookup"><span data-stu-id="2cd05-123">Go to Browse</span></span>
2. <span data-ttu-id="2cd05-124">Selezionare Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2cd05-124">Select Azure Active Directory</span></span>
3. <span data-ttu-id="2cd05-125">Selezionare Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="2cd05-125">Then select Azure AD Connect</span></span>

<span data-ttu-id="2cd05-126">Dovrebbe essere visualizzata la seguente schermata:</span><span class="sxs-lookup"><span data-stu-id="2cd05-126">You should see the following:</span></span>

![Pannello Azure AD Connect](media/active-directory-aadconnect-germany/germany1.png)

<span data-ttu-id="2cd05-128">La tabella seguente illustra le funzionalità visualizzate nel pannello.</span><span class="sxs-lookup"><span data-stu-id="2cd05-128">The following table describes the features shown in the blade.</span></span>

| <span data-ttu-id="2cd05-129">Titolo</span><span class="sxs-lookup"><span data-stu-id="2cd05-129">Title</span></span> | <span data-ttu-id="2cd05-130">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2cd05-130">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2cd05-131">STATO SINCRONIZZAZIONE</span><span class="sxs-lookup"><span data-stu-id="2cd05-131">SYNC STATUS</span></span> |<span data-ttu-id="2cd05-132">Indica se la sincronizzazione è abilitata o disabilitata.</span><span class="sxs-lookup"><span data-stu-id="2cd05-132">Let's you know whether synchronization is enabled or disabled.</span></span> |
| <span data-ttu-id="2cd05-133">ULTIMA SINCRONIZZAZIONE</span><span class="sxs-lookup"><span data-stu-id="2cd05-133">LAST SYNC</span></span> |<span data-ttu-id="2cd05-134">Ultima volta in cui è stata completata correttamente una sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="2cd05-134">The last time a successful sync completed.</span></span> |
| <span data-ttu-id="2cd05-135">DOMINI FEDERATI</span><span class="sxs-lookup"><span data-stu-id="2cd05-135">FEDERATED DOMAINS</span></span> |<span data-ttu-id="2cd05-136">Indica il numero di domini federati attualmente configurati.</span><span class="sxs-lookup"><span data-stu-id="2cd05-136">Shows the number of federated domains currently configured.</span></span> |

## <a name="installation"></a><span data-ttu-id="2cd05-137">Installazione</span><span class="sxs-lookup"><span data-stu-id="2cd05-137">Installation</span></span>
<span data-ttu-id="2cd05-138">Per installare Azure AD Connect, è possibile usare la documentazione disponibile [qui](active-directory-aadconnect.md#install-azure-ad-connect).</span><span class="sxs-lookup"><span data-stu-id="2cd05-138">To install Azure AD Connect, you can use the documentation [here](active-directory-aadconnect.md#install-azure-ad-connect).</span></span>

## <a name="advanced-features-and-additional-information"></a><span data-ttu-id="2cd05-139">Funzionalità avanzate e informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="2cd05-139">Advanced features and Additional Information</span></span>
<span data-ttu-id="2cd05-140">Per altre informazioni e indicazioni sulle impostazioni personalizzate o sulle configurazioni avanzate, vedere [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="2cd05-140">For additional information and guidance on custom settings or advanced configurations, start with [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>  <span data-ttu-id="2cd05-141">Questa pagina contiene informazioni e collegamenti ad altre indicazioni.</span><span class="sxs-lookup"><span data-stu-id="2cd05-141">This page provides information and links to additional guidance.</span></span>

