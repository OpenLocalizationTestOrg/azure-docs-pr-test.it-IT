---
title: "aaaDashboard, monitoraggio, scalabilità, configura e le connessioni ibride in servizi BizTalk | Documenti Microsoft"
description: "Informazioni sui controlli hello e monitorare le prestazioni nelle schede portale classico hello per i servizi BizTalk: Dashboard, monitoraggio, scalabilità, configura e le connessioni ibride. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7a1815db-0de2-4274-8be0-198c1b077324
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c9fafdad20489571ee3849bbacd2c2b10933154f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="review-hello-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a>Esaminare le schede del Dashboard, monitoraggio, scalabilità, configura e connessione ibrida hello

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Dopo aver creato il BizTalk Service e distribuire l'applicazione, è possibile modificare alcune delle impostazioni del servizio BizTalk hello e monitorare le prestazioni dell'applicazione hello. 

Quando si apre hello portale di Azure classico, viene automaticamente indirizzato alla hello **tutti gli elementi** scheda tooview il BizTalk Service, selezionare il BizTalk Service in hello **tutti gli elementi** tab o seleziona hello **Servizi BIZTALK** ; e quindi selezionare il nome di BizTalk Service.

Verrà visualizzata una nuova finestra con hello seguenti schede. In questo argomento vengono descritte queste schede.

## <a name="quickstart-quickstartquickstart"></a>Guida introduttiva (![Guida introduttiva][Quickstart])
A seconda di hello BizTalk Services Edition, tutte le opzioni elencate non siano disponibili. 

<table border="1">
    <tr>
        <td><strong>Ottenere strumenti hello</strong></td>
        <td>Scaricare i modelli di progetto Visual Studio per la hello tooinstall hello BizTalk Services SDK nel computer di sviluppo locale. Questi modelli creano hello <strong>servizi BizTalk</strong> (bridge) e hello <strong>elementi del servizio BizTalk</strong> progetti di Visual Studio (Transform) che sono distribuiti tooyour BizTalk Service.
        <br/><br/>
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Come avviare in uso hello Azure BizTalk Services SDK </a> e <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">hello installare Azure BizTalk Services SDK</a> elenchi hello tooget passaggi avviato.
        </td>
    </tr>
    <tr>
        <td><strong>Creare contratti con il partner</strong></td>
        <td>Verrà visualizzata la hello portale servizi BizTalk di Azure ospitati in Azure in cui si aggiungere partner e creare X12, AS2 e i contratti EDIFACT EDI.
        <br/><br/>
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurazione dei componenti per la messaggistica EDI nel portale dei servizi BizTalk</a> elenchi hello tooget passaggi avviato.
        </td>
    </tr>

<tr>
        <td><strong>Altre informazioni sui Servizi BizTalk</strong></td>
        <td>Passare toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> toolearn informazioni sui servizi BizTalk di Azure.</td>
</tr>
</table>


Nella barra delle applicazioni hello nella parte inferiore di hello, è possibile:

<table border="1">

<tr>
<td><strong>Gestire</strong> la distribuzione delle applicazioni</td>
<td>È possibile aprire il portale di servizi BizTalk di Azure hello. Portale dei servizi BizTalk di Hello è hello entrata tooEDI configurazione, incluse l'aggiunta di partner e la creazione di X12, AS2 e i contratti EDIFACT.
<br/><br/>
Questo è hello identico <strong>creare accordi tra partner</strong> su hello <strong>avvio rapido</strong> scheda.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurazione dei componenti per la messaggistica EDI nel portale dei servizi BizTalk</a> vengono fornite ulteriori informazioni su hello portale dei servizi BizTalk.</td>
</tr>

<tr>
<td><strong>Informazioni di connessione</strong> di hello Namespace di controllo di accesso</td>
<td>Quando si seleziona informazioni di connessione, quindi hello Namespace di controllo di accesso, autorità di certificazione predefinita e vengono visualizzati chiave predefinita. È possibile copiare questi valori.
<br/><br/>
È inoltre possibile aprire hello portale controllo di accesso. <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Creare un controllo di accesso Namespace</a> vengono fornite ulteriori informazioni sul portale di Access Control hello.</td>
</tr>

