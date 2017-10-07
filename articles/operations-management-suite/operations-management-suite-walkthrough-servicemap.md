---
title: aaaService mappa soluzione corsi demo | Documenti Microsoft
description: "Mappa del servizio è una soluzione di Operations Management Suite (OMS) che rileva automaticamente i componenti dell'applicazione in Windows e mappe e i sistemi Linux hello la comunicazione tra servizi.  Si tratta di una demo valore speciale paced autonoma che viene illustrato l'utilizzo di mapping servizio tooidentify e diagnostica un problema simulato in un'applicazione web."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: 13f26241cd55a9b35c07d6ca52760a968abffc64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-oms-self-paced-demo---service-map"></a>Demo per la formazione autonoma sulla soluzione Service Map in Operations Management Suite (OMS)
Si tratta di una demo valore speciale paced self che illustra l'utilizzo di hello [soluzione mappa del servizio](operations-management-suite-service-map.md) in tooidentify Operations Management Suite (OMS) e diagnosticare un problema simulato in un'applicazione web.  Mappa del servizio consente di individuare automaticamente i componenti dell'applicazione nei sistemi Windows e Linux e mappe hello la comunicazione tra servizi.  Consente di consolidare i dati raccolti da altri tooassist di servizi OMS l'analisi delle prestazioni e l'identificazione dei problemi.  Si utilizzeranno inoltre [Accedi ricerche Log Analitica](../log-analytics/log-analytics-log-searches.md) toodrill verso il basso sui dati raccolti in problema principale hello tooidentify di ordine.


## <a name="scenario-description"></a>Descrizione dello scenario
Appena ricevuto una notifica che un'applicazione hello portale per i clienti ACME problemi di prestazioni.  Hello solo le informazioni che occorre sono che questi problemi ha iniziato a circa 4:00 am PST oggi.  Si è sicuri di interamente di tutti i componenti di hello tale portale hello dipende diverso da un set di server web.  

## <a name="components-and-features-used"></a>Componenti e le funzionalità usati
- [Soluzione Service Map](operations-management-suite-service-map.md)
- [Ricerche nei log in Log Analytics](../log-analytics/log-analytics-log-searches.md)


## <a name="walk-through"></a>Procedura dettagliata

