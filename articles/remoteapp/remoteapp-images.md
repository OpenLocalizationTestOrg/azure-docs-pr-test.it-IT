---
title: "Cosa è incluso nelle immagini modello di Azure RemoteApp | Documentazione Microsoft"
description: Informazioni sulle immagini modello incluse con Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9cd4e1a16a7c42bd00d9e543d7b62b72e9de3fc8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-in-the-azure-remoteapp-template-images"></a><span data-ttu-id="d6187-104">Cosa è incluso nelle immagini modello di Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="d6187-104">What is in the Azure RemoteApp template images?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d6187-105">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="d6187-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="d6187-106">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="d6187-106">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="d6187-107">La sottoscrizione di Azure RemoteApp include tre immagini modello:</span><span class="sxs-lookup"><span data-stu-id="d6187-107">Your Azure RemoteApp subscription includes three template images:</span></span>

* <span data-ttu-id="d6187-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="d6187-108">Windows Server 2012</span></span>
* <span data-ttu-id="d6187-109">Microsoft Office 365 ProPlus (richiede una sottoscrizione di Office 365)</span><span class="sxs-lookup"><span data-stu-id="d6187-109">Microsoft Office 365 ProPlus (Office 365 subscription required)</span></span>
* <span data-ttu-id="d6187-110">Microsoft Office 2013 Professional Plus (solo versione di valutazione)</span><span class="sxs-lookup"><span data-stu-id="d6187-110">Microsoft Office 2013 Professional Plus (trial only)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6187-111">La sottoscrizione di Azure RemoteApp consente di accedere al software nell'immagine, a eccezione di Office 365 ProPlus, che richiede una sottoscrizione separata, e di Office 2013, che non può essere usato nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="d6187-111">Your Azure RemoteApp subscription grants you access to the software in the images, with the exception of Office 365 ProPlus, which requires a separate subscription, and Office 2013, which cannot be used in production.</span></span> <span data-ttu-id="d6187-112">Ciò significa che è possibile condividere i programmi o le app nelle immagini modello con gli utenti.</span><span class="sxs-lookup"><span data-stu-id="d6187-112">This means that you can share the programs or apps on the template images with your users.</span></span> <span data-ttu-id="d6187-113">Ad esempio, se si crea una raccolta che usa l'immagine di Windows Server 2012 R2, è possibile pubblicare System Center Endpoint Protection per consentire agli utenti di accedere mediante RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="d6187-113">For example, if you create a collection that uses the Windows Server 2012 R2 image, you can publish System Center Endpoint Protection for users to access through RemoteApp.</span></span>
> 
> <span data-ttu-id="d6187-114">Per altre informazioni, consultare la pagina relativa ai [dettagli sulle licenze di RemoteApp](remoteapp-licensing.md) .</span><span class="sxs-lookup"><span data-stu-id="d6187-114">Check out the [RemoteApp licensing details](remoteapp-licensing.md) for more information.</span></span> <span data-ttu-id="d6187-115">Oltre a [Utilizzo di Office con Azure RemoteApp](remoteapp-o365.md) per le licenze di Office.</span><span class="sxs-lookup"><span data-stu-id="d6187-115">And [Using Office with Azure RemoteApp](remoteapp-o365.md) for the Office licensing info.</span></span>
> 
> 

<span data-ttu-id="d6187-116">Di seguito sono riportati i dettagli sul contenuto di ogni immagine.</span><span class="sxs-lookup"><span data-stu-id="d6187-116">Read on for details on what each image contains.</span></span>

## <a name="windows-server-2012-r2--the-vanilla-image"></a><span data-ttu-id="d6187-117">Windows Server 2012 R2 (immagine "vanilla")</span><span class="sxs-lookup"><span data-stu-id="d6187-117">Windows Server 2012 R2  ("the vanilla image")</span></span>
<span data-ttu-id="d6187-118">Questa immagine si basa sul sistema operativo Microsoft Windows Server 2012 R2 Datacenter e ha i seguenti ruoli e funzionalità installati per soddisfare i requisiti per le immagini modello di Azure RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="d6187-118">This image is based on Microsoft Windows Server 2012 R2 Datacenter operating system and has the following roles and features installed to meet the requirements for Azure RemoteApp template images:</span></span>

