---
title: aaaMigrating soluzioni EDI di BizTalk Server tooBizTalk Guida tecnica di servizi | Documenti Microsoft
description: Eseguire la migrazione EDI tooMABS; Servizi BizTalk di Microsoft Azure
services: biztalk-services
documentationcenter: na
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 61c179fa-3f37-495b-8016-dee7474fd3a6
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 34cca3c939a6a7845a860ead6858287000d03ee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-biztalk-server-edi-solutions-toobiztalk-services-technical-guide"></a>La migrazione di servizi tooBizTalk soluzioni EDI di BizTalk Server: Guida tecnica

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Autori: Tim Wieman e Nitin Mehrotra

Revisore: Karthik Bharthy

Scritto con: Servizi BizTalk di Microsoft Azure, versione di febbraio 2014.

## <a name="introduction"></a>Introduzione
Electronic Data Interchange (EDI) è uno dei hello più diffusi con cui le aziende scambio elettronico dei dati, definito anche come transazioni Business-to-Business o B2B. BizTalk Server è stato supporto EDI per oltre un decennio, poiché hello versione iniziale. Con i servizi BizTalk, Microsoft continua a supportare hello per le soluzioni EDI sulla piattaforma Microsoft Azure hello. Le transazioni B2B sono per lo più esterne tooan organizzazione e pertanto è più facile tooimplement se è stato implementato in una piattaforma cloud. Microsoft Azure fornisce questa funzionalità tramite i servizi BizTalk.

Mentre alcuni clienti considerano servizi BizTalk come piattaforma "vergine" per nuove soluzioni EDI, molti clienti hanno attuali soluzioni EDI di BizTalk Server che potrebbero desiderare toomigrate tooAzure. Poiché BizTalk Services EDI è strutturata hello in base alle entità stessa chiave come EDI di BizTalk Server architettura (partner commerciali, entità, contratti), è possibile toomigrate EDI di BizTalk Server elementi tooBizTalk dei servizi.

Questo documento vengono illustrate alcune differenze hello coinvolti tooBizTalk di elementi EDI di BizTalk Server eseguire la migrazione di servizi. In questo documento si presuppone si abbia una conoscenza pratica dell'elaborazione EDI di BizTalk Server e dei contratti per partner commerciali. Per ulteriori informazioni su EDI di BizTalk Server, vedere [Gestione dei trading partner mediante BizTalk Server](https://msdn.microsoft.com/library/bb259970.aspx).

## <a name="which-version-of-biztalk-server-edi-artifacts-can-be-migrated-toobiztalk-services"></a>La versione degli elementi EDI di BizTalk Server può essere eseguita la migrazione di servizi tooBizTalk?
modulo di Hello EDI di BizTalk Server è stata notevolmente migliorata per BizTalk Server 2010, quando era nuova tooinclude partner, profili e contratti. Utilizza i servizi BizTalk hello hello di tooorganize modello stesso e i partner commerciali e hello divisioni aziendali all'interno di tali partner. Di conseguenza, gli elementi da BizTalk Server 2010 e versioni successive versioni tooBizTalk migrazione EDI servizi, è un processo molto più semplice. gli elementi EDI di toomigrate associati a versioni precedenti tooBizTalk Server 2010, è necessario eseguire prima l'aggiornamento tooBizTalk Server 2010 e quindi eseguire la migrazione di elementi EDI tooBizTalk servizi.

## <a name="scenariosmessage-flow"></a>Scenari e flusso messaggi
Come con BizTalk Server, l’elaborazione EDI nei servizi BizTalk si basa su una soluzione di gestione dei partner commerciali (TPM, Trading Partner Management). Hello soluzione TPM è hello componenti chiave seguenti:

* I partner commerciali, che rappresentano l'organizzazione in una transazione B2B.
* I profili, che rappresentano divisioni all'interno di un partner commerciale.
* Commerciali accordi tra partner (o contratti), che rappresenta il contratto commerciale hello tra due partner o profili.

Hello seguente figura illustra analogie hello, e le differenze tra una soluzione EDI di BizTalk Server e di una soluzione EDI di BizTalk Services:

![][EDImessageflow]

Hello differenze e le analogie rilevanti tra un flusso di soluzione EDI in BizTalk Server e i servizi BizTalk:

