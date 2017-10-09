---
title: integrazione di Gateway con Centro sicurezza di Azure aaaApplication | Documenti Microsoft
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
ms.openlocfilehash: 6f6ace105e84c01f525ab02938e81ce040c5c9d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a>Panoramica dell'integrazione tra il gateway applicazione e il Centro sicurezza di Azure

Informazioni sulla protezione delle risorse dell'applicazione Web tramite il gateway applicazione e il Centro sicurezza di Azure. Firewall applicazione web di Application gateway (WAF) si integra con [Centro sicurezza PC](../security-center/security-center-intro.md) tooprovide tooprevent una semplice visualizzazione, rilevare e rispondere toothreats toounprotected applicazioni nell'ambiente in uso.

## <a name="overview"></a>Panoramica

Il WAF del gateway applicazione è una raccomandazione del Centro sicurezza per la protezione delle applicazioni Web da attacchi e vulnerabilità. Risorse Web abilitato che non sono protetti da WAF mostrano nel Centro protezione hello come indicazioni di alto livello di gravità. Consigli per i firewall applicazione web vengono visualizzati nella hello **Panoramica** pagina **applicazioni**.

![integrazione con il Centro sicurezza][1]

Fare clic su qualsiasi indicazioni relative al firewall applicazione web consente di aprire un nuovo pannello con dettagli hello della raccomandazione hello.

## <a name="add-a-web-application-firewall-tooan-existing-resource"></a>Aggiungere una risorsa esistente web application firewall tooan

Passare troppo**più servizi** > **sicurezza + identità** > **Centro sicurezza PC** e hello **Centro sicurezza PC - Panoramica**  pannello, fare clic su **applicazioni**. In hello **Centro sicurezza PC - applicazioni** pannello tabella hello contiene un elenco di applicazioni che Centro sicurezza rilevato nella sottoscrizione.

![applicazioni Web][3]

Facendo clic su un'applicazione web con un problema grave, viene visualizzato hello **l'integrità della protezione applicazione** blade. Nella seguente figura hello hello applicazione web che non è protetto da un firewall applicazione web. 

![risorse Web non protette][2]

Fare clic su **aggiunge un firewall applicazione web** in **indicazioni** tooopen hello **aggiungere una Web Application Firewall** blade.

Se non si dispone di un Gateway applicazione esistente o desidera toocreate uno nuovo, fare clic su **Crea nuovo** e hello **creare un nuovo Web Application Firewall** pannello e fare clic su **Microsoft - Gateway applicazione**. Verrà visualizzata tramite hello passaggi toocreate un gateway applicazione. A questo punto, l'applicazione Web viene aggiunta come risorsa protetta e il Centro sicurezza rileva che la risorsa è protetta da un web application firewall. La risorsa non viene aggiunta come membro del pool back-end.

Se è presente un gateway applicazione, è possibile selezionarlo in **Usa la soluzione esistente**

![pannello di aggiunta di web application firewall][4]

Aggiunta di un gateway di applicazione tooan applicazione web tramite il Centro sicurezza PC non risorse hello come un membro del pool back-end, questa operazione deve essere eseguita sulla risorsa di gateway applicazione hello direttamente.

## <a name="add-a-resource-tooan-existing-web-application-firewall"></a>Aggiungere un risorsa tooan web dell'applicazione del firewall esistente

Passare troppo**più servizi** > **sicurezza + identità** > **Centro sicurezza PC** e hello **Centro sicurezza PC - Panoramica**  pannello, fare clic su **soluzioni Partner**. Mostrano i gateway di applicazione compatibile con il Centro sicurezza PC esistenti in hello **soluzioni dei Partner** blade.

![soluzioni partner][7]

Fare clic su **collegamento app** tooopen hello **collegamento applicazioni** pannello qui vengono fornite applicazioni di hello opzioni tooselect esistenti. Scegliere tooprotect applicazioni hello e fare clic su **OK**. Non aggiunge hello toohello back-end pool di applicazioni web del gateway applicazione hello. Consente di impostare le risorse di hello come una risorsa protetta in modo da Centro sicurezza PC sia possibile tenere traccia. risorsa di hello tooadd come un membro del pool back-end, questa operazione deve essere eseguita nel gateway applicazione hello, dal pannello corrente hello è possibile fare clic su **console soluzione** toobe eseguite resource di gateway applicazione toohello in cui è possibile aggiungere web hello pool di applicazioni toohello back-end.

![applicazioni di soluzioni partner][6]

## <a name="finalize-configuration"></a>Completare la configurazione

Centro sicurezza PC tiene traccia delle applicazioni aggiunto gateway applicazione tooan come una risorsa protetta.  Monitorato lo stato di hello della risorsa e si assicura che è protetta da un gateway applicazione. passaggio successivo Hello è tooadd hello private IP, indirizzo IP pubblico o scheda NIC del pool back-end di toohello di macchina virtuale di gateway applicazione hello. Fino a quando questa operazione viene eseguita un'indicazione aggiuntiva di **Finalizza la protezione di applicazione** viene visualizzato solo dopo l'aggiunta di risorse hello.

![pannello di aggiunta di web application firewall][5]

## <a name="security-alerts"></a>Avvisi di sicurezza

All'interno di Centro sicurezza PC passare troppo**rilevamento** > **degli avvisi di sicurezza**.  Vengono visualizzati gli avvisi WAF per i gateway applicazione. Gli avvisi sono suddivisi per regola WAF.

![avvisi di sicurezza][8]

Fare clic su una regola per visualizzare un elenco degli avvisi per la regola WAF specifica. Ogni avviso Mostra ulteriori informazioni su come trovare hello. Dettagli Hello forniscono un gateway applicazione toohello di collegamento.
 
![dettagli dell'avviso][9]

## <a name="next-steps"></a>Passaggi successivi

toolearn come tooenable firewall di applicazione web su un gateway applicazione esistente, visitare [crea o aggiorna un Gateway applicazione Azure con firewall applicazione web](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png