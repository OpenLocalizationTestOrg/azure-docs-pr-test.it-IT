---
title: integrazione di Gateway con Centro sicurezza di Azure aaaApplication | Documenti Microsoft
description: Questa pagina include informazioni sull'integrazione del gateway applicazione nel Centro sicurezza di Azure.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: e5ea5cf9-3b41-4b85-a12c-e758bff7f3ec
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 06/07/2017
ms.author: gwallace
ms.openlocfilehash: 6f6ace105e84c01f525ab02938e81ce040c5c9d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a><span data-ttu-id="ba812-103">Panoramica dell'integrazione tra il gateway applicazione e il Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="ba812-103">Overview of integration between Application Gateway and Azure Security Center</span></span>

<span data-ttu-id="ba812-104">Informazioni sulla protezione delle risorse dell'applicazione Web tramite il gateway applicazione e il Centro sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba812-104">Learn how Application Gateway and Security Center help protect your web application resources.</span></span> <span data-ttu-id="ba812-105">Firewall applicazione web di Application gateway (WAF) si integra con [Centro sicurezza PC](../security-center/security-center-intro.md) tooprovide tooprevent una semplice visualizzazione, rilevare e rispondere toothreats toounprotected applicazioni nell'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="ba812-105">Application gateway web application firewall (WAF) integrates with [Security Center](../security-center/security-center-intro.md) tooprovide a seamless view tooprevent, detect and respond toothreats toounprotected web applications in your environment.</span></span>

## <a name="overview"></a><span data-ttu-id="ba812-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ba812-106">Overview</span></span>

<span data-ttu-id="ba812-107">Il WAF del gateway applicazione è una raccomandazione del Centro sicurezza per la protezione delle applicazioni Web da attacchi e vulnerabilità.</span><span class="sxs-lookup"><span data-stu-id="ba812-107">Application Gateway WAF is a recommendation in Security Center for protecting web applications from exploits and vulnerabilities.</span></span> <span data-ttu-id="ba812-108">Risorse Web abilitato che non sono protetti da WAF mostrano nel Centro protezione hello come indicazioni di alto livello di gravità.</span><span class="sxs-lookup"><span data-stu-id="ba812-108">Web enabled resources that are not protected by WAF show in hello security center as high severity recommendations.</span></span> <span data-ttu-id="ba812-109">Consigli per i firewall applicazione web vengono visualizzati nella hello **Panoramica** pagina **applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ba812-109">Recommendations for web application firewalls are shown on hello **Overview** page, under **Applications**.</span></span>

![integrazione con il Centro sicurezza][1]

<span data-ttu-id="ba812-111">Fare clic su qualsiasi indicazioni relative al firewall applicazione web consente di aprire un nuovo pannello con dettagli hello della raccomandazione hello.</span><span class="sxs-lookup"><span data-stu-id="ba812-111">Clicking any recommendations regarding web application firewall opens a new blade showing hello details of hello recommendation.</span></span>

## <a name="add-a-web-application-firewall-tooan-existing-resource"></a><span data-ttu-id="ba812-112">Aggiungere una risorsa esistente web application firewall tooan</span><span class="sxs-lookup"><span data-stu-id="ba812-112">Add a web application firewall tooan existing resource</span></span>

<span data-ttu-id="ba812-113">Passare troppo**più servizi** > **sicurezza + identità** > **Centro sicurezza PC** e hello **Centro sicurezza PC - Panoramica**  pannello, fare clic su **applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="ba812-113">Navigate too**More Services** > **Security + Identity** > **Security Center** and on hello **Security Center - Overview** blade, click **Applications**.</span></span> <span data-ttu-id="ba812-114">In hello **Centro sicurezza PC - applicazioni** pannello tabella hello contiene un elenco di applicazioni che Centro sicurezza rilevato nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ba812-114">On hello **Security Center - Applications** blade, hello table contains a list of applications that Security Center detected in your subscription.</span></span>

![applicazioni Web][3]

<span data-ttu-id="ba812-116">Facendo clic su un'applicazione web con un problema grave, viene visualizzato hello **l'integrità della protezione applicazione** blade.</span><span class="sxs-lookup"><span data-stu-id="ba812-116">By clicking on a web application with a critical issue, you get hello **Application security health** blade.</span></span> <span data-ttu-id="ba812-117">Nella seguente figura hello hello applicazione web che non è protetto da un firewall applicazione web.</span><span class="sxs-lookup"><span data-stu-id="ba812-117">In hello image below, hello web application that is not protected by a web application firewall.</span></span> 

