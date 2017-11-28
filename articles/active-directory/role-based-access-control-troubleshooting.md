---
title: aaaTroubleshoot RBAC Azure | Documenti Microsoft
description: Assistenza per problemi o domande sulle risorse del controllo degli accessi in base al ruolo.
services: azure-portal
documentationcenter: na
author: andredm7
manager: femila
ms.assetid: df42cca2-02d6-4f3c-9d56-260e1eb7dc44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 15feced32d8459d90c4c246d335932f90e1fc91f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-troubleshooting"></a><span data-ttu-id="2fffc-103">Risoluzione dei problemi del controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="2fffc-103">Role-Based Access Control troubleshooting</span></span>

<span data-ttu-id="2fffc-104">In questo articolo documento risponde alle domande comuni su hello specifici diritti di accesso che vengono concesse ai ruoli, in modo da sapere quali tooexpect quando si utilizzano ruoli nel portale di Azure hello hello e possibile risolvere i problemi di accesso.</span><span class="sxs-lookup"><span data-stu-id="2fffc-104">This document article answers common questions about hello specific access rights that are granted with roles, so that you know what tooexpect when using hello roles in hello Azure portal and can troubleshoot access problems.</span></span> <span data-ttu-id="2fffc-105">Questi tre ruoli coprono tutti i tipi di risorsa:</span><span class="sxs-lookup"><span data-stu-id="2fffc-105">These three roles cover all resource types:</span></span>

* <span data-ttu-id="2fffc-106">Proprietario</span><span class="sxs-lookup"><span data-stu-id="2fffc-106">Owner</span></span>  
* <span data-ttu-id="2fffc-107">Collaboratore</span><span class="sxs-lookup"><span data-stu-id="2fffc-107">Contributor</span></span>  
* <span data-ttu-id="2fffc-108">Reader</span><span class="sxs-lookup"><span data-stu-id="2fffc-108">Reader</span></span>  

<span data-ttu-id="2fffc-109">I proprietari e i collaboratori dispongono dell'accesso completo toohello gestione esperienza, ma non è possibile assegnare un collaboratore accesso tooother utenti o gruppi.</span><span class="sxs-lookup"><span data-stu-id="2fffc-109">Owners and contributors both have full access toohello management experience, but a contributor can’t give access tooother users or groups.</span></span> <span data-ttu-id="2fffc-110">Le cose interessanti un po' più con il ruolo di lettore hello, in modo che sia in cui è necessario passare del tempo.</span><span class="sxs-lookup"><span data-stu-id="2fffc-110">Things get a little more interesting with hello reader role, so that’s where we'll spend some time.</span></span> <span data-ttu-id="2fffc-111">Vedere hello [articolo avviato get Role-Based Access Control](role-based-access-control-configure.md) per informazioni dettagliate sulla modalità di accesso toogrant.</span><span class="sxs-lookup"><span data-stu-id="2fffc-111">See hello [Role-Based Access Control get-started article](role-based-access-control-configure.md) for details on how toogrant access.</span></span>

## <a name="app-service-workloads"></a><span data-ttu-id="2fffc-112">Carichi di lavoro del servizio app</span><span class="sxs-lookup"><span data-stu-id="2fffc-112">App service workloads</span></span>
### <a name="write-access-capabilities"></a><span data-ttu-id="2fffc-113">Funzionalità di accesso in scrittura</span><span class="sxs-lookup"><span data-stu-id="2fffc-113">Write access capabilities</span></span>
<span data-ttu-id="2fffc-114">Se si concede a un'utente accesso in sola lettura tooa singolo web app, sono disabilitate alcune funzionalità che non è prevedibile.</span><span class="sxs-lookup"><span data-stu-id="2fffc-114">If you grant a user read-only access tooa single web app, some features are disabled that you might not expect.</span></span> <span data-ttu-id="2fffc-115">Hello seguenti funzionalità di gestione richiede **scrivere** accedere tooa web app (Collaboratore o proprietario) e non sono disponibili in qualsiasi scenario di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="2fffc-115">hello following management capabilities require **write** access tooa web app (either Contributor or Owner), and aren’t available in any read-only scenario.</span></span>

