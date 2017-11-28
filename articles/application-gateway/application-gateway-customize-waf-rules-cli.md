---
title: regole del firewall applicazione web aaaCustomize in Gateway applicazione Azure - CLI di Azure 2.0 | Documenti Microsoft
description: Questo articolo fornisce informazioni sul funzionamento delle regole firewall di applicazione web toocustomize in Gateway applicazione con hello CLI di Azure 2.0.
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
ms.openlocfilehash: b83ffb9f6a7e0d0c8c970885d2bcb3b63d32581c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-cli-20"></a><span data-ttu-id="69332-103">Personalizzare le regole di firewall applicazione web tramite hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="69332-103">Customize web application firewall rules through hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="69332-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="69332-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="69332-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="69332-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="69332-106">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="69332-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="69332-107">firewall applicazione web di Hello Gateway applicazione Azure (WAF) fornisce protezione per le applicazioni web.</span><span class="sxs-lookup"><span data-stu-id="69332-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="69332-108">Queste protezioni sono fornite da hello aprire Web applicazione sicurezza progetto (OWASP) Core regola impostata (CR).</span><span class="sxs-lookup"><span data-stu-id="69332-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="69332-109">Alcune regole possono generare falsi positivi e bloccare il traffico reale.</span><span class="sxs-lookup"><span data-stu-id="69332-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="69332-110">Per questo motivo, il Gateway applicazione fornisce le regole e gruppi di regole toocustomize funzionalità hello.</span><span class="sxs-lookup"><span data-stu-id="69332-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="69332-111">Per ulteriori informazioni sui gruppi di regole specifici hello e sulle regole, vedere [elenco di regole e gruppi di regole CRS firewall applicazione web](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="69332-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="69332-112">Visualizzare le regole e i gruppi di regole</span><span class="sxs-lookup"><span data-stu-id="69332-112">View rule groups and rules</span></span>

<span data-ttu-id="69332-113">Hello esempi di codice seguente mostra come tooview regole regole e gruppi che possono essere configurati.</span><span class="sxs-lookup"><span data-stu-id="69332-113">hello following code examples show how tooview rules and rule groups that are configurable.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="69332-114">Visualizzare i gruppi di regole</span><span class="sxs-lookup"><span data-stu-id="69332-114">View rule groups</span></span>

<span data-ttu-id="69332-115">Hello di esempio seguente viene illustrato come tooview hello gruppi di regole:</span><span class="sxs-lookup"><span data-stu-id="69332-115">hello following example shows how tooview hello rule groups:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

<span data-ttu-id="69332-116">Dopo l'output di Hello è una risposta troncata da hello sopra riportato:</span><span class="sxs-lookup"><span data-stu-id="69332-116">hello following output is a truncated response from hello preceding example:</span></span>

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

### <a name="view-rules-in-a-rule-group"></a><span data-ttu-id="69332-117">Visualizzare le regole in un gruppo di regole</span><span class="sxs-lookup"><span data-stu-id="69332-117">View rules in a rule group</span></span>

<span data-ttu-id="69332-118">Hello di esempio seguente viene illustrato come tooview regole in un gruppo di regole specificato:</span><span class="sxs-lookup"><span data-stu-id="69332-118">hello following example shows how tooview rules in a specified rule group:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

<span data-ttu-id="69332-119">Dopo l'output di Hello è una risposta troncata da hello sopra riportato:</span><span class="sxs-lookup"><span data-stu-id="69332-119">hello following output is a truncated response from hello preceding example:</span></span>

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

## <a name="disable-rules"></a><span data-ttu-id="69332-120">Disabilitare le regole</span><span class="sxs-lookup"><span data-stu-id="69332-120">Disable rules</span></span>

<span data-ttu-id="69332-121">esempio Hello disabilita le regole `910018` e `910017` su un gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="69332-121">hello following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="69332-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="69332-122">Next steps</span></span>

<span data-ttu-id="69332-123">Dopo aver configurato le regole disabilitate, utili come tooview i log WAF.</span><span class="sxs-lookup"><span data-stu-id="69332-123">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="69332-124">Per altre informazioni, vedere [Diagnostica del gateway applicazione](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="69332-124">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
