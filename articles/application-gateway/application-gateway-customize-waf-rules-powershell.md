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
# <a name="customize-web-application-firewall-rules-through-powershell"></a>Personalizzare le regole del web application firewall con PowerShell

> [!div class="op_single_selector"]
> * [Portale di Azure](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Interfaccia della riga di comando di Azure 2.0](application-gateway-customize-waf-rules-cli.md)

firewall applicazione web di Hello Gateway applicazione Azure (WAF) fornisce protezione per le applicazioni web. Queste protezioni sono fornite da hello aprire Web applicazione sicurezza progetto (OWASP) Core regola impostata (CR). Alcune regole possono generare falsi positivi e bloccare il traffico reale. Per questo motivo, il Gateway applicazione fornisce le regole e gruppi di regole toocustomize funzionalità hello. Per ulteriori informazioni sui gruppi di regole specifici hello e sulle regole, vedere [elenco di regole e gruppi CRS regola firewall di applicazioni web](application-gateway-crs-rulegroups-rules.md).

## <a name="view-rule-groups-and-rules"></a>Visualizzare le regole e i gruppi di regole

Hello esempi di codice seguente mostra come tooview regole e gruppi che possono essere configurati su un gateway applicazione WAF abilitata all'uso di regole.

### <a name="view-rule-groups"></a>Visualizzare i gruppi di regole

Hello seguente esempio viene illustrato come i gruppi di regole tooview:

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

Dopo l'output di Hello è una risposta troncata da hello sopra riportato:

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

## <a name="disable-rules"></a>Disabilitare le regole

esempio Hello disabilita le regole `910018` e `910017` su un gateway applicazione:

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a>Passaggi successivi

Dopo aver configurato le regole disabilitate, utili come tooview i log WAF. Per altre informazioni, vedere [Diagnostica del gateway applicazione](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
