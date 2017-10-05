---
title: "Esecuzione del mapping di un nome DNS personalizzato esistente con un’app Web di Azure | Microsoft Docs"
description: Informazioni su come aggiungere un nome di dominio DNS personalizzato esistente, ad esempio il dominio personale, in un'app Web, nel back-end dell'app per dispositivi mobili o nell'app per le API del servizio app di Azure.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 973cda462e8d258cc848e1036891c7f8af043102
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="map-an-existing-custom-dns-name-to-azure-web-apps"></a><span data-ttu-id="e19f6-103">Esecuzione del mapping di un nome DNS personalizzato esistente con un app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="e19f6-103">Map an existing custom DNS name to Azure Web Apps</span></span>

<span data-ttu-id="e19f6-104">Le [app Web di Azure](app-service-web-overview.md) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="e19f6-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="e19f6-105">Questa esercitazione illustra come eseguire il mapping di un nome DNS personalizzato esistente alle app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="e19f6-105">This tutorial shows you how to map an existing custom DNS name to Azure Web Apps.</span></span>

![Passaggio all'app di Azure nel portale](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

<span data-ttu-id="e19f6-107">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="e19f6-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e19f6-108">Eseguire il mapping di un sottodominio (ad esempio, `www.contoso.com`) usando un record CNAME</span><span class="sxs-lookup"><span data-stu-id="e19f6-108">Map a subdomain (for example, `www.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="e19f6-109">Eseguire il mapping di un dominio radice (ad esempio, `contoso.com`) usando un record A</span><span class="sxs-lookup"><span data-stu-id="e19f6-109">Map a root domain (for example, `contoso.com`) by using an A record</span></span>
> * <span data-ttu-id="e19f6-110">Eseguire il mapping di un dominio con caratteri jolly (ad esempio, `*.contoso.com`) usando un record CNAME</span><span class="sxs-lookup"><span data-stu-id="e19f6-110">Map a wildcard domain (for example, `*.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="e19f6-111">Automatizzare il mapping dei domini con script</span><span class="sxs-lookup"><span data-stu-id="e19f6-111">Automate domain mapping with scripts</span></span>

<span data-ttu-id="e19f6-112">È possibile utilizzare un **record CNAME** o un **record A** per eseguire il mapping di un nome DNS personalizzato con un servizio app.</span><span class="sxs-lookup"><span data-stu-id="e19f6-112">You can use either a **CNAME record** or an **A record** to map a custom DNS name to App Service.</span></span> 

> [!NOTE]
> <span data-ttu-id="e19f6-113">È consigliabile usare un record CNAME per tutti i nomi DNS personalizzati tranne il dominio radice (ad esempio, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="e19f6-113">We recommend that you use a CNAME for all custom DNS names except a root domain (for example, `contoso.com`).</span></span>

<span data-ttu-id="e19f6-114">Per eseguire la migrazione di un sito in tempo reale e del relativo nome di dominio DNS al servizio app, vedere [Migrare un nome DNS attivo nel servizio app di Azure](app-service-custom-domain-name-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="e19f6-114">To migrate a live site and its DNS domain name to App Service, see [Migrate an active DNS name to Azure App Service](app-service-custom-domain-name-migrate.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e19f6-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e19f6-115">Prerequisites</span></span>

<span data-ttu-id="e19f6-116">Per completare questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="e19f6-116">To complete this tutorial:</span></span>

* <span data-ttu-id="e19f6-117">[Creare un'app del servizio app](/azure/app-service/) oppure usare un'app creata per un'altra esercitazione.</span><span class="sxs-lookup"><span data-stu-id="e19f6-117">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>
* <span data-ttu-id="e19f6-118">Acquistare un nome di dominio e assicurarsi di avere accesso al registro DNS per il provider del dominio, ad esempio GoDaddy.</span><span class="sxs-lookup"><span data-stu-id="e19f6-118">Purchase a domain name and make sure you have access to the DNS registry for your domain provider (such as GoDaddy).</span></span>

  <span data-ttu-id="e19f6-119">Ad esempio, per aggiungere le voci DNS per `contoso.com` e `www.contoso.com` è necessario essere autorizzati a configurare le impostazioni DNS per il dominio radice `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="e19f6-119">For example, to add DNS entries for `contoso.com` and `www.contoso.com`, you must be able to configure the DNS settings for the `contoso.com` root domain.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e19f6-120">Se non è disponibile un nome di dominio esistente, può essere utile [acquistare un dominio tramite il portale di Azure](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="e19f6-120">If you don't have an existing domain name, consider [purchasing a domain using the Azure portal](custom-dns-web-site-buydomains-web-app.md).</span></span> 

## <a name="prepare-the-app"></a><span data-ttu-id="e19f6-121">Preparare l'app</span><span class="sxs-lookup"><span data-stu-id="e19f6-121">Prepare the app</span></span>

<span data-ttu-id="e19f6-122">Per eseguire il mapping di un nome DNS personalizzato a un'app Web, è necessario che il [piano di servizio app](https://azure.microsoft.com/pricing/details/app-service/) dell'app Web sia un livello a pagamento (**Condiviso**, **Base**, **Standard** o **Premium**).</span><span class="sxs-lookup"><span data-stu-id="e19f6-122">To map a custom DNS name to a web app, the web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="e19f6-123">In questo passaggio si verifica che l'app del servizio app si trovi nel piano tariffario supportato.</span><span class="sxs-lookup"><span data-stu-id="e19f6-123">In this step, you make sure that the App Service app is in the supported pricing tier.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="e19f6-124">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="e19f6-124">Sign in to Azure</span></span>

<span data-ttu-id="e19f6-125">Aprire il [portale di Azure](https://portal.azure.com) e accedere con l'account Azure.</span><span class="sxs-lookup"><span data-stu-id="e19f6-125">Open the [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-to-the-app-in-the-azure-portal"></a><span data-ttu-id="e19f6-126">Passare all'app nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e19f6-126">Navigate to the app in the Azure portal</span></span>

<span data-ttu-id="e19f6-127">Dal menu a sinistra selezionare **Servizi app** e quindi selezionare il nome dell'app.</span><span class="sxs-lookup"><span data-stu-id="e19f6-127">From the left menu, select **App Services**, and then select the name of the app.</span></span>

![Passaggio all'app di Azure nel portale](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="e19f6-129">Viene visualizzata la pagina di gestione dell'app del servizio app.</span><span class="sxs-lookup"><span data-stu-id="e19f6-129">You see the management page of the App Service app.</span></span>  

<a name="checkpricing"></a>

### <a name="check-the-pricing-tier"></a><span data-ttu-id="e19f6-130">Scegliere il piano tariffario</span><span class="sxs-lookup"><span data-stu-id="e19f6-130">Check the pricing tier</span></span>

<span data-ttu-id="e19f6-131">Nel riquadro di spostamento a sinistra della pagina dell'app scorrere fino alla sezione **Impostazioni** e selezionare **Scala verticalmente (piano di servizio app)**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-131">In the left navigation of the app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menu di scalabilità verticale](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="e19f6-133">Il livello corrente dell'app è evidenziato da un bordo blu.</span><span class="sxs-lookup"><span data-stu-id="e19f6-133">The app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="e19f6-134">Verificare che l'app non sia inclusa nel livello **Gratuito**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-134">Check to make sure that the app is not in the **Free** tier.</span></span> <span data-ttu-id="e19f6-135">Il DNS personalizzato non è supportato nel livello **Gratuito**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-135">Custom DNS is not supported in the **Free** tier.</span></span> 

![Controllare il piano tariffario](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="e19f6-137">Se il piano del servizio app non è **Gratuito**, chiudere la pagina **Scegli il piano tariffario** e passare a [Esecuzione del mapping di un record CNAME](#cname).</span><span class="sxs-lookup"><span data-stu-id="e19f6-137">If the App Service plan is not **Free**, close the **Choose your pricing tier** page and skip to [Map a CNAME record](#cname).</span></span>

<a name="scaleup"></a>

### <a name="scale-up-the-app-service-plan"></a><span data-ttu-id="e19f6-138">Passare a un piano di servizio app di livello superiore</span><span class="sxs-lookup"><span data-stu-id="e19f6-138">Scale up the App Service plan</span></span>

<span data-ttu-id="e19f6-139">Selezionare uno dei livelli non gratuiti (**Condiviso**, **Base**, **Standard** o **Premium**).</span><span class="sxs-lookup"><span data-stu-id="e19f6-139">Select any of the non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="e19f6-140">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-140">Click **Select**.</span></span>

![Controllare il piano tariffario](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="e19f6-142">La visualizzazione della notifica seguente indica che l'operazione di passaggio al livello superiore è stata completata.</span><span class="sxs-lookup"><span data-stu-id="e19f6-142">When you see the following notification, the scale operation is complete.</span></span>

![Conferma operazione di scalabilità](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a><span data-ttu-id="e19f6-144">Esecuzione del mapping di un record CNAME</span><span class="sxs-lookup"><span data-stu-id="e19f6-144">Map a CNAME record</span></span>

<span data-ttu-id="e19f6-145">nell'esempio dell'esercitazione si aggiunge un record CNAME per il sottodominio `www`, ad esempio `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="e19f6-145">In the tutorial example, you add a CNAME record for the `www` subdomain (for example, `www.contoso.com`).</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-cname-record"></a><span data-ttu-id="e19f6-146">Creazione di un record CNAME</span><span class="sxs-lookup"><span data-stu-id="e19f6-146">Create the CNAME record</span></span>

<span data-ttu-id="e19f6-147">Aggiungere un record CNAME per eseguire il mapping di un sottodominio al nome host predefinito dell'app (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="e19f6-147">Add a CNAME record to map a subdomain to the app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="e19f6-148">Per l'esempio di dominio `www.contoso.com`, aggiungere un record CNAME che esegue il mapping del nome `www` a `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="e19f6-148">For the `www.contoso.com` domain example, add a CNAME record that maps the name `www` to `<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="e19f6-149">Dopo aver aggiunto il record CNAME, la pagina dei record DNS è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e19f6-149">After you add the CNAME, the DNS records page looks like the following example:</span></span>

![Passaggio all'app di Azure nel portale](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-the-cname-record-mapping-in-azure"></a><span data-ttu-id="e19f6-151">Abilitare il mapping dei record CNAME in Azure</span><span class="sxs-lookup"><span data-stu-id="e19f6-151">Enable the CNAME record mapping in Azure</span></span>

<span data-ttu-id="e19f6-152">Nel riquadro di spostamento a sinistra della pagina dell'app nel portale di Azure selezionare **Domini personalizzati**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-152">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Menu del dominio personalizzato](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="e19f6-154">Nella pagina **Domini personalizzati** dell'app aggiungere il nome DNS personalizzato completo (`www.contoso.com`) all'elenco.</span><span class="sxs-lookup"><span data-stu-id="e19f6-154">In the **Custom domains** page of the app, add the fully qualified custom DNS name (`www.contoso.com`) to the list.</span></span>

<span data-ttu-id="e19f6-155">Selezionare l'icona **+** accanto ad **Aggiungi il nome host**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-155">Select the **+** icon next to **Add hostname**.</span></span>

![Aggiunta del nome host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="e19f6-157">Digitare il nome di dominio completo per il quale è stato aggiunto un record CNAME, ad esempio `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="e19f6-157">Type the fully qualified domain name that you added a CNAME record for, such as `www.contoso.com`.</span></span> 

<span data-ttu-id="e19f6-158">Selezionare **Convalida**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-158">Select **Validate**.</span></span>

<span data-ttu-id="e19f6-159">Viene attivato il pulsante **Aggiungi il nome host**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-159">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="e19f6-160">Assicurarsi che **Tipo di record del nome host** sia impostato su **CNAME (www.example.com o qualsiasi sottodominio)**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-160">Make sure that **Hostname record type** is set to **CNAME (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="e19f6-161">Selezionare **Aggiungi il nome host**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-161">Select **Add hostname**.</span></span>

![Aggiunta del nome DNS all'app](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="e19f6-163">La visualizzazione del nuovo nome host nella pagina **Domini personalizzati** dell'app potrebbe richiedere qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="e19f6-163">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="e19f6-164">Provare ad aggiornare il browser per visualizzare i dati più recenti.</span><span class="sxs-lookup"><span data-stu-id="e19f6-164">Try refreshing the browser to update the data.</span></span>

![Record CNAME aggiunto](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="e19f6-166">Se è stato saltato un passaggio o è stato inserito un errore di digitazione, nella parte inferiore della pagina viene visualizzato un errore di verifica.</span><span class="sxs-lookup"><span data-stu-id="e19f6-166">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span></span>

![Errore di verifica](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a><span data-ttu-id="e19f6-168">Esecuzione del mapping di un record A</span><span class="sxs-lookup"><span data-stu-id="e19f6-168">Map an A record</span></span>

<span data-ttu-id="e19f6-169">Nell'esempio dell'esercitazione si aggiunge un record A per il dominio radice, ad esempio `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="e19f6-169">In the tutorial example, you add an A record for the root domain (for example, `contoso.com`).</span></span> 

<a name="info"></a>

### <a name="copy-the-apps-ip-address"></a><span data-ttu-id="e19f6-170">Copiare l'indirizzo IP dell'app</span><span class="sxs-lookup"><span data-stu-id="e19f6-170">Copy the app's IP address</span></span>

<span data-ttu-id="e19f6-171">Per eseguire il mapping di un record A, è necessario l'indirizzo IP esterno dell'app.</span><span class="sxs-lookup"><span data-stu-id="e19f6-171">To map an A record, you need the app's external IP address.</span></span> <span data-ttu-id="e19f6-172">È possibile trovare questo indirizzo IP nella pagina **Domini personalizzati** dell'app nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e19f6-172">You can find this IP address in the app's **Custom domains** page in the Azure portal.</span></span>

<span data-ttu-id="e19f6-173">Nel riquadro di spostamento a sinistra della pagina dell'app nel portale di Azure selezionare **Domini personalizzati**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-173">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Menu del dominio personalizzato](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="e19f6-175">Nella pagina **Domini personalizzati**, copiare l'indirizzo IP dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e19f6-175">In the **Custom domains** page, copy the app's IP address.</span></span>

![Passaggio all'app di Azure nel portale](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-a-record"></a><span data-ttu-id="e19f6-177">Creazione di un record A</span><span class="sxs-lookup"><span data-stu-id="e19f6-177">Create the A record</span></span>

<span data-ttu-id="e19f6-178">Per eseguire il mapping di un record A a un'app, il servizio app richiede **due** record DNS:</span><span class="sxs-lookup"><span data-stu-id="e19f6-178">To map an A record to an app, App Service requires **two** DNS records:</span></span>

- <span data-ttu-id="e19f6-179">Un record **A** di cui eseguire il mapping all'indirizzo IP dell'app.</span><span class="sxs-lookup"><span data-stu-id="e19f6-179">An **A** record to map to the app's IP address.</span></span>
- <span data-ttu-id="e19f6-180">Un record **TXT** di cui eseguire il mapping al nome host predefinito dell'app `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="e19f6-180">A **TXT** record to map to the app's default hostname `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="e19f6-181">Il servizio app usa questo record solo in fase di configurazione per verificare che si è proprietari del dominio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="e19f6-181">App Service uses this record only at configuration time, to verify that you own the custom domain.</span></span> <span data-ttu-id="e19f6-182">Dopo che il dominio personalizzato è stato convalidato e configurato nel servizio app, è possibile eliminare il record TXT.</span><span class="sxs-lookup"><span data-stu-id="e19f6-182">After your custom domain is validated and configured in App Service, you can delete this TXT record.</span></span> 

<span data-ttu-id="e19f6-183">Per l’esempio di dominio `contoso.com`, creare i record A e TXT in base alla tabella seguente (`@` rappresenta in genere il dominio radice).</span><span class="sxs-lookup"><span data-stu-id="e19f6-183">For the `contoso.com` domain example, create the A and TXT records according to the following table (`@` typically represents the root domain).</span></span> 

| <span data-ttu-id="e19f6-184">Tipo di record</span><span class="sxs-lookup"><span data-stu-id="e19f6-184">Record type</span></span> | <span data-ttu-id="e19f6-185">Host</span><span class="sxs-lookup"><span data-stu-id="e19f6-185">Host</span></span> | <span data-ttu-id="e19f6-186">Valore</span><span class="sxs-lookup"><span data-stu-id="e19f6-186">Value</span></span> |
| - | - | - |
| <span data-ttu-id="e19f6-187">Una </span><span class="sxs-lookup"><span data-stu-id="e19f6-187">A</span></span> | `@` | <span data-ttu-id="e19f6-188">Indirizzo IP ricavato da [Copiare l'indirizzo IP dell'app](#info)</span><span class="sxs-lookup"><span data-stu-id="e19f6-188">IP address from [Copy the app's IP address](#info)</span></span> |
| <span data-ttu-id="e19f6-189">TXT</span><span class="sxs-lookup"><span data-stu-id="e19f6-189">TXT</span></span> | `@` | `<app_name>.azurewebsites.net` |

<span data-ttu-id="e19f6-190">Dopo aver aggiunto i record, la pagina dei record DNS è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e19f6-190">When the records are added, the DNS records page looks like the following example:</span></span>

![Pagina dei record DNS](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-the-a-record-mapping-in-the-app"></a><span data-ttu-id="e19f6-192">Abilitare il mapping del record A nell'app</span><span class="sxs-lookup"><span data-stu-id="e19f6-192">Enable the A record mapping in the app</span></span>

<span data-ttu-id="e19f6-193">Nella pagina **Domini personalizzati** dell'app nel portale di Azure aggiungere il nome DNS personalizzato completo, ad esempio `contoso.com`, all'elenco.</span><span class="sxs-lookup"><span data-stu-id="e19f6-193">Back in the app's **Custom domains** page in the Azure portal, add the fully qualified custom DNS name (for example, `contoso.com`) to the list.</span></span>

<span data-ttu-id="e19f6-194">Selezionare l'icona **+** accanto ad **Aggiungi il nome host**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-194">Select the **+** icon next to **Add hostname**.</span></span>

![Aggiunta del nome host](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

<span data-ttu-id="e19f6-196">Digitare il nome di dominio completo per il quale è stato configurato il record A, ad esempio `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="e19f6-196">Type the fully qualified domain name that you configured the A record for, such as `contoso.com`.</span></span>

<span data-ttu-id="e19f6-197">Selezionare **Convalida**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-197">Select **Validate**.</span></span>

<span data-ttu-id="e19f6-198">Viene attivato il pulsante **Aggiungi il nome host**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-198">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="e19f6-199">Assicurarsi che **Tipo di record del nome host** sia impostato su **Record A (esempio.com)**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-199">Make sure that **Hostname record type** is set to **A record (example.com)**.</span></span>

<span data-ttu-id="e19f6-200">Selezionare **Aggiungi il nome host**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-200">Select **Add hostname**.</span></span>

![Aggiunta del nome DNS all'app](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

<span data-ttu-id="e19f6-202">La visualizzazione del nuovo nome host nella pagina **Domini personalizzati** dell'app potrebbe richiedere qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="e19f6-202">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="e19f6-203">Provare ad aggiornare il browser per visualizzare i dati più recenti.</span><span class="sxs-lookup"><span data-stu-id="e19f6-203">Try refreshing the browser to update the data.</span></span>

![Record A aggiunto](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

<span data-ttu-id="e19f6-205">Se è stato saltato un passaggio o è stato inserito un errore di digitazione, nella parte inferiore della pagina viene visualizzato un errore di verifica.</span><span class="sxs-lookup"><span data-stu-id="e19f6-205">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span></span>

![Errore di verifica](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a><span data-ttu-id="e19f6-207">Esecuzione del mapping di un dominio con caratteri jolly</span><span class="sxs-lookup"><span data-stu-id="e19f6-207">Map a wildcard domain</span></span>

<span data-ttu-id="e19f6-208">Nell'esempio dell'esercitazione si esegue il mapping di un [nome DNS con caratteri jolly](https://en.wikipedia.org/wiki/Wildcard_DNS_record), ad esempio `*.contoso.com`, all'app del servizio app aggiungendo un record CNAME.</span><span class="sxs-lookup"><span data-stu-id="e19f6-208">In the tutorial example, you map a [wildcard DNS name](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (for example, `*.contoso.com`) to the App Service app by adding a CNAME record.</span></span> 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-cname-record"></a><span data-ttu-id="e19f6-209">Creazione di un record CNAME</span><span class="sxs-lookup"><span data-stu-id="e19f6-209">Create the CNAME record</span></span>

<span data-ttu-id="e19f6-210">Aggiungere un record CNAME per eseguire il mapping di un nome con caratteri jolly al nome host predefinito dell'app (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="e19f6-210">Add a CNAME record to map a wildcard name to the app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="e19f6-211">Per l'esempio di dominio `*.contoso.com`, il record CNAME eseguirà il mapping del nome `*` a `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="e19f6-211">For the `*.contoso.com` domain example, the CNAME record will map the name `*` to `<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="e19f6-212">Dopo aver aggiunto il record CNAME, la pagina dei record DNS è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e19f6-212">When the CNAME is added, the DNS records page looks like the following example:</span></span>

![Passaggio all'app di Azure nel portale](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-the-cname-record-mapping-in-the-app"></a><span data-ttu-id="e19f6-214">Abilitare il mapping dei record CNAME nell'app</span><span class="sxs-lookup"><span data-stu-id="e19f6-214">Enable the CNAME record mapping in the app</span></span>

<span data-ttu-id="e19f6-215">È ora possibile aggiungere qualsiasi sottodominio che corrisponde al nome con caratteri jolly nell'app, ad esempio `sub1.contoso.com` e `sub2.contoso.com` corrispondono a `*.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="e19f6-215">You can now add any subdomain that matches the wildcard name to the app (for example, `sub1.contoso.com` and `sub2.contoso.com` match `*.contoso.com`).</span></span> 

<span data-ttu-id="e19f6-216">Nel riquadro di spostamento a sinistra della pagina dell'app nel portale di Azure selezionare **Domini personalizzati**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-216">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Menu del dominio personalizzato](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="e19f6-218">Selezionare l'icona **+** accanto ad **Aggiungi il nome host**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-218">Select the **+** icon next to **Add hostname**.</span></span>

![Aggiunta del nome host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="e19f6-220">Digitare un nome di dominio completo corrispondente al dominio con caratteri jolly, ad esempio `sub1.contoso.com`, quindi selezionare **Convalida**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-220">Type a fully qualified domain name that matches the wildcard domain (for example, `sub1.contoso.com`), and then select **Validate**.</span></span>

<span data-ttu-id="e19f6-221">Viene attivato il pulsante **Aggiungi il nome host**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-221">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="e19f6-222">Assicurarsi che **Tipo di record del nome host** sia impostato su **CNAME (www.example.com o qualsiasi sottodominio)**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-222">Make sure that **Hostname record type** is set to **CNAME record (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="e19f6-223">Selezionare **Aggiungi il nome host**.</span><span class="sxs-lookup"><span data-stu-id="e19f6-223">Select **Add hostname**.</span></span>

![Aggiunta del nome DNS all'app](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

<span data-ttu-id="e19f6-225">La visualizzazione del nuovo nome host nella pagina **Domini personalizzati** dell'app potrebbe richiedere qualche minuto.</span><span class="sxs-lookup"><span data-stu-id="e19f6-225">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="e19f6-226">Provare ad aggiornare il browser per visualizzare i dati più recenti.</span><span class="sxs-lookup"><span data-stu-id="e19f6-226">Try refreshing the browser to update the data.</span></span>

<span data-ttu-id="e19f6-227">Fare di nuovo clic sull'icona **+** per aggiungere un altro nome host corrispondente al dominio con caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="e19f6-227">Select the **+** icon again to add another hostname that matches the wildcard domain.</span></span> <span data-ttu-id="e19f6-228">Ad esempio, aggiungere `sub2.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="e19f6-228">For example, add `sub2.contoso.com`.</span></span>

![Record CNAME aggiunto](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a><span data-ttu-id="e19f6-230">Prova nel browser</span><span class="sxs-lookup"><span data-stu-id="e19f6-230">Test in browser</span></span>

<span data-ttu-id="e19f6-231">Passare al nome o ai nomi DNS configurati in precedenza, ad esempio `contoso.com`,  `www.contoso.com`, `sub1.contoso.com` e `sub2.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="e19f6-231">Browse to the DNS name(s) that you configured earlier (for example, `contoso.com`,  `www.contoso.com`, `sub1.contoso.com`, and `sub2.contoso.com`).</span></span>

![Passaggio all'app di Azure nel portale](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a><span data-ttu-id="e19f6-233">Automatizzazione con gli script</span><span class="sxs-lookup"><span data-stu-id="e19f6-233">Automate with scripts</span></span>

<span data-ttu-id="e19f6-234">È possibile automatizzare la gestione dei domini personalizzati con gli script, usando l'[interfaccia della riga di comando di Azure](/cli/azure/install-azure-cli) o [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e19f6-234">You can automate management of custom domains with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="azure-cli"></a><span data-ttu-id="e19f6-235">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="e19f6-235">Azure CLI</span></span> 

<span data-ttu-id="e19f6-236">Il seguente comando aggiunge un nome DNS personalizzato configurato a un'applicazione del servizio app.</span><span class="sxs-lookup"><span data-stu-id="e19f6-236">The following command adds a configured custom DNS name to an App Service app.</span></span> 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

<span data-ttu-id="e19f6-237">Per altre informazioni, vedere [Eseguire il mapping di un dominio personalizzato a un'app Web](scripts/app-service-cli-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="e19f6-237">For more information, see [Map a custom domain to a web app](scripts/app-service-cli-configure-custom-domain.md).</span></span> 

### <a name="azure-powershell"></a><span data-ttu-id="e19f6-238">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e19f6-238">Azure PowerShell</span></span> 

<span data-ttu-id="e19f6-239">Il seguente comando aggiunge un nome DNS personalizzato configurato a un'applicazione del servizio app.</span><span class="sxs-lookup"><span data-stu-id="e19f6-239">The following command adds a configured custom DNS name to an App Service app.</span></span> 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

<span data-ttu-id="e19f6-240">Per ulteriori informazioni, vedere [Assegnazione di un dominio personalizzato a un’app Web](scripts/app-service-powershell-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="e19f6-240">For more information, see [Assign a custom domain to a web app](scripts/app-service-powershell-configure-custom-domain.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e19f6-241">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e19f6-241">Next steps</span></span>

<span data-ttu-id="e19f6-242">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="e19f6-242">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e19f6-243">Eseguire il mapping di un sottodominio usando un record CNAME</span><span class="sxs-lookup"><span data-stu-id="e19f6-243">Map a subdomain by using a CNAME record</span></span>
> * <span data-ttu-id="e19f6-244">Eseguire il mapping di un dominio radice usando un record A</span><span class="sxs-lookup"><span data-stu-id="e19f6-244">Map a root domain by using an A record</span></span>
> * <span data-ttu-id="e19f6-245">Eseguire il mapping di un dominio con caratteri jolly usando un record CNAME</span><span class="sxs-lookup"><span data-stu-id="e19f6-245">Map a wildcard domain by using a CNAME record</span></span>
> * <span data-ttu-id="e19f6-246">Automatizzare il mapping dei domini con script</span><span class="sxs-lookup"><span data-stu-id="e19f6-246">Automate domain mapping with scripts</span></span>

<span data-ttu-id="e19f6-247">Passare all'esercitazione successiva per apprendere come associare un certificato SSL personalizzato a un'app Web.</span><span class="sxs-lookup"><span data-stu-id="e19f6-247">Advance to the next tutorial to learn how to bind a custom SSL certificate to a web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e19f6-248">Associare un certificato SSL personalizzato esistente ad app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="e19f6-248">Bind an existing custom SSL certificate to Azure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
