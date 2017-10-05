---
title: Risolvere i problemi di RBAC di Azure | Microsoft Docs
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
ms.openlocfilehash: 407c030ea159915d4d7ac21760a3d17ec2204372
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="role-based-access-control-troubleshooting"></a><span data-ttu-id="92a1f-103">Risoluzione dei problemi del controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="92a1f-103">Role-Based Access Control troubleshooting</span></span>

<span data-ttu-id="92a1f-104">Questo articolo contiene le risposte alle domande comuni sui diritti di accesso specifici concessi ai ruoli, in modo da sapere cosa accade quando si usano i ruoli nel Portale di Azure e da poter risolvere i problemi di accesso.</span><span class="sxs-lookup"><span data-stu-id="92a1f-104">This document article answers common questions about the specific access rights that are granted with roles, so that you know what to expect when using the roles in the Azure portal and can troubleshoot access problems.</span></span> <span data-ttu-id="92a1f-105">Questi tre ruoli coprono tutti i tipi di risorsa:</span><span class="sxs-lookup"><span data-stu-id="92a1f-105">These three roles cover all resource types:</span></span>

* <span data-ttu-id="92a1f-106">Proprietario</span><span class="sxs-lookup"><span data-stu-id="92a1f-106">Owner</span></span>  
* <span data-ttu-id="92a1f-107">Collaboratore</span><span class="sxs-lookup"><span data-stu-id="92a1f-107">Contributor</span></span>  
* <span data-ttu-id="92a1f-108">Lettore</span><span class="sxs-lookup"><span data-stu-id="92a1f-108">Reader</span></span>  

<span data-ttu-id="92a1f-109">Proprietari e collaboratori hanno accesso completo all'esperienza di gestione, ma il collaboratore non può concedere l'accesso ad altri utenti o gruppi.</span><span class="sxs-lookup"><span data-stu-id="92a1f-109">Owners and contributors both have full access to the management experience, but a contributor can’t give access to other users or groups.</span></span> <span data-ttu-id="92a1f-110">Il ruolo di lettore è maggiormente articolato e verrà quindi esaminato in maniera più approfondita.</span><span class="sxs-lookup"><span data-stu-id="92a1f-110">Things get a little more interesting with the reader role, so that’s where we'll spend some time.</span></span> <span data-ttu-id="92a1f-111">Per informazioni dettagliate su come concedere l'accesso, vedere [Controllo degli accessi in base al ruolo di Azure](role-based-access-control-configure.md) .</span><span class="sxs-lookup"><span data-stu-id="92a1f-111">See the [Role-Based Access Control get-started article](role-based-access-control-configure.md) for details on how to grant access.</span></span>

## <a name="app-service-workloads"></a><span data-ttu-id="92a1f-112">Carichi di lavoro del servizio app</span><span class="sxs-lookup"><span data-stu-id="92a1f-112">App service workloads</span></span>
### <a name="write-access-capabilities"></a><span data-ttu-id="92a1f-113">Funzionalità di accesso in scrittura</span><span class="sxs-lookup"><span data-stu-id="92a1f-113">Write access capabilities</span></span>
<span data-ttu-id="92a1f-114">Se si concede a un utente l'accesso in sola lettura a un'unica app Web, sono disabilitate alcune funzionalità non prevedibili.</span><span class="sxs-lookup"><span data-stu-id="92a1f-114">If you grant a user read-only access to a single web app, some features are disabled that you might not expect.</span></span> <span data-ttu-id="92a1f-115">Per le funzionalità di gestione seguenti è necessario avere accesso **in scrittura** a un'app Web, come Collaboratore o Proprietario. Tali funzionalità non saranno disponibili in uno scenario di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="92a1f-115">The following management capabilities require **write** access to a web app (either Contributor or Owner), and aren’t available in any read-only scenario.</span></span>

