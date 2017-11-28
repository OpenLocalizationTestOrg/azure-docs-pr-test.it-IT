---
title: aaaMigrate un DNS active nome tooAzure servizio App | Documenti Microsoft
description: "Informazioni su come un nome di dominio DNS personalizzato che è già assegnato tooa toomigrate live tooAzure sito servizio App senza alcun tempo di inattività."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 10da5b8a-1823-41a3-a2ff-a0717c2b5c2d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: cephalin
ms.openlocfilehash: fbc4cc30dcb87efb2e867cb65c5404b667661e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-active-dns-name-tooazure-app-service"></a><span data-ttu-id="808fd-103">Eseguire la migrazione di un active tooAzure di nome DNS del servizio App</span><span class="sxs-lookup"><span data-stu-id="808fd-103">Migrate an active DNS name tooAzure App Service</span></span>

<span data-ttu-id="808fd-104">Questo articolo viene illustrato come un DNS active toomigrate denominati troppo[Azure App Service](../app-service/app-service-value-prop-what-is.md) senza alcun tempo di inattività.</span><span class="sxs-lookup"><span data-stu-id="808fd-104">This article shows you how toomigrate an active DNS name too[Azure App Service](../app-service/app-service-value-prop-what-is.md) without any downtime.</span></span>

<span data-ttu-id="808fd-105">Quando si esegue la migrazione di un sito in tempo reale e il relativo tooApp nome di dominio DNS del servizio, tale nome DNS è già in uso presso il traffico in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="808fd-105">When you migrate a live site and its DNS domain name tooApp Service, that DNS name is already serving live traffic.</span></span> <span data-ttu-id="808fd-106">È possibile evitare periodi di inattività per la risoluzione DNS durante la migrazione di hello associando hello active tooyour di nome DNS del servizio App app modalità preemptive.</span><span class="sxs-lookup"><span data-stu-id="808fd-106">You can avoid downtime in DNS resolution during hello migration by binding hello active DNS name tooyour App Service app preemptively.</span></span>

