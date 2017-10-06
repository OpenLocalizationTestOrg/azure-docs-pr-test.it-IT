---
title: firewall applicazione aaaIntroduction tooweb (WAF) per il Gateway applicazione Azure | Documenti Microsoft
description: Questa pagina offre una panoramica di Web application firewall (WAF) per il gateway applicazione
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 04b362bc-6653-4765-86f6-55ee8ec2a0ff
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: amsriva
ms.openlocfilehash: 5a42ce0fb2bd12a391844099e2de8fa2571195e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="web-application-firewall-waf"></a>Web application firewall (WAF)

Web application firewall (WAF) è una funzionalità del gateway applicazione che offre una protezione centralizzata delle applicazioni Web da exploit e vulnerabilità comuni. 

Firewall applicazione Web è in base alle regole da hello [set di regole di base OWASP](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) 3.0 o 2.2.9. Le applicazioni Web sono sempre più vittime di attacchi che sfruttano le più comuni vulnerabilità note. Comuni tra questi attacchi sono gli attacchi SQL injection, cross-site scripting attacchi tooname alcuni. Impedire gli attacchi nel codice dell'applicazione può risultare complessa e potrebbe richiedere manutenzione rigorosa, l'applicazione di patch e il monitoraggio a più livelli della topologia applicazione hello. Firewall applicazione web centralizzata rende molto più semplice gestione della sicurezza e offre migliorato garanzia agli amministratori di tooapplication contro minacce o intrusioni. Una soluzione WAF può inoltre riflettere minaccia alla sicurezza tooa più veloce per l'applicazione di patch una vulnerabilità nota in una posizione centrale e la protezione di ognuna delle singole applicazioni web. Gateway applicazione esistente può essere facilmente convertito tooa web applicazione firewall abilitato applicazioni gateway.

![imageURLroute](./media/application-gateway-web-application-firewall-overview/WAF1.png)

Gateway applicazione funziona come un'applicazione recapito controller e offerte terminazione SSL, l'affinità di sessione basato su cookie, distribuzione del carico round robin, il routing basato sul contenuto, toohost possibilità più miglioramenti di siti Web e di sicurezza. Miglioramenti apportati alla sicurezza offerta da Gateway applicazione includono Gestione criteri di SSL, fine tooend supporto SSL. Sicurezza dell'applicazione è ora rafforzata da WAF (firewall applicazione web) viene integrato direttamente offerta hello ADC. Fornisce un toomanage posizione centrale tooconfigure semplice e proteggere le applicazioni web comuni alle vulnerabilità di web.

## <a name="benefits"></a>Vantaggi

di seguito Hello sono i vantaggi principali hello che forniscono firewall applicazione web e di Gateway applicazione:

### <a name="protection"></a>Protezione

* Proteggere l'applicazione web da attacchi senza codice toobackend modifica e vulnerabilità di web.

* Web più proteggere le applicazioni di hello stesso tempo dietro un gateway applicazione. Gateway applicazione supporta l'hosting di siti Web too20 dietro un singolo gateway che possono essere protette da attacchi web con WAF.

### <a name="monitoring"></a>Monitoraggio

* Monitorare l'applicazione Web contro gli attacchi tramite un log di Web application firewall in tempo reale. Questo file di registro è integrato con [Monitor Azure](../monitoring-and-diagnostics/monitoring-overview.md) tootrack WAF degli avvisi e registri e monitorare facilmente le tendenze.

* Web application firewall sarà presto integrato con il Centro sicurezza di Azure. Centro sicurezza di Azure consente la visualizzazione centrale dello stato di sicurezza hello di tutte le risorse di Azure.

### <a name="customization"></a>Personalizzazione

* Hello possibilità toocustomize WAF regole e regole gruppi toosuit dei requisiti dell'applicazione ed eliminare i falsi positivi.

## <a name="features"></a>Funzionalità

