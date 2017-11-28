---
title: aaaAzure AD Connect in Germania Cloud Microsoft
description: "Azure AD Connect integra le directory locali con Azure Active Directory. In questo modo tooprovide un'identità comune per le applicazioni di Office 365, Azure e SaaS integrata con Azure AD."
keywords: "Introduzione tooAzure AD Connect, panoramica di Azure AD Connect, che cos'è Azure AD Connect, installare active directory, in Germania, foresta nero"
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
ms.openlocfilehash: f32194fa6c365614f68e5d1ddcf0dac44d223292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a><span data-ttu-id="9a50d-105">Azure AD Connect in Microsoft Cloud per la Germania: anteprima pubblica</span><span class="sxs-lookup"><span data-stu-id="9a50d-105">Azure AD Connect in Microsoft Cloud Germany - Public Preview</span></span>
## <a name="introduction"></a><span data-ttu-id="9a50d-106">Introduzione</span><span class="sxs-lookup"><span data-stu-id="9a50d-106">Introduction</span></span>
<span data-ttu-id="9a50d-107">Azure AD Connect consente la sincronizzazione tra Active Directory locale e Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9a50d-107">Azure AD Connect provides synchronization between your on-premises Active Directory and Azure Active Directory.</span></span>
<span data-ttu-id="9a50d-108">Attualmente, molti degli scenari di hello in [Microsoft Cloud Germania](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) deve essere eseguita dall'operatore hello.</span><span class="sxs-lookup"><span data-stu-id="9a50d-108">Currently, many of hello scenarios in [Microsoft Cloud Germany](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) must be done by hello operator.</span></span> <span data-ttu-id="9a50d-109">Quando si utilizza Microsoft Cloud Germania, è necessario prestare attenzione hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="9a50d-109">When using Microsoft Cloud Germany, you must be aware of hello following:</span></span>

* <span data-ttu-id="9a50d-110">Hello che seguenti URL deve essere aperta su un server proxy per la sincronizzazione toooccur correttamente:</span><span class="sxs-lookup"><span data-stu-id="9a50d-110">hello following URLs must be opened on a proxy server for synchronization toooccur successfully:</span></span>
  
  * <span data-ttu-id="9a50d-111">*.microsoftonline.de</span><span class="sxs-lookup"><span data-stu-id="9a50d-111">*.microsoftonline.de</span></span>
  * <span data-ttu-id="9a50d-112">*.windows.net</span><span class="sxs-lookup"><span data-stu-id="9a50d-112">*.windows.net</span></span>
  * * <span data-ttu-id="9a50d-113">Elenchi di revoche dei certificati</span><span class="sxs-lookup"><span data-stu-id="9a50d-113">Certificate Revocation Lists</span></span>
* <span data-ttu-id="9a50d-114">Quando si accede nella directory di Azure AD tooyour, è necessario utilizzare un account nel dominio onmicrosoft.de hello.</span><span class="sxs-lookup"><span data-stu-id="9a50d-114">When you sign in tooyour Azure AD directory, you must use an account in hello onmicrosoft.de domain.</span></span>
* <span data-ttu-id="9a50d-115">Hello seguenti caratteristiche non sono disponibile:</span><span class="sxs-lookup"><span data-stu-id="9a50d-115">hello following features are not available:</span></span>
  * <span data-ttu-id="9a50d-116">Azure AD Connect Health</span><span class="sxs-lookup"><span data-stu-id="9a50d-116">Azure AD Connect Health</span></span>
  * <span data-ttu-id="9a50d-117">Aggiornamenti automatici</span><span class="sxs-lookup"><span data-stu-id="9a50d-117">Automatic updates</span></span>
 
## <a name="download"></a><span data-ttu-id="9a50d-118">Scaricare</span><span class="sxs-lookup"><span data-stu-id="9a50d-118">Download</span></span>
<span data-ttu-id="9a50d-119">È possibile scaricare Azure AD Connect dal Pannello di hello Azure AD Connect nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="9a50d-119">You can download Azure AD Connect from hello Azure AD Connect blade within hello portal.</span></span>  <span data-ttu-id="9a50d-120">Utilizzare le istruzioni di hello seguito blade di toolocate hello Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9a50d-120">Use hello instructions below toolocate hello Azure AD Connect blade.</span></span>

