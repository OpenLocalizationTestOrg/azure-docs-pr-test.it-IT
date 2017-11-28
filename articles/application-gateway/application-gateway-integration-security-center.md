---
title: Integrazione del gateway applicazione con il Centro sicurezza di Azure | Microsoft Docs
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
ms.openlocfilehash: 737cdff3140be68cf9d6d396b470dd09c65c52f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a><span data-ttu-id="9cf7d-103">Panoramica dell'integrazione tra il gateway applicazione e il Centro sicurezza di Azure</span><span class="sxs-lookup"><span data-stu-id="9cf7d-103">Overview of integration between Application Gateway and Azure Security Center</span></span>

<span data-ttu-id="9cf7d-104">Informazioni sulla protezione delle risorse dell'applicazione Web tramite il gateway applicazione e il Centro sicurezza di Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-104">Learn how Application Gateway and Security Center help protect your web application resources.</span></span> <span data-ttu-id="9cf7d-105">Il web application firewall (WAF) del gateway applicazione è integrato nel [Centro sicurezza](../security-center/security-center-intro.md) per offrire alle applicazioni Web non protette dell'ambiente una visualizzazione semplice per prevenire, rilevare e rispondere alle minacce.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-105">Application gateway web application firewall (WAF) integrates with [Security Center](../security-center/security-center-intro.md) to provide a seamless view to prevent, detect and respond to threats to unprotected web applications in your environment.</span></span>

## <a name="overview"></a><span data-ttu-id="9cf7d-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="9cf7d-106">Overview</span></span>

<span data-ttu-id="9cf7d-107">Il WAF del gateway applicazione è una raccomandazione del Centro sicurezza per la protezione delle applicazioni Web da attacchi e vulnerabilità.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-107">Application Gateway WAF is a recommendation in Security Center for protecting web applications from exploits and vulnerabilities.</span></span> <span data-ttu-id="9cf7d-108">Le risorse abilitate per il Web non protette da WAF sono visualizzate nel Centro sicurezza come raccomandazioni con gravità elevata.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-108">Web enabled resources that are not protected by WAF show in the security center as high severity recommendations.</span></span> <span data-ttu-id="9cf7d-109">Le raccomandazioni per i web application firewall sono visualizzate nella pagina **Panoramica** in **Applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-109">Recommendations for web application firewalls are shown on the **Overview** page, under **Applications**.</span></span>

![integrazione con il Centro sicurezza][1]

<span data-ttu-id="9cf7d-111">Se si fa clic su una raccomandazione relativa a web application firewall, viene aperto un nuovo pannello che visualizza i dettagli della raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-111">Clicking any recommendations regarding web application firewall opens a new blade showing the details of the recommendation.</span></span>

## <a name="add-a-web-application-firewall-to-an-existing-resource"></a><span data-ttu-id="9cf7d-112">Aggiungere un web application firewall a una risorsa esistente</span><span class="sxs-lookup"><span data-stu-id="9cf7d-112">Add a web application firewall to an existing resource</span></span>

<span data-ttu-id="9cf7d-113">Passare ad **Altri servizi** > **Sicurezza e identità** > **Centro sicurezza PC** e nel pannello **Centro sicurezza PC - Panoramica** fare clic su **Applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-113">Navigate to **More Services** > **Security + Identity** > **Security Center** and on the **Security Center - Overview** blade, click **Applications**.</span></span> <span data-ttu-id="9cf7d-114">La tabella nel pannello **Centro sicurezza PC - Applicazioni** contiene un elenco delle applicazioni rilevate dal Centro sicurezza nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-114">On the **Security Center - Applications** blade, the table contains a list of applications that Security Center detected in your subscription.</span></span>

![applicazioni Web][3]

<span data-ttu-id="9cf7d-116">Se si fa clic su un'applicazione Web con un problema critico, viene visualizzato il pannello **Integrità della sicurezza dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-116">By clicking on a web application with a critical issue, you get the **Application security health** blade.</span></span> <span data-ttu-id="9cf7d-117">Nell'immagine seguente è illustrata l'applicazione Web che non è protetta da un web application firewall.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-117">In the image below, the web application that is not protected by a web application firewall.</span></span> 