### <a name="1-connect-toohello-oms-experience-center"></a>1. Connessione toohello OMS esperienza Center
Questa procedura dettagliata Usa hello [Operations Management Suite esperienza Center](https://experience.mms.microsoft.com/) che fornisce un ambiente completo di OMS con dati di esempio. Per iniziare, seguendo il collegamento, fornire le informazioni e quindi selezionare hello **Insight & Analitica** scenario.


### <a name="2-start-service-map"></a>2. Avviare Service Map
Avviare Esplora mappa del servizio hello facendo clic su hello **mappa del servizio** riquadro.

![Riquadro Service Map](media/operations-management-suite-walkthrough-servicemap/tile.png)

console di Hello mappa del servizio viene visualizzato.  In hello riquadro sinistro è un elenco di computer nell'ambiente di cui è installato l'agente di mapping servizio hello.  Basta selezionare i computer hello che si desidera tooview da questo elenco.

![Elenco di computer](media/operations-management-suite-walkthrough-servicemap/computer-list.png)


### <a name="3-view-computer"></a>3. Visualizzare un computer
Sappiamo che i server web hello sono dette AcmeWFE001 e AcmeWFE002, pertanto questa opzione sembri toostart una scelta ragionevole.  Fare clic su **AcmeWFE001**.  Consente di visualizzare la mappa hello per AcmeWFE001 e tutte le relative dipendenze.  È possibile visualizzare i processi in esecuzione sul computer selezionato hello e che comunicano con i servizi esterni.

![Server Web](media/operations-management-suite-walkthrough-servicemap/web-server.png)

Siamo massimizzare le prestazioni di hello del nostro web applicazione fare quindi clic su hello **AcmeAppPool (Pool di applicazioni IIS)** processo.  Consente di visualizzare i dettagli di hello per questo processo e vengono evidenziate le relative dipendenze.  

![Pool di app](media/operations-management-suite-walkthrough-servicemap/app-pool.png)


### <a name="4-change-time-window"></a>4. Cambiare l'intervallo di tempo

Preferire tale problema hello iniziato alle 4:00 AM andiamo esaminerà Qual era il problema in quel momento. Fare clic su **intervallo di tempo** e modificare hello ora too4: 00 AM PST (mantenere hello data corrente e regolare per il fuso orario locale) di durata pari a 20 minuti.

![Selezione ora](./media/operations-management-suite-walkthrough-servicemap/time-picker.png)


### <a name="5-view-alert"></a>5. Visualizzare un avviso

Vediamo ora tale hello **acmetomcat** dipendenza è un avviso, in modo che il problema.  Fare clic sull'icona di avviso hello in **acmetomcat** dettagli hello tooshow per avviso hello.  L'utilizzo della CPU è indicato come critico ed è possibile espandere l'avviso per visualizzare altri dettagli.  Si tratta probabilmente della causa del rallentamento delle prestazioni. 

![Avviso](./media/operations-management-suite-walkthrough-servicemap/alert.png)


### <a name="6-view-performance"></a>6. Visualizzare le prestazioni

Esaminare **acmetomcat** più da vicino.  Fare clic nella hello superiore destra della **acmetomcat** e selezionare **carico Server mappa** tooshow hello dettagli e le dipendenze per questa macchina. È possibile quindi analizzare un po' più in tali tooverify i contatori delle prestazioni nostri sospetto.  Seleziona hello **prestazioni** hello toodisplay scheda [i contatori delle prestazioni raccolti da Log Analitica](../log-analytics/log-analytics-data-sources-performance-counters.md) in intervallo di tempo hello.  Possiamo vedere che ci troviamo picchi periodici nell'hello processore e memoria.

![Prestazioni](./media/operations-management-suite-walkthrough-servicemap/performance.png)


### <a name="7-view-change-tracking"></a>7. Visualizzare il rilevamento modifiche
Provare ora a scoprire la possibile causa di questo utilizzo elevato.  Fare clic su hello **riepilogo** scheda.  Fornisce informazioni che OMS sono raccolti da computer hello, ad esempio non è stato possibile connessioni, gli avvisi critici e le modifiche del software.  Le sezioni con interessanti informazioni recenti devono già essere espanso, ed è possibile espandere tooinspect informazioni nelle sezioni che contengono.


Espandere **Rilevamento modifiche**, se non è già aperto.  Mostra le informazioni raccolte da hello [soluzione Change Tracking](../log-analytics/log-analytics-change-tracking.md).  Sembra che in questo intervallo di tempo sia stata apportata una modifica al software.  Fare clic su **Software** tooget dettagli.  Un processo di backup è stato aggiunto macchina toohello subito dopo 4:00 AM, in modo causa hello toobe per hello eccessivo di risorse viene utilizzato questo valore viene visualizzato.

![Rilevamento modifiche](./media/operations-management-suite-walkthrough-servicemap/change-tracking.png)



### <a name="8-view-details-in-log-search"></a>8. Visualizzare i dettagli nella ricerca dei log
È possibile verificare ulteriormente questo esaminando hello dettagliate informazioni sulle prestazioni raccolte nell'archivio di Log Analitica hello.  Fare clic su hello **avvisi** scheda nuovo e quindi su una delle hello **elevato della CPU** gli avvisi.  Fare clic su **Mostra in Ricerca log**.  Verrà visualizzata una finestra di ricerca nei Log hello in cui è possibile eseguire [log ricerche](../log-analytics/log-analytics-log-searches.md) su tutti i dati archiviati nel repository di hello.  Mappa del servizio è già presente un queriy per noi avviso hello tooretrieve si è interessati.  

![Ricerca log](./media/operations-management-suite-walkthrough-servicemap/log-search.png)


### <a name="9-open-saved-search"></a>9. Aprire una ricerca salvata
Vediamo se è possibile ottenere alcuni ulteriori dettagli su raccolta prestazioni hello che ha generato questo avviso e verificare se il nostro sospetto che problemi di hello sono causati da tale processo di backup.  Modificare anche l'intervallo di tempo hello**6 ore**.  Fare clic su **Preferiti** e scorrere verso il basso toohello salvato Cerca **mappa del servizio**.  Si tratta delle query create in modo specifico per l'analisi.  Fare clic su **Top 5 Processes by CPU for acmetomcat** (Primi 5 processi per CPU per acmetomcat).

![Ricerca salvata](./media/operations-management-suite-walkthrough-servicemap/saved-search.png)


Questa query restituisce un elenco di hello processi primi 5 utilizzo del processore in **acmetomcat**.  È possibile esaminare hello query tooget un linguaggio di query toohello introduzione utilizzato per ricerche nei log.  Se si era interessati a processi hello in altri computer, è possibile modificare hello query tooretrieve tali informazioni.

In questo caso, si noterà che hello processo di backup in modo coerente utilizza circa 60% della CPU del server di app hello.  È evidente che questo processo è la causa del problema di prestazioni.  La soluzione sarebbe ovviamente tooremove questo nuovo software server di applicazione hello di backup.  È possibile sfruttare effettivamente stato configurazione DSC (Desired) gestiti da criteri di toodefine di automazione di Azure per garantire che questo processo non viene mai eseguita su tali sistemi critici.


## <a name="summary-points"></a>Riepilogo
- [Service Map](operations-management-suite-service-map.md) permette di visualizzare l'intera applicazione, anche se non se ne conoscono tutti i server e le dipendenze.
- Mappa del servizio espone i dati raccolti da altri toohelp soluzioni OMS identificare i problemi con l'applicazione e l'infrastruttura sottostante.
- [Log delle ricerche](../log-analytics/log-analytics-log-searches.md) consentono di organizzare toodrill verso il basso in dati specifici raccolti nel repository di hello Analitica di Log.    

## <a name="next-steps"></a>Passaggi successivi
- Altre informazioni su [Service Map](operations-management-suite-service-map.md).
- [Distribuire e configurare](operations-management-suite-service-map-configure.md) Service Map.
- Informazioni su [Log Analytics](../log-analytics/log-analytics-overview.md), necessario per Service Map, che archivia i dati operativi memorizzati dagli agenti.