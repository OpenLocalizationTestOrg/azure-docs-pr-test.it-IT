---
title: "Dashboard, Monitoraggio, Scalabilità, Configura e Connessioni ibride in Servizi BizTalk | Documentazione Microsoft"
description: Informazioni su controlli e monitoraggio delle prestazioni dei servizi BizTalk
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
ms.openlocfilehash: 351809cd5f165a863dc02bfadf78fa59cbaabfd7
ms.sourcegitcommit: dcf5f175454a5a6a26965482965ae1f2bf6dca0a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/10/2017
---
# <a name="review-the-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a>Analizzare le schede Dashboard, Monitor, Scala, Configura e Connessione ibrida

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Dopo aver creato il servizio BizTalk e aver distribuito l'applicazione, è possibile modificare alcune impostazioni del servizio BizTalk e monitorare le prestazioni dell'applicazione. 

> [!INCLUDE [Use APIs to manage MABS](../../includes/biztalk-services-retirement-azure-classic-portal.md)]

Verrà aperta una nuova finestra con le schede seguenti: In questo argomento vengono descritte queste schede.

## <a name="quickstart-quickstartquickstart"></a>Guida introduttiva (![Guida introduttiva][Quickstart])
A seconda dell'edizione di Servizi BizTalk, non tutte le opzioni elencate potrebbero essere disponibili. 

<table border="1">
    <tr>
        <td><strong>Ottenere gli strumenti</strong></td>
        <td>Scaricare l'SDK di Servizi BizTalk per installare i modelli di progetto di Visual Studio sul computer di sviluppo locale. I modelli consentono di creare i progetti di Visual Studio <strong>BizTalk Services</strong> (bridge) e <strong>BizTalk Service Artifacts</strong> (Transform) distribuiti nel servizio BizTalk.
        <br/><br/>Gli articoli 
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Come iniziare a usare Azure BizTalk Services SDK</a> e <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installare Azure BizTalk Services SDK elencano tutte le procedure introduttive</a>.
        </td>
    </tr>
    <tr>
        <td><strong>Creare contratti con il partner</strong></td>
        <td>Consente di aprire il portale Servizi BizTalk di Azure ospitato su Azure dove aggiungere partner e creare contratti EDI X12, AS2 ed EDIFACT.
        <br/><br/>L'articolo 
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurazione di componenti per la messaggistica EDI nel portale dei servizi BizTalk</a> elenca le procedure introduttive.
        </td>
    </tr>

<tr>
        <td><strong>Altre informazioni sui Servizi BizTalk</strong></td>
        <td>Per altre informazioni sui Servizi BizTalk di Azure visitare l'<a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">area risorse</a>.</td>
</tr>
</table>


Sulla barra delle applicazioni in basso è possibile:

<table border="1">

<tr>
<td><strong>Gestire</strong> la distribuzione delle applicazioni</td>
<td>Viene aperto il portale di Servizi BizTalk di Azure. Il portale di Servizi BizTalk è l'ingresso alla configurazione EDI, incluse l'aggiunta di partner e la creazione di contratti X12, AS2 ed EDIFACT.
<br/><br/>
Questa opzione ha la stessa funzione dell'opzione <strong>Crea contratti partner</strong> nella scheda <strong>Avvio rapido</strong>.
<br/><br/>L'articolo 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurazione di componenti per la messaggistica EDI nel portale dei servizi BizTalk</a> contiene altre informazioni sul portale dei servizi BizTalk.</td>
</tr>

<tr>
<td><strong>Informazioni di connessione</strong> dello spazio dei nomi di controllo di accesso</td>
<td>Quando si seleziona Informazioni di connessione, vengono visualizzati i valori di Spazio dei nomi di Access Control, Autorità emittente predefinita e Chiave predefinita. È possibile copiare questi valori.
<br/><br/>
È anche possibile aprire il portale di Controllo di accesso. L'articolo <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Creare uno spazio dei nomi di Controllo di accesso</a> offre altre informazioni sul portale di Controllo di accesso.</td>
</tr>

