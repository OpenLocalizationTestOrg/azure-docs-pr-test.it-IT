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
# <a name="customize-web-application-firewall-rules-through-hello-azure-portal"></a>Personalizzare le regole di firewall applicazione web tramite hello portale di Azure

> [!div class="op_single_selector"]
> * [Portale di Azure](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Interfaccia della riga di comando di Azure 2.0](application-gateway-customize-waf-rules-cli.md)

firewall applicazione web di Hello Gateway applicazione Azure (WAF) fornisce protezione per le applicazioni web. Queste protezioni sono fornite da hello aprire Web applicazione sicurezza progetto (OWASP) Core regola impostata (CR). Alcune regole possono generare falsi positivi e bloccare il traffico reale. Per questo motivo, il Gateway applicazione fornisce le regole e gruppi di regole toocustomize funzionalità hello. Per ulteriori informazioni sui gruppi di regole specifici hello e sulle regole, vedere [elenco di regole e gruppi di regole CRS firewall applicazione web](application-gateway-crs-rulegroups-rules.md).

>[!NOTE]
> Se il gateway applicazione non utilizza il livello di WAF hello, nel riquadro di destra hello hello opzione tooupgrade hello gateway toohello WAF livello applicazione. 

![Abilitare WAF][fig1]

## <a name="view-rule-groups-and-rules"></a>Visualizzare le regole e i gruppi di regole

**regole e gruppi di regole tooview**
   1. Gateway applicazione toohello Sfoglia e quindi selezionare **firewall applicazione Web**.  
   2. Selezionare **Advanced rule configuration** (Configurazione regole avanzata).  
   Questa visualizzazione mostra una tabella nella pagina di hello di tutti i gruppi di regole hello fornito con hello scelto set di regole. Tutte le caselle di controllo della regola hello sono selezionate.

![Configurare regole disabilitate][1]

## <a name="search-for-rules-toodisable"></a>Cerca regole toodisable

Hello **impostazioni firewall applicazione Web** pannello sono disponibili funzionalità hello toofilter hello regole tramite una ricerca di testo. risultato Hello vengono visualizzati solo i gruppi di regole hello e regole che contengono testo hello che per effettuare la ricerca.

![Cercare le regole][2]

## <a name="disable-rule-groups-and-rules"></a>Disabilitare le regole e i gruppi di regole

Quando si disabilitano le regole, è possibile disabilitare un intero gruppo di regole o regole specifiche in uno o più gruppi di regole. 

**toodisable gruppi di regole o regole specifiche**

   1. Ricerca di regole hello o gruppi di regole che si desidera toodisable.
   2. Deselezionare le caselle di controllo hello hello alle regole che si desidera toodisable. 
   2. Selezionare **Salva**. 

![Salvare le modifiche][3]

## <a name="next-steps"></a>Passaggi successivi

Dopo aver configurato le regole disabilitate, utili come tooview i log WAF. Per altre informazioni, vedere [Diagnostica del gateway applicazione](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
