---
title: Personalizzare le regole del web application firewall nel gateway applicazione Azure - PowerShell | Microsoft Docs
description: Questo articolo descrive come personalizzare le regole del web application firewall nel gateway applicazione con PowerShell.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: 681625e40035b05c593c6161236cb80b7db576b9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-powershell"></a><span data-ttu-id="2e0f3-103">Personalizzare le regole del web application firewall con PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e0f3-103">Customize web application firewall rules through PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2e0f3-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2e0f3-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="2e0f3-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e0f3-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="2e0f3-106">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="2e0f3-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="2e0f3-107">Il Web application firewall del gateway applicazione di Azure (WAF) fornisce la protezione per le Applicazioni Web.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="2e0f3-108">Queste protezioni vengono fornite dal Set di regole principali (CRS) di Open Web Application Security Project (OWASP).</span><span class="sxs-lookup"><span data-stu-id="2e0f3-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="2e0f3-109">Alcune regole possono generare falsi positivi e bloccare il traffico reale.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="2e0f3-110">Per questo motivo, il gateway applicazione offre la possibilità di personalizzare regole e gruppi di regole.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="2e0f3-111">Per altre informazioni su regole e gruppi di regole specifici, vedere l'[Elenco di regole e gruppi di regole CRS del Web application firewall](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="2e0f3-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS Rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="2e0f3-112">Visualizzare le regole e i gruppi di regole</span><span class="sxs-lookup"><span data-stu-id="2e0f3-112">View rule groups and rules</span></span>

<span data-ttu-id="2e0f3-113">Gli esempi di codice seguenti illustrano come visualizzare le regole e i gruppi di regole configurabili in un gateway applicazione abilitato per il web application firewall (WAF).</span><span class="sxs-lookup"><span data-stu-id="2e0f3-113">The following code examples show how to view rules and rule groups that are configurable on a WAF-enabled application gateway.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="2e0f3-114">Visualizzare i gruppi di regole</span><span class="sxs-lookup"><span data-stu-id="2e0f3-114">View rule groups</span></span>

<span data-ttu-id="2e0f3-115">L'esempio seguente mostra come visualizzare i gruppi di regole:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-115">The following example shows how to view rule groups:</span></span>

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

<span data-ttu-id="2e0f3-116">Di seguito è riportata una parte di risposta dell'esempio precedente:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-116">The following output is a truncated response from the preceding example:</span></span>

```
OWASP (Ver. 3.0):

    REQUEST-910-IP-REPUTATION:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            910011     Rule 910011
            910012     Rule 910012
            ...        ...

    REQUEST-911-METHOD-ENFORCEMENT:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            911011     Rule 911011
            ...        ...

OWASP (Ver. 2.2.9):

    crs_20_protocol_violations:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            960911     Invalid HTTP Request Line
            981227     Apache Error: Invalid URI in Request.
            960000     Attempted multipart/form-data bypass
            ...        ...
```

## <a name="disable-rules"></a><span data-ttu-id="2e0f3-117">Disabilitare le regole</span><span class="sxs-lookup"><span data-stu-id="2e0f3-117">Disable rules</span></span>

<span data-ttu-id="2e0f3-118">L'esempio seguente disabilita le regole `910018` e `910017` in un gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="2e0f3-118">The following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="2e0f3-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2e0f3-119">Next steps</span></span>

<span data-ttu-id="2e0f3-120">Dopo aver configurato le regole disattivate, viene descritto come visualizzare i log WAF.</span><span class="sxs-lookup"><span data-stu-id="2e0f3-120">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="2e0f3-121">Per altre informazioni, vedere [Diagnostica del gateway applicazione](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="2e0f3-121">For more information, see [Application Gateway Diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
