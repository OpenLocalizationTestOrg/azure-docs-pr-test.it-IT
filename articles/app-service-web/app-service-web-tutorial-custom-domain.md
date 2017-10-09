---
title: aaaMap un DNS personalizzato esistente nome app Web tooAzure | Documenti Microsoft
description: Informazioni su come tooadd un dominio DNS personalizzato esistente nome app web di tooa (dominio personale), back-end dell'app mobile o app per le API in Azure App Service.
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
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a><span data-ttu-id="9b997-103">Eseguire il mapping di un esistente personalizzato DNS nome tooAzure App Web</span><span class="sxs-lookup"><span data-stu-id="9b997-103">Map an existing custom DNS name tooAzure Web Apps</span></span>

<span data-ttu-id="9b997-104">Le [app Web di Azure](app-service-web-overview.md) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="9b997-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="9b997-105">Questa esercitazione viene illustrato come assegnare un nome app Web tooAzure toomap un DNS personalizzato esistente.</span><span class="sxs-lookup"><span data-stu-id="9b997-105">This tutorial shows you how toomap an existing custom DNS name tooAzure Web Apps.</span></span>

![Spostamento del portale tooAzure app](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

<span data-ttu-id="9b997-107">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="9b997-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9b997-108">Eseguire il mapping di un sottodominio (ad esempio, `www.contoso.com`) usando un record CNAME</span><span class="sxs-lookup"><span data-stu-id="9b997-108">Map a subdomain (for example, `www.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="9b997-109">Eseguire il mapping di un dominio radice (ad esempio, `contoso.com`) usando un record A</span><span class="sxs-lookup"><span data-stu-id="9b997-109">Map a root domain (for example, `contoso.com`) by using an A record</span></span>
> * <span data-ttu-id="9b997-110">Eseguire il mapping di un dominio con caratteri jolly (ad esempio, `*.contoso.com`) usando un record CNAME</span><span class="sxs-lookup"><span data-stu-id="9b997-110">Map a wildcard domain (for example, `*.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="9b997-111">Automatizzare il mapping dei domini con script</span><span class="sxs-lookup"><span data-stu-id="9b997-111">Automate domain mapping with scripts</span></span>

<span data-ttu-id="9b997-112">È possibile utilizzare un **record CNAME** o **un record** toomap un DNS personalizzato nome tooApp servizio.</span><span class="sxs-lookup"><span data-stu-id="9b997-112">You can use either a **CNAME record** or an **A record** toomap a custom DNS name tooApp Service.</span></span> 

> [!NOTE]
> <span data-ttu-id="9b997-113">È consigliabile usare un record CNAME per tutti i nomi DNS personalizzati tranne il dominio radice (ad esempio, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="9b997-113">We recommend that you use a CNAME for all custom DNS names except a root domain (for example, `contoso.com`).</span></span>

<span data-ttu-id="9b997-114">toomigrate un sito in tempo reale e il relativo tooApp nome di dominio DNS del servizio, vedere [eseguire la migrazione di un tooAzure di nome DNS del servizio App active](app-service-custom-domain-name-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="9b997-114">toomigrate a live site and its DNS domain name tooApp Service, see [Migrate an active DNS name tooAzure App Service](app-service-custom-domain-name-migrate.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b997-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9b997-115">Prerequisites</span></span>

<span data-ttu-id="9b997-116">toocomplete questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="9b997-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="9b997-117">[Creare un'app del servizio app](/azure/app-service/) oppure usare un'app creata per un'altra esercitazione.</span><span class="sxs-lookup"><span data-stu-id="9b997-117">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>
* <span data-ttu-id="9b997-118">Acquistare un nome di dominio e assicurarsi di disporre del Registro di sistema di accesso toohello DNS per il provider del dominio (ad esempio GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="9b997-118">Purchase a domain name and make sure you have access toohello DNS registry for your domain provider (such as GoDaddy).</span></span>

  <span data-ttu-id="9b997-119">Ad esempio, le voci DNS tooadd per `contoso.com` e `www.contoso.com`, è necessario essere in grado di tooconfigure hello impostazioni DNS hello `contoso.com` dominio radice.</span><span class="sxs-lookup"><span data-stu-id="9b997-119">For example, tooadd DNS entries for `contoso.com` and `www.contoso.com`, you must be able tooconfigure hello DNS settings for hello `contoso.com` root domain.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9b997-120">Se non è un dominio esistente nome, prendere in considerazione [acquisto di un dominio utilizzando hello Azure portal](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="9b997-120">If you don't have an existing domain name, consider [purchasing a domain using hello Azure portal](custom-dns-web-site-buydomains-web-app.md).</span></span> 

## <a name="prepare-hello-app"></a><span data-ttu-id="9b997-121">Preparare l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="9b997-121">Prepare hello app</span></span>

<span data-ttu-id="9b997-122">toomap un personalizzato DNS nome tooa dell'app web, app web hello [piano di servizio App](https://azure.microsoft.com/pricing/details/app-service/) deve essere un livello a pagamento (**Shared**, **base**, **Standard**, o  **Premium**).</span><span class="sxs-lookup"><span data-stu-id="9b997-122">toomap a custom DNS name tooa web app, hello web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="9b997-123">In questo passaggio assicurarsi che il servizio App app è in hello hello supportato piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="9b997-123">In this step, you make sure that hello App Service app is in hello supported pricing tier.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="9b997-124">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="9b997-124">Sign in tooAzure</span></span>

<span data-ttu-id="9b997-125">Aprire hello [portale di Azure](https://portal.azure.com) e accedere con l'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="9b997-125">Open hello [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-toohello-app-in-hello-azure-portal"></a><span data-ttu-id="9b997-126">Passare toohello app nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="9b997-126">Navigate toohello app in hello Azure portal</span></span>

<span data-ttu-id="9b997-127">Scegliere dal menu a sinistra hello **servizi App**e quindi selezionare il nome di hello di app hello.</span><span class="sxs-lookup"><span data-stu-id="9b997-127">From hello left menu, select **App Services**, and then select hello name of hello app.</span></span>

![Spostamento del portale tooAzure app](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="9b997-129">Verrà visualizzata hello pagina di gestione di app del servizio App hello.</span><span class="sxs-lookup"><span data-stu-id="9b997-129">You see hello management page of hello App Service app.</span></span>  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="9b997-130">Controllo hello piano tariffario</span><span class="sxs-lookup"><span data-stu-id="9b997-130">Check hello pricing tier</span></span>

<span data-ttu-id="9b997-131">Hello navigazione della pagina dell'app hello a sinistra, scorrere toohello **impostazioni** sezione e selezionare **scalabilità verticale (piano di servizio App)**.</span><span class="sxs-lookup"><span data-stu-id="9b997-131">In hello left navigation of hello app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menu di scalabilità verticale](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="9b997-133">livello corrente dell'applicazione Hello è evidenziato da un bordo blu.</span><span class="sxs-lookup"><span data-stu-id="9b997-133">hello app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="9b997-134">Verificare che tale applicazione hello non hello toomake **libero** livello.</span><span class="sxs-lookup"><span data-stu-id="9b997-134">Check toomake sure that hello app is not in hello **Free** tier.</span></span> <span data-ttu-id="9b997-135">DNS personalizzato non è supportato in hello **libero** livello.</span><span class="sxs-lookup"><span data-stu-id="9b997-135">Custom DNS is not supported in hello **Free** tier.</span></span> 

![Controllare il piano tariffario](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="9b997-137">Se hello piano di servizio App non è **libero**, chiudere hello **scegliere il piano tariffario** pagina e andare troppo[mapping di un record CNAME](#cname).</span><span class="sxs-lookup"><span data-stu-id="9b997-137">If hello App Service plan is not **Free**, close hello **Choose your pricing tier** page and skip too[Map a CNAME record](#cname).</span></span>

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a><span data-ttu-id="9b997-138">Applicare la scalabilità verticale hello piano di servizio App</span><span class="sxs-lookup"><span data-stu-id="9b997-138">Scale up hello App Service plan</span></span>

<span data-ttu-id="9b997-139">Selezionare uno dei livelli di hello non disponibili (**Shared**, **base**, **Standard**, o **Premium**).</span><span class="sxs-lookup"><span data-stu-id="9b997-139">Select any of hello non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="9b997-140">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="9b997-140">Click **Select**.</span></span>

![Controllare il piano tariffario](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="9b997-142">Quando viene visualizzata hello previa notifica, l'operazione di ridimensionamento hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="9b997-142">When you see hello following notification, hello scale operation is complete.</span></span>

![Conferma operazione di scalabilità](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a><span data-ttu-id="9b997-144">Esecuzione del mapping di un record CNAME</span><span class="sxs-lookup"><span data-stu-id="9b997-144">Map a CNAME record</span></span>

<span data-ttu-id="9b997-145">Nell'esempio di esercitazione hello, si aggiunge un record CNAME per hello `www` sottodominio (ad esempio, `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="9b997-145">In hello tutorial example, you add a CNAME record for hello `www` subdomain (for example, `www.contoso.com`).</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="9b997-146">Creare record CNAME hello</span><span class="sxs-lookup"><span data-stu-id="9b997-146">Create hello CNAME record</span></span>

<span data-ttu-id="9b997-147">Aggiungere un toomap record CNAME nome host predefinito dell'app un sottodominio toohello (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="9b997-147">Add a CNAME record toomap a subdomain toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="9b997-148">Per hello `www.contoso.com` esempio dominio, aggiungere un record CNAME che esegue il mapping nome hello `www` troppo`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="9b997-148">For hello `www.contoso.com` domain example, add a CNAME record that maps hello name `www` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="9b997-149">Dopo aver aggiunto hello CNAME, pagina record DNS di hello aspetto hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="9b997-149">After you add hello CNAME, hello DNS records page looks like hello following example:</span></span>

![Spostamento del portale tooAzure app](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a><span data-ttu-id="9b997-151">Abilitare il mapping di record CNAME hello in Azure</span><span class="sxs-lookup"><span data-stu-id="9b997-151">Enable hello CNAME record mapping in Azure</span></span>

<span data-ttu-id="9b997-152">Nel riquadro di spostamento della pagina app hello sinistro nel portale di Azure hello di hello, selezionare **i domini personalizzati**.</span><span class="sxs-lookup"><span data-stu-id="9b997-152">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Menu del dominio personalizzato](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="9b997-154">In hello **i domini personalizzati** pagina dell'applicazione hello, aggiungere hello personalizzato nome DNS completo (`www.contoso.com`) toohello elenco.</span><span class="sxs-lookup"><span data-stu-id="9b997-154">In hello **Custom domains** page of hello app, add hello fully qualified custom DNS name (`www.contoso.com`) toohello list.</span></span>

<span data-ttu-id="9b997-155">Seleziona hello  **+**  icona Avanti troppo**aggiungere hostname**.</span><span class="sxs-lookup"><span data-stu-id="9b997-155">Select hello **+** icon next too**Add hostname**.</span></span>

![Aggiunta del nome host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="9b997-157">Aggiungere un record CNAME per, ad esempio nome di dominio completo di tipo hello `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="9b997-157">Type hello fully qualified domain name that you added a CNAME record for, such as `www.contoso.com`.</span></span> 

<span data-ttu-id="9b997-158">Selezionare **Convalida**.</span><span class="sxs-lookup"><span data-stu-id="9b997-158">Select **Validate**.</span></span>

<span data-ttu-id="9b997-159">Hello **aggiungere hostname** pulsante è attivato.</span><span class="sxs-lookup"><span data-stu-id="9b997-159">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="9b997-160">Assicurarsi che **tipo di record Hostname** è troppo**CNAME (www.example.com o qualsiasi sottodominio)**.</span><span class="sxs-lookup"><span data-stu-id="9b997-160">Make sure that **Hostname record type** is set too**CNAME (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="9b997-161">Selezionare **Aggiungi il nome host**.</span><span class="sxs-lookup"><span data-stu-id="9b997-161">Select **Add hostname**.</span></span>

![Aggiungere app toohello di nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="9b997-163">Potrebbe richiedere del tempo hello nuovo nome host toobe riportate nella finestra dell'applicazione hello **i domini personalizzati** pagina.</span><span class="sxs-lookup"><span data-stu-id="9b997-163">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="9b997-164">Provare ad aggiornare dati hello tooupdate di hello del browser.</span><span class="sxs-lookup"><span data-stu-id="9b997-164">Try refreshing hello browser tooupdate hello data.</span></span>

![Record CNAME aggiunto](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="9b997-166">Se manca un passaggio o apportate a un errore di digitazione in un punto precedente, viene visualizzato un errore di verifica nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="9b997-166">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![Errore di verifica](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a><span data-ttu-id="9b997-168">Esecuzione del mapping di un record A</span><span class="sxs-lookup"><span data-stu-id="9b997-168">Map an A record</span></span>

<span data-ttu-id="9b997-169">Nell'esempio di esercitazione hello, aggiungere un record A per il dominio radice hello (ad esempio, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="9b997-169">In hello tutorial example, you add an A record for hello root domain (for example, `contoso.com`).</span></span> 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a><span data-ttu-id="9b997-170">Copiare l'indirizzo IP dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="9b997-170">Copy hello app's IP address</span></span>

<span data-ttu-id="9b997-171">toomap un record, è necessario un indirizzo IP esterno dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9b997-171">toomap an A record, you need hello app's external IP address.</span></span> <span data-ttu-id="9b997-172">È possibile trovare questo indirizzo IP in app di hello **i domini personalizzati** pagina hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9b997-172">You can find this IP address in hello app's **Custom domains** page in hello Azure portal.</span></span>

<span data-ttu-id="9b997-173">Nel riquadro di spostamento della pagina app hello sinistro nel portale di Azure hello di hello, selezionare **i domini personalizzati**.</span><span class="sxs-lookup"><span data-stu-id="9b997-173">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Menu del dominio personalizzato](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="9b997-175">In hello **i domini personalizzati** copiare l'indirizzo IP dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9b997-175">In hello **Custom domains** page, copy hello app's IP address.</span></span>

![Spostamento del portale tooAzure app](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a><span data-ttu-id="9b997-177">Creare record hello</span><span class="sxs-lookup"><span data-stu-id="9b997-177">Create hello A record</span></span>

<span data-ttu-id="9b997-178">app tooan record toomap un servizio App richiede **due** record DNS:</span><span class="sxs-lookup"><span data-stu-id="9b997-178">toomap an A record tooan app, App Service requires **two** DNS records:</span></span>

- <span data-ttu-id="9b997-179">Un **A** registrare l'indirizzo IP dell'app toohello toomap.</span><span class="sxs-lookup"><span data-stu-id="9b997-179">An **A** record toomap toohello app's IP address.</span></span>
- <span data-ttu-id="9b997-180">Oggetto **TXT** record nome host predefinito dell'app toohello toomap `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="9b997-180">A **TXT** record toomap toohello app's default hostname `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="9b997-181">Servizio App Usa questo record solo in fase di configurazione, che si è proprietari di dominio personalizzato hello tooverify.</span><span class="sxs-lookup"><span data-stu-id="9b997-181">App Service uses this record only at configuration time, tooverify that you own hello custom domain.</span></span> <span data-ttu-id="9b997-182">Dopo che il dominio personalizzato è stato convalidato e configurato nel servizio app, è possibile eliminare il record TXT.</span><span class="sxs-lookup"><span data-stu-id="9b997-182">After your custom domain is validated and configured in App Service, you can delete this TXT record.</span></span> 

<span data-ttu-id="9b997-183">Per hello `contoso.com` esempio dominio, creare record TXT e in base toohello nella tabella seguente, hello (`@` in genere rappresenta hello dominio radice).</span><span class="sxs-lookup"><span data-stu-id="9b997-183">For hello `contoso.com` domain example, create hello A and TXT records according toohello following table (`@` typically represents hello root domain).</span></span> 

| <span data-ttu-id="9b997-184">Tipo di record</span><span class="sxs-lookup"><span data-stu-id="9b997-184">Record type</span></span> | <span data-ttu-id="9b997-185">Host</span><span class="sxs-lookup"><span data-stu-id="9b997-185">Host</span></span> | <span data-ttu-id="9b997-186">Valore</span><span class="sxs-lookup"><span data-stu-id="9b997-186">Value</span></span> |
| - | - | - |
| <span data-ttu-id="9b997-187">Una </span><span class="sxs-lookup"><span data-stu-id="9b997-187">A</span></span> | `@` | <span data-ttu-id="9b997-188">Indirizzo IP da [indirizzo IP dell'applicazione hello copia](#info)</span><span class="sxs-lookup"><span data-stu-id="9b997-188">IP address from [Copy hello app's IP address](#info)</span></span> |
| <span data-ttu-id="9b997-189">TXT</span><span class="sxs-lookup"><span data-stu-id="9b997-189">TXT</span></span> | `@` | `<app_name>.azurewebsites.net` |

<span data-ttu-id="9b997-190">Quando vengono aggiunti record hello, pagina record DNS hello aspetto hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="9b997-190">When hello records are added, hello DNS records page looks like hello following example:</span></span>

![Pagina dei record DNS](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a><span data-ttu-id="9b997-192">Abilitare un mapping di record nell'app hello hello</span><span class="sxs-lookup"><span data-stu-id="9b997-192">Enable hello A record mapping in hello app</span></span>

<span data-ttu-id="9b997-193">Dell'applicazione hello **i domini personalizzati** pagina hello portale di Azure, aggiungere hello personalizzato nome DNS completo (ad esempio, `contoso.com`) toohello elenco.</span><span class="sxs-lookup"><span data-stu-id="9b997-193">Back in hello app's **Custom domains** page in hello Azure portal, add hello fully qualified custom DNS name (for example, `contoso.com`) toohello list.</span></span>

<span data-ttu-id="9b997-194">Seleziona hello  **+**  icona Avanti troppo**aggiungere hostname**.</span><span class="sxs-lookup"><span data-stu-id="9b997-194">Select hello **+** icon next too**Add hostname**.</span></span>

![Aggiunta del nome host](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

<span data-ttu-id="9b997-196">Nome di dominio completo tipo hello è configurato il record A hello, ad esempio `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="9b997-196">Type hello fully qualified domain name that you configured hello A record for, such as `contoso.com`.</span></span>

<span data-ttu-id="9b997-197">Selezionare **Convalida**.</span><span class="sxs-lookup"><span data-stu-id="9b997-197">Select **Validate**.</span></span>

<span data-ttu-id="9b997-198">Hello **aggiungere hostname** pulsante è attivato.</span><span class="sxs-lookup"><span data-stu-id="9b997-198">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="9b997-199">Assicurarsi che **tipo di record Hostname** è troppo**un record (example.com)**.</span><span class="sxs-lookup"><span data-stu-id="9b997-199">Make sure that **Hostname record type** is set too**A record (example.com)**.</span></span>

<span data-ttu-id="9b997-200">Selezionare **Aggiungi il nome host**.</span><span class="sxs-lookup"><span data-stu-id="9b997-200">Select **Add hostname**.</span></span>

![Aggiungere app toohello di nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

<span data-ttu-id="9b997-202">Potrebbe richiedere del tempo hello nuovo nome host toobe riportate nella finestra dell'applicazione hello **i domini personalizzati** pagina.</span><span class="sxs-lookup"><span data-stu-id="9b997-202">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="9b997-203">Provare ad aggiornare dati hello tooupdate di hello del browser.</span><span class="sxs-lookup"><span data-stu-id="9b997-203">Try refreshing hello browser tooupdate hello data.</span></span>

![Record A aggiunto](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

<span data-ttu-id="9b997-205">Se manca un passaggio o apportate a un errore di digitazione in un punto precedente, viene visualizzato un errore di verifica nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="9b997-205">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![Errore di verifica](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a><span data-ttu-id="9b997-207">Esecuzione del mapping di un dominio con caratteri jolly</span><span class="sxs-lookup"><span data-stu-id="9b997-207">Map a wildcard domain</span></span>

<span data-ttu-id="9b997-208">Nell'esempio di esercitazione hello, si esegue il mapping un [nome DNS jolly](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (ad esempio, `*.contoso.com`) toohello app del servizio App aggiungendo un record CNAME.</span><span class="sxs-lookup"><span data-stu-id="9b997-208">In hello tutorial example, you map a [wildcard DNS name](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (for example, `*.contoso.com`) toohello App Service app by adding a CNAME record.</span></span> 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="9b997-209">Creare record CNAME hello</span><span class="sxs-lookup"><span data-stu-id="9b997-209">Create hello CNAME record</span></span>

<span data-ttu-id="9b997-210">Aggiungere un toomap record CNAME nome host predefinito dell'applicazione di toohello nome con caratteri jolly (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="9b997-210">Add a CNAME record toomap a wildcard name toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="9b997-211">Per hello `*.contoso.com` esempio dominio hello record CNAME verrà eseguito il mapping nome hello `*` troppo`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="9b997-211">For hello `*.contoso.com` domain example, hello CNAME record will map hello name `*` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="9b997-212">Quando viene aggiunto hello CNAME, pagina record DNS hello aspetto hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="9b997-212">When hello CNAME is added, hello DNS records page looks like hello following example:</span></span>

![Spostamento del portale tooAzure app](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a><span data-ttu-id="9b997-214">Abilitare il mapping di record CNAME hello in app hello</span><span class="sxs-lookup"><span data-stu-id="9b997-214">Enable hello CNAME record mapping in hello app</span></span>

<span data-ttu-id="9b997-215">È ora possibile aggiungere qualsiasi sottodominio corrispondente hello jolly nome toohello app (ad esempio, `sub1.contoso.com` e `sub2.contoso.com` corrispondono `*.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="9b997-215">You can now add any subdomain that matches hello wildcard name toohello app (for example, `sub1.contoso.com` and `sub2.contoso.com` match `*.contoso.com`).</span></span> 

<span data-ttu-id="9b997-216">Nel riquadro di spostamento della pagina app hello sinistro nel portale di Azure hello di hello, selezionare **i domini personalizzati**.</span><span class="sxs-lookup"><span data-stu-id="9b997-216">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Menu del dominio personalizzato](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="9b997-218">Seleziona hello  **+**  icona Avanti troppo**aggiungere hostname**.</span><span class="sxs-lookup"><span data-stu-id="9b997-218">Select hello **+** icon next too**Add hostname**.</span></span>

![Aggiunta del nome host](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="9b997-220">Digitare un nome di dominio completo corrispondente hello jolly dominio (ad esempio, `sub1.contoso.com`), quindi selezionare **convalida**.</span><span class="sxs-lookup"><span data-stu-id="9b997-220">Type a fully qualified domain name that matches hello wildcard domain (for example, `sub1.contoso.com`), and then select **Validate**.</span></span>

<span data-ttu-id="9b997-221">Hello **aggiungere hostname** pulsante è attivato.</span><span class="sxs-lookup"><span data-stu-id="9b997-221">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="9b997-222">Assicurarsi che **tipo di record Hostname** è troppo**record CNAME (www.example.com o qualsiasi sottodominio)**.</span><span class="sxs-lookup"><span data-stu-id="9b997-222">Make sure that **Hostname record type** is set too**CNAME record (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="9b997-223">Selezionare **Aggiungi il nome host**.</span><span class="sxs-lookup"><span data-stu-id="9b997-223">Select **Add hostname**.</span></span>

![Aggiungere app toohello di nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

<span data-ttu-id="9b997-225">Potrebbe richiedere del tempo hello nuovo nome host toobe riportate nella finestra dell'applicazione hello **i domini personalizzati** pagina.</span><span class="sxs-lookup"><span data-stu-id="9b997-225">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="9b997-226">Provare ad aggiornare dati hello tooupdate di hello del browser.</span><span class="sxs-lookup"><span data-stu-id="9b997-226">Try refreshing hello browser tooupdate hello data.</span></span>

<span data-ttu-id="9b997-227">Seleziona hello  **+**  icona tooadd nuovamente un altro nome host al dominio con caratteri jolly hello.</span><span class="sxs-lookup"><span data-stu-id="9b997-227">Select hello **+** icon again tooadd another hostname that matches hello wildcard domain.</span></span> <span data-ttu-id="9b997-228">Ad esempio, aggiungere `sub2.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="9b997-228">For example, add `sub2.contoso.com`.</span></span>

![Record CNAME aggiunto](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a><span data-ttu-id="9b997-230">Prova nel browser</span><span class="sxs-lookup"><span data-stu-id="9b997-230">Test in browser</span></span>

<span data-ttu-id="9b997-231">Individuare i nomi DNS toohello configurata in precedenza (ad esempio, `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, e `sub2.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="9b997-231">Browse toohello DNS name(s) that you configured earlier (for example, `contoso.com`,  `www.contoso.com`, `sub1.contoso.com`, and `sub2.contoso.com`).</span></span>

![Spostamento del portale tooAzure app](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a><span data-ttu-id="9b997-233">Automatizzazione con gli script</span><span class="sxs-lookup"><span data-stu-id="9b997-233">Automate with scripts</span></span>

<span data-ttu-id="9b997-234">È possibile automatizzare la gestione dei domini personalizzati con gli script, utilizzando hello [CLI di Azure](/cli/azure/install-azure-cli) o [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9b997-234">You can automate management of custom domains with scripts, using hello [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="azure-cli"></a><span data-ttu-id="9b997-235">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="9b997-235">Azure CLI</span></span> 

<span data-ttu-id="9b997-236">Hello comando seguente consente di aggiungere una configurazione personalizzata DNS nome tooan app del servizio App.</span><span class="sxs-lookup"><span data-stu-id="9b997-236">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

<span data-ttu-id="9b997-237">Per ulteriori informazioni, vedere [eseguire il mapping di un'app web di dominio personalizzato tooa](scripts/app-service-cli-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="9b997-237">For more information, see [Map a custom domain tooa web app](scripts/app-service-cli-configure-custom-domain.md).</span></span> 

### <a name="azure-powershell"></a><span data-ttu-id="9b997-238">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b997-238">Azure PowerShell</span></span> 

<span data-ttu-id="9b997-239">Hello comando seguente consente di aggiungere una configurazione personalizzata DNS nome tooan app del servizio App.</span><span class="sxs-lookup"><span data-stu-id="9b997-239">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

<span data-ttu-id="9b997-240">Per ulteriori informazioni, vedere [assegnare un'app web di dominio personalizzato tooa](scripts/app-service-powershell-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="9b997-240">For more information, see [Assign a custom domain tooa web app](scripts/app-service-powershell-configure-custom-domain.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b997-241">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9b997-241">Next steps</span></span>

<span data-ttu-id="9b997-242">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="9b997-242">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9b997-243">Eseguire il mapping di un sottodominio usando un record CNAME</span><span class="sxs-lookup"><span data-stu-id="9b997-243">Map a subdomain by using a CNAME record</span></span>
> * <span data-ttu-id="9b997-244">Eseguire il mapping di un dominio radice usando un record A</span><span class="sxs-lookup"><span data-stu-id="9b997-244">Map a root domain by using an A record</span></span>
> * <span data-ttu-id="9b997-245">Eseguire il mapping di un dominio con caratteri jolly usando un record CNAME</span><span class="sxs-lookup"><span data-stu-id="9b997-245">Map a wildcard domain by using a CNAME record</span></span>
> * <span data-ttu-id="9b997-246">Automatizzare il mapping dei domini con script</span><span class="sxs-lookup"><span data-stu-id="9b997-246">Automate domain mapping with scripts</span></span>

<span data-ttu-id="9b997-247">Spostare toolearn esercitazione successiva toohello come toobind un SSL personalizzato certificato tooa web app.</span><span class="sxs-lookup"><span data-stu-id="9b997-247">Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9b997-248">Associare un esistente personalizzato SSL certificato tooAzure App Web</span><span class="sxs-lookup"><span data-stu-id="9b997-248">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
