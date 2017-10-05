---
title: Acquistare un nome di dominio personalizzato per app Web Azure
description: Informazioni su come acquistare un nome di dominio personalizzato con un'app Web in Servizio app di Azure.
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 3cb22b935624041ab51e64028a1b668fd694f9b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a><span data-ttu-id="d9bc3-103">Acquistare un nome di dominio personalizzato per app Web Azure</span><span class="sxs-lookup"><span data-stu-id="d9bc3-103">Buy a custom domain name for Azure Web Apps</span></span>

<span data-ttu-id="d9bc3-104">I domini del servizio app (anteprima) sono i domini di primo livello che sono gestiti direttamente in Azure.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-104">App Service domains (preview) are top-level domains that are managed directly in Azure.</span></span> <span data-ttu-id="d9bc3-105">Semplificano le operazioni di gestione dei domini personalizzati per le [app Web di Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d9bc3-105">They make it easy to manage custom domains for [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="d9bc3-106">In questa esercitazione viene illustrato come acquistare un dominio del servizio app e come assegnare i nomi DNS alle app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-106">This tutorial shows you how to buy an App Service domain and assign DNS names to Azure Web Apps.</span></span>

<span data-ttu-id="d9bc3-107">Questo articolo è per il Servizio app di Azure (app Web, app per le API, app per dispositivi mobili, app per la logica).</span><span class="sxs-lookup"><span data-stu-id="d9bc3-107">This article is for Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps).</span></span> <span data-ttu-id="d9bc3-108">Per una macchina virtuale di Azure o per Archiviazione di Azure, vedere [Assign App Service domain to Azure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/) (Assegnare il dominio del servizio app alla macchina virtuale di Azure o ad Archiviazione di Azure).</span><span class="sxs-lookup"><span data-stu-id="d9bc3-108">For Azure VM or Azure Storage, see [Assign App Service domain to Azure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span></span> <span data-ttu-id="d9bc3-109">Per i servizi cloud, vedere [Configurazione di un nome di dominio personalizzato per un servizio cloud di Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d9bc3-109">For Cloud Services, see [Configuring a custom domain name for an Azure cloud service](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9bc3-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d9bc3-110">Prerequisites</span></span>

<span data-ttu-id="d9bc3-111">Per completare questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="d9bc3-111">To complete this tutorial:</span></span>

* <span data-ttu-id="d9bc3-112">[Creare un'app del servizio app](/azure/app-service/) oppure usare un'app creata per un'altra esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-112">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>

## <a name="prepare-the-app"></a><span data-ttu-id="d9bc3-113">Preparare l'app</span><span class="sxs-lookup"><span data-stu-id="d9bc3-113">Prepare the app</span></span>

<span data-ttu-id="d9bc3-114">Per usare domini personalizzati nelle app Web di Azure, è necessario che il [piano di servizio app](https://azure.microsoft.com/pricing/details/app-service/) dell'app Web sia un livello a pagamento (**Condiviso**, **Basic**, **Standard** o **Premium**).</span><span class="sxs-lookup"><span data-stu-id="d9bc3-114">To use custom domains in Azure Web Apps, your web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="d9bc3-115">In questo passaggio, verificare che l'app Web sia supportata dal piano tariffario adeguato.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-115">In this step, you make sure that the web app is in the supported pricing tier.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="d9bc3-116">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="d9bc3-116">Sign in to Azure</span></span>

<span data-ttu-id="d9bc3-117">Aprire il [portale di Azure](https://portal.azure.com) e accedere con l'account Azure.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-117">Open the [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-to-the-app-in-the-azure-portal"></a><span data-ttu-id="d9bc3-118">Passare all'app nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d9bc3-118">Navigate to the app in the Azure portal</span></span>

<span data-ttu-id="d9bc3-119">Dal menu a sinistra selezionare **Servizi app** e quindi selezionare il nome dell'app.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-119">From the left menu, select **App Services**, and then select the name of the app.</span></span>

![Passaggio all'app di Azure nel portale](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="d9bc3-121">Viene visualizzata la pagina di gestione dell'app del servizio app.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-121">You see the management page of the App Service app.</span></span>  

### <a name="check-the-pricing-tier"></a><span data-ttu-id="d9bc3-122">Scegliere il piano tariffario</span><span class="sxs-lookup"><span data-stu-id="d9bc3-122">Check the pricing tier</span></span>

<span data-ttu-id="d9bc3-123">Nel riquadro di spostamento a sinistra della pagina dell'app scorrere fino alla sezione **Impostazioni** e selezionare **Scala verticalmente (piano di servizio app)**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-123">In the left navigation of the app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menu di scalabilità verticale](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="d9bc3-125">Il livello corrente dell'app è evidenziato da un bordo blu.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-125">The app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="d9bc3-126">Verificare che l'app non sia inclusa nel livello **Gratuito**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-126">Check to make sure that the app is not in the **Free** tier.</span></span> <span data-ttu-id="d9bc3-127">Il DNS personalizzato non è supportato nel livello **Gratuito**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-127">Custom DNS is not supported in the **Free** tier.</span></span> 

![Controllare il piano tariffario](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="d9bc3-129">Se il piano di servizio app non è **Gratuito**, chiudere la pagina **Scegliere il piano tariffario** e passare a [Acquista il dominio](#buy-the-domain).</span><span class="sxs-lookup"><span data-stu-id="d9bc3-129">If the App Service plan is not **Free**, close the **Choose your pricing tier** page and skip to [Buy the domain](#buy-the-domain).</span></span>

### <a name="scale-up-the-app-service-plan"></a><span data-ttu-id="d9bc3-130">Passare a un piano di servizio app di livello superiore</span><span class="sxs-lookup"><span data-stu-id="d9bc3-130">Scale up the App Service plan</span></span>

<span data-ttu-id="d9bc3-131">Selezionare uno dei livelli non gratuiti (**Condiviso**, **Base**, **Standard** o **Premium**).</span><span class="sxs-lookup"><span data-stu-id="d9bc3-131">Select any of the non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="d9bc3-132">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-132">Click **Select**.</span></span>

![Controllare il piano tariffario](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="d9bc3-134">La visualizzazione della notifica seguente indica che l'operazione di passaggio al livello superiore è stata completata.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-134">When you see the following notification, the scale operation is complete.</span></span>

![Conferma operazione di scalabilità](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-the-domain"></a><span data-ttu-id="d9bc3-136">Acquistare il dominio</span><span class="sxs-lookup"><span data-stu-id="d9bc3-136">Buy the domain</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="d9bc3-137">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="d9bc3-137">Sign in to Azure</span></span>
<span data-ttu-id="d9bc3-138">Aprire il [portale di Azure](https://portal.azure.com/) e accedere con l'account Azure.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-138">Open the [Azure portal](https://portal.azure.com/) and sign in with your Azure account.</span></span>

### <a name="launch-buy-domains"></a><span data-ttu-id="d9bc3-139">Avvio di Acquistare un dominio</span><span class="sxs-lookup"><span data-stu-id="d9bc3-139">Launch Buy domains</span></span>
<span data-ttu-id="d9bc3-140">Nella scheda **App Web** fare clic sul nome dell'app Web, selezionare **Impostazioni** e quindi **Domini personalizzati**</span><span class="sxs-lookup"><span data-stu-id="d9bc3-140">In the **Web Apps** tab, click the name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="d9bc3-141">Nella pagina **Domini personalizzati** fare clic su **Acquista domini**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-141">In the **Custom domains** page, click **Buy domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-the-domain-purchase"></a><span data-ttu-id="d9bc3-142">Configurare l’acquisto del dominio</span><span class="sxs-lookup"><span data-stu-id="d9bc3-142">Configure the domain purchase</span></span>

<span data-ttu-id="d9bc3-143">Nella pagina **Dominio del servizio app**, digitare il nome di dominio che si desidera acquistare nel riquadro **Ricerca dominio** , quindi digitare `Enter`.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-143">In the **App Service Domain** page, in the **Search for domain** box, type the domain name you want to buy and type `Enter`.</span></span> <span data-ttu-id="d9bc3-144">I domini disponibili suggeriti vengono visualizzati sotto la casella di testo.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-144">The suggested available domains are shown just below the text box.</span></span> <span data-ttu-id="d9bc3-145">Selezionare uno o più domini che si desidera acquistare.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-145">Select one or more domains you want to buy.</span></span> 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

<span data-ttu-id="d9bc3-146">Scegliere **Informazioni di contatto** e compilare il modulo di informazioni di contatto del dominio.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-146">Click the **Contact Information** and fill out the domain's contact information form.</span></span> <span data-ttu-id="d9bc3-147">Al termine, fare clic su **OK** per tornare alla pagina del dominio di servizio app.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-147">When finished, click **OK** to return to the App Service Domain page.</span></span>
   
<span data-ttu-id="d9bc3-148">È molto importante compilare tutti i campi obbligatori con la massima correttezza possibile.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-148">It is important that you fill out all required fields with as much accuracy as possible.</span></span> <span data-ttu-id="d9bc3-149">I dati non corretti relativi alle informazioni di contatto causano errori nell'acquisto dei domini.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-149">Incorrect data for contact information can result in failure to purchase domains.</span></span> 

<span data-ttu-id="d9bc3-150">Selezionare quindi le opzioni desiderate per il dominio.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-150">Next, select the desired options for your domain.</span></span> <span data-ttu-id="d9bc3-151">Vedere la tabella seguente per alcune spiegazioni:</span><span class="sxs-lookup"><span data-stu-id="d9bc3-151">See the following table for explanations:</span></span>

| <span data-ttu-id="d9bc3-152">Impostazione</span><span class="sxs-lookup"><span data-stu-id="d9bc3-152">Setting</span></span> | <span data-ttu-id="d9bc3-153">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="d9bc3-153">Suggested Value</span></span> | <span data-ttu-id="d9bc3-154">Descrizione</span><span class="sxs-lookup"><span data-stu-id="d9bc3-154">Description</span></span> |
|-|-|-|
|<span data-ttu-id="d9bc3-155">Rinnovo automatico</span><span class="sxs-lookup"><span data-stu-id="d9bc3-155">Auto renew</span></span> | <span data-ttu-id="d9bc3-156">**Abilitazione**</span><span class="sxs-lookup"><span data-stu-id="d9bc3-156">**Enable**</span></span> | <span data-ttu-id="d9bc3-157">Rinnova il dominio del servizio App automaticamente ogni anno.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-157">Renews your App Service Domain automatically every year.</span></span> <span data-ttu-id="d9bc3-158">Al momento del rinnovo, sulla carta di credito viene addebitato lo stesso prezzo di acquisto.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-158">Your credit card is charged the same purchase price at the time of renewal.</span></span> |
|<span data-ttu-id="d9bc3-159">Protezione della privacy</span><span class="sxs-lookup"><span data-stu-id="d9bc3-159">Privacy protection</span></span> | <span data-ttu-id="d9bc3-160">Abilita</span><span class="sxs-lookup"><span data-stu-id="d9bc3-160">Enable</span></span> | <span data-ttu-id="d9bc3-161">Optare per "Protezione della privacy", che è incluso nel prezzo di acquisto _gratuitamente_ (ad eccezione dei domini di primo livello il cui registro non supporta la protezione della privacy, ad esempio _.co.in_, _.co.uk_ e così via).</span><span class="sxs-lookup"><span data-stu-id="d9bc3-161">Opt in to "Privacy protection", which is included in the purchase price _for free_ (except for top-level domains whose registry do not support privacy protection, such as _.co.in_, _.co.uk_, and so on).</span></span> |
| <span data-ttu-id="d9bc3-162">Assegnare i nomi host predefiniti</span><span class="sxs-lookup"><span data-stu-id="d9bc3-162">Assign default hostnames</span></span> | <span data-ttu-id="d9bc3-163">**www** e **@**</span><span class="sxs-lookup"><span data-stu-id="d9bc3-163">**www** and **@**</span></span> | <span data-ttu-id="d9bc3-164">Selezionare le associazioni del nome host desiderate, se necessario.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-164">Select the desired hostname bindings, if desired.</span></span> <span data-ttu-id="d9bc3-165">Una volta completata l'operazione di acquisto del dominio, l'app Web è accessibile tramite i nomi host selezionati.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-165">When the domain purchase operation is complete, your web app can be accessed at the selected hostnames.</span></span> <span data-ttu-id="d9bc3-166">Se l'app Web è nascosta da [Gestione traffico di Microsoft Azure](https://azure.microsoft.com/services/traffic-manager/), non viene visualizzata l'opzione per assegnare il dominio radice (@), perché Gestione traffico non supporta record A.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-166">If the web app is behind [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), you don't see the option to assign the root domain (@), because Traffic Manager does not support A records.</span></span> <span data-ttu-id="d9bc3-167">Al termine dell'acquisto di un dominio, è possibile apportare modifiche alle assegnazioni di nome host.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-167">You can make changes to the hostname assignments after the domain purchase completes.</span></span> |

### <a name="accept-terms-and-purchase"></a><span data-ttu-id="d9bc3-168">Accettare i termini di acquisto</span><span class="sxs-lookup"><span data-stu-id="d9bc3-168">Accept terms and purchase</span></span>

<span data-ttu-id="d9bc3-169">Fare clic su **Termini legali** per leggere i termini e le tariffe, quindi fare clic su **Acquista**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-169">Click **Legal Terms** to review the terms and the charges, then click **Buy**.</span></span>

> [!NOTE]
> <span data-ttu-id="d9bc3-170">I domini del servizio app usano il DNS di Azure per ospitare i domini.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-170">App Service Domains use Azure DNS to host the domains.</span></span> <span data-ttu-id="d9bc3-171">Oltre alla tariffa di registrazione del dominio, si applicano le spese di utilizzo per il DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-171">In addition to the domain registration fee, usage charges for Azure DNS apply.</span></span> <span data-ttu-id="d9bc3-172">Per altre informazioni, vedere la pagina relativa ai [prezzi del DNS di Azure](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="d9bc3-172">For information, see [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>
>
>

<span data-ttu-id="d9bc3-173">Nella pagina **Dominio di servizio app** fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-173">Back in the **App Service Domain** page, click **OK**.</span></span> <span data-ttu-id="d9bc3-174">Mentre l'operazione è in corso, vedrai le notifiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="d9bc3-174">While the operation is in progress, you see the following notifications:</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-the-hostnames"></a><span data-ttu-id="d9bc3-175">Verifica dei nomi host</span><span class="sxs-lookup"><span data-stu-id="d9bc3-175">Test the hostnames</span></span>

<span data-ttu-id="d9bc3-176">Se sono stati assegnati nomi host predefiniti all'app Web, è anche possibile visualizzare una notifica di esito positivo per ogni nome host selezionato.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-176">If you have assigned default hostnames to your web app, you also see a success notification for each selected hostname.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

<span data-ttu-id="d9bc3-177">I nomi host selezionati vengono visualizzati nella pagina **Domini personalizzati**, nella sezione **Nomi host**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-177">You also see the selected hostnames in the **Custom domains** page, in the **Hostnames** section.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

<span data-ttu-id="d9bc3-178">Per verificare i nomi host, navigare nei nomi host elencati dal browser.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-178">To test the hostnames, navigate to the listed hostnames in the browser.</span></span> <span data-ttu-id="d9bc3-179">Nell'esempio nella schermata precedente, navigare in _kontoso.net_ e _www.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-179">In the example in the preceding screenshot, try navigating to _kontoso.net_ and _www.kontoso.net_.</span></span>

## <a name="assign-hostnames-to-web-app"></a><span data-ttu-id="d9bc3-180">Assegnare i nomi host per app Web</span><span class="sxs-lookup"><span data-stu-id="d9bc3-180">Assign hostnames to web app</span></span>

<span data-ttu-id="d9bc3-181">Se si sceglie di non assegnare uno o più nomi host predefiniti per l'app Web durante il processo di acquisto oppure se è necessario assegnare un nome host non elencato, è possibile assegnare un nome host in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-181">If you choose not to assign one or more default hostnames to your web app during the purchase process, or if you need to assign a hostname not listed, you can assign a hostname at anytime.</span></span>

<span data-ttu-id="d9bc3-182">È inoltre possibile assegnare i nomi host nel dominio del servizio app a qualsiasi altra app Web.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-182">You can also assign hostnames in the App Service Domain to any other web app.</span></span> <span data-ttu-id="d9bc3-183">I passaggi variano a seconda se il dominio del servizio app e l'app Web appartengono alla stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-183">The steps depend on whether the App Service Domain and the web app belong to the same subscription.</span></span>

- <span data-ttu-id="d9bc3-184">Sottoscrizione diversa: eseguire il mapping personalizzato dei record DNS dal dominio del servizio app all'app Web analogamente a un dominio acquistato esternamente.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-184">Different subscription: Map custom DNS records from the App Service Domain to the web app like an externally purchased domain.</span></span> <span data-ttu-id="d9bc3-185">Per informazioni sull'aggiunta di nomi DNS personalizzati a un dominio del servizio app, vedere [Gestione dei record DNS personalizzati](#custom).</span><span class="sxs-lookup"><span data-stu-id="d9bc3-185">For information on adding custom DNS names to an App Service Domain, see [Manage custom DNS records](#custom).</span></span> <span data-ttu-id="d9bc3-186">Per eseguire il mapping di un dominio esterno acquistato per un'app Web, vedere [Eseguire il mapping di un nome DNS personalizzato esistente per le app Web di Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="d9bc3-186">To map an external purchased domain to a web app, see [Map an existing custom DNS name to Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span> 
- <span data-ttu-id="d9bc3-187">In caso di medesima sottoscrizione, eseguire la procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-187">Same subscription: Use the following steps.</span></span>

### <a name="launch-add-hostname"></a><span data-ttu-id="d9bc3-188">Avviare Aggiungi nome host</span><span class="sxs-lookup"><span data-stu-id="d9bc3-188">Launch add hostname</span></span>
<span data-ttu-id="d9bc3-189">Nella pagina **servizi App**, selezionare il nome dell'app Web a cui si desidera assegnare i nomi host, selezionare **Impostazioni**, quindi selezionare **Domini personalizzati**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-189">In the **App Services** page, select the name of your web app that you want to assign hostnames to, select **Settings**, and then select **Custom domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="d9bc3-190">Verificare che il dominio acquistato sia presente nella sezione **domini del servizio app**, ma non selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-190">Make sure that your purchased domain is listed in the **App Service Domains** section, but don't select it.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> <span data-ttu-id="d9bc3-191">Tutti i domini del servizio app con la stessa sottoscrizione vengono visualizzati nella pagina dell'app Web **Domini personalizzati**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-191">All App Service Domains in the same subscription are shown in the web app's **Custom domains** page.</span></span> <span data-ttu-id="d9bc3-192">Se il dominio è nella sottoscrizione dell'app Web, ma non è possibile visualizzarlo nella pagina dell'app Web **Domini personalizzati**, provare a riaprire la pagina **Domini personalizzati** pagina o aggiornare la pagina Web.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-192">If your domain is in the web app's subscription, but you cannot see it in the web app's **Custom domains** page, try reopening the **Custom domains** page or refresh the webpage.</span></span> <span data-ttu-id="d9bc3-193">Inoltre, selezionare l'icona a forma di campanella nella parte superiore del portale di Azure per verificare lo stato di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-193">Also, check the notification bell at the top of the Azure portal for progress or creation failures.</span></span>
>
>

<span data-ttu-id="d9bc3-194">Selezionare **Aggiungi il nome host**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-194">Select **Add hostname**.</span></span>

### <a name="configure-hostname"></a><span data-ttu-id="d9bc3-195">Configurare il nome host</span><span class="sxs-lookup"><span data-stu-id="d9bc3-195">Configure hostname</span></span>
<span data-ttu-id="d9bc3-196">Nella finestra di dialogo **Aggiungere nome host**, digitare il nome di dominio completo del dominio del servizio app o di qualsiasi sottodominio.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-196">In the **Add hostname** dialog, type the fully qualified domain name of your App Service Domain or any subdomain.</span></span> <span data-ttu-id="d9bc3-197">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d9bc3-197">For example:</span></span>

- <span data-ttu-id="d9bc3-198">kontoso.net</span><span class="sxs-lookup"><span data-stu-id="d9bc3-198">kontoso.net</span></span>
- <span data-ttu-id="d9bc3-199">www.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="d9bc3-199">www.kontoso.net</span></span>
- <span data-ttu-id="d9bc3-200">abc.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="d9bc3-200">abc.kontoso.net</span></span>

<span data-ttu-id="d9bc3-201">Al termine, selezionare **Convalida**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-201">When finished, select **Validate**.</span></span> <span data-ttu-id="d9bc3-202">Il tipo di record del nome host viene selezionato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-202">The hostname record type is automatically selected for you.</span></span>

<span data-ttu-id="d9bc3-203">Selezionare **Aggiungi il nome host**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-203">Select **Add hostname**.</span></span>

<span data-ttu-id="d9bc3-204">Una volta completata l'operazione, viene visualizzata una notifica di esito positivo per il nome di host assegnato.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-204">When the operation is complete, you see a success notification for the assigned hostname.</span></span>  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a><span data-ttu-id="d9bc3-205">Chiudere Aggiungi il nome host</span><span class="sxs-lookup"><span data-stu-id="d9bc3-205">Close add hostname</span></span>
<span data-ttu-id="d9bc3-206">Nella pagina **Aggiungi il nome host**, assegnare qualsiasi nome host all'app Web, in base alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-206">In the **Add hostname** page, assign any other hostname to your web app, as desired.</span></span> <span data-ttu-id="d9bc3-207">Al termine, chiudere la pagina **Aggiungi il nome host**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-207">When finished, close the **Add hostname** page.</span></span>

<span data-ttu-id="d9bc3-208">Viene visualizzato il nome host appena assegnato nella pagina dell’app **Domini personalizzati**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-208">You should now see the newly assigned hostname(s) in your app's **Custom domains** page.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-the-hostnames"></a><span data-ttu-id="d9bc3-209">Verifica dei nomi host</span><span class="sxs-lookup"><span data-stu-id="d9bc3-209">Test the hostnames</span></span>

<span data-ttu-id="d9bc3-210">Navigare tra i nomi host elencati nel browser.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-210">Navigate to the listed hostnames in the browser.</span></span> <span data-ttu-id="d9bc3-211">Nell'esempio della schermata precedente, navigare in _abc.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-211">In the example in the preceding screenshot, try navigating to _abc.kontoso.net_.</span></span>

<a name="custom" />

## <a name="manage-custom-dns-records"></a><span data-ttu-id="d9bc3-212">Gestire i record DNS personalizzati</span><span class="sxs-lookup"><span data-stu-id="d9bc3-212">Manage custom DNS records</span></span>

<span data-ttu-id="d9bc3-213">In Azure, i record DNS per un dominio del servizio app vengono gestiti tramite [DNS di Azure](https://azure.microsoft.com/services/dns/).</span><span class="sxs-lookup"><span data-stu-id="d9bc3-213">In Azure, DNS records for an App Service Domain are managed using [Azure DNS](https://azure.microsoft.com/services/dns/).</span></span> <span data-ttu-id="d9bc3-214">È possibile aggiungere, rimuovere e aggiornare i record DNS, esattamente come per un dominio acquistato esternamente.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-214">You can add, remove, and update DNS records, just like for an externally purchased domain.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="d9bc3-215">Aprire Dominio del servizio app</span><span class="sxs-lookup"><span data-stu-id="d9bc3-215">Open App Service Domain</span></span>

<span data-ttu-id="d9bc3-216">Nel portale di Azure, nel menu a sinistra, selezionare **Più servizi** > **Domini del servizio app**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-216">In the Azure portal, from the left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="d9bc3-217">Selezionare il dominio da gestire.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-217">Select the domain to manage.</span></span> 

### <a name="access-dns-zone"></a><span data-ttu-id="d9bc3-218">Accesso alla Zona DNS</span><span class="sxs-lookup"><span data-stu-id="d9bc3-218">Access DNS zone</span></span>

<span data-ttu-id="d9bc3-219">Nel menu a sinistra del dominio, selezionare **Zona DNS**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-219">In the domain's left menu, select **DNS zone**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

<span data-ttu-id="d9bc3-220">Questa azione permette di aprire la pagina [Zona DNS](../dns/dns-zones-records.md) del dominio del servizio App nel DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-220">This action opens the [DNS zone](../dns/dns-zones-records.md) page of your App Service Domain in Azure DNS.</span></span> <span data-ttu-id="d9bc3-221">Per informazioni su come modificare i record DNS, vedere [Come gestire le zone DNS nel portale di Azure](../dns/dns-operations-dnszones-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d9bc3-221">For information on how to edit DNS records, see [How to manage DNS Zones in the Azure portal](../dns/dns-operations-dnszones-portal.md).</span></span>

## <a name="cancel-purchase-delete-domain"></a><span data-ttu-id="d9bc3-222">Annullare l'acquisto (elimina dominio)</span><span class="sxs-lookup"><span data-stu-id="d9bc3-222">Cancel purchase (delete domain)</span></span>

<span data-ttu-id="d9bc3-223">Dopo aver acquistato il dominio del servizio app, si hanno a disposizione cinque giorni per annullare l'acquisto e ricevere un rimborso completo.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-223">After you purchase the App Service Domain, you have five days to cancel your purchase for a full refund.</span></span> <span data-ttu-id="d9bc3-224">Dopo cinque giorni, è possibile eliminare il dominio del servizio app, ma non è possibile ricevere un rimborso.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-224">After five days, you can delete the App Service Domain, but cannot receive a refund.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="d9bc3-225">Aprire Dominio del servizio app</span><span class="sxs-lookup"><span data-stu-id="d9bc3-225">Open App Service Domain</span></span>

<span data-ttu-id="d9bc3-226">Nel portale di Azure, nel menu a sinistra, selezionare **Più servizi** > **Domini del servizio app**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-226">In the Azure portal, from the left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="d9bc3-227">Selezionare il dominio che si desidera annullare o eliminare.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-227">Select the domain to you want to cancel or delete.</span></span> 

### <a name="delete-hostname-bindings"></a><span data-ttu-id="d9bc3-228">Eliminare associazioni nome host</span><span class="sxs-lookup"><span data-stu-id="d9bc3-228">Delete hostname bindings</span></span>

<span data-ttu-id="d9bc3-229">Nel menu a sinistra del dominio, selezionare **Associazioni nome host**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-229">In the domain's left menu, select **Hostname bindings**.</span></span> <span data-ttu-id="d9bc3-230">Le associazioni nome host da tutti i servizi Azure sono elencate di seguito.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-230">The hostname bindings from all Azure services are listed here.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

<span data-ttu-id="d9bc3-231">Non è possibile eliminare il dominio del servizio app finché non vengono eliminate tutte le associazioni nome host.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-231">You cannot delete the App Service Domain until all hostname bindings are deleted.</span></span>

<span data-ttu-id="d9bc3-232">Eliminare le associazioni nome host selezionando **...** > **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-232">Delete each hostname binding by selecting **...** > **Delete**.</span></span> <span data-ttu-id="d9bc3-233">Dopo l'eliminazione di tutte le associazioni, selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-233">After all the bindings are deleted, select **Save**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a><span data-ttu-id="d9bc3-234">Annullare o eliminare</span><span class="sxs-lookup"><span data-stu-id="d9bc3-234">Cancel or delete</span></span>

<span data-ttu-id="d9bc3-235">Nel menu a sinistra del dominio, selezionare **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-235">In the domain's left menu, select **Overview**.</span></span> 

<span data-ttu-id="d9bc3-236">Se non è trascorso il periodo di cancellazione del dominio acquistato, selezionare **Annulla acquisto**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-236">If the cancellation period on the purchased domain has not elapsed, select **Cancel purchase**.</span></span> <span data-ttu-id="d9bc3-237">In caso contrario, viene visualizzato il pulsante **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-237">Otherwise, you see a **Delete** button instead.</span></span> <span data-ttu-id="d9bc3-238">Per eliminare il dominio senza rimborso, selezionare **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-238">To delete the domain without a refund, select **Delete**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

<span data-ttu-id="d9bc3-239">Selezionare **OK** per confermare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-239">Select **OK** to confirm the operation.</span></span> <span data-ttu-id="d9bc3-240">Se non si desidera continuare, fare clic su qualsiasi punto all'esterno della finestra di dialogo di conferma.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-240">If you don't want to proceed, click anywhere outside of the confirmation dialog.</span></span>

<span data-ttu-id="d9bc3-241">Al termine dell’operazione, il dominio viene rilasciato dalla sottoscrizione e può essere riacquistato dagli altri utenti.</span><span class="sxs-lookup"><span data-stu-id="d9bc3-241">After the operation is complete, the domain is released from your subscription and available for anyone to purchase again.</span></span> 
