---
title: soluzione di rete Analitica in Log Analitica aaaAzure | Documenti Microsoft
description: "È possibile utilizzare hello soluzione Analitica di rete di Azure nei registri del gruppo protezione rete di Azure tooreview Analitica di Log e nei registri di Gateway applicazione Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a>Soluzioni di monitoraggio di rete di Azure in Log Analytics

Log Analitica offre hello seguenti soluzioni per il monitoraggio delle reti:
* Monitoraggio delle prestazioni di rete per
 * Monitoraggio integrità hello della rete
* Azure tooreview analitica di Gateway applicazione
 * Log di gateway applicazione di Azure
 * Metriche di gateway applicazione di Azure
* Gruppo di sicurezza di rete di Azure analitica tooreview
 * Log dei gruppi di sicurezza di rete di Azure

## <a name="network-performance-monitor-npm"></a>Monitoraggio delle prestazioni di rete

Hello [Network Performance Monitor](log-analytics-network-performance-monitor.md) soluzione di gestione è una soluzione, che controlla integrità hello, disponibilità e raggiungibilità di reti di monitoraggio di rete.  È utilizzato toomonitor connettività tra:

* Cloud pubblico e risorse locali
* Data center e percorsi utente (succursali)
* Subnet che ospitano vari livelli di un'applicazione multilivello.

Per altre informazioni, vedere [Monitoraggio delle prestazioni di rete](log-analytics-network-performance-monitor.md).

## <a name="azure-application-gateway-and-network-security-group-analytics"></a>Azure Application Gateway Analytics e Azure Network Security Group Analytics
soluzioni di hello toouse:
1. Aggiungere tooLog soluzione di gestione hello Analitica, e
2. Abilitare la diagnostica toodirect hello diagnostica tooa Log Analitica dell'area di lavoro. Non è necessario toowrite nell'archiviazione Blob tooAzure hello registri.

È possibile abilitare la diagnostica e la soluzione corrispondente hello per uno o entrambi i gruppi di sicurezza di rete e di Gateway applicazione.

Se non si abilita la registrazione diagnostica per un determinato tipo di risorsa, ma installare la soluzione hello, pannelli di dashboard hello per tale risorsa sono vuoti e visualizzare un messaggio di errore.

