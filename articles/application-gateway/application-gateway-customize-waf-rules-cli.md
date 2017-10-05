---
title: Personalizzare le regole del web application firewall nel gateway applicazione di Azure - Interfaccia della riga di comando di Azure 2.0 | Microsoft Docs
description: Questo articolo descrive come personalizzare le regole del web application firewall nel gateway applicazione con l'interfaccia della riga di comando di Azure 2.0.
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
ms.openlocfilehash: 456be048dc2d82cd50d145b71f17a84a7189ea96
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-the-azure-cli-20"></a><span data-ttu-id="c1b2d-103">Personalizzare le regole del web application firewall con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="c1b2d-103">Customize web application firewall rules through the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c1b2d-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c1b2d-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="c1b2d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1b2d-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="c1b2d-106">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="c1b2d-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="c1b2d-107">Il Web application firewall del gateway applicazione di Azure (WAF) fornisce la protezione per le Applicazioni Web.</span><span class="sxs-lookup"><span data-stu-id="c1b2d-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="c1b2d-108">Queste protezioni vengono fornite dal Set di regole principali (CRS) di Open Web Application Security Project (OWASP).</span><span class="sxs-lookup"><span data-stu-id="c1b2d-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="c1b2d-109">Alcune regole possono generare falsi positivi e bloccare il traffico reale.</span><span class="sxs-lookup"><span data-stu-id="c1b2d-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="c1b2d-110">Per questo motivo, il gateway applicazione offre la possibilità di personalizzare regole e gruppi di regole.</span><span class="sxs-lookup"><span data-stu-id="c1b2d-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="c1b2d-111">Per altre informazioni su regole e gruppi di regole specifici, vedere l'[Elenco di regole e gruppi di regole CRS del Web application firewall](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="c1b2d-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="c1b2d-112">Visualizzare le regole e i gruppi di regole</span><span class="sxs-lookup"><span data-stu-id="c1b2d-112">View rule groups and rules</span></span>

<span data-ttu-id="c1b2d-113">Gli esempi di codice seguenti illustrano come visualizzare le regole e i gruppi di regole configurabili.</span><span class="sxs-lookup"><span data-stu-id="c1b2d-113">The following code examples show how to view rules and rule groups that are configurable.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="c1b2d-114">Visualizzare i gruppi di regole</span><span class="sxs-lookup"><span data-stu-id="c1b2d-114">View rule groups</span></span>

<span data-ttu-id="c1b2d-115">L'esempio seguente mostra come visualizzare i gruppi di regole:</span><span class="sxs-lookup"><span data-stu-id="c1b2d-115">The following example shows how to view the rule groups:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

<span data-ttu-id="c1b2d-116">Di seguito è riportata una parte di risposta dell'esempio precedente:</span><span class="sxs-lookup"><span data-stu-id="c1b2d-116">The following output is a truncated response from the preceding example:</span></span>

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  },
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_2.2.9",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
   "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "crs_20_protocol_violations",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "2.2.9",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

### <a name="view-rules-in-a-rule-group"></a><span data-ttu-id="c1b2d-117">Visualizzare le regole in un gruppo di regole</span><span class="sxs-lookup"><span data-stu-id="c1b2d-117">View rules in a rule group</span></span>

<span data-ttu-id="c1b2d-118">L'esempio seguente mostra come visualizzare le regole in un gruppo di regole specificato:</span><span class="sxs-lookup"><span data-stu-id="c1b2d-118">The following example shows how to view rules in a specified rule group:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

<span data-ttu-id="c1b2d-119">Di seguito è riportata una parte di risposta dell'esempio precedente:</span><span class="sxs-lookup"><span data-stu-id="c1b2d-119">The following output is a truncated response from the preceding example:</span></span>

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": [
          {
            "description": "Rule 910011",
            "ruleId": 910011
          },
          ...
        ]
      }
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

## <a name="disable-rules"></a><span data-ttu-id="c1b2d-120">Disabilitare le regole</span><span class="sxs-lookup"><span data-stu-id="c1b2d-120">Disable rules</span></span>

<span data-ttu-id="c1b2d-121">L'esempio seguente disabilita le regole `910018` e `910017` in un gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="c1b2d-121">The following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="c1b2d-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c1b2d-122">Next steps</span></span>

<span data-ttu-id="c1b2d-123">Dopo aver configurato le regole disattivate, viene descritto come visualizzare i log WAF.</span><span class="sxs-lookup"><span data-stu-id="c1b2d-123">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="c1b2d-124">Per altre informazioni, vedere [Diagnostica del gateway applicazione](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="c1b2d-124">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