![risorse Web non protette][2]

<span data-ttu-id="9cf7d-119">Fare clic su **Aggiungi un web application firewall** in **Raccomandazioni** per aprire il pannello **Aggiungi un web application firewall**.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-119">Click **Add a web application firewall** under **Recommendations** to open the **Add a Web Application Firewall** blade.</span></span>

<span data-ttu-id="9cf7d-120">Se non è presente un gateway applicazione o si vuole crearne uno nuovo, fare clic su **Crea nuovo** e nel pannello **Nuovo web application firewall** fare clic su **Microsoft - Gateway applicazione**.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-120">If you do not have an existing Application Gateway, or want to create a new one, click **Create New** and on the **Create a new Web Application Firewall** blade, and click **Microsoft - Application Gateway**.</span></span> <span data-ttu-id="9cf7d-121">Vengono descritti i passaggi per la creazione di un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-121">This takes you through the steps to create an application gateway.</span></span> <span data-ttu-id="9cf7d-122">A questo punto, l'applicazione Web viene aggiunta come risorsa protetta e il Centro sicurezza rileva che la risorsa è protetta da un web application firewall.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-122">At this point, your web application is added as a protected resource, Security Center now tracks that this resource is protected by a web application firewall.</span></span> <span data-ttu-id="9cf7d-123">La risorsa non viene aggiunta come membro del pool back-end.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-123">This does not add it as a backend pool member.</span></span>

<span data-ttu-id="9cf7d-124">Se è presente un gateway applicazione, è possibile selezionarlo in **Usa la soluzione esistente**</span><span class="sxs-lookup"><span data-stu-id="9cf7d-124">If you have an existing application gateway, you can choose it under **Use existing solution**</span></span>

![pannello di aggiunta di web application firewall][4]

<span data-ttu-id="9cf7d-126">Poiché l'aggiunta di un'applicazione Web a un gateway applicazione tramite il Centro sicurezza non aggiunge la risorsa come membro del pool back-end, questa operazione deve essere eseguita direttamente nella risorsa del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-126">Adding a web application to an application gateway through Security Center does not add the resource as a backend pool member, this must be done on the application gateway resource directly.</span></span>

## <a name="add-a-resource-to-an-existing-web-application-firewall"></a><span data-ttu-id="9cf7d-127">Aggiungere una risorsa a un web application firewall esistente</span><span class="sxs-lookup"><span data-stu-id="9cf7d-127">Add a resource to an existing web application firewall</span></span>

<span data-ttu-id="9cf7d-128">Passare ad **Altri servizi** > **Sicurezza e identità** > **Centro sicurezza PC** e nel pannello **Centro sicurezza PC - Panoramica** fare clic su **Soluzioni partner**.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-128">Navigate to **More Services** > **Security + Identity** > **Security Center** and on the **Security Center - Overview** blade, click **Partner solutions**.</span></span> <span data-ttu-id="9cf7d-129">I gateway applicazione compatibili con il Centro sicurezza esistenti sono visualizzati nel pannello **Soluzioni partner**.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-129">Existing Security Center aware application gateways show in the **Partner Solutions** blade.</span></span>

![soluzioni partner][7]

<span data-ttu-id="9cf7d-131">Fare clic su **Collega app** per aprire il pannello **Collega applicazioni** nel quale sarà possibile selezionare le applicazioni esistenti.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-131">Click **Link app** to open the **Link Applications** blade, here you are given the options to select existing applications.</span></span> <span data-ttu-id="9cf7d-132">Scegliere le applicazioni da proteggere e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-132">Choose the applications to protect and click **OK**.</span></span> <span data-ttu-id="9cf7d-133">Questa operazione non aggiunge l'applicazione Web al pool back-end del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-133">This does not add the web application to the backend pool of the application gateway.</span></span> <span data-ttu-id="9cf7d-134">ma imposta la risorsa come risorsa protetta in modo che il Centro sicurezza possa rilevarla.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-134">This sets the resources as a protected resource so Security Center can track it.</span></span> <span data-ttu-id="9cf7d-135">Per aggiungere la risorsa come membro del pool back-end è necessario eseguire questa operazione nel gateway applicazione: dal pannello corrente fare clic su **Console della soluzione** per passare alla risorsa del gateway applicazione nella quale è possibile aggiungere l'applicazione Web al pool back-end.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-135">To add the resource as a backend pool member, this must be done on the application gateway, from the current blade you can click **Solution console** to be taken to the application gateway resource where you can add the web application to the backend pool.</span></span>

![applicazioni di soluzioni partner][6]

## <a name="finalize-configuration"></a><span data-ttu-id="9cf7d-137">Completare la configurazione</span><span class="sxs-lookup"><span data-stu-id="9cf7d-137">Finalize configuration</span></span>

<span data-ttu-id="9cf7d-138">Il Centro sicurezza rileva le applicazioni aggiunte a un gateway applicazione come risorse protette.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-138">Security Center tracks applications added to an application gateway as a protected resource.</span></span>  <span data-ttu-id="9cf7d-139">Il Centro sicurezza monitora l'integrità della risorsa e verifica che sia protetta da un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-139">It monitors the health of this resource and ensures that it is protected by an application gateway.</span></span> <span data-ttu-id="9cf7d-140">Il passaggio successivo consiste nell'aggiungere l'IP privato, l'IP pubblico o la scheda di interfaccia di rete della macchina virtuale al pool back-end del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-140">The next step is to add the private IP, public IP, or NIC of your virtual machine to the backend pool of the application gateway.</span></span> <span data-ttu-id="9cf7d-141">Prima del completamento del passaggio, viene visualizzata la raccomandazione aggiuntiva **Finalizza la protezione dell'applicazione** fino a quando la risorsa non viene aggiunta.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-141">Until this is done an additional recommendation of **Finalize application protection** is shown until the resource is added.</span></span>

![pannello di aggiunta di web application firewall][5]

## <a name="security-alerts"></a><span data-ttu-id="9cf7d-143">Avvisi di sicurezza</span><span class="sxs-lookup"><span data-stu-id="9cf7d-143">Security Alerts</span></span>

<span data-ttu-id="9cf7d-144">In Centro sicurezza passare a **RILEVAMENTO** > **Avvisi di sicurezza**.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-144">Within Security Center navigate to **DETECTION** > **Security Alerts**.</span></span>  <span data-ttu-id="9cf7d-145">Vengono visualizzati gli avvisi WAF per i gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-145">Here you find WAF alerts for your application gateways.</span></span> <span data-ttu-id="9cf7d-146">Gli avvisi sono suddivisi per regola WAF.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-146">Alerts are broken down by WAF rule.</span></span>

![avvisi di sicurezza][8]

<span data-ttu-id="9cf7d-148">Fare clic su una regola per visualizzare un elenco degli avvisi per la regola WAF specifica.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-148">Clicking an rule will provide a list of alerts for that specific WAF rule.</span></span> <span data-ttu-id="9cf7d-149">Ogni avviso visualizza dettagli aggiuntivi sull'elemento individuato.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-149">Each alert shows additional details on the finding.</span></span> <span data-ttu-id="9cf7d-150">I dettagli includono un collegamento al gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="9cf7d-150">The details provide a link to the application gateway.</span></span>
 
![dettagli dell'avviso][9]

## <a name="next-steps"></a><span data-ttu-id="9cf7d-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9cf7d-152">Next steps</span></span>

<span data-ttu-id="9cf7d-153">Per informazioni su come abilitare il web application firewall in un gateway applicazione esistente, vedere [Creare o aggiornare un gateway applicazione di Azure con web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span><span class="sxs-lookup"><span data-stu-id="9cf7d-153">To learn how to enable web application firewall on an existing application gateway, visit [Create or update an Azure Application Gateway with web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span></span>

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png