* <span data-ttu-id="d6187-119">.NET Framework 4.5, 3.5.1, 3.5</span><span class="sxs-lookup"><span data-stu-id="d6187-119">.NET Framework 4.5, 3.5.1, 3.5</span></span>
* <span data-ttu-id="d6187-120">Esperienza desktop</span><span class="sxs-lookup"><span data-stu-id="d6187-120">Desktop Experience</span></span>
* <span data-ttu-id="d6187-121">Servizi di riconoscimento della grafia</span><span class="sxs-lookup"><span data-stu-id="d6187-121">Ink and Handwriting Services</span></span>
* <span data-ttu-id="d6187-122">Media Foundation</span><span class="sxs-lookup"><span data-stu-id="d6187-122">Media Foundation</span></span>
* <span data-ttu-id="d6187-123">Host sessione Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="d6187-123">Remote Desktop Session Host</span></span>
* <span data-ttu-id="d6187-124">Windows PowerShell 4.0</span><span class="sxs-lookup"><span data-stu-id="d6187-124">Windows PowerShell 4.0</span></span>
* <span data-ttu-id="d6187-125">Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="d6187-125">Windows PowerShell ISE</span></span>
* <span data-ttu-id="d6187-126">Supporto WoW64</span><span class="sxs-lookup"><span data-stu-id="d6187-126">WoW64 Support</span></span>

<span data-ttu-id="d6187-127">Nell'immagine sono anche installate le applicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6187-127">This image also has the following applications installed:</span></span>

* <span data-ttu-id="d6187-128">Adobe Flash Player</span><span class="sxs-lookup"><span data-stu-id="d6187-128">Adobe Flash Player</span></span>
* <span data-ttu-id="d6187-129">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="d6187-129">Microsoft Silverlight</span></span>
* <span data-ttu-id="d6187-130">Microsoft System Center 2012 Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="d6187-130">Microsoft System Center 2012 Endpoint Protection</span></span>
* <span data-ttu-id="d6187-131">Microsoft Windows Media Player</span><span class="sxs-lookup"><span data-stu-id="d6187-131">Microsoft Windows Media Player</span></span>

## <a name="microsoft-office-365-proplus-subscription-required"></a><span data-ttu-id="d6187-132">Microsoft Office 365 ProPlus (sottoscrizione necessaria)</span><span class="sxs-lookup"><span data-stu-id="d6187-132">Microsoft Office 365 ProPlus (subscription required)</span></span>
<span data-ttu-id="d6187-133">Office 365 è l'applicazione più richiesta ed è pertanto stata creata un'immagine personalizzata pronta per l'uso.</span><span class="sxs-lookup"><span data-stu-id="d6187-133">Office 365 is the most requested application, so we created a "custom" image for you to work with.</span></span>

<span data-ttu-id="d6187-134">Si tratta di un'estensione dell'immagine "vanilla" e presenta i seguenti componenti di Microsoft Office 365 ProPlus installati, oltre a quelli descritti nell'immagine Windows Server 2012 R2:</span><span class="sxs-lookup"><span data-stu-id="d6187-134">This image is an extension of the vanilla image and has the following components of Microsoft Office 365 ProPlus installed in addition to the components described in the Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="d6187-135">Access</span><span class="sxs-lookup"><span data-stu-id="d6187-135">Access</span></span>
* <span data-ttu-id="d6187-136">Excel</span><span class="sxs-lookup"><span data-stu-id="d6187-136">Excel</span></span>
* <span data-ttu-id="d6187-137">Lync</span><span class="sxs-lookup"><span data-stu-id="d6187-137">Lync</span></span>
* <span data-ttu-id="d6187-138">OneNote</span><span class="sxs-lookup"><span data-stu-id="d6187-138">OneNote</span></span>
* <span data-ttu-id="d6187-139">OneDrive for Business. Si noti che l'agente di sincronizzazione non è supportato con Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="d6187-139">OneDrive for Business (note that the sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="d6187-140">Outlook</span><span class="sxs-lookup"><span data-stu-id="d6187-140">Outlook</span></span>
* <span data-ttu-id="d6187-141">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="d6187-141">PowerPoint</span></span>
* <span data-ttu-id="d6187-142">Word</span><span class="sxs-lookup"><span data-stu-id="d6187-142">Word</span></span>
* <span data-ttu-id="d6187-143">Strumenti di correzione di Microsoft Office</span><span class="sxs-lookup"><span data-stu-id="d6187-143">Microsoft Office Proofing Tools</span></span>

