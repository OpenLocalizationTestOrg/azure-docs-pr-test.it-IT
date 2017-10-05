---
title: Opzioni per la migrazione da Azure RemoteApp | Microsoft Docs
description: Informazioni sulle opzioni per la migrazione da Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 9ab63124e2521ee1922d15c1e388c54d50eb8301
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a><span data-ttu-id="cb8c4-103">Opzioni per la migrazione da Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="cb8c4-103">Options for migrating out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cb8c4-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="cb8c4-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="cb8c4-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>


<span data-ttu-id="cb8c4-106">Se si è interrotto l'uso di Azure RemoteApp dopo l'[annuncio del ritiro](https://go.microsoft.com/fwlink/?linkid=821148) o perché è terminato il periodo di valutazione, è necessario eseguire la migrazione da Azure RemoteApp a un altro servizio app.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-106">If you have stopped using Azure RemoteApp because of the [retirement announcement](https://go.microsoft.com/fwlink/?linkid=821148) or because you've finished your evaluation, you need to migrate off of Azure RemoteApp to another app service.</span></span> <span data-ttu-id="cb8c4-107">La migrazione può essere effettuata in due modi: con una distribuzione autogestita (spesso denominata Infrastructure as a Service [IaaS]) o tramite un'offerta completamente gestita (spesso denominata Platform as a Service oppure Software as a Service [PaaS/SaaS]).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-107">There are two different approaches for migrating: a self-managed (often called Infrastructure as a Service [IaaS]) deployment or a fully managed (often called Platform as a Service or Software as a Service [PaaS/SaaS]) offering.</span></span> 

<span data-ttu-id="cb8c4-108">L'approccio IaaS self-service consiste in una distribuzione "fai da te" gestita dall'utente e di sua proprietà, direttamente distribuita su macchine virtuali (VM) o sistemi fisici.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-108">Self-service IaaS is a do-it-yourself deployment that is managed, operated, and owned by you, directly deployed on virtual machines (VMs) or physical systems.</span></span> <span data-ttu-id="cb8c4-109">Altrimenti, un'offerta PaaS/SaaS completamente gestita è più simile ad Azure RemoteApp: un partner fornisce un livello di servizio in una soluzione .NET di comunicazione remota che gestisce gli aspetti operativi e di manutenzione, mentre il cliente si occupa di gestire app e immagini.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-109">At the other end, a fully managed PaaS/SaaS offering is more like Azure RemoteApp - a partner provides a service layer on top of a remoting solution that handles operational and servicing, while you, as the customer, do some image and app management.</span></span>

<span data-ttu-id="cb8c4-110">[Visualizzare il webinar di Azure RemoteApp sulle opzioni di migrazione](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp) oppure continuare a leggere per altre informazioni (inclusi alcuni esempi di diverse opzioni di hosting).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-110">[View the Azure RemoteApp webinars on migration options](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), or read on for more information (including examples of the different hosting options).</span></span>

## <a name="self-managed-iaas-solutions"></a><span data-ttu-id="cb8c4-111">Soluzioni autogestite (IaaS)</span><span class="sxs-lookup"><span data-stu-id="cb8c4-111">Self-managed (IaaS) solutions</span></span>
### <a name="rds-on-iaas"></a><span data-ttu-id="cb8c4-112">**RDS su IaaS**</span><span class="sxs-lookup"><span data-stu-id="cb8c4-112">**RDS on IaaS**</span></span>
<span data-ttu-id="cb8c4-113">È possibile implementare una distribuzione di Servizi Desktop remoto (in Windows Server) basata su una sessione nativa tramite RemoteApp o desktop locali oppure in un ambiente ospitato (come le VM di Azure).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-113">You can deploy a native session-based Remote Desktop Services (in Windows Server) deployment using either RemoteApp or desktops on-premises or in a hosted environment (like on Azure VMs).</span></span> <span data-ttu-id="cb8c4-114">Le distribuzioni di Servizi Desktop remoto su IaaS sono particolarmente indicate per i clienti che le conoscono già e che possiedono le necessarie competenze tecniche in merito.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-114">RDS on IaaS deployments are best for customers already familiar with and that have existing technical expertise with RDS deployments.</span></span> 

> [!NOTE]
> <span data-ttu-id="cb8c4-115">Per poter usufruire di questa opzione di distribuzione, è necessario disporre di un contratto multilicenza con Software Assurance (SA) per le licenze CAL per Servizi Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-115">You need Volume Licensing with Software Assurance (SA) for RDS client access licenses to use this deployment option.</span></span>

<span data-ttu-id="cb8c4-116">Distribuire Servizi Desktop remoto nelle VM di Azure è più semplice che mai se si usano i modelli di distribuzione e applicazione delle patch (leggere una [panoramica](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) e quindi [accedere ai modelli](https://aka.ms/rdautomation)).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-116">Deploying RDS on Azure VMs is easier than ever when you use deployment and patching templates (read an [overview](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) and then [go get them](https://aka.ms/rdautomation)).</span></span> <span data-ttu-id="cb8c4-117">Le stesse funzionalità di scalabilità elastica si ottengono con il modello di distribuzione classica di Azure (non il modello di risorse di Azure) all'interno di Azure RemoteApp tramite lo [script per la scalabilità automatica](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), pur essendo disponibili altre personalizzazioni e configurazioni.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-117">You can get the same elastic scaling capabilities with Azure classic deployment model resources (not Azure Resource Model resources) within Azure RemoteApp by using the [auto scaling script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), although there are more customizations and configurations.</span></span> <span data-ttu-id="cb8c4-118">Quando si distribuiscono i Servizi Desktop remoto su VM di Azure, è possibile avvalersi del [supporto tecnico di Azure](https://azure.microsoft.com/support/plans/), gestito dagli stessi professionisti che forniscono assistenza per Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-118">When you deploy RDS on Azure VMs, support is provided through [Azure Support](https://azure.microsoft.com/support/plans/), the same support professionals that supported you with Azure RemoteApp.</span></span> <span data-ttu-id="cb8c4-119">Per una stima dei costi basata sull'uso esistente, è possibile contattare il [supporto tecnico di Azure](https://azure.microsoft.com/support/plans/) oppure eseguire il calcolo autonomamente usando l'apposito strumento presto disponibile.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-119">You can get cost estimates based on your existing usage by contacting [Azure Support](https://azure.microsoft.com/support/plans/), or you can perform calculations yourself using a soon to be released Cost Calculator.</span></span>  <span data-ttu-id="cb8c4-120">Inoltre, con le VM serie N (attualmente in Private Preview), è possibile aggiungere vGPU. Per informazioni su come aggiungere vGPU e [sfruttare i miglioramenti dei Servizi Desktop remoto in Windows Server 2016](https://myignite.microsoft.com/videos/2794), è disponibile una sessione introduttiva.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-120">Also, with N-series VMs (currently in private preview) you can add vGPU - hear more about adding vGPU and about how to [harness RDS improvements in Windows Server 2016](https://myignite.microsoft.com/videos/2794) in our Ignite session.</span></span>   

<span data-ttu-id="cb8c4-121">Per un aiuto in fase di distribuzione, è possibile consultare le guide dettagliate alla distribuzione di [Windows Server 2012 R2](http://aka.ms/rdsonazure) e [Windows Server 2016](http://aka.ms/rdsonazure2016).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-121">We have step by step deployment guides for [Windows Server 2012 R2](http://aka.ms/rdsonazure) and [Windows Server 2016](http://aka.ms/rdsonazure2016) to assist with your deployment.</span></span> <span data-ttu-id="cb8c4-122">Per conoscere tutte le novità, consultare il [blog su Desktop remoto](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-122">Check out the [Remote Desktop blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) for the latest news.</span></span>

### <a name="citrix-on-iaas"></a><span data-ttu-id="cb8c4-123">**Citrix in IaaS**</span><span class="sxs-lookup"><span data-stu-id="cb8c4-123">**Citrix on IaaS**</span></span>
<span data-ttu-id="cb8c4-124">Una distribuzione Citrix nativa di XenApp o XenDesktop in base alla sessione può essere effettuata in locale o in un ambiente ospitato (ad esempio, nelle VM di Azure).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-124">A native Citrix deployment of session-based XenApp or XenDesktop can be deployed on-premises or within a hosted environment (such as on Azure VMs).</span></span> 

<span data-ttu-id="cb8c4-125">Per altre informazioni, consultare la guida dettagliata alla distribuzione [Citrix XA 7.6 in Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-125">Check out the step-by-step deployment guide, [Citrix XA 7.6 on Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), for more information.</span></span> <span data-ttu-id="cb8c4-126">Sono inoltre disponibili altre informazioni su [Citrix in Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), con in più il calcolatore dei prezzi.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-126">Read more about [Citrix on Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), including a price calculator.</span></span> <span data-ttu-id="cb8c4-127">Infine, è possibile discutere le opzioni disponibili con un [contatto Citrix](http://citrix.com/English/contact/index.asp).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-127">You can also find a [Citrix contact](http://citrix.com/English/contact/index.asp) to discuss your options with.</span></span>

## <a name="fully-managed-paassaas-offerings"></a><span data-ttu-id="cb8c4-128">Offerte completamente gestite (PaaS/SaaS)</span><span class="sxs-lookup"><span data-stu-id="cb8c4-128">Fully managed (PaaS/SaaS) offerings</span></span>

### <a name="citrix-xenapp-essentials-released-april-2017"></a><span data-ttu-id="cb8c4-129">Citrix XenApp Essentials (rilasciato nell'aprile 2017)</span><span class="sxs-lookup"><span data-stu-id="cb8c4-129">Citrix XenApp Essentials (released April 2017)</span></span>
<span data-ttu-id="cb8c4-130">Ora disponibile in [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials è il nuovo servizio di virtualizzazione delle applicazioni che combina la potenza e flessibilità della piattaforma Citrix Cloud con la visione semplice, prescrittiva e facile da usare di Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-130">Available now on the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials is the new application virtualization service, combining the power and flexibility of the Citrix Cloud platform with the simple, prescriptive, and easy-to-consume vision of Microsoft Azure RemoteApp.</span></span> 

<span data-ttu-id="cb8c4-131">I clienti di Azure RemoteApp esistenti possono [registrarsi per una prova gratuita](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-131">Existing Azure RemoteApp customers can [register for a free trial](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span></span>  <span data-ttu-id="cb8c4-132">Nota: solo il servizio utente Citrix è gratuito, verranno addebitati i costi di calcolo e archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="cb8c4-132">Note: Only Citrix user service charge is free, Azure compute and storage costs apply</span></span>

<span data-ttu-id="cb8c4-133">Altre informazioni:</span><span class="sxs-lookup"><span data-stu-id="cb8c4-133">Learn More:</span></span>
- [<span data-ttu-id="cb8c4-134">Come eseguire la migrazione da Azure RemoteApp a Citrix XenApp Essentials</span><span class="sxs-lookup"><span data-stu-id="cb8c4-134">Migrate from Azure RemoteApp to Citrix XenApp Essentials</span></span>](remoteapp-migrate-citrix.md)
- [<span data-ttu-id="cb8c4-135">Citrix e Microsoft</span><span class="sxs-lookup"><span data-stu-id="cb8c4-135">Citrix and Microsoft</span></span>](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- <span data-ttu-id="cb8c4-136">[Presentazione di Citrix XenApp Essentials](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-136">[Citrix XenApp Essentials presentation](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span></span>  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a><span data-ttu-id="cb8c4-137">Servizio Citrix Cloud XenApp e servizio XenDesktop</span><span class="sxs-lookup"><span data-stu-id="cb8c4-137">Citrix Cloud XenApp Service and XenDesktop Service</span></span> 

<span data-ttu-id="cb8c4-138">[Servizio Citrix Cloud XenApp e servizio XenDesktop](https://www.citrix.com/products/citrix-cloud/services.html) è la soluzione migliore per la fornitura sia di applicazioni che di desktop, oltre a capacità avanzate di gestione e monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-138">[Citrix Cloud XenApp Service and XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) is the best solution for the delivery of both apps and desktops, plus advanced management and monitoring capabilities.</span></span> 

#### <a name="conexlink-platform-name-mycloudit"></a><span data-ttu-id="cb8c4-139">Conexlink (nome della piattaforma: MyCloudIT)</span><span class="sxs-lookup"><span data-stu-id="cb8c4-139">Conexlink (Platform name: MyCloudIT)</span></span>
<span data-ttu-id="cb8c4-140">[MyCloudIT](https://mycloudit.com) è una piattaforma di automazione che consente alle aziende IT di semplificare, ottimizzare e ridimensionare la migrazione e l'erogazione di desktop remoti, applicazioni remote e infrastrutture nel cloud di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-140">[MyCloudIT](https://mycloudit.com) is an automation platform for IT companies to simplify, optimize, and scale the migration and delivery of remote desktops, remote applications, and infrastructure in the Microsoft Azure Cloud.</span></span> 

<span data-ttu-id="cb8c4-141">La piattaforma MyCloudIT riduce i tempi di distribuzione del 95% e i costi di Azure del 30%, trasferendo nel cloud l'intera infrastruttura IT di ogni cliente in poche sequenze di tasti.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-141">The MyCloudIT platform reduces deployment time by 95%, Azure cost by 30%, and moves their client's entire IT infrastructure into the cloud in a matter of a few key strokes.</span></span> <span data-ttu-id="cb8c4-142">Ora i partner possono gestire i clienti da un unico dashboard globale, assistere gli utenti finali del servizio in tutto il mondo come mai prima d'ora e aumentare i ricavi senza aggiungere costi generali o richiedere una formazione completa su Azure.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-142">Partners can now manage customers from one global dashboard, service end users around the world like never before, and grow revenues without adding additional overhead or extensive Azure training.</span></span>  

> <span data-ttu-id="cb8c4-143">Sede principale: Dallas (Texas)</span><span class="sxs-lookup"><span data-stu-id="cb8c4-143">Primary location: Dallas, TX, USA</span></span>
> 
> <span data-ttu-id="cb8c4-144">Regione operativa: tutto il mondo</span><span class="sxs-lookup"><span data-stu-id="cb8c4-144">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="cb8c4-145">Stato partner: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span><span class="sxs-lookup"><span data-stu-id="cb8c4-145">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span></span>
> 
> <span data-ttu-id="cb8c4-146">Provider di servizi cloud Microsoft: sì</span><span class="sxs-lookup"><span data-stu-id="cb8c4-146">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="cb8c4-147">Offerta di soluzioni desktop e RemoteApp basate sulla sessione: sì, entrambe</span><span class="sxs-lookup"><span data-stu-id="cb8c4-147">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="cb8c4-148">Soluzioni per la migrazione di Azure RemoteApp: sì, [altre informazioni](https://mycloudit.com/remote-app-microsoft/)</span><span class="sxs-lookup"><span data-stu-id="cb8c4-148">Azure RemoteApp migration solutions: Yes, [learn more](https://mycloudit.com/remote-app-microsoft/)</span></span>
> 
> <span data-ttu-id="cb8c4-149">Brian Garoutte, Vicepresidente dell'area Business Development</span><span class="sxs-lookup"><span data-stu-id="cb8c4-149">Brian Garoutte, VP of Business Development</span></span>
> 
> <span data-ttu-id="cb8c4-150">Telefono: 972-218-0741</span><span class="sxs-lookup"><span data-stu-id="cb8c4-150">Phone: 972-218-0741</span></span>
>   
> <span data-ttu-id="cb8c4-151">E-mail: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span><span class="sxs-lookup"><span data-stu-id="cb8c4-151">Email: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span></span>

### <a name="frame"></a><span data-ttu-id="cb8c4-152">Frame</span><span class="sxs-lookup"><span data-stu-id="cb8c4-152">Frame</span></span>

<span data-ttu-id="cb8c4-153">Organizzazioni IT in enterprise ed enti pubblici, fornitori di servizi gestiti e fornitori leader di software scelgono Frame per creare e gestire nel cloud aree di lavoro software-defined protette.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-153">IT organizations in enterprise and government, managed service providers, and leading software vendors choose Frame to create and manage their secure, software-defined workspaces in the cloud.</span></span> <span data-ttu-id="cb8c4-154">Dalle piccole alle grandi organizzazioni, Frame rende incredibilmente semplice l'accesso degli utenti alle applicazioni Windows in qualsiasi browser e da qualsiasi dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-154">From small to large organizations, Frame makes it incredibly easy to let users access Windows applications on any browser from any device.</span></span> <span data-ttu-id="cb8c4-155">La piattaforma Frame include tutto ciò che serve a un amministratore per distribuire le applicazioni dal cloud, inclusa l'infrastruttura di Azure e le licenze RDS (usare il proprio account Azure e le proprie licenze è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-155">The Frame platform includes everything an admin needs to deploy applications from the cloud including the Azure infrastructure and RDS licenses (bringing your own Azure account and licenses is optional).</span></span> 

<span data-ttu-id="cb8c4-156">Altre informazioni su [Frame in Azure](https://www.fra.me/ara).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-156">Learn more about [Frame on Azure](https://www.fra.me/ara).</span></span> 

> <span data-ttu-id="cb8c4-157">Località primaria: San Mateo, CA, USA</span><span class="sxs-lookup"><span data-stu-id="cb8c4-157">Primary location: San Mateo, CA, USA</span></span>
>
> <span data-ttu-id="cb8c4-158">Regione operativa: tutto il mondo</span><span class="sxs-lookup"><span data-stu-id="cb8c4-158">Operation region: Worldwide</span></span>
>
> <span data-ttu-id="cb8c4-159">Partner Microsoft: Sì</span><span class="sxs-lookup"><span data-stu-id="cb8c4-159">Microsoft Partner: Yes</span></span>
> 
> <span data-ttu-id="cb8c4-160">Telefono: 1-480-269-4668</span><span class="sxs-lookup"><span data-stu-id="cb8c4-160">Phone: 1-480-269-4668</span></span>

### <a name="awingu"></a><span data-ttu-id="cb8c4-161">Awingu</span><span class="sxs-lookup"><span data-stu-id="cb8c4-161">Awingu</span></span>
<span data-ttu-id="cb8c4-162">Awingu offre una semplice soluzione online per l'area di lavoro che esegue applicazioni legacy, SaaS e documenti da un browser html5.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-162">Awingu provides a simple online workspace solution running legacy apps, SaaS and documents from an html5 browser.</span></span> <span data-ttu-id="cb8c4-163">Di conseguenza rende disponibili tutte le applicazioni in modo sicuro in qualsiasi tipo di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-163">As such, making any applications securely available on any type of device.</span></span> <span data-ttu-id="cb8c4-164">Per i servizi SaaS è disponibile un'ampia gamma di opzioni Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-164">For SaaS services, a wide range op Single-Sign-On options is available.</span></span> <span data-ttu-id="cb8c4-165">Inoltre è possibile integrare profondamente diversi file system (cloud) nell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-165">Also diverse (cloud) files systems can be deeply integrated into your workspace.</span></span> <span data-ttu-id="cb8c4-166">Oltre alla mobilità totale, l'area di lavoro online avanzata di Awingu fornirà una sicurezza ottimale con controlli granulari (ad esempio download/caricamento), controllo sull'utilizzo completo, Multi-Factor Authentication (ad esempio Azure Multi-Factor Authentication), registrazione delle sessioni e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-166">Next to full mobility, Awingu's rich online workspace will give optimal security with granular controls (e.g. downloading/uploading), full usage auditing, Multi-Factor Authentication (e.g. Azure MFA), session recording and more.</span></span> <span data-ttu-id="cb8c4-167">Awingu consente in modo predefinito la condivisione dei documenti e delle sessioni di applicazione per una collaborazione ottimizzata e sicura.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-167">Out-of-the-box, Awingu enables document and application session sharing for optimized and secure collaboration.</span></span>
<span data-ttu-id="cb8c4-168">La soluzione Awingu è multi-tenant, multi-AD e open API.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-168">Awingu's solution is multi-tenant, multi-AD and open API.</span></span> <span data-ttu-id="cb8c4-169">È utilizzata da piccole e grandi aziende, provider di servizi cloud e [ISV](http://www.isv2saas.com).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-169">It is used by small and large businesses, Cloud Service Providers and [ISVs](http://www.isv2saas.com).</span></span> <span data-ttu-id="cb8c4-170">Questi clienti apprezzano soprattutto la facilità di utilizzo e installazione e il basso TCO.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-170">These customers especially appreciate the easy-of-use, ease-to-install and low TCO.</span></span>

<span data-ttu-id="cb8c4-171">Awingu All-in-One è [disponibile in Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) con 2 utenti contemporanei integrati.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-171">Awingu All-in-One is [available in the Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) with 2 built-in concurrent users.</span></span> <span data-ttu-id="cb8c4-172">Sono disponibili licenze aggiuntive tramite un'[ampia gamma di distributori e rivenditori](http://www.awingu.com/reseller).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-172">Additional licenses are available through a [wide range of distributors and resellers](http://www.awingu.com/reseller).</span></span>

<span data-ttu-id="cb8c4-173">Altre informazioni sono disponibili nell'articolo [Looking for an Azure RemoteApp alternative?](http://alternative-for-azure-remoteapp.awingu.com/) (Stai cercando un'alternativa a RemoteApp?).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-173">Learn more about [Awingu on as alternative to Azure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span></span>


> <span data-ttu-id="cb8c4-174">Sede principale: Belgio</span><span class="sxs-lookup"><span data-stu-id="cb8c4-174">Primary location: Belgium</span></span>
> 
> <span data-ttu-id="cb8c4-175">Aree operative: EMEA, America del Nord e Brasile</span><span class="sxs-lookup"><span data-stu-id="cb8c4-175">Operating regions: EMEA, North America and Brazil</span></span>
> 
> <span data-ttu-id="cb8c4-176">Offerta di soluzioni desktop e RemoteApp basate sulla sessione: sì, entrambe</span><span class="sxs-lookup"><span data-stu-id="cb8c4-176">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span> 
> 
> <span data-ttu-id="cb8c4-177">**Globale**:</span><span class="sxs-lookup"><span data-stu-id="cb8c4-177">**Global**:</span></span>
> 
> <span data-ttu-id="cb8c4-178">Arnaud Marlière, CMO</span><span class="sxs-lookup"><span data-stu-id="cb8c4-178">Arnaud Marlière, CMO</span></span>
> 
> <span data-ttu-id="cb8c4-179">E-mail: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="cb8c4-179">Email: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span></span>
> 
> <span data-ttu-id="cb8c4-180">Telefono: +1 646 583 3025</span><span class="sxs-lookup"><span data-stu-id="cb8c4-180">Phone: +1 646 583 3025</span></span>
> 
> <span data-ttu-id="cb8c4-181">**Sede centrale in Belgio**:</span><span class="sxs-lookup"><span data-stu-id="cb8c4-181">**Belgium HQ**:</span></span>
> 
> <span data-ttu-id="cb8c4-182">Ottergemsesteenweg-Zuid 808 B44</span><span class="sxs-lookup"><span data-stu-id="cb8c4-182">Ottergemsesteenweg-Zuid 808 B44</span></span>
> 
> <span data-ttu-id="cb8c4-183">9000 Gent</span><span class="sxs-lookup"><span data-stu-id="cb8c4-183">9000 Gent</span></span>
> 
> <span data-ttu-id="cb8c4-184">E-mail: [info@awingu.com](mailto:info@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="cb8c4-184">Email: [info@awingu.com](mailto:info@awingu.com)</span></span> 
> 
> <span data-ttu-id="cb8c4-185">Telefono: +32 9 296 40 11</span><span class="sxs-lookup"><span data-stu-id="cb8c4-185">Phone: +32 9 296 40 11</span></span>
> 
> <span data-ttu-id="cb8c4-186">**USA**:</span><span class="sxs-lookup"><span data-stu-id="cb8c4-186">**USA**:</span></span>
> 
> <span data-ttu-id="cb8c4-187">7th floor, 1177 Ave of the Americas,</span><span class="sxs-lookup"><span data-stu-id="cb8c4-187">7th floor, 1177 Ave of the Americas,</span></span>
> 
> <span data-ttu-id="cb8c4-188">New York, NY 10036</span><span class="sxs-lookup"><span data-stu-id="cb8c4-188">New York, NY 10036</span></span>
> 
> <span data-ttu-id="cb8c4-189">E-mail: [info.us@awingu.com](mailto:info.us@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="cb8c4-189">Email: [info.us@awingu.com](mailto:info.us@awingu.com)</span></span>

### <a name="microsoft-hosted-service-provider"></a><span data-ttu-id="cb8c4-190">Provider di servizi ospitati Microsoft</span><span class="sxs-lookup"><span data-stu-id="cb8c4-190">Microsoft Hosted Service Provider</span></span>
<span data-ttu-id="cb8c4-191">I partner di hosting offrono in genere un servizio per desktop e applicazioni Windows ospitato completamente gestito, che può includere la gestione delle risorse di Azure, dei sistemi operativi, delle applicazioni e del supporto tecnico tramite i contratti di licenza stipulati fra il partner e Microsoft e altri fornitori di software, in aggiunta a un contratto di licenza per provider di servizi che disciplina la rivendita di licenze SAL (Subscriber Access License).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-191">Hosting partners typically offer a fully managed hosted Windows desktop and application service, which may include managing the Azure resources, operating systems, applications, and helpdesk using the partner's licensing agreements with Microsoft and other software providers along with being a Service Provider License Agreement to allow reselling of Subscriber Access License (SAL).</span></span> <span data-ttu-id="cb8c4-192">Le informazioni seguenti forniscono tutti i dettagli e i contatti di alcuni provider di servizi di hosting specializzati nell'assistere i clienti durante la migrazione di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-192">The following information provides details and contact information for some of the hosters that specialize in assisting customers with their Azure RemoteApp migration.</span></span> <span data-ttu-id="cb8c4-193">Consultare l'[elenco aggiornato dei provider di servizi ospitati](http://aka.ms/rdsonazurecertified) che hanno portato a termine il percorso di apprendimento e la valutazione su RDS in IaaS.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-193">Check out [the current list of Hosted Service Providers](http://aka.ms/rdsonazurecertified) that have completed the RDS on IaaS learning path and assessment.</span></span>  

### <a name="citrix-service-provider-program"></a><span data-ttu-id="cb8c4-194">Programma Citrix Service Provider</span><span class="sxs-lookup"><span data-stu-id="cb8c4-194">Citrix Service Provider Program</span></span>
<span data-ttu-id="cb8c4-195">Il programma Citrix Service Provider facilita i provider di servizi nell'offrire alle piccole e medie imprese la semplicità del cloud computing virtuale, racchiudendo tutti i servizi desiderati in un agevole modello con pagamento in base al consumo.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-195">The Citrix Service Provider Program makes it easy for service providers to deliver the simplicity of virtual cloud computing to SMBs, offering them the services they want in an easy, pay-as-you-go model.</span></span> <span data-ttu-id="cb8c4-196">I provider di servizi Citrix possono accrescere il business relativo al contratto Microsoft SPLA ed espandere gli investimenti nella piattaforma dei Servizi Desktop remoto con qualsiasi dispositivo, l'accesso da postazioni remote, il supporto per il maggior numero di applicazioni, un'esperienza avanzata e livelli superiori di sicurezza e scalabilità.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-196">Citrix Service Providers grow their Microsoft SPLA businesses and expand their RDS platform investments with any device, anywhere access, the broadest application support, a rich experience, added security and increased scalability.</span></span> <span data-ttu-id="cb8c4-197">A loro volta, gli stessi provider di servizi Citrix possono attrarre più sottoscrittori, aumentare la soddisfazione dei clienti e ridurre i costi operativi.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-197">In turn, Citrix Service Providers attract more subscribers, increase customer satisfaction and reduce their operational costs.</span></span> <span data-ttu-id="cb8c4-198">[Leggere altre informazioni](http://www.citrix.com/products/service-providers.html) o [cercare un partner](https://www.citrix.com/buy/partnerlocator.html).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-198">[Learn more](http://www.citrix.com/products/service-providers.html) or [find a partner](https://www.citrix.com/buy/partnerlocator.html).</span></span>

#### <a name="acuutech"></a><span data-ttu-id="cb8c4-199">Acuutech</span><span class="sxs-lookup"><span data-stu-id="cb8c4-199">Acuutech</span></span>
<span data-ttu-id="cb8c4-200">[Acuutech](http://www.acuutech.com) è specializzata nel fornire soluzioni desktop in hosting e distribuire ai clienti di tutto il mondo esperienze complete per desktop e applicazioni ISV basate su tecnologie Microsoft da Azure e dai propri data center.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-200">[Acuutech](http://www.acuutech.com) specializes in providing hosted desktop solutions, delivering full desktop and ISV applications experiences built on Microsoft technology to a global client base from Azure and their own datacenters.</span></span>

> <span data-ttu-id="cb8c4-201">Sede principale: Londra; Singapore; Houston (Texas)</span><span class="sxs-lookup"><span data-stu-id="cb8c4-201">Primary location: London, UK; Singapore; Houston, TX</span></span>
> 
> <span data-ttu-id="cb8c4-202">Regione operativa: tutto il mondo</span><span class="sxs-lookup"><span data-stu-id="cb8c4-202">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="cb8c4-203">Stato partner: Gold</span><span class="sxs-lookup"><span data-stu-id="cb8c4-203">Partner status: Gold</span></span>
> 
> <span data-ttu-id="cb8c4-204">Provider di servizi cloud Microsoft: sì</span><span class="sxs-lookup"><span data-stu-id="cb8c4-204">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="cb8c4-205">Offerta di soluzioni desktop e RemoteApp basate sulla sessione: sì, entrambe</span><span class="sxs-lookup"><span data-stu-id="cb8c4-205">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="cb8c4-206">Soluzioni per la migrazione di Azure RemoteApp: sì, [altre informazioni](http://www.acuutech.com/ara-migration/)</span><span class="sxs-lookup"><span data-stu-id="cb8c4-206">Azure RemoteApp migration solutions: Yes, [learn more](http://www.acuutech.com/ara-migration/)</span></span>
> 
> <span data-ttu-id="cb8c4-207">**Regno Unito**:</span><span class="sxs-lookup"><span data-stu-id="cb8c4-207">**United Kingdom**:</span></span>
>   
> <span data-ttu-id="cb8c4-208">5/6 York House, Langston Road,</span><span class="sxs-lookup"><span data-stu-id="cb8c4-208">5/6 York House, Langston Road,</span></span>
>   
> <span data-ttu-id="cb8c4-209">Loughton, Essex IG10 3TQ</span><span class="sxs-lookup"><span data-stu-id="cb8c4-209">Loughton, Essex IG10 3TQ</span></span>
>   
> <span data-ttu-id="cb8c4-210">Telefono: +44 (0) 20 8502 2155</span><span class="sxs-lookup"><span data-stu-id="cb8c4-210">Phone: +44 (0) 20 8502 2155</span></span>
> 
> <span data-ttu-id="cb8c4-211">**Singapore**:</span><span class="sxs-lookup"><span data-stu-id="cb8c4-211">**Singapore**:</span></span>
>   
> <span data-ttu-id="cb8c4-212">100 Cecil Street, #09-02,</span><span class="sxs-lookup"><span data-stu-id="cb8c4-212">100 Cecil Street, #09-02,</span></span> 
>   
> <span data-ttu-id="cb8c4-213">The Globe, Singapore 069532</span><span class="sxs-lookup"><span data-stu-id="cb8c4-213">The Globe, Singapore 069532</span></span>
> 
> <span data-ttu-id="cb8c4-214">Telefono: +65 6709 4933</span><span class="sxs-lookup"><span data-stu-id="cb8c4-214">Phone: +65 6709 4933</span></span>
>   
> <span data-ttu-id="cb8c4-215">**America del Nord**:</span><span class="sxs-lookup"><span data-stu-id="cb8c4-215">**North America**:</span></span>
>   
> <span data-ttu-id="cb8c4-216">3601 S. Sandman St.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-216">3601 S. Sandman St.</span></span>
>   
> <span data-ttu-id="cb8c4-217">Suite 200, Houston, TX 77098</span><span class="sxs-lookup"><span data-stu-id="cb8c4-217">Suite 200, Houston, TX 77098</span></span>
>   
> <span data-ttu-id="cb8c4-218">Telefono: +1 713 691 0800</span><span class="sxs-lookup"><span data-stu-id="cb8c4-218">Phone: +1 713 691 0800</span></span>

#### <a name="aspex"></a><span data-ttu-id="cb8c4-219">ASPEX</span><span class="sxs-lookup"><span data-stu-id="cb8c4-219">ASPEX</span></span>
<span data-ttu-id="cb8c4-220">[ASPEX](http://www.aspex.be/en) fornisce servizi agli ISV che desiderano passare al cloud e ottimizzare le configurazioni cloud esistenti.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-220">[ASPEX](http://www.aspex.be/en) specializes in ISVs transitioning to the Cloud and ISV‘ looking to optimize their current cloud setups.</span></span> <span data-ttu-id="cb8c4-221">ASPEX offre un'ampia gamma di servizi gestiti, DevOps e di consulenza.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-221">ASPEX offers a wide range of managed services, devops, and consulting services.</span></span>  

> <span data-ttu-id="cb8c4-222">Sede principale: Anversa</span><span class="sxs-lookup"><span data-stu-id="cb8c4-222">Primary location: Antwerp, Belgium</span></span>
> 
> <span data-ttu-id="cb8c4-223">Regione operativa: Europa occidentale</span><span class="sxs-lookup"><span data-stu-id="cb8c4-223">Operation region: Western Europe</span></span>
> 
> <span data-ttu-id="cb8c4-224">Stato partner: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span><span class="sxs-lookup"><span data-stu-id="cb8c4-224">Partner status: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span></span>
> 
> <span data-ttu-id="cb8c4-225">Provider di servizi cloud Microsoft: sì</span><span class="sxs-lookup"><span data-stu-id="cb8c4-225">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="cb8c4-226">Offerta di soluzioni desktop e RemoteApp basate sulla sessione: sì, entrambe</span><span class="sxs-lookup"><span data-stu-id="cb8c4-226">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="cb8c4-227">Soluzioni per la migrazione di Azure RemoteApp: sì, [altre informazioni](https://www.aspex.be/en/azure-remote-apps)</span><span class="sxs-lookup"><span data-stu-id="cb8c4-227">Azure RemoteApp migration solutions: Yes, [learn more](https://www.aspex.be/en/azure-remote-apps)</span></span>
> 
> <span data-ttu-id="cb8c4-228">Telefono: +3232202198</span><span class="sxs-lookup"><span data-stu-id="cb8c4-228">Phone: +3232202198</span></span>
> 
> <span data-ttu-id="cb8c4-229">E-mail: [info@aspex.be](mailto:info@aspex.be)</span><span class="sxs-lookup"><span data-stu-id="cb8c4-229">Mail: [info@aspex.be](mailto:info@aspex.be)</span></span>
> 
> <span data-ttu-id="cb8c4-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span><span class="sxs-lookup"><span data-stu-id="cb8c4-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span></span>

#### <a name="caasecom"></a><span data-ttu-id="cb8c4-231">Caase.com</span><span class="sxs-lookup"><span data-stu-id="cb8c4-231">Caase.com</span></span>
<span data-ttu-id="cb8c4-232">[Caase.com](http://www.caase.com/) facilita il passaggio a un modo efficiente di lavorare nel cloud di Microsoft per le aziende, i governi locali, i corpi governativi e le istituzioni di assistenza sanitaria.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-232">[Caase.com](http://www.caase.com/) helps businesses, local governments, non-governmental bodies and healthcare institutions with their journey towards a smarter way of work in the Microsoft Cloud.</span></span> <span data-ttu-id="cb8c4-233">Produttività e sicurezza in qualsiasi luogo, con qualsiasi dispositivo e a basso costo IT.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-233">Being productive and secure at any place, with any device and at low IT cost.</span></span> <span data-ttu-id="cb8c4-234">Caase.com è un vero specialista di Microsoft Office365, Azure, Enterprise Mobility e Sicurezza e Windows.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-234">Caase.com is a true specialist for Microsoft Office365, Azure, Enterprise Mobility and Security and Windows.</span></span> <span data-ttu-id="cb8c4-235">Grazie alla consulenza, ai servizi di migrazione, ai programmi di adozione, alla formazione, alla gestione e al supporto di Microsoft, Caase.com crea una piattaforma sicura e ottimizzata per la collaborazione per i dipendenti, i partner e i fornitori dei clienti.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-235">With our consultancy, migration services, adoption programs, training, management and support Caase.com creates an optimized and secure platform for collaboration for both customers’ employees, partners and suppliers.</span></span>
<span data-ttu-id="cb8c4-236">Caase.com è il genio dell'area di lavoro di Azure, ovvero l'area di lavoro per dispositivi mobili, e dell'area di lavoro digitale, ovvero l'Intranet dei social.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-236">Caase.com is the mastermind of the Azure Remote Workspace (mobile workplace) and the Digital Workplace (Social Intranet).</span></span> <span data-ttu-id="cb8c4-237">Entrambe le soluzioni, eseguite con l'adozione, sono il fondamento che garantisce agli utenti un esperienza piacevole, efficace e ottimale nella relativa route per il cloud di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-237">Both solutions – accomplished with adoption – are the foundation which ensures that the users of these solutions have the most pleasant, successful and effective experience in their route to the Microsoft Cloud.</span></span>
<span data-ttu-id="cb8c4-238">Per la traduzione in olandese e un filmato di supporto visitare questa pagina: http://caase.com/over-ons/</span><span class="sxs-lookup"><span data-stu-id="cb8c4-238">Dutch translation ánd a supporting movie over here: http://caase.com/over-ons/</span></span>

> <span data-ttu-id="cb8c4-239">Area di operatività: con sede in Olanda e portata globale</span><span class="sxs-lookup"><span data-stu-id="cb8c4-239">Operation region: Dutch based, global reach</span></span>
> 
> <span data-ttu-id="cb8c4-240">Stato partner: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span><span class="sxs-lookup"><span data-stu-id="cb8c4-240">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span></span>
> 
> <span data-ttu-id="cb8c4-241">Provider di servizi cloud Microsoft: sì</span><span class="sxs-lookup"><span data-stu-id="cb8c4-241">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="cb8c4-242">Offerta di soluzioni desktop e RemoteApp basate sulla sessione: sì, entrambe</span><span class="sxs-lookup"><span data-stu-id="cb8c4-242">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="cb8c4-243">Soluzioni per la migrazione di Azure RemoteApp: sì, [altre informazioni](http://caase.com/diensten/microsoft-azure/).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-243">Azure RemoteApp migration solutions: Yes, [learn more](http://caase.com/diensten/microsoft-azure/).</span></span>
> 
> 
> <span data-ttu-id="cb8c4-244">Paesi Bassi:</span><span class="sxs-lookup"><span data-stu-id="cb8c4-244">Netherlands:</span></span>
> 
> <span data-ttu-id="cb8c4-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span><span class="sxs-lookup"><span data-stu-id="cb8c4-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span></span>
> 
> <span data-ttu-id="cb8c4-246">7521 BE, Enschede</span><span class="sxs-lookup"><span data-stu-id="cb8c4-246">7521 BE, Enschede</span></span>
> 
> <span data-ttu-id="cb8c4-247">Telefono: +31 (0) 88 4320 000</span><span class="sxs-lookup"><span data-stu-id="cb8c4-247">Phone: +31 (0) 88 4320 000</span></span>


#### <a name="nerdio"></a><span data-ttu-id="cb8c4-248">Nerdio</span><span class="sxs-lookup"><span data-stu-id="cb8c4-248">Nerdio</span></span>
<span data-ttu-id="cb8c4-249">[Nerdio for Azure](http://getnerdio.com/nfa/) è una piattaforma di automazione IT che offre un provisioning estremamente semplice, oltre alla gestione e all'ottimizzazione di interi ambienti IT nel cloud di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-249">[Nerdio for Azure](http://getnerdio.com/nfa/) is an IT automation platform that delivers ridiculously simple provisioning, management and optimization of complete IT environments in the Microsoft cloud.</span></span> <span data-ttu-id="cb8c4-250">Consente di configurare desktop virtuali, applicazioni remote e server in un paio di ore;</span><span class="sxs-lookup"><span data-stu-id="cb8c4-250">Stand up virtual desktops, remote apps and servers in a couple of hours.</span></span> <span data-ttu-id="cb8c4-251">amministrare l'ambiente in tre clic o meno con il portale di amministrazione di Nerdio;</span><span class="sxs-lookup"><span data-stu-id="cb8c4-251">Administer the environment in three clicks or less with Nerdio Admin Portal.</span></span> <span data-ttu-id="cb8c4-252">usare il ridimensionamento automatico intelligente e risparmiare dal 40 al 60% di risorse IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-252">Use intelligent auto-scaling and save 40 to 60% in Azure IaaS resources.</span></span>

> <span data-ttu-id="cb8c4-253">Sede principale: area di Chicago, IL Sede operativa: a livello globale Stato del partner: [Oro](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Provider del servizio cloud di Microsoft: sì</span><span class="sxs-lookup"><span data-stu-id="cb8c4-253">Primary location: Chicago, IL Operation region: Worldwide Partner status: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="cb8c4-254">Offerta di soluzioni desktop e RemoteApp basate sulla sessione: sì, entrambe</span><span class="sxs-lookup"><span data-stu-id="cb8c4-254">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="cb8c4-255">Soluzioni per la migrazione di Azure RemoteApp: sì</span><span class="sxs-lookup"><span data-stu-id="cb8c4-255">Azure RemoteApp migration solutions: Yes</span></span>
> 
> 
> <span data-ttu-id="cb8c4-256">8001 Lincoln Ave</span><span class="sxs-lookup"><span data-stu-id="cb8c4-256">8001 Lincoln Ave</span></span>
> 
> <span data-ttu-id="cb8c4-257">Suite 212</span><span class="sxs-lookup"><span data-stu-id="cb8c4-257">Suite 212</span></span>
> 
> <span data-ttu-id="cb8c4-258">Skokie, IL 60077</span><span class="sxs-lookup"><span data-stu-id="cb8c4-258">Skokie, IL 60077</span></span>
> 
> <span data-ttu-id="cb8c4-259">USA</span><span class="sxs-lookup"><span data-stu-id="cb8c4-259">USA</span></span>
> 
> <span data-ttu-id="cb8c4-260">(844) 4NERDIO ext.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-260">(844) 4NERDIO ext.</span></span> <span data-ttu-id="cb8c4-261">6</span><span class="sxs-lookup"><span data-stu-id="cb8c4-261">6</span></span>
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a><span data-ttu-id="cb8c4-262">**SaaSplaza**</span><span class="sxs-lookup"><span data-stu-id="cb8c4-262">**SaaSplaza**</span></span>
<span data-ttu-id="cb8c4-263">[SaaSplaza](http://www.saasplaza.com/) offre un portfolio Microsoft Dynamics completo (NAV, AX, GP, SL, CRM) con cloud privato e pubblico (Azure).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-263">[SaaSplaza](http://www.saasplaza.com/) offers complete Microsoft Dynamics portfolio (NAV, AX, GP, SL, CRM) private and public cloud (Azure).</span></span>

> <span data-ttu-id="cb8c4-264">Località primaria: Paesi Bassi</span><span class="sxs-lookup"><span data-stu-id="cb8c4-264">Primary location: Netherlands</span></span>
> 
> <span data-ttu-id="cb8c4-265">Area operativa: tutto il mondo</span><span class="sxs-lookup"><span data-stu-id="cb8c4-265">Operation Region: Worldwide</span></span>
> 
> <span data-ttu-id="cb8c4-266">Stato partner: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span><span class="sxs-lookup"><span data-stu-id="cb8c4-266">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span></span>
> 
> <span data-ttu-id="cb8c4-267">Provider di servizi cloud Microsoft: sì</span><span class="sxs-lookup"><span data-stu-id="cb8c4-267">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="cb8c4-268">Offerta di soluzioni desktop e RemoteApp basate sulla sessione: sì, entrambe</span><span class="sxs-lookup"><span data-stu-id="cb8c4-268">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="cb8c4-269">**EMEA**:</span><span class="sxs-lookup"><span data-stu-id="cb8c4-269">**EMEA**:</span></span>
> 
> <span data-ttu-id="cb8c4-270">Prins Mauritslaan 29-35</span><span class="sxs-lookup"><span data-stu-id="cb8c4-270">Prins Mauritslaan 29-35</span></span>
> 
> <span data-ttu-id="cb8c4-271">71 LP Badhoevedorp</span><span class="sxs-lookup"><span data-stu-id="cb8c4-271">71 LP Badhoevedorp</span></span>
> 
> <span data-ttu-id="cb8c4-272">Paesi Bassi</span><span class="sxs-lookup"><span data-stu-id="cb8c4-272">The Netherlands</span></span>
> 
> <span data-ttu-id="cb8c4-273">Telefono: +31 20 547 8060</span><span class="sxs-lookup"><span data-stu-id="cb8c4-273">Phone: +31 20 547 8060</span></span> 
> 
>  <span data-ttu-id="cb8c4-274">**Americhe**:</span><span class="sxs-lookup"><span data-stu-id="cb8c4-274">**Americas**:</span></span>
> 
> <span data-ttu-id="cb8c4-275">171 Saxony Road, Suite 105</span><span class="sxs-lookup"><span data-stu-id="cb8c4-275">171 Saxony Road, Suite 105</span></span>
> 
> <span data-ttu-id="cb8c4-276">Encinitas, CA 92024</span><span class="sxs-lookup"><span data-stu-id="cb8c4-276">Encinitas, CA 92024</span></span>
> 
> <span data-ttu-id="cb8c4-277">San Diego</span><span class="sxs-lookup"><span data-stu-id="cb8c4-277">San Diego</span></span>
> 
> <span data-ttu-id="cb8c4-278">Stati Uniti</span><span class="sxs-lookup"><span data-stu-id="cb8c4-278">United States</span></span>
> 
> <span data-ttu-id="cb8c4-279">Telefono: +1 858 385 8900</span><span class="sxs-lookup"><span data-stu-id="cb8c4-279">Phone: +1 858 385 8900</span></span> 
> 
> <span data-ttu-id="cb8c4-280">**APAC**:</span><span class="sxs-lookup"><span data-stu-id="cb8c4-280">**APAC**:</span></span>
> 
> <span data-ttu-id="cb8c4-281">105 Cecil Street</span><span class="sxs-lookup"><span data-stu-id="cb8c4-281">105 Cecil Street</span></span>
>    
> <span data-ttu-id="cb8c4-282">\#11-08, The Octagon</span><span class="sxs-lookup"><span data-stu-id="cb8c4-282">\#11-08, The Octagon</span></span>
> 
> <span data-ttu-id="cb8c4-283">Singapore 069534</span><span class="sxs-lookup"><span data-stu-id="cb8c4-283">Singapore 069534</span></span>
> 
> <span data-ttu-id="cb8c4-284">Singapore</span><span class="sxs-lookup"><span data-stu-id="cb8c4-284">Singapore</span></span>
>   
> <span data-ttu-id="cb8c4-285">Telefono - Singapore: +65 6222 6591</span><span class="sxs-lookup"><span data-stu-id="cb8c4-285">Phone - Singapore: +65 6222 6591</span></span>
> 
> <span data-ttu-id="cb8c4-286">Telefono - Australia: +61 2 8310 5568</span><span class="sxs-lookup"><span data-stu-id="cb8c4-286">Phone - Australia: +61 2 8310 5568</span></span> 
>    
> <span data-ttu-id="cb8c4-287">Telefono - Nuova Zelanda: +64 4 488 0321</span><span class="sxs-lookup"><span data-stu-id="cb8c4-287">Phone - New Zealand: +64 4 488 0321</span></span>
> 
## <a name="need-more-help"></a><span data-ttu-id="cb8c4-288">Ulteriore assistenza</span><span class="sxs-lookup"><span data-stu-id="cb8c4-288">Need more help?</span></span>
<span data-ttu-id="cb8c4-289">Per farsi aiutare nella scelta o se si hanno altre domande,</span><span class="sxs-lookup"><span data-stu-id="cb8c4-289">Still need help choosing or have further questions?</span></span> <span data-ttu-id="cb8c4-290">usare uno dei metodi seguenti.</span><span class="sxs-lookup"><span data-stu-id="cb8c4-290">Use one of the following methods to get help.</span></span> 

1. <span data-ttu-id="cb8c4-291">Scrivere un'e-mail all'indirizzo [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-291">Email us at [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span></span>
2. <span data-ttu-id="cb8c4-292">Contattare il [supporto tecnico di Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-292">Contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="cb8c4-293">Aprire un [caso di supporto su Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-293">Start by opening an [Azure support case](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
3. <span data-ttu-id="cb8c4-294">Contattare il</span><span class="sxs-lookup"><span data-stu-id="cb8c4-294">Call us.</span></span> <span data-ttu-id="cb8c4-295">[team di vendita locale](https://azure.microsoft.com/overview/sales-number/).</span><span class="sxs-lookup"><span data-stu-id="cb8c4-295">[Find a local sales number](https://azure.microsoft.com/overview/sales-number/).</span></span>