* <span data-ttu-id="92a1f-116">Comandi (quali avvio, interruzione e così via)</span><span class="sxs-lookup"><span data-stu-id="92a1f-116">Commands (like start, stop, etc.)</span></span>
* <span data-ttu-id="92a1f-117">Modifica di impostazioni quali la configurazione generale, le impostazioni di scalabilità, di backup e di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="92a1f-117">Changing settings like general configuration, scale settings, backup settings, and monitoring settings</span></span>
* <span data-ttu-id="92a1f-118">Accesso a credenziali di pubblicazione e altri segreti, quali le impostazioni delle app e le stringhe di connessione.</span><span class="sxs-lookup"><span data-stu-id="92a1f-118">Accessing publishing credentials and other secrets like app settings and connection strings</span></span>
* <span data-ttu-id="92a1f-119">Streaming dei log</span><span class="sxs-lookup"><span data-stu-id="92a1f-119">Streaming logs</span></span>
* <span data-ttu-id="92a1f-120">Configurazione dei log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="92a1f-120">Diagnostic logs configuration</span></span>
* <span data-ttu-id="92a1f-121">Console (prompt dei comandi)</span><span class="sxs-lookup"><span data-stu-id="92a1f-121">Console (command prompt)</span></span>
* <span data-ttu-id="92a1f-122">Distribuzioni attive e recenti, per la distribuzione continua del Git locale</span><span class="sxs-lookup"><span data-stu-id="92a1f-122">Active and recent deployments (for local git continuous deployment)</span></span>
* <span data-ttu-id="92a1f-123">Spesa prevista</span><span class="sxs-lookup"><span data-stu-id="92a1f-123">Estimated spend</span></span>
* <span data-ttu-id="92a1f-124">Test Web</span><span class="sxs-lookup"><span data-stu-id="92a1f-124">Web tests</span></span>
* <span data-ttu-id="92a1f-125">Rete virtuale, visibile per un lettore solo se in precedenza era già stata configurata una rete virtuale da un utente con accesso in scrittura.</span><span class="sxs-lookup"><span data-stu-id="92a1f-125">Virtual network (only visible to a reader if a virtual network has previously been configured by a user with write access).</span></span>

<span data-ttu-id="92a1f-126">Se non è possibile accedere a nessuno di questi titoli, è necessario richiedere all'amministratore l'accesso come Collaboratore per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="92a1f-126">If you can't access any of these tiles, you need to ask your administrator for Contributor access to the web app.</span></span>

### <a name="dealing-with-related-resources"></a><span data-ttu-id="92a1f-127">Gestione delle risorse correlate</span><span class="sxs-lookup"><span data-stu-id="92a1f-127">Dealing with related resources</span></span>
<span data-ttu-id="92a1f-128">La complessità delle app Web è accentuata dalle interazioni tra alcune risorse diverse.</span><span class="sxs-lookup"><span data-stu-id="92a1f-128">Web apps are complicated by the presence of a few different resources that interplay.</span></span> <span data-ttu-id="92a1f-129">Di seguito è illustrato un tipico gruppo di risorse con alcuni siti Web:</span><span class="sxs-lookup"><span data-stu-id="92a1f-129">Here is a typical resource group with a couple websites:</span></span>

![Gruppo di risorse per app Web](./media/role-based-access-control-troubleshooting/website-resource-model.png)

<span data-ttu-id="92a1f-131">Quindi, se si concede l'accesso solo all'app Web, la maggior parte delle funzionalità del pannello del sito Web nel portale di Azure viene disabilitata.</span><span class="sxs-lookup"><span data-stu-id="92a1f-131">As a result, if you grant someone access to just the web app, much of the functionality on the website blade in the Azure portal is disabled.</span></span>

<span data-ttu-id="92a1f-132">Questi elementi richiedono accesso **in scrittura** al **piano di servizio App** che corrisponde al sito Web:</span><span class="sxs-lookup"><span data-stu-id="92a1f-132">These items require **write** access to the **App Service plan** that corresponds to your website:</span></span>  

* <span data-ttu-id="92a1f-133">Visualizzazione del piano tariffario dell'app Web, che può essere Free o Standard</span><span class="sxs-lookup"><span data-stu-id="92a1f-133">Viewing the web app’s pricing tier (Free or Standard)</span></span>  
* <span data-ttu-id="92a1f-134">Configurazione di scalabilità, ossia numero di istanze, dimensione della macchina virtuale, impostazioni di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="92a1f-134">Scale configuration (number of instances, virtual machine size, autoscale settings)</span></span>  
* <span data-ttu-id="92a1f-135">Quote, ad esempio archiviazione, larghezza di banda e CPU</span><span class="sxs-lookup"><span data-stu-id="92a1f-135">Quotas (storage, bandwidth, CPU)</span></span>  

<span data-ttu-id="92a1f-136">Gli elementi seguenti richiedono accesso **in scrittura** all'intero **gruppo di risorse** che contiene il sito Web:</span><span class="sxs-lookup"><span data-stu-id="92a1f-136">These items require **write** access to the whole **Resource group** that contains your website:</span></span>  

* <span data-ttu-id="92a1f-137">Certificati e associazioni SSL. I certificati SSL possono essere condivisi tra siti appartenenti allo stesso gruppo di risorse e area geografica.</span><span class="sxs-lookup"><span data-stu-id="92a1f-137">SSL Certificates and bindings (SSL certificates can be shared between sites in the same resource group and geo-location)</span></span>  
* <span data-ttu-id="92a1f-138">Regole di avviso</span><span class="sxs-lookup"><span data-stu-id="92a1f-138">Alert rules</span></span>  
* <span data-ttu-id="92a1f-139">Impostazioni di scalabilità automatica</span><span class="sxs-lookup"><span data-stu-id="92a1f-139">Autoscale settings</span></span>  
* <span data-ttu-id="92a1f-140">Componenti di Application Insights</span><span class="sxs-lookup"><span data-stu-id="92a1f-140">Application insights components</span></span>  
* <span data-ttu-id="92a1f-141">Test Web</span><span class="sxs-lookup"><span data-stu-id="92a1f-141">Web tests</span></span>  