<tr>
<td><strong>Chiavi di sincronizzazione</strong> nell'account di archiviazione</td>
<td>Quando si crea un account di archiviazione, vengono create automaticamente una chiave primaria e una chiave secondaria. Queste chiavi di crittografia controllano l'accesso all'account di archiviazione. Il servizio BizTalk usa automaticamente la chiave primaria. L'opzione <strong>Chiavi di sincronizzazione</strong> consente agli utenti di passare dalla chiave primaria alla secondaria e viceversa senza interrompere il servizio BizTalk.
<br/><br/>
Ad esempio, si potrebbe voler usare una nuova chiave primaria per l'account di archiviazione nel servizio BizTalk. A tale scopo, seguire questa procedura:
<br/><br/>
<ol>
<li>Selezionare il servizio BizTalk e quindi <strong>Chiavi di sincronizzazione</strong>. Selezionare la chiave secondaria. Così facendo, il servizio BizTalk comincia a usare la chiave secondaria.</li>
<li>Selezionare il proprio account di archiviazione e rigenerare la chiave primaria. Si tenga presente che il servizio BizTalk sta usando la chiave secondaria.</li>
<li>Selezionare il servizio BizTalk e quindi <strong>Chiavi di sincronizzazione</strong>. Selezionare adesso la chiave primaria, ossia la nuova chiave primaria rigenerata dall'utente.</li>
<li>Selezionare il proprio account di archiviazione e rigenerare la chiave secondaria.</li>
</ol>
<br/>
Questo processo è denominato "chiavi di rollover". Lo scopo è quello di consentire agli utenti di passare dalla chiave primaria alla secondaria e viceversa senza interrompere il servizio BizTalk.</td>
</tr>

<tr>
<td><strong>Eliminare</strong> l'applicazione</td>
<td>Quando si fa clic su Elimina, il servizio BizTalk e tutti gli elementi distribuiti verranno rimossi.</td>
</tr>
</table>


## <a name="dashboard"></a>Dashboard
A seconda dell'edizione di Servizi BizTalk, non tutte le opzioni elencate potrebbero essere disponibili. 

Quando si seleziona il nome del servizio BizTalk, viene visualizzata la scheda Dashboard, in cui è possibile effettuare le operazioni seguenti:

##### <a name="usage-overview-shows-the-number-of-used-hybrid-connections"></a>Panoramica sull'utilizzo: mostra il numero delle connessioni ibride usate
Visualizza anche l'uso dei dati espresso in GB. 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a>Grafico delle metriche: mostra un elenco fisso di metriche delle prestazioni
Include i valori in tempo reale riguardo l'integrità del servizio BizTalk. È anche possibile specificare il valore **Relativo** o **Assoluto** e l'**intervallo** di tempo delle metriche visualizzate nel grafico. 

