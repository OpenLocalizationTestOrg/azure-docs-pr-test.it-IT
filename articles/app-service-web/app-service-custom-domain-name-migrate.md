---
title: Eseguire la migrazione di un nome DNS attivo al Servizio app di Azure | Microsoft Docs
description: "Informazioni su come eseguire la migrazione di un nome di dominio DNS personalizzato già assegnato a un sito live al Servizio app di Azure senza tempi di inattività."
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
ms.openlocfilehash: 89308c1c684a639950467b72d26703cc07c50c14
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-an-active-dns-name-to-azure-app-service"></a><span data-ttu-id="71509-103">Eseguire la migrazione di un nome DNS attivo al Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="71509-103">Migrate an active DNS name to Azure App Service</span></span>

<span data-ttu-id="71509-104">Questo articolo descrive come eseguire la migrazione di un nome DNS attivo al [Servizio app di Azure](../app-service/app-service-value-prop-what-is.md) senza tempi di inattività.</span><span class="sxs-lookup"><span data-stu-id="71509-104">This article shows you how to migrate an active DNS name to [Azure App Service](../app-service/app-service-value-prop-what-is.md) without any downtime.</span></span>

<span data-ttu-id="71509-105">Quando si esegue la migrazione di un sito live e del relativo nome di dominio DNS al Servizio app di Azure, tale nome DNS è già usato dal traffico live.</span><span class="sxs-lookup"><span data-stu-id="71509-105">When you migrate a live site and its DNS domain name to App Service, that DNS name is already serving live traffic.</span></span> <span data-ttu-id="71509-106">È possibile evitare tempi di inattività nella risoluzione DNS durante la migrazione associando preventivamente il nome DNS attivo al Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="71509-106">You can avoid downtime in DNS resolution during the migration by binding the active DNS name to your App Service app preemptively.</span></span>