![risorse Web non protette][2]

<span data-ttu-id="ba812-119">Fare clic su **aggiunge un firewall applicazione web** in **indicazioni** tooopen hello **aggiungere una Web Application Firewall** blade.</span><span class="sxs-lookup"><span data-stu-id="ba812-119">Click **Add a web application firewall** under **Recommendations** tooopen hello **Add a Web Application Firewall** blade.</span></span>

<span data-ttu-id="ba812-120">Se non si dispone di un Gateway applicazione esistente o desidera toocreate uno nuovo, fare clic su **Crea nuovo** e hello **creare un nuovo Web Application Firewall** pannello e fare clic su **Microsoft - Gateway applicazione**.</span><span class="sxs-lookup"><span data-stu-id="ba812-120">If you do not have an existing Application Gateway, or want toocreate a new one, click **Create New** and on hello **Create a new Web Application Firewall** blade, and click **Microsoft - Application Gateway**.</span></span> <span data-ttu-id="ba812-121">Verrà visualizzata tramite hello passaggi toocreate un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="ba812-121">This takes you through hello steps toocreate an application gateway.</span></span> <span data-ttu-id="ba812-122">A questo punto, l'applicazione Web viene aggiunta come risorsa protetta e il Centro sicurezza rileva che la risorsa è protetta da un web application firewall.</span><span class="sxs-lookup"><span data-stu-id="ba812-122">At this point, your web application is added as a protected resource, Security Center now tracks that this resource is protected by a web application firewall.</span></span> <span data-ttu-id="ba812-123">La risorsa non viene aggiunta come membro del pool back-end.</span><span class="sxs-lookup"><span data-stu-id="ba812-123">This does not add it as a backend pool member.</span></span>

<span data-ttu-id="ba812-124">Se è presente un gateway applicazione, è possibile selezionarlo in **Usa la soluzione esistente**</span><span class="sxs-lookup"><span data-stu-id="ba812-124">If you have an existing application gateway, you can choose it under **Use existing solution**</span></span>

![pannello di aggiunta di web application firewall][4]

<span data-ttu-id="ba812-126">Aggiunta di un gateway di applicazione tooan applicazione web tramite il Centro sicurezza PC non risorse hello come un membro del pool back-end, questa operazione deve essere eseguita sulla risorsa di gateway applicazione hello direttamente.</span><span class="sxs-lookup"><span data-stu-id="ba812-126">Adding a web application tooan application gateway through Security Center does not add hello resource as a backend pool member, this must be done on hello application gateway resource directly.</span></span>

## <a name="add-a-resource-tooan-existing-web-application-firewall"></a><span data-ttu-id="ba812-127">Aggiungere un risorsa tooan web dell'applicazione del firewall esistente</span><span class="sxs-lookup"><span data-stu-id="ba812-127">Add a resource tooan existing web application firewall</span></span>

<span data-ttu-id="ba812-128">Passare troppo**più servizi** > **sicurezza + identità** > **Centro sicurezza PC** e hello **Centro sicurezza PC - Panoramica**  pannello, fare clic su **soluzioni Partner**.</span><span class="sxs-lookup"><span data-stu-id="ba812-128">Navigate too**More Services** > **Security + Identity** > **Security Center** and on hello **Security Center - Overview** blade, click **Partner solutions**.</span></span> <span data-ttu-id="ba812-129">Mostrano i gateway di applicazione compatibile con il Centro sicurezza PC esistenti in hello **soluzioni dei Partner** blade.</span><span class="sxs-lookup"><span data-stu-id="ba812-129">Existing Security Center aware application gateways show in hello **Partner Solutions** blade.</span></span>

![soluzioni partner][7]