<span data-ttu-id="d6187-144">L'immagine include inoltre Visio Pro e Project Pro.</span><span class="sxs-lookup"><span data-stu-id="d6187-144">The image also includes Visio Pro and Project Pro.</span></span>

<span data-ttu-id="d6187-145">E anche le applicazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="d6187-145">And the following applications, as well:</span></span>

* <span data-ttu-id="d6187-146">SQL Native client</span><span class="sxs-lookup"><span data-stu-id="d6187-146">SQL Native client</span></span>
* <span data-ttu-id="d6187-147">Driver ODBC</span><span class="sxs-lookup"><span data-stu-id="d6187-147">ODBC Driver</span></span>
* <span data-ttu-id="d6187-148">Client di data mining di SQL Server</span><span class="sxs-lookup"><span data-stu-id="d6187-148">SQL Server Data Mining client</span></span>
* <span data-ttu-id="d6187-149">Client MasterDataServices</span><span class="sxs-lookup"><span data-stu-id="d6187-149">MasterDataServices client</span></span>
* <span data-ttu-id="d6187-150">Microsoft Publisher</span><span class="sxs-lookup"><span data-stu-id="d6187-150">Microsoft Publisher</span></span>
* <span data-ttu-id="d6187-151">PowerQuery</span><span class="sxs-lookup"><span data-stu-id="d6187-151">PowerQuery</span></span>
* <span data-ttu-id="d6187-152">PowerMap</span><span class="sxs-lookup"><span data-stu-id="d6187-152">PowerMap</span></span>