* <span data-ttu-id="2fffc-116">Comandi (quali avvio, interruzione e così via)</span><span class="sxs-lookup"><span data-stu-id="2fffc-116">Commands (like start, stop, etc.)</span></span>
* <span data-ttu-id="2fffc-117">Modifica di impostazioni quali la configurazione generale, le impostazioni di scalabilità, di backup e di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="2fffc-117">Changing settings like general configuration, scale settings, backup settings, and monitoring settings</span></span>
* <span data-ttu-id="2fffc-118">Accesso a credenziali di pubblicazione e altri segreti, quali le impostazioni delle app e le stringhe di connessione.</span><span class="sxs-lookup"><span data-stu-id="2fffc-118">Accessing publishing credentials and other secrets like app settings and connection strings</span></span>
* <span data-ttu-id="2fffc-119">Streaming dei log</span><span class="sxs-lookup"><span data-stu-id="2fffc-119">Streaming logs</span></span>
* <span data-ttu-id="2fffc-120">Configurazione dei log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="2fffc-120">Diagnostic logs configuration</span></span>
* <span data-ttu-id="2fffc-121">Console (prompt dei comandi)</span><span class="sxs-lookup"><span data-stu-id="2fffc-121">Console (command prompt)</span></span>
* <span data-ttu-id="2fffc-122">Distribuzioni attive e recenti, per la distribuzione continua del Git locale</span><span class="sxs-lookup"><span data-stu-id="2fffc-122">Active and recent deployments (for local git continuous deployment)</span></span>
* <span data-ttu-id="2fffc-123">Spesa prevista</span><span class="sxs-lookup"><span data-stu-id="2fffc-123">Estimated spend</span></span>
* <span data-ttu-id="2fffc-124">Test Web</span><span class="sxs-lookup"><span data-stu-id="2fffc-124">Web tests</span></span>
* <span data-ttu-id="2fffc-125">Rete virtuale (solo lettura tooa visibile se una rete virtuale è stata configurata in precedenza da un utente con accesso in scrittura).</span><span class="sxs-lookup"><span data-stu-id="2fffc-125">Virtual network (only visible tooa reader if a virtual network has previously been configured by a user with write access).</span></span>

<span data-ttu-id="2fffc-126">Se non è possibile accedere a uno di questi riquadri, è necessario tooask l'amministratore per l'app web di collaboratore accesso toohello.</span><span class="sxs-lookup"><span data-stu-id="2fffc-126">If you can't access any of these tiles, you need tooask your administrator for Contributor access toohello web app.</span></span>

### <a name="dealing-with-related-resources"></a><span data-ttu-id="2fffc-127">Gestione delle risorse correlate</span><span class="sxs-lookup"><span data-stu-id="2fffc-127">Dealing with related resources</span></span>
<span data-ttu-id="2fffc-128">Le app Web sono complicate da presenza hello di alcune risorse diverse che interazione.</span><span class="sxs-lookup"><span data-stu-id="2fffc-128">Web apps are complicated by hello presence of a few different resources that interplay.</span></span> <span data-ttu-id="2fffc-129">Di seguito è illustrato un tipico gruppo di risorse con alcuni siti Web:</span><span class="sxs-lookup"><span data-stu-id="2fffc-129">Here is a typical resource group with a couple websites:</span></span>

![Gruppo di risorse per app Web](./media/role-based-access-control-troubleshooting/website-resource-model.png)

<span data-ttu-id="2fffc-131">Di conseguenza, se si autorizza l'applicazione web di accesso toojust hello, gran parte delle funzionalità di hello nel Pannello di hello sito Web nel portale di Azure hello è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="2fffc-131">As a result, if you grant someone access toojust hello web app, much of hello functionality on hello website blade in hello Azure portal is disabled.</span></span>

<span data-ttu-id="2fffc-132">Questi elementi richiedono **scrivere** accedere toohello **piano di servizio App** corrispondente sito Web tooyour:</span><span class="sxs-lookup"><span data-stu-id="2fffc-132">These items require **write** access toohello **App Service plan** that corresponds tooyour website:</span></span>  

* <span data-ttu-id="2fffc-133">App web hello di visualizzazione del piano tariffario (Free o Standard)</span><span class="sxs-lookup"><span data-stu-id="2fffc-133">Viewing hello web app’s pricing tier (Free or Standard)</span></span>  
* <span data-ttu-id="2fffc-134">Configurazione di scalabilità, ossia numero di istanze, dimensione della macchina virtuale, impostazioni di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="2fffc-134">Scale configuration (number of instances, virtual machine size, autoscale settings)</span></span>  
* <span data-ttu-id="2fffc-135">Quote, ad esempio archiviazione, larghezza di banda e CPU</span><span class="sxs-lookup"><span data-stu-id="2fffc-135">Quotas (storage, bandwidth, CPU)</span></span>  

<span data-ttu-id="2fffc-136">Questi elementi richiedono **scrivere** toohello accesso intero **gruppo di risorse** che contiene il sito Web:</span><span class="sxs-lookup"><span data-stu-id="2fffc-136">These items require **write** access toohello whole **Resource group** that contains your website:</span></span>  

* <span data-ttu-id="2fffc-137">I certificati SSL e associazioni (i certificati SSL possono essere condivisi tra siti in hello stesso gruppo di risorse e posizione geografica)</span><span class="sxs-lookup"><span data-stu-id="2fffc-137">SSL Certificates and bindings (SSL certificates can be shared between sites in hello same resource group and geo-location)</span></span>  
* <span data-ttu-id="2fffc-138">Regole di avviso</span><span class="sxs-lookup"><span data-stu-id="2fffc-138">Alert rules</span></span>  
* <span data-ttu-id="2fffc-139">Impostazioni di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="2fffc-139">Autoscale settings</span></span>  
* <span data-ttu-id="2fffc-140">Componenti di Application Insights</span><span class="sxs-lookup"><span data-stu-id="2fffc-140">Application insights components</span></span>  
* <span data-ttu-id="2fffc-141">Test Web</span><span class="sxs-lookup"><span data-stu-id="2fffc-141">Web tests</span></span>  