<span data-ttu-id="ba812-131">Fare clic su **collegamento app** tooopen hello **collegamento applicazioni** pannello qui vengono fornite applicazioni di hello opzioni tooselect esistenti.</span><span class="sxs-lookup"><span data-stu-id="ba812-131">Click **Link app** tooopen hello **Link Applications** blade, here you are given hello options tooselect existing applications.</span></span> <span data-ttu-id="ba812-132">Scegliere tooprotect applicazioni hello e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ba812-132">Choose hello applications tooprotect and click **OK**.</span></span> <span data-ttu-id="ba812-133">Non aggiunge hello toohello back-end pool di applicazioni web del gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ba812-133">This does not add hello web application toohello backend pool of hello application gateway.</span></span> <span data-ttu-id="ba812-134">Consente di impostare le risorse di hello come una risorsa protetta in modo da Centro sicurezza PC sia possibile tenere traccia.</span><span class="sxs-lookup"><span data-stu-id="ba812-134">This sets hello resources as a protected resource so Security Center can track it.</span></span> <span data-ttu-id="ba812-135">risorsa di hello tooadd come un membro del pool back-end, questa operazione deve essere eseguita nel gateway applicazione hello, dal pannello corrente hello è possibile fare clic su **console soluzione** toobe eseguite resource di gateway applicazione toohello in cui è possibile aggiungere web hello pool di applicazioni toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="ba812-135">tooadd hello resource as a backend pool member, this must be done on hello application gateway, from hello current blade you can click **Solution console** toobe taken toohello application gateway resource where you can add hello web application toohello backend pool.</span></span>

![applicazioni di soluzioni partner][6]

## <a name="finalize-configuration"></a><span data-ttu-id="ba812-137">Completare la configurazione</span><span class="sxs-lookup"><span data-stu-id="ba812-137">Finalize configuration</span></span>

<span data-ttu-id="ba812-138">Centro sicurezza PC tiene traccia delle applicazioni aggiunto gateway applicazione tooan come una risorsa protetta.</span><span class="sxs-lookup"><span data-stu-id="ba812-138">Security Center tracks applications added tooan application gateway as a protected resource.</span></span>  <span data-ttu-id="ba812-139">Monitorato lo stato di hello della risorsa e si assicura che è protetta da un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="ba812-139">It monitors hello health of this resource and ensures that it is protected by an application gateway.</span></span> <span data-ttu-id="ba812-140">passaggio successivo Hello è tooadd hello private IP, indirizzo IP pubblico o scheda NIC del pool back-end di toohello di macchina virtuale di gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="ba812-140">hello next step is tooadd hello private IP, public IP, or NIC of your virtual machine toohello backend pool of hello application gateway.</span></span> <span data-ttu-id="ba812-141">Fino a quando questa operazione viene eseguita un'indicazione aggiuntiva di **Finalizza la protezione di applicazione** viene visualizzato solo dopo l'aggiunta di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="ba812-141">Until this is done an additional recommendation of **Finalize application protection** is shown until hello resource is added.</span></span>

![pannello di aggiunta di web application firewall][5]

## <a name="security-alerts"></a><span data-ttu-id="ba812-143">Avvisi di sicurezza</span><span class="sxs-lookup"><span data-stu-id="ba812-143">Security Alerts</span></span>

<span data-ttu-id="ba812-144">All'interno di Centro sicurezza PC passare troppo**rilevamento** > **degli avvisi di sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="ba812-144">Within Security Center navigate too**DETECTION** > **Security Alerts**.</span></span>  <span data-ttu-id="ba812-145">Vengono visualizzati gli avvisi WAF per i gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="ba812-145">Here you find WAF alerts for your application gateways.</span></span> <span data-ttu-id="ba812-146">Gli avvisi sono suddivisi per regola WAF.</span><span class="sxs-lookup"><span data-stu-id="ba812-146">Alerts are broken down by WAF rule.</span></span>

![avvisi di sicurezza][8]

<span data-ttu-id="ba812-148">Fare clic su una regola per visualizzare un elenco degli avvisi per la regola WAF specifica.</span><span class="sxs-lookup"><span data-stu-id="ba812-148">Clicking an rule will provide a list of alerts for that specific WAF rule.</span></span> <span data-ttu-id="ba812-149">Ogni avviso Mostra ulteriori informazioni su come trovare hello.</span><span class="sxs-lookup"><span data-stu-id="ba812-149">Each alert shows additional details on hello finding.</span></span> <span data-ttu-id="ba812-150">Dettagli Hello forniscono un gateway applicazione toohello di collegamento.</span><span class="sxs-lookup"><span data-stu-id="ba812-150">hello details provide a link toohello application gateway.</span></span>
 
![dettagli dell'avviso][9]

## <a name="next-steps"></a><span data-ttu-id="ba812-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ba812-152">Next steps</span></span>

<span data-ttu-id="ba812-153">toolearn come tooenable firewall di applicazione web su un gateway applicazione esistente, visitare [crea o aggiorna un Gateway applicazione Azure con firewall applicazione web](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span><span class="sxs-lookup"><span data-stu-id="ba812-153">toolearn how tooenable web application firewall on an existing application gateway, visit [Create or update an Azure Application Gateway with web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span></span>

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png