* Analogo a BizTalk Server utilizza un tooreceive pipeline EDIReceive un messaggio EDI e un toosend pipeline EDISend un messaggio EDI, servizi BizTalk utilizza un tooreceive bridge di ricezione EDI e di trasmissione EDI bridge toosend messaggi EDI. In BizTalk Server, hello pipeline sono associate a un contratto mediante trasmissione o porte di ricezione. Nei servizi BizTalk, contratto hello stesso indica trasmissione hello o bridge di ricezione.
* In BizTalk Server, dopo i processi di pipeline EDIReceive hello hello messaggio EDI, il messaggio hello è tooa dump database di SQL Server. pipeline EdiSend Hello quindi preleva il messaggio hello dal database di SQL Server hello, elabora e lo invia toohello partner commerciale.
  
    Nei servizi BizTalk, dopo hello EDI ricevuto messaggio EDI hello processi bridge instrada processo esterno tooan di messaggio hello. processo esterno Hello può essere eseguito in Microsoft Azure o in locale. processo esterno Hello deve indirizzare toohello messaggio hello; bridge di trasmissione EDI bridge di trasmissione Hello non esegue il pull intrinsecamente messaggio hello. Dopo l'elaborazione del messaggio hello, hello bridge di trasmissione EDI indirizza partner commerciale toohello di messaggio hello.

Servizi BizTalk fornisce un tooquickly esperienza di configurazione da usare creare e distribuire un contratto B2B tra partner commerciali senza configurare qualsiasi calcolo di Microsoft Azure istanze (ruoli Web o di lavoro), tutti i database SQL di Microsoft Azure o qualsiasi Account di archiviazione di Microsoft Azure. Scenari più complessi richiederanno l'associazione di flussi di lavoro o altri elaborazione del servizio "intorno hello bordi" di un accordo tra Partner commerciali, ovvero prima o dopo l'elaborazione di bridge EDI del contratto. In dettaglio, hello seguenti sequenze di eventi si verificano durante un messaggio EDI elaborazione nei servizi BizTalk.

1. Un messaggio EDI viene ricevuto dal partner commerciale Fabrikam.  Per la ricezione di messaggi EDI dai partner commerciali, i servizi BizTalk supportano i protocolli di trasporto, quali FTP, SFTP, AS2 e HTTP/S.
2. Hello elaborazione sul lato di ricezione del contratto partner commerciali Disassembla formato tooXML del messaggio EDI hello.  È possibile indirizzare endpoint Bus tooService hello disassemblato EDI messaggio (in formato XML), ad esempio un endpoint di inoltro del Bus di servizio, argomento di Service Bus, coda del Bus di servizio o un bridge di servizi BizTalk.
3. Hello messaggi XML disassemblati possono quindi essere ricevuti dall'endpoint hello per un'ulteriore elaborazione personalizzata.  Questi endpoint possono essere elaborati da un componente locale o un calcolo di Microsoft Azure toofurther processo hello messaggio di istanza in un servizio Windows Workflow (WF) o Windows Communication Foundation (WCF), ad esempio.
4. Hello "elaborazione sul lato di trasmissione" dell'accordo tra partner commerciali hello quindi Assembla messaggio XML in formato EDI e lo invia tootrading partner Contoso.  Per l'invio di messaggi EDI tootrading partner, servizi di BizTalk supporta hello stessi protocolli di quelli utilizzati per la ricezione di messaggi EDI.

Questo documento vengono inoltre fornite linee guida concettuali su servizi di migrazione di alcune delle tooBizTalk di elementi EDI di BizTalk Server diversi hello.

## <a name="sendreceive-ports-tootrading-partners"></a>Porte di trasmissione/ricezione tooTrading partner
In BizTalk Server è configurare indirizzi di ricezione e messaggi EDI/XML tooreceive di porte di ricezione da partner commerciali e si imposta il partner tootrading i messaggi di porte di trasmissione toosend EDI/XML. Vengono quindi associate tooa queste porte accordo tra partner commerciali mediante hello console di amministrazione BizTalk Server. Nei servizi BizTalk, in cui si ricevono messaggi dal partner commerciali e si trasmettono i partner di tootrading i messaggi vengono configurati come parte dell'accordo tra partner commerciali stesso (come parte delle impostazioni di trasporto) hello in posizioni di hello hello portale dei servizi BizTalk .  Pertanto, non è importante il concetto di hello di "porte di trasmissione" e "indirizzi di ricezione", per sé, nei servizi BizTalk. Per altre informazioni, vedere [Creare contratti](https://msdn.microsoft.com/library/windowsazure/hh689908.aspx).