<span data-ttu-id="71509-107">Se i tempi di inattività non rappresentano un problema nella risoluzione DNS, vedere [Eseguire il mapping di un nome DNS personalizzato esistente alle app Web di Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="71509-107">If you're not worried about downtime in DNS resolution, see [Map an existing custom DNS name to Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71509-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="71509-108">Prerequisites</span></span>

<span data-ttu-id="71509-109">Per completare questa procedura:</span><span class="sxs-lookup"><span data-stu-id="71509-109">To complete this how-to:</span></span>

- <span data-ttu-id="71509-110">[Verificare che l'app del servizio app non sia inclusa nel livello GRATUITO](app-service-web-tutorial-custom-domain.md#checkpricing).</span><span class="sxs-lookup"><span data-stu-id="71509-110">[Make sure that your App Service app is not in FREE tier](app-service-web-tutorial-custom-domain.md#checkpricing).</span></span>

## <a name="bind-the-domain-name-preemptively"></a><span data-ttu-id="71509-111">Associare preventivamente il nome del dominio</span><span class="sxs-lookup"><span data-stu-id="71509-111">Bind the domain name preemptively</span></span>

<span data-ttu-id="71509-112">Quando si associa preventivamente un dominio personalizzato, è necessario eseguire entrambe le operazioni seguenti prima di apportare modifiche ai record DNS:</span><span class="sxs-lookup"><span data-stu-id="71509-112">When you bind a custom domain preemptively, you accomplish both of the following before making any changes to your DNS records:</span></span>

- <span data-ttu-id="71509-113">Verificare la proprietà del dominio</span><span class="sxs-lookup"><span data-stu-id="71509-113">Verify domain ownership</span></span>
- <span data-ttu-id="71509-114">Abilitare il nome di dominio per l'app</span><span class="sxs-lookup"><span data-stu-id="71509-114">Enable the domain name for your app</span></span>

<span data-ttu-id="71509-115">Dopo aver eseguito la migrazione del nome DNS personalizzato dal sito precedente all'app del servizio app, non si verificheranno più tempi di inattività nella risoluzione DNS.</span><span class="sxs-lookup"><span data-stu-id="71509-115">When you finally migrate your custom DNS name from the old site to the App Service app, there will be no downtime in DNS resolution.</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a><span data-ttu-id="71509-116">Creare un record di verifica del dominio</span><span class="sxs-lookup"><span data-stu-id="71509-116">Create domain verification record</span></span>

<span data-ttu-id="71509-117">Per verificare la proprietà del dominio, aggiungere un record TXT.</span><span class="sxs-lookup"><span data-stu-id="71509-117">To verify domain ownership, Add a TXT record.</span></span> <span data-ttu-id="71509-118">Il record TXT esegue il mapping da _awverify.&lt;subdomain>_ a _&lt;appname>.azurewebsites.net_.</span><span class="sxs-lookup"><span data-stu-id="71509-118">The TXT record maps from _awverify.&lt;subdomain>_ to _&lt;appname>.azurewebsites.net_.</span></span> 

<span data-ttu-id="71509-119">Il record TXT necessario varia a seconda del record DNS di cui si vuole eseguire la migrazione.</span><span class="sxs-lookup"><span data-stu-id="71509-119">The TXT record you need depends on the DNS record you want to migrate.</span></span> <span data-ttu-id="71509-120">Ad esempio, vedere la tabella seguente (`@` rappresenta in genere il dominio radice):</span><span class="sxs-lookup"><span data-stu-id="71509-120">For examples, see the following table (`@` typically represents the root domain):</span></span>  

| <span data-ttu-id="71509-121">Esempio di record DNS</span><span class="sxs-lookup"><span data-stu-id="71509-121">DNS record example</span></span> | <span data-ttu-id="71509-122">Host TXT</span><span class="sxs-lookup"><span data-stu-id="71509-122">TXT Host</span></span> | <span data-ttu-id="71509-123">Valore TXT</span><span class="sxs-lookup"><span data-stu-id="71509-123">TXT Value</span></span> |
| - | - | - |
| <span data-ttu-id="71509-124">@ (radice)</span><span class="sxs-lookup"><span data-stu-id="71509-124">@ (root)</span></span> | <span data-ttu-id="71509-125">_awverify_</span><span class="sxs-lookup"><span data-stu-id="71509-125">_awverify_</span></span> | <span data-ttu-id="71509-126">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="71509-126">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="71509-127">www (sottodominio)</span><span class="sxs-lookup"><span data-stu-id="71509-127">www (sub)</span></span> | <span data-ttu-id="71509-128">_awverify.www_</span><span class="sxs-lookup"><span data-stu-id="71509-128">_awverify.www_</span></span> | <span data-ttu-id="71509-129">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="71509-129">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="71509-130">\* (wildcard)</span><span class="sxs-lookup"><span data-stu-id="71509-130">\* (wildcard)</span></span> | <span data-ttu-id="71509-131">_awverify.\*_</span><span class="sxs-lookup"><span data-stu-id="71509-131">_awverify.\*_</span></span> | <span data-ttu-id="71509-132">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="71509-132">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="71509-133">Nella pagina dei record DNS prendere nota del tipo di record del nome DNS di cui si vuole eseguire la migrazione.</span><span class="sxs-lookup"><span data-stu-id="71509-133">In your DNS records page, note the record type of the DNS name you want to migrate.</span></span> <span data-ttu-id="71509-134">Il servizio app supporta i mapping da record CNAME e A.</span><span class="sxs-lookup"><span data-stu-id="71509-134">App Service supports mappings from CNAME and A records.</span></span>

### <a name="enable-the-domain-for-your-app"></a><span data-ttu-id="71509-135">Abilitare il dominio per l'app</span><span class="sxs-lookup"><span data-stu-id="71509-135">Enable the domain for your app</span></span>

<span data-ttu-id="71509-136">Nel riquadro di spostamento a sinistra della pagina dell'app nel [portale di Azure](https://portal.azure.com) selezionare **Domini personalizzati**.</span><span class="sxs-lookup"><span data-stu-id="71509-136">In the [Azure portal](https://portal.azure.com), in the left navigation of the app page, select **Custom domains**.</span></span> 

![Menu del dominio personalizzato](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="71509-138">Nella pagina **Domini personalizzati** selezionare l'icona **+** accanto ad **Aggiungi il nome host**.</span><span class="sxs-lookup"><span data-stu-id="71509-138">In the **Custom domains** page, select the **+** icon next to **Add hostname**.</span></span>

![Aggiunta del nome host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="71509-140">Digitare il nome di dominio completo al quale è stato aggiunto un record TXT, ad esempio `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="71509-140">Type the fully qualified domain name that you added the TXT record for, such as `www.contoso.com`.</span></span> <span data-ttu-id="71509-141">Per un dominio con caratteri jolly (ad esempio \*. contoso.com), è possibile usare un nome DNS qualsiasi che corrisponda al dominio con caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="71509-141">For a wildcard domain (like \*.contoso.com), you can use any DNS name that matches the wildcard domain.</span></span> 

<span data-ttu-id="71509-142">Selezionare **Convalida**.</span><span class="sxs-lookup"><span data-stu-id="71509-142">Select **Validate**.</span></span>

<span data-ttu-id="71509-143">Viene attivato il pulsante **Aggiungi il nome host**.</span><span class="sxs-lookup"><span data-stu-id="71509-143">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="71509-144">Assicurarsi che **Tipo di record del nome host** sia impostato sul tipo di record DNS di cui si vuole eseguire la migrazione.</span><span class="sxs-lookup"><span data-stu-id="71509-144">Make sure that **Hostname record type** is set to the DNS record type you want to migrate.</span></span>

<span data-ttu-id="71509-145">Selezionare **Aggiungi il nome host**.</span><span class="sxs-lookup"><span data-stu-id="71509-145">Select **Add hostname**.</span></span>

![Aggiunta del nome DNS all'app](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="71509-147">La visualizzazione del nuovo nome host nella pagina **Domini personalizzati** dell'app potrebbe richiedere qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="71509-147">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="71509-148">Provare ad aggiornare il browser per visualizzare i dati più recenti.</span><span class="sxs-lookup"><span data-stu-id="71509-148">Try refreshing the browser to update the data.</span></span>

![Record CNAME aggiunto](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="71509-150">Il dominio DNS personalizzato è ora abilitato nell'app Azure.</span><span class="sxs-lookup"><span data-stu-id="71509-150">Your custom DNS name is now enabled in your Azure app.</span></span> 

## <a name="remap-the-active-dns-name"></a><span data-ttu-id="71509-151">Modificare il mapping del nome DNS attivo</span><span class="sxs-lookup"><span data-stu-id="71509-151">Remap the active DNS name</span></span>

<span data-ttu-id="71509-152">A questo punto resta solo da modificare il mapping del record DNS attivo in modo che faccia riferimento al servizio app.</span><span class="sxs-lookup"><span data-stu-id="71509-152">The only thing left to do is remapping your active DNS record to point to App Service.</span></span> <span data-ttu-id="71509-153">Per il momento si riferisce ancora al sito precedente.</span><span class="sxs-lookup"><span data-stu-id="71509-153">Right now, it still points to your old site.</span></span>

<a name="info"></a>

### <a name="copy-the-apps-ip-address-a-record-only"></a><span data-ttu-id="71509-154">Copiare l'indirizzo IP dell'app (solo record A)</span><span class="sxs-lookup"><span data-stu-id="71509-154">Copy the app's IP address (A record only)</span></span>

<span data-ttu-id="71509-155">Se si vuole modificare il mapping di un record CNAME, ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="71509-155">If you are remapping a CNAME record, skip this section.</span></span> 

<span data-ttu-id="71509-156">Per modificare il mapping di un record A, è necessario l'indirizzo IP esterno dell'app del servizio app, visualizzato nella pagina **Domini personalizzati**.</span><span class="sxs-lookup"><span data-stu-id="71509-156">To remap an A record, you need the App Service app's external IP address, which is shown in the **Custom domains** page.</span></span>

<span data-ttu-id="71509-157">Chiudere la pagina **Aggiungi il nome host** selezionando **X** nell'angolo in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="71509-157">Close the **Add hostname** page by selecting **X** in the upper-right corner.</span></span> 

<span data-ttu-id="71509-158">Nella pagina **Domini personalizzati**, copiare l'indirizzo IP dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="71509-158">In the **Custom domains** page, copy the app's IP address.</span></span>

![Passaggio all'app di Azure nel portale](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-the-dns-record"></a><span data-ttu-id="71509-160">Aggiornare il record DNS</span><span class="sxs-lookup"><span data-stu-id="71509-160">Update the DNS record</span></span>

<span data-ttu-id="71509-161">Tornare alla pagina dei record DNS del provider di dominio e selezionare il record DNS per il quale si vuole modificare il mapping.</span><span class="sxs-lookup"><span data-stu-id="71509-161">Back in the DNS records page of your domain provider, select the DNS record to remap.</span></span>

<span data-ttu-id="71509-162">Per l'esempio di dominio radice `contoso.com`, modificare il mapping del record A o CNAME come negli esempi illustrati nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="71509-162">For the `contoso.com` root domain example, remap the A or CNAME record like the examples in the following table:</span></span> 

| <span data-ttu-id="71509-163">Esempio di FQDN</span><span class="sxs-lookup"><span data-stu-id="71509-163">FQDN example</span></span> | <span data-ttu-id="71509-164">Tipo di record</span><span class="sxs-lookup"><span data-stu-id="71509-164">Record type</span></span> | <span data-ttu-id="71509-165">Host</span><span class="sxs-lookup"><span data-stu-id="71509-165">Host</span></span> | <span data-ttu-id="71509-166">Valore</span><span class="sxs-lookup"><span data-stu-id="71509-166">Value</span></span> |
| - | - | - | - |
| <span data-ttu-id="71509-167">contoso.com (radice)</span><span class="sxs-lookup"><span data-stu-id="71509-167">contoso.com (root)</span></span> | <span data-ttu-id="71509-168">Una </span><span class="sxs-lookup"><span data-stu-id="71509-168">A</span></span> | `@` | <span data-ttu-id="71509-169">Indirizzo IP ricavato da [Copiare l'indirizzo IP dell'app](#info)</span><span class="sxs-lookup"><span data-stu-id="71509-169">IP address from [Copy the app's IP address](#info)</span></span> |
| <span data-ttu-id="71509-170">www.contoso.com (sottodominio)</span><span class="sxs-lookup"><span data-stu-id="71509-170">www.contoso.com (sub)</span></span> | <span data-ttu-id="71509-171">CNAME</span><span class="sxs-lookup"><span data-stu-id="71509-171">CNAME</span></span> | `www` | <span data-ttu-id="71509-172">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="71509-172">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="71509-173">\*.contoso.com (carattere jolly)</span><span class="sxs-lookup"><span data-stu-id="71509-173">\*.contoso.com (wildcard)</span></span> | <span data-ttu-id="71509-174">CNAME</span><span class="sxs-lookup"><span data-stu-id="71509-174">CNAME</span></span> | _\*_ | <span data-ttu-id="71509-175">_&lt;appname>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="71509-175">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="71509-176">Salvare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="71509-176">Save your settings.</span></span>

<span data-ttu-id="71509-177">Le query DNS inizieranno a risolversi nell'app del servizio app immediatamente dopo la propagazione DNS.</span><span class="sxs-lookup"><span data-stu-id="71509-177">DNS queries should start resolving to your App Service app immediately after DNS propagation happens.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71509-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="71509-178">Next steps</span></span>

<span data-ttu-id="71509-179">Informazioni su come associare un certificato SSL personalizzato al servizio app.</span><span class="sxs-lookup"><span data-stu-id="71509-179">Learn how to bind a custom SSL certificate to App Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="71509-180">Associare un certificato SSL personalizzato esistente ad app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="71509-180">Bind an existing custom SSL certificate to Azure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