### <a name="hello-azure-ad-connect-blade"></a><span data-ttu-id="9a50d-121">Hello Azure AD Connect pannello</span><span class="sxs-lookup"><span data-stu-id="9a50d-121">hello Azure AD Connect Blade</span></span>
<span data-ttu-id="9a50d-122">Dopo l'accesso nel portale di Azure toohello, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="9a50d-122">Once you have signed in toohello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="9a50d-123">Passare tooBrowse</span><span class="sxs-lookup"><span data-stu-id="9a50d-123">Go tooBrowse</span></span>
2. <span data-ttu-id="9a50d-124">Selezionare Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9a50d-124">Select Azure Active Directory</span></span>
3. <span data-ttu-id="9a50d-125">Selezionare Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="9a50d-125">Then select Azure AD Connect</span></span>

<span data-ttu-id="9a50d-126">Verrà visualizzato hello segue:</span><span class="sxs-lookup"><span data-stu-id="9a50d-126">You should see hello following:</span></span>

![Pannello Azure AD Connect](media/active-directory-aadconnect-germany/germany1.png)

<span data-ttu-id="9a50d-128">Hello tabella seguente vengono descritte le funzionalità di hello illustrate nel pannello hello.</span><span class="sxs-lookup"><span data-stu-id="9a50d-128">hello following table describes hello features shown in hello blade.</span></span>

| <span data-ttu-id="9a50d-129">Titolo</span><span class="sxs-lookup"><span data-stu-id="9a50d-129">Title</span></span> | <span data-ttu-id="9a50d-130">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9a50d-130">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9a50d-131">STATO SINCRONIZZAZIONE</span><span class="sxs-lookup"><span data-stu-id="9a50d-131">SYNC STATUS</span></span> |<span data-ttu-id="9a50d-132">Indica se la sincronizzazione è abilitata o disabilitata.</span><span class="sxs-lookup"><span data-stu-id="9a50d-132">Let's you know whether synchronization is enabled or disabled.</span></span> |
| <span data-ttu-id="9a50d-133">ULTIMA SINCRONIZZAZIONE</span><span class="sxs-lookup"><span data-stu-id="9a50d-133">LAST SYNC</span></span> |<span data-ttu-id="9a50d-134">Hello ultima una sincronizzazione completata.</span><span class="sxs-lookup"><span data-stu-id="9a50d-134">hello last time a successful sync completed.</span></span> |
| <span data-ttu-id="9a50d-135">DOMINI FEDERATI</span><span class="sxs-lookup"><span data-stu-id="9a50d-135">FEDERATED DOMAINS</span></span> |<span data-ttu-id="9a50d-136">Mostra il numero di hello di domini federati attualmente configurato.</span><span class="sxs-lookup"><span data-stu-id="9a50d-136">Shows hello number of federated domains currently configured.</span></span> |

## <a name="installation"></a><span data-ttu-id="9a50d-137">Installazione</span><span class="sxs-lookup"><span data-stu-id="9a50d-137">Installation</span></span>
<span data-ttu-id="9a50d-138">tooinstall Azure AD Connect, è possibile utilizzare la documentazione di hello [qui](active-directory-aadconnect.md#install-azure-ad-connect).</span><span class="sxs-lookup"><span data-stu-id="9a50d-138">tooinstall Azure AD Connect, you can use hello documentation [here](active-directory-aadconnect.md#install-azure-ad-connect).</span></span>

## <a name="advanced-features-and-additional-information"></a><span data-ttu-id="9a50d-139">Funzionalità avanzate e informazioni aggiuntive</span><span class="sxs-lookup"><span data-stu-id="9a50d-139">Advanced features and Additional Information</span></span>
<span data-ttu-id="9a50d-140">Per altre informazioni e indicazioni sulle impostazioni personalizzate o sulle configurazioni avanzate, vedere [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="9a50d-140">For additional information and guidance on custom settings or advanced configurations, start with [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>  <span data-ttu-id="9a50d-141">Questa pagina fornisce informazioni e collegamenti tooadditional indicazioni.</span><span class="sxs-lookup"><span data-stu-id="9a50d-141">This page provides information and links tooadditional guidance.</span></span>

