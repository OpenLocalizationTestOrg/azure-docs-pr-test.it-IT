---
title: stato di replica di Active Directory con Azure Log Analitica aaaMonitor | Documenti Microsoft
description: Hello pack della soluzione lo stato di replica Active Directory consente di monitorare l'ambiente Active Directory per tutti gli errori di replica e regolarmente risultati hello nel dashboard OMS.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 1b988972-8e01-4f83-a7f4-87f62778f91d
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 235e4f7a066ea50b79f681398182b22c91fb6d31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-active-directory-replication-status-with-log-analytics"></a>Monitorare lo stato della replica di Active Directory con Log Analytics

![Simbolo di Stato replica di AD](./media/log-analytics-ad-replication-status/ad-replication-status-symbol.png)

Active Directory è un componente chiave di un ambiente IT aziendale. tooensure la disponibilità elevata e prestazioni elevate, ogni controller di dominio ha la propria copia del database di Active Directory hello. I controller di dominio replicano tra loro le modifiche toopropagate ordine enterprise hello. Errori nel processo di replica possono causare diversi problemi azienda hello.

Hello pack della soluzione lo stato della replica di Active Directory consente di monitorare l'ambiente Active Directory per tutti gli errori di replica e regolarmente risultati hello nel dashboard OMS.

## <a name="installing-and-configuring-hello-solution"></a>Installazione e configurazione di soluzione hello
Utilizzare hello tooinstall le informazioni seguenti e configurare la soluzione hello.

* È necessario installare gli agenti nei controller di dominio che sono membri di hello dominio toobe valutata. In alternativa, è necessario installare gli agenti nei server membri e configurare la replica dei dati tooOMS di hello agenti toosend AD. toounderstand tooconnect tooOMS computer Windows, vedere [tooLog computer Windows di connettersi Analitica](log-analytics-windows-agents.md). Se il controller di dominio è già parte di un ambiente esistente di System Center Operations Manager che si desidera tooconnect tooOMS, vedere [tooLog connettere Operations Manager Analitica](log-analytics-om-agents.md).
* Aggiungere hello lo stato di replica Active Directory soluzione tooyour all'area di lavoro OMS tramite il processo di hello [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).  Non è richiesta alcuna ulteriore configurazione.

## <a name="ad-replication-status-data-collection-details"></a>Dettagli sulla raccolta dati di Stato replica di Active Directory
Hello nella tabella seguente illustra i metodi di raccolta dati e altri dettagli sulla modalità di raccolta dati per stato di replica di Active Directory.

| Piattaforma | Agente diretto | Agente SCOM | Archiviazione di Azure | SCOM obbligatorio? | Dati dell'agente SCOM inviati con il gruppo di gestione | frequenza della raccolta |
| --- | --- | --- | --- | --- | --- | --- |
| Windows |&#8226; |&#8226; |  |  |&#8226; |ogni cinque giorni |

## <a name="optionally-enable-a-non-domain-controller-toosend-ad-data-toooms"></a>Facoltativamente, abilitare tooOMS di dati toosend AD un controller non di dominio
Se non si desidera tooconnect qualsiasi controller di dominio direttamente tooOMS, è possibile utilizzare qualsiasi altro computer connesso a OMS in toocollect il dominio dati per hello soluzione lo stato della replica di Active Directory Service pack e fare in modo inviare i dati di hello.

### <a name="tooenable-a-non-domain-controller-toosend-ad-data-toooms"></a>tooenable tooOMS di dati toosend AD un controller non di dominio
1. Verificare che tale computer hello è un membro del dominio di hello che si desidera toomonitor usando soluzione lo stato della replica hello Active Directory.
2. [Connettersi tooOMS di computer Windows hello](log-analytics-windows-agents.md) o [connettersi utilizzando il tooOMS di ambiente esistente di Operations Manager](log-analytics-om-agents.md), se non è già connessi.
3. In tale computer, impostare hello seguente chiave del Registro di sistema:

   * Chiave: **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\HealthService\Parameters\Management Groups\<ManagementGroupName>\Solutions\ADReplication**
   * Valore: **IsTarget**
   * Dati valore: **true**

   > [!NOTE]
   > Le modifiche diventano effettive fino a quando il hello di riavvio del servizio Microsoft Monitoring Agent (HealthService.exe).
   >
   >

## <a name="understanding-replication-errors"></a>Informazioni sugli errori di replica
Quando si dispone di dati di stato di replica AD inviati tooOMS, vedrai un toohello simile riquadro seguente immagine nel dashboard OMS hello che indica il numero di errori di replica è installata.  
![Riquadro Stato replica di Active Directory](./media/log-analytics-ad-replication-status/oms-ad-replication-tile.png)

