---
title: aaaBuy un nome di dominio personalizzato per le app Web di Azure
description: Informazioni su come assegnare un nome toobuy un dominio personalizzato con un'app web nel servizio App di Azure.
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
ms.openlocfilehash: 2ff61a3f27020516c917fe105ece99eb2a5754b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a><span data-ttu-id="e732b-103">Acquistare un nome di dominio personalizzato per app Web Azure</span><span class="sxs-lookup"><span data-stu-id="e732b-103">Buy a custom domain name for Azure Web Apps</span></span>

<span data-ttu-id="e732b-104">I domini del servizio app (anteprima) sono i domini di primo livello che sono gestiti direttamente in Azure.</span><span class="sxs-lookup"><span data-stu-id="e732b-104">App Service domains (preview) are top-level domains that are managed directly in Azure.</span></span> <span data-ttu-id="e732b-105">Rendono i domini personalizzati toomanage semplice [App Web di Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e732b-105">They make it easy toomanage custom domains for [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="e732b-106">Questa esercitazione viene illustrato come un dominio di servizio App toobuy e assegnare DNS nomi tooAzure Web App.</span><span class="sxs-lookup"><span data-stu-id="e732b-106">This tutorial shows you how toobuy an App Service domain and assign DNS names tooAzure Web Apps.</span></span>

<span data-ttu-id="e732b-107">Questo articolo è per il Servizio app di Azure (app Web, app per le API, app per dispositivi mobili, app per la logica).</span><span class="sxs-lookup"><span data-stu-id="e732b-107">This article is for Azure App Service (Web Apps, API Apps, Mobile Apps, Logic Apps).</span></span> <span data-ttu-id="e732b-108">Per una macchina virtuale di Azure o archiviazione di Azure, vedere [tooAzure dominio assegnare App servizio macchina virtuale o archiviazione di Azure](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span><span class="sxs-lookup"><span data-stu-id="e732b-108">For Azure VM or Azure Storage, see [Assign App Service domain tooAzure VM or Azure Storage](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/).</span></span> <span data-ttu-id="e732b-109">Per i servizi cloud, vedere [Configurazione di un nome di dominio personalizzato per un servizio cloud di Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e732b-109">For Cloud Services, see [Configuring a custom domain name for an Azure cloud service](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e732b-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e732b-110">Prerequisites</span></span>

<span data-ttu-id="e732b-111">toocomplete questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="e732b-111">toocomplete this tutorial:</span></span>

* <span data-ttu-id="e732b-112">[Creare un'app del servizio app](/azure/app-service/) oppure usare un'app creata per un'altra esercitazione.</span><span class="sxs-lookup"><span data-stu-id="e732b-112">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>

## <a name="prepare-hello-app"></a><span data-ttu-id="e732b-113">Preparare l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="e732b-113">Prepare hello app</span></span>

<span data-ttu-id="e732b-114">i domini personalizzati toouse in App Web di Azure, l'app web [piano di servizio App](https://azure.microsoft.com/pricing/details/app-service/) deve essere un livello a pagamento (**Shared**, **base**, **Standard**, o **Premium**).</span><span class="sxs-lookup"><span data-stu-id="e732b-114">toouse custom domains in Azure Web Apps, your web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="e732b-115">In questo passaggio è assicurarsi che Hello web app è in hello supportato piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="e732b-115">In this step, you make sure that hello web app is in hello supported pricing tier.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="e732b-116">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="e732b-116">Sign in tooAzure</span></span>

<span data-ttu-id="e732b-117">Aprire hello [portale di Azure](https://portal.azure.com) e accedere con l'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="e732b-117">Open hello [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-toohello-app-in-hello-azure-portal"></a><span data-ttu-id="e732b-118">Passare toohello app nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="e732b-118">Navigate toohello app in hello Azure portal</span></span>

<span data-ttu-id="e732b-119">Scegliere dal menu a sinistra hello **servizi App**e quindi selezionare il nome di hello di app hello.</span><span class="sxs-lookup"><span data-stu-id="e732b-119">From hello left menu, select **App Services**, and then select hello name of hello app.</span></span>

![Spostamento del portale tooAzure app](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="e732b-121">Verrà visualizzata hello pagina di gestione di app del servizio App hello.</span><span class="sxs-lookup"><span data-stu-id="e732b-121">You see hello management page of hello App Service app.</span></span>  

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="e732b-122">Controllo hello piano tariffario</span><span class="sxs-lookup"><span data-stu-id="e732b-122">Check hello pricing tier</span></span>

<span data-ttu-id="e732b-123">Hello navigazione della pagina dell'app hello a sinistra, scorrere toohello **impostazioni** sezione e selezionare **scalabilità verticale (piano di servizio App)**.</span><span class="sxs-lookup"><span data-stu-id="e732b-123">In hello left navigation of hello app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menu di scalabilità verticale](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="e732b-125">livello corrente dell'applicazione Hello è evidenziato da un bordo blu.</span><span class="sxs-lookup"><span data-stu-id="e732b-125">hello app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="e732b-126">Verificare che tale applicazione hello non hello toomake **libero** livello.</span><span class="sxs-lookup"><span data-stu-id="e732b-126">Check toomake sure that hello app is not in hello **Free** tier.</span></span> <span data-ttu-id="e732b-127">DNS personalizzato non è supportato in hello **libero** livello.</span><span class="sxs-lookup"><span data-stu-id="e732b-127">Custom DNS is not supported in hello **Free** tier.</span></span> 

![Controllare il piano tariffario](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="e732b-129">Se hello piano di servizio App non è **libero**, chiudere hello **scegliere il piano tariffario** pagina e andare troppo[dominio hello acquistare](#buy-the-domain).</span><span class="sxs-lookup"><span data-stu-id="e732b-129">If hello App Service plan is not **Free**, close hello **Choose your pricing tier** page and skip too[Buy hello domain](#buy-the-domain).</span></span>

### <a name="scale-up-hello-app-service-plan"></a><span data-ttu-id="e732b-130">Applicare la scalabilità verticale hello piano di servizio App</span><span class="sxs-lookup"><span data-stu-id="e732b-130">Scale up hello App Service plan</span></span>

<span data-ttu-id="e732b-131">Selezionare uno dei livelli di hello non disponibili (**Shared**, **base**, **Standard**, o **Premium**).</span><span class="sxs-lookup"><span data-stu-id="e732b-131">Select any of hello non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="e732b-132">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="e732b-132">Click **Select**.</span></span>

![Controllare il piano tariffario](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="e732b-134">Quando viene visualizzata hello previa notifica, l'operazione di ridimensionamento hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="e732b-134">When you see hello following notification, hello scale operation is complete.</span></span>

![Conferma operazione di scalabilità](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-hello-domain"></a><span data-ttu-id="e732b-136">Acquisto di hello dominio</span><span class="sxs-lookup"><span data-stu-id="e732b-136">Buy hello domain</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="e732b-137">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="e732b-137">Sign in tooAzure</span></span>
<span data-ttu-id="e732b-138">Aprire hello [portale di Azure](https://portal.azure.com/) e accedere con l'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="e732b-138">Open hello [Azure portal](https://portal.azure.com/) and sign in with your Azure account.</span></span>

### <a name="launch-buy-domains"></a><span data-ttu-id="e732b-139">Avvio di Acquistare un dominio</span><span class="sxs-lookup"><span data-stu-id="e732b-139">Launch Buy domains</span></span>
<span data-ttu-id="e732b-140">In hello **App Web** scheda, fare clic sul nome dell'app web, selezionare hello **impostazioni**, quindi selezionare **i domini personalizzati**</span><span class="sxs-lookup"><span data-stu-id="e732b-140">In hello **Web Apps** tab, click hello name of your web app, select **Settings**, and then select **Custom domains**</span></span>
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="e732b-141">In hello **i domini personalizzati** pagina, fare clic su **acquistare domini**.</span><span class="sxs-lookup"><span data-stu-id="e732b-141">In hello **Custom domains** page, click **Buy domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-hello-domain-purchase"></a><span data-ttu-id="e732b-142">Configurare l'acquisto di dominio hello</span><span class="sxs-lookup"><span data-stu-id="e732b-142">Configure hello domain purchase</span></span>

<span data-ttu-id="e732b-143">In hello **dominio del servizio App** pagina hello **Cerca dominio** casella, si desidera toobuy e tipo di nome di dominio di tipo hello `Enter`.</span><span class="sxs-lookup"><span data-stu-id="e732b-143">In hello **App Service Domain** page, in hello **Search for domain** box, type hello domain name you want toobuy and type `Enter`.</span></span> <span data-ttu-id="e732b-144">Hello suggeriti i domini disponibili vengono visualizzati sotto la casella di testo hello.</span><span class="sxs-lookup"><span data-stu-id="e732b-144">hello suggested available domains are shown just below hello text box.</span></span> <span data-ttu-id="e732b-145">Selezionare uno o più domini che si desidera toobuy.</span><span class="sxs-lookup"><span data-stu-id="e732b-145">Select one or more domains you want toobuy.</span></span> 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

<span data-ttu-id="e732b-146">Fare clic su hello **informazioni di contatto** e compilare il modulo di informazioni di contatto del dominio hello.</span><span class="sxs-lookup"><span data-stu-id="e732b-146">Click hello **Contact Information** and fill out hello domain's contact information form.</span></span> <span data-ttu-id="e732b-147">Al termine, fare clic su **OK** pagina di tooreturn toohello dominio del servizio App.</span><span class="sxs-lookup"><span data-stu-id="e732b-147">When finished, click **OK** tooreturn toohello App Service Domain page.</span></span>
   
<span data-ttu-id="e732b-148">È molto importante compilare tutti i campi obbligatori con la massima correttezza possibile.</span><span class="sxs-lookup"><span data-stu-id="e732b-148">It is important that you fill out all required fields with as much accuracy as possible.</span></span> <span data-ttu-id="e732b-149">Domini di errore toopurchase possono generare dati non corretti per le informazioni di contatto.</span><span class="sxs-lookup"><span data-stu-id="e732b-149">Incorrect data for contact information can result in failure toopurchase domains.</span></span> 

<span data-ttu-id="e732b-150">Successivamente, selezionare le opzioni di hello desiderato per il dominio.</span><span class="sxs-lookup"><span data-stu-id="e732b-150">Next, select hello desired options for your domain.</span></span> <span data-ttu-id="e732b-151">Vedere hello spiegazioni nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="e732b-151">See hello following table for explanations:</span></span>

| <span data-ttu-id="e732b-152">Impostazione</span><span class="sxs-lookup"><span data-stu-id="e732b-152">Setting</span></span> | <span data-ttu-id="e732b-153">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="e732b-153">Suggested Value</span></span> | <span data-ttu-id="e732b-154">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e732b-154">Description</span></span> |
|-|-|-|
|<span data-ttu-id="e732b-155">Rinnovo automatico</span><span class="sxs-lookup"><span data-stu-id="e732b-155">Auto renew</span></span> | <span data-ttu-id="e732b-156">**Abilitazione**</span><span class="sxs-lookup"><span data-stu-id="e732b-156">**Enable**</span></span> | <span data-ttu-id="e732b-157">Rinnova il dominio del servizio App automaticamente ogni anno.</span><span class="sxs-lookup"><span data-stu-id="e732b-157">Renews your App Service Domain automatically every year.</span></span> <span data-ttu-id="e732b-158">Viene addebitata sulla carta di credito hello stesso prezzo di acquisto in fase di hello del rinnovo.</span><span class="sxs-lookup"><span data-stu-id="e732b-158">Your credit card is charged hello same purchase price at hello time of renewal.</span></span> |
|<span data-ttu-id="e732b-159">Protezione della privacy</span><span class="sxs-lookup"><span data-stu-id="e732b-159">Privacy protection</span></span> | <span data-ttu-id="e732b-160">Abilita</span><span class="sxs-lookup"><span data-stu-id="e732b-160">Enable</span></span> | <span data-ttu-id="e732b-161">Consente di partecipare troppo "Protezione", che è incluso nel prezzo di acquisto hello _gratuitamente_ (ad eccezione di domini di primo livello cui Registro di sistema non supporta la protezione della privacy, ad esempio _. co.in_, _. Co.uk_e così via).</span><span class="sxs-lookup"><span data-stu-id="e732b-161">Opt in too"Privacy protection", which is included in hello purchase price _for free_ (except for top-level domains whose registry do not support privacy protection, such as _.co.in_, _.co.uk_, and so on).</span></span> |
| <span data-ttu-id="e732b-162">Assegnare i nomi host predefiniti</span><span class="sxs-lookup"><span data-stu-id="e732b-162">Assign default hostnames</span></span> | <span data-ttu-id="e732b-163">**www** e **@**</span><span class="sxs-lookup"><span data-stu-id="e732b-163">**www** and **@**</span></span> | <span data-ttu-id="e732b-164">Seleziona hello desiderato le associazioni nome host, se necessario.</span><span class="sxs-lookup"><span data-stu-id="e732b-164">Select hello desired hostname bindings, if desired.</span></span> <span data-ttu-id="e732b-165">Una volta completata l'operazione di acquisto hello dominio, l'app web accessibili in nomi host hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="e732b-165">When hello domain purchase operation is complete, your web app can be accessed at hello selected hostnames.</span></span> <span data-ttu-id="e732b-166">Se l'applicazione web hello è protetto da [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), non viene visualizzato il dominio radice hello di hello opzione tooassign (@), perché Gestione traffico non non supporto un record.</span><span class="sxs-lookup"><span data-stu-id="e732b-166">If hello web app is behind [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), you don't see hello option tooassign hello root domain (@), because Traffic Manager does not support A records.</span></span> <span data-ttu-id="e732b-167">È possibile apportare modifiche toohello hostname assegnazioni al termine dell'acquisto dominio hello.</span><span class="sxs-lookup"><span data-stu-id="e732b-167">You can make changes toohello hostname assignments after hello domain purchase completes.</span></span> |

### <a name="accept-terms-and-purchase"></a><span data-ttu-id="e732b-168">Accettare i termini di acquisto</span><span class="sxs-lookup"><span data-stu-id="e732b-168">Accept terms and purchase</span></span>

<span data-ttu-id="e732b-169">Fare clic su **legali** termini hello tooreview hello spese e, quindi fare clic su **acquistare**.</span><span class="sxs-lookup"><span data-stu-id="e732b-169">Click **Legal Terms** tooreview hello terms and hello charges, then click **Buy**.</span></span>

> [!NOTE]
> <span data-ttu-id="e732b-170">I domini del servizio App utilizzano domini di hello toohost di DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="e732b-170">App Service Domains use Azure DNS toohost hello domains.</span></span> <span data-ttu-id="e732b-171">Inoltre toohello tassa di registrazione di dominio, si applicano gli addebiti di utilizzo per DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="e732b-171">In addition toohello domain registration fee, usage charges for Azure DNS apply.</span></span> <span data-ttu-id="e732b-172">Per altre informazioni, vedere la pagina relativa ai [prezzi del DNS di Azure](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="e732b-172">For information, see [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>
>
>

<span data-ttu-id="e732b-173">In hello **dominio del servizio App** pagina, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e732b-173">Back in hello **App Service Domain** page, click **OK**.</span></span> <span data-ttu-id="e732b-174">Durante l'operazione di hello è in corso, vedrai hello seguendo le notifiche:</span><span class="sxs-lookup"><span data-stu-id="e732b-174">While hello operation is in progress, you see hello following notifications:</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-hello-hostnames"></a><span data-ttu-id="e732b-175">Nomi host hello di test</span><span class="sxs-lookup"><span data-stu-id="e732b-175">Test hello hostnames</span></span>

<span data-ttu-id="e732b-176">Se è stato assegnato l'impostazione predefinita i nomi host tooyour web app, è inoltre possibile visualizzare una notifica di esito positivo per ogni nome di host selezionati.</span><span class="sxs-lookup"><span data-stu-id="e732b-176">If you have assigned default hostnames tooyour web app, you also see a success notification for each selected hostname.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

<span data-ttu-id="e732b-177">È inoltre visualizzare i nomi host hello selezionato in hello **i domini personalizzati** pagina hello **i nomi host** sezione.</span><span class="sxs-lookup"><span data-stu-id="e732b-177">You also see hello selected hostnames in hello **Custom domains** page, in hello **Hostnames** section.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

<span data-ttu-id="e732b-178">i nomi host hello tootest, passare i nomi host toohello elencato nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="e732b-178">tootest hello hostnames, navigate toohello listed hostnames in hello browser.</span></span> <span data-ttu-id="e732b-179">Nell'esempio hello in hello precedente schermata, tenta di spostarsi too_kontoso.net_ e _www.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="e732b-179">In hello example in hello preceding screenshot, try navigating too_kontoso.net_ and _www.kontoso.net_.</span></span>

## <a name="assign-hostnames-tooweb-app"></a><span data-ttu-id="e732b-180">Assegnare i nomi host tooweb app</span><span class="sxs-lookup"><span data-stu-id="e732b-180">Assign hostnames tooweb app</span></span>

<span data-ttu-id="e732b-181">Se si sceglie di non tooassign uno o più nomi host tooyour web app predefinita hello durante il processo di acquisto, o se è necessario un nome host tooassign non elencati, è possibile assegnare un nome host in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="e732b-181">If you choose not tooassign one or more default hostnames tooyour web app during hello purchase process, or if you need tooassign a hostname not listed, you can assign a hostname at anytime.</span></span>

<span data-ttu-id="e732b-182">È inoltre possibile assegnare i nomi host negli hello dominio del servizio App tooany altre app web.</span><span class="sxs-lookup"><span data-stu-id="e732b-182">You can also assign hostnames in hello App Service Domain tooany other web app.</span></span> <span data-ttu-id="e732b-183">Hello passaggi variano a seconda se hello dominio del servizio App e app web hello appartengono toohello stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="e732b-183">hello steps depend on whether hello App Service Domain and hello web app belong toohello same subscription.</span></span>

- <span data-ttu-id="e732b-184">Sottoscrizione diversa: eseguire il mapping di record DNS personalizzati dall'app web di hello dominio del servizio App toohello Analogamente a un dominio esternamente acquistato.</span><span class="sxs-lookup"><span data-stu-id="e732b-184">Different subscription: Map custom DNS records from hello App Service Domain toohello web app like an externally purchased domain.</span></span> <span data-ttu-id="e732b-185">Per informazioni sull'aggiunta di DNS personalizzato dei nomi di dominio del servizio App tooan, vedere [gestire i record DNS personalizzati](#custom).</span><span class="sxs-lookup"><span data-stu-id="e732b-185">For information on adding custom DNS names tooan App Service Domain, see [Manage custom DNS records](#custom).</span></span> <span data-ttu-id="e732b-186">toomap un'app web tooa dominio acquistate esterno, vedere [mappare un esistente personalizzato DNS nome tooAzure App Web](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="e732b-186">toomap an external purchased domain tooa web app, see [Map an existing custom DNS name tooAzure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span> 
- <span data-ttu-id="e732b-187">Stessa sottoscrizione: hello utilizzare alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="e732b-187">Same subscription: Use hello following steps.</span></span>

### <a name="launch-add-hostname"></a><span data-ttu-id="e732b-188">Avviare Aggiungi nome host</span><span class="sxs-lookup"><span data-stu-id="e732b-188">Launch add hostname</span></span>
<span data-ttu-id="e732b-189">In hello **servizi App** pagina, il nome di hello selezionare dell'app web che si desidera tooassign nomi host, selezionare **impostazioni**, quindi selezionare **i domini personalizzati**.</span><span class="sxs-lookup"><span data-stu-id="e732b-189">In hello **App Services** page, select hello name of your web app that you want tooassign hostnames to, select **Settings**, and then select **Custom domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

<span data-ttu-id="e732b-190">Assicurarsi che il dominio acquistato sia elencato in hello **domini del servizio App** sezione senza selezionarla.</span><span class="sxs-lookup"><span data-stu-id="e732b-190">Make sure that your purchased domain is listed in hello **App Service Domains** section, but don't select it.</span></span> 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> <span data-ttu-id="e732b-191">Tutti i domini di servizio App hello nella stessa sottoscrizione dell'app web hello **i domini personalizzati** pagina.</span><span class="sxs-lookup"><span data-stu-id="e732b-191">All App Service Domains in hello same subscription are shown in hello web app's **Custom domains** page.</span></span> <span data-ttu-id="e732b-192">Se il dominio è nella sottoscrizione dell'app web hello, ma non è possibile visualizzare in app web hello **i domini personalizzati** pagina, provare a riaprire hello **i domini personalizzati** pagina o aggiornare la pagina Web hello.</span><span class="sxs-lookup"><span data-stu-id="e732b-192">If your domain is in hello web app's subscription, but you cannot see it in hello web app's **Custom domains** page, try reopening hello **Custom domains** page or refresh hello webpage.</span></span> <span data-ttu-id="e732b-193">Controllare inoltre a campana hello notifica nella parte superiore di hello di hello portale di Azure per gli errori di creazione o lo stato di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="e732b-193">Also, check hello notification bell at hello top of hello Azure portal for progress or creation failures.</span></span>
>
>

<span data-ttu-id="e732b-194">Selezionare **Aggiungi il nome host**.</span><span class="sxs-lookup"><span data-stu-id="e732b-194">Select **Add hostname**.</span></span>

### <a name="configure-hostname"></a><span data-ttu-id="e732b-195">Configurare il nome host</span><span class="sxs-lookup"><span data-stu-id="e732b-195">Configure hostname</span></span>
<span data-ttu-id="e732b-196">In hello **aggiungere hostname** finestra di dialogo, hello dominio completo del tipo il dominio del servizio App o un sottodominio.</span><span class="sxs-lookup"><span data-stu-id="e732b-196">In hello **Add hostname** dialog, type hello fully qualified domain name of your App Service Domain or any subdomain.</span></span> <span data-ttu-id="e732b-197">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e732b-197">For example:</span></span>

- <span data-ttu-id="e732b-198">kontoso.net</span><span class="sxs-lookup"><span data-stu-id="e732b-198">kontoso.net</span></span>
- <span data-ttu-id="e732b-199">www.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="e732b-199">www.kontoso.net</span></span>
- <span data-ttu-id="e732b-200">abc.kontoso.net</span><span class="sxs-lookup"><span data-stu-id="e732b-200">abc.kontoso.net</span></span>

<span data-ttu-id="e732b-201">Al termine, selezionare **Convalida**.</span><span class="sxs-lookup"><span data-stu-id="e732b-201">When finished, select **Validate**.</span></span> <span data-ttu-id="e732b-202">tipo di record hostname Hello viene selezionato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e732b-202">hello hostname record type is automatically selected for you.</span></span>

<span data-ttu-id="e732b-203">Selezionare **Aggiungi il nome host**.</span><span class="sxs-lookup"><span data-stu-id="e732b-203">Select **Add hostname**.</span></span>

<span data-ttu-id="e732b-204">Quando l'operazione di hello è stata completata, viene visualizzata una notifica di esito positivo per hello assegnato il nome host.</span><span class="sxs-lookup"><span data-stu-id="e732b-204">When hello operation is complete, you see a success notification for hello assigned hostname.</span></span>  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a><span data-ttu-id="e732b-205">Chiudere Aggiungi il nome host</span><span class="sxs-lookup"><span data-stu-id="e732b-205">Close add hostname</span></span>
<span data-ttu-id="e732b-206">In hello **aggiungere hostname** pagina, assegnare a qualsiasi altra nome host tooyour app web, in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="e732b-206">In hello **Add hostname** page, assign any other hostname tooyour web app, as desired.</span></span> <span data-ttu-id="e732b-207">Al termine, chiudere hello **aggiungere hostname** pagina.</span><span class="sxs-lookup"><span data-stu-id="e732b-207">When finished, close hello **Add hostname** page.</span></span>

<span data-ttu-id="e732b-208">Dovrebbe essere hostname(s) hello appena assegnato dell'app **i domini personalizzati** pagina.</span><span class="sxs-lookup"><span data-stu-id="e732b-208">You should now see hello newly assigned hostname(s) in your app's **Custom domains** page.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-hello-hostnames"></a><span data-ttu-id="e732b-209">Nomi host hello di test</span><span class="sxs-lookup"><span data-stu-id="e732b-209">Test hello hostnames</span></span>

<span data-ttu-id="e732b-210">Passare i nomi host toohello elencato nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="e732b-210">Navigate toohello listed hostnames in hello browser.</span></span> <span data-ttu-id="e732b-211">Nell'esempio hello nella precedente schermata hello, provare a passare too_abc.kontoso.net_.</span><span class="sxs-lookup"><span data-stu-id="e732b-211">In hello example in hello preceding screenshot, try navigating too_abc.kontoso.net_.</span></span>

<a name="custom" />

## <a name="manage-custom-dns-records"></a><span data-ttu-id="e732b-212">Gestire i record DNS personalizzati</span><span class="sxs-lookup"><span data-stu-id="e732b-212">Manage custom DNS records</span></span>

<span data-ttu-id="e732b-213">In Azure, i record DNS per un dominio del servizio app vengono gestiti tramite [DNS di Azure](https://azure.microsoft.com/services/dns/).</span><span class="sxs-lookup"><span data-stu-id="e732b-213">In Azure, DNS records for an App Service Domain are managed using [Azure DNS](https://azure.microsoft.com/services/dns/).</span></span> <span data-ttu-id="e732b-214">È possibile aggiungere, rimuovere e aggiornare i record DNS, esattamente come per un dominio acquistato esternamente.</span><span class="sxs-lookup"><span data-stu-id="e732b-214">You can add, remove, and update DNS records, just like for an externally purchased domain.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="e732b-215">Aprire Dominio del servizio app</span><span class="sxs-lookup"><span data-stu-id="e732b-215">Open App Service Domain</span></span>

<span data-ttu-id="e732b-216">Nel portale di Azure, dal menu a sinistra di hello, hello selezionare **più servizi** > **domini del servizio App**.</span><span class="sxs-lookup"><span data-stu-id="e732b-216">In hello Azure portal, from hello left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="e732b-217">Selezionare toomanage dominio hello.</span><span class="sxs-lookup"><span data-stu-id="e732b-217">Select hello domain toomanage.</span></span> 

### <a name="access-dns-zone"></a><span data-ttu-id="e732b-218">Accesso alla Zona DNS</span><span class="sxs-lookup"><span data-stu-id="e732b-218">Access DNS zone</span></span>

<span data-ttu-id="e732b-219">Nel menu a sinistra del dominio hello, selezionare **zona DNS**.</span><span class="sxs-lookup"><span data-stu-id="e732b-219">In hello domain's left menu, select **DNS zone**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

<span data-ttu-id="e732b-220">Questa azione apre hello [zona DNS](../dns/dns-zones-records.md) pagina del servizio App dominio in DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="e732b-220">This action opens hello [DNS zone](../dns/dns-zones-records.md) page of your App Service Domain in Azure DNS.</span></span> <span data-ttu-id="e732b-221">Per informazioni su come i record DNS tooedit, vedere [come zone DNS toomanage hello Azure portal](../dns/dns-operations-dnszones-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e732b-221">For information on how tooedit DNS records, see [How toomanage DNS Zones in hello Azure portal](../dns/dns-operations-dnszones-portal.md).</span></span>

## <a name="cancel-purchase-delete-domain"></a><span data-ttu-id="e732b-222">Annullare l'acquisto (elimina dominio)</span><span class="sxs-lookup"><span data-stu-id="e732b-222">Cancel purchase (delete domain)</span></span>

<span data-ttu-id="e732b-223">Dopo aver acquistato hello dominio dell'applicazione del servizio, è necessario toocancel cinque giorni l'acquisto per un rimborso completo.</span><span class="sxs-lookup"><span data-stu-id="e732b-223">After you purchase hello App Service Domain, you have five days toocancel your purchase for a full refund.</span></span> <span data-ttu-id="e732b-224">Dopo cinque giorni, è possibile eliminare hello dominio del servizio App, ma non è possibile ricevere un rimborso.</span><span class="sxs-lookup"><span data-stu-id="e732b-224">After five days, you can delete hello App Service Domain, but cannot receive a refund.</span></span>

### <a name="open-app-service-domain"></a><span data-ttu-id="e732b-225">Aprire Dominio del servizio app</span><span class="sxs-lookup"><span data-stu-id="e732b-225">Open App Service Domain</span></span>

<span data-ttu-id="e732b-226">Nel portale di Azure, dal menu a sinistra di hello, hello selezionare **più servizi** > **domini del servizio App**.</span><span class="sxs-lookup"><span data-stu-id="e732b-226">In hello Azure portal, from hello left menu, select **More Services** > **App Service Domains**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

<span data-ttu-id="e732b-227">Selezionare hello dominio tooyou desidera toocancel o eliminare.</span><span class="sxs-lookup"><span data-stu-id="e732b-227">Select hello domain tooyou want toocancel or delete.</span></span> 

### <a name="delete-hostname-bindings"></a><span data-ttu-id="e732b-228">Eliminare associazioni nome host</span><span class="sxs-lookup"><span data-stu-id="e732b-228">Delete hostname bindings</span></span>

<span data-ttu-id="e732b-229">Nel menu a sinistra del dominio hello, selezionare **le associazioni nome host**.</span><span class="sxs-lookup"><span data-stu-id="e732b-229">In hello domain's left menu, select **Hostname bindings**.</span></span> <span data-ttu-id="e732b-230">le associazioni nome host Hello da tutti i servizi Azure sono elencate di seguito.</span><span class="sxs-lookup"><span data-stu-id="e732b-230">hello hostname bindings from all Azure services are listed here.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

<span data-ttu-id="e732b-231">È possibile eliminare hello dominio dell'applicazione del servizio vengono eliminate tutte le associazioni nome host.</span><span class="sxs-lookup"><span data-stu-id="e732b-231">You cannot delete hello App Service Domain until all hostname bindings are deleted.</span></span>

<span data-ttu-id="e732b-232">Eliminare le associazioni nome host selezionando **...** > **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="e732b-232">Delete each hostname binding by selecting **...** > **Delete**.</span></span> <span data-ttu-id="e732b-233">Dopo l'eliminazione di tutte le associazioni hello, selezionare **salvare**.</span><span class="sxs-lookup"><span data-stu-id="e732b-233">After all hello bindings are deleted, select **Save**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a><span data-ttu-id="e732b-234">Annullare o eliminare</span><span class="sxs-lookup"><span data-stu-id="e732b-234">Cancel or delete</span></span>

<span data-ttu-id="e732b-235">Nel menu a sinistra del dominio hello, selezionare **Panoramica**.</span><span class="sxs-lookup"><span data-stu-id="e732b-235">In hello domain's left menu, select **Overview**.</span></span> 

<span data-ttu-id="e732b-236">Se il periodo di annullamento hello sul dominio hello acquistato non è trascorso, selezionare **annullare acquisto**.</span><span class="sxs-lookup"><span data-stu-id="e732b-236">If hello cancellation period on hello purchased domain has not elapsed, select **Cancel purchase**.</span></span> <span data-ttu-id="e732b-237">In caso contrario, viene visualizzato il pulsante **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="e732b-237">Otherwise, you see a **Delete** button instead.</span></span> <span data-ttu-id="e732b-238">dominio hello toodelete senza restituzione, seleziona **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="e732b-238">toodelete hello domain without a refund, select **Delete**.</span></span>

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

<span data-ttu-id="e732b-239">Selezionare **OK** operazione hello tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="e732b-239">Select **OK** tooconfirm hello operation.</span></span> <span data-ttu-id="e732b-240">Se non si desidera tooproceed, fare clic all'esterno di finestra di dialogo Conferma hello.</span><span class="sxs-lookup"><span data-stu-id="e732b-240">If you don't want tooproceed, click anywhere outside of hello confirmation dialog.</span></span>

<span data-ttu-id="e732b-241">Una volta completata l'operazione di hello, dominio hello è stato rilasciato dalla sottoscrizione e disponibile per tutti gli utenti toopurchase nuovamente.</span><span class="sxs-lookup"><span data-stu-id="e732b-241">After hello operation is complete, hello domain is released from your subscription and available for anyone toopurchase again.</span></span> 