<span data-ttu-id="d6187-153">La piena funzionalità delle app di Office 365 ProPlus è disponibile solo per gli utenti che dispongono di un piano di Office 365 ProPlus.</span><span class="sxs-lookup"><span data-stu-id="d6187-153">Full functionality of Office 365 ProPlus apps is available only for users who have an Office 365 ProPlus plan.</span></span> <span data-ttu-id="d6187-154">Per altre informazioni sui piani di sottoscrizione di Office 365, vedere [Opzioni di piani di Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6187-154">For more details on the Office 365 subscription plans see [Office 365 service plans](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span></span> <span data-ttu-id="d6187-155">Altre domande?</span><span class="sxs-lookup"><span data-stu-id="d6187-155">Still have questions?</span></span> <span data-ttu-id="d6187-156">Consultare le informazioni di [Office 365 + RemoteApp](remoteapp-o365.md) .</span><span class="sxs-lookup"><span data-stu-id="d6187-156">Check out the [Office 365 + RemoteApp](remoteapp-o365.md) information.</span></span> <span data-ttu-id="d6187-157">Vedere anche il nuovo articolo [Come usare l'abbonamento a Office 365 con Azure RemoteApp](remoteapp-officesubscription.md).</span><span class="sxs-lookup"><span data-stu-id="d6187-157">Also check out the new article, [How to use your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).</span></span>

<span data-ttu-id="d6187-158">Si noti che è necessario concedere in licenza Office 365 ProPlus, Visio Pro e Project Pro separatamente, - ciascuno ha le propria licenze.</span><span class="sxs-lookup"><span data-stu-id="d6187-158">Note that you need to license Office 365 ProPlus, Visio Pro, and Project Pro separately - they each have their own license.</span></span>

## <a name="microsoft-office-2013-professional-plus-trial-only"></a><span data-ttu-id="d6187-159">Microsoft Office 2013 Professional Plus (solo versione di valutazione)</span><span class="sxs-lookup"><span data-stu-id="d6187-159">Microsoft Office 2013 Professional Plus (trial only)</span></span>
<span data-ttu-id="d6187-160">Durante il periodo di valutazione gratuita, è possibile provare il servizio con l'immagine di Office 2013.</span><span class="sxs-lookup"><span data-stu-id="d6187-160">During the free trial period, you can test the service with the Office 2013 image.</span></span>

<span data-ttu-id="d6187-161">Si tratta di un'estensione dell'immagine "vanilla" e presenta i seguenti componenti di Microsoft Office 2013 Professional Plus installati, oltre a quelli descritti nell'immagine Windows Server 2012 R2:</span><span class="sxs-lookup"><span data-stu-id="d6187-161">This image is an extension of the vanilla image and has the following components of Microsoft Office 2013 Professional Plus installed in addition to the components described in the Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="d6187-162">Access</span><span class="sxs-lookup"><span data-stu-id="d6187-162">Access</span></span>
* <span data-ttu-id="d6187-163">Excel</span><span class="sxs-lookup"><span data-stu-id="d6187-163">Excel</span></span>
* <span data-ttu-id="d6187-164">Lync</span><span class="sxs-lookup"><span data-stu-id="d6187-164">Lync</span></span>
* <span data-ttu-id="d6187-165">OneNote</span><span class="sxs-lookup"><span data-stu-id="d6187-165">OneNote</span></span>
* <span data-ttu-id="d6187-166">OneDrive for Business. Si noti che l'agente di sincronizzazione non è supportato con Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="d6187-166">OneDrive for Business (note that the sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="d6187-167">Outlook</span><span class="sxs-lookup"><span data-stu-id="d6187-167">Outlook</span></span>
* <span data-ttu-id="d6187-168">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="d6187-168">PowerPoint</span></span>
* <span data-ttu-id="d6187-169">Project</span><span class="sxs-lookup"><span data-stu-id="d6187-169">Project</span></span>
* <span data-ttu-id="d6187-170">Visio</span><span class="sxs-lookup"><span data-stu-id="d6187-170">Visio</span></span>
* <span data-ttu-id="d6187-171">Word</span><span class="sxs-lookup"><span data-stu-id="d6187-171">Word</span></span>
* <span data-ttu-id="d6187-172">Strumenti di correzione di Microsoft Office</span><span class="sxs-lookup"><span data-stu-id="d6187-172">Microsoft Office Proofing Tools</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6187-173">**Informazioni legali** : questa immagine non include una licenza di Microsoft Office e *non può essere usata per ambienti di produzione*.</span><span class="sxs-lookup"><span data-stu-id="d6187-173">**Legal information:** This image does not include a Microsoft Office license and *cannot be used for production*.</span></span> <span data-ttu-id="d6187-174">L'immagine di Office 2013 Professional Plus è destinata esclusivamente alla valutazione.</span><span class="sxs-lookup"><span data-stu-id="d6187-174">The Office 2013 Professional Plus image is intended for trial use only.</span></span> <span data-ttu-id="d6187-175">Se si desidera usare le applicazioni Office in Azure RemoteApp per la produzione, è necessario usare l'immagine di Office 365 ProPlus.</span><span class="sxs-lookup"><span data-stu-id="d6187-175">If you want to use Office apps in Azure RemoteApp for production, you need to use the Office 365 ProPlus image.</span></span> <span data-ttu-id="d6187-176">Per altre informazioni sulla licenza di Office, vedere [Usare Office 365 con Azure RemoteApp](remoteapp-o365.md)</span><span class="sxs-lookup"><span data-stu-id="d6187-176">For more details on licensing Office, see [Using Office 365 with Azure RemoteApp](remoteapp-o365.md)</span></span>
> 
> 