Firewall applicazione Web è preconfigurato con CRS 3.0 per impostazione predefinita, oppure è possibile scegliere toouse 2.2.9. CRS 3.0 offre meno falsi positivi rispetto alla versione 2.2.9. Hello possibilità troppo[personalizzare regole toosuit esigenze](application-gateway-customize-waf-rules-portal.md) viene fornito. Alcune delle vulnerabilità web comuni hello firewall applicazione web consente di proteggere include:

* Protezione dagli attacchi SQL injection
* Protezione dagli attacchi di scripting intersito
* Protezione dai comuni attacchi Web, ad esempio attacchi di iniezione di comandi, richieste HTTP non valide, attacchi HTTP Response Splitting e Remote File Inclusion
* Protezione dalle violazioni del protocollo HTTP
* Protezione contro eventuali anomalie del protocollo HTTP, ad esempio user agent host mancante e accept header
* Prevenzione contro robot, crawler e scanner
* Rilevamento di errori di configurazione comuni dell'applicazione (ad esempio, Apache, IIS e così via)

Per un elenco dettagliato delle regole e le protezioni vedere seguente hello [set di regole di base](#core-rule-sets).

### <a name="core-rule-sets"></a>Set di regole principali

Il gateway applicazione supporta due set di regole, ovvero CRS 3.0 e CRS 2.2.9. Questi set di regole principali sono raccolte di regole che proteggono le applicazioni Web da attività dannose.

#### <a name="owasp30"></a>OWASP_3.0

set di regole di base Hello 3.0 fornito è 13 gruppi di regole come illustrato nella seguente tabella hello. Ognuno di questi gruppi di regole contiene più regole che possono essere disabilitate.

|RuleGroup|Descrizione|
|---|---|
|**[REQUEST-910-IP-REPUTATION](application-gateway-crs-rulegroups-rules.md#crs910)**|Contiene le regole tooprotect contro spamming noti o attività dannose.|
|**[REQUEST-911-METHOD-ENFORCEMENT](application-gateway-crs-rulegroups-rules.md#crs911)**|Contiene le regole toolock metodi inattivi (PUT, PATCH <...)|
|**[REQUEST-912-DOS-PROTECTION](application-gateway-crs-rulegroups-rules.md#crs912)**| Contiene le regole tooprotect contro gli attacchi Denial of Service (DoS).|
|**[REQUEST-913-SCANNER-DETECTION](application-gateway-crs-rulegroups-rules.md#crs913)**| Contiene le regole tooprotect contro gli scanner di porta e l'ambiente.|
|**[REQUEST-920-PROTOCOL-ENFORCEMENT](application-gateway-crs-rulegroups-rules.md#crs920)**|Contiene regole tooprotect rispetto al protocollo e problemi di codifica.|
|**[REQUEST-921-PROTOCOL-ATTACK](application-gateway-crs-rulegroups-rules.md#crs921)**|Contiene le regole tooprotect contro injection di intestazione, richieste non valide e nella suddivisione della risposta|
|**[REQUEST-930-APPLICATION-ATTACK-LFI](application-gateway-crs-rulegroups-rules.md#crs930)**|Contiene le regole tooprotect contro gli attacchi di tipo e il percorso file.|
|**[REQUEST-931-APPLICATION-ATTACK-RFI](application-gateway-crs-rulegroups-rules.md#crs931)**|Contiene le regole tooprotect in remoto File di inclusione (RFI)|
|**[REQUEST-932-APPLICATION-ATTACK-RCE](application-gateway-crs-rulegroups-rules.md#crs932)**|Contiene le regole tooprotect nuovamente l'esecuzione di codice.|
|**[REQUEST-933-APPLICATION-ATTACK-PHP](application-gateway-crs-rulegroups-rules.md#crs933)**|Contiene le regole tooprotect da attacchi injection di PHP.|
|**[REQUEST-941-APPLICATION-ATTACK-XSS](application-gateway-crs-rulegroups-rules.md#crs941)**|Contiene le regole per la protezione da cross site scripting.|
|**[REQUEST-942-APPLICATION-ATTACK-SQLI](application-gateway-crs-rulegroups-rules.md#crs942)**|Contiene le regole per la protezione da attacchi SQL injection.|
|**[REQUEST-943-APPLICATION-ATTACK-SESSION-FIXATION](application-gateway-crs-rulegroups-rules.md#crs943)**|Contiene le regole tooprotect contro gli attacchi di determinazione di sessione.|

#### <a name="owasp229"></a>OWASP_2.2.9

set di regole di base Hello 2.2.9 fornito dispone di 10 gruppi di regole come illustrato nella seguente tabella hello. Ognuno di questi gruppi di regole contiene più regole che possono essere disabilitate.

|RuleGroup|Descrizione|
|---|---|
|**[crs_20_protocol_violations](application-gateway-crs-rulegroups-rules.md#crs20)**|Contiene le regole tooprotect contro le violazioni di protocollo (caratteri non validi, GET con un corpo della richiesta, ecc.)|
|**[crs_21_protocol_anomalies](application-gateway-crs-rulegroups-rules.md#crs21)**|Contiene le regole tooprotect con le informazioni di intestazione non corretta.|
|**[crs_23_request_limits](application-gateway-crs-rulegroups-rules.md#crs23)**|Contiene le regole tooprotect contro argomenti o i file che superano i limiti.|
|**[crs_30_http_policy](application-gateway-crs-rulegroups-rules.md#crs30)**|Contiene le regole tooprotect da metodi con restrizioni, le intestazioni e i tipi di file. |
|**[crs_35_bad_robots](application-gateway-crs-rulegroups-rules.md#crs35)**|Contiene le regole tooprotect contro crawler e gli scanner.|
|**[crs_40_generic_attacks](application-gateway-crs-rulegroups-rules.md#crs40)**|Contiene le regole tooprotect attacchi generico (complemento di sessione, inclusione di file remoto, attacco intrusivo nel codice PHP e così via)|
|**[crs_41_sql_injection_attacks](application-gateway-crs-rulegroups-rules.md#crs41sql)**|Contiene le regole tooprotect da attacchi SQL injection|
|**[crs_41_xss_attacks](application-gateway-crs-rulegroups-rules.md#crs41xss)**|Contiene le regole tooprotect contro cross-site scripting.|
|**[crs_42_tight_security](application-gateway-crs-rulegroups-rules.md#crs42)**|Contiene una regola tooprotect contro gli attacchi di attraversamento di percorso|
|**[crs_45_trojans](application-gateway-crs-rulegroups-rules.md#crs45)**|Contiene le regole tooprotect contro backdoor Trojan.|

### <a name="waf-modes"></a>Modalità del WAF

WAF di Gateway applicazione può essere configurato toorun in hello due modalità seguenti:

* **Modalità di rilevamento** : quando toorun configurato in modalità di rilevamento, WAF di Gateway applicazione monitora e registra tutti gli avvisi nel file di log tooa. Registrazione della diagnostica per il Gateway applicazione deve essere attivata utilizzando hello **diagnostica** sezione. È inoltre necessario tooensure che hello WAF log è selezionato e attivato. Quando viene eseguito in modalità di rilevamento, Web application firewall non blocca le richieste in ingresso.
* **Modalità di prevenzione** : quando toorun configurato in modalità di prevenzione, Gateway applicazione blocca attivamente intrusioni e attacchi rilevati da regole. autore dell'attacco Hello riceve un'eccezione di accesso non autorizzato 403 e hello connessione viene terminata. Modalità di prevenzione continua toolog tali attacchi hello WAF log.

### <a name="application-gateway-waf-reports"></a>Monitoraggio WAF

Monitoraggio dell'integrità di hello del gateway applicazione è importante. Monitoraggio dell'integrità di hello le applicazioni web application firewall e hello che protegge vengono forniti tramite la registrazione e l'integrazione con Monitor di Azure, il centro di sicurezza di Azure (presto disponibile) e Log Analitica.

![diagnostica](./media/application-gateway-web-application-firewall-overview/diagnostics.png)

#### <a name="azure-monitor"></a>Monitoraggio di Azure

Ogni log del gateway applicazione è integrato con [Monitoraggio di Azure](../monitoring-and-diagnostics/monitoring-overview.md).  In questo modo le informazioni di diagnostica tootrack inclusi WAF avvisi e registri.  Questa funzionalità viene fornita all'interno delle risorse di Gateway applicazione nel portale di hello in hello hello **diagnostica** scheda o tramite hello Azure monitoraggio del servizio direttamente. informazioni su come abilitare i log di diagnostica per il gateway applicazione visitare toolearn [diagnostica del Gateway applicazione](application-gateway-diagnostics.md)

#### <a name="azure-security-center"></a>Centro sicurezza di Azure

[Centro sicurezza di Azure](../security-center/security-center-intro.md) consente di impedire, rilevare e rispondere toothreats con una maggiore visibilità e controllo sui hello protezione delle risorse di Azure. Il gateway applicazione è ora [integrato nel Centro sicurezza di Azure](application-gateway-integration-security-center.md). Centro sicurezza di Azure esegue l'analisi delle applicazioni web di ambiente toodetect non protetto. Ora possibile consigliabile tooprotect WAF di gateway applicazione queste risorse vulnerabili. È possibile creare applicazioni gateway WAF direttamente da hello Centro sicurezza di Azure.  Queste istanze WAF sono integrate con Centro sicurezza di Azure e restituiscono avvisi e informazioni sull'integrità tooAzure centro di sicurezza per i report.

![Figura 1](./media/application-gateway-web-application-firewall-overview/figure1.png)

#### <a name="logging"></a>Registrazione

Il WAF del gateway applicazione fornisce rapporti dettagliati su ogni minaccia rilevata. La registrazione è integrata con i log di diagnostica di Azure e gli avvisi vengono registrati in formato JSON. Questi log possono essere integrati con [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).

![imageURLroute](./media/application-gateway-web-application-firewall-overview/waf2.png)

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupId}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{appGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

## <a name="application-gateway-waf-sku-pricing"></a>Prezzi dello SKU WAF del gateway applicazione

Web application firewall è disponibile in un nuovo SKU del WAF. Questo prodotto è disponibile solo nel modello di provisioning di gestione risorse di Azure e non nel modello di distribuzione classica hello. Lo SKU del WAF è disponibile solo in istanze del gateway applicazione di medie e grandi dimensioni. Tutti i limiti di hello per il gateway applicazione si applicano anche toohello WAF SKU. I prezzi sono basati su una tariffa oraria per istanza del gateway e una tariffa di elaborazione dei dati. I prezzi orari del gateway per lo SKU del WAF sono diversi dalle tariffe dello SKU standard e sono indicati nella pagina relativa ai [dettagli sui prezzi del gateway applicazione](https://azure.microsoft.com/pricing/details/application-gateway/). L'elaborazione dati rimangono addebiti hello stesso. Non sono presenti tariffe per regola o gruppo di regole. È possibile proteggere più applicazioni web dietro hello stesso web firewall applicazione e non sono previsti costi aggiuntivi per il supporto di più applicazioni. 

La fatturazione per WAF inizia in modo efficace 5/5/2017, fino a quando hello quindi gateway SKU WAF continua toobe addebitato in base alle tariffe standard.

## <a name="next-steps"></a>Passaggi successivi

Dopo aver appreso informazioni sulle funzionalità di hello di WAF, visitare [come tooconfigure web firewall applicazione Gateway applicazione](application-gateway-web-application-firewall-portal.md).

