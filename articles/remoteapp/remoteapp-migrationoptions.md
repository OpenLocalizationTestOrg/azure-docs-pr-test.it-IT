---
title: aaaOptions per eseguire la migrazione da Azure RemoteApp | Documenti Microsoft
description: Informazioni sulle opzioni di hello per eseguire la migrazione da Azure RemoteApp.
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
ms.openlocfilehash: 75324597881520d0c75939983b728ae9bbd7f436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a><span data-ttu-id="a0cd3-103">Opzioni per la migrazione da Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="a0cd3-103">Options for migrating out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a0cd3-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="a0cd3-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>


<span data-ttu-id="a0cd3-106">Se è stata interrotta con RemoteApp di Azure a causa di hello [annuncio del ritiro](https://go.microsoft.com/fwlink/?linkid=821148) o perché è stata completata la valutazione, è necessario toomigrate di fuori di servizio app di Azure RemoteApp tooanother.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-106">If you have stopped using Azure RemoteApp because of hello [retirement announcement](https://go.microsoft.com/fwlink/?linkid=821148) or because you've finished your evaluation, you need toomigrate off of Azure RemoteApp tooanother app service.</span></span> <span data-ttu-id="a0cd3-107">La migrazione può essere effettuata in due modi: con una distribuzione autogestita (spesso denominata Infrastructure as a Service [IaaS]) o tramite un'offerta completamente gestita (spesso denominata Platform as a Service oppure Software as a Service [PaaS/SaaS]).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-107">There are two different approaches for migrating: a self-managed (often called Infrastructure as a Service [IaaS]) deployment or a fully managed (often called Platform as a Service or Software as a Service [PaaS/SaaS]) offering.</span></span> 

<span data-ttu-id="a0cd3-108">L'approccio IaaS self-service consiste in una distribuzione "fai da te" gestita dall'utente e di sua proprietà, direttamente distribuita su macchine virtuali (VM) o sistemi fisici.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-108">Self-service IaaS is a do-it-yourself deployment that is managed, operated, and owned by you, directly deployed on virtual machines (VMs) or physical systems.</span></span> <span data-ttu-id="a0cd3-109">In altri hello terminare, l'offerta più simili a Azure RemoteApp - un partner fornisce un livello di servizio all'inizio di una soluzione di comunicazione remota che gestisce operativo un PaaS/SaaS completamente gestito e la manutenzione, quando il computer, come cliente hello, eseguire alcune app e l'immagine di gestione.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-109">At hello other end, a fully managed PaaS/SaaS offering is more like Azure RemoteApp - a partner provides a service layer on top of a remoting solution that handles operational and servicing, while you, as hello customer, do some image and app management.</span></span>

<span data-ttu-id="a0cd3-110">[Visualizzare hello Azure RemoteApp webinar sulle opzioni di migrazione](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), o di lettura in per altre informazioni (con esempi di hello diversa opzioni di hosting).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-110">[View hello Azure RemoteApp webinars on migration options](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), or read on for more information (including examples of hello different hosting options).</span></span>

## <a name="self-managed-iaas-solutions"></a><span data-ttu-id="a0cd3-111">Soluzioni autogestite (IaaS)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-111">Self-managed (IaaS) solutions</span></span>
### <a name="rds-on-iaas"></a><span data-ttu-id="a0cd3-112">**RDS su IaaS**</span><span class="sxs-lookup"><span data-stu-id="a0cd3-112">**RDS on IaaS**</span></span>
<span data-ttu-id="a0cd3-113">È possibile implementare una distribuzione di Servizi Desktop remoto (in Windows Server) basata su una sessione nativa tramite RemoteApp o desktop locali oppure in un ambiente ospitato (come le VM di Azure).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-113">You can deploy a native session-based Remote Desktop Services (in Windows Server) deployment using either RemoteApp or desktops on-premises or in a hosted environment (like on Azure VMs).</span></span> <span data-ttu-id="a0cd3-114">Le distribuzioni di Servizi Desktop remoto su IaaS sono particolarmente indicate per i clienti che le conoscono già e che possiedono le necessarie competenze tecniche in merito.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-114">RDS on IaaS deployments are best for customers already familiar with and that have existing technical expertise with RDS deployments.</span></span> 

> [!NOTE]
> <span data-ttu-id="a0cd3-115">È necessario un contratto multilicenza con Software Assurance (SA) per toouse licenze accesso client di servizi desktop remoto questa opzione di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-115">You need Volume Licensing with Software Assurance (SA) for RDS client access licenses toouse this deployment option.</span></span>

<span data-ttu-id="a0cd3-116">Distribuire Servizi Desktop remoto nelle VM di Azure è più semplice che mai se si usano i modelli di distribuzione e applicazione delle patch (leggere una [panoramica](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) e quindi [accedere ai modelli](https://aka.ms/rdautomation)).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-116">Deploying RDS on Azure VMs is easier than ever when you use deployment and patching templates (read an [overview](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) and then [go get them](https://aka.ms/rdautomation)).</span></span> <span data-ttu-id="a0cd3-117">È possibile ottenere hello stesse funzionalità di scalabilità elastica con risorse del modello di distribuzione classico di Azure (non le risorse di un modello di risorse di Azure) all'interno di Azure RemoteApp con hello [script di scalabilità automatica](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), anche se esistono più elementi le personalizzazioni e le configurazioni.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-117">You can get hello same elastic scaling capabilities with Azure classic deployment model resources (not Azure Resource Model resources) within Azure RemoteApp by using hello [auto scaling script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), although there are more customizations and configurations.</span></span> <span data-ttu-id="a0cd3-118">Quando si distribuisce Servizi Desktop remoto in macchine virtuali di Azure, il supporto viene fornito tramite [Azure supporta](https://azure.microsoft.com/support/plans/), hello stesso personale di supporto tecnico è supportata con Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-118">When you deploy RDS on Azure VMs, support is provided through [Azure Support](https://azure.microsoft.com/support/plans/), hello same support professionals that supported you with Azure RemoteApp.</span></span> <span data-ttu-id="a0cd3-119">È possibile ottenere stime dei costi in base all'utilizzo esistente contattando [supporto Azure](https://azure.microsoft.com/support/plans/), calcoli può essere eseguita manualmente o utilizzando un appena toobe rilasciato calcolatore dei costi.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-119">You can get cost estimates based on your existing usage by contacting [Azure Support](https://azure.microsoft.com/support/plans/), or you can perform calculations yourself using a soon toobe released Cost Calculator.</span></span>  <span data-ttu-id="a0cd3-120">Inoltre, con le macchine virtuali serie N (attualmente in anteprima privata) è possibile aggiungere vGPU - lieti di ricevere informazioni sull'aggiunta di vGPU e su come troppo[sfruttare i miglioramenti di servizi desktop remoto in Windows Server 2016](https://myignite.microsoft.com/videos/2794) nella sessione il nostro Ignite.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-120">Also, with N-series VMs (currently in private preview) you can add vGPU - hear more about adding vGPU and about how too[harness RDS improvements in Windows Server 2016](https://myignite.microsoft.com/videos/2794) in our Ignite session.</span></span>   

<span data-ttu-id="a0cd3-121">Sono disponibili le guide alla distribuzione dettagliata per [Windows Server 2012 R2](http://aka.ms/rdsonazure) e [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist con la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-121">We have step by step deployment guides for [Windows Server 2012 R2](http://aka.ms/rdsonazure) and [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist with your deployment.</span></span> <span data-ttu-id="a0cd3-122">Estrarre hello [blog di Desktop remoto](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) per notizie più recenti di hello.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-122">Check out hello [Remote Desktop blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) for hello latest news.</span></span>

### <a name="citrix-on-iaas"></a><span data-ttu-id="a0cd3-123">**Citrix in IaaS**</span><span class="sxs-lookup"><span data-stu-id="a0cd3-123">**Citrix on IaaS**</span></span>
<span data-ttu-id="a0cd3-124">Una distribuzione Citrix nativa di XenApp o XenDesktop in base alla sessione può essere effettuata in locale o in un ambiente ospitato (ad esempio, nelle VM di Azure).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-124">A native Citrix deployment of session-based XenApp or XenDesktop can be deployed on-premises or within a hosted environment (such as on Azure VMs).</span></span> 

<span data-ttu-id="a0cd3-125">Estrarre hello Guida dettagliata alla distribuzione, [Citrix XA 7.6 in Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-125">Check out hello step-by-step deployment guide, [Citrix XA 7.6 on Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), for more information.</span></span> <span data-ttu-id="a0cd3-126">Sono inoltre disponibili altre informazioni su [Citrix in Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), con in più il calcolatore dei prezzi.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-126">Read more about [Citrix on Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), including a price calculator.</span></span> <span data-ttu-id="a0cd3-127">È anche possibile trovare un [contatto Citrix](http://citrix.com/English/contact/index.asp) toodiscuss le opzioni.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-127">You can also find a [Citrix contact](http://citrix.com/English/contact/index.asp) toodiscuss your options with.</span></span>

## <a name="fully-managed-paassaas-offerings"></a><span data-ttu-id="a0cd3-128">Offerte completamente gestite (PaaS/SaaS)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-128">Fully managed (PaaS/SaaS) offerings</span></span>

### <a name="citrix-xenapp-essentials-released-april-2017"></a><span data-ttu-id="a0cd3-129">Citrix XenApp Essentials (rilasciato nell'aprile 2017)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-129">Citrix XenApp Essentials (released April 2017)</span></span>
<span data-ttu-id="a0cd3-130">Disponibili su hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix informazioni Essentials è hello nuova applicazione virtualizzazione servizio, la combinazione di risparmio energia hello e flessibilità di hello piattaforma Cloud Citrix con hello semplice prescrittivo, e visione all'uso di Microsoft Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-130">Available now on hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials is hello new application virtualization service, combining hello power and flexibility of hello Citrix Cloud platform with hello simple, prescriptive, and easy-to-consume vision of Microsoft Azure RemoteApp.</span></span> 

<span data-ttu-id="a0cd3-131">I clienti di Azure RemoteApp esistenti possono [registrarsi per una prova gratuita](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-131">Existing Azure RemoteApp customers can [register for a free trial](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span></span>  <span data-ttu-id="a0cd3-132">Nota: solo il servizio utente Citrix è gratuito, verranno addebitati i costi di calcolo e archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a0cd3-132">Note: Only Citrix user service charge is free, Azure compute and storage costs apply</span></span>

<span data-ttu-id="a0cd3-133">Altre informazioni:</span><span class="sxs-lookup"><span data-stu-id="a0cd3-133">Learn More:</span></span>
- [<span data-ttu-id="a0cd3-134">Eseguire la migrazione da Azure RemoteApp tooCitrix informazioni Essentials</span><span class="sxs-lookup"><span data-stu-id="a0cd3-134">Migrate from Azure RemoteApp tooCitrix XenApp Essentials</span></span>](remoteapp-migrate-citrix.md)
- [<span data-ttu-id="a0cd3-135">Citrix e Microsoft</span><span class="sxs-lookup"><span data-stu-id="a0cd3-135">Citrix and Microsoft</span></span>](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- <span data-ttu-id="a0cd3-136">[Presentazione di Citrix XenApp Essentials](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-136">[Citrix XenApp Essentials presentation](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span></span>  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a><span data-ttu-id="a0cd3-137">Servizio Citrix Cloud XenApp e servizio XenDesktop</span><span class="sxs-lookup"><span data-stu-id="a0cd3-137">Citrix Cloud XenApp Service and XenDesktop Service</span></span> 

<span data-ttu-id="a0cd3-138">[Servizio informazioni Cloud di Citrix e XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) sia hello la soluzione migliore per il recapito di hello di sia le applicazioni e desktop, più avanzate di gestione e funzionalità di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-138">[Citrix Cloud XenApp Service and XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) is hello best solution for hello delivery of both apps and desktops, plus advanced management and monitoring capabilities.</span></span> 

#### <a name="conexlink-platform-name-mycloudit"></a><span data-ttu-id="a0cd3-139">Conexlink (nome della piattaforma: MyCloudIT)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-139">Conexlink (Platform name: MyCloudIT)</span></span>
<span data-ttu-id="a0cd3-140">[MyCloudIT](https://mycloudit.com) è una piattaforma di automazione per toosimplify le aziende IT, ottimizzare e scalare migrazione hello e recapito di desktop remoto, le applicazioni remote e infrastruttura hello Cloud di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-140">[MyCloudIT](https://mycloudit.com) is an automation platform for IT companies toosimplify, optimize, and scale hello migration and delivery of remote desktops, remote applications, and infrastructure in hello Microsoft Azure Cloud.</span></span> 

<span data-ttu-id="a0cd3-141">piattaforma MyCloudIT Hello riduce il tempo di distribuzione del 95%, Azure costo del 30% e sposta l'intera infrastruttura IT di propri clienti nel cloud hello nel giro di qualche pressioni di tasti.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-141">hello MyCloudIT platform reduces deployment time by 95%, Azure cost by 30%, and moves their client's entire IT infrastructure into hello cloud in a matter of a few key strokes.</span></span> <span data-ttu-id="a0cd3-142">Partner possono ora gestire i clienti da un dashboard globale, gli utenti finali di servizio in tutto il mondo hello come mai prima e aumento delle dimensioni dei ricavi senza aggiungere un ulteriore sovraccarico o formazione di Azure completa.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-142">Partners can now manage customers from one global dashboard, service end users around hello world like never before, and grow revenues without adding additional overhead or extensive Azure training.</span></span>  

> <span data-ttu-id="a0cd3-143">Sede principale: Dallas (Texas)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-143">Primary location: Dallas, TX, USA</span></span>
> 
> <span data-ttu-id="a0cd3-144">Regione operativa: tutto il mondo</span><span class="sxs-lookup"><span data-stu-id="a0cd3-144">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="a0cd3-145">Stato partner: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-145">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span></span>
> 
> <span data-ttu-id="a0cd3-146">Provider di servizi cloud Microsoft: sì</span><span class="sxs-lookup"><span data-stu-id="a0cd3-146">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="a0cd3-147">Offerta di soluzioni desktop e RemoteApp basate sulla sessione: sì, entrambe</span><span class="sxs-lookup"><span data-stu-id="a0cd3-147">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="a0cd3-148">Soluzioni per la migrazione di Azure RemoteApp: sì, [altre informazioni](https://mycloudit.com/remote-app-microsoft/)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-148">Azure RemoteApp migration solutions: Yes, [learn more](https://mycloudit.com/remote-app-microsoft/)</span></span>
> 
> <span data-ttu-id="a0cd3-149">Brian Garoutte, Vicepresidente dell'area Business Development</span><span class="sxs-lookup"><span data-stu-id="a0cd3-149">Brian Garoutte, VP of Business Development</span></span>
> 
> <span data-ttu-id="a0cd3-150">Telefono: 972-218-0741</span><span class="sxs-lookup"><span data-stu-id="a0cd3-150">Phone: 972-218-0741</span></span>
>   
> <span data-ttu-id="a0cd3-151">E-mail: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-151">Email: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span></span>

### <a name="frame"></a><span data-ttu-id="a0cd3-152">Frame</span><span class="sxs-lookup"><span data-stu-id="a0cd3-152">Frame</span></span>

<span data-ttu-id="a0cd3-153">Le organizzazioni IT dell'organizzazione e per enti pubblici, provider di servizi gestiti e principali fornitori di software scegliere toocreate Frame e gestire le aree di lavoro nel cloud hello protette, definita dal software.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-153">IT organizations in enterprise and government, managed service providers, and leading software vendors choose Frame toocreate and manage their secure, software-defined workspaces in hello cloud.</span></span> <span data-ttu-id="a0cd3-154">Da organizzazioni di piccole dimensioni toolarge, Frame rende estremamente semplice toolet utenti accedere alle applicazioni di Windows in qualsiasi browser da qualsiasi dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-154">From small toolarge organizations, Frame makes it incredibly easy toolet users access Windows applications on any browser from any device.</span></span> <span data-ttu-id="a0cd3-155">Hello Frame piattaforma include tutto ciò che un amministratore deve toodeploy di applicazioni cloud hello inclusi hello dell'infrastruttura di Azure e licenze di servizi desktop remoto (riportare il proprio account Azure e licenze è facoltativo).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-155">hello Frame platform includes everything an admin needs toodeploy applications from hello cloud including hello Azure infrastructure and RDS licenses (bringing your own Azure account and licenses is optional).</span></span> 

<span data-ttu-id="a0cd3-156">Altre informazioni su [Frame in Azure](https://www.fra.me/ara).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-156">Learn more about [Frame on Azure](https://www.fra.me/ara).</span></span> 

> <span data-ttu-id="a0cd3-157">Località primaria: San Mateo, CA, USA</span><span class="sxs-lookup"><span data-stu-id="a0cd3-157">Primary location: San Mateo, CA, USA</span></span>
>
> <span data-ttu-id="a0cd3-158">Regione operativa: tutto il mondo</span><span class="sxs-lookup"><span data-stu-id="a0cd3-158">Operation region: Worldwide</span></span>
>
> <span data-ttu-id="a0cd3-159">Partner Microsoft: Sì</span><span class="sxs-lookup"><span data-stu-id="a0cd3-159">Microsoft Partner: Yes</span></span>
> 
> <span data-ttu-id="a0cd3-160">Telefono: 1-480-269-4668</span><span class="sxs-lookup"><span data-stu-id="a0cd3-160">Phone: 1-480-269-4668</span></span>

### <a name="awingu"></a><span data-ttu-id="a0cd3-161">Awingu</span><span class="sxs-lookup"><span data-stu-id="a0cd3-161">Awingu</span></span>
<span data-ttu-id="a0cd3-162">Awingu offre una semplice soluzione online per l'area di lavoro che esegue applicazioni legacy, SaaS e documenti da un browser html5.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-162">Awingu provides a simple online workspace solution running legacy apps, SaaS and documents from an html5 browser.</span></span> <span data-ttu-id="a0cd3-163">Di conseguenza rende disponibili tutte le applicazioni in modo sicuro in qualsiasi tipo di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-163">As such, making any applications securely available on any type of device.</span></span> <span data-ttu-id="a0cd3-164">Per i servizi SaaS è disponibile un'ampia gamma di opzioni Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-164">For SaaS services, a wide range op Single-Sign-On options is available.</span></span> <span data-ttu-id="a0cd3-165">Inoltre è possibile integrare profondamente diversi file system (cloud) nell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-165">Also diverse (cloud) files systems can be deeply integrated into your workspace.</span></span> <span data-ttu-id="a0cd3-166">Mobilità toofull successiva, RTF online dell'area di lavoro dell'Awingu fornirà una sicurezza ottimale con controlli granulari (ad esempio il download/caricamento), informazioni complete sull'utilizzo di controllo, multi-Factor Authentication (ad esempio Azure MFA), la registrazione di sessioni e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-166">Next toofull mobility, Awingu's rich online workspace will give optimal security with granular controls (e.g. downloading/uploading), full usage auditing, Multi-Factor Authentication (e.g. Azure MFA), session recording and more.</span></span> <span data-ttu-id="a0cd3-167">Awingu consente in modo predefinito la condivisione dei documenti e delle sessioni di applicazione per una collaborazione ottimizzata e sicura.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-167">Out-of-the-box, Awingu enables document and application session sharing for optimized and secure collaboration.</span></span>
<span data-ttu-id="a0cd3-168">La soluzione Awingu è multi-tenant, multi-AD e open API.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-168">Awingu's solution is multi-tenant, multi-AD and open API.</span></span> <span data-ttu-id="a0cd3-169">È utilizzata da piccole e grandi aziende, provider di servizi cloud e [ISV](http://www.isv2saas.com).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-169">It is used by small and large businesses, Cloud Service Providers and [ISVs](http://www.isv2saas.com).</span></span> <span data-ttu-id="a0cd3-170">Questi clienti apprezzano particolarmente hello semplice di utilizzo, per semplificare l'installazione e a basso costo totale di proprietà.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-170">These customers especially appreciate hello easy-of-use, ease-to-install and low TCO.</span></span>

<span data-ttu-id="a0cd3-171">È Awingu All-in-One [disponibile in Azure Marketplace hello](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) con 2 utenti simultanei incorporati.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-171">Awingu All-in-One is [available in hello Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) with 2 built-in concurrent users.</span></span> <span data-ttu-id="a0cd3-172">Sono disponibili licenze aggiuntive tramite un'[ampia gamma di distributori e rivenditori](http://www.awingu.com/reseller).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-172">Additional licenses are available through a [wide range of distributors and resellers](http://www.awingu.com/reseller).</span></span>

<span data-ttu-id="a0cd3-173">Altre informazioni, vedere [Awingu su come alternativa tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-173">Learn more about [Awingu on as alternative tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span></span>


> <span data-ttu-id="a0cd3-174">Sede principale: Belgio</span><span class="sxs-lookup"><span data-stu-id="a0cd3-174">Primary location: Belgium</span></span>
> 
> <span data-ttu-id="a0cd3-175">Aree operative: EMEA, America del Nord e Brasile</span><span class="sxs-lookup"><span data-stu-id="a0cd3-175">Operating regions: EMEA, North America and Brazil</span></span>
> 
> <span data-ttu-id="a0cd3-176">Offerta di soluzioni desktop e RemoteApp basate sulla sessione: sì, entrambe</span><span class="sxs-lookup"><span data-stu-id="a0cd3-176">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span> 
> 
> <span data-ttu-id="a0cd3-177">**Globale**:</span><span class="sxs-lookup"><span data-stu-id="a0cd3-177">**Global**:</span></span>
> 
> <span data-ttu-id="a0cd3-178">Arnaud Marlière, CMO</span><span class="sxs-lookup"><span data-stu-id="a0cd3-178">Arnaud Marlière, CMO</span></span>
> 
> <span data-ttu-id="a0cd3-179">E-mail: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-179">Email: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span></span>
> 
> <span data-ttu-id="a0cd3-180">Telefono: +1 646 583 3025</span><span class="sxs-lookup"><span data-stu-id="a0cd3-180">Phone: +1 646 583 3025</span></span>
> 
> <span data-ttu-id="a0cd3-181">**Sede centrale in Belgio**:</span><span class="sxs-lookup"><span data-stu-id="a0cd3-181">**Belgium HQ**:</span></span>
> 
> <span data-ttu-id="a0cd3-182">Ottergemsesteenweg-Zuid 808 B44</span><span class="sxs-lookup"><span data-stu-id="a0cd3-182">Ottergemsesteenweg-Zuid 808 B44</span></span>
> 
> <span data-ttu-id="a0cd3-183">9000 Gent</span><span class="sxs-lookup"><span data-stu-id="a0cd3-183">9000 Gent</span></span>
> 
> <span data-ttu-id="a0cd3-184">E-mail: [info@awingu.com](mailto:info@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-184">Email: [info@awingu.com](mailto:info@awingu.com)</span></span> 
> 
> <span data-ttu-id="a0cd3-185">Telefono: +32 9 296 40 11</span><span class="sxs-lookup"><span data-stu-id="a0cd3-185">Phone: +32 9 296 40 11</span></span>
> 
> <span data-ttu-id="a0cd3-186">**USA**:</span><span class="sxs-lookup"><span data-stu-id="a0cd3-186">**USA**:</span></span>
> 
> <span data-ttu-id="a0cd3-187">7 floor, Ave 1177 di hello Americas,</span><span class="sxs-lookup"><span data-stu-id="a0cd3-187">7th floor, 1177 Ave of hello Americas,</span></span>
> 
> <span data-ttu-id="a0cd3-188">New York, NY 10036</span><span class="sxs-lookup"><span data-stu-id="a0cd3-188">New York, NY 10036</span></span>
> 
> <span data-ttu-id="a0cd3-189">E-mail: [info.us@awingu.com](mailto:info.us@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-189">Email: [info.us@awingu.com](mailto:info.us@awingu.com)</span></span>

### <a name="microsoft-hosted-service-provider"></a><span data-ttu-id="a0cd3-190">Provider di servizi ospitati Microsoft</span><span class="sxs-lookup"><span data-stu-id="a0cd3-190">Microsoft Hosted Service Provider</span></span>
<span data-ttu-id="a0cd3-191">I partner di hosting offrono in genere completamente gestito ospitato desktop di Windows hello di servizio dell'applicazione, che può includere la gestione delle risorse di Azure, sistemi operativi, applicazioni e supporto tecnico con i partner di hello di licenze contratti Microsoft e altri fornitori di software insieme in un contratto di licenza di Provider di servizi tooallow rivendita di licenza di accesso sottoscrittore (SAL).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-191">Hosting partners typically offer a fully managed hosted Windows desktop and application service, which may include managing hello Azure resources, operating systems, applications, and helpdesk using hello partner's licensing agreements with Microsoft and other software providers along with being a Service Provider License Agreement tooallow reselling of Subscriber Access License (SAL).</span></span> <span data-ttu-id="a0cd3-192">Hello seguito vengono fornite informazioni dettagliate e informazioni di contatto per alcune delle hosting hello specializzate nell'assistenza ai clienti con la migrazione di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-192">hello following information provides details and contact information for some of hello hosters that specialize in assisting customers with their Azure RemoteApp migration.</span></span> <span data-ttu-id="a0cd3-193">Estrarre [elenco corrente di hello del provider di servizi ospitati](http://aka.ms/rdsonazurecertified) ha completato l'hello in IaaS apprendimento percorso e la valutazione di servizi desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-193">Check out [hello current list of Hosted Service Providers](http://aka.ms/rdsonazurecertified) that have completed hello RDS on IaaS learning path and assessment.</span></span>  

### <a name="citrix-service-provider-program"></a><span data-ttu-id="a0cd3-194">Programma Citrix Service Provider</span><span class="sxs-lookup"><span data-stu-id="a0cd3-194">Citrix Service Provider Program</span></span>
<span data-ttu-id="a0cd3-195">Programma di Provider del servizio Citrix Hello rende più semplice per semplicità di hello toodeliver provider del servizio di virtuale cloud computing tooSMBs, l'offerta di servizi di hello che vogliono in un modello semplice e pagamento a consumo.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-195">hello Citrix Service Provider Program makes it easy for service providers toodeliver hello simplicity of virtual cloud computing tooSMBs, offering them hello services they want in an easy, pay-as-you-go model.</span></span> <span data-ttu-id="a0cd3-196">I provider di servizi Citrix crescita SPLA di Microsoft ed espandere gli investimenti di piattaforma di servizi desktop remoto con qualsiasi dispositivo, accesso remoto via Internet, hello più ampio supporto dell'applicazione, un'esperienza, maggiore sicurezza e aumentare la scalabilità.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-196">Citrix Service Providers grow their Microsoft SPLA businesses and expand their RDS platform investments with any device, anywhere access, hello broadest application support, a rich experience, added security and increased scalability.</span></span> <span data-ttu-id="a0cd3-197">A loro volta, gli stessi provider di servizi Citrix possono attrarre più sottoscrittori, aumentare la soddisfazione dei clienti e ridurre i costi operativi.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-197">In turn, Citrix Service Providers attract more subscribers, increase customer satisfaction and reduce their operational costs.</span></span> <span data-ttu-id="a0cd3-198">[Leggere altre informazioni](http://www.citrix.com/products/service-providers.html) o [cercare un partner](https://www.citrix.com/buy/partnerlocator.html).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-198">[Learn more](http://www.citrix.com/products/service-providers.html) or [find a partner](https://www.citrix.com/buy/partnerlocator.html).</span></span>

#### <a name="acuutech"></a><span data-ttu-id="a0cd3-199">Acuutech</span><span class="sxs-lookup"><span data-stu-id="a0cd3-199">Acuutech</span></span>
<span data-ttu-id="a0cd3-200">[Acuutech](http://www.acuutech.com) è progettato per offrire soluzioni desktop ospitate, recapito completo desktop e applicazioni di ISV esperienze basate su tecnologia tooa globale client Microsoft base da Azure e i propri Data Center.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-200">[Acuutech](http://www.acuutech.com) specializes in providing hosted desktop solutions, delivering full desktop and ISV applications experiences built on Microsoft technology tooa global client base from Azure and their own datacenters.</span></span>

> <span data-ttu-id="a0cd3-201">Sede principale: Londra; Singapore; Houston (Texas)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-201">Primary location: London, UK; Singapore; Houston, TX</span></span>
> 
> <span data-ttu-id="a0cd3-202">Regione operativa: tutto il mondo</span><span class="sxs-lookup"><span data-stu-id="a0cd3-202">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="a0cd3-203">Stato partner: Gold</span><span class="sxs-lookup"><span data-stu-id="a0cd3-203">Partner status: Gold</span></span>
> 
> <span data-ttu-id="a0cd3-204">Provider di servizi cloud Microsoft: sì</span><span class="sxs-lookup"><span data-stu-id="a0cd3-204">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="a0cd3-205">Offerta di soluzioni desktop e RemoteApp basate sulla sessione: sì, entrambe</span><span class="sxs-lookup"><span data-stu-id="a0cd3-205">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="a0cd3-206">Soluzioni per la migrazione di Azure RemoteApp: sì, [altre informazioni](http://www.acuutech.com/ara-migration/)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-206">Azure RemoteApp migration solutions: Yes, [learn more](http://www.acuutech.com/ara-migration/)</span></span>
> 
> <span data-ttu-id="a0cd3-207">**Regno Unito**:</span><span class="sxs-lookup"><span data-stu-id="a0cd3-207">**United Kingdom**:</span></span>
>   
> <span data-ttu-id="a0cd3-208">5/6 York House, Langston Road,</span><span class="sxs-lookup"><span data-stu-id="a0cd3-208">5/6 York House, Langston Road,</span></span>
>   
> <span data-ttu-id="a0cd3-209">Loughton, Essex IG10 3TQ</span><span class="sxs-lookup"><span data-stu-id="a0cd3-209">Loughton, Essex IG10 3TQ</span></span>
>   
> <span data-ttu-id="a0cd3-210">Telefono: +44 (0) 20 8502 2155</span><span class="sxs-lookup"><span data-stu-id="a0cd3-210">Phone: +44 (0) 20 8502 2155</span></span>
> 
> <span data-ttu-id="a0cd3-211">**Singapore**:</span><span class="sxs-lookup"><span data-stu-id="a0cd3-211">**Singapore**:</span></span>
>   
> <span data-ttu-id="a0cd3-212">100 Cecil Street, #09-02,</span><span class="sxs-lookup"><span data-stu-id="a0cd3-212">100 Cecil Street, #09-02,</span></span> 
>   
> <span data-ttu-id="a0cd3-213">Hello 069532 globo, Singapore</span><span class="sxs-lookup"><span data-stu-id="a0cd3-213">hello Globe, Singapore 069532</span></span>
> 
> <span data-ttu-id="a0cd3-214">Telefono: +65 6709 4933</span><span class="sxs-lookup"><span data-stu-id="a0cd3-214">Phone: +65 6709 4933</span></span>
>   
> <span data-ttu-id="a0cd3-215">**America del Nord**:</span><span class="sxs-lookup"><span data-stu-id="a0cd3-215">**North America**:</span></span>
>   
> <span data-ttu-id="a0cd3-216">3601 S. Sandman St.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-216">3601 S. Sandman St.</span></span>
>   
> <span data-ttu-id="a0cd3-217">Suite 200, Houston, TX 77098</span><span class="sxs-lookup"><span data-stu-id="a0cd3-217">Suite 200, Houston, TX 77098</span></span>
>   
> <span data-ttu-id="a0cd3-218">Telefono: +1 713 691 0800</span><span class="sxs-lookup"><span data-stu-id="a0cd3-218">Phone: +1 713 691 0800</span></span>

#### <a name="aspex"></a><span data-ttu-id="a0cd3-219">ASPEX</span><span class="sxs-lookup"><span data-stu-id="a0cd3-219">ASPEX</span></span>
<span data-ttu-id="a0cd3-220">[ASPEX](http://www.aspex.be/en) è progettato per gli ISV transizione toohello Cloud e ISV' ricerca toooptimize le impostazioni di cloud corrente.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-220">[ASPEX](http://www.aspex.be/en) specializes in ISVs transitioning toohello Cloud and ISV‘ looking toooptimize their current cloud setups.</span></span> <span data-ttu-id="a0cd3-221">ASPEX offre un'ampia gamma di servizi gestiti, DevOps e di consulenza.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-221">ASPEX offers a wide range of managed services, devops, and consulting services.</span></span>  

> <span data-ttu-id="a0cd3-222">Sede principale: Anversa</span><span class="sxs-lookup"><span data-stu-id="a0cd3-222">Primary location: Antwerp, Belgium</span></span>
> 
> <span data-ttu-id="a0cd3-223">Regione operativa: Europa occidentale</span><span class="sxs-lookup"><span data-stu-id="a0cd3-223">Operation region: Western Europe</span></span>
> 
> <span data-ttu-id="a0cd3-224">Stato partner: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-224">Partner status: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span></span>
> 
> <span data-ttu-id="a0cd3-225">Provider di servizi cloud Microsoft: sì</span><span class="sxs-lookup"><span data-stu-id="a0cd3-225">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="a0cd3-226">Offerta di soluzioni desktop e RemoteApp basate sulla sessione: sì, entrambe</span><span class="sxs-lookup"><span data-stu-id="a0cd3-226">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="a0cd3-227">Soluzioni per la migrazione di Azure RemoteApp: sì, [altre informazioni](https://www.aspex.be/en/azure-remote-apps)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-227">Azure RemoteApp migration solutions: Yes, [learn more](https://www.aspex.be/en/azure-remote-apps)</span></span>
> 
> <span data-ttu-id="a0cd3-228">Telefono: +3232202198</span><span class="sxs-lookup"><span data-stu-id="a0cd3-228">Phone: +3232202198</span></span>
> 
> <span data-ttu-id="a0cd3-229">E-mail: [info@aspex.be](mailto:info@aspex.be)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-229">Mail: [info@aspex.be](mailto:info@aspex.be)</span></span>
> 
> <span data-ttu-id="a0cd3-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span></span>

#### <a name="caasecom"></a><span data-ttu-id="a0cd3-231">Caase.com</span><span class="sxs-lookup"><span data-stu-id="a0cd3-231">Caase.com</span></span>
<span data-ttu-id="a0cd3-232">[Caase.com](http://www.caase.com/) consente di aziende, amministrazioni locali, organismi non governativi, sanitari con il viaggio verso un modo efficiente di lavoro in hello Cloud Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-232">[Caase.com](http://www.caase.com/) helps businesses, local governments, non-governmental bodies and healthcare institutions with their journey towards a smarter way of work in hello Microsoft Cloud.</span></span> <span data-ttu-id="a0cd3-233">Produttività e sicurezza in qualsiasi luogo, con qualsiasi dispositivo e a basso costo IT.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-233">Being productive and secure at any place, with any device and at low IT cost.</span></span> <span data-ttu-id="a0cd3-234">Caase.com è un vero specialista di Microsoft Office365, Azure, Enterprise Mobility e Sicurezza e Windows.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-234">Caase.com is a true specialist for Microsoft Office365, Azure, Enterprise Mobility and Security and Windows.</span></span> <span data-ttu-id="a0cd3-235">Grazie alla consulenza, ai servizi di migrazione, ai programmi di adozione, alla formazione, alla gestione e al supporto di Microsoft, Caase.com crea una piattaforma sicura e ottimizzata per la collaborazione per i dipendenti, i partner e i fornitori dei clienti.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-235">With our consultancy, migration services, adoption programs, training, management and support Caase.com creates an optimized and secure platform for collaboration for both customers’ employees, partners and suppliers.</span></span>
<span data-ttu-id="a0cd3-236">Caase.com è mastermind hello di hello Azure remoto dell'area di lavoro (area di lavoro per dispositivi mobili) e hello digitale all'area di lavoro (Social Intranet).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-236">Caase.com is hello mastermind of hello Azure Remote Workspace (mobile workplace) and hello Digital Workplace (Social Intranet).</span></span> <span data-ttu-id="a0cd3-237">Entrambe le soluzioni – eseguite con l'adozione di – sono foundation hello che consente agli utenti di hello di queste soluzioni di analisi di più piacevole, efficace e di hello nella loro toohello route Cloud Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-237">Both solutions – accomplished with adoption – are hello foundation which ensures that hello users of these solutions have hello most pleasant, successful and effective experience in their route toohello Microsoft Cloud.</span></span>
<span data-ttu-id="a0cd3-238">Per la traduzione in olandese e un filmato di supporto visitare questa pagina: http://caase.com/over-ons/</span><span class="sxs-lookup"><span data-stu-id="a0cd3-238">Dutch translation ánd a supporting movie over here: http://caase.com/over-ons/</span></span>

> <span data-ttu-id="a0cd3-239">Area di operatività: con sede in Olanda e portata globale</span><span class="sxs-lookup"><span data-stu-id="a0cd3-239">Operation region: Dutch based, global reach</span></span>
> 
> <span data-ttu-id="a0cd3-240">Stato partner: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-240">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span></span>
> 
> <span data-ttu-id="a0cd3-241">Provider di servizi cloud Microsoft: sì</span><span class="sxs-lookup"><span data-stu-id="a0cd3-241">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="a0cd3-242">Offerta di soluzioni desktop e RemoteApp basate sulla sessione: sì, entrambe</span><span class="sxs-lookup"><span data-stu-id="a0cd3-242">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="a0cd3-243">Soluzioni per la migrazione di Azure RemoteApp: sì, [altre informazioni](http://caase.com/diensten/microsoft-azure/).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-243">Azure RemoteApp migration solutions: Yes, [learn more](http://caase.com/diensten/microsoft-azure/).</span></span>
> 
> 
> <span data-ttu-id="a0cd3-244">Paesi Bassi:</span><span class="sxs-lookup"><span data-stu-id="a0cd3-244">Netherlands:</span></span>
> 
> <span data-ttu-id="a0cd3-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span></span>
> 
> <span data-ttu-id="a0cd3-246">7521 BE, Enschede</span><span class="sxs-lookup"><span data-stu-id="a0cd3-246">7521 BE, Enschede</span></span>
> 
> <span data-ttu-id="a0cd3-247">Telefono: +31 (0) 88 4320 000</span><span class="sxs-lookup"><span data-stu-id="a0cd3-247">Phone: +31 (0) 88 4320 000</span></span>


#### <a name="nerdio"></a><span data-ttu-id="a0cd3-248">Nerdio</span><span class="sxs-lookup"><span data-stu-id="a0cd3-248">Nerdio</span></span>
<span data-ttu-id="a0cd3-249">[Nerdio per Azure](http://getnerdio.com/nfa/) è una piattaforma di automazione IT che offre provisioning estremamente semplice, gestione e ottimizzazione di ambienti IT completati hello cloud Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-249">[Nerdio for Azure](http://getnerdio.com/nfa/) is an IT automation platform that delivers ridiculously simple provisioning, management and optimization of complete IT environments in hello Microsoft cloud.</span></span> <span data-ttu-id="a0cd3-250">Consente di configurare desktop virtuali, applicazioni remote e server in un paio di ore;</span><span class="sxs-lookup"><span data-stu-id="a0cd3-250">Stand up virtual desktops, remote apps and servers in a couple of hours.</span></span> <span data-ttu-id="a0cd3-251">Amministrare l'ambiente hello in tre clic o meno con il portale di amministrazione di Nerdio.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-251">Administer hello environment in three clicks or less with Nerdio Admin Portal.</span></span> <span data-ttu-id="a0cd3-252">Utilizzare intelligente il ridimensionamento automatico e salvare 40% di too60 nelle risorse IaaS di Azure.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-252">Use intelligent auto-scaling and save 40 too60% in Azure IaaS resources.</span></span>

> <span data-ttu-id="a0cd3-253">Sede principale: area di Chicago, IL Sede operativa: a livello globale Stato del partner: [Oro](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Provider del servizio cloud di Microsoft: sì</span><span class="sxs-lookup"><span data-stu-id="a0cd3-253">Primary location: Chicago, IL Operation region: Worldwide Partner status: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="a0cd3-254">Offerta di soluzioni desktop e RemoteApp basate sulla sessione: sì, entrambe</span><span class="sxs-lookup"><span data-stu-id="a0cd3-254">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="a0cd3-255">Soluzioni per la migrazione di Azure RemoteApp: sì</span><span class="sxs-lookup"><span data-stu-id="a0cd3-255">Azure RemoteApp migration solutions: Yes</span></span>
> 
> 
> <span data-ttu-id="a0cd3-256">8001 Lincoln Ave</span><span class="sxs-lookup"><span data-stu-id="a0cd3-256">8001 Lincoln Ave</span></span>
> 
> <span data-ttu-id="a0cd3-257">Suite 212</span><span class="sxs-lookup"><span data-stu-id="a0cd3-257">Suite 212</span></span>
> 
> <span data-ttu-id="a0cd3-258">Skokie, IL 60077</span><span class="sxs-lookup"><span data-stu-id="a0cd3-258">Skokie, IL 60077</span></span>
> 
> <span data-ttu-id="a0cd3-259">USA</span><span class="sxs-lookup"><span data-stu-id="a0cd3-259">USA</span></span>
> 
> <span data-ttu-id="a0cd3-260">(844) 4NERDIO ext. 6</span><span class="sxs-lookup"><span data-stu-id="a0cd3-260">(844) 4NERDIO ext. 6</span></span>
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a><span data-ttu-id="a0cd3-261">**SaaSplaza**</span><span class="sxs-lookup"><span data-stu-id="a0cd3-261">**SaaSplaza**</span></span>
<span data-ttu-id="a0cd3-262">[SaaSplaza](http://www.saasplaza.com/) offre un portfolio Microsoft Dynamics completo (NAV, AX, GP, SL, CRM) con cloud privato e pubblico (Azure).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-262">[SaaSplaza](http://www.saasplaza.com/) offers complete Microsoft Dynamics portfolio (NAV, AX, GP, SL, CRM) private and public cloud (Azure).</span></span>

> <span data-ttu-id="a0cd3-263">Località primaria: Paesi Bassi</span><span class="sxs-lookup"><span data-stu-id="a0cd3-263">Primary location: Netherlands</span></span>
> 
> <span data-ttu-id="a0cd3-264">Area operativa: tutto il mondo</span><span class="sxs-lookup"><span data-stu-id="a0cd3-264">Operation Region: Worldwide</span></span>
> 
> <span data-ttu-id="a0cd3-265">Stato partner: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-265">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span></span>
> 
> <span data-ttu-id="a0cd3-266">Provider di servizi cloud Microsoft: sì</span><span class="sxs-lookup"><span data-stu-id="a0cd3-266">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="a0cd3-267">Offerta di soluzioni desktop e RemoteApp basate sulla sessione: sì, entrambe</span><span class="sxs-lookup"><span data-stu-id="a0cd3-267">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="a0cd3-268">**EMEA**:</span><span class="sxs-lookup"><span data-stu-id="a0cd3-268">**EMEA**:</span></span>
> 
> <span data-ttu-id="a0cd3-269">Prins Mauritslaan 29-35</span><span class="sxs-lookup"><span data-stu-id="a0cd3-269">Prins Mauritslaan 29-35</span></span>
> 
> <span data-ttu-id="a0cd3-270">71 LP Badhoevedorp</span><span class="sxs-lookup"><span data-stu-id="a0cd3-270">71 LP Badhoevedorp</span></span>
> 
> <span data-ttu-id="a0cd3-271">Hello (Paesi Bassi)</span><span class="sxs-lookup"><span data-stu-id="a0cd3-271">hello Netherlands</span></span>
> 
> <span data-ttu-id="a0cd3-272">Telefono: +31 20 547 8060</span><span class="sxs-lookup"><span data-stu-id="a0cd3-272">Phone: +31 20 547 8060</span></span> 
> 
>  <span data-ttu-id="a0cd3-273">**Americhe**:</span><span class="sxs-lookup"><span data-stu-id="a0cd3-273">**Americas**:</span></span>
> 
> <span data-ttu-id="a0cd3-274">171 Saxony Road, Suite 105</span><span class="sxs-lookup"><span data-stu-id="a0cd3-274">171 Saxony Road, Suite 105</span></span>
> 
> <span data-ttu-id="a0cd3-275">Encinitas, CA 92024</span><span class="sxs-lookup"><span data-stu-id="a0cd3-275">Encinitas, CA 92024</span></span>
> 
> <span data-ttu-id="a0cd3-276">San Diego</span><span class="sxs-lookup"><span data-stu-id="a0cd3-276">San Diego</span></span>
> 
> <span data-ttu-id="a0cd3-277">Stati Uniti</span><span class="sxs-lookup"><span data-stu-id="a0cd3-277">United States</span></span>
> 
> <span data-ttu-id="a0cd3-278">Telefono: +1 858 385 8900</span><span class="sxs-lookup"><span data-stu-id="a0cd3-278">Phone: +1 858 385 8900</span></span> 
> 
> <span data-ttu-id="a0cd3-279">**APAC**:</span><span class="sxs-lookup"><span data-stu-id="a0cd3-279">**APAC**:</span></span>
> 
> <span data-ttu-id="a0cd3-280">105 Cecil Street</span><span class="sxs-lookup"><span data-stu-id="a0cd3-280">105 Cecil Street</span></span>
>    
> <span data-ttu-id="a0cd3-281">\#11-08, hello ottagono</span><span class="sxs-lookup"><span data-stu-id="a0cd3-281">\#11-08, hello Octagon</span></span>
> 
> <span data-ttu-id="a0cd3-282">Singapore 069534</span><span class="sxs-lookup"><span data-stu-id="a0cd3-282">Singapore 069534</span></span>
> 
> <span data-ttu-id="a0cd3-283">Singapore</span><span class="sxs-lookup"><span data-stu-id="a0cd3-283">Singapore</span></span>
>   
> <span data-ttu-id="a0cd3-284">Telefono - Singapore: +65 6222 6591</span><span class="sxs-lookup"><span data-stu-id="a0cd3-284">Phone - Singapore: +65 6222 6591</span></span>
> 
> <span data-ttu-id="a0cd3-285">Telefono - Australia: +61 2 8310 5568</span><span class="sxs-lookup"><span data-stu-id="a0cd3-285">Phone - Australia: +61 2 8310 5568</span></span> 
>    
> <span data-ttu-id="a0cd3-286">Telefono - Nuova Zelanda: +64 4 488 0321</span><span class="sxs-lookup"><span data-stu-id="a0cd3-286">Phone - New Zealand: +64 4 488 0321</span></span>
> 
## <a name="need-more-help"></a><span data-ttu-id="a0cd3-287">Ulteriore assistenza</span><span class="sxs-lookup"><span data-stu-id="a0cd3-287">Need more help?</span></span>
<span data-ttu-id="a0cd3-288">Per farsi aiutare nella scelta o se si hanno altre domande,</span><span class="sxs-lookup"><span data-stu-id="a0cd3-288">Still need help choosing or have further questions?</span></span> <span data-ttu-id="a0cd3-289">Utilizzare uno dei seguenti metodi tooget Guida hello.</span><span class="sxs-lookup"><span data-stu-id="a0cd3-289">Use one of hello following methods tooget help.</span></span> 

1. <span data-ttu-id="a0cd3-290">Scrivere un'e-mail all'indirizzo [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-290">Email us at [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span></span>
2. <span data-ttu-id="a0cd3-291">Contattare il [supporto tecnico di Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-291">Contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="a0cd3-292">Aprire un [caso di supporto su Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-292">Start by opening an [Azure support case](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
3. <span data-ttu-id="a0cd3-293">Contattare il</span><span class="sxs-lookup"><span data-stu-id="a0cd3-293">Call us.</span></span> <span data-ttu-id="a0cd3-294">[team di vendita locale](https://azure.microsoft.com/overview/sales-number/).</span><span class="sxs-lookup"><span data-stu-id="a0cd3-294">[Find a local sales number](https://azure.microsoft.com/overview/sales-number/).</span></span>