<span data-ttu-id="808fd-107">Se non si ritiene che la risoluzione DNS periodi di inattività, vedere [mappare un esistente personalizzato DNS nome tooAzure App Web](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="808fd-107">If you're not worried about downtime in DNS resolution, see [Map an existing custom DNS name tooAzure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="808fd-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="808fd-108">Prerequisites</span></span>

<span data-ttu-id="808fd-109">toocomplete questo procedure:</span><span class="sxs-lookup"><span data-stu-id="808fd-109">toocomplete this how-to:</span></span>

- <span data-ttu-id="808fd-110">[Verificare che l'app del servizio app non sia inclusa nel livello GRATUITO](app-service-web-tutorial-custom-domain.md#checkpricing).</span><span class="sxs-lookup"><span data-stu-id="808fd-110">[Make sure that your App Service app is not in FREE tier](app-service-web-tutorial-custom-domain.md#checkpricing).</span></span>

## <a name="bind-hello-domain-name-preemptively"></a><span data-ttu-id="808fd-111">Associare il nome di dominio hello modalità preemptive</span><span class="sxs-lookup"><span data-stu-id="808fd-111">Bind hello domain name preemptively</span></span>

<span data-ttu-id="808fd-112">Quando si associa un dominio personalizzato modalità preemptive, eseguire entrambe le operazioni seguenti hello prima di apportare modifiche ai record DNS:</span><span class="sxs-lookup"><span data-stu-id="808fd-112">When you bind a custom domain preemptively, you accomplish both of hello following before making any changes to your DNS records:</span></span>

- <span data-ttu-id="808fd-113">Verificare la proprietà del dominio</span><span class="sxs-lookup"><span data-stu-id="808fd-113">Verify domain ownership</span></span>
- <span data-ttu-id="808fd-114">Abilita hello nome di dominio per l'app</span><span class="sxs-lookup"><span data-stu-id="808fd-114">Enable hello domain name for your app</span></span>

<span data-ttu-id="808fd-115">Quando si migra infine il nome DNS personalizzato hello vecchio sito toohello app del servizio App, non saranno presenti tempi di inattività nella risoluzione DNS.</span><span class="sxs-lookup"><span data-stu-id="808fd-115">When you finally migrate your custom DNS name from hello old site toohello App Service app, there will be no downtime in DNS resolution.</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a><span data-ttu-id="808fd-116">Creare un record di verifica del dominio</span><span class="sxs-lookup"><span data-stu-id="808fd-116">Create domain verification record</span></span>

<span data-ttu-id="808fd-117">la proprietà dominio tooverify, Aggiungi un TXT record.</span><span class="sxs-lookup"><span data-stu-id="808fd-117">tooverify domain ownership, Add a TXT record.</span></span> <span data-ttu-id="808fd-118">esegue il mapping di Hello record TXT da _awverify.&lt; sottodominio >_ too_&lt;appname >. azurewebsites.net_.</span><span class="sxs-lookup"><span data-stu-id="808fd-118">hello TXT record maps from _awverify.&lt;subdomain>_ too_&lt;appname>.azurewebsites.net_.</span></span> 

<span data-ttu-id="808fd-119">Hello record TXT, è necessario dipende dal record DNS che si desidera toomigrate hello.</span><span class="sxs-lookup"><span data-stu-id="808fd-119">hello TXT record you need depends on hello DNS record you want toomigrate.</span></span> <span data-ttu-id="808fd-120">Per esempi, vedere hello nella tabella seguente (`@` in genere rappresenta hello dominio principale):</span><span class="sxs-lookup"><span data-stu-id="808fd-120">For examples, see hello following table (`@` typically represents hello root domain):</span></span>  

| <span data-ttu-id="808fd-121">Esempio di record DNS</span><span class="sxs-lookup"><span data-stu-id="808fd-121">DNS record example</span></span> | <span data-ttu-id="808fd-122">Host TXT</span><span class="sxs-lookup"><span data-stu-id="808fd-122">TXT Host</span></span> | <span data-ttu-id="808fd-123">Valore TXT</span><span class="sxs-lookup"><span data-stu-id="808fd-123">TXT Value</span></span> |
| - | - | - |
| <span data-ttu-id="808fd-124">@ (radice)</span><span class="sxs-lookup"><span data-stu-id="808fd-124">@ (root)</span></span> | <span data-ttu-id="808fd-125">_awverify_</span><span class="sxs-lookup"><span data-stu-id="808fd-125">_awverify_</span></span> | <span data-ttu-id="808fd-126">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="808fd-126">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="808fd-127">www (sottodominio)</span><span class="sxs-lookup"><span data-stu-id="808fd-127">www (sub)</span></span> | <span data-ttu-id="808fd-128">_awverify.www_</span><span class="sxs-lookup"><span data-stu-id="808fd-128">_awverify.www_</span></span> | <span data-ttu-id="808fd-129">_&lt;appname&gt;.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="808fd-129">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="808fd-130">\* (wildcard)</span><span class="sxs-lookup"><span data-stu-id="808fd-130">\* (wildcard)</span></span> | <span data-ttu-id="808fd-131">_awverify.\*_</span><span class="sxs-lookup"><span data-stu-id="808fd-131">_awverify.\*_</span></span> | <span data-ttu-id="808fd-132">_&lt;appname&gt;.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="808fd-132">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="808fd-133">Nella pagina di record DNS, tipo di record di hello del nome DNS desiderato toomigrate hello nota.</span><span class="sxs-lookup"><span data-stu-id="808fd-133">In your DNS records page, note hello record type of hello DNS name you want toomigrate.</span></span> <span data-ttu-id="808fd-134">Il servizio app supporta i mapping da record CNAME e A.</span><span class="sxs-lookup"><span data-stu-id="808fd-134">App Service supports mappings from CNAME and A records.</span></span>

### <a name="enable-hello-domain-for-your-app"></a><span data-ttu-id="808fd-135">Abilitare hello dominio per l'app</span><span class="sxs-lookup"><span data-stu-id="808fd-135">Enable hello domain for your app</span></span>

<span data-ttu-id="808fd-136">In hello [portale di Azure](https://portal.azure.com)in hello spostamento a sinistra della pagina app hello, selezionare **i domini personalizzati**.</span><span class="sxs-lookup"><span data-stu-id="808fd-136">In hello [Azure portal](https://portal.azure.com), in hello left navigation of hello app page, select **Custom domains**.</span></span> 

![Menu del dominio personalizzato](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="808fd-138">In hello **i domini personalizzati** pagina, seleziona hello  **+**  icona Avanti troppo**aggiungere hostname**.</span><span class="sxs-lookup"><span data-stu-id="808fd-138">In hello **Custom domains** page, select hello **+** icon next too**Add hostname**.</span></span>

![Aggiunta del nome host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="808fd-140">Nome dominio completo del tipo hello aggiunti record TXT hello, ad esempio `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="808fd-140">Type hello fully qualified domain name that you added hello TXT record for, such as `www.contoso.com`.</span></span> <span data-ttu-id="808fd-141">Per un dominio con caratteri jolly (ad esempio \*. contoso.com), è possibile utilizzare qualsiasi nome DNS al dominio con caratteri jolly hello.</span><span class="sxs-lookup"><span data-stu-id="808fd-141">For a wildcard domain (like \*.contoso.com), you can use any DNS name that matches hello wildcard domain.</span></span> 

<span data-ttu-id="808fd-142">Selezionare **Convalida**.</span><span class="sxs-lookup"><span data-stu-id="808fd-142">Select **Validate**.</span></span>

<span data-ttu-id="808fd-143">Hello **aggiungere hostname** pulsante è attivato.</span><span class="sxs-lookup"><span data-stu-id="808fd-143">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="808fd-144">Assicurarsi che **tipo di record Hostname** è di tipo di record DNS toohello desiderato toomigrate impostato.</span><span class="sxs-lookup"><span data-stu-id="808fd-144">Make sure that **Hostname record type** is set toohello DNS record type you want toomigrate.</span></span>

<span data-ttu-id="808fd-145">Selezionare **Aggiungi il nome host**.</span><span class="sxs-lookup"><span data-stu-id="808fd-145">Select **Add hostname**.</span></span>

![Aggiungere app toohello di nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="808fd-147">Potrebbe richiedere del tempo hello nuovo nome host toobe riportate nella finestra dell'applicazione hello **i domini personalizzati** pagina.</span><span class="sxs-lookup"><span data-stu-id="808fd-147">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="808fd-148">Provare ad aggiornare dati hello tooupdate di hello del browser.</span><span class="sxs-lookup"><span data-stu-id="808fd-148">Try refreshing hello browser tooupdate hello data.</span></span>

![Record CNAME aggiunto](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="808fd-150">Il dominio DNS personalizzato è ora abilitato nell'app Azure.</span><span class="sxs-lookup"><span data-stu-id="808fd-150">Your custom DNS name is now enabled in your Azure app.</span></span> 

## <a name="remap-hello-active-dns-name"></a><span data-ttu-id="808fd-151">Modificare il nome DNS active hello mapping</span><span class="sxs-lookup"><span data-stu-id="808fd-151">Remap hello active DNS name</span></span>

<span data-ttu-id="808fd-152">Hello solo toodo a sinistra di cosa è mapping l'active tooApp di toopoint record DNS del servizio.</span><span class="sxs-lookup"><span data-stu-id="808fd-152">hello only thing left toodo is remapping your active DNS record toopoint tooApp Service.</span></span> <span data-ttu-id="808fd-153">Destra a questo punto, fa ancora riferimento tooyour vecchio sito.</span><span class="sxs-lookup"><span data-stu-id="808fd-153">Right now, it still points tooyour old site.</span></span>

<a name="info"></a>

### <a name="copy-hello-apps-ip-address-a-record-only"></a><span data-ttu-id="808fd-154">Copiare l'indirizzo IP dell'applicazione hello (solo un record)</span><span class="sxs-lookup"><span data-stu-id="808fd-154">Copy hello app's IP address (A record only)</span></span>

<span data-ttu-id="808fd-155">Se si vuole modificare il mapping di un record CNAME, ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="808fd-155">If you are remapping a CNAME record, skip this section.</span></span> 

<span data-ttu-id="808fd-156">tooremap un record, è necessario indirizzo IP esterno dell'applicazione di servizio App hello, come illustrato nella hello **i domini personalizzati** pagina.</span><span class="sxs-lookup"><span data-stu-id="808fd-156">tooremap an A record, you need hello App Service app's external IP address, which is shown in hello **Custom domains** page.</span></span>

<span data-ttu-id="808fd-157">Chiude hello **aggiungere hostname** selezionando **X** nell'angolo superiore destro di hello.</span><span class="sxs-lookup"><span data-stu-id="808fd-157">Close hello **Add hostname** page by selecting **X** in hello upper-right corner.</span></span> 

<span data-ttu-id="808fd-158">In hello **i domini personalizzati** copiare l'indirizzo IP dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="808fd-158">In hello **Custom domains** page, copy hello app's IP address.</span></span>

![Spostamento del portale tooAzure app](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-hello-dns-record"></a><span data-ttu-id="808fd-160">Aggiornamento del record DNS hello</span><span class="sxs-lookup"><span data-stu-id="808fd-160">Update hello DNS record</span></span>

<span data-ttu-id="808fd-161">Nella pagina di record DNS hello del provider di dominio, selezionare hello tooremap di record DNS.</span><span class="sxs-lookup"><span data-stu-id="808fd-161">Back in hello DNS records page of your domain provider, select hello DNS record tooremap.</span></span>

<span data-ttu-id="808fd-162">Per hello `contoso.com` esempio dominio radice, modificare i record A o CNAME hello, come negli esempi di hello hello nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="808fd-162">For hello `contoso.com` root domain example, remap hello A or CNAME record like hello examples in hello following table:</span></span> 

| <span data-ttu-id="808fd-163">Esempio di FQDN</span><span class="sxs-lookup"><span data-stu-id="808fd-163">FQDN example</span></span> | <span data-ttu-id="808fd-164">Tipo di record</span><span class="sxs-lookup"><span data-stu-id="808fd-164">Record type</span></span> | <span data-ttu-id="808fd-165">Host</span><span class="sxs-lookup"><span data-stu-id="808fd-165">Host</span></span> | <span data-ttu-id="808fd-166">Valore</span><span class="sxs-lookup"><span data-stu-id="808fd-166">Value</span></span> |
| - | - | - | - |
| <span data-ttu-id="808fd-167">contoso.com (radice)</span><span class="sxs-lookup"><span data-stu-id="808fd-167">contoso.com (root)</span></span> | <span data-ttu-id="808fd-168">Una </span><span class="sxs-lookup"><span data-stu-id="808fd-168">A</span></span> | `@` | <span data-ttu-id="808fd-169">Indirizzo IP da [indirizzo IP dell'applicazione hello copia](#info)</span><span class="sxs-lookup"><span data-stu-id="808fd-169">IP address from [Copy hello app's IP address](#info)</span></span> |
| <span data-ttu-id="808fd-170">www.contoso.com (sottodominio)</span><span class="sxs-lookup"><span data-stu-id="808fd-170">www.contoso.com (sub)</span></span> | <span data-ttu-id="808fd-171">CNAME</span><span class="sxs-lookup"><span data-stu-id="808fd-171">CNAME</span></span> | `www` | <span data-ttu-id="808fd-172">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="808fd-172">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="808fd-173">\*.contoso.com (carattere jolly)</span><span class="sxs-lookup"><span data-stu-id="808fd-173">\*.contoso.com (wildcard)</span></span> | <span data-ttu-id="808fd-174">CNAME</span><span class="sxs-lookup"><span data-stu-id="808fd-174">CNAME</span></span> | _\*_ | <span data-ttu-id="808fd-175">_&lt;appname&gt;.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="808fd-175">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="808fd-176">Salvare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="808fd-176">Save your settings.</span></span>

<span data-ttu-id="808fd-177">Query DNS devono iniziare a risolvere tooyour app del servizio App immediatamente dopo l'operazione di propagazione DNS.</span><span class="sxs-lookup"><span data-stu-id="808fd-177">DNS queries should start resolving tooyour App Service app immediately after DNS propagation happens.</span></span>

## <a name="next-steps"></a><span data-ttu-id="808fd-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="808fd-178">Next steps</span></span>

<span data-ttu-id="808fd-179">Informazioni su come toobind un SSL personalizzato certificato tooApp servizio.</span><span class="sxs-lookup"><span data-stu-id="808fd-179">Learn how toobind a custom SSL certificate tooApp Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="808fd-180">Associare un esistente personalizzato SSL certificato tooAzure App Web</span><span class="sxs-lookup"><span data-stu-id="808fd-180">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