> [!NOTE]
> Nel gennaio January 2017, hello supportate consentono di inviare i log da gruppi di sicurezza di rete e di gateway applicazione tooLog che Analitica modificato. Se viene visualizzato hello **Analitica di rete di Azure (deprecato)** soluzioni, fare riferimento troppo[la migrazione da una soluzione Analitica rete precedente hello](#migrating-from-the-old-networking-analytics-solution) per la procedura è necessario toofollow.
>
>

## <a name="review-azure-networking-data-collection-details"></a>Esaminare i dettagli della raccolta di dati di rete di Azure
analitica di Gateway applicazione Azure Hello hello Network Security Group analitica soluzioni di gestione e raccolta i registri di diagnostica direttamente dal gateway applicazione Azure e i gruppi di sicurezza di rete. Non è necessario toowrite hello registri tooAzure nell'archiviazione Blob e non è richiesto per la raccolta dati.

Hello nella tabella seguente illustra i metodi di raccolta dati e altri dettagli sulla modalità di raccolta dati per analitica di Gateway applicazione Azure e analitica Network Security Group hello.

| Piattaforma | Agente diretto | Agente di Systems Center Operations Manager | Azure | È necessario Operations Manager? | Dati dell'agente Operations Manager inviati con il gruppo di gestione | Frequenza della raccolta |
| --- | --- | --- | --- | --- | --- | --- |
| Azure |  |  |&#8226; |  |  |Quando connesso |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a>Soluzione di analisi del gateway applicazione di Azure in Log Analytics

![Simbolo di Analisi gateway applicazione di Azure](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

Hello seguendo i registri è supportato per i gateway applicazione:

* ApplicationGatewayAccessLog
* ApplicationGatewayPerformanceLog
* ApplicationGatewayFirewallLog

Hello seguenti metriche è supportato per i gateway applicazione:

* Velocità effettiva di 5 minuti

### <a name="install-and-configure-hello-solution"></a>Installare e configurare la soluzione hello
Utilizzare hello seguendo le istruzioni tooinstall e configurare la soluzione analitica di Gateway applicazione Azure hello:

1. Abilitare una soluzione analitica di Gateway applicazione Azure hello da [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) o tramite il processo di hello descritto in [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).
2. Abilitare la registrazione diagnostica per hello [gateway applicazione](../application-gateway/application-gateway-diagnostics.md) desiderato toomonitor.

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a>Abilitare la diagnostica di Gateway applicazione Azure nel portale di hello

1. Nel portale di Azure hello, passare toohello Gateway applicazione risorse toomonitor
2. Selezionare *log di diagnostica* hello tooopen dopo

   ![Immagine della risorsa gateway applicazione di Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. Fare clic su *attivare la diagnostica* hello tooopen dopo

   ![Immagine della risorsa gateway applicazione di Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. tooturn sulla diagnostica, fare clic su *su* in *stato*
5. Fare clic sulla casella di controllo hello *inviare tooLog Analitica*
6. Selezionare un'area di lavoro Log Analytics esistente o creare una
7. Fare clic sulla casella di controllo di hello in **Log** per ognuna delle hello log tipi toocollect
8. Fare clic su *salvare* registrazione hello tooenable di diagnostica tooLog Analitica

#### <a name="enable-azure-network-diagnostics-using-powershell"></a>Abilitare la diagnostica di rete di Azure tramite PowerShell

Hello lo script di PowerShell seguente viene fornito un esempio di come tooenable registrazione diagnostica per il gateway applicazione.

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a>Usare l'analisi dei gateway applicazione di Azure
![Immagine del riquadro di analisi dei gateway applicazione di Azure](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

Dopo aver fatto clic hello **analitica di Gateway applicazione Azure** riquadro su hello panoramica, è possibile visualizzare i riepiloghi dei registri e quindi eseguire il drill-toodetails per hello seguenti categorie:

* Log di accesso del gateway applicazione
  * Errori di client e server per i log di accesso del gateway applicazione
  * Richieste all'ora per ogni gateway applicazione
  * Richieste non riuscite all'ora per ogni gateway applicazione
  * Errori per agente utente per gateway applicazione
* Prestazioni del gateway applicazione
  * Integrità dell'host per il gateway applicazione
  * Valore massimo e 95° percentile per le richieste non riuscite del gateway applicazione

![Immagine del dashboard di analisi del gateway applicazione di Azure](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![Immagine del dashboard di analisi del gateway applicazione di Azure](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

In hello **analitica di Gateway applicazione Azure** dashboard, esaminare le informazioni di riepilogo hello in uno dei pannelli hello e quindi fare clic su uno tooview informazioni dettagliate sulla pagina ricerca nei log hello.

In qualsiasi pagina di ricerca log hello di, è possibile visualizzare i risultati dal tempo, i risultati dettagliati e alla cronologia di ricerca. È inoltre possibile filtrare dai risultati di hello toonarrow facet.


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a>Soluzione di analisi del gruppo di sicurezza di rete di Azure in Log Analytics

![Simbolo di Analisi gruppo di sicurezza di rete di Azure](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

Hello seguendo i registri è supportato per i gruppi di sicurezza di rete:

* NetworkSecurityGroupEvent
* NetworkSecurityGroupRuleCounter

### <a name="install-and-configure-hello-solution"></a>Installare e configurare la soluzione hello
Utilizzare hello seguendo le istruzioni tooinstall e configurare la soluzione di hello Analitica di rete di Azure:

1. Abilitare la soluzione analitica di gruppo di sicurezza di rete di Azure hello da [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) o tramite il processo di hello descritto in [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).
2. Abilitare la registrazione diagnostica per hello [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) risorse desiderate toomonitor.

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a>Abilitare la diagnostica di gruppo di sicurezza di rete di Azure nel portale di hello

1. Nel portale di Azure hello, passare toohello Network Security Group risorse toomonitor
2. Selezionare *log di diagnostica* hello tooopen dopo

   ![Immagine della risorsa gruppo di sicurezza di rete di Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. Fare clic su *attivare la diagnostica* hello tooopen dopo

   ![Immagine della risorsa gruppo di sicurezza di rete di Azure](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. tooturn sulla diagnostica, fare clic su *su* in *stato*
5. Fare clic sulla casella di controllo hello *inviare tooLog Analitica*
6. Selezionare un'area di lavoro Log Analytics esistente o creare una
7. Fare clic sulla casella di controllo di hello in **Log** per ognuna delle hello log tipi toocollect
8. Fare clic su *salvare* registrazione hello tooenable di diagnostica tooLog Analitica

### <a name="enable-azure-network-diagnostics-using-powershell"></a>Abilitare la diagnostica di rete di Azure tramite PowerShell

Hello lo script di PowerShell seguente viene fornito un esempio di come tooenable registrazione diagnostica per i gruppi di sicurezza di rete
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a>Usare l'analisi del gruppo di sicurezza di rete di Azure
Dopo aver fatto clic hello **analitica gruppo di sicurezza di rete di Azure** riquadro su hello panoramica, è possibile visualizzare i riepiloghi dei registri e quindi eseguire il drill-toodetails per hello seguenti categorie:

* Flussi bloccati dei gruppi di sicurezza di rete
  * Regole dei gruppi di sicurezza di rete con flussi bloccati
  * Indirizzi MAC con flussi bloccati
* Flussi consentiti dei gruppi di sicurezza di rete
  * Regole dei gruppi di sicurezza di rete con flussi consentiti
  * Indirizzi MAC con flussi consentiti

![Immagine del dashboard di analisi del gruppo di sicurezza di rete di Azure](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![Immagine del dashboard di analisi del gruppo di sicurezza di rete di Azure](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

In hello **analitica gruppo di sicurezza di rete di Azure** dashboard, esaminare le informazioni di riepilogo hello in uno dei pannelli hello e quindi fare clic su uno tooview informazioni dettagliate sulla pagina ricerca nei log hello.

In qualsiasi pagina di ricerca log hello di, è possibile visualizzare i risultati dal tempo, i risultati dettagliati e alla cronologia di ricerca. È inoltre possibile filtrare dai risultati di hello toonarrow facet.

## <a name="migrating-from-hello-old-networking-analytics-solution"></a>La migrazione da una soluzione Analitica rete precedente hello
Nel gennaio January 2017, hello supportate consentono di inviare i log dal gateway applicazione Azure e i gruppi di sicurezza di rete di Azure tooLog che Analitica modificato. Queste modifiche consentono hello seguenti vantaggi:
+ I log vengono scritti direttamente tooLog Analitica senza hello necessario toouse un account di archiviazione
+ Minore latenza dall'ora di hello quando i registri sono generati toothem disponibile nel Log Analitica
+ Meno passaggi di configurazione
+ Un formato comune per tutti i tipi di diagnostica di Azure

hello toouse aggiornata soluzioni:

1. [Configurare diagnostica toobe inviato direttamente tooLog Analitica da gateway per applicazioni Azure](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [Configurare diagnostica toobe inviato tooLog Analitica direttamente dai gruppi di sicurezza di rete di Azure](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. Abilitare hello *Analitica di Gateway applicazione Azure* hello e *Analitica di gruppo di sicurezza di Azure rete* soluzione tramite hello processo descritto in [soluzioni aggiungere Log Analitica da Hello Solutions Gallery](log-analytics-add-solutions.md)
3. Aggiornare le query salvate, dashboard o avvisi toouse hello nuovo tipo di dati
  + Il tipo è tooAzureDiagnostics. È possibile utilizzare i log di rete hello ResourceType toofilter tooAzure.

    | Invece di: | Usare: |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + Per qualsiasi campo che contiene un suffisso di \_s, \_d, o \_g in nome hello cambia hello primo carattere toolower maiuscole/minuscole
   + Per qualsiasi campo che contiene un suffisso di \_o nel nome, i dati di hello è suddiviso in singoli campi in base ai nomi di campo hello annidato.
4. Rimuovere hello *Analitica di rete di Azure (obsoleto)* soluzione.
  + Se si utilizza PowerShell, usare `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`

I dati raccolti prima modifica hello non è visibile nella nuova soluzione hello. È possibile continuare tooquery per questa operazione utilizzando dati hello vecchio tipo e i nomi dei campi.

## <a name="troubleshooting"></a>Risoluzione dei problemi
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>Passaggi successivi
* Utilizzare [Accedi ricerche Log Analitica](log-analytics-log-searches.md) tooview in dettaglio i dati di diagnostica di Azure.