## <a name="virtual-machine-workloads"></a><span data-ttu-id="2fffc-142">Carichi di lavoro delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="2fffc-142">Virtual machine workloads</span></span>
<span data-ttu-id="2fffc-143">Molto come con le app web, alcune funzionalità nel pannello macchine virtuali hello richiedono una macchina virtuale di accesso in scrittura toohello o tooother risorse nel gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="2fffc-143">Much like with web apps, some features on hello virtual machine blade require write access toohello virtual machine, or tooother resources in hello resource group.</span></span>

<span data-ttu-id="2fffc-144">Macchine virtuali sono nomi tooDomain correlati, le reti virtuali, gli account di archiviazione e le regole di avviso.</span><span class="sxs-lookup"><span data-stu-id="2fffc-144">Virtual machines are related tooDomain names, virtual networks, storage accounts, and alert rules.</span></span>

<span data-ttu-id="2fffc-145">Questi elementi richiedono **scrivere** accedere toohello **macchina virtuale**:</span><span class="sxs-lookup"><span data-stu-id="2fffc-145">These items require **write** access toohello **Virtual machine**:</span></span>

* <span data-ttu-id="2fffc-146">Endpoint</span><span class="sxs-lookup"><span data-stu-id="2fffc-146">Endpoints</span></span>  
* <span data-ttu-id="2fffc-147">Indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="2fffc-147">IP addresses</span></span>  
* <span data-ttu-id="2fffc-148">Dischi</span><span class="sxs-lookup"><span data-stu-id="2fffc-148">Disks</span></span>  
* <span data-ttu-id="2fffc-149">Estensioni</span><span class="sxs-lookup"><span data-stu-id="2fffc-149">Extensions</span></span>  

<span data-ttu-id="2fffc-150">Questi cubi richiedono **scrivere** hello tooboth accesso **macchina virtuale**, hello e **gruppo di risorse** (insieme a nome di dominio hello) che non sia:</span><span class="sxs-lookup"><span data-stu-id="2fffc-150">These require **write** access tooboth hello **Virtual machine**, and hello **Resource group** (along with hello Domain name) that it is in:</span></span>  

* <span data-ttu-id="2fffc-151">Set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="2fffc-151">Availability set</span></span>  
* <span data-ttu-id="2fffc-152">Set con carico bilanciato</span><span class="sxs-lookup"><span data-stu-id="2fffc-152">Load balanced set</span></span>  
* <span data-ttu-id="2fffc-153">Regole di avviso</span><span class="sxs-lookup"><span data-stu-id="2fffc-153">Alert rules</span></span>  

<span data-ttu-id="2fffc-154">Se non è possibile accedere a uno di questi riquadri, chiedere all'amministratore per gruppo di risorse toohello accesso collaboratore.</span><span class="sxs-lookup"><span data-stu-id="2fffc-154">If you can't access any of these tiles, ask your administrator for Contributor access toohello Resource group.</span></span>

## <a name="see-more"></a><span data-ttu-id="2fffc-155">Altro</span><span class="sxs-lookup"><span data-stu-id="2fffc-155">See more</span></span>
* <span data-ttu-id="2fffc-156">[Controllo di accesso basato su ruoli](role-based-access-control-configure.md): Introduzione a RBAC in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fffc-156">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="2fffc-157">[Ruoli predefiniti](role-based-access-built-in-roles.md): ottenere informazioni sui ruoli hello forniti come standard in RBAC.</span><span class="sxs-lookup"><span data-stu-id="2fffc-157">[Built-in roles](role-based-access-built-in-roles.md): Get details about hello roles that come standard in RBAC.</span></span>
* <span data-ttu-id="2fffc-158">[Ruoli personalizzati in Azure RBAC](role-based-access-control-custom-roles.md): informazioni su come toocreate ruoli personalizzati toofit le esigenze di accesso.</span><span class="sxs-lookup"><span data-stu-id="2fffc-158">[Custom roles in Azure RBAC](role-based-access-control-custom-roles.md): Learn how toocreate custom roles toofit your access needs.</span></span>
* <span data-ttu-id="2fffc-159">[Creare un report della cronologia delle modifiche relative all'accesso](role-based-access-control-access-change-history-report.md): monitoraggio delle modifiche nelle assegnazioni dei ruoli nel controllo degli accessi in base al ruolo.</span><span class="sxs-lookup"><span data-stu-id="2fffc-159">[Create an access change history report](role-based-access-control-access-change-history-report.md): Keep track of changing role assignments in RBAC.</span></span>

