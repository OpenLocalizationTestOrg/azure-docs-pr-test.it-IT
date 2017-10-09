---
title: aaaIIS registra nel Log Analitica | Documenti Microsoft
description: "Internet Information Services (IIS) archivia le attività dell'utente in file log che possono essere raccolti da Log Analytics.  In questo articolo viene descritto come tooconfigure raccolta di log di IIS e i dettagli del record di hello che ha creato nel repository OMS hello."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: cec5ff0a-01f5-4262-b2e8-e3db7b7467d2
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: bwren
ms.openlocfilehash: c5575351090cdabaf651bcb49867794ee3a4b6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="iis-logs-in-log-analytics"></a>Log di IIS in Log Analytics
Internet Information Services (IIS) archivia le attività dell'utente in file log che possono essere raccolti da Log Analytics.  

![Log di IIS](media/log-analytics-data-sources-iis-logs/overview.png)

## <a name="configuring-iis-logs"></a>Configurazione dei log di IIS
Log Analytics raccoglie le voci dai file log creati da IIS, quindi è necessario [configurare la registrazione in IIS](https://technet.microsoft.com/library/hh831775.aspx).

Log Analytics supporta solo i file log IIS archiviati in formato W3C e non supporta campi personalizzati o IIS Advanced Logging.  
Log Analytics non raccoglie log in formato nativo NCSA o IIS.

Configurare i log di IIS in Log Analitica da hello [menu dati nelle impostazioni di registro Analitica](log-analytics-data-sources.md#configuring-data-sources).  Non occorre selezionare nessuna impostazione oltre a **Raccogli i file di log IIS in formato W3C**.

È consigliabile quando si abilita la raccolta di log IIS, è necessario configurare impostazione rollover del log IIS hello in ogni server.

## <a name="data-collection"></a>Raccolta dei dati
Log Analytics raccoglie le voci dei log di IIS da ogni origine connessa a intervalli di circa 15 minuti.  agente Hello registra al suo posto in ogni log di eventi raccolti da.  Se l'agente hello è offline, quindi Log Analitica raccoglie gli eventi dall'ultimo libero, anche se tali eventi sono stati creati mentre hello agent era offline.

## <a name="iis-log-record-properties"></a>Proprietà dei record del log di IIS
I record di log IIS sono un tipo di **W3CIISLog** e dispone di proprietà hello in hello nella tabella seguente:

| Proprietà | Descrizione |
|:--- |:--- |
| Computer |Nome del computer hello hello eventi raccolti da. |
| cIP |Indirizzo IP del client hello. |
| csMethod |Metodo della richiesta di hello, ad esempio GET o POST. |
| csReferer |Sito che hello utente seguito un collegamento dal sito corrente toohello. |
| csUserAgent |Tipo di browser del client hello. |
| csUserName |Nome di hello autenticato l'utente che ha avuto accesso server hello. Gli utenti anonimi sono indicati da un trattino. |
| csUriStem |Destinazione della richiesta di hello, ad esempio una pagina web. |
| csUriQuery |Query, se presente, tale client hello cercava tooperform. |
| ManagementGroupName |Nome del gruppo di gestione di hello per gli agenti di Operations Manager.  Per gli altri agenti, corrisponde ad AOI-\<ID area di lavoro\> |
| RemoteIPCountry |Paese dell'indirizzo IP di hello del client hello. |
| RemoteIPLatitude |Latitudine dell'indirizzo IP del client hello. |
| RemoteIPLongitude |Longitudine dell'indirizzo IP del client hello. |
| scStatus |Codice stato HTTP. |
| scSubStatus |Codice errore dello stato secondario. |
| scWin32Status |Codice di stato Windows. |
| sIP |Indirizzo IP del server web hello. |
| SourceSystem |OpsMgr |
| sPort |Porta su hello server hello client connesso. |
| sSiteName |Nome del sito IIS hello. |
| TimeGenerated |Data e ora voce hello è stata registrata. |
| TimeTaken |Richiesta di lunghezza di hello tooprocess tempo in millisecondi. |

## <a name="log-searches-with-iis-logs"></a>Ricerche nei log con i log di IIS
Hello nella tabella seguente vengono forniti esempi di query di log che recuperano i record di log IIS.

| Query | Descrizione |
|:--- |:--- |
| Type=W3CIISLog |Tutti i record del log di IIS. |
| Type=W3CIISLog scStatus=500 |Tutti i record del log IIS con stato restituito pari a 500. |
| Tipo=W3CIISLog &#124; Measure count() by cIP |Numero di voci del log di IIS in base all'indirizzo IP del client. |
| Tipo=W3CIISLog csHost="www.contoso.com" &#124; Measure count() by csUriStem |Conteggio di IIS voci dall'URL per hello host www.contoso.com di log. |
| Tipo=W3CIISLog &#124; Measure Sum(csBytes) by Computer &#124; top 500000 |Numero totale di byte ricevuti da ogni computer che esegue IIS. |

>[!NOTE]
> Se l'area di lavoro è stato aggiornato toohello [Analitica Log nuovo linguaggio di query](log-analytics-log-search-upgrade.md), quindi hello sopra query modificherebbe toohello seguente.

> | Query | Descrizione |
|:--- |:--- |
| W3CIISLog |Tutti i record del log di IIS. |
| W3CIISLog &#124; where scStatus==500 |Tutti i record del log IIS con stato restituito pari a 500. |
| W3CIISLog &#124; summarize count() by cIP |Numero di voci del log di IIS in base all'indirizzo IP del client. |
| W3CIISLog &#124; where csHost=="www.contoso.com" &#124; summarize count() by csUriStem |Conteggio di IIS voci dall'URL per hello host www.contoso.com di log. |
| W3CIISLog &#124; summarize sum(csBytes) by Computer &#124; take 500000 |Numero totale di byte ricevuti da ogni computer che esegue IIS. |

## <a name="next-steps"></a>Passaggi successivi
* Configurare altri toocollect Log Analitica [origini dati](log-analytics-data-sources.md) per l'analisi.
* Informazioni su [log ricerche](log-analytics-log-searches.md) tooanalyze hello dati raccolti da origini dati e le soluzioni.
* Configurare gli avvisi nel registro Analitica tooproactively notifica di condizioni importanti riscontrate nei log IIS.