## <a name="virtual-machine-workloads"></a><span data-ttu-id="92a1f-142">Carichi di lavoro delle macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="92a1f-142">Virtual machine workloads</span></span>
<span data-ttu-id="92a1f-143">Analogamente a quanto accade con le app Web, alcune funzionalità del blade della macchina virtuale richiedono l'accesso in scrittura alla macchina virtuale o ad altre risorse del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="92a1f-143">Much like with web apps, some features on the virtual machine blade require write access to the virtual machine, or to other resources in the resource group.</span></span>

<span data-ttu-id="92a1f-144">Le macchine virtuali sono correlate a nomi di dominio, reti virtuali, account di archiviazione e regole di avviso.</span><span class="sxs-lookup"><span data-stu-id="92a1f-144">Virtual machines are related to Domain names, virtual networks, storage accounts, and alert rules.</span></span>

<span data-ttu-id="92a1f-145">Gli elementi seguenti richiedono accesso **in scrittura** alla **macchina virtuale**:</span><span class="sxs-lookup"><span data-stu-id="92a1f-145">These items require **write** access to the **Virtual machine**:</span></span>

* <span data-ttu-id="92a1f-146">Endpoint</span><span class="sxs-lookup"><span data-stu-id="92a1f-146">Endpoints</span></span>  
* <span data-ttu-id="92a1f-147">Indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="92a1f-147">IP addresses</span></span>  
* <span data-ttu-id="92a1f-148">Dischi</span><span class="sxs-lookup"><span data-stu-id="92a1f-148">Disks</span></span>  
* <span data-ttu-id="92a1f-149">Estensioni</span><span class="sxs-lookup"><span data-stu-id="92a1f-149">Extensions</span></span>  

<span data-ttu-id="92a1f-150">Gli elementi seguenti richiedono accesso **in scrittura** sia alla **macchina virtuale** che al **gruppo di risorse**, così come al nome di dominio a cui appartiene:</span><span class="sxs-lookup"><span data-stu-id="92a1f-150">These require **write** access to both the **Virtual machine**, and the **Resource group** (along with the Domain name) that it is in:</span></span>  

* <span data-ttu-id="92a1f-151">Set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="92a1f-151">Availability set</span></span>  
* <span data-ttu-id="92a1f-152">Set con carico bilanciato</span><span class="sxs-lookup"><span data-stu-id="92a1f-152">Load balanced set</span></span>  
* <span data-ttu-id="92a1f-153">Regole di avviso</span><span class="sxs-lookup"><span data-stu-id="92a1f-153">Alert rules</span></span>  

<span data-ttu-id="92a1f-154">Se non è possibile accedere a nessuno di questi riquadri, richiedere all'amministratore l'accesso come Collaboratore al gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="92a1f-154">If you can't access any of these tiles, ask your administrator for Contributor access to the Resource group.</span></span>

## <a name="see-more"></a><span data-ttu-id="92a1f-155">Altro</span><span class="sxs-lookup"><span data-stu-id="92a1f-155">See more</span></span>
* <span data-ttu-id="92a1f-156">[Controllo degli accessi in base al ruolo](role-based-access-control-configure.md): introduzione al controllo degli accessi in base al ruolo nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="92a1f-156">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span></span>
* <span data-ttu-id="92a1f-157">[Ruoli predefiniti](role-based-access-built-in-roles.md): informazioni dettagliate sui ruoli predefiniti del controllo degli accessi in base al ruolo.</span><span class="sxs-lookup"><span data-stu-id="92a1f-157">[Built-in roles](role-based-access-built-in-roles.md): Get details about the roles that come standard in RBAC.</span></span>
* <span data-ttu-id="92a1f-158">[Ruoli personalizzati nel controllo degli accessi in base al ruolo di Azure](role-based-access-control-custom-roles.md): informazioni su come creare ruoli personalizzati per esigenze di accesso specifiche.</span><span class="sxs-lookup"><span data-stu-id="92a1f-158">[Custom roles in Azure RBAC](role-based-access-control-custom-roles.md): Learn how to create custom roles to fit your access needs.</span></span>
* <span data-ttu-id="92a1f-159">[Creare un report della cronologia delle modifiche relative all'accesso](role-based-access-control-access-change-history-report.md): monitoraggio delle modifiche nelle assegnazioni dei ruoli nel controllo degli accessi in base al ruolo.</span><span class="sxs-lookup"><span data-stu-id="92a1f-159">[Create an access change history report](role-based-access-control-access-change-history-report.md): Keep track of changing role assignments in RBAC.</span></span>

