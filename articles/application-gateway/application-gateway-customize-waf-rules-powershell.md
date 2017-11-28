---
title: regole del firewall applicazione web aaaCustomize in Gateway applicazione Azure - PowerShell | Documenti Microsoft
description: Questo articolo fornisce informazioni sul funzionamento delle regole firewall di applicazione web toocustomize nel Gateway di applicazione con PowerShell.
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
ms.openlocfilehash: f320e687b0f621515255469dac8e375cdd900dda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-powershell"></a><span data-ttu-id="c5fa2-103">Personalizzare le regole del web application firewall con PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5fa2-103">Customize web application firewall rules through PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c5fa2-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c5fa2-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="c5fa2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5fa2-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="c5fa2-106">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="c5fa2-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="c5fa2-107">firewall applicazione web di Hello Gateway applicazione Azure (WAF) fornisce protezione per le applicazioni web.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="c5fa2-108">Queste protezioni sono fornite da hello aprire Web applicazione sicurezza progetto (OWASP) Core regola impostata (CR).</span><span class="sxs-lookup"><span data-stu-id="c5fa2-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="c5fa2-109">Alcune regole possono generare falsi positivi e bloccare il traffico reale.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="c5fa2-110">Per questo motivo, il Gateway applicazione fornisce le regole e gruppi di regole toocustomize funzionalità hello.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="c5fa2-111">Per ulteriori informazioni sui gruppi di regole specifici hello e sulle regole, vedere [elenco di regole e gruppi CRS regola firewall di applicazioni web](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="c5fa2-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS Rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="c5fa2-112">Visualizzare le regole e i gruppi di regole</span><span class="sxs-lookup"><span data-stu-id="c5fa2-112">View rule groups and rules</span></span>

<span data-ttu-id="c5fa2-113">Hello esempi di codice seguente mostra come tooview regole e gruppi che possono essere configurati su un gateway applicazione WAF abilitata all'uso di regole.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-113">hello following code examples show how tooview rules and rule groups that are configurable on a WAF-enabled application gateway.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="c5fa2-114">Visualizzare i gruppi di regole</span><span class="sxs-lookup"><span data-stu-id="c5fa2-114">View rule groups</span></span>

<span data-ttu-id="c5fa2-115">Hello seguente esempio viene illustrato come i gruppi di regole tooview:</span><span class="sxs-lookup"><span data-stu-id="c5fa2-115">hello following example shows how tooview rule groups:</span></span>

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

<span data-ttu-id="c5fa2-116">Dopo l'output di Hello è una risposta troncata da hello sopra riportato:</span><span class="sxs-lookup"><span data-stu-id="c5fa2-116">hello following output is a truncated response from hello preceding example:</span></span>

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

## <a name="disable-rules"></a><span data-ttu-id="c5fa2-117">Disabilitare le regole</span><span class="sxs-lookup"><span data-stu-id="c5fa2-117">Disable rules</span></span>

<span data-ttu-id="c5fa2-118">esempio Hello disabilita le regole `910018` e `910017` su un gateway applicazione:</span><span class="sxs-lookup"><span data-stu-id="c5fa2-118">hello following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="c5fa2-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c5fa2-119">Next steps</span></span>

<span data-ttu-id="c5fa2-120">Dopo aver configurato le regole disabilitate, utili come tooview i log WAF.</span><span class="sxs-lookup"><span data-stu-id="c5fa2-120">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="c5fa2-121">Per altre informazioni, vedere [Diagnostica del gateway applicazione](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="c5fa2-121">For more information, see [Application Gateway Diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