## <a name="pipelines-bridges"></a>Pipeline (bridge)
In EDI di BizTalk Server, le pipeline sono entità di elaborazione dei messaggi che possono anche includere logica personalizzata per la funzionalità di elaborazione specifiche, come richiesto da un'applicazione hello. Per i servizi BizTalk, hello equivalente sarebbe un bridge EDI. Tuttavia nei servizi BizTalk, per il momento, hello Bridge EDI sono "chiusi".  Ovvero, non è possibile aggiungere il propria bridge EDI tooan di attività personalizzate. Qualsiasi elaborazione personalizzata deve essere eseguita all'esterno di bridge EDI hello nell'applicazione, prima o dopo che il messaggio hello entra bridge hello configurato come parte di hello accordo tra Partner commerciali. I bridge EAI avere hello opzione toodo personalizzate per l'elaborazione. Se si desidera un'elaborazione personalizzata, è possibile utilizzare i bridge EAI prima o dopo il messaggio hello viene elaborato dal bridge EDI hello. Per ulteriori informazioni, vedere [come tooInclude di codice personalizzato nei bridge](https://msdn.microsoft.com/library/azure/dn232389.aspx).

È possibile inserire un flusso di pubblicazione/sottoscrizione con codice personalizzato e/o tramite Bus di servizio di messaggistica code e argomenti prima di hello accordo tra partner commerciali riceve il messaggio hello o dopo il contratto di hello elabora il messaggio hello e lo indirizza tooa endpoint di Service Bus.

Vedere **scenari e flusso messaggi** in questo argomento per modello di flusso di messaggi hello.

## <a name="agreements"></a>Contratti
Se si ha familiarità con gli accordi di Partner commerciali di BizTalk Server 2010 utilizzato per l'elaborazione EDI hello, quindi servizi BizTalk di accordi di trading partner molto familiare. La maggior parte delle impostazioni sono hello stesso contratto di hello e utilizzare hello stessa terminologia. In alcuni casi, hello le impostazioni dell'accordo è molto più semplice toohello confrontato stesse impostazioni in BizTalk Server. I servizi BizTalk di Microsoft Azure supportano il trasporto X12, EDIFACT e AS2.

Servizi BizTalk di Microsoft Azure fornisce inoltre un **migrazione dei dati TPM** strumento toomigrate trading partner e contratti dal modulo di Partner commerciali di BizTalk Server tooBizTalk portale dei servizi. lo strumento di migrazione dei dati TPM Hello è disponibile come parte di un pacchetto di strumenti, che può essere scaricato da hello [MABS SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057). pacchetto di Hello include anche un file Leggimi che vengono fornite istruzioni su come strumento hello toouse e informazioni sulla risoluzione dei problemi di base per hello dello strumento.

## <a name="schemas"></a>Schemi
I servizi BizTalk forniscono gli schemi EDI che possono essere utilizzati nelle soluzioni dei servizi BizTalk.  Inoltre, gli schemi EDI di BizTalk Server anche utilizzabile con i servizi BizTalk perché il nodo radice hello dello schema EDI hello è lo stesso in BizTalk Server, nonché servizi BizTalk. In questo modo, si verrà toodirectly in grado di eseguire gli schemi EDI di BizTalk Server e utilizzarli nelle soluzioni EDI hello sviluppate tramite servizi BizTalk. È inoltre possibile scaricare gli schemi di hello da hello [MABS SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057).

## <a name="maps-transforms"></a>Mappe (trasformazioni)
Le mappe di BizTalk Server sono chiamate trasformazioni nei servizi BizTalk. La migrazione di mappe da BizTalk Server tooBizTalk di che Services potrebbe essere uno hello tooachieve attività più complesse (a seconda della complessità della mappa). strumento di mapping Hello utilizzato per i servizi BizTalk è diverso da hello BizTalk mapper. Anche se mapper hello è principalmente hello stesso, formato hello della mappa sottostante è diverso. Hello functoid (chiamato **operazioni di mapping** nei servizi BizTalk) disponibili toohello utenti sono diversi.  In effetti, non è possibile utilizzare direttamente una mappa BizTalk nei servizi BizTalk. Inoltre, non tutti i functoid hello disponibili in BizTalk Server sono disponibili come operazioni mappa nei servizi BizTalk.

### <a name="new-transform-operations"></a>Nuove operazioni di trasformazione
Mentre l'elenco di hello di operazioni di mapping di trasformazione disponibili potrebbe apparire piuttosto diverso da hello mapper di BizTalk Server, BizTalk Services trasforma hanno hello stesse attività di nuove modalità di esecuzione. Ad esempio, le trasformazioni dei servizi BizTalk hanno le **operazioni di elenco** Questo non è disponibile in BizTalk mapper di hello.  Hello **operazioni elenco** consentono toocreate e operano su un "elenco", in un elenco è un set di elementi (noto anche come "righe") e ogni elemento può avere più membri (noto anche come "colonne").  È possibile ordinare l'elenco di hello, selezionare gli elementi in base a una condizione e così via.

