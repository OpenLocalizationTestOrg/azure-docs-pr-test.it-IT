---
title: Personalizzare regole del Web application firewall nel gateway applicazione di Azure - Portale di Azure | Microsoft Docs
description: Questo articolo descrive come personalizzare le regole del web application firewall nel gateway applicazione con il portale di Azure.
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
ms.openlocfilehash: cdcbadbc3765dfc583c26e1b1453863d421c9a72
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="f8a2c-103">Personalizzare le regole del web application firewall con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f8a2c-103">Customize web application firewall rules through the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f8a2c-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="f8a2c-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="f8a2c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8a2c-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="f8a2c-106">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="f8a2c-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="f8a2c-107">Il Web application firewall del gateway applicazione di Azure (WAF) fornisce la protezione per le Applicazioni Web.</span><span class="sxs-lookup"><span data-stu-id="f8a2c-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="f8a2c-108">Queste protezioni vengono fornite dal Set di regole principali (CRS) di Open Web Application Security Project (OWASP).</span><span class="sxs-lookup"><span data-stu-id="f8a2c-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="f8a2c-109">Alcune regole possono generare falsi positivi e bloccare il traffico reale.</span><span class="sxs-lookup"><span data-stu-id="f8a2c-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="f8a2c-110">Per questo motivo, il gateway applicazione offre la possibilità di personalizzare regole e gruppi di regole.</span><span class="sxs-lookup"><span data-stu-id="f8a2c-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="f8a2c-111">Per altre informazioni su regole e gruppi di regole specifici, vedere l'[Elenco di regole e gruppi di regole CRS del Web application firewall](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="f8a2c-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

>[!NOTE]
> <span data-ttu-id="f8a2c-112">Se il gateway applicazione non sta usando il livello WAF, l'opzione per aggiornare il gateway applicazione al livello WAF, come visualizzato nel riquadro a destra.</span><span class="sxs-lookup"><span data-stu-id="f8a2c-112">If your application gateway is not using the WAF tier, the option to upgrade the application gateway to the WAF tier appears in the right pane.</span></span> 

![Abilitare WAF][fig1]

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="f8a2c-114">Visualizzare le regole e i gruppi di regole</span><span class="sxs-lookup"><span data-stu-id="f8a2c-114">View rule groups and rules</span></span>

<span data-ttu-id="f8a2c-115">**Visualizzare le regole e i gruppi di regole**</span><span class="sxs-lookup"><span data-stu-id="f8a2c-115">**To view rule groups and rules**</span></span>
   1. <span data-ttu-id="f8a2c-116">Esplorare il gateway applicazione, e quindi selezionare **Web application firewall**.</span><span class="sxs-lookup"><span data-stu-id="f8a2c-116">Browse to the application gateway, and then select **Web application firewall**.</span></span>  
   2. <span data-ttu-id="f8a2c-117">Selezionare **Advanced rule configuration** (Configurazione regole avanzata).</span><span class="sxs-lookup"><span data-stu-id="f8a2c-117">Select **Advanced rule configuration**.</span></span>  
   <span data-ttu-id="f8a2c-118">Questa visualizzazione mostra una tabella nella pagina di tutti i gruppi di regole forniti con il set di regole selezionato.</span><span class="sxs-lookup"><span data-stu-id="f8a2c-118">This view shows a table on the page of all the rule groups provided with the chosen rule set.</span></span> <span data-ttu-id="f8a2c-119">Vengono selezionate tutte le caselle di controllo della regola.</span><span class="sxs-lookup"><span data-stu-id="f8a2c-119">All of the rule's check boxes are selected.</span></span>

![Configurare regole disabilitate][1]

## <a name="search-for-rules-to-disable"></a><span data-ttu-id="f8a2c-121">Ricerca di regole da disabilitare</span><span class="sxs-lookup"><span data-stu-id="f8a2c-121">Search for rules to disable</span></span>

<span data-ttu-id="f8a2c-122">Il pannello delle **Impostazioni del Web application firewall** offre la possibilità di filtrare le regole tramite una ricerca di testo.</span><span class="sxs-lookup"><span data-stu-id="f8a2c-122">The **Web application firewall settings** blade provides the capability to filter the rules through a text search.</span></span> <span data-ttu-id="f8a2c-123">Il risultato visualizza solo le regole e i gruppi di regole contenenti il testo ricercato.</span><span class="sxs-lookup"><span data-stu-id="f8a2c-123">The result displays only the rule groups and rules that contain the text you searched for.</span></span>

![Cercare le regole][2]

## <a name="disable-rule-groups-and-rules"></a><span data-ttu-id="f8a2c-125">Disabilitare le regole e i gruppi di regole</span><span class="sxs-lookup"><span data-stu-id="f8a2c-125">Disable rule groups and rules</span></span>

<span data-ttu-id="f8a2c-126">Quando si disabilitano le regole, è possibile disabilitare un intero gruppo di regole o regole specifiche in uno o più gruppi di regole.</span><span class="sxs-lookup"><span data-stu-id="f8a2c-126">When your're disabling rules, you can disable an entire rule group or specific rules under one or more rule groups.</span></span> 

<span data-ttu-id="f8a2c-127">**Disabilitare gruppi di regole o regole specifiche**</span><span class="sxs-lookup"><span data-stu-id="f8a2c-127">**To disable rule groups or specific rules**</span></span>

   1. <span data-ttu-id="f8a2c-128">Cercare le regole o i gruppi di regole che si desidera disabilitare.</span><span class="sxs-lookup"><span data-stu-id="f8a2c-128">Search for the rules or rule groups that you want to disable.</span></span>
   2. <span data-ttu-id="f8a2c-129">Deselezionare le caselle di controllo per le regole che si desidera disabilitare.</span><span class="sxs-lookup"><span data-stu-id="f8a2c-129">Clear the check boxes for the rules that you want to disable.</span></span> 
   2. <span data-ttu-id="f8a2c-130">Selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f8a2c-130">Select **Save**.</span></span> 

![Salvare le modifiche][3]

## <a name="next-steps"></a><span data-ttu-id="f8a2c-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f8a2c-132">Next steps</span></span>

<span data-ttu-id="f8a2c-133">Dopo aver configurato le regole disattivate, viene descritto come visualizzare i log WAF.</span><span class="sxs-lookup"><span data-stu-id="f8a2c-133">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="f8a2c-134">Per altre informazioni, vedere [Diagnostica del gateway applicazione](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="f8a2c-134">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
