---
title: "aaaMonitor accedere ai log, registri di prestazioni, integrità back-end e le metriche per il Gateway applicazione | Documenti Microsoft"
description: Informazioni su come tooenable e gestire i registri di accesso e registri di prestazioni per il Gateway applicazione
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: tysonn
tags: azure-resource-manager
ms.assetid: 300628b8-8e3d-40ab-b294-3ecc5e48ef98
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: amitsriva
ms.openlocfilehash: 36ebf15c28f776158350ef8e73d617ef68e09266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-end-health-diagnostic-logs-and-metrics-for-application-gateway"></a>Integrità back-end, log di diagnostica e metriche per il gateway applicazione

Tramite il Gateway applicazione Azure, è possibile monitorare le risorse in hello seguenti modi:

* [Integrità di back-end](#back-end-health): Gateway applicazione fornisce l'integrità di hello funzionalità toomonitor hello del server hello hello pool back-end tramite hello portale di Azure e PowerShell. È inoltre possibile trovare integrità hello di pool back-end hello tramite i log di diagnostica delle prestazioni di hello.

* [Registri](#diagnostic-logs): i registri consentono per le prestazioni, l'accesso, e altri toobe dati salvati o utilizzati da una risorsa a scopo di monitoraggio.

* [Metriche](#metrics): il gateway applicazione include attualmente una sola metrica. Questa metrica consente di misurare la velocità effettiva hello del gateway applicazione hello in byte al secondo.

## <a name="back-end-health"></a>Integrità back-end

Gateway applicazione fornisce l'integrità di hello funzionalità toomonitor hello dei singoli membri di pool back-end hello tramite il portale di hello, PowerShell e interfaccia di hello della riga di comando (CLI). È anche possibile trovare uno stato di integrità aggregato riepilogo del pool back-end tramite i log di diagnostica delle prestazioni di hello. 

rapporto di stato di back-end Hello riflette l'output di hello di istanze di hello Gateway applicazione integrità probe toohello back-end. Quando l'individuazione tramite probe ha esito positivo e hello nuovamente end possono ricevere il traffico, è considerato integro. In caso contrario, viene considerato non integro.

> [!IMPORTANT]
> Se è presente un gruppo di sicurezza di rete (gruppo) in una subnet del Gateway applicazione, aprire gli intervalli di porte 65503 65534 subnet Gateway applicazione hello per il traffico in ingresso. Queste porte sono obbligatorie per toowork di API back-end integrità hello.


### <a name="view-back-end-health-through-hello-portal"></a>Visualizzare lo stato di back-end tramite il portale di hello

Nel portale di hello integrità back-end viene fornito automaticamente. In un gateway applicazione esistente selezionare **Monitoraggio** > **Integrità back-end**. 

Ogni membro nel pool back-end hello è elencato in questa pagina (se si tratta di una scheda di rete, l'IP o FQDN). Vengono visualizzati il nome del pool back-end, la porta, il nome delle impostazioni HTTP back-end e lo stato di integrità. I valori validi per lo stato di integrità sono **Integro**, **Danneggiato** e **Sconosciuto**.

> [!NOTE]
> Se viene visualizzato lo stato di integrità di back-end di **sconosciuto**, assicurarsi che back-end toohello di accesso non sia bloccata da una regola di gruppo, una route definita dall'utente (UDR) o un DNS nella rete virtuale hello personalizzato.

![Integrità back-end][10]

### <a name="view-back-end-health-through-powershell"></a>Visualizzare l'integrità back-end tramite PowerShell

Hello codice di PowerShell seguente viene illustrato come tooview integrità di back-end tramite hello `Get-AzureRmApplicationGatewayBackendHealth` cmdlet:

```powershell
Get-AzureRmApplicationGatewayBackendHealth -Name ApplicationGateway1 -ResourceGroupName Contoso
```

### <a name="view-back-end-health-through-azure-cli-20"></a>Visualizzare l'integrità back-end tramite l'interfaccia della riga di comando di Azure 2.0

```azurecli
az network application-gateway show-backend-health --resource-group AdatumAppGatewayRG --name AdatumAppGateway
```

### <a name="results"></a>Risultati

Hello frammento di codice seguente viene illustrato un esempio di risposta hello:

```json
{
"BackendAddressPool": {
    "Id": "/subscriptions/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/appGatewayBackendPool"
},
"BackendHttpSettingsCollection": [
    {
    "BackendHttpSettings": {
        "Id": "/00000000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings"
    },
    "Servers": [
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        },
        {
        "Address": "hostname.westus.cloudapp.azure.com",
        "Health": "Healthy"
        }
    ]
    }
]
}
```

## <a name="diagnostic-logging"></a>Registri di diagnostica

È possibile utilizzare diversi tipi di registri in Azure toomanage e risolvere i problemi di gateway applicazione. È possibile accedere alcuni di questi log tramite il portale di hello. Tutti i log possono essere estratti dall'archiviazione BLOB di Azure e visualizzati in strumenti differenti, ad esempio [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md), Excel e Power BI. È possibile ulteriori informazioni sui tipi diversi hello dei log da hello seguente elenco:

* **Log attività**: È possibile utilizzare [log attività Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (precedentemente conosciuto come registri e i log di controllo) tooview tutte le operazioni che vengono inviate tooyour sottoscrizione di Azure e il relativo stato. Le voci di log di attività vengono raccolti per impostazione predefinita, ed è possibile visualizzarli in hello portale di Azure.
* **Log di accesso**: È possibile utilizzare modelli di accesso questo log tooview Gateway applicazione e analizzare informazioni importanti, inclusi chiamante hello IP, URL richiesto, latenza nella risposta, codice restituito e byte e la disconnessione. Il log di accesso viene raccolto ogni 300 secondi. Il log contiene un record per ogni istanza del gateway applicazione. istanza di Gateway applicazione Hello può essere identificato dalla proprietà instanceId hello.
* **Log delle prestazioni**: È possibile utilizzare questo tooview log delle prestazioni di istanze del Gateway applicazione. Questo log acquisisce le informazioni sulle prestazioni di ogni istanza, inclusi il totale delle richieste servite, la velocità effettiva in byte, il totale delle richieste non riuscite e il numero delle istanze back-end integre e non integre. Il log delle prestazioni viene raccolto ogni 60 secondi.
* **Registro firewall**: È possibile utilizzare questo richieste hello tooview di log che vengono registrati tramite la modalità di rilevamento o prevenzione di un gateway di applicazione che viene configurato con firewall applicazione web di hello.

> [!NOTE]
> Sono disponibili solo per le risorse distribuite nel modello di distribuzione Azure Resource Manager hello log. Non è possibile utilizzare i log per le risorse nel modello di distribuzione classica hello. Per una migliore comprensione dei modelli di hello due, vedere hello [distribuzione classica e gestione di informazioni sulle risorse](../azure-resource-manager/resource-manager-deployment-model.md) articolo.

Sono disponibili tre opzioni di archiviazione dei log:

* **Account di archiviazione**: ideali quando i log vengono archiviati per un periodo più lungo ed esaminati quando necessario.
* **Hub eventi**: gli hub eventi sono un'ottima opzione per l'integrazione con altre informazioni di sicurezza e avvisi tooget per le risorse di strumenti di gestione degli eventi (SEIM).
* **Log Analytics**: soluzione adatta al monitoraggio generale in tempo reale dell'applicazione o all'analisi delle tendenze.

### <a name="enable-logging-through-powershell"></a>Abilitare la registrazione tramite PowerShell

Registrazione attività viene abilitata automaticamente per tutte le risorse di Resource Manager. È necessario abilitare l'accesso e la raccolta dei dati di hello disponibili tramite i registri di prestazioni registrazione toostart. tooenable registrazione, utilizzare hello alla procedura seguente:

1. Annotare l'ID di risorsa dell'account di archiviazione, dove vengono archiviati i dati di log hello. Questo valore è formato hello: /Subscriptions/<ID\<subscriptionId\>/ResourceGroups /\<nome gruppo di risorse\>/providers/Microsoft.Storage/storageAccounts/\<nomeaccountdiarchiviazione\>. È possibile usare qualsiasi account di archiviazione della sottoscrizione. Utilizzare queste informazioni hello toofind portale Azure.

    ![Portale: ID risorsa dell'account di archiviazione](./media/application-gateway-diagnostics/diagnostics1.png)

2. Prendere nota dell'ID risorsa del gateway applicazione per cui è abilitata la registrazione. Questo valore è formato hello: /Subscriptions/<ID\<subscriptionId\>/ResourceGroups /\<nome gruppo di risorse\>/providers/Microsoft.Network/applicationGateways/\<gateway applicazione nome\>. È possibile utilizzare toofind portale hello queste informazioni.

    ![Portale: ID risorsa del gateway applicazione](./media/application-gateway-diagnostics/diagnostics2.png)

3. Abilitare la registrazione diagnostica tramite hello cmdlet di PowerShell seguente:

    ```powershell
    Set-AzureRmDiagnosticSetting  -ResourceId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name> -StorageAccountId /subscriptions/<subscriptionId>/resourceGroups/<resource group name>/providers/Microsoft.Storage/storageAccounts/<storage account name> -Enabled $true     
    ```
    
> [!TIP] 
>I log attività non richiedono un account di archiviazione separato. utilizzo di Hello dell'archiviazione per l'accesso e la registrazione delle prestazioni comporta costi di servizio.

### <a name="enable-logging-through-hello-azure-portal"></a>Abilitare la registrazione tramite hello portale di Azure

1. Nel portale di Azure hello, trovare la risorsa e fare clic su **log di diagnostica**.

   Per il gateway applicazione sono disponibili tre log:

   * Log di accesso
   * Log delle prestazioni
   * Log del firewall

2. toostart la raccolta dei dati, fare clic su **attivare la diagnostica**.

   ![Attivare la diagnostica][1]

3. Hello **le impostazioni di diagnostica** pannello fornisce le impostazioni di hello per hello i log di diagnostica. In questo esempio, Log Analitica archivia i registri di hello. Fare clic su **configura** in **Log Analitica** tooconfigure l'area di lavoro. È anche possibile utilizzare gli hub di eventi e un archivio account toosave hello i log di diagnostica.

   ![Avvio del processo di configurazione hello][2]

4. Scegliere un'area di lavoro di Operations Management Suite (OMS) oppure crearne una nuova. Questo esempio usa un'area di lavoro esistente.

   ![Opzioni per le aree di lavoro OMS][3]

5. Confermare le impostazioni di hello e fare clic su **salvare**.

   ![Pannello delle impostazioni di diagnostica con le selezioni][4]

### <a name="activity-log"></a>Log attività

Per impostazione predefinita, Azure genera log attività hello. Hello registri vengono mantenuti per 90 giorni nell'archivio di registri eventi Azure hello. Altre informazioni su questi registri leggendo hello [visualizzare eventi e log attività](../monitoring-and-diagnostics/insights-debugging-with-events.md) articolo.

### <a name="access-log"></a>Log di accesso

log di accesso Hello viene generato solo se è attivato in ogni istanza del Gateway applicazione, come descritto in dettaglio nella hello passaggi precedenti. Hello dati vengono archiviati nell'account di archiviazione hello specificato quando è abilitata la registrazione di hello. Ogni accesso del Gateway applicazione viene registrato nel formato JSON, come illustrato nell'esempio seguente hello:


|Valore  |Descrizione  |
|---------|---------|
|instanceId     | Gateway applicazione istanza richiesta hello servite.        |
|clientIP     | IP di origine per la richiesta di hello.        |
|clientPort     | Porta di origine per la richiesta di hello.       |
|httpMethod     | Metodo HTTP utilizzato dalla richiesta hello.       |
|requestUri     | URI della richiesta ricevuta hello.        |
|RequestQuery     | **Server di routing**: istanza del pool Back-end che è stato inviato una richiesta di hello. </br> **X-AzureApplicationGateway-LOG-ID**: ID di correlazione utilizzato per la richiesta hello. Può essere utilizzato tootroubleshoot traffico problemi nei server back-end di hello. </br>**STATO SERVER**: codice di risposta HTTP ricevuti dal back-end hello Gateway applicazione.       |
|UserAgent     | Agente utente dall'intestazione della richiesta HTTP hello.        |
|httpStatus     | Codice di stato HTTP restituito toohello client di Gateway applicazione.       |
|httpVersion     | Versione HTTP della richiesta di hello.        |
|receivedBytes     | Dimensione del pacchetto ricevuto, espressa in byte.        |
|sentBytes| Dimensione del pacchetto inviato, espressa in byte.|
|timeTaken| Periodo di tempo (in millisecondi) impiegato per una richiesta toobe elaborati e toobe la risposta inviata. Viene calcolata come intervallo hello dall'ora di hello quando il Gateway applicazione riceve il primo byte hello di un'ora di toohello richiesta HTTP quando la risposta hello inviano al termine dell'operazione. È importante toonote che hello campo Time-Taken in genere include ora hello che i pacchetti hello richiesta e risposta vengono trasmessi in rete hello. |
|sslEnabled| Indica se i pool back-end di comunicazione toohello utilizzato SSL. I valori validi sono on e off.|
```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/PEERINGTEST/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayAccess",
    "time": "2017-04-26T19:27:38Z",
    "category": "ApplicationGatewayAccessLog",
    "properties": {
        "instanceId": "ApplicationGatewayRole_IN_0",
        "clientIP": "191.96.249.97",
        "clientPort": 46886,
        "httpMethod": "GET",
        "requestUri": "/phpmyadmin/scripts/setup.php",
        "requestQuery": "X-AzureApplicationGateway-CACHE-HIT=0&SERVER-ROUTED=10.4.0.4&X-AzureApplicationGateway-LOG-ID=874f1f0f-6807-41c9-b7bc-f3cfa74aa0b1&SERVER-STATUS=404",
        "userAgent": "-",
        "httpStatus": 404,
        "httpVersion": "HTTP/1.0",
        "receivedBytes": 65,
        "sentBytes": 553,
        "timeTaken": 205,
        "sslEnabled": "off"
    }
}
```

### <a name="performance-log"></a>Log delle prestazioni

log delle prestazioni Hello viene generato solo se è abilitata in ogni istanza del Gateway applicazione, come descritto in dettaglio nella hello passaggi precedenti. Hello dati vengono archiviati nell'account di archiviazione hello specificato quando è abilitata la registrazione di hello. dati del registro prestazioni Hello viene generati in intervalli di 1 minuto. viene registrato Hello dati seguenti:


|Valore  |Descrizione  |
|---------|---------|
|instanceId     |  Istanza del gateway applicazione per cui vengono generati i dati delle prestazioni. Per un gateway applicazione a più istanze viene visualizzata una riga per ogni istanza.        |
|healthyHostCount     | Numero di host integro nel pool back-end hello.        |
|unHealthyHostCount     | Numero di host nel pool back-end hello.        |
|requestCount     | Numero di richieste gestite.        |
|latency | Latenza (in millisecondi) delle richieste da hello istanza toohello di back-end che risponde alle richieste di hello. |
|failedRequestCount| Numero di richieste non riuscite.|
|throughput| Velocità effettiva Media dall'ultimo log hello, espresso in byte al secondo.|

```json
{
    "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
    "operationName": "ApplicationGatewayPerformance",
    "time": "2016-04-09T00:00:00Z",
    "category": "ApplicationGatewayPerformanceLog",
    "properties":
    {
        "instanceId":"ApplicationGatewayRole_IN_1",
        "healthyHostCount":"4",
        "unHealthyHostCount":"0",
        "requestCount":"185",
        "latency":"0",
        "failedRequestCount":"0",
        "throughput":"119427"
    }
}
```

> [!NOTE]
> Latenza viene calcolata dal momento hello primo byte di hello della richiesta HTTP hello è ora toohello ricevuto quando non viene inviato l'ultimo byte hello di hello risposta HTTP. Gateway applicazione tempo di elaborazione di hello di hello somma di più hello toohello costo di rete torna terminare, più tempo hello hello back-end accetta tooprocess hello richiesta.

### <a name="firewall-log"></a>Log del firewall

Registro firewall Hello viene generato solo se è abilitata per il gateway ogni applicazione, come descritto in dettaglio nella hello passaggi precedenti. Questo log richiede inoltre che il firewall applicazione web hello è configurato su un gateway applicazione. Hello dati vengono archiviati nell'account di archiviazione hello specificato quando è abilitata la registrazione di hello. viene registrato Hello dati seguenti:


|Valore  |Descrizione  |
|---------|---------|
|instanceId     | Istanza del gateway applicazione per cui vengono generati i dati del firewall. Per un gateway applicazione a più istanze viene visualizzata una riga per ogni istanza.         |
|clientIp     |   IP di origine per la richiesta di hello.      |
|clientPort     |  Porta di origine per la richiesta di hello.       |
|requestUri     | URL della richiesta ricevuta hello.       |
|ruleSetType     | Tipo di set di regole. valore disponibile di Hello è OWASP.        |
|ruleSetVersion     | Versione del set di regole usata. I valori disponibili sono 2.2.9 e 3.0.     |
|ruleId     | ID regola di generazione evento hello.        |
|Message     | Messaggio descrittivo per hello evento. Ulteriori informazioni sono fornite nella sezione dettagli hello.        |
|action     |  Azione eseguita su richiesta hello. I valori disponibili sono Blocked e Allowed.      |
|site     | Sito per cui hello log è stato generato. Attualmente viene visualizzato solo Global poiché le regole sono globali.|
|informazioni dettagliate     | Dettagli dell'evento hello.        |
|details.message     | Descrizione della regola hello.        |
|details.data     | Trovare i dati specifici nella richiesta di tale regola hello corrispondente.         |
|details.file     | File di configurazione contenente una regola di hello.        |
|details.line     | Numero di riga nel file di configurazione hello che ha attivato hello evento.       |

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{applicationGatewayName}",
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

### <a name="view-and-analyze-hello-activity-log"></a>Visualizzare e analizzare i log attività hello

È possibile visualizzare e analizzare i dati del log attività utilizzando uno dei seguenti metodi hello:

* **Gli strumenti di Azure**: recuperare informazioni dal registro attività hello tramite Azure PowerShell, hello CLI di Azure, hello l'API REST di Azure o hello portale di Azure. Istruzioni dettagliate per ogni metodo sono descritti in dettaglio in hello [operazioni di attività con Gestione risorse](../azure-resource-manager/resource-group-audit.md) articolo.
* **Power BI**: se non si ha ancora un account [Power BI](https://powerbi.microsoft.com/pricing) , è possibile crearne uno di prova gratuitamente. Utilizzando hello [log attività Azure pacchetto di contenuto per Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-pack-azure-audit-logs/), è possibile analizzare i dati con i dashboard preconfigurati, che è possibile utilizzare così come sono oppure personalizzare.

### <a name="view-and-analyze-hello-access-performance-and-firewall-logs"></a>Visualizzare e analizzare accesso hello, prestazioni e i log del firewall

Azure [Log Analitica](../log-analytics/log-analytics-azure-networking-analytics.md) può raccogliere i file di registro eventi e contatori di hello dall'account di archiviazione Blob. Sono inclusi i log di visualizzazioni e tooanalyze funzionalità di ricerca avanzate.

È possibile anche connettersi tooyour account di archiviazione e recupero delle voci di log hello JSON per i log di accesso e le prestazioni. Dopo aver scaricato i file JSON hello, è possibile convertirli tooCSV e visualizzarli in Excel, Power BI o qualsiasi altro strumento di visualizzazione dei dati.

> [!TIP]
> Se si ha familiarità con Visual Studio e concetti di base di modificare i valori costanti e variabili in c#, è possibile utilizzare hello [log strumenti convertitore](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponibili da GitHub.
> 
> 

## <a name="metrics"></a>Metrica

Le metriche sono una funzionalità per alcune risorse di Azure in cui è possibile visualizzare i contatori delle prestazioni nel portale di hello. Per il gateway applicazione è ora disponibile una sola metrica. Questa metrica è la velocità effettiva ed è possibile visualizzarlo nel portale di hello. Gateway applicazione tooan e fare clic su **metriche**. i valori hello tooview, selezionare la velocità effettiva in hello **le metriche disponibili** sezione. Nella seguente immagine di hello, è possibile visualizzare un esempio con filtri di hello che è possibile utilizzare dati hello toodisplay negli intervalli di tempo diverso.

![Visualizzazione della metrica con filtri][5]

vedere un elenco corrente di metriche, toosee [metriche con Monitor di Azure supportata](../monitoring-and-diagnostics/monitoring-supported-metrics.md).

### <a name="alert-rules"></a>Regole di avviso

È possibile avviare le regole di avviso in base alle metriche per una risorsa. Ad esempio, un avviso può chiamare un webhook o un amministratore di posta elettronica se la velocità effettiva hello del gateway applicazione hello è di sopra, sotto o con una soglia per un periodo specificato.

Hello di esempio seguente viene illustrato come creare una regola di avviso che invia un amministratore di posta elettronica tooan dopo le violazioni della velocità effettiva una soglia:

1. Fare clic su **Aggiungi avviso metrica** tooopen hello **Aggiungi regola** blade. È anche possibile contattare questo pannello pannello metriche hello.

   ![Pulsante "Aggiungi avviso per la metrica"][6]

2. In hello **Aggiungi regola** pannello compilare nome hello, la condizione, inviare una notifica di sezioni e fare clic su **OK**.

   * In hello **condizione** selettore, selezionare uno dei valori hello quattro: **maggiore**, **maggiore o uguale**, **minore**, o  **Minore o uguale a**.

   * In hello **periodo** selettore, selezionare un periodo compreso tra 5 minuti too6 ore.

   * Se si seleziona **i proprietari, collaboratori e lettori di posta elettronica**, posta elettronica hello può essere dinamica in base agli utenti di hello che dispongono di accesso toothat risorse. In caso contrario, è possibile fornire un elenco delimitato da virgole di utenti in hello **email(s) amministratore aggiuntive** casella.

   ![Aggiungere il pannello delle regole][7]

Se viene superata la soglia hello, arriva un messaggio di posta elettronica è simile toohello uno in hello seguente immagine:

![Messaggio di posta elettronica per il superamento della soglia][8]

Dopo aver creato un avviso per la metrica, viene visualizzato un elenco di avvisi. Fornisce una panoramica di tutte le regole di avviso hello.

![Elenco di avvisi e regole][9]

toolearn più sulle notifiche di avviso, vedere [ricevere notifiche di avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

toounderstand ulteriori informazioni su webhook e come è possibile utilizzare con gli avvisi, visitare [configurare un webhook su un avviso di metrica Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

## <a name="next-steps"></a>Passaggi successivi

* Visualizzare i log contatori ed eventi usando [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).
* Post di blog [Visualize your Azure activity log with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) (Visualizzare il log attività di Azure con Power BI).
* Post di blog [View and analyze Azure activity logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) (Visualizzare e analizzare i log attività di Azure in Power BI e altre opzioni).

[1]: ./media/application-gateway-diagnostics/figure1.png
[2]: ./media/application-gateway-diagnostics/figure2.png
[3]: ./media/application-gateway-diagnostics/figure3.png
[4]: ./media/application-gateway-diagnostics/figure4.png
[5]: ./media/application-gateway-diagnostics/figure5.png
[6]: ./media/application-gateway-diagnostics/figure6.png
[7]: ./media/application-gateway-diagnostics/figure7.png
[8]: ./media/application-gateway-diagnostics/figure8.png
[9]: ./media/application-gateway-diagnostics/figure9.png
[10]: ./media/application-gateway-diagnostics/figure10.png