Un altro esempio di nuove funzionalità di BizTalk Services trasforma sono hello **operazioni ciclo**.  È difficile toocreate annidati cicli in hello mapper di BizTalk Server.  Di conseguenza, operazioni di mapping di hello ciclo vengono aggiunti per hello BizTalk Services trasforma.

Un altro esempio è hello **If-Then-Else** operazione di mapping.  È stato possibile in BizTalk mapper di hello eseguendo un'operazione if-then-else, ma richiede più functoid tooaccomplish un'attività apparentemente semplice.

### <a name="migrating-biztalk-server-maps"></a>Migrazione delle mappe di BizTalk Server
Servizi BizTalk di Microsoft Azure fornisce che un toomigrate strumento BizTalk Server esegue il mapping tooBizTalk servizi trasformazioni. Hello **BTMMigrationTool** è disponibile come parte di hello **strumenti** pacchetto fornito con hello [download di BizTalk Services SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057). Per ulteriori informazioni sullo strumento hello, vedere [convertire un tooa mappa BizTalk trasformazione dei servizi BizTalk](https://msdn.microsoft.com/library/windowsazure/hh949812.aspx).

È possibile anche visualizzare un esempio di Sandro Pereira, MVP di BizTalk, nella modalità troppo[migrare le trasformazioni di servizi di BizTalk Server mappe tooBizTalk](http://social.technet.microsoft.com/wiki/contents/articles/23220.migrating-biztalk-server-maps-to-windows-azure-biztalk-services-wabs-maps.aspx).

## <a name="orchestrations"></a>Orchestrazioni
Se è necessario toomigrate tooMicrosoft l'elaborazione dell'orchestrazione di BizTalk Server Azure, le orchestrazioni hello sarebbe necessario toobe riscritte poiché in Microsoft Azure non supporta orchestrazioni di BizTalk Server in esecuzione.  È possibile riscrivere la funzionalità di orchestrazione hello in un servizio di Windows Workflow Foundation 4.0 (WF4).  Questo potrebbe essere una riscrittura completa poiché non è attualmente alcuna migrazione da tooWF4 orchestrazioni di BizTalk Server. Di seguito sono riportate alcune risorse per Windows Workflow:

* [*Come toointegrate Service di un flusso di lavoro WCF con code del Bus di servizio e gli argomenti* ](https://msdn.microsoft.com/library/azure/hh709041.aspx) cura di Paolo Salvatori. 
* [*Creazione di applicazioni con Windows Workflow Foundation e Azure* sessione](http://go.microsoft.com/fwlink/p/?LinkId=237314) conferenza Build 2011 hello.
* [*Centro per sviluppatori Windows Workflow Foundation*](http://go.microsoft.com/fwlink/p/?LinkId=237315) in MSDN.
* [*Documentazione di Windows Workflow Foundation 4 (WF4)*](https://msdn.microsoft.com/library/dd489441.aspx) in MSDN.

## <a name="other-considerations"></a>Altre considerazioni
Di seguito sono riportate alcune informazioni da tenere in considerazione quando si usano i servizi BizTalk.

### <a name="fallback-agreements"></a>Accordi di fallback
L'elaborazione EDI di BizTalk Server esiste il concetto di hello di "Accordi di Fallback".  I servizi BizTalk **non** hanno ancora un concetto di accordo di fallback.  Vedere gli argomenti della documentazione di BizTalk [hello ruolo degli accordi nell'elaborazione EDI](http://go.microsoft.com/fwlink/p/?LinkId=237317) e [configurazione globale o proprietà dell'accordo Fallback](https://msdn.microsoft.com/library/bb245981.aspx) per informazioni sull'utilizzo di accordi di Fallback in BizTalk Server.

### <a name="routing-toomultiple-destinations"></a>Destinazioni di routing toomultiple
Bridge di servizi BizTalk, nello stato corrente non supporta destinazioni di routing messaggi toomultiple utilizzando la pubblicazione-sottoscrizione modello. Ma è possibile indirizzare i messaggi da un servizi BizTalk bridge tooa argomento di Service Bus, che possono essere presenti più messaggi hello tooreceive di sottoscrizioni in più di un endpoint.

## <a name="conclusion"></a>Conclusioni
Servizi BizTalk di Microsoft Azure viene aggiornato a intervalli regolari tooadd altre caratteristiche e funzionalità. A ogni aggiornamento, saremo lieti di toofacilitate funzionalità toosupporting aumentato la creazione di soluzioni end-to-end mediante servizi BizTalk e altre tecnologie di Azure.

## <a name="see-also"></a>Vedere anche
[Sviluppo di applicazioni aziendali con Azure](https://msdn.microsoft.com/library/azure/hh674490.aspx)

[EDImessageflow]: ./media/biztalk-migrating-to-edi-guide/IC719455.png