**Gli errori critici di replica** sono gli errori che si trovano o superiore al 75% di hello [definitiva](https://technet.microsoft.com/library/cc784932%28v=ws.10%29.aspx) per la foresta di Active Directory.

Quando si fa clic su riquadro hello, è possibile visualizzare ulteriori informazioni sugli errori di hello.
![Dashboard Stato replica di Active Directory](./media/log-analytics-ad-replication-status/oms-ad-replication-dash.png)

### <a name="destination-server-status-and-source-server-status"></a>Stato del server di destinazione e stato del server di origine
Queste colonne indicano lo stato di hello del server di destinazione e i server di origine in cui si verificano errori di replica. numero di Hello dopo ogni nome di controller di dominio indica il numero di hello di errori di replica nel controller di dominio.

gli errori di Hello per i server di destinazione e il server di origine vengono visualizzati alcuni problemi sono più facile tootroubleshoot dalla prospettiva di server di origine hello e ad altri utenti dalla prospettiva di server di destinazione hello.

In questo esempio, si noterà che molti server di destinazione sono approssimativamente hello stesso numero di errori, ma è presente un server di origine (ADDC35) che ha molte più errori rispetto hello tutti gli altri. È probabile che vi sia un problema nel ADDC35 che causa il partner di replica tooits toofail toosend dati. Risoluzione dei problemi di hello in ADDC35 molti errori hello che vengono visualizzati nell'area server di destinazione hello potrebbe essere risolto.

### <a name="replication-error-types"></a>Tipi di errori di replica
Quest'area fornisce informazioni sui tipi di hello di errori rilevati in tutta l'organizzazione. Ogni errore con un codice numerico univoco e un messaggio che può aiutarti a determinare la causa principale di hello di errore hello.

anello Hello nella parte superiore di hello offre un'idea dei quali gli errori vengono visualizzati più e meno di frequente nel proprio ambiente.

Viene illustrato quando più controller di dominio verificano hello lo stesso errore di replica. In questo caso, si potrebbe essere in grado di toodiscover o identificare una soluzione in un controller di dominio, quindi ripetere su altri controller di dominio interessati hello stesso errore.

### <a name="tombstone-lifetime"></a>durata di rimozione definitiva
durata oggetto contrassegnato per rimozione Hello determina quanto tempo un oggetto eliminato, noto tooas rimozione definitiva, verrà conservata nel database di Active Directory hello. Quando un oggetto eliminato passa hello durata della rimozione, un processo di garbage collection rimuove automaticamente dal database di Active Directory hello.

durata della rimozione di Hello predefinito è 180 giorni, per le versioni più recenti di Windows, ma era 60 giorni nelle versioni precedenti e può essere modificata in modo esplicito da un amministratore di Active Directory.

È importante tooknow se si verificano errori di replica che si stanno avvicinando o hanno superato la durata della rimozione hello. Se due controller di dominio verifica un errore di replica che rende persistente oltre la durata della rimozione hello, la replica viene disabilitata tra i due controller di dominio, anche se hello replica errore sottostante è fissa.

Hello area definitiva consente di identificare i punti in cui la replica disabilitata è il rischio di verificarsi. Ogni errore hello **il 100% TSL** categoria rappresenta una partizione che non ha replicato tra il server di origine e di destinazione alla durata della rimozione hello minimo per la foresta hello.

In questo caso, semplicemente la correzione di errore di replica hello non sarà sufficiente. Come minimo, è necessario toomanually tooidentify di analizzare e pulire gli oggetti il tempo di ritardo prima di poter riavviare la replica. Potrebbe anche essere toodecommission un controller di dominio.

In aggiunta tooidentifying eventuali errori della replica che sono rese persistenti oltre hello definitiva, inoltre desidera toopay attenzione tooany gli errori rientrano hello **TSL 50-75%** o **TSL 75-100%** categorie.

Si tratta di errori che sono chiaramente residui, non temporaneo, pertanto è probabilmente necessario tooresolve l'intervento. buone notizie Hello sono che essi non hanno ancora raggiunto definitiva hello. Se si corregge i problemi tempestivamente e *prima* raggiungono definitiva hello, riavvia la replica con un minimo intervento manuale.

Come notato in precedenza, riquadro del dashboard per la soluzione di stato di replica hello AD hello Mostra il numero di hello di *critico* nel proprio ambiente, che è definita come gli errori che sono più del 75% della durata oggetto contrassegnato per rimozione (inclusi gli errori di replica errori che sono su 100% di TSL). Cercare tookeep questo numero da 0.

> [!NOTE]
> I calcoli di percentuale durata di rimozione definitiva di tutti i hello sono basati sulla durata della rimozione effettiva hello per la foresta di Active Directory, in modo che tali percentuali sono precisione, anche se è impostato un valore di durata personalizzati per la rimozione è attendibile.
>
>

### <a name="ad-replication-status-details"></a>Dettagli di Stato replica di Active Directory
Quando si fa clic su qualsiasi elemento in uno degli elenchi di hello, visualizzare ulteriori dettagli su di esso con ricerca di Log. risultati di Hello sono filtrati tooshow solo hello errori correlati toothat elemento. Ad esempio, se si fa clic sul primo controller di dominio hello elencata sotto **dello stato del Server di destinazione (ADDC02)**, vedrai risultati di ricerca filtrati tooshow errori con il controller di dominio elencato come server di destinazione hello:

![Errori di stato replica di Active Directory nei risultati della ricerca](./media/log-analytics-ad-replication-status/oms-ad-replication-search-details.png)

Da qui, è possibile filtrare ulteriormente, modificare la query di ricerca hello e così via. Per ulteriori informazioni sull'utilizzo di hello ricerca nei Log, vedere [Log ricerche](log-analytics-log-searches.md).

Hello **HelpLink** campo Mostra hello URL di una pagina di TechNet con dettagli aggiuntivi sull'errore specifico. È possibile copiare e incollare il collegamento del browser finestra toosee le informazioni sulla risoluzione dei problemi e correzione di errore hello.

È anche possibile fare clic su **esportare** tooexport hello risultati tooExcel. Esportazione di dati hello consentono di visualizzare i dati di errore di replica in qualsiasi modo desiderato.

![errori di stato replica di Active Directory esportati in Excel](./media/log-analytics-ad-replication-status/oms-ad-replication-export.png)

## <a name="ad-replication-status-faq"></a>Domande frequenti su Stato replica di Active Directory
**D: con quale frequenza vengono aggiornati i dati di Stato replica di Active Directory?**
R: hello informazioni vengono aggiornate ogni cinque giorni.

**D: è un modo tooconfigure la frequenza di aggiornamento dati?**
R: attualmente non è possibile.

**D: si necessario tooadd tutti my domain controller toomy area di lavoro OMS nello stato di replica toosee ordine?**
R: no, è necessario aggiungere un solo controller di dominio. Se si dispone di più controller di dominio nell'area di lavoro OMS, i dati da tutti gli elementi vengono inviati tooOMS.

**D: non si desidera tooadd qualsiasi area di lavoro OMS di toomy i controller di dominio. È possibile utilizzare hello soluzione lo stato della replica di Active Directory?**
A: Sì. È possibile impostare il valore di hello di un tooenable chiave del Registro di sistema è. Vedere [tooenable tooOMS di dati toosend AD un controller di dominio non](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).

**D: qual è il nome di hello del processo di hello hello la raccolta dei dati?**
R: AdvisorAssessment.exe

**D: come tempo occorre per toobe dati raccolti?**
R: tempo di raccolta dati di dipende dalle dimensioni hello dell'ambiente Active Directory hello, ma in genere richiede meno di 15 minuti.

**D: quali tipi di dati vengono raccolti?**
R: le informazioni di replica vengono raccolte tramite LDAP.

**D: è un modo tooconfigure la raccolta dei dati?**
R: attualmente non è possibile.

**D: che cosa fare le autorizzazioni sono necessarie toocollect dati?**
R: normale utente autorizzazioni tooActive Directory sono sufficienti.

## <a name="troubleshoot-data-collection-problems"></a>Risolvere i problemi di raccolta dati
Dati degli ordini toocollect, pacchetto di soluzione lo stato della replica di hello AD richiede almeno un dominio controller toobe connesso tooyour area di lavoro OMS. Fino a quando non ci si connette a un controller di dominio, viene visualizzato un messaggio che indica che **la raccolta di dati è ancora in corso**.

Se occorre assistenza per la connessione a uno dei controller di dominio, è possibile visualizzare la documentazione in [tooLog computer Windows di connettersi Analitica](log-analytics-windows-agents.md). In alternativa, se il controller di dominio è già connesso tooan ambiente System Center Operations Manager, è possibile visualizzare la documentazione in [tooLog connettere System Center Operations Manager Analitica](log-analytics-om-agents.md).

Se non si desidera tooconnect qualsiasi controller di dominio direttamente tooOMS o tooSCOM, vedere [tooenable tooOMS di dati toosend AD un controller di dominio non](#to-enable-a-non-domain-controller-to-send-ad-data-to-oms).

## <a name="next-steps"></a>Passaggi successivi
* Utilizzare [Accedi ricerche Log Analitica](log-analytics-log-searches.md) tooview in dettaglio i dati di stato di replica di Active Directory.