Per una descrizione delle metriche delle prestazioni, vedere la sezione [Metriche disponibili](#Metrics) in questo argomento.

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a>Riepilogo rapido: elenca le proprietà del servizio BizTalk
<table border="1">

<tr>
<td><strong>Aggiornare le credenziali di Database di rilevamento</strong></td>
<td>Consente di modificare il nome utente e la password usati per accedere al database di rilevamento.</td>
</tr>
<tr>
<td><strong>Aggiornare il certificato SSL</strong></td>
<td>Consente di aggiornare il servizio BizTalk in modo da usare un certificato SSL diverso. Quando si <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">crea il servizio BizTalk</a>, viene creato automaticamente un certificato SSL autofirmato.</td>
</tr>
<tr>
<td><strong>Scaricare il certificato</strong></td>
<td>Consente di scaricare il certificato SSL usato dal servizio BizTalk su un computer locale.</td>
</tr>
<tr>
<td><strong>Status</strong></td>
<td>Visualizza lo stato corrente del servizio BizTalk. Vedere <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">Servizi BizTalk: Tabella degli stati del servizio</a>. </td>
</tr>
<tr>
<td><strong>URL del servizio</strong></td>
<td>L'URL del servizio BizTalk. È uguale al valore di <strong>URL di dominio</strong> immesso al momento della creazione del servizio BizTalk.</td>
</tr>
<tr>
<td><strong>Indirizzo IP virtuale pubblico (VIP)</strong></td>
<td>Questo indirizzo IP viene assegnato al servizio BizTalk, È usato per tutti gli endpoint di input ed è l'indirizzo di origine per il traffico in uscita. Questo indirizzo IP appartiene al proprio servizio BizTalk, se viene creato. Se si elimina il servizio BizTalk, l'indirizzo IP viene assegnato a un altro servizio BizTalk.</td>
</tr>
<tr>
<td><strong>Spazio dei nomi ACS</strong></td>
<td>Consente di eseguire l'autenticazione con il servizio BizTalk.</td>
</tr>
<tr>
<td><strong>Edizione</strong></td>
<td>Elenca l'edizione immessa al momento della creazione del servizio BizTalk.</td>
</tr>
<tr>
<td><strong>Posizione</strong></td>
<td>Visualizza l'area geografica in cui è ospitato il servizio BizTalk.</td>
</tr>
<tr>
<td><strong>Creato</strong></td>
<td>Visualizza la data e l'ora della creazione del servizio BizTalk.</td>
</tr>
<tr>
<td><strong>Database di rilevamento</strong></td>
<td>Database SQL di Azure in cui sono archiviate le tabelle di rilevamento usate dal servizio BizTalk. 
<br/><br/>In 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Descrizione dei requisiti</a> sono disponibili informazioni dettagliate sul database di rilevamento.</td>
</tr>
<tr>
<td><strong>Memoria di monitoraggio/archiviazione</strong></td>
<td>Nome dell'account di archiviazione di Azure in cui è archiviato l'output del monitoraggio del servizio BizTalk.
<br/><br/>In 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Descrizione dei requisiti</a> sono disponibili informazioni dettagliate sull'account di archiviazione.</td>
</tr>
<tr>
<td><strong>Nome sottoscrizione</strong></td>
<td>Indica il nome della sottoscrizione che ospita il servizio BizTalk. La sottoscrizione controlla l'accesso.</td>
</tr>
<tr>
<td><strong>ID sottoscrizione</strong></td>
<td>Quando si crea una sottoscrizione viene generato automaticamente un ID sottoscrizione. Quando si utilizzano le API REST può essere necessario immettere l'ID sottoscrizione.</td>
</tr>
</table>

In [Servizi BizTalk: Provisioning ](http://go.microsoft.com/fwlink/p/?LinkID=302280) sono elencati i passaggi necessari per creare un servizio BizTalk.

##### <a name="manage-connection-information-sync-keys-and-delete-in-the-task-bar"></a>Gestisci, Informazioni di connessione, Chiavi di sincronizzazione ed Elimina sulla barra delle applicazioni:
<table border="1">

<tr>
<td><strong>Gestire</strong> la distribuzione delle applicazioni</td>
<td>Viene aperto il portale di Servizi BizTalk di Azure. Il portale di Servizi BizTalk è l'ingresso alla configurazione EDI, incluse l'aggiunta di partner e la creazione di contratti X12, AS2 ed EDIFACT.
<br/><br/>
Questa opzione ha la stessa funzione dell'opzione <strong>Crea contratti partner</strong> nella scheda <strong>Avvio rapido</strong>.
<br/><br/>L'articolo 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurazione di componenti per la messaggistica EDI nel portale dei servizi BizTalk</a> contiene altre informazioni sul portale dei servizi BizTalk.</td>
</tr>
<tr>
<td><strong>Informazioni di connessione</strong> dello spazio dei nomi di controllo di accesso</td>
<td>Visualizza i valori di Spazio dei nomi di Access Control, Autorità emittente predefinita e Chiave predefinita, che possono essere copiati.
<br/><br/>
È anche possibile aprire il portale di Controllo di accesso. Questo portale di Controllo di accesso è lo stesso di quando si usa l'opzione Active Directory nel pannello di navigazione a sinistra.
<br/><br/>L'articolo 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Gestione dello spazio dei nomi ACS</a> offre altre informazioni sul portale di Controllo di accesso.</td>
</tr>
<tr>
<td><strong>Chiavi di sincronizzazione</strong> nell'account di archiviazione</td>
<td>Quando si crea un account di archiviazione, vengono create automaticamente una chiave primaria e una chiave secondaria. Queste chiavi di crittografia controllano l'accesso all'account di archiviazione. Il servizio BizTalk usa automaticamente la chiave primaria. L'opzione <strong>Chiavi di sincronizzazione</strong> consente agli utenti di passare dalla chiave primaria alla secondaria e viceversa senza interrompere il servizio BizTalk.
<br/><br/>
Ad esempio, si potrebbe voler usare una nuova chiave primaria per l'account di archiviazione nel servizio BizTalk. A tale scopo, seguire questa procedura:
<br/><br/>
<ol>
<li>Selezionare il servizio BizTalk e quindi <strong>Chiavi di sincronizzazione</strong>. Selezionare la chiave secondaria. Così facendo, il servizio BizTalk comincia a usare la chiave secondaria.</li>
<li>Selezionare il proprio account di archiviazione e rigenerare la chiave primaria. Si tenga presente che il servizio BizTalk sta usando la chiave secondaria.</li>
<li>Selezionare il servizio BizTalk e quindi <strong>Chiavi di sincronizzazione</strong>. Selezionare adesso la chiave primaria, ossia la nuova chiave primaria rigenerata dall'utente.</li>
<li>Selezionare il proprio account di archiviazione e rigenerare la chiave secondaria.</li>
</ol>
<br/>
Questo processo è denominato "chiavi di rollover". Lo scopo è quello di consentire agli utenti di passare dalla chiave primaria alla secondaria e viceversa senza interrompere il servizio BizTalk.</td>
</tr>

<tr>
<td><strong>Eliminare</strong> l'applicazione</td>
<td>Il servizio BizTalk e tutti gli elementi distribuiti verranno rimossi.</td>
</tr>
</table>


## <a name="monitor"></a>Monitoraggio
Non si applica all'edizione gratuita.

Quando si seleziona il nome del servizio BizTalk, la scheda Monitoraggio è disponibile e visualizza quanto indicato di seguito:

##### <a name="metric-graph-displays-the-selected-performance-metrics"></a>Grafico delle metriche: visualizza le metriche delle prestazioni selezionate
Include i valori in tempo reale riguardo l'integrità del servizio BizTalk. È l'utente a scegliere quali metriche visualizzare. È possibile visualizzare fino a un massimo di sei metriche delle prestazioni simultaneamente. 

È anche possibile specificare il valore **Relativo** o **Assoluto** e l'**intervallo** di tempo delle metriche visualizzate. 

##### <a name="to-remove-or-display-metrics-in-the-graph"></a>Per rimuovere o visualizzare la metrica nel grafico
1. Selezionare la scheda **Monitoraggio** .
2. Selezionare **Aggiungi metriche** sulla barra delle applicazioni:  
   ![Fare clic su Aggiungi metriche][AddMetrics]
3. Controllare la metrica delle prestazioni che si desidera visualizzare.
4. Fare clic sul segno di spunta per tornare alla scheda **Monitoraggio** .
5. Fare clic sul cerchio accanto alla metrica desiderata per visualizzarne il valore nel grafico.  
   
    Ad esempio, la metrica **Utilizzo CPU** è inattiva e il relativo output non è visualizzato nel grafico:  
   ![Metrica Utilizzo CPU disabilitata][GrayedMetric]  
   
    Selezionare il cerchio inattivo per abilitare la metrica **Utilizzo CPU** per visualizzarne l'output nel grafico:  
   ![Metrica Utilizzo CPU abilitata][EnabledMetric]
6. Per rimuovere una metrica dal grafico e dall'elenco, fare clic su **Elimina metrica** sulla barra delle applicazioni. Per aggiungere di nuovo la metrica all'elenco, fare clic su **Aggiungi metriche** sulla barra delle applicazioni, controllare la metrica e fare clic sul segno di spunta per tornare alla scheda **Monitoraggio**. Selezionare il cerchio in grigio per abilitare la metrica.

## <a name="Metrics"></a>Metriche disponibili
Sono disponibili i contatori/le metriche seguenti:

<table border="1">

<tr>
<td><strong>Latenza RountdTrip</strong></td>
<td>Visualizza il tempo medio, espresso in millisecondi (ms), impiegato per l'elaborazione completa di un messaggio da parte del servizio BizTalk dal momento della ricezione attraverso tutti i bridge. Vengono conteggiati solo i messaggi correttamente elaborati.<br/><br/>
Quando si verificano gli eventi seguenti viene creato un timestamp:
<ul>
<li>Il messaggio accede al gateway</li>
<li>Il messaggio viene indirizzato alla destinazione</li>
<li>Si riceve una risposta dalla destinazione</li>
<li>La risposta di conferma della destinazione viene inviata al gateway</li>
</ul>
<br/>
Questa metrica indica il risultato del calcolo seguente:
<br/><br/>
[La risposta di conferma della destinazione viene inviata al gateway] - [Il messaggio accede al gateway]</td>
</tr>
<tr>
<td><strong>Errore nell'origine</strong></td>
<td>Visualizza il numero totale di messaggi di cui il servizio BizTalk non eseguito correttamente il pull dagli endpoint di origine.</td>
</tr>
<tr>
<td><strong>Uso di CPU</strong></td>
<td>Consente di elencare il valore % tempo processore di tutte le istanze del ruolo.</td>
</tr>
<tr>
<td><strong>Latenza di elaborazione</strong></td>
<td>Visualizza il tempo medio, espresso in millisecondi (ms), impiegato per l'elaborazione di un messaggio da parte del servizio BizTalk attraverso tutti i bridge, esclusi il tempo impiegato nelle destinazioni. Vengono conteggiati solo i messaggi correttamente elaborati.<br/><br/>
Quando si verifica uno degli eventi seguenti viene creato un timestamp:

<ul>
<li>Il messaggio accede al gateway</li>
<li>Il messaggio viene indirizzato alla destinazione</li>
<li>Si riceve una risposta dalla destinazione</li>
<li>La risposta di conferma della destinazione viene inviata al gateway</li>
</ul>
<br/>Questa metrica indica il risultato del calcolo seguente:<br/><br/>
[La risposta di conferma della destinazione viene inviata al gateway] - [Il messaggio accede al gateway] - [Si riceve una risposta dalla destinazione] + [Il messaggio viene indirizzato alla destinazione]\</td>
</tr>
<tr>
<td><strong>Errori nel processo</strong></td>
<td>Visualizza il numero totale di messaggi che il servizio BizTalk non ha elaborato correttamente attraverso tutti i bridge entro un determinato intervallo di tempo.</td>
</tr>
<tr>
<td><strong>Messaggi inviati</strong></td>
<td>Visualizza il numero totale di messaggi inviati dal servizio BizTalk attraverso tutti i bridge entro un determinato intervallo di tempo. Questa metrica viene incrementata quando un messaggio inviato da una pipeline raggiunge la destinazione della route. Questa metrica non indica la corretta elaborazione di un messaggio.<br/><br/>
In uno scenario di tipo richiesta-risposta, la metrica viene incrementata quando la destinazione della route restituisce una conferma di ricezione alla pipeline.</td>
</tr>
<tr>
<td><strong>Messaggi ricevuti</strong></td>
<td>Visualizza il numero totale di messaggi ricevuti dal servizio BizTalk attraverso tutti i bridge entro un determinato intervallo di tempo. Questa metrica viene incrementata quando si riceve un nuovo messaggio inviato dalla pipeline.</td>
</tr>
<tr>
<td><strong>Messaggi in elaborazione</strong></td>
<td>Visualizza il numero totale di messaggi attualmente in corso di elaborazione da parte del servizio BizTalk entro un determinato intervallo di tempo.</td>
</tr>
<tr>
<td><strong>Messaggi elaborati</strong></td>
<td>Visualizza il numero totale di messaggi correttamente elaborati dal servizio BizTalk attraverso tutti i bridge entro un determinato intervallo di tempo. Questa metrica viene incrementata quando si riceve correttamente un messaggio inviato dalla pipeline, che viene quindi correttamente indirizzato alla destinazione.</td>
</tr>
</table>


## <a name="scale"></a>Scalabilità
Nella scheda Scale è possibile aggiungere o sottrarre il numero di unità utilizzate dal servizio BizTalk. Per impostazione predefinita è configurata una sola unità. È possibile aggiungere ulteriori unità per la scalabilità del servizio BizTalk. Quando si aumenta la scalabilità si aumenta anche la velocità effettiva. Aumenta inoltre la quantità di risorse, inclusi i bridge distribuiti, i contratti, le connessioni LOB e la potenza di elaborazione. Se ad esempio si aumenta la scalabilità da 1 unità a 2 unità, è possibile distribuire un numero doppio di bridge, di contratti e di connessioni LOB, oltre a una quantità doppia di potenza di elaborazione.

Alcune edizioni di BizTalk non offrono un'opzione di scalabilità: in questo caso è consentita una sola unità. Per determinare il numero di unità in base al quale è possibile ridimensionare l'edizione in uso, vedere l'articolo [Servizi BizTalk: Grafico edizioni](biztalk-editions-feature-chart.md).

L'aumento del numero di unità può incidere sui prezzi. Se si aumentano le unità, quando si seleziona **Salva** verrà visualizzato un messaggio che informa dell'impatto sulla fatturazione. Sta all'utente sceglie se continuare. Quando si aumenta il numero di unità, lo stato del servizio BizTalk passa da Active ad Updating. Nello stato Updating l'esecuzione del servizio BizTalk non verrà interrotta.

[Servizi BizTalk: Grafico edizioni](biztalk-editions-feature-chart.md) viene definita una "Unità".

## <a name="configure"></a>Configurare
Non si applica alle connessioni ibride.

Imposta Stato backup su Nessuno o Automatico. Se è impostato su Nessuno, non vengono creati backup automaticamente. Se è impostato su Automatico, configurare il percorso di backup, la frequenza e la durata di mantenimento dei file di backup. 

[Servizi BizTalk: backup e ripristino](biztalk-backup-restore.md) sono disponibili informazioni dettagliate. 

## <a name="HybridConnections"></a>Connessioni ibride
Le connessioni ibride consentono la connessione di un'applicazione Azure, come App Web o App per dispositivi mobili nel servizio app di Azure, a una risorsa locale che usa una porta TCP statica, ad esempio SQL Server, MySQL, API Web HTTP e la maggior parte dei servizi Web personalizzati. Le connessioni ibride sono gestite nei servizi BizTalk.

Per creare o gestire connessioni ibride in Siti Web di Azure, vedere l'articolo relativo alle [Connessioni ibride](integration-hybrid-connection-overview.md).

## <a name="next"></a>Avanti
Ora che è stata acquisita familiarità con le diverse schede è possibile ottenere altre informazioni sulle funzionalità dei Servizi BizTalk di Azure:

* [Servizi BizTalk: limitazione](biztalk-throttling-thresholds.md)  
* [Servizi BizTalk: nome e chiave dell'autorità emittente](biztalk-issuer-name-issuer-key.md)  
* [Servizi BizTalk: backup e ripristino](biztalk-backup-restore.md)

## <a name="see-also"></a>Vedere anche
* [Connessioni ibride](integration-hybrid-connection-overview.md)  
* [Servizi BizTalk: Grafico edizioni Developer, Basic, Standard e Premium](biztalk-editions-feature-chart.md)  
* [Servizi BizTalk: Provisioning](biztalk-provision-services.md)  
* [Servizi BizTalk: Tabella degli stati del servizio](biztalk-service-state-chart.md)  
* [Come iniziare a usare l'SDK di Servizi BizTalk di Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