<tr>
<td><strong>Le chiavi di sincronizzazione</strong> in hello Account di archiviazione</td>
<td>Quando si crea un account di archiviazione, vengono create automaticamente una chiave primaria e una chiave secondaria. Queste chiavi di crittografia di controllo accesso tooyour Account di archiviazione. Il BizTalk Service utilizza automaticamente hello chiave primaria. <strong>Sincronizzare le chiavi</strong> abilitare gli utenti tooswitch tra hello chiave primaria e chiave secondaria hello senza interrompere hello BizTalk Service.
<br/><br/>
Ad esempio, si desidera hello BizTalk Service toouse una nuova chiave primaria per hello Account di archiviazione. toodo questo:
<br/><br/>
<ol>
<li>Selezionare il servizio BizTalk e quindi <strong>Chiavi di sincronizzazione</strong>. Selezionare hello chiave secondaria. Quando si esegue questa operazione, hello BizTalk Service avvia utilizzando hello chiave secondaria.</li>
<li>Nel portale di Azure classico hello, selezionare l'account di archiviazione e rigenerare la chiave primaria hello. Tenere presente, il BizTalk Service utilizza hello chiave secondaria.</li>
<li>Selezionare il servizio BizTalk e quindi <strong>Chiavi di sincronizzazione</strong>. A questo punto, selezionare hello chiave primaria. Questo è hello nuova chiave primaria è stata rigenerata.</li>
<li>Nel portale di Azure classico hello, selezionare l'account di archiviazione e rigenerare la chiave secondaria hello.</li>
</ol>
<br/>
Questo processo è denominato "chiavi di rollover". scopo di Hello è tooenable utenti tooswitch tra hello chiave primaria e chiave secondaria hello senza interrompere hello BizTalk Service.</td>
</tr>

<tr>
<td><strong>Eliminare</strong> l'applicazione</td>
<td>Quando si seleziona, Elimina, il BizTalk Service e vengono rimossi tutti gli elementi distribuiti tooit.</td>
</tr>
</table>


## <a name="dashboard"></a>Dashboard
A seconda di hello BizTalk Services Edition, tutte le opzioni elencate non siano disponibili. 

Quando si seleziona il nome di BizTalk Service, viene visualizzata nella scheda Dashboard hello. in cui è possibile effettuare le operazioni seguenti:

##### <a name="usage-overview-shows-hello-number-of-used-hybrid-connections"></a>Panoramica sull'utilizzo: Mostra il numero di hello di utilizzate connessioni ibride
Visualizza anche l'utilizzo di dati hello in GB. 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a>Grafico delle metriche: mostra un elenco fisso di metriche delle prestazioni
Queste metriche forniscono valori in tempo reale relativamente integrità hello di hello BizTalk Service. È anche possibile scegliere hello **relativo** o **assoluto** hello e valori di intervallo di tempo **intervallo** di metriche di hello che vengono visualizzate nel grafico hello. 

