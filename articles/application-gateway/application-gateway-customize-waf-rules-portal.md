---
title: regole del firewall applicazione web aaaCustomize in Gateway applicazione Azure - portale di Azure | Documenti Microsoft
description: Questo articolo fornisce informazioni sul funzionamento delle regole firewall di applicazione web toocustomize in Gateway applicazione con hello portale di Azure.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 1159500b-17ba-41e7-88d6-b96986795084
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: gwallace
ms.openlocfilehash: 36a999279e0370b9f803e12257856a56753b23a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="bb4e1-103">Personalizzare le regole di firewall applicazione web tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="bb4e1-103">Customize web application firewall rules through hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bb4e1-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="bb4e1-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="bb4e1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb4e1-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="bb4e1-106">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="bb4e1-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="bb4e1-107">firewall applicazione web di Hello Gateway applicazione Azure (WAF) fornisce protezione per le applicazioni web.</span><span class="sxs-lookup"><span data-stu-id="bb4e1-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="bb4e1-108">Queste protezioni sono fornite da hello aprire Web applicazione sicurezza progetto (OWASP) Core regola impostata (CR).</span><span class="sxs-lookup"><span data-stu-id="bb4e1-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="bb4e1-109">Alcune regole possono generare falsi positivi e bloccare il traffico reale.</span><span class="sxs-lookup"><span data-stu-id="bb4e1-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="bb4e1-110">Per questo motivo, il Gateway applicazione fornisce le regole e gruppi di regole toocustomize funzionalità hello.</span><span class="sxs-lookup"><span data-stu-id="bb4e1-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="bb4e1-111">Per ulteriori informazioni sui gruppi di regole specifici hello e sulle regole, vedere [elenco di regole e gruppi di regole CRS firewall applicazione web](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="bb4e1-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

>[!NOTE]
> <span data-ttu-id="bb4e1-112">Se il gateway applicazione non utilizza il livello di WAF hello, nel riquadro di destra hello hello opzione tooupgrade hello gateway toohello WAF livello applicazione.</span><span class="sxs-lookup"><span data-stu-id="bb4e1-112">If your application gateway is not using hello WAF tier, hello option tooupgrade hello application gateway toohello WAF tier appears in hello right pane.</span></span> 

![Abilitare WAF][fig1]

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="bb4e1-114">Visualizzare le regole e i gruppi di regole</span><span class="sxs-lookup"><span data-stu-id="bb4e1-114">View rule groups and rules</span></span>

<span data-ttu-id="bb4e1-115">**regole e gruppi di regole tooview**</span><span class="sxs-lookup"><span data-stu-id="bb4e1-115">**tooview rule groups and rules**</span></span>
   1. <span data-ttu-id="bb4e1-116">Gateway applicazione toohello Sfoglia e quindi selezionare **firewall applicazione Web**.</span><span class="sxs-lookup"><span data-stu-id="bb4e1-116">Browse toohello application gateway, and then select **Web application firewall**.</span></span>  
   2. <span data-ttu-id="bb4e1-117">Selezionare **Advanced rule configuration** (Configurazione regole avanzata).</span><span class="sxs-lookup"><span data-stu-id="bb4e1-117">Select **Advanced rule configuration**.</span></span>  
   <span data-ttu-id="bb4e1-118">Questa visualizzazione mostra una tabella nella pagina di hello di tutti i gruppi di regole hello fornito con hello scelto set di regole.</span><span class="sxs-lookup"><span data-stu-id="bb4e1-118">This view shows a table on hello page of all hello rule groups provided with hello chosen rule set.</span></span> <span data-ttu-id="bb4e1-119">Tutte le caselle di controllo della regola hello sono selezionate.</span><span class="sxs-lookup"><span data-stu-id="bb4e1-119">All of hello rule's check boxes are selected.</span></span>

![Configurare regole disabilitate][1]

## <a name="search-for-rules-toodisable"></a><span data-ttu-id="bb4e1-121">Cerca regole toodisable</span><span class="sxs-lookup"><span data-stu-id="bb4e1-121">Search for rules toodisable</span></span>

<span data-ttu-id="bb4e1-122">Hello **impostazioni firewall applicazione Web** pannello sono disponibili funzionalità hello toofilter hello regole tramite una ricerca di testo.</span><span class="sxs-lookup"><span data-stu-id="bb4e1-122">hello **Web application firewall settings** blade provides hello capability toofilter hello rules through a text search.</span></span> <span data-ttu-id="bb4e1-123">risultato Hello vengono visualizzati solo i gruppi di regole hello e regole che contengono testo hello che per effettuare la ricerca.</span><span class="sxs-lookup"><span data-stu-id="bb4e1-123">hello result displays only hello rule groups and rules that contain hello text you searched for.</span></span>

![Cercare le regole][2]

## <a name="disable-rule-groups-and-rules"></a><span data-ttu-id="bb4e1-125">Disabilitare le regole e i gruppi di regole</span><span class="sxs-lookup"><span data-stu-id="bb4e1-125">Disable rule groups and rules</span></span>

<span data-ttu-id="bb4e1-126">Quando si disabilitano le regole, è possibile disabilitare un intero gruppo di regole o regole specifiche in uno o più gruppi di regole.</span><span class="sxs-lookup"><span data-stu-id="bb4e1-126">When your're disabling rules, you can disable an entire rule group or specific rules under one or more rule groups.</span></span> 

<span data-ttu-id="bb4e1-127">**toodisable gruppi di regole o regole specifiche**</span><span class="sxs-lookup"><span data-stu-id="bb4e1-127">**toodisable rule groups or specific rules**</span></span>

   1. <span data-ttu-id="bb4e1-128">Ricerca di regole hello o gruppi di regole che si desidera toodisable.</span><span class="sxs-lookup"><span data-stu-id="bb4e1-128">Search for hello rules or rule groups that you want toodisable.</span></span>
   2. <span data-ttu-id="bb4e1-129">Deselezionare le caselle di controllo hello hello alle regole che si desidera toodisable.</span><span class="sxs-lookup"><span data-stu-id="bb4e1-129">Clear hello check boxes for hello rules that you want toodisable.</span></span> 
   2. <span data-ttu-id="bb4e1-130">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="bb4e1-130">Select **Save**.</span></span> 

![Salvare le modifiche][3]

## <a name="next-steps"></a><span data-ttu-id="bb4e1-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bb4e1-132">Next steps</span></span>

<span data-ttu-id="bb4e1-133">Dopo aver configurato le regole disabilitate, utili come tooview i log WAF.</span><span class="sxs-lookup"><span data-stu-id="bb4e1-133">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="bb4e1-134">Per altre informazioni, vedere [Diagnostica del gateway applicazione](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="bb4e1-134">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
