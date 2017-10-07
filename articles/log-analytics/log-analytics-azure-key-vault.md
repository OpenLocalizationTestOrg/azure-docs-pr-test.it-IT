---
title: soluzione di insieme di credenziali chiave nel registro Analitica aaaAzure | Documenti Microsoft
description: "È possibile utilizzare soluzioni insieme credenziali chiavi Azure hello in tooreview Analitica Log che registra insieme credenziali chiavi Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 5e25e6d6-dd20-4528-9820-6e2958a40dae
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 1c6eae26ded7ad55b0159a3be09cdc9901596298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-analytics-solution-in-log-analytics"></a>Soluzione di Azure Key Vault Analytics in Log Analytics

![Simbolo di Key Vault](./media/log-analytics-azure-keyvault/key-vault-analytics-symbol.png)

È possibile utilizzare soluzioni insieme credenziali chiavi Azure hello in tooreview Analitica Log che registra AuditEvent insieme di credenziali chiave di Azure.

soluzione hello toouse, è necessario tooenable registrazione di diagnostica Azure insieme di credenziali chiave e dell'area di lavoro di hello diretto diagnostica tooa Analitica di Log. Non è necessario toowrite nell'archiviazione Blob tooAzure hello registri.

> [!NOTE]
> Nel gennaio January 2017, hello supportate consentono di inviare i log dall'insieme di credenziali chiave tooLog che Analitica modificato. Mostra se soluzione insieme di credenziali chiave hello utilizza *(obsoleto)* nel titolo hello, fare riferimento troppo[la migrazione da una soluzione di insieme di credenziali chiave precedente hello](#migrating-from-the-old-key-vault-solution) per la procedura è necessario toofollow.
>
>

## <a name="install-and-configure-hello-solution"></a>Installare e configurare la soluzione hello
Utilizzare hello seguendo le istruzioni tooinstall e configurare la soluzione insieme credenziali chiavi Azure hello:

