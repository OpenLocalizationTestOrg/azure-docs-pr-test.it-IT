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
# <a name="customize-web-application-firewall-rules-through-hello-azure-cli-20"></a>Personalizzare le regole di firewall applicazione web tramite hello Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Portale di Azure](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Interfaccia della riga di comando di Azure 2.0](application-gateway-customize-waf-rules-cli.md)

firewall applicazione web di Hello Gateway applicazione Azure (WAF) fornisce protezione per le applicazioni web. Queste protezioni sono fornite da hello aprire Web applicazione sicurezza progetto (OWASP) Core regola impostata (CR). Alcune regole possono generare falsi positivi e bloccare il traffico reale. Per questo motivo, il Gateway applicazione fornisce le regole e gruppi di regole toocustomize funzionalità hello. Per ulteriori informazioni sui gruppi di regole specifici hello e sulle regole, vedere [elenco di regole e gruppi di regole CRS firewall applicazione web](application-gateway-crs-rulegroups-rules.md).

## <a name="view-rule-groups-and-rules"></a>Visualizzare le regole e i gruppi di regole

Hello esempi di codice seguente mostra come tooview regole regole e gruppi che possono essere configurati.

### <a name="view-rule-groups"></a>Visualizzare i gruppi di regole

Hello di esempio seguente viene illustrato come tooview hello gruppi di regole:

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

Dopo l'output di Hello è una risposta troncata da hello sopra riportato:

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

### <a name="view-rules-in-a-rule-group"></a>Visualizzare le regole in un gruppo di regole

Hello di esempio seguente viene illustrato come tooview regole in un gruppo di regole specificato:

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

Dopo l'output di Hello è una risposta troncata da hello sopra riportato:

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

## <a name="disable-rules"></a>Disabilitare le regole

esempio Hello disabilita le regole `910018` e `910017` su un gateway applicazione:

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a>Passaggi successivi

Dopo aver configurato le regole disabilitate, utili come tooview i log WAF. Per altre informazioni, vedere [Diagnostica del gateway applicazione](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
