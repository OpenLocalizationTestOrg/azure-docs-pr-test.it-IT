---
title: aaaWhat's New in hello Azure Toolkit per Eclipse
description: "Informazioni sulle funzionalità più recenti hello hello Azure Toolkit per Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 16b066ea-aae7-4c30-9a12-fa0c3711b93e
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm;asirveda;martinsawicki
ms.openlocfilehash: d74eacfb75447a3d659a0c2dc2e247ae6e3ce1b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="whats-new-in-hello-azure-toolkit-for-eclipse"></a>Novità in Azure Toolkit per Eclipse hello
## <a name="azure-toolkit-for-eclipse-releases"></a>Versioni di Azure Toolkit for Eclipse
In questo articolo contiene informazioni su hello varie versioni e ultimi aggiornamenti toohello Azure Toolkit per Eclipse.

> [!NOTE]
> È inoltre disponibile un Toolkit di Azure per hello IntelliJ IDE. Per ulteriori informazioni, vedere [Azure Toolkit per IntelliJ].
> 
> 

### <a name="april-14-2017"></a>14 aprile 2017
Hello Azure Toolkit per Eclipse - versione aprile 2017 include hello seguenti miglioramenti:

* **Azure Sign In esperienza migliorata**: hello Azure Toolkit per Eclipse ora supporta due metodi di registrazione all'account Azure: *Interactive* e *automatizzata*. Per ulteriori informazioni, vedere [Azure Sign In istruzioni per hello Azure Toolkit per Eclipse].
* **Pubblicazione con i contenitori Docker**: è ora possibile pubblicare le applicazioni Web come contenitori Docker usando il Toolkit di Azure per Eclipse. Per ulteriori informazioni, vedere [come un'App Web come un contenitore Docker usando toopublish hello Azure Toolkit per Eclipse].
* **Gestione degli Account di archiviazione**: hello Azure Toolkit per Eclipse ora supporta la gestione di account di archiviazione da hello visualizzazione di Esplora risorse di Azure. Per ulteriori informazioni, vedere [utilizzando la gestione di account di archiviazione di Azure Explorer per Eclipse hello].
* **Virtual Machine Management**: hello Azure Toolkit per Eclipse ora supporta la gestione delle macchine virtuali da hello visualizzazione di Esplora risorse di Azure. Per ulteriori informazioni, vedere [utilizzando Gestione delle macchine virtuali di Azure Explorer per Eclipse hello].
* **Rimozione del supporto del debug remoto**. Debug remoto di applicazioni web Java in Azure App Service è stato rimosso da hello Azure Toolkit per Eclipse; Questo è necessario tooresolve alcuni problemi dei clienti che sono stati verificati quando si utilizza hello toolkit.

### <a name="august-26-2016"></a>26 agosto 2016
Hello Azure Toolkit per Eclipse - versione di agosto 2016 include hello seguenti miglioramenti:

* **Distribuzioni di JDK personalizzate**. Hello Azure Toolkit per Eclipse supporta ora specifica e la distribuzione di un contenitore di Azure WebApp tooyour di versione JDK arbitrario:
  * In inoltre toohello JDK fornite da Azure, è possibile scegliere tra un'ampia selezione di versioni Zulu OpenJDK reso disponibile in Azure da Azul Systems.
  * È possibile specificare la propria distribuzione di JDK anche se questo viene caricato come un account di archiviazione tooyour file ZIP.
* **Miglioramenti toohello visualizzazione Esplora risorse di Azure**:
  * Supporto per la gestione delle macchine virtuali utilizzando il nuovo modello di gestione risorse di Azure: è possibile elencare, creare ed eliminare le macchine virtuali basate su Gestione risorse senza uscire hello IDE.
  * Supporto per la gestione di Account di archiviazione blob usando Gestione risorse di Azure, che integra le funzionalità esistenti per la gestione di account di archiviazione "classiche" hello.
* **Microsoft JDBC Driver 6.0 per SQL Server**. Questo aggiornamento include il driver JDBC più recente di hello per Microsoft SQL Server (v 6.0), che è ora inclusa come una libreria che è possibile aggiungere facilmente i progetti Java tooyour, sostituendo in tal modo la versione precedente di hello.

### <a name="june-29-2016"></a>29 giugno 2016
Hello Azure Toolkit per Eclipse - versione di giugno 2016 include hello seguenti miglioramenti:

* **Requisito Java 8**. Hello Azure Toolkit per Eclipse, richiede ora Java 8, anche se questo requisito è solo per il toolkit di hello: le applicazioni possono continuare toouse tutte le versioni di Java supportate da Azure.
* **Supporto per JDK Java più recente di hello**. le versioni più recenti di Hello di hello Java JDK sono ora supportate da hello Azure Toolkit per Eclipse.
* **Supporto per Azure SDK versione 2.9.1**. versione più recente di Hello di hello Azure SDK è ora hello minimo prerequisito per hello Azure Toolkit per Eclipse.
* **Campioni integrati**. Hello Azure Toolkit per Eclipse include ora un'introduzione agli sviluppatori toohelp diverse applicazioni di esempio.
* **Integrazione dello strumento HDInsight**. Gli strumenti di HDInsight di Azure vengono aggregati ora hello Azure Toolkit per Eclipse. Per altre informazioni, vedere il [plug-in degli strumenti HDInsight per Eclipse].
* **Debug remoto delle app Web Java**. Hello Azure Toolkit per Eclipse supporta ora il debug remoto di App web Java nel servizio App di Azure.
* **Supporto per la versione di hello Luna Eclipse.** Hello nuova versione minima richiesta Eclipse IDE è Luna.

### <a name="april-12-2016"></a>12 aprile 2016
Hello Azure Toolkit per Eclipse - versione di aprile 2016 include hello seguenti miglioramenti:

* **Supporto per Azure SDK versione 2.9.0**. versione più recente di Hello di hello Azure SDK è ora hello minimo prerequisito per hello Azure Toolkit per Eclipse.
* **Vari usabilità, velocità di risposta e miglioramenti delle prestazioni correlati a supporto di App Web tooAzure**. Un numero di ottimizzazioni delle prestazioni in modo hello Toolkit comunica con il risultato di Azure in un'interfaccia utente più reattiva.
* **Capacità toodelete un contenitore di applicazione Web esistente in Azure da in Eclipse**. Hello Azure Toolkit per Eclipse consente ora toodelete un contenitore Web di Azure esistente senza uscire da Eclipse.

### <a name="march-7-2016"></a>7 marzo 2016
Hello Azure Toolkit per Eclipse - versione di marzo 2016 include hello seguenti miglioramenti:

* **Supporto per la distribuzione rapida di applicazioni Java leggere**. Hello Azure Toolkit per Eclipse supporta ora la distribuzione rapida di hello delle applicazioni Java leggere in contenitori di App Web di Azure, pertanto la distribuzione di applicazioni Java ora accetta secondi anziché minuti.
* **Supporto per la gestione di App Web utilizzando la visualizzazione di Esplora risorse di Azure hello**. visualizzazione di Esplora risorse di Azure Toolkit hello Hello supporta ora per elenco, avvio e arresto di App Web di Azure.
* **Distribuzioni aggiornate di Tomcat, Jetty e Zulu OpenJDK**. Hello Azure Toolkit per Eclipse fornisce supporto per le versioni aggiornate di Tomcat, Jetty e Zulu OpenJDK per le distribuzioni di Java in servizi cloud di Azure.

### <a name="january-4-2016"></a>4 gennaio 2016
Hello Azure Toolkit per Eclipse - versione di gennaio 2016 include hello seguenti miglioramenti:

* **Supporto per Zulu OpenJDK Aggiorna hello**. Per ulteriori informazioni, vedere hello [pagina web di Azul Systems per Zulu OpenJDK hello].
* **Distribuzioni aggiornate di Tomcat e Jetty**. sono state aggiornate Hello Jetty Tomcat le distribuzioni e quali sono disponibili in Microsoft Azure per l'utilizzo con hello Azure Toolkit per Eclipse.
* **Parità di funzionalità tra i toolkit Eclipse e IntelliJ per Azure**. Hello Azure Toolkit per Eclipse e hello [Azure Toolkit per IntelliJ] ora supportano hello stesso set di funzionalità.

### <a name="september-1-2015"></a>1° settembre 2015
Hello Azure Toolkit per Eclipse - versione di settembre 2015 include hello seguenti miglioramenti:

* **Supporto per Zulu OpenJDK Aggiorna hello**. Per ulteriori informazioni, vedere hello [pagina web di Azul Systems per Zulu OpenJDK hello].
* **Distribuzioni aggiornate di Tomcat e Jetty**. sono state aggiornate Hello Jetty Tomcat le distribuzioni e quali sono disponibili in Microsoft Azure per l'utilizzo con hello Azure Toolkit per Eclipse. (Queste distribuzioni consente agli sviluppatori toocreate rapido sviluppo e test i progetti con hello Azure Toolkit per Eclipse.
* **Supporto per i riferimenti di Tomcat e Jetty aggiornati automaticamente**. In aggiunta toohello specifiche versioni di Tomcat e Jetty disponibili in Azure, gli sviluppatori ora possono fare riferimento a un hello tooas cui distribuzione "più recente (auto-aggiornato)", che aggiorna automaticamente toohello distribuzione più recente di ogni versione principale versione di hello Jetty o Tomcat successivo le istanze del ruolo vengono riciclate. (Viene eseguito il riciclo automaticamente, ma gli sviluppatori possono attivare manualmente un riciclo tramite hello portale di Azure). Questa nuova funzionalità significa che gli sviluppatori non è necessario tooredeploy loro toohave in grado di toobe applicazione software server aggiornato. (
* Questa funzionalità è attualmente concepita solo a scopo di sviluppo e test e per applicazioni non cruciali e non è consigliabile per l'ambiente di produzione.
* **Visualizzazione di esplorazione delle risorse di Azure per BLOB, code e tabelle nell'archiviazione di Azure**. Questo consente agli sviluppatori un set di attività comuni con i relativi elementi di archiviazione direttamente dall'IDE di Eclipse hello tooperform. Ad esempio, eliminazione, caricamento o download di BLOB.

### <a name="august-1-2015"></a>1° agosto 2015
Hello Azure Toolkit per Eclipse - versione di agosto 2015 include hello seguenti miglioramenti:

* **Gestione della chiave di strumentazione di Application Insights**. Questo aggiornamento consente tooacquire, creare e gestire le chiavi di strumentazione di Application Insights direttamente dall'IDE di Eclipse hello.
* **Microsoft JDBC Driver 4.1 per SQL Server**. Questo aggiornamento include il supporto per il driver JDBC più recente di hello per Microsoft SQL Server.
* **Versione 2.7 di hello Azure SDK**. Questo toohello aggiornamento più recente di Azure SDK è hello nuovo prerequisito per hello Toolkit quando viene installato in Windows. Non è necessario nei sistemi operativi non Windows.
* **Supporto per l'aggiornamento di hello v7 Zulu OpenJDK**. Per ulteriori informazioni, vedere hello [pagina web di Azul Systems per Zulu OpenJDK hello].

### <a name="may-1-2015"></a>1° maggio 2015
Hello Azure Toolkit per Eclipse - versione di maggio 2015 include hello seguenti miglioramenti:

* **Interfaccia utente migliorata per la selezione del server**. Questa versione semplifica l'utilizzo di hello di hello toolkit nei sistemi operativi non Windows.
* **Supporto per i progetti Maven**. Questa versione supporta i progetti Maven come applicazioni, quali toolkit hello è possibile distribuire tooAzure e configurare Application Insights.
* **Versione 2.6 di Azure SDK hello**. Questo toohello aggiornamento più recente di Azure SDK è hello nuovo prerequisito per hello Toolkit quando viene installato in Windows. Non è necessario nei sistemi operativi non Windows.
* **Aggiornamento della distribuzione invece della ripubblicazione**. Se si sta ripubblicando un progetto di distribuzione quando la versione precedente di hello è già in tempo reale, hello toolkit ora Usa funzionalità di aggiornamento della distribuzione di Azure anziché arrestare la distribuzione precedente hello e ripubblicare da zero, come in hello precedente. Questo consente il toorun servizio cloud senza interruzioni quando possibile, consentendo di ottenere un'elevata disponibilità anche durante un aggiornamento e consente di velocizzare hello nuovamente processo di pubblicazione.
* **Supporto per più recente di Zulu OpenJDK v8 a hello - aggiornamento 40**. Per ulteriori informazioni, vedere hello [pagina web di Azul Systems per Zulu OpenJDK hello].

### <a name="march-9-2015"></a>9 marzo 2015
Hello Azure Toolkit per Eclipse - versione di marzo 2015 include hello seguenti miglioramenti:

* **Supporto per Mac, Ubuntu e altre versioni di Linux**. Questa versione di hello Azure Toolkit per Eclipse aggiunge il supporto per Mac OS e diverse piattaforme Unix, pertanto gli sviluppatori possono installare toocreate toolkit hello, configurare e pubblica progetti di Java tooAzure dei servizi Cloud (PaaS) da Eclipse in esecuzione in sistemi operativi diverso da Windows.

> [!NOTE]
> Questa funzionalità è disponibile in anteprima e non è consigliabile usarla in ambienti di produzione. Non è disponibile un contratto di servizio per l'assistenza clienti, ma l'invio di qualsiasi tipo di commenti e suggerimenti è consigliabile e apprezzato.
> 
> 

* **Nuovo plug-in di Application Insights**. Gli sviluppatori sono in grado di tooconfigure la telemetria server automatica con Application Insights in Azure.
* **Automazione della distribuzione da riga di comando basata su Ant**. Questa funzionalità consente la pubblicazione di hello tooautomate gli sviluppatori per le versioni più recenti delle proprie distribuzioni usando Ant all'esterno di Eclipse. Uno script pregenerato viene configurato automaticamente per un progetto dopo hello prima volta che viene distribuito da Eclipse e nelle distribuzioni successive possono utilizzare hello script toofully automatizzare le distribuzioni tramite riga di comando hello solo.
* **Disponibilità di Tomcat e Jetty in Azure per una distribuzione più semplice e veloce**. Gli sviluppatori ora possono fare riferimento a vari Tomcat e Jetty versioni disponibili in Azure direttamente invece di disporre di un account di tootheir server Java tooupload (o tramite hello Toolkit), quindi non è non tooupload necessario un server Java per scenari introduttivi e veloce.
* **Metodo di scelta rapida per la pubblicazione di servizi cloud di Java web App tooAzure**. curva di apprendimento hello tooreduce per gli scenari di sviluppo e test semplici, gli sviluppatori possono pubblicare le applicazioni Java più direttamente tooAzure. Anziché toogo tramite il processo di hello di creazione e configurazione di un progetto di distribuzione di Azure, le applicazioni verranno distribuite con un'istanza predefinita di Tomcat v8 e Zulu JVM (OpenJDK).

### <a name="january-30-2015"></a>30 gennaio 2015
Hello Azure Toolkit per Eclipse - versione di gennaio 2015 include hello seguenti miglioramenti:

* **Supporto per IBM® WebSphere® Application Server Liberty Core**. Questa versione aggiunge hello IBM WebSphere Application Server Liberty Core toohello elenco di server applicazioni supportati da quale hello toolkit è in grado di toodeploy tooAzure. Quest'ultima aggiunta espande l'elenco corrente di hello del server applicazioni supportati &quot;di casella&quot; da hello Toolkit, che già include diverse versioni di Tomcat, Jetty, JBoss e GlassFish.
* **Inclusione di Application Insights SDK**. Questa libreria di API client rilasciate di recente (v 0.9.0) fa ora parte di Package for Azure Libraries for Java hello.
* **Aggiornamento del Package for Azure Libraries for Java**. Questo aggiornamento include Azure Libraries for Java v 0.7.0 e Storage Client API v 2.0.0, nonché v 0.9.0 hello di Application Insights SDK rilasciate di recente.

### <a name="november-12-2014"></a>12 novembre 2014
Hello Azure Toolkit per Eclipse - versione di novembre 2014 include i seguenti miglioramenti hello:

* **Supporto per Azure SDK 2.5**. Questo toohello aggiornamento più recente di Azure SDK è hello nuovo prerequisito per hello Toolkit.
* **Supporto per la versione aggiornata pacchetti hello Zulu OpenJDK v 1.8, v 1.7 e v 1.6**. Per ulteriori informazioni, vedere hello [pagina web di Azul Systems per Zulu OpenJDK hello].
* **Supporto per nuove dimensioni D Standard hello per i servizi cloud**, che offre il miglioramento delle prestazioni e le risorse di memoria aggiuntiva. Per altre informazioni, vedere la pagina [Dimensioni delle macchine virtuali e dei servizi cloud per Azure].

### <a name="october-17-2014"></a>17 ottobre 2014
Hello Azure Toolkit per Eclipse - versione di ottobre 2014 include i seguenti miglioramenti hello:

* **Miglioramenti delle prestazioni in scenari di hello pubblica tooCloud**. Il caricamento delle informazioni di sottoscrizione è più veloce nel caso di utenti con più sottoscrizioni e account di archiviazione.
* **Supporto per la versione aggiornata del pacchetto di hello Zulu OpenJDK v 1.8**. Per ulteriori informazioni, vedere hello [pagina web di Azul Systems per Zulu OpenJDK hello].
* **Supporto per deprecare le versioni precedenti dei JDK di terze parti**. Pacchetti JDK deprecati non sono più visualizzati nel menu a discesa hello per nuovi progetti di distribuzione. Progetti esistenti che fanno riferimento a pacchetti JDK deprecati continueranno in grado di toodo per volta hello, ma è consigliabile tooupgrade toorely tali progetti in hello più recente.
* **Versione aggiornata di hello Package for Azure Libraries per libreria di API client Java**. Per ulteriori informazioni, vedere hello [API Client di Microsoft Azure].
* **Correzioni di bug.** Questa versione contiene numerose correzioni di bug varie basate su report degli utenti e testing.

### <a name="august-5-2014"></a>5 agosto 2014
Hello Azure Toolkit per Eclipse - versione di agosto 2014 include i seguenti miglioramenti hello

* **Supporto per Azure SDK 2.4.** Le versioni precedenti di hello Eclipse Toolkit non funzionerà con questo nuovo SDK.
* **Le versioni aggiornate di hello Zulu OpenJDK v 1.6, 1.7 e v 1.8 pacchetti.** Per ulteriori informazioni, vedere hello [pagina web di Azul Systems per Zulu OpenJDK hello].
* **Versione aggiornata di hello Package for Azure Libraries per la libreria di API client di Java.** Per ulteriori informazioni, vedere hello [API Client di Microsoft Azure].
* **Supporto per il più recente formato di file delle impostazioni di pubblicazione.** È stato aggiunto il supporto per la versione 2.0 del formato di file di impostazioni di pubblicazione hello.
* **Modifiche all'architettura sottostante funzionalità tooCloud pubblica di hello.** Hello Toolkit è ora utilizzando hello appena rilasciato API Client di Microsoft Azure per Java per il supporto di pubblicazione al cloud.
* **Correzioni di bug.** Questa versione include numerose correzioni di bug richieste dagli utenti.

### <a name="june-12-2014"></a>12 giugno 2014
Hello Azure Toolkit per Eclipse - versione di giugno 2014 è un aggiornamento di manutenzione secondario che fornisce i seguenti miglioramenti hello:

* **Il supporto per hello Zulu OpenJDK v 1.8 di pacchetto.** Per ulteriori informazioni, vedere hello [pagina web di Azul Systems per Zulu OpenJDK hello].
* **Versioni aggiornate di hello Zulu OpenJDK v 1.6 e 1.7 pacchetti.** Per ulteriori informazioni, vedere hello [pagina web di Azul Systems per Zulu OpenJDK hello].
* **Versione aggiornata di hello Package for Azure Libraries per la libreria di API client di Java.** Per ulteriori informazioni, vedere hello [API Client di Microsoft Azure].
* **Correzioni di bug.** Questa versione include numerose correzioni di bug richieste dagli utenti.

### <a name="april-4-2014"></a>4 aprile 2014
è stata rilasciata Hello Azure Plugin for Eclipse - versione di aprile 2014. Questo è un aggiornamento accompagna versione hello di hello Azure SDK 2.3, che è un prerequisito e verrà scaricato automaticamente quando si installa hello di plug-in. Questo aggiornamento include nuove funzionalità, correzioni di bug e alcuni miglioramenti a livello di usabilità basati su feedback dall'hello anteprima di febbraio 2014:

* **Supporto per la versione di hello Azure SDK 2.3.** Hello Azure Plugin for Eclipse - versione di aprile 2014 richiede Azure SDK 2.3. Quando si utilizza hello nuovo plug-in, se non si dispone già di Azure SDK 2.3, sarà possibile tooallow richiesta l'installazione. Non utilizzare Azure SDK 2.3 con le versioni precedenti di plug-in hello.
* **Aggiornamento di applicazioni senza la distribuzione del pacchetto completo.** Quando si distribuiscono applicazioni Java che fanno parte del progetto, plug-in hello ora carica automaticamente nell'account di archiviazione selezionato in modo che sia possibile aggiornarlo e riciclare hello ruolo istanze toodeploy hello applicazioni più recente senza toorebuild e ridistribuire hello intero pacchetto.
* **Tomcat 8 ora è un server applicazioni riconosciuto.** Se si seleziona una directory di installazione di Tomcat 8 nel computer locale hello **Server** scheda di hello **Azure Deployment Project** finestra di dialogo, plug-in hello verrà automaticamente il rilevamento ed essere in grado di toodeploy Tomcat 8 in modo automatico, simile toohello versioni precedenti di Tomcat già nell'elenco di hello.
* **Aggiornamenti pacchetto Azul Zulu OpenJDK: v1.7 aggiornamento 51 e v1.6 aggiornamento 47.** A partire da questa versione è disponibile l'aggiornamento 51 del pacchetto Zulu Open JDK v7 di Azul System. Iniziano anche a essere disponibili i pacchetti Zulu Open JDK v6 a partire dall'aggiornamento 47. Questi aggiornamenti sono inoltre toohello aggiornamento disponibile in precedenza Zulu Open JDK v7 pacchetto aggiornamento 45, 40 e 25 aggiornare.
* **Supporto per le dimensioni A8 e A9 delle macchine virtuali di Microsoft Azure.** È ora possibile distribuire un cloud servizio toohello elevato della memoria A8 e le dimensioni della macchina virtuale A9. Per altre informazioni su queste dimensioni delle macchine virtuali, vedere [Dimensioni delle macchine virtuali e dei servizi cloud per Azure].
* **Reindirizzamento automatico da tooHTTPS HTTP per i ruoli abilitato per SSL.** Quando il servizio cloud contiene solo ruoli HTTPS, se richiesta dell'utente hello specifica HTTP, verrà reindirizzati automaticamente tooHTTPS. Non è un hello toohandle ruolo separato HTTP non toocreate necessità richieste.
* **Express Emulator usato per l'emulazione locale.** Hello Express Emulator di Azure viene ora usato come emulatore hello durante il debug delle applicazioni in locale.
* **Re-branding di Azure in Microsoft Azure.** Le schermate dell'interfaccia utente riflettono il re-branding di Azure che non è più denominato Azure.

### <a name="february-6-2014"></a>6 febbraio 2014
Hello Azure Plugin for Eclipse di febbraio 2014 anteprima ha rilasciato. Questo aggiornamento include nuove funzionalità, correzioni di bug e alcuni miglioramenti a livello di usabilità basati su feedback dall'hello anteprima di ottobre 2013:

* **Supporto per l'offload SSL.** Offload Sockets Layer (SSL) protetto è stato aggiunto come funzionalità, consentono di abilitare tooeasily Hypertext Transfer Protocol Secure (HTTPS) supportano nella distribuzione Java in Azure, senza la necessità di tooconfigure SSL nel server applicazioni Java. Ciò è particolarmente rilevante nell'affinità di sessione e/o negli scenari di comunicazione autenticati. Ad esempio, quando si utilizza hello servizio Access Control (ACS) filtrare, già supportato dal toolkit hello. Per ulteriori informazioni, vedere [offload SSL] e [come tooUse offload SSL].
* **GlassFish 4 ora è un server applicazioni riconosciuto.** Se si seleziona una directory di installazione di GlassFish 4 nel computer locale hello **Server** scheda di hello **Azure Deployment Project** finestra di dialogo, plug-in hello verrà automaticamente il rilevamento ed essere in grado di toodeploy GlassFish OSE 4 in modo automatico, simile versione toohello GlassFish OSE 3 già nell'elenco di hello.
* **Aggiornamento 45 del pacchetto Azul Zulu OpenJDK.** Partire da questa versione, aggiornamento 45 per Azul System Zulu (pacchetto Open JDK v7) è ora disponibile. Questo è inoltre aggiornamento disponibile in precedenza toohello 40 e 25 aggiornare.
* **Supporto dell'impostazione automatica per le porte di endpoint private.** È possibile impostare un tooautomatic porta privata per gli endpoint di input e gli endpoint interni toolet Azure assegna un endpoint toothat porta automaticamente. In precedenza era possibile assegnare solo un numero di porta specifico.
* **Supporto per la personalizzazione di nome (CN) del certificato hello in hello autofirmati la creazione del certificato dell'interfaccia utente.** In precedenza, hello stesso nome a livello di codice è stato utilizzato per tutti i nuovi certificati; ora è possibile specificare la propria toohelp nome certificato distinguere tra più certificati in hello portale di Azure usati per scopi diversi.
* **Barra degli strumenti di Azure:** hello Azure sulla barra degli strumenti è stata aggiornata con hello seguenti modifiche: 
  * ![][ic710876]Questa icona è stato aggiunto per hello **New Azure Deployment Project**.
  * ![][ic710877]Questa icona è stato aggiunto come una finestra di dialogo Creazione di un certificato autofirmato toohello di scelta rapida.
* **Supporto per le dimensioni A5 delle macchine virtuali di Azure.** È ora possibile distribuire un cloud servizio toohello elevato della memoria dimensione A5 della macchina virtuale. Per altre informazioni sulle dimensioni delle macchine virtuali, vedere [Dimensioni delle macchine virtuali e dei servizi cloud per Azure].
* **Supporto per Microsoft Windows Server 2012 R2.** È ora possibile selezionare Windows Server 2012 R2 come sistema operativo di hello cloud.

### <a name="october-22-2013"></a>22 ottobre 2013
Hello Azure Plugin for Eclipse di ottobre 2013 Preview è stata rilasciata. Questo aggiornamento include nuove funzionalità, correzioni di bug e alcuni miglioramenti a livello di usabilità basati su feedback dall'hello anteprima di settembre 2013:

* **Supporto per la versione di hello Azure SDK 2.2.** Hello Azure Plugin for Eclipse - ottobre 2013 Preview supporta Azure SDK 2.2. plug-in Hello funzionerà comunque con Azure SDK 2.1 e installerà automaticamente Azure SDK 2.2 se non si dispone già di almeno Azure SDK 2.1 installato.
* **Aggiornamento 40 del pacchetto Azul Zulu OpenJDK.** Come annunciato per hello settembre 2013 Preview, hello ora plug-in consente l'utilizzo di un JDK fornito da terze parti direttamente in Azure, senza la necessità di tooupload JDK personalizzato. Nella versione di ottobre 2013 hello, aggiornamento 40 per Zulu (pacchetto Open JDK v7) di Azul System è ora disponibile. Questo è in toohello aggiunta a quella pubblicata originariamente dell'aggiornamento 25.
* **Collegamento alla distribuzione cloud in hello Log attività.** All'interno di hello Log attività di Azure, quando la distribuzione ha lo stato **pubblicato**, è possibile fare clic su **pubblicato** poiché corrisponde a una distribuzione tooyour collegamento; la distribuzione verrà quindi aperta nel browser. (hello stato **pubblicato** in precedenza è stato denominato **esegue**.)
* **Selezione del sistema operativo disponibile in fase di pubblicazione.** Hello **pubblicare tooAzure** finestra di dialogo contiene un nuovo campo, **sistema operativo di destinazione**, che fornisce un modo più facilmente individuabile per tooset è il sistema operativo di destinazione.
* **Sovrascrittura automatica della distribuzione precedente.** Hello **pubblicare tooAzure** finestra di dialogo contiene una nuova casella di controllo, **Sovrascrivi distribuzione precedente**. Se questa opzione è selezionata, quando viene pubblicata la nuova distribuzione verrà automaticamente sovrascritta distribuzione precedente hello; si verifica una situazione non &quot;409 conflict&quot; problemi durante la pubblicazione toohello nello stesso percorso senza prima Annullamento distribuzione precedente hello.
* **Jetty 9 ora è un server applicazioni riconosciuto.** Se si seleziona una directory di installazione di Jetty 9 nel computer locale hello **Server** scheda di hello **Azure Deployment Project** finestra di dialogo, plug-in hello verrà automaticamente il rilevamento ed essere in grado di toodeploy Jetty 9 in un modo automatico, simile toohello versioni precedenti di Jetty già nell'elenco di hello.
* **Aggiungere un ruolo dal menu di scelta rapida progetto hello.** Hello **Azure** il menu di scelta rapida progetto contiene ora una nuova voce di menu **Aggiungi ruolo**, che fornisce un modo più rapido e più facilmente individuabile per si tooadd un tooyour ruolo nuovo progetto Azure.
* **Un aggiornamento toohello pacchetto per hello librerie di Azure per la libreria di Java.** Si basa sulla versione 0.4.6 dell'hello [API Client di Microsoft Azure].

### <a name="september-25-2013"></a>25 settembre 2013
Hello Azure Plugin for Eclipse di settembre 2013 Preview è stata rilasciata. Questo aggiornamento include nuove funzionalità, correzioni di bug e alcuni miglioramenti a livello di usabilità basati su feedback dall'hello anteprima di agosto 2013:

* **Capacità toodeploy hello pacchetto Azul Zulu OpenJDK disponibile in Azure.** Una nuova opzione è stato aggiunto quando si specifica hello JDK toouse con la distribuzione di Azure. Utilizzando questa opzione, è possibile distribuire un pacchetto JDK di terze parti direttamente nel cloud di Azure, hello senza tooupload personalizzati. Azul Systems fornisce hello innanzitutto tale pacchetto chiamato Zulu, basati su OpenJDK, che può essere distribuito utilizzando questa opzione hello.
* **Un aggiornamento toohello pacchetto per hello librerie di Azure per la libreria di Java.** Si basa sulla versione 0.4.5 dell'hello [API Client di Microsoft Azure].

### <a name="august-1-2013"></a>1° agosto 2013
Hello Azure Plugin for Eclipse di agosto 2013 Preview è stata rilasciata. Questo è un aggiornamento accompagna versione hello di hello Azure SDK 2.1, che è un prerequisito e verrà scaricato automaticamente quando si installa hello di plug-in. Questo aggiornamento include nuove funzionalità, correzioni di bug e alcuni miglioramenti a livello di usabilità basati su feedback dall'hello anteprima di luglio 2013:

* **La rimozione di opzioni tooinclude hello JDK locale e il server applicazioni locale come parte del pacchetto di distribuzione hello.** Download di hello JDK e server applicazioni dall'archiviazione cloud durante la distribuzione di hello è preferibile tooembedding tali componenti in hello del pacchetto, poiché il download dei risultati di elementi hello in tempi di distribuzione più veloce e dimensioni pacchetto distribuzione più piccoli e più semplice manutenzione. Di conseguenza, hello opzioni tooinclude hello JDK e server applicazioni in pacchetto di distribuzione hello sono state rimosse. Progetti esistenti che sono stati configurati tooinclude hello JDK locale e il server applicazioni locale come parte del pacchetto di distribuzione hello verrà automaticamente convertito tooauto-caricamento hello JDK archiviazione e dell'applicazione server toocloud.
* **Supporto per la versione di hello Azure SDK 2.1.** Hello Azure Plugin for Eclipse di agosto 2013 Preview richiede Azure SDK 2.1. Non utilizzare Anteprima di agosto 2013 hello con le versioni precedenti di hello Azure SDK e si utilizza Azure SDK 2.1 con le versioni precedenti di hello Azure Plugin for Eclipse.
* **Supporto per la versione di Eclipse Kepler hello.** Toothis correlati, hello nuova versione minima richiesta IDE di Eclipse è Indigo. Hello Azure Plugin for Eclipse è non è più ufficialmente testato in Helios.

### <a name="july-3-2013"></a>3 luglio 2013
Hello Azure Plugin for Eclipse di luglio 2013 Preview è stata rilasciata. Questo aggiornamento include nuove funzionalità, correzioni di bug e alcuni miglioramenti a livello di usabilità basati su feedback rispetto hello potrebbe 2013 Preview:

* **Possibilità toocreate un nuovo account di archiviazione.** Oggetto **New** pulsante è stato aggiunto toohello **Add Storage Account** finestra di dialogo. In questo modo è toocreate un account di archiviazione all'interno di plug-in Eclipse hello, senza la necessità di toolog in toohello il portale di gestione di Azure. (Abbia già una sottoscrizione di Azure di toouse questa funzionalità.) Per ulteriori informazioni sulla creazione di un nuovo account di archiviazione, vedere [toocreate un nuovo account di archiviazione].
* **Nuova opzione &quot;(auto)&quot; per l'account di archiviazione usato per la distribuzione automatica di JDK e server e per la memorizzazione nella cache.** Quando si utilizza hello **caricamento automatico** opzione per hello JDK e server applicazioni, è ora possibile specificare **(auto)** per hello URL e l'archiviazione al toouse di account durante il caricamento di hello JDK e server applicazioni, o quando si utilizza la memorizzazione nella cache di Azure. Queste funzionalità, quindi, utilizzerà automaticamente hello stesso account di archiviazione come hello che si seleziona in hello **pubblicare tooAzure** finestra di dialogo. Hello [la creazione di un'applicazione Hello World per Azure in Eclipse] esercitazione è stata aggiornata toouse hello nuovo **(auto)** opzione.
* **Capacità tooset gli endpoint del servizio di Azure.** Specificare gli endpoint del servizio hello che determinano che se l'applicazione è distribuita tooand gestita dalla piattaforma Azure globale hello, Azure gestito da 21Vianet in Cina o una privata piattaforma Azure. Per altre informazioni, vedere [Endpoint del servizio di Azure].
* **Possibilità di specificare una risorsa di archiviazione locale per distribuzioni di grandi dimensioni.** In caso di hello che la distribuzione è troppo grande toobe contenuta nella cartella approot predefinita di hello, è ora possibile specificare una risorsa di archiviazione locale come destinazione di distribuzione hello per il JDK e server applicazioni. Per altre informazioni, vedere [Distribuzione di distribuzioni di grandi dimensioni].
* **Supporto per le dimensioni A6 e A7 delle macchine virtuali di Azure.** È ora possibile distribuire un cloud servizio toohello elevato della memoria A6 e dimensioni delle macchine virtuali A7. Per altre informazioni su queste dimensioni, vedere [Dimensioni delle macchine virtuali e dei servizi cloud per Azure].
* **Un aggiornamento toohello pacchetto per hello librerie di Azure per la libreria di Java.** Si basa sulla versione 0.4.4 dell'hello [API Client di Microsoft Azure].

### <a name="may-1-2013"></a>1° maggio 2013
Hello Azure Plugin for Eclipse - potrebbe 2013 Preview ha rilasciato. Questo è un aggiornamento principale accompagna versione hello di hello Azure SDK 2.0, che è un prerequisito e verrà scaricato automaticamente quando si installa hello di plug-in. Questa versione include nuove funzionalità, correzioni di bug e alcuni miglioramenti a livello di usabilità basati su feedback dall'hello anteprima di febbraio 2013:

* **Caricamento automatico del JDK hello e server applicazioni e distribuzione da archiviazione di Azure.** Una nuova opzione che consente di caricare automaticamente hello JDK selezionato e il server applicazioni, quando necessario, tooa specificato l'account di archiviazione di Azure e distribuire questi componenti da qui, invece di incorporamento nel pacchetto di distribuzione hello o having di caricamento utente hello quindi manualmente. Questa funzionalità comunemente richiesta può migliorare notevolmente la facilità di hello di hello distribuzione JDK e i componenti server, specialmente per gli utenti meno esperti. Per una procedura dettagliata sull'uso di queste opzioni, vedere [la creazione di un'applicazione Hello World per Azure in Eclipse].
* **Verifica dell'account di archiviazione e gli account di archiviazione tooreference possibilità più facilmente (tramite un controllo elenco a discesa) centralizzati.** Si applica toomultiple funzionalità che si basano sull'archiviazione, ad esempio JDK e distribuzione dei componenti server e la memorizzazione nella cache. Per altre informazioni, vedere [Elenco di account di archiviazione di Azure].
* **Configurazione dell'accesso remoto semplificato nella procedura guidata tooCloud di hello pubblica.** È sufficiente toodo è di tipo in un nome utente e password tooenable accesso remoto o lasciare vuota la casella tookeep accesso remoto disabilitato.
* **Un aggiornamento toohello pacchetto per hello librerie di Azure per la libreria di Java.** Si basa sulla versione 0.4.2 dell'hello [API Client di Microsoft Azure].
* **Supporto per le sessioni permanenti in Windows Server 2012.** In precedenza le sessioni permanenti funzionavano solo in Windows Server 2008 R2, mentre ora entrambe le destinazioni dei sistemi operativi cloud supportano l'affinità di sessione.
* **Miglioramenti delle prestazioni di caricamento del pacchetto.** Anche quando hello JDK e server applicazioni sono incorporati nel pacchetto di distribuzione hello, parte relativa al caricamento hello hello processo di distribuzione può essere circa due volte più rapidamente rispetto tooprevious versioni.

### <a name="february-8-2013"></a>8 febbraio 2013
Hello Azure Plugin for Eclipse di febbraio 2013 Preview è stata rilasciata. Si tratta di un aggiornamento secondario include correzioni di bug, miglioramenti a livello di usabilità basati su feedback e alcune nuove funzionalità dall'hello anteprima di novembre 2012:

* Supporto per la distribuzione di JDK, server applicazioni e arbitrario altri componenti di Azure pubblico o privato il download di archiviazione anziché includerli nel pacchetto di distribuzione hello durante la distribuzione cloud toohello del blob.
* Ordine di hello toochange possibilità in cui vengono elaborati i componenti di un ruolo definito dall'utente, mediante aggiunta hello di **Sposta su** e **Sposta giù** pulsanti hello **componenti** sezione di hello **Azure Role Properties**.
* Un aggiornamento toohello **pacchetto per Azure Libraries for Java hello** libreria, basata sulla versione 0.4.0 di hello [API Client di Microsoft Azure].

### <a name="november-5-2012"></a>5 Novembre 2012
Hello Azure Plugin for Eclipse - novembre 2012 anteprima ha rilasciato. Si tratta di un aggiornamento principale include numerose nuove funzionalità, nonché correzioni di bug aggiuntive e miglioramenti a livello di usabilità basati su feedback dall'hello settembre 2012 anteprima:

* Supporto per Microsoft Windows Server 2012 come sistema operativo di hello cloud.
* Supporto per la memorizzazione nella cache di Azure con risorse condivise per i client che supportano Memcache.
* Inclusione delle librerie client di Apache Qpid JMS hello per sfruttare i vantaggi della messaggistica basata su Azure AMQP.
* Un miglioramento **nuovo progetto** procedura guidata, con una nuova pagina alla fine di hello che fornisce gli utenti con hello possibilità tooquickly abilitare diverse funzionalità principali comuni nel progetto: sessioni permanenti, memorizzazione nella cache e il debug remoto.
* Riduzione automatica di too1 di istanze di ruolo durante l'esecuzione nell'emulatore di calcolo hello, tooavoid conflitti di binding porta tra istanze del server.

### <a name="september-28-2012"></a>28 settembre 2012
Hello Azure Plugin for Eclipse - settembre 2012 anteprima ha rilasciato. Questo aggiornamento del servizio include una serie di correzioni di bug aggiuntive rispetto hello anteprima di agosto 2012, nonché alcuni miglioramenti a livello di usabilità basati su feedback nelle funzionalità esistenti:

* Supporto per Microsoft Windows 8 e Microsoft Windows Server 2012 come sistema operativo di sviluppo hello, risoluzione dei problemi che in precedenza impedivano hello di plug-in di funzionare correttamente in questi sistemi operativi.
* Supporto migliorato per specificare gli intervalli di porte degli endpoint.
* Correzioni di bug relativi toofile percorsi contenenti spazi.
* Miglioramenti del menu contesto ruolo per impostazioni di configurazione specifiche toorole di accesso più veloce.
* Perfezionamenti secondari nella hello **pubblicare toocloud** procedura guidata e una serie di correzioni di bug aggiuntive.

### <a name="august-28-2012"></a>28 agosto 2012
Hello Azure Plugin for Eclipse - agosto 2012 anteprima ha rilasciato. Questo aggiornamento del servizio include correzioni di bug aggiuntive dopo hello anteprima di luglio 2012, nonché miglioramenti a livello di usabilità basati su commenti e suggerimenti per le funzionalità esistenti:

* In finestra di dialogo Azure Access Control Services Filter hello:
  * **Hello tooembed opzione certificato di firma** nel file WAR dell'applicazione, toosimplify del cloud di distribuzione.
  * **Opzione toocreate un certificato autofirmato** all'interno di ACS hello filtrare dell'interfaccia utente. Per ulteriori informazioni su hello Azure Access Control Services Filter, vedere [come utenti Web con accesso controllo servizio Azure usando Eclipse tooAuthenticate].
* Nella procedura guidata Azure Deployment Project hello (si applica anche pagina proprietà di configurazione del Server del ruolo toohello):
  * **L'individuazione automatica di hello percorso JDK** nel computer in uso (che è possibile ignorare).
  * **Il rilevamento automatico del tipo di server hello** quando si seleziona directory di installazione server applicazione hello.

### <a name="july-15-2012"></a>15 luglio 2012
Hello Azure Plugin for Eclipse - luglio 2012 anteprima, che risolve un numero di hello bug di priorità più alto trovati e/o segnalati dagli utenti dopo hello versione giugno 2012, è stata rilasciata. Questo è solo un aggiornamento del servizio, non include nuove funzionalità.

### <a name="june-7-2012"></a>7 giugno 2012
È stata rilasciata la versione CTP di Azure Plugin for Eclipse di giugno 2012. Le nuove funzionalità includono:

* **Creazione guidata nuovo progetto di distribuzione di Azure:** consente si tooselect il JDK, server applicazioni Java e le applicazioni Java direttamente in hello migliorata della procedura guidata dell'interfaccia utente. Sono incluse nell'elenco di hello del server della casella configurazioni toochoose da Tomcat 6, Tomcat 7, GlassFish OSE 3, Jetty 7, Jetty 8, JBoss 6 e JBoss 7 (autonomo). Inoltre, è possibile personalizzare l'elenco di hello configurazioni del server. Questo miglioramento dell'interfaccia utente è un'alternativa toodragging e l'eliminazione di file compressi e copiare gli script di avvio è stata precedentemente hello approccio principale. Quel metodo funziona ancora correttamente, ma verrà probabilmente usato per scenari più avanzati.
* **Pagina delle proprietà ruolo Server Configuration:** consente tooeasily commutatore hello JDK, server applicazioni Java e le applicazioni associate con la distribuzione dopo aver creato il progetto di hello. Per altre informazioni, vedere [Proprietà di configurazione del server].
* **&quot;Pubblicare toocloud&quot; procedura guidata:** fornisce un modo semplice di toodeploy tooAzure il progetto direttamente da Eclipse, automazione hello in precedenza manuale impegnativo di recuperare le credenziali, la firma nel portale di gestione di Azure, toohello Carica un pacchetto, e così via. Per un esempio di come toodirectly distribuire tooAzure il progetto, vedere [la creazione di un'applicazione Hello World per Azure in Eclipse].
* **Barra degli strumenti di Azure:** barra degli strumenti di Azure è ora disponibile in Eclipse, che contiene i pulsanti per richiamare hello seguenti caratteristiche:
  * ![][ic710879]**Run in Azure Emulator**: esegue il progetto nell'emulatore hello.
  * ![][ic710880]**Reimposta emulatore di Azure**: Reimposta hello emulatore.
  * ![][ic710881]**Build Cloud Package for Azure**: compila il pacchetto per la distribuzione.
  * ![][ic710876]**New Azure Deployment Project**: crea un nuovo progetto di distribuzione di Azure.
  * ![][ic710882]**Pubblicare tooAzure Cloud**: pubblica tooAzure il progetto.
  * ![][ic710883]**Unpublish**: elimina la distribuzione.
  * Molti di questi pulsanti della barra degli strumenti di Azure vengono usati in [la creazione di un'applicazione Hello World per Azure in Eclipse].
* **Azure Libraries for Java:** ora disponibile come parte di hello singolo pacchetto per librerie di Azure per la libreria di Java in Eclipse, accompagna l'installazione di plug-in di hello e che contiene tutte le dipendenze necessarie come hello. Aggiungere una raccolta di toohello informazioni di riferimento nel progetto Java e non è necessario toodownload nulla separatamente. Per ulteriori informazioni, vedere [installazione hello Azure Toolkit per Eclipse].
* **Microsoft JDBC Driver 4.0 per SQL Server disponibile durante l'installazione di plug-in:** durante l'installazione di hello nuovo plug-in, è possibile installare versioni più recenti di hello di hello Microsoft JDBC Driver per SQL Server.
* **Azure Access Control Service Filter disponibile durante l'installazione di plug-in:** questo nuovo componente, incluso come una libreria di Eclipse Toolkit hello, consente il Java web application tooseamlessly sfruttano di Azure servizio Access Control (ACS) autenticazione tramite diversi provider di identità, ad esempio Google, Live.com e Yahoo!. Non è necessario utilizzare la logica di autenticazione toowrite manualmente, è sufficiente configurare alcune opzioni e consente di eseguire hello pesante alla rimozione dell'abilitazione toosign utenti tramite ACS filtro hello. È possibile concentrarsi solo sulla scrittura di codice hello che offre agli utenti accesso tooresources basata sull'identità, come restituito tooyour applicazione dal filtro hello in oggetto richiesta hello. Per un'esercitazione sull'utilizzo di ACS hello filtro, vedere [come utenti Web con accesso controllo servizio Azure usando Eclipse tooAuthenticate].
* **Il rilevamento automatico del prerequisito hello Azure SDK 1.7:** quando si crea un nuovo progetto di distribuzione di Azure, Azure SDK 1.7 verranno scaricate automaticamente se non è già installato.
* **Endpoint di istanza:** consente l'accesso diretto agli endpoint delle porte per la comunicazione con le istanze del ruolo con carico bilanciato. È possono aggiungere gli endpoint dell'istanza tramite endpoint hello dell'interfaccia utente, disponibile tramite hello [proprietà endpoint] pagina. Ciò consente di abilitare il debug remoto e la diagnostica JMX per specifiche di calcolo istanze in esecuzione nel cloud hello in scenari con multi-istanza distribuzioni. 
* **Componenti dell'interfaccia utente:** rende più semplice per gli utenti avanzati tooset le dipendenze del progetto tra singoli ruoli di Azure nel progetto hello e altre risorse esterne, ad esempio progetti di applicazioni Java; rende facile toodescribe logica di distribuzione . Per altre informazioni, vedere [Proprietà dei componenti].
* **L'aggiornamento automatico delle versioni precedenti dei progetti:** quando si apre un'area di lavoro che include il progetto Azure creato con una versione precedente di plug-in di hello, progetti precedenti hello verranno visualizzati in Eclipse come chiusi, perché le versioni precedenti dei progetti non sono compatibile con una nuova versione di hello. Se si tenta di tooopen uno di questi progetti precedenti, verrà avviata una procedura guidata di aggiornamento. Se si accetta toohello aggiornamento, un nuovo progetto, **Upgraded** nome toohello accodati, verranno creati e aggiornati automaticamente toowork con nuova versione di hello. È possibile rinominare il nuovo progetto di hello in base alle esigenze. Come parte dell'aggiornamento di hello, il progetto originale non verrà modificato e rimarrà chiuso.

### <a name="december-10-2011"></a>10 dicembre 2011
È stata rilasciata la versione CTP di Azure Plugin for Eclipse di dicembre 2011. Le nuove funzionalità includono:

* **Supporto per affinità di sessione (&quot;sessioni permanenti&quot;):** consente di abilitare applicazioni Java con stato in cluster tramite una semplice casella di controllo. Per altre informazioni, vedere [Affinità di sessione].
* **Pre-apportate esempi di script di avvio:** per hello server Java più comuni (Tomcat, Jetty, JBoss, GlassFish), che è possibile semplicemente copiati e incollati dalle directory degli esempi del progetto nello script di avvio.
* **Output di avvio dell'emulatore in tempo reale:** è possibile osservare esecuzione hello di tutti i passaggi di hello dallo script di avvio in una finestra della console dedicata, che mostra lo stato di avanzamento hello e gli errori nello script come viene eseguita da Azure.
* **Monitoraggio automatico leggero di java.exe:** forza un riciclo dei ruoli quando si interrompe l'esecuzione di java.exe usando uno script leggero predefinito incluso nella distribuzione.
* **Interfaccia utente di configurazione di debug remoto di app Java:** consente si tooeasily abilitare tooaccess debugger remoto di Eclipse all'app Java in esecuzione in hello emulatore o hello cloud di Azure, è possibile eseguire un'istruzione e il debug del codice Java in tempo reale. Per altre informazioni, vedere [Debug delle applicazione Azure in Eclipse].
* **Interfaccia utente di configurazione risorsa di archiviazione locale:** in modo non è più necessario tooconfigure di risorse locali manipolando direttamente hello XML. Questa funzionalità consente inoltre tooaccess toohello percorso effettivo della risorsa locale dopo la distribuzione tramite una variabile di ambiente, che è possibile fare riferimento direttamente dallo script di avvio. Per altre informazioni, vedere [Proprietà dell'archiviazione in locale].
* **Configurazione della variabile di ambiente dell'interfaccia utente:** in modo non è più necessario tooset le variabili di ambiente tramite la modifica manuale del file XML di configurazione hello. Per altre informazioni, vedere [Proprietà delle variabili di ambiente].
* **Il driver JDBC per SQL Azure:** viene installato tramite plug-in hello come una libreria di Eclipse integrata direttamente, l'abilitazione di programmazione più semplice per SQL Azure. 
* **Interfaccia utente di configurazione dal menu di scelta rapida accesso toorole**: solo pulsante destro del mouse sulla cartella ruolo hello e fare clic su **proprietà**.
* **Icone personalizzate del progetto di Azure e della cartella del ruolo:** per una migliore visibilità e un'esplorazione più facile dell'area di lavoro e del progetto.

## <a name="see-also"></a>Vedere anche
Per ulteriori informazioni su hello Azure Toolkit per ambienti Java, vedere hello seguenti collegamenti:

* [Toolkit di Azure per Eclipse]
  * *Novità in Azure Toolkit for Eclipse (articolo) hello*
  * [installazione hello Azure Toolkit per Eclipse]
  * [Creare un'app Web Hello World per Azure in Eclipse]
  * [Sign In istruzioni per hello Azure Toolkit per Eclipse]
* [Azure Toolkit per IntelliJ]
  * [Novità in Azure Toolkit per IntelliJ hello]
  * [Installazione di hello Azure Toolkit per IntelliJ]
  * [Sign In istruzioni per hello Azure Toolkit per IntelliJ]
  * [Creare un'App Web Hello World per Azure in IntelliJ]

Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure].

<!-- URL List -->

[Toolkit di Azure per Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij.md
[Creare un'app Web Hello World per Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Creare un'App Web Hello World per Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[installazione hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Installazione di hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Sign In istruzioni per hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign In istruzioni per hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[What's New in hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novità in Azure Toolkit per IntelliJ hello]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Sign In istruzioni per hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[come un'App Web come un contenitore Docker usando toopublish hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-publish-as-docker-container.md
[utilizzando la gestione di account di archiviazione di Azure Explorer per Eclipse hello]: ./azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer.md
[utilizzando Gestione delle macchine virtuali di Azure Explorer per Eclipse hello]: ./azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer.md

[Centro per sviluppatori Java di Azure]: http://go.microsoft.com/fwlink/?LinkID=699547

[pagina web di Azul Systems per Zulu OpenJDK hello]: http://go.microsoft.com/fwlink/?LinkId=402457
[Endpoint del servizio di Azure]: http://go.microsoft.com/fwlink/?LinkID=699526
[Elenco di account di archiviazione di Azure]: http://go.microsoft.com/fwlink/?LinkID=699528
[Proprietà dei componenti]: http://go.microsoft.com/fwlink/?LinkID=699525#components_properties
[la creazione di un'applicazione Hello World per Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Debug delle applicazione Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699535
[Distribuzione di distribuzioni di grandi dimensioni]: http://go.microsoft.com/fwlink/?LinkID=699536
[proprietà endpoint]: http://go.microsoft.com/fwlink/?LinkID=699525#endpoints_properties
[Proprietà delle variabili di ambiente]: http://go.microsoft.com/fwlink/?LinkID=699525#environment_variables_properties
[plug-in degli strumenti HDInsight per Eclipse]: ./hdinsight/hdinsight-apache-spark-eclipse-tool-plugin.md
[come utenti Web con accesso controllo servizio Azure usando Eclipse tooAuthenticate]: http://go.microsoft.com/fwlink/?LinkID=264703
[come tooUse offload SSL]: http://go.microsoft.com/fwlink/?LinkID=699545
[L'installazione di hello Azure Toolkit per Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Proprietà dell'archiviazione in locale]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties
[API Client di Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=280397
[Proprietà di configurazione del server]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[Affinità di sessione]: http://go.microsoft.com/fwlink/?LinkID=699548
[offload SSL]: http://go.microsoft.com/fwlink/?LinkID=699549
[toocreate un nuovo account di archiviazione]: http://go.microsoft.com/fwlink/?LinkID=699528#create_new
[Dimensioni delle macchine virtuali e dei servizi cloud per Azure]: http://go.microsoft.com/fwlink/?LinkId=466520

<!-- IMG List -->

[ic710876]: ./media/azure-toolkit-for-eclipse-whats-new/ic710876.png
[ic710877]: ./media/azure-toolkit-for-eclipse-whats-new/ic710877.png
[ic710879]: ./media/azure-toolkit-for-eclipse-whats-new/ic710879.png
[ic710880]: ./media/azure-toolkit-for-eclipse-whats-new/ic710880.png
[ic710881]: ./media/azure-toolkit-for-eclipse-whats-new/ic710881.png
[ic710876]: ./media/azure-toolkit-for-eclipse-whats-new/ic710876.png
[ic710882]: ./media/azure-toolkit-for-eclipse-whats-new/ic710882.png
[ic710883]: ./media/azure-toolkit-for-eclipse-whats-new/ic710883.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh694270.aspx -->