1. Abilitare soluzioni insieme credenziali chiavi Azure hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) o tramite il processo di hello descritto in [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).
2. Abilitare la diagnostica per toomonitor risorse di hello insieme di credenziali chiave di registrazione, utilizzando entrambi hello [portale](#enable-key-vault-diagnostics-in-the-portal) o [PowerShell](#enable-key-vault-diagnostics-using-powershell)

### <a name="enable-key-vault-diagnostics-in-hello-portal"></a>Abilitare la diagnostica di insieme di credenziali chiave nel portale di hello

1. Nel portale di Azure hello, spostarsi toohello insieme di credenziali chiave risorsa toomonitor
2. Selezionare *log di diagnostica* hello tooopen dopo

   ![Immagine del riquadro Insieme di credenziali delle chiavi di Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics01.png)
3. Fare clic su *attivare la diagnostica* hello tooopen dopo

   ![Immagine del riquadro Insieme di credenziali delle chiavi di Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics02.png)
4. tooturn sulla diagnostica, fare clic su *su* in *stato*
5. Fare clic sulla casella di controllo hello *inviare tooLog Analitica*
6. Selezionare un'area di lavoro Log Analytics esistente o creare una
7. tooenable *AuditEvent* log, fare clic su casella di controllo hello in Log
8. Fare clic su *salvare* registrazione hello tooenable di diagnostica tooLog Analitica

### <a name="enable-key-vault-diagnostics-using-powershell"></a>Abilitare la diagnostica di Key Vault utilizzando PowerShell
Hello lo script di PowerShell seguente viene fornito un esempio di come toouse `Set-AzureRmDiagnosticSetting` tooenable registrazione diagnostica per l'insieme di credenziali chiave:
```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```



## <a name="review-azure-key-vault-data-collection-details"></a>Esaminare i dettagli della raccolta di dati dell'Insieme di credenziali delle chiavi di Azure
Soluzione insieme di credenziali chiave di Azure raccoglie i log di diagnostica direttamente da hello insieme di credenziali chiave.
Non è necessario toowrite hello registri tooAzure nell'archiviazione Blob e non è richiesto per la raccolta dati.

Hello nella tabella seguente illustra i metodi di raccolta dati e altri dettagli sulla modalità di raccolta dati per insieme credenziali chiavi Azure.

| Piattaforma | Agente diretto | Agente di Systems Center Operations Manager | Azure | È necessario Operations Manager? | Dati dell'agente Operations Manager inviati con il gruppo di gestione | Frequenza della raccolta |
| --- | --- | --- | --- | --- | --- | --- |
| Azure |  |  |&#8226; |  |  | all'arrivo |

## <a name="use-azure-key-vault"></a>Usare l'Insieme di credenziali delle chiavi di Azure
Dopo aver [installare la soluzione hello](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), visualizzare i dati di insieme di credenziali chiave hello facendo hello **insieme credenziali chiavi Azure** riquadro da hello **Panoramica** pagina del Log Analitica.

![Immagine del riquadro Insieme di credenziali delle chiavi di Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault-tile.png)

Dopo aver fatto clic hello **Panoramica** riquadro, è possibile visualizzare i riepiloghi dei log e quindi drill in toodetails per hello seguenti categorie:

* Volume di tutte le operazioni dell'insieme di credenziali delle chiavi nel tempo
* Volumi di operazioni non riuscite nel tempo
* Latenza operativa media per operazione
* Qualità del servizio per le operazioni con il numero di hello delle operazioni che richiedono più di 1000 ms e un elenco delle operazioni che richiedono più di 1000 ms

![Immagine del dashboard dell'Insieme di credenziali delle chiavi di Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault01.png)

![Immagine del dashboard dell'Insieme di credenziali delle chiavi di Azure](./media/log-analytics-azure-keyvault/log-analytics-keyvault02.png)

### <a name="tooview-details-for-any-operation"></a>Dettagli tooview per qualsiasi operazione
1. In hello **Panoramica** pagina, fare clic su hello **insieme credenziali chiavi Azure** riquadro.
2. In hello **insieme credenziali chiavi Azure** dashboard, esaminare le informazioni di riepilogo hello in uno dei pannelli hello e quindi fare clic su uno tooview dettagliate le informazioni nella pagina di ricerca log hello.

    In qualsiasi pagina di ricerca log hello di, è possibile visualizzare i risultati dal tempo, i risultati dettagliati e alla cronologia di ricerca. È inoltre possibile filtrare dai risultati di hello toonarrow facet.

## <a name="log-analytics-records"></a>Record di Log Analytics
Hello soluzione insieme credenziali chiavi Azure analizza i record che hanno un tipo di **KeyVaults** che vengono raccolti da [AuditEvent registri](../key-vault/key-vault-logging.md) in diagnostica di Azure.  Le proprietà per tali record sono in hello nella tabella seguente:  

| Proprietà | Descrizione |
|:--- |:--- |
| Tipo |*AzureDiagnostics* |
| SourceSystem |*Azzurro* |
| CallerIpAddress |Indirizzo IP del client hello che ha effettuato la richiesta hello |
| Categoria | *AuditEvent* |
| CorrelationId |Un GUID facoltativo che hello client può passare toocorrelate log lato client con i registri dal lato del servizio (insieme di credenziali chiave). |
| DurationMs |Tempo impiegato richiesta dell'API REST hello tooservice, in millisecondi. Questa volta non include la latenza di rete, pertanto ora hello in cui si esegue una misurazione sul lato client hello potrebbe non corrispondere a questo momento. |
| httpStatusCode_d |Codice di stato HTTP restituito dalla richiesta hello (ad esempio, *200*) |
| id_s |ID univoco della richiesta di hello |
| identity_claim_appid_g | GUID per l'id applicazione hello |
| OperationName |Nome dell'operazione di hello, come documentato [la registrazione dell'insieme di credenziali chiave di Azure](../key-vault/key-vault-logging.md) |
| OperationVersion |Versione dell'API REST richiesto da hello client (ad esempio *2015-06-01*) |
| requestUri_s |URI della richiesta di hello |
| Risorsa |Nome dell'insieme di credenziali chiave hello |
| ResourceGroup |Gruppo di risorse dell'insieme di credenziali chiave hello |
| ResourceId |ID della risorsa Gestione risorse di Azure. Per i registri di insieme di credenziali chiave, si tratta di ID di risorsa hello insieme di credenziali chiave. |
| ResourceProvider |*MICROSOFT.KEYVAULT* |
| ResourceType | *VAULTS* |
| ResultSignature |Stato HTTP (ad esempio *OK*) |
| ResultType |Risultato della richiesta dell'API REST (ad esempio *Operazione completata*) |
| SubscriptionId |ID sottoscrizione di Azure della sottoscrizione hello contenente hello insieme di credenziali chiave |

## <a name="migrating-from-hello-old-key-vault-solution"></a>La migrazione da una soluzione di insieme di credenziali chiave precedente hello
Nel gennaio January 2017, hello supportate consentono di inviare i log dall'insieme di credenziali chiave tooLog che Analitica modificato. Queste modifiche consentono hello seguenti vantaggi:
+ I log vengono scritti direttamente tooLog Analitica senza hello necessario toouse un account di archiviazione
+ Minore latenza dall'ora di hello quando i registri sono generati toothem disponibile nel Log Analitica
+ Meno passaggi di configurazione
+ Un formato comune per tutti i tipi di diagnostica di Azure

soluzione hello aggiornato toouse:

1. [Configurare diagnostica toobe inviato tooLog Analitica direttamente dall'insieme di credenziali chiave](#enable-key-vault-diagnostics-in-the-portal)  
2. Per abilitare soluzioni insieme credenziali chiavi Azure hello hello processo descritto in [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md)
3. Aggiornare le query salvate, dashboard o avvisi toouse hello nuovo tipo di dati
  + È di tipo di modifica da: KeyVaults tooAzureDiagnostics. È possibile utilizzare hello ResourceType toofilter tooKey insieme di credenziali di log.
  - Invece di: `Type=KeyVaults`, utilizzare i campi `Type=AzureDiagnostics ResourceType=VAULTS`:
  + I nomi dei campi distinguono tra maiuscole e minuscole
  - Per qualsiasi campo che contiene un suffisso di \_s, \_d, o \_g in nome hello cambia hello primo carattere toolower maiuscole/minuscole
  - Per qualsiasi campo che contiene un suffisso di \_o nel nome, i dati di hello è suddiviso in singoli campi in base ai nomi di campo hello annidato. Ad esempio, hello UPN del chiamante hello viene archiviato in un campo`identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`
   - TooCallerIPAddress CallerIpAddress campo modificato
   - Il campo RemoteIPCountry non è più presente
4. Rimuovere hello *chiave dell'insieme di credenziali Analitica (obsoleto)* soluzione. Se si utilizza PowerShell, usare `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`

I dati raccolti prima modifica hello non è visibile nella nuova soluzione hello. È possibile continuare tooquery per questa operazione utilizzando dati hello vecchio tipo e i nomi dei campi.

## <a name="troubleshooting"></a>Risoluzione dei problemi
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>Passaggi successivi
* Utilizzare [Accedi ricerche Log Analitica](log-analytics-log-searches.md) tooview in dettaglio i dati insieme credenziali chiavi Azure.
