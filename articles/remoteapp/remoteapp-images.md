---
title: aaaWhat si trova in immagini modello RemoteApp di Azure di hello? | Microsoft Docs
description: Informazioni sulle immagini modello hello incluse con Azure RemoteApp.
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
ms.openlocfilehash: ea012cec8dc581a8bd4a5a138ce302de19d5c6af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-in-hello-azure-remoteapp-template-images"></a><span data-ttu-id="40db6-104">Che cos'è immagini modello RemoteApp di Azure di hello?</span><span class="sxs-lookup"><span data-stu-id="40db6-104">What is in hello Azure RemoteApp template images?</span></span>
> [!IMPORTANT]
> <span data-ttu-id="40db6-105">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="40db6-105">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="40db6-106">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="40db6-106">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="40db6-107">La sottoscrizione di Azure RemoteApp include tre immagini modello:</span><span class="sxs-lookup"><span data-stu-id="40db6-107">Your Azure RemoteApp subscription includes three template images:</span></span>

* <span data-ttu-id="40db6-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="40db6-108">Windows Server 2012</span></span>
* <span data-ttu-id="40db6-109">Microsoft Office 365 ProPlus (richiede una sottoscrizione di Office 365)</span><span class="sxs-lookup"><span data-stu-id="40db6-109">Microsoft Office 365 ProPlus (Office 365 subscription required)</span></span>
* <span data-ttu-id="40db6-110">Microsoft Office 2013 Professional Plus (solo versione di valutazione)</span><span class="sxs-lookup"><span data-stu-id="40db6-110">Microsoft Office 2013 Professional Plus (trial only)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="40db6-111">La sottoscrizione di Azure RemoteApp consente di accedere software toohello nelle immagini di hello, con l'eccezione hello di Office 365 ProPlus, che richiede una sottoscrizione separata, e Office 2013, non può essere utilizzato nell'ambiente di produzione.</span><span class="sxs-lookup"><span data-stu-id="40db6-111">Your Azure RemoteApp subscription grants you access toohello software in hello images, with hello exception of Office 365 ProPlus, which requires a separate subscription, and Office 2013, which cannot be used in production.</span></span> <span data-ttu-id="40db6-112">Ciò significa che è possibile condividere i programmi hello o App sulle immagini modello hello con gli utenti.</span><span class="sxs-lookup"><span data-stu-id="40db6-112">This means that you can share hello programs or apps on hello template images with your users.</span></span> <span data-ttu-id="40db6-113">Ad esempio, se si crea una raccolta che usi l'immagine di Windows Server 2012 R2 hello, è possibile pubblicare System Center Endpoint Protection per gli utenti tooaccess tramite RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="40db6-113">For example, if you create a collection that uses hello Windows Server 2012 R2 image, you can publish System Center Endpoint Protection for users tooaccess through RemoteApp.</span></span>
> 
> <span data-ttu-id="40db6-114">Estrarre hello [RemoteApp licenze dettagli](remoteapp-licensing.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="40db6-114">Check out hello [RemoteApp licensing details](remoteapp-licensing.md) for more information.</span></span> <span data-ttu-id="40db6-115">E [utilizzando Office con Azure RemoteApp](remoteapp-o365.md) per hello informazioni sulle licenze di Office.</span><span class="sxs-lookup"><span data-stu-id="40db6-115">And [Using Office with Azure RemoteApp](remoteapp-o365.md) for hello Office licensing info.</span></span>
> 
> 

<span data-ttu-id="40db6-116">Di seguito sono riportati i dettagli sul contenuto di ogni immagine.</span><span class="sxs-lookup"><span data-stu-id="40db6-116">Read on for details on what each image contains.</span></span>

## <a name="windows-server-2012-r2--hello-vanilla-image"></a><span data-ttu-id="40db6-117">Windows Server 2012 R2 ("hello vaniglia immagine")</span><span class="sxs-lookup"><span data-stu-id="40db6-117">Windows Server 2012 R2  ("hello vanilla image")</span></span>
<span data-ttu-id="40db6-118">Questa immagine è basata su sistema operativo Microsoft Windows Server 2012 R2 Datacenter e hello seguenti ruoli e funzionalità installati toomeet requisiti di hello per le immagini modello RemoteApp di Azure:</span><span class="sxs-lookup"><span data-stu-id="40db6-118">This image is based on Microsoft Windows Server 2012 R2 Datacenter operating system and has hello following roles and features installed toomeet hello requirements for Azure RemoteApp template images:</span></span>

* <span data-ttu-id="40db6-119">.NET Framework 4.5, 3.5.1, 3.5</span><span class="sxs-lookup"><span data-stu-id="40db6-119">.NET Framework 4.5, 3.5.1, 3.5</span></span>
* <span data-ttu-id="40db6-120">Esperienza desktop</span><span class="sxs-lookup"><span data-stu-id="40db6-120">Desktop Experience</span></span>
* <span data-ttu-id="40db6-121">Servizi di riconoscimento della grafia</span><span class="sxs-lookup"><span data-stu-id="40db6-121">Ink and Handwriting Services</span></span>
* <span data-ttu-id="40db6-122">Media Foundation</span><span class="sxs-lookup"><span data-stu-id="40db6-122">Media Foundation</span></span>
* <span data-ttu-id="40db6-123">Host sessione Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="40db6-123">Remote Desktop Session Host</span></span>
* <span data-ttu-id="40db6-124">Windows PowerShell 4.0</span><span class="sxs-lookup"><span data-stu-id="40db6-124">Windows PowerShell 4.0</span></span>
* <span data-ttu-id="40db6-125">Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="40db6-125">Windows PowerShell ISE</span></span>
* <span data-ttu-id="40db6-126">Supporto WoW64</span><span class="sxs-lookup"><span data-stu-id="40db6-126">WoW64 Support</span></span>

<span data-ttu-id="40db6-127">Questa immagine presenta anche hello seguendo le applicazioni installate:</span><span class="sxs-lookup"><span data-stu-id="40db6-127">This image also has hello following applications installed:</span></span>

* <span data-ttu-id="40db6-128">Adobe Flash Player</span><span class="sxs-lookup"><span data-stu-id="40db6-128">Adobe Flash Player</span></span>
* <span data-ttu-id="40db6-129">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="40db6-129">Microsoft Silverlight</span></span>
* <span data-ttu-id="40db6-130">Microsoft System Center 2012 Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="40db6-130">Microsoft System Center 2012 Endpoint Protection</span></span>
* <span data-ttu-id="40db6-131">Microsoft Windows Media Player</span><span class="sxs-lookup"><span data-stu-id="40db6-131">Microsoft Windows Media Player</span></span>

## <a name="microsoft-office-365-proplus-subscription-required"></a><span data-ttu-id="40db6-132">Microsoft Office 365 ProPlus (sottoscrizione necessaria)</span><span class="sxs-lookup"><span data-stu-id="40db6-132">Microsoft Office 365 ProPlus (subscription required)</span></span>
<span data-ttu-id="40db6-133">Office 365 è hello più applicazione richiesta, pertanto è creata un'immagine di "custom" toowork con.</span><span class="sxs-lookup"><span data-stu-id="40db6-133">Office 365 is hello most requested application, so we created a "custom" image for you toowork with.</span></span>

<span data-ttu-id="40db6-134">Questa immagine è un'estensione dell'immagine di vaniglia hello e hello seguenti componenti di Microsoft Office 365 ProPlus installato inoltre componenti toohello descritti nell'immagine di Windows Server 2012 R2 hello:</span><span class="sxs-lookup"><span data-stu-id="40db6-134">This image is an extension of hello vanilla image and has hello following components of Microsoft Office 365 ProPlus installed in addition toohello components described in hello Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="40db6-135">Accesso</span><span class="sxs-lookup"><span data-stu-id="40db6-135">Access</span></span>
* <span data-ttu-id="40db6-136">Excel</span><span class="sxs-lookup"><span data-stu-id="40db6-136">Excel</span></span>
* <span data-ttu-id="40db6-137">Lync</span><span class="sxs-lookup"><span data-stu-id="40db6-137">Lync</span></span>
* <span data-ttu-id="40db6-138">OneNote</span><span class="sxs-lookup"><span data-stu-id="40db6-138">OneNote</span></span>
* <span data-ttu-id="40db6-139">OneDrive for Business (si noti che l'agente di sincronizzazione hello non è supportato per l'utilizzo con Azure RemoteApp)</span><span class="sxs-lookup"><span data-stu-id="40db6-139">OneDrive for Business (note that hello sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="40db6-140">Outlook</span><span class="sxs-lookup"><span data-stu-id="40db6-140">Outlook</span></span>
* <span data-ttu-id="40db6-141">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="40db6-141">PowerPoint</span></span>
* <span data-ttu-id="40db6-142">Word</span><span class="sxs-lookup"><span data-stu-id="40db6-142">Word</span></span>
* <span data-ttu-id="40db6-143">Strumenti di correzione di Microsoft Office</span><span class="sxs-lookup"><span data-stu-id="40db6-143">Microsoft Office Proofing Tools</span></span>

<span data-ttu-id="40db6-144">immagine di Hello include anche Visio Pro e progetto Pro.</span><span class="sxs-lookup"><span data-stu-id="40db6-144">hello image also includes Visio Pro and Project Pro.</span></span>

<span data-ttu-id="40db6-145">E hello applicazioni, di seguito:</span><span class="sxs-lookup"><span data-stu-id="40db6-145">And hello following applications, as well:</span></span>

* <span data-ttu-id="40db6-146">SQL Native client</span><span class="sxs-lookup"><span data-stu-id="40db6-146">SQL Native client</span></span>
* <span data-ttu-id="40db6-147">Driver ODBC</span><span class="sxs-lookup"><span data-stu-id="40db6-147">ODBC Driver</span></span>
* <span data-ttu-id="40db6-148">Client di data mining di SQL Server</span><span class="sxs-lookup"><span data-stu-id="40db6-148">SQL Server Data Mining client</span></span>
* <span data-ttu-id="40db6-149">Client MasterDataServices</span><span class="sxs-lookup"><span data-stu-id="40db6-149">MasterDataServices client</span></span>
* <span data-ttu-id="40db6-150">Microsoft Publisher</span><span class="sxs-lookup"><span data-stu-id="40db6-150">Microsoft Publisher</span></span>
* <span data-ttu-id="40db6-151">PowerQuery</span><span class="sxs-lookup"><span data-stu-id="40db6-151">PowerQuery</span></span>
* <span data-ttu-id="40db6-152">PowerMap</span><span class="sxs-lookup"><span data-stu-id="40db6-152">PowerMap</span></span>

<span data-ttu-id="40db6-153">La piena funzionalità delle app di Office 365 ProPlus è disponibile solo per gli utenti che dispongono di un piano di Office 365 ProPlus.</span><span class="sxs-lookup"><span data-stu-id="40db6-153">Full functionality of Office 365 ProPlus apps is available only for users who have an Office 365 ProPlus plan.</span></span> <span data-ttu-id="40db6-154">Per ulteriori informazioni sulla sottoscrizione di Office 365 hello vedere piani [i piani di servizio di Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span><span class="sxs-lookup"><span data-stu-id="40db6-154">For more details on hello Office 365 subscription plans see [Office 365 service plans](http://technet.microsoft.com/library/office-365-plan-options.aspx).</span></span> <span data-ttu-id="40db6-155">Altre domande?</span><span class="sxs-lookup"><span data-stu-id="40db6-155">Still have questions?</span></span> <span data-ttu-id="40db6-156">Estrarre hello [Office 365 + RemoteApp](remoteapp-o365.md) informazioni.</span><span class="sxs-lookup"><span data-stu-id="40db6-156">Check out hello [Office 365 + RemoteApp](remoteapp-o365.md) information.</span></span> <span data-ttu-id="40db6-157">Controllare inoltre il nuovo articolo hello, [come toouse l'abbonamento a Office 365 con Azure RemoteApp](remoteapp-officesubscription.md).</span><span class="sxs-lookup"><span data-stu-id="40db6-157">Also check out hello new article, [How toouse your Office 365 subscription with Azure RemoteApp](remoteapp-officesubscription.md).</span></span>

<span data-ttu-id="40db6-158">Si noti che è necessario toolicense Office 365 ProPlus Visio Pro e progetto Pro separatamente, ognuna di esse presenta la propria licenza.</span><span class="sxs-lookup"><span data-stu-id="40db6-158">Note that you need toolicense Office 365 ProPlus, Visio Pro, and Project Pro separately - they each have their own license.</span></span>

## <a name="microsoft-office-2013-professional-plus-trial-only"></a><span data-ttu-id="40db6-159">Microsoft Office 2013 Professional Plus (solo versione di valutazione)</span><span class="sxs-lookup"><span data-stu-id="40db6-159">Microsoft Office 2013 Professional Plus (trial only)</span></span>
<span data-ttu-id="40db6-160">Durante il periodo di valutazione gratuita di hello, è possibile testare il servizio di hello con immagine di hello Office 2013.</span><span class="sxs-lookup"><span data-stu-id="40db6-160">During hello free trial period, you can test hello service with hello Office 2013 image.</span></span>

<span data-ttu-id="40db6-161">Questa immagine è un'estensione dell'immagine di vaniglia hello e hello seguenti componenti di Microsoft Office 2013 Professional Plus installato inoltre componenti toohello descritti nell'immagine di Windows Server 2012 R2 hello:</span><span class="sxs-lookup"><span data-stu-id="40db6-161">This image is an extension of hello vanilla image and has hello following components of Microsoft Office 2013 Professional Plus installed in addition toohello components described in hello Windows Server 2012 R2 image:</span></span>

* <span data-ttu-id="40db6-162">Accesso</span><span class="sxs-lookup"><span data-stu-id="40db6-162">Access</span></span>
* <span data-ttu-id="40db6-163">Excel</span><span class="sxs-lookup"><span data-stu-id="40db6-163">Excel</span></span>
* <span data-ttu-id="40db6-164">Lync</span><span class="sxs-lookup"><span data-stu-id="40db6-164">Lync</span></span>
* <span data-ttu-id="40db6-165">OneNote</span><span class="sxs-lookup"><span data-stu-id="40db6-165">OneNote</span></span>
* <span data-ttu-id="40db6-166">OneDrive for Business (si noti che l'agente di sincronizzazione hello non è supportato per l'utilizzo con Azure RemoteApp)</span><span class="sxs-lookup"><span data-stu-id="40db6-166">OneDrive for Business (note that hello sync agent is not supported for use with Azure RemoteApp)</span></span>
* <span data-ttu-id="40db6-167">Outlook</span><span class="sxs-lookup"><span data-stu-id="40db6-167">Outlook</span></span>
* <span data-ttu-id="40db6-168">PowerPoint</span><span class="sxs-lookup"><span data-stu-id="40db6-168">PowerPoint</span></span>
* <span data-ttu-id="40db6-169">Project</span><span class="sxs-lookup"><span data-stu-id="40db6-169">Project</span></span>
* <span data-ttu-id="40db6-170">Visio</span><span class="sxs-lookup"><span data-stu-id="40db6-170">Visio</span></span>
* <span data-ttu-id="40db6-171">Word</span><span class="sxs-lookup"><span data-stu-id="40db6-171">Word</span></span>
* <span data-ttu-id="40db6-172">Strumenti di correzione di Microsoft Office</span><span class="sxs-lookup"><span data-stu-id="40db6-172">Microsoft Office Proofing Tools</span></span>

> [!IMPORTANT]
> <span data-ttu-id="40db6-173">**Informazioni legali** : questa immagine non include una licenza di Microsoft Office e *non può essere usata per ambienti di produzione*.</span><span class="sxs-lookup"><span data-stu-id="40db6-173">**Legal information:** This image does not include a Microsoft Office license and *cannot be used for production*.</span></span> <span data-ttu-id="40db6-174">immagine di Office 2013 Professional Plus Hello è solo per uso versione di valutazione.</span><span class="sxs-lookup"><span data-stu-id="40db6-174">hello Office 2013 Professional Plus image is intended for trial use only.</span></span> <span data-ttu-id="40db6-175">Se si desidera toouse Office App in Azure RemoteApp per la produzione, è necessario l'immagine di Office 365 ProPlus hello toouse.</span><span class="sxs-lookup"><span data-stu-id="40db6-175">If you want toouse Office apps in Azure RemoteApp for production, you need toouse hello Office 365 ProPlus image.</span></span> <span data-ttu-id="40db6-176">Per altre informazioni sulla licenza di Office, vedere [Usare Office 365 con Azure RemoteApp](remoteapp-o365.md)</span><span class="sxs-lookup"><span data-stu-id="40db6-176">For more details on licensing Office, see [Using Office 365 with Azure RemoteApp](remoteapp-o365.md)</span></span>
> 
> 