Per una descrizione di queste misurazioni delle prestazioni, andare troppo[le metriche disponibili](#Metrics) in questo argomento.

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a>Riepilogo rapido: elenca le proprietà del servizio BizTalk
<table border="1">

<tr>
<td><strong>Aggiornare le credenziali di Database di rilevamento</strong></td>
<td>Le modifiche hello nome utente e password utilizzati toolog in hello Database di rilevamento.</td>
</tr>
<tr>
<td><strong>Aggiornare il certificato SSL</strong></td>
<td>Può aggiornare hello BizTalk Service toouse un certificato SSL diverso. Un certificato SSL autofirmato viene creato automaticamente quando si <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">creare hello BizTalk Service</a>.</td>
</tr>
<tr>
<td><strong>Scaricare il certificato</strong></td>
<td>È possibile scaricare il certificato SSL hello utilizzato dal computer locale tooa BizTalk Service.</td>
</tr>
<tr>
<td><strong>Status</strong></td>
<td>Visualizza lo stato corrente di hello del BizTalk Service. Vedere <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">Servizi BizTalk: Tabella degli stati del servizio</a>. </td>
</tr>
<tr>
<td><strong>URL del servizio</strong></td>
<td>Hello URL per il BizTalk Service. Questo è hello stesso come hello <strong>URL di dominio</strong> immesso quando si crea il BizTalk Service.</td>
</tr>
<tr>
<td><strong>Indirizzo IP virtuale pubblico (VIP)</strong></td>
<td>indirizzo IP Hello assegnato tooyour BizTalk Service. Viene utilizzato per tutti gli endpoint di input e hello indirizzo di origine per il traffico in uscita. Questo indirizzo IP appartiene tooyour BizTalk Service fino a quando viene creato. Se si elimina hello BizTalk Service, l'indirizzo IP hello viene assegnato tooanother BizTalk Service.</td>
</tr>
<tr>
<td><strong>Spazio dei nomi ACS</strong></td>
<td>Esegue l'autenticazione con hello BizTalk Service.</td>
</tr>
<tr>
<td><strong>Edizione</strong></td>
<td>Elenca hello che Edition immesso quando viene creato hello BizTalk Service.</td>
</tr>
<tr>
<td><strong>Posizione</strong></td>
<td>Consente di visualizzare hello area geografica che ospita il BizTalk Service.</td>
</tr>
<tr>
<td><strong>Creato</strong></td>
<td>Hello di data e ora hello Visualizza BizTalk Service è stato creato.</td>
</tr>
<tr>
<td><strong>Database di rilevamento</strong></td>
<td>nome del Database SQL di Azure Hello che archivia hello utilizzate per il BizTalk Service tabelle di rilevamento. 
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">SPIEGAZIONE requisiti</a> fornisce informazioni dettagliate su Database di rilevamento hello.</td>
</tr>
<tr>
<td><strong>Memoria di monitoraggio/archiviazione</strong></td>
<td>nome account di archiviazione di Azure Hello che archivia il monitoraggio dell'output del BizTalk Service hello.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">SPIEGAZIONE requisiti</a> fornisce informazioni dettagliate su hello account di archiviazione.</td>
</tr>
<tr>
<td><strong>Nome sottoscrizione</strong></td>
<td>Elenca sottoscrizione hello che ospita il BizTalk Service. sottoscrizione Hello regola accesso toohello portale di Azure classico.</td>
</tr>
<tr>
<td><strong>ID sottoscrizione</strong></td>
<td>Quando si crea una sottoscrizione viene generato automaticamente un ID sottoscrizione. Quando si utilizza l'API REST, potrebbe essere necessario hello tooenter ID sottoscrizione.</td>
</tr>
</table>

[Servizi BizTalk: Portale classico di Azure tramite il Provisioning](http://go.microsoft.com/fwlink/p/?LinkID=302280) elenchi hello passaggi toocreate un BizTalk Service.

##### <a name="manage-connection-information-sync-keys-and-delete-in-hello-task-bar"></a>Informazioni di connessione, le chiavi di sincronizzazione, gestione ed eliminare nella barra delle applicazioni hello:
<table border="1">

<tr>
<td><strong>Gestire</strong> la distribuzione delle applicazioni</td>
<td>Apre hello portale servizi BizTalk di Azure. Portale dei servizi BizTalk di Hello è hello entrata tooEDI configurazione, incluse l'aggiunta di partner e la creazione di X12, AS2 e i contratti EDIFACT.
<br/><br/>
Questo è hello identico <strong>creare accordi tra partner</strong> su hello <strong>avvio rapido</strong> scheda.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurazione dei componenti per la messaggistica EDI nel portale dei servizi BizTalk</a> vengono fornite ulteriori informazioni su hello portale dei servizi BizTalk.</td>
</tr>
<tr>
<td><strong>Informazioni di connessione</strong> di hello Namespace di controllo di accesso</td>
<td>Consente di visualizzare hello Namespace di controllo di accesso, l'autorità di certificazione predefinita e valori di chiave predefinita. che può essere copiato.
<br/><br/>
È inoltre possibile aprire hello portale controllo di accesso. Questo portale di controllo di accesso è hello come utilizzando l'opzione di Active Directory hello nel riquadro di spostamento a sinistra di hello.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">La gestione di ACS Namespace</a> vengono fornite ulteriori informazioni sul portale di Access Control hello.</td>
</tr>
<tr>
<td><strong>Le chiavi di sincronizzazione</strong> in hello Account di archiviazione</td>
<td>Quando si crea un account di archiviazione, vengono create automaticamente una chiave primaria e una chiave secondaria. Queste chiavi di crittografia di controllo accesso tooyour Account di archiviazione. Il BizTalk Service utilizza automaticamente hello chiave primaria. <strong>Sincronizzare le chiavi</strong> abilitare gli utenti tooswitch tra hello chiave primaria e chiave secondaria hello senza interrompere hello BizTalk Service.
<br/><br/>
Ad esempio, si desidera hello BizTalk Service toouse una nuova chiave primaria per hello Account di archiviazione. toodo questo:
<br/><br/>
<ol>
<li>Selezionare il servizio BizTalk e quindi <strong>Chiavi di sincronizzazione</strong>. Selezionare hello chiave secondaria. Quando si esegue questa operazione, hello BizTalk Service avvia utilizzando hello chiave secondaria.</li>
<li>Nel portale di Azure classico hello, selezionare l'account di archiviazione e rigenerare la chiave primaria hello. Tenere presente, il BizTalk Service utilizza hello chiave secondaria.</li>
<li>Selezionare il servizio BizTalk e quindi <strong>Chiavi di sincronizzazione</strong>. A questo punto, selezionare hello chiave primaria. Questo è hello nuova chiave primaria è stata rigenerata.</li>
<li>Nel portale di Azure classico hello, selezionare l'account di archiviazione e rigenerare la chiave secondaria hello.</li>
</ol>
<br/>
Questo processo è denominato "chiavi di rollover". scopo di Hello è tooenable utenti tooswitch tra hello chiave primaria e chiave secondaria hello senza interrompere hello BizTalk Service.</td>
</tr>

<tr>
<td><strong>Eliminare</strong> l'applicazione</td>
<td>Il BizTalk Service e tutti gli elementi distribuiti tooit vengono rimossi.</td>
</tr>
</table>


## <a name="monitor"></a>Monitorare
Non si applica toohello edizione gratuita.

Quando si seleziona il nome di BizTalk Service, nella scheda Monitoraggio hello è disponibile e viene visualizzato il seguente hello:

##### <a name="metric-graph-displays-hello-selected-performance-metrics"></a>Metrica grafico: Hello Visualizza selezionato le metriche delle prestazioni
Queste metriche forniscono valori in tempo reale relativamente integrità hello di hello BizTalk Service. È l'utente a scegliere quali metriche visualizzare. È possibile visualizzare fino a un massimo di sei metriche delle prestazioni simultaneamente. 

È anche possibile scegliere hello **relativo** o **assoluto** hello e valori di intervallo di tempo **intervallo** di metriche di hello che vengono visualizzate. 

##### <a name="tooremove-or-display-metrics-in-hello-graph"></a>tooremove o visualizzare le metriche nel grafico hello:
1. Seleziona hello **monitoraggio** scheda.
2. Selezionare **Aggiungi metriche** nella barra delle applicazioni hello:  
   ![Fare clic su Aggiungi metriche][AddMetrics]
3. Controllare le metriche delle prestazioni di hello desiderato toodisplay.
4. Selezionare hello segno di spunta tooreturn toohello **monitoraggio** scheda.
5. Selezionare hello cerchio Avanti toohello metrica toodisplay valore del tale metrica grafico hello.  
   
    Ad esempio, hello **l'utilizzo della CPU** metrica è inattivo; l'output non viene visualizzata nel grafico hello:  
   ![Metrica Utilizzo CPU disabilitata][GrayedMetric]  
   
    Seleziona hello in grigio hello tooenable cerchio **l'utilizzo della CPU** toodisplay metrica l'output nel grafico hello:  
   ![Metrica Utilizzo CPU abilitata][EnabledMetric]
6. Selezionare una metrica dal grafico visualizzato hello ed elenco hello tooremove **Elimina metrica** nella barra delle applicazioni hello. tooadd hello metrica toohello indietro elenco, selezionare **Aggiungi metriche** hello sulla barra delle applicazioni, controllare la metrica hello e selezionare hello segno di spunta tooreturn toohello **monitoraggio** scheda. Cerchio tooenable hello metrica disabilitata hello Seleziona.

## <a name="Metrics"></a>Metriche disponibili
Hello contatori/metriche delle prestazioni seguenti sono disponibile:

<table border="1">

<tr>
<td><strong>Latenza RountdTrip</strong></td>
<td>Consente di visualizzare hello tempo medio in millisecondi (ms) tooprocess che viene ricevuto un messaggio dal messaggio hello in fase di hello fino a quando il messaggio hello viene completamente elaborato da hello BizTalk Service tra tutti i Bridge. Vengono conteggiati solo i messaggi correttamente elaborati.<br/><br/>
Quando si verifica hello dopo gli eventi, viene creato un timestamp:
<ul>
<li>Gateway hello viene inserito un messaggio</li>
<li>Il messaggio è indirizzato toohello destinazione</li>
<li>Si riceve una risposta dalla destinazione</li>
<li>Destinazione acknowledgement risposta inviata toohello gateway</li>
</ul>
<br/>
Questa metrica Mostra il risultato di hello di hello calcolo seguente:
<br/><br/>
[Destinazione acknowledgement risposta inviata toohello gateway] - [viene inserito un messaggio gateway hello]</td>
</tr>
<tr>
<td><strong>Errore nell'origine</strong></td>
<td>Visualizza hello il numero totale di messaggi non riusciti da hello BizTalk Service durante l'estrazione dei messaggi dagli endpoint di origine hello.</td>
</tr>
<tr>
<td><strong>Uso di CPU</strong></td>
<td>Elenca hello % tempo processore medio di tutte le istanze di ruolo.</td>
</tr>
<tr>
<td><strong>Latenza di elaborazione</strong></td>
<td>Consente di visualizzare hello tempo medio In millisecondi (ms) tooprocess un messaggio hello BizTalk Service tra tutti i bridge, escluso il tempo di hello impiegato nelle destinazioni. Vengono conteggiati solo i messaggi correttamente elaborati.<br/><br/>
Quando ognuno dei seguenti eventi hello si verificano, viene creato un timestamp:

<ul>
<li>Gateway hello viene inserito un messaggio</li>
<li>Il messaggio è indirizzato toohello destinazione</li>
<li>Si riceve una risposta dalla destinazione</li>
<li>Destinazione acknowledgement risposta inviata toohello gateway</li>
</ul>
<br/>Questa metrica Mostra il risultato di hello di hello calcolo seguente:<br/><br/>
[Destinazione acknowledgement risposta inviata toohello gateway] - [viene inserito un messaggio gateway hello] - [destinazione risposte] + [messaggio è indirizzato toohello destinazione]</td>
</tr>
<tr>
<td><strong>Errori nel processo</strong></td>
<td>Visualizza hello il numero totale di messaggi non riusciti durante l'elaborazione da hello BizTalk Service tra tutti i bridge hello all'interno di un intervallo di tempo.</td>
</tr>
<tr>
<td><strong>Messaggi inviati</strong></td>
<td>Visualizza hello il numero totale di messaggi inviati dall'hello BizTalk Service tra tutti i Bridge all'interno di un intervallo di tempo. Questa metrica viene incrementata quando un messaggio inviato da una pipeline raggiunga la destinazione di route hello. Questa metrica non indica la corretta elaborazione di un messaggio.<br/><br/>
In uno scenario Request / Reply, metrica hello viene incrementato quando la destinazione di route hello invia una pipeline di ricezione acknowledgement toohello indietro.</td>
</tr>
<tr>
<td><strong>Messaggi ricevuti</strong></td>
<td>Visualizza hello il numero totale di messaggi ricevuti dalle hello BizTalk Service tra tutti i Bridge all'interno di un intervallo di tempo. Questa metrica viene incrementata quando viene ricevuto un nuovo messaggio dalla pipeline hello.</td>
</tr>
<tr>
<td><strong>Messaggi in elaborazione</strong></td>
<td>Consente di visualizzare hello numero totale di messaggi attualmente elaborati in hello BizTalk Service all'interno di un intervallo di tempo.</td>
</tr>
<tr>
<td><strong>Messaggi elaborati</strong></td>
<td>Consente di visualizzare hello numero totale dei messaggi correttamente elaborati da hello BizTalk Service tra tutti i Bridge all'interno di un intervallo di tempo. Questa metrica viene incrementata quando un messaggio viene ricevuto correttamente da pipeline hello e di destinazione toohello indirizzato correttamente.</td>
</tr>
</table>


## <a name="scale"></a>Scalabilità
Nella scheda Scala hello, è possibile aggiungere o sottrarre hello numero di unità utilizzata per il BizTalk Service. Per impostazione predefinita è configurata una sola unità. Unità aggiuntive possono essere aggiunti tooscale il BizTalk Service. Quando si aumenta la scala hello, si stanno aumentando la velocità effettiva. quantità di Hello delle risorse aumenta anche, come bridge distribuiti, contratti, le connessioni LOB e potenza di elaborazione. Ad esempio, si aumenta scala hello da 1 unità too2 unità. In questo caso, è possibile distribuire hello doppie numero di Bridge, double contratti hello, double connessioni LOB hello e potenza di elaborazione hello double.

Alcune edizioni di BizTalk non offrono un'opzione di scalabilità: in questo caso è consentita una sola unità. toodetermine il numero di unità può essere ridimensionato l'edizione, vedere troppo[servizi BizTalk: grafico edizioni](biztalk-editions-feature-chart.md).

Aumentare il numero di hello unità può influire sui prezzi. Se si aumenta l'unità di hello, selezionando **salvare** viene visualizzato un messaggio che indica se la fatturazione è stata interessata. Scegliere quindi toocontinue. Quando si aumenta il numero di hello di unità, lo stato di BizTalk Service hello cambia da tooUpdating attivo. In hello lo stato di aggiornamento, il BizTalk Service continua toorun.

[Servizi BizTalk: Grafico edizioni](biztalk-editions-feature-chart.md) viene definita una "Unità".

## <a name="configure"></a>Configurare
Non è applicabile tooHybrid connessioni.

Imposta hello stato Backup tooNone o automatico. Quando impostato tooNone, non viene creato automaticamente alcun backup. Quando impostato tooAutomatic, configurare un percorso di backup hello, frequenza di hello di hello backup e il tempo tookeep hello i file di backup. 

[Servizi BizTalk: Backup e ripristino](biztalk-backup-restore.md) fornisce dettagli hello. 

## <a name="HybridConnections"></a>Connessioni ibride
Le connessioni ibride connettono un'applicazione Azure, ad esempio le applicazioni Web o App per dispositivi mobili in Azure App Service, risorsa locale tooan che utilizza una porta TCP statica, ad esempio SQL Server, MySQL, API Web HTTP e più servizi Web personalizzati. Le connessioni ibride vengono gestite nei servizi BizTalk nel portale di Azure classico hello.

toocreate connessioni ibride in Azure App Service, vedere [accesso risorse locali mediante connessioni ibride in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).

toocreate o gestire le connessioni ibride in servizi BizTalk di Azure, vedere [connessioni ibride](integration-hybrid-connection-overview.md).

## <a name="next"></a>Avanti
Ora che si ha familiarità con diverse schede hello, ulteriori informazioni sulle funzionalità di servizi BizTalk di Azure hello:

* [Servizi BizTalk: limitazione](biztalk-throttling-thresholds.md)  
* [Servizi BizTalk: nome e chiave dell'autorità emittente](biztalk-issuer-name-issuer-key.md)  
* [Servizi BizTalk: backup e ripristino](biztalk-backup-restore.md)

## <a name="see-also"></a>Vedere anche
* [Connessioni ibride](integration-hybrid-connection-overview.md)  
* [Servizi BizTalk: Grafico edizioni Developer, Basic, Standard e Premium](biztalk-editions-feature-chart.md)  
* [Servizi BizTalk: effettuare il provisioning di un servizio BizTalk mediante il portale di Azure classico](biztalk-provision-services.md)  
* [Servizi BizTalk: Tabella degli stati del servizio](biztalk-service-state-chart.md)  
* [Come è possibile utilizzare hello Azure BizTalk Services SDK](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

