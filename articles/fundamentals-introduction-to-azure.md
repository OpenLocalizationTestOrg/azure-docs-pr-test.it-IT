---
title: aaaIntro tooMicrosoft Azure | Documenti Microsoft
description: Nuovo tooMicrosoft Azure? Ottenere una panoramica di base di hello servizi offerte con esempi di come si rivelano utili.
services: " "
documentationcenter: .net
author: rboucher
manager: carolz
editor: 
ms.assetid: 6f47f711-2208-4c21-8c1d-826a54c05c29
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2015
ms.author: robb
ms.openlocfilehash: 6791506abe813e19ca7b04d78d35cb46352a9028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-microsoft-azure"></a>Introduzione a Microsoft Azure
Microsoft Azure è una piattaforma di applicazione di Microsoft per il cloud pubblico hello.  obiettivo di Hello di questo articolo è toogive è una base per comprendere i principi fondamentali di hello di Azure, anche se non riconosce i cloud computing.

**Come tooread questo articolo**

Azure sta crescendo tutto il tempo hello è facile tooget di overload.  Iniziare con i servizi base hello, che vengono elencati per primi in questo articolo e quindi passare tooadditional servizi. Implica che non è possibile utilizzare solo i servizi aggiuntivi di hello autonomamente, ma i servizi di base hello costituiscono core hello di un'applicazione in esecuzione in Azure.

**Commenti e suggerimenti**

I commenti degli utenti sono importanti. Questo articolo dovrebbe fornire una panoramica efficiente di Azure. In caso contrario, segnalare nella sezione commenti hello nella parte inferiore di hello della pagina hello. Fornire alcuni dettagli sui quali previsto toosee e come tooimprove hello articolo.  

## <a name="hello-components-of-azure"></a>Hello componenti di Azure
Azure Raggruppa i servizi in categorie in hello portale di gestione e su vari strumenti visivi come hello [che cos'è Azure infografica](https://azure.microsoft.com/documentation/infographics/azure/) . Portale di gestione di Hello è ciò che si usa toomanage più (ma non tutte) di servizi in Azure.

In questo articolo verrà utilizzato un **organizzazione diversa** tootalk sui servizi basati su funzione simili e toocall importanti servizi secondari che fanno parte di quelli più grandi.  

![Componenti di Azure](./media/fundamentals-introduction-to-azure/AzureComponentsIntroNew780.png)   
 *Figura: Azure fornisce servizi per applicazioni accessibili tramite Internet ed eseguiti nei data center di Azure.*

## <a name="management-portal"></a>Portale di gestione
Azure offre un'interfaccia web chiamata hello [portale di gestione](http://manage.windowsazure.com) che consente agli amministratori tooaccess e amministrare la maggior parte, ma Azure non di tutte le funzionalità.  In genere, Microsoft rilascia hello più recente dell'interfaccia utente del portale beta prima della disattivazione uno precedente. Hello più recente viene chiamato hello ["Portale di anteprima di Azure"](https://portal.azure.com/).

Quando entrambi i portali sono attivi si verifica in genere una lunga sovrapposizione: benché i servizi principali siano disponibili in entrambi i portali, non tutte le funzionalità potrebbero esserlo. Servizi più recenti potrebbero essere visualizzate in hello più recente del portale prima e meno recenti servizi e funzionalità può esistere solo in hello quello meno recente.  messaggio Hello qui è che se non si trova un elemento nel portale precedente hello, controllare hello più recente e viceversa.

## <a name="compute"></a>Calcolo
Una delle operazioni di base di hello che una piattaforma cloud è eseguire le applicazioni. Ciascuno dei modelli di calcolo di Azure hello tooplay il proprio ruolo.

È possibile usare queste tecnologie separatamente o combinare la base appropriata in base alle necessità toocreate hello per l'applicazione. approccio Hello scelta dipende sui problemi che si sta tentando di toosolve.

### <a name="azure-virtual-machines"></a>Macchine virtuali di Azure
![Macchine virtuali di Azure ROBBCSIART_TEST](./media/fundamentals-introduction-to-azure/mscsiart_VirtualMachinesIntroNew_12345.png)   
*Figura: Macchine virtuali di Azure offre il controllo completo su istanze di macchine virtuali nel cloud hello.*

possibilità di Hello toocreate una macchina virtuale su richiesta, se viene fornito da un'immagine standard o da una, può rivelarsi molto utile. Questo approccio, comunemente noto come IaaS (Infrastructure as a Service), è quanto fornito da Macchine virtuali di Azure. La figura 2 mostra una combinazione dell'esecuzione di una macchina virtuale (VM) e la modalità toocreate da un disco rigido virtuale.  

toocreate una macchina virtuale, specificare il disco rigido virtuale toouse e hello della dimensione della macchina virtuale.  Quindi paga per ora hello che hello che macchina virtuale è in esecuzione. Si paga per minuto hello e solo in fase di esecuzione, se è disponibile un addebito di archiviazione minima per mantenere hello VHD disponibili. Azure offre una raccolta di dischi rigidi virtuali (denominati "immagini") che contengono toostart un sistema operativo avviabile dal magazzino. Includono opzioni Microsoft e dei partner, ad esempio Windows Server e Linux, SQL Server, Oracle e molte altre ancora. È gratuito toocreate dischi rigidi virtuali e le immagini e quindi caricarli manualmente. Può persino caricare VHD che contengono solo dati e quindi accedere a tali VHD dalle macchine virtuali in esecuzione.

Ogni volta che hello VHD provenga da, è possibile archiviare in modo permanente le modifiche apportate durante l'esecuzione di una macchina virtuale. Hello in seguito che si creerà una macchina virtuale da tale disco rigido virtuale, operazioni prelevati in cui è stata interrotta. Hello dischi rigidi virtuali che nuovamente hello macchine virtuali vengono archiviati nel BLOB di archiviazione di Azure, si parlerà più avanti.  Ciò significa che si ottiene tooensure ridondanza che delle macchine virtuali non scompaiano a causa di errori toohardware e disco. È anche possibile toocopy hello modificato disco rigido virtuale all'esterno di Azure, quindi eseguirlo in locale.

L'applicazione viene eseguito all'interno di uno o più macchine virtuali, a seconda di come creato in precedenza o decidere toocreate, da zero.

Questo approccio generale piuttosto toocloud calcolo può essere utilizzato tooaddress diversi problemi.

**Scenari di macchine virtuali**

1. **Sviluppo/Test** -è possibile utilizzarle toocreate una piattaforma di sviluppo e test economica che è possibile arrestare quando hai finito di usarlo. oppure per creare ed eseguire applicazioni basate su qualsiasi linguaggio o libreria. Tali applicazioni possono utilizzare una delle opzioni di gestione dati hello forniti da Azure ed è anche possibile scegliere toouse SQL Server o un altro sistema DBMS in esecuzione in uno o più macchine virtuali.
2. **Spostare le applicazioni tooAzure (accuratezza e MAIUSC)** -"Sollevamento e spostamento" si riferisce toomoving applicazione molto come si utilizzerebbe un toomove carrelli un oggetto di grandi dimensioni.  È "accuratezza" hello disco rigido virtuale dal Data Center locale e "Sposta" in tooAzure ed eseguirlo.  In genere è toodo alcune dipendenze tooremove di lavoro in altri sistemi. Se sono presenti troppe dipendenze, è possibile scegliere l'opzione 3.  
3. **Estensione del data center** : usare le macchine virtuali Azure come estensione del data center locale, che esegue SharePoint o altre applicazioni. toosupport, è possibile toocreate domini di Windows nel cloud hello eseguendo Active Directory in macchine virtuali di Azure. È possibile utilizzare tootie di rete virtuale di Azure (illustrata più avanti) la rete locale e la rete in Azure contemporaneamente.

### <a name="web-apps"></a>App Web
![Applicazioni Web di Azure ROBBCSIART_TEST](./media/fundamentals-introduction-to-azure/mscsiart_AzureWebsitesIntroNew_12345.png)   
 *Figura: Le app Web di Azure esegue un'applicazione del sito Web nel cloud hello senza la necessità di server web di toomanage hello sottostante.*

Operazioni hello più comuni che gli utenti nel cloud hello viene eseguito siti e applicazioni web. Macchine virtuali di Azure consente, ma ancora lascia il compito di hello dell'amministrazione di uno o più macchine virtuali e hello sottostante i sistemi operativi. I ruoli Web dei servizi cloud possono effettuare questa operazione, ma implementarli e distribuirli richiede un'attività amministrativa.  Cosa accade se si desidera un sito Web in un altro utente si occupa di lavoro amministrazione hello?

Questo è ciò che fornisce esattamente App Web. Questo modello di calcolo offre un ambiente web gestita tramite il portale di gestione di Azure hello, nonché API. È possibile spostare un'applicazione del sito Web esistente in App Web invariata oppure è possibile creare una nuova direttamente nel cloud di hello. Quando un sito Web è in esecuzione, è possibile aggiungere o rimuovere le istanze in modo dinamico, basarsi su Bilanciamento delle richieste di applicazioni Web di Azure tooload tra loro. Le app di Azure offre un'opzione condivisa, il sito Web in cui viene eseguito in una macchina virtuale con altri siti, e un'opzione di standard che consente a un sito toorun nella propria macchina virtuale. opzione standard Hello consente inoltre di aumentare dimensioni hello (potenza di elaborazione) delle istanze in uso se necessario.

Per gli ambienti di sviluppo, App Web supporta .NET, PHP, Node.js, Java e Python insieme a database SQL e MySQL (di ClearDB, un partner Microsoft) per l'archivio relazionale. Fornisce inoltre il supporto incorporato per numerose applicazioni ampiamente diffuse, ad esempio WordPress, Joomla e Drupal. obiettivo di Hello è tooprovide un basso costo, scalabile e la piattaforma su vasta scala utile per la creazione di siti e applicazioni web nel cloud pubblico hello.

**Scenari di Applicazioni Web**

App Web è utile per le aziende, sviluppatori e agenzie di progettazione web di toobe desiderato. Per le aziende, si tratta di una soluzione di facile gestione, scalabile, estremamente sicura e a disponibilità elevate per l'esecuzione di siti Web di presenza. Quando è necessario tooset un sito Web, è migliore toostart con le app Web di Azure e procedere tooCloud servizi una volta è necessario una funzionalità che non è disponibile. Vedere a fine hello della sezione "Calcolo" hello per ulteriori collegamenti che consentono di toochoose tra le opzioni di hello.

### <a name="cloud-services"></a>Servizi cloud
![Servizio cloud di Azure](./media/fundamentals-introduction-to-azure/CloudServicesIntroNew.png)   
*Figura: Servizi Cloud di Azure fornisce un punto toorun altamente scalabile personalizzato codice su una piattaforma come un ambiente del servizio (PaaS)*

Si supponga di che voler toobuild un'applicazione cloud che può supportare un numero elevato di utenti simultanei e non richiede una quantità amministrazione mai diventa inattivo. Potrebbe essere un fornitore di software stabilita, ad esempio, che hanno deciso tooembrace Software come servizio (SaaS) per la creazione di una versione di una delle applicazioni nel cloud hello. Oppure di una start-up che si propone di creare un'applicazione per il grande pubblico per la quale è prevista una crescita rapida. Se si sceglie di utilizzare Azure, sarà necessario individuare il modello di esecuzione più adatto.

Applicazioni Web di Azure consente la creazione di questo tipo di applicazione Web, ma con alcuni vincoli, come ad esempio il fatto che non è disponibile un accesso amministrativo e pertanto non è possibile installare software arbitrario. Macchine virtuali di Azure offre grande flessibilità, incluso l'accesso amministrativo ed è certo che sia possibile utilizzarlo toobuild applicazioni estremamente scalabili, ma sarà necessario toohandle molti aspetti di affidabilità e amministrazione manualmente. Si desidera è un'opzione che consente di hello controllo, è necessario ma gestisce anche la maggior parte del lavoro hello necessaria per l'amministrazione e l'affidabilità.

Questo è ciò che offre Servizi cloud di Azure. Questa tecnologia è progettata espressamente toosupport scalabile, affidabile e bassa amministratore applicazioni ed è un esempio di ciò che viene comunemente denominata piattaforma come servizio (PaaS). toouse, si crea un'applicazione mediante la tecnologia di hello desiderato, ad esempio c#, Java, PHP, Python, Node.js o un altro elemento. Quindi, il codice viene eseguita in macchine virtuali (istanze di cui viene fatto riferimento tooas) in esecuzione una versione di Windows Server.

Ma queste macchine virtuali sono diversi dai hello quelle create con macchine virtuali di Azure. Innanzitutto, sono gestite da Azure, che effettua operazioni quali l'installazione di patch del sistema operativo e l'implementazione di nuove immagini con patch applicate. Ciò implica che l'applicazione non deve mantenere lo stato nelle istanze del ruolo web o di lavoro; è opportuno invece mantenere in una delle opzioni di gestione dati di Azure hello descritte nella sezione successiva hello. Azure esegue inoltre il monitoraggio di queste macchine virtuali, riavviando quelle che presentano errori. È possibile impostare cloud services tooautomatically creare istanze di più o meno nella risposta toodemand. In questo modo si toohandle aumento utilizzo e la scala in modo che la maggior parte non sono il pagamento quando è presente un utilizzo inferiore.

Si dispone di due ruoli toochoose da quando si crea un'istanza, entrambe basate su Windows Server. Hello differenza principale tra hello due è che un'istanza di un ruolo web in esecuzione IIS, mentre un'istanza di un ruolo di lavoro non. Entrambi sono gestiti in hello del comune per toouse un'applicazione sia stesso modo, tuttavia e. Ad esempio, un'istanza del ruolo web potrebbe accettare le richieste degli utenti, quindi passarli tooa istanza di ruolo di lavoro per l'elaborazione. tooscale verso l'alto o verso il basso l'applicazione, è possibile richiedere che Azure creare più istanze di un ruolo o di arrestare le istanze esistenti. E simili tooAzure macchine virtuali, vengono addebitati solo ora hello che ogni istanza del ruolo web o di lavoro è in esecuzione.

**Scenari di servizi cloud**

Servizi cloud sono toosupport ideale notevole scalabilità quando è necessario maggiore controllo sul piattaforma hello quelli previsti per le app Web di Azure, ma non il controllo del sistema operativo sottostante hello.

#### <a name="choosing-a-compute-model"></a>Scelta di un modello di calcolo
pagina Hello [confronto App Web di Azure, servizi Cloud e macchine virtuali](app-service-web/choose-web-site-cloud-service-vm.md) fornisce informazioni più dettagliate su come toochoose un modello di calcolo.

## <a name="data-management"></a>Gestione dati
Alle applicazioni servono i dati e ad applicazioni diverse servono tipi di dati diversi. Per questo motivo, Azure fornisce diversi modi toostore e gestire i dati. Azure fornisce numerose opzioni di archiviazione, ma sono tutte progettate per un'archiviazione prolungata nel tempo.  Con uno qualsiasi di queste opzioni, sono sempre presenti 3 copie dei dati mantenuti sincronizzati in un Data Center di Azure - 6, se si consente a Azure toouse tooback di ridondanza geografica dei Data Center tooanother almeno 300 miglia di distanza.     

### <a name="in-virtual-machines"></a>All'interno delle macchine virtuali
possibilità di Hello toorun SQL Server o un altro sistema DBMS in una macchina virtuale creata con macchine virtuali di Azure già citate. Tenere presente che questa opzione non è limitato toorelational sistemi. Puoi anche tecnologie NoSQL toorun gratuita, ad esempio MongoDB e Cassandra. È in esecuzione il sistema di database vengono replicati semplice it si è utilizzato tooin dei propri Data Center, ma richiede anche la gestione amministrazione hello del DBMS.  In altre opzioni, Azure gestisce più o intera amministrazione hello automaticamente.

Lo stato di hello di hello macchina virtuale e qualsiasi disco dati aggiuntivi creare o caricare nuovamente, sono supportate da archiviazione blob (che si parlerà più avanti).  

### <a name="azure-sql-database"></a>Database SQL di Azure
![Database SQL di archiviazione di Azure](./media/fundamentals-introduction-to-azure/StorageAzureSQLDatabaseIntroNew.png)   

*Figura: Database SQL di Azure fornisce un servizio di database relazionale gestito nel cloud hello.*

Per l'archiviazione relazionale, Azure offre funzionalità di hello Database SQL. Non lasciare hello denominazione ingannare l'utente. Si tratta di un database diverso rispetto a un tipico database SQL fornito da SQL Server in esecuzione su Windows Server.  

In precedenza denominato SQL Azure, Database SQL di Azure offre tutte hello le funzionalità principali di un database relazionale sistema di gestione, tra cui le transazioni atomiche, accesso ai dati simultaneo da più utenti con una programmazione familiare, query SQL ANSI e l'integrità dei dati modello. Come per SQL Server, è possibile accedere al database SQL mediante Entity Framework, ADO.NET, JDBC e altre tecnologie di accesso ai dati note. Supporta inoltre la maggior parte delle hello linguaggio T-SQL, insieme agli strumenti di SQL Server, ad esempio SQL Server Management Studio. Per chiunque abbia familiarità con SQL Server (o altro database relazionale), l'utilizzo del database SQL risulta estremamente semplice.

Database SQL non è semplicemente un DBMS in hello it cloud di un servizio PaaS. È comunque possibile controllare i dati e chi può accedervi, ma il Database SQL si occupa di lavoro amministrazione grunt hello, come la gestione dell'infrastruttura hardware hello e mantenere automaticamente software di database e del sistema operativo di hello backup toodate. Il database SQL fornisce disponibilità elevata, backup automatici, funzionalità di ripristino a un momento specifico e possibilità di replicare copie tra varie aree geografiche.  

**Scenari per il database SQL**

Se si sta creando un'applicazione Azure (tramite uno qualsiasi dei modelli di calcolo hello) che richiede l'archiviazione relazionale, Database SQL può essere una scelta ottimale. Le applicazioni in esecuzione cloud hello esterno è inoltre possono utilizzare questo servizio, tuttavia, pertanto vi sono molti altri scenari. Ad esempio, è possibile accedere ai dati archiviati in SQL Database da diversi sistemi client, inclusi desktop, portatili, tablet e telefoni cellulari. Poiché offre disponibilità elevata incorporata tramite replica, Database SQL consente inoltre di ridurre i tempi di inattività.

### <a name="tables"></a>Tabelle
![Tabelle di archiviazione di Azure](./media/fundamentals-introduction-to-azure/StorageTablesIntroNew.png)  

*Figura: Le tabelle di Azure offre toostore dati flat modo NoSQL.*

Questa funzionalità è a volte indicata con un nome diverso in quanto fa parte di una funzionalità più ampia denominata "archiviazione di Azure". Se viene visualizzato "tables", "Tabelle di Azure" o "tabelle di archiviazione", si tratta tutti hello stessa operazione.  

E non confondere in base al nome hello: questa tecnologia non fornisce l'archiviazione relazionale. Di fatto, è un esempio di approccio NoSQL denominato archivio chiave-valore. Le tabelle di Azure consentono a un'applicazione di archiviare proprietà di vari tipi, ad esempio stringhe, numeri interi e date. Un'applicazione può quindi recuperare un gruppo di proprietà fornendo una chiave univoca per tale gruppo. Mentre le complesse operazioni come join non sono supportati, le tabelle offrono dati tootyped l'accesso rapido. Si tratta anche molto scalabile, con un toohold in grado di singola tabella per quanto tempo un terabyte di dati. E corrispondenza loro semplicità, le tabelle sono in genere meno costoso toouse rispetto all'archiviazione relazionale del Database SQL.

**Scenari per le tabelle**

Si supponga che si desidera toocreate un'applicazione Azure che fast deve accedere ai dati tootyped, potrebbe essere un numero elevato di esso, ma non necessario tooperform SQL le query più complesse per i dati. Si supponga, ad esempio, che si sta creando un'applicazione consumer che richiede le informazioni cliente toostore per ogni utente. L'app verrà toobe molto diffuso, è necessario tooallow di grandi quantità di dati, ma è non serve a molto con i dati oltre la memorizzazione, quindi recuperarli in modo semplice. Si tratta esattamente hello tipo di scenario in cui le tabelle di Azure può risultare utile.

### <a name="blobs"></a>Blobs
![BLOB di archiviazione di Azure](./media/fundamentals-introduction-to-azure/StorageBlobsIntroNew.png)    
*Figura: i blob di Azure forniscono dati binari non strutturati.*  

BLOB di Azure (nuovamente solo "BLOB di archiviazione" e "Archiviazione di Blob" sono hello differisce) è progettata toostore dati binari non strutturati. Analogamente alle tabelle, i BLOB offrono una funzionalità di storage conveniente e un singolo BLOB può contenere fino a 1 TB (un terabyte) di dati. Le applicazioni di Azure possono inoltre utilizzare le unità Azure, tramite le quali i BLOB forniscono un archivio permanente per un file system Windows montato in un'istanza di Azure. un'applicazione Hello vede normali file di Windows, ma il contenuto di hello è effettivamente archiviato in un blob.

L'archiviazione BLOB è usata da molte altre funzionalità di Azure (tra cui le macchine virtuali), pertanto è sicuramente in grado di gestire anche i carichi di lavoro dell'utente.

**Scenari per i BLOB**

Un'applicazione per l'archiviazione di video, file di grandi dimensioni o altre informazioni binarie può usare i BLOB come soluzione di archiviazione semplice e a un costo contenuto. I BLOB sono anche comunemente usati insieme ad altri servizi come la rete per la distribuzione di contenuti, che verrà descritta in seguito.  

### <a name="import--export"></a>Importazione/esportazione
![Azure Import Export Service](./media/fundamentals-introduction-to-azure/ImportExportIntroNew.png)  

*Figura: Azure importazione / esportazione fornisce hello possibilità tooship tooor un disco rigido fisico da Azure per l'importazione di dati bulk più rapido ed economico o esportazione.*  

Talvolta toomove una grande quantità di dati in Azure. Questa operazione richiederebbe molto tempo, addirittura giorni, e l'uso di una elevata quantità di larghezza di banda. In questi casi, è possibile utilizzare importazione/esportazione di Azure, che consente di tooship crittografata con Bitlocker da 3,5" unità disco rigido SATA direttamente tooAzure data center, in cui Microsoft trasferirà hello dati nell'archiviazione blob per l'utente.  Una volta completato il caricamento di hello, Microsoft offre hello unità indietro tooyou.  È inoltre possibile richiedere che grandi quantità di dati dall'archiviazione Blob da esportare nel disco rigido in e inviato tooyou indietro tramite posta elettronica.

**Scenari di importazione/esportazione**

* **La migrazione dei dati di grandi dimensioni** : ogni volta che si dispone di grandi quantità di dati (terabyte) che si desidera tooupload tooAzure, servizio di importazione/esportazione hello è spesso molto più rapido ed economico probabilmente il trasferimento su hello rispetto a internet. Dopo aver aggiunto dati hello BLOB, è possibile elaborarlo in altri formati, ad esempio l'archiviazione tabelle o di un Database SQL.
* **Ripristino dei dati archiviati** -è possibile utilizzare importazione/esportazione toohave Microsoft trasferiscono grandi quantità di dati archiviati nell'archiviazione Blob di Azure tooa dispositivo di archiviazione è di trasmissione e quindi che il dispositivo recapitati tooa indietro posizione desiderata. Poiché questa operazione richiede del tempo, non è un'opzione idonea per il disaster recovery. È preferibile per i dati archiviati per i quali non occorre effettuare l'accesso velocemente.

### <a name="file-service"></a>Servizio file
![Servizio file di Azure](./media/fundamentals-introduction-to-azure/FileServiceIntroNew.png)    
*Figura: Servizi di File di Azure offre SMB \\ \\server\share. percorsi per le applicazioni in esecuzione nel cloud hello.*

In locale, è comune toohave grandi quantità di spazio di archiviazione di file accessibili tramite il protocollo Server Message Block (SMB) di hello utilizzando un \\ \\server\share. formato. Azure offre ora un servizio che consente di toouse questo protocollo nel cloud hello. Applicazioni in esecuzione in Azure è possono utilizzare il file tooshare tra le macchine virtuali utilizzando API come ReadFile e WriteFile del familiarità file system. Inoltre, è possono anche accedere file hello in hello contemporaneamente tramite un'interfaccia REST, che consente di condivisioni hello tooaccess locale quando si imposta anche una rete virtuale. File di Azure si basa su servizio blob hello, pertanto eredita hello stesso disponibilità, durabilità, scalabilità e ridondanza geografica incorporate in archiviazione di Azure.

**Scenari per File di Azure**

* **Migrazione cloud esistente di toohello app** -il più semplice toohello cloud di toomigrate locale applicazioni che utilizzano file presenta dati tooshare tra le parti di un'applicazione hello. Ogni macchina virtuale si connette toohello condivisione di file e quindi è possibile leggere e scrivere file esattamente come rispetto a un file locale condividerebbero.
* **Le impostazioni dell'applicazione condivisi** -un modello comune per le applicazioni distribuite è toohave i file di configurazione in una posizione centralizzata in cui è possibile accedervi da molte macchine virtuali diverse. Questi file di configurazione possono essere archiviati in una condivisione di File Azure ed essere letti da tutte le istanze delle applicazioni. le impostazioni di Hello possono anche essere gestite tramite l'interfaccia REST hello, che consente l'accesso in tutto il mondo toohello i file di configurazione.
* **Condivisione di diagnostica** : è possibile salvare e condividere file di diagnostica come log, metriche e dump di arresto anomalo del sistema. Presenza di questi file è disponibili tramite SMB hello e interfaccia REST consente un'ampia gamma di strumenti di analisi per l'elaborazione e analisi dei dati di diagnostica hello toouse applicazioni.
* **Sviluppo/Test/Debug** : quando gli sviluppatori o gli amministratori lavorano su macchine virtuali nel cloud hello, devono spesso un set di strumenti o utilità. L'installazione e la distribuzione di queste utilità su ogni macchina virtuale richiede molto tempo. I file di Azure, uno sviluppatore o un amministratore può archiviare i propri strumenti preferiti in una condivisione file e connettersi toothem da qualsiasi macchina virtuale.

## <a name="networking"></a>Rete
Azure viene attualmente eseguito in molti Data Center distribuiti in HelloWorld. Quando si esegue un'applicazione o archiviare i dati, è possibile selezionare uno o più toouse questi Data Center. È inoltre possibile connettere i Data Center toothese in vari modi tramite servizi hello riportati di seguito.

### <a name="virtual-network"></a>Rete virtuale
![VirtualNetwork](./media/fundamentals-introduction-to-azure/VirtualNetworkIntroNew.png)   

*Figura: Le reti virtuali fornisce una rete privata nel cloud hello in modo diversi servizi in grado di comunicare tooeach altro, o le risorse locali tooon se si imposta una connessione VPN cross-premise.*  

Un modo utile toouse un cloud pubblico è tootreat come un'estensione del proprio Data Center.

Grazie alla possibilità di creare macchine virtuali su richiesta e quindi di rimuoverle (interrompendo il pagamento) quando non sono più necessarie, è possibile disporre di ulteriore potenza di elaborazione solo quando serve. E poiché le macchine virtuali di Azure consente di creare macchine virtuali in esecuzione SharePoint, Active Directory e altro software locale familiarità, questo approccio può funzionare con le applicazioni di hello di che si dispone già.

toomake questo molto utile, tuttavia, gli utenti dovrebbero tootreat in grado di toobe queste applicazioni come se fossero in esecuzione nel proprio Data Center. E questo è il servizio offerto da Rete virtuale di Azure. Utilizza un dispositivo gateway VPN, un amministratore può configurare una rete privata virtuale (VPN) tra la rete locale e le macchine virtuali che sono distribuiti tooa rete virtuale in Azure. Poiché si assegna un IP v4 indirizzi toohello cloud macchine virtuali, vengono visualizzate toobe sulla rete. Gli utenti dell'organizzazione possono accedere alle applicazioni di hello tali macchine virtuali contengono come se fossero in esecuzione in locale.

Per altre informazioni sulla pianificazione e sulla creazione di una rete virtuale adatta alle esigenze dell'utente, vedere [Rete virtuale](virtual-network/virtual-networks-overview.md).

### <a name="express-route"></a>Express Route
![ExpressRoute](./media/fundamentals-introduction-to-azure/ExpressRouteIntroNew.png)   

*Figura: ExpressRoute utilizza una rete virtuale di Azure, ma vengono indirizzate le connessioni tramite linee anziché più velocemente dedicate hello rete Internet pubblica.*  

Se è necessaria ulteriore larghezza di banda o sicurezza rispetto a quelle che la rete virtuale di Azure è in grado di fornire, è possibile valutare ExpressRoute. In alcuni casi ExpressRoute può anche offrire un risparmio di denaro. È comunque necessario avere una rete virtuale in Azure, ma il collegamento hello tra Azure e il sito utilizza una connessione dedicata che non viene trasmesso hello rete Internet pubblica. In ordine toouse questo servizio, è necessario toohave un contratto con un provider di servizi di rete o un provider di exchange.

La configurazione di una connessione ExpressRoute richiede più tempo e la pianificazione, pertanto è opportuno toostart con una connessione VPN da sito a sito, quindi eseguire la migrazione tooan connessione ExpressRoute.

Per altre informazioni su ExpressRoute, vedere [Panoramica tecnica relativa a ExpressRoute](expressroute/expressroute-introduction.md).

### <a name="traffic-manager"></a>Gestione traffico
![TrafficManager](./media/fundamentals-introduction-to-azure/TrafficManagerIntroNew.png)   

*Figura: Traffic Manager di Azure consente di tooroute traffico globale tooyour servizio in base alle regole intelligente.*

Se l'applicazione Azure è in esecuzione in più Data Center, è possibile utilizzare in modo intelligente le richieste di gestione traffico di Azure tooroute degli utenti tra più istanze dell'applicazione hello. È inoltre possibile inviare traffico hello di tooservices non è in esecuzione in Azure, purché siano accessibili da internet.  

Un'applicazione Azure con utenti in solo una singola parte di hello world è possibile eseguire in un solo Data Center di Azure. Un'applicazione con utenti sparsi in tutto il mondo hello, tuttavia, è più probabile toorun in più Data Center, forse anche tutti gli elementi. In questo secondo caso, si trovano ad affrontare un problema: come è in modo intelligente indirizzare istanze tooapplication gli utenti? La maggior parte del tempo di hello, si vorrà ogni utente tooaccess hello Data Center più vicino tooher, poiché è probabile che sarà il tempo di risposta migliore hello. Ma cosa accade se quell'istanza dell'applicazione hello è sovraccarico o non disponibile? In questo caso, nel caso di essere automaticamente la richiesta toodirect nice tooanother datacenter. Questo è ciò che offre Gestione traffico di Azure.

proprietario Hello di un'applicazione definisce regole per specificare come le richieste degli utenti devono essere toodatacenters diretti, quindi si basano su gestione traffico toocarry out queste regole. Ad esempio, gli utenti potrebbero essere in genere Data Center di Azure più vicino toohello diretto, ma viene inviati tooanother uno quando il tempo di risposta hello dal proprio Data Center predefinito supera il tempo di risposta hello da altri Data Center. Per le applicazioni distribuite globalmente con molti utenti, è utile di problemi di servizio predefinito toohandle simili.

Gestione traffico Usa endpoint tooservice utenti tooroute di Directory Name Service (DNS), ma ulteriormente traffico non passa attraverso Traffic Manager dopo aver stabilita la connessione. In tal modo, Gestione traffico non costituisce un collo di bottiglia che potrebbe rallentare le comunicazioni del servizio.

## <a name="developer-services"></a>Servizi per gli sviluppatori
Azure offre numerosi strumenti toohelp sviluppatori e professionisti IT di creare e gestire le applicazioni nel cloud hello.  

### <a name="azure-sdk"></a>Azure SDK
Nel 2008, hello prima versione preliminare di Azure è supportato solo lo sviluppo di .NET. Oggi è invece possibile creare applicazioni Azure in qualsiasi linguaggio. Attualmente Microsoft fornisce SDK specifici per linguaggio per .NET, Java, PHP, Node.js, Ruby e Python. È inoltre disponibile un SDK di Azure generale che offre il supporto di base per qualsiasi linguaggio, ad esempio C++.  

Questi SDK supportano l'utente nelle attività di creazione, distribuzione e gestione di applicazioni Azure. È possibile scaricarli da [www.microsoftazure.com](https://azure.microsoft.com/downloads/) o GitHub e possono essere usati con Visual Studio ed Eclipse. Azure offre anche strumenti da riga di comando che gli sviluppatori possono usare con qualsiasi ambiente di sviluppo o editor, inclusi gli strumenti per la distribuzione di applicazioni tooAzure dai sistemi Linux e Macintosh.

Questi SDK, oltre a supportare gli utenti per la creazione di applicazioni Azure, forniscono librerie client che consentono di creare software che usa tali servizi di Azure. Ad esempio, è possibile compilare un'applicazione che legge e scrive i BLOB di Azure o creare uno strumento che consente di distribuire applicazioni Azure tramite l'interfaccia di gestione di Azure hello.

### <a name="visual-studio-team-services"></a>Visual Studio Team Services
Visual Studio Team Services è un nome di marketing che comprendono un numero che toodevelop delle applicazioni in hello Azure.

confusione tooavoid - non fornisce una versione basata su Web o ospitata di Visual Studio. È sempre necessario avere una copia in esecuzione in locale di Visual Studio. Tuttavia, fornisce molti altri strumenti che possono rivelarsi molto utili.

Include un sistema di controllo del codice sorgente ospitato denominato Team Foundation Service, che offre controllo della versione e rilevamento degli elementi di lavoro.  Per il controllo della versione è persino possibile usare Git, se si preferisce questa opzione. E può essere variata controllo del codice sorgente hello che è utilizzare dal progetto. È possibile creare progetti team privata senza limiti accessibile da un punto qualsiasi in HelloWorld.  

Visual Studio Team Services fornisce un servizio di test di carico. È possibile eseguire il test di carico creato in Visual Studio in macchine virtuali nel cloud hello. Specificare hello il numero totale di utenti da test tooload con, Visual Studio Team Services verrà automaticamente e determinare il numero di agenti necessari, creare rapidamente macchine virtuali hello necessario eseguire i test di carico. I sottoscrittori di MSDN ricevono migliaia di minuti-utente gratuiti di test di carico ogni mese.

Visual Studio Team Services offre inoltre il supporto per lo sviluppo Agile con funzionalità quali compilazione di integrazione continua, bacheche kanban e chat del team virtuali.

**Scenari di Visual Studio Team Services**

Visual Studio Team Services è un'opzione valida per le aziende che necessitano di toocollaborate in tutto il mondo e dispone già di infrastruttura hello in luogo toodo così. È possibile impostare in pochi minuti, scegliere un sistema di controllo del codice sorgente e iniziare a scrivere il codice e compilare il giorno stesso.  gli strumenti di team Hello forniscono una posizione per il coordinamento e la collaborazione e strumenti aggiuntivi hello forniscono analisi hello necessari tootest e ottimizzare rapidamente l'applicazione.

Tuttavia, le organizzazioni che già dispone di un sistema di on-premise possono testare i nuovi progetti in Visual Studio Team Services toosee se risulta più efficiente.   

### <a name="application-insights"></a>Application Insights
![Application Insights](./media/fundamentals-introduction-to-azure/ApplicationInsights.png)  

*Figura: Application Insights esegue il monitoraggio delle prestazioni e dell'utilizzo dell'app Web o del dispositivo attiva.*

Dopo aver pubblicato l'app, indipendentemente dal fatto che venga eseguita su dispositivi mobili, desktop o browser Web, Application Insights ne indica le prestazioni e le operazioni eseguite dagli utenti. Mantengono un conteggio di arresti anomali del sistema e di risposta lenti, di avviso se hello figure superano le soglie accettabile e consentono di diagnosticare i problemi.

Quando si sviluppa una nuova funzionalità, pianificare toomeasure il suo successo con gli utenti. Analizzando i modelli di utilizzo, è possibile ottenere informazioni sulle soluzioni ottimali per i clienti e migliorare l'app in ogni ciclo di sviluppo.

Anche se è ospitato in Azure, Application Insights funziona per una gamma sempre più vasta di app, sia in Azure che in altri ambienti. Sono supportate le app Web J2EE e ASP.NET, nonché le applicazioni per iOS, Android, OSX e Windows. Dati di telemetria viene inviato da un SDK compilato con l'applicazione hello, toobe analizzati e visualizzati in hello servizio Application Insights in Azure.

Se si desidera più specializzato analitica, esportare database tooa flusso dati di telemetria hello o tooPower BI o qualsiasi altro strumento.

**Scenari di Application Insights**

Si sta sviluppando un'app. Può trattarsi di un'app Web o un'app per dispositivi mobili o un'app per dispositivi mobili con back-end Web.

* Ottimizzare le prestazioni di hello dell'app dopo la pubblicazione o durante il test di carico.  Application Insights consente di aggregare i dati di telemetria da tutte le istanze di hello installato e si presenta con grafici di tempi di risposta richiesta e conteggio delle eccezioni, tempi di risposta delle dipendenze e altri indicatori di prestazioni. In questo modo, è possibile ottimizzare le prestazioni dell'app. È possibile inserire codice tooreport dati più specifici se è necessario.
* Rilevare e diagnosticare i problemi nell'app attiva. Se gli indicatori di prestazioni raggiungono valori di soglia accettabili, è possibile ottenere avvisi tramite posta elettronica. È possibile esaminare le sessioni utente specifico, ad esempio i richiesta hello toosee che ha causato un'eccezione.
* Tenere traccia dell'utilizzo tooassess hello esito ogni nuova funzionalità. Quando si progetta una nuova storia utente, pianificare toomeasure quanto viene usato e se gli utenti raggiungono gli obiettivi previsti. Application Insights offre dati di utilizzo di base, come visualizzazioni di pagina web, ed è possibile inserire codice tootrack hello esperienza dell'utente in modo più dettagliato.

### <a name="automation"></a>Automazione
Nessuno piace toowaste tempo hello manuale stesso elabora più volte. Automazione di Azure fornisce un modo per si toocreate, monitorare, gestire e distribuire le risorse nell'ambiente Azure.  

L'automazione utilizza "runbook", che utilizza i flussi di lavoro di Windows PowerShell (e PowerShell normali) in copre hello. I runbook sono concepiti toobe eseguito senza l'intervento dell'utente. Consente di flussi di lavoro PowerShell stato hello di un toobe script salvato al Checkpoint lungo hello modo. Se si verifica un errore, non è necessario toostart uno script da inizio hello. È possibile riavviarlo all'ultimo checkpoint hello. Ciò consente di risparmiare molto lavoro sta tentando di handle di script hello toomake tutti gli errori possibili.

**Scenari di automazione**

Automazione di Azure è un manuale di hello tooautomate scelta ottimale, esecuzione prolungata, soggette a errori e operazioni ripetute di frequente in Azure.

### <a name="api-management"></a>Gestione API
Creazione e la pubblicazione di interfacce (API) su hello internet è un tooapplications di servizi tooprovide modo comune. Se tali servizi sono resellable (ad esempio, dati meteorologici), un'organizzazione può consentire di terze parti tooaccess questi stessi servizi a pagamento. Quando si scala toomore partner, verranno in genere necessario toooptimize e controllare l'accesso.  Alcuni partner potrebbe essere necessario anche dati hello in un formato diverso.

Gestione API di Azure semplifica per le organizzazioni toopublish API toopartners, dipendenti e gli sviluppatori di terze parti in modo sicuro e scalabile. Fornisce un endpoint API diverso e funziona come un proxy toocall hello endpoint effettivo fornendo servizi come la memorizzazione nella cache, trasformazione, la limitazione delle richieste, controllo dell'accesso e aggregazione analitica.

**Scenari di Gestione API**

Si supponga che la società dispone di un set di dispositivi necessario tutte toocall tooa indietro servizio centrale tooget dati, ad esempio, una società di spedizioni che dispone di dispositivi in ogni camion spostamenti hello.  Certamente società hello desidererà tooset backup tootrack un sistema è proprio camion affinché possa stimare e aggiornare i tempi di recapito in modo affidabile. Può sapere quanti sono i veicoli in dotazione e pianificare in modo appropriato.  Ogni carrello sarà necessario un dispositivo che richiama tooa posizione centrale e di posizionamento e velocità dati, probabilmente più.

Un cliente di hello società di spedizione sarà probabilmente anche trarre vantaggio da ottenere i posizionamento di dati.  cliente Hello possibile utilizzarlo tooknow quanto prodotti siano tootravel, in cui essi improvvisi, quanti sono pagamento lungo determinate route (se combinato con ciò che è stato pagato tooship). Se hello società di spedizione consente di aggregare i dati già, molti clienti potrebbero pagare.  Ma deve tooprovide modo i clienti toogive hello dati quindi hello società di spedizione. Una volta che forniscono accesso toocustomers, potrebbero non disporre controllo sulla frequenza hello query sui dati. Hanno regole tooprovide su chi può accedere a dati. Tutte queste regole avrebbe toobe incorporate le API esterna. ed è in questa situazione che Gestione API può essere di aiuto.  

## <a name="identity-and-access"></a>Identità e accesso
L'utilizzo delle identità è importante per la maggior parte delle applicazioni. Le informazioni relative all'identità di un utente consentono a un'applicazione di decidere la modalità di interazione con tale utente. Azure fornisce servizi toohelp traccia identità nonché integrarlo con gli archivi di identità che si stia già utilizzando.

### <a name="active-directory"></a>Active Directory
Come la maggior parte dei servizi di directory, Azure Active Directory archivia informazioni sugli utenti e organizzazioni hello che cui appartengono. Consente agli utenti di accedere, quindi lo fornisce i token e di presentarle tooapplications tooprove la propria identità. Consente inoltre di sincronizzare le informazioni relative agli utenti con Windows Server Active Directory in esecuzione nella rete locale. Mentre i meccanismi di hello e formati di dati utilizzati da Azure Active Directory non sono identici a quelli usati in Windows Server Active Directory, le funzioni di hello che esegue sono molto simili.

È importante toounderstand che Azure Active Directory è progettato principalmente per l'utilizzo dalle applicazioni cloud. Può ad esempio essere usato da applicazioni in esecuzione in Azure o in altre piattaforme cloud. Viene anche usato dalle applicazioni di Microsoft, ad esempio le applicazioni di Office 365. Se si desidera tooextend il Data Center nel cloud di hello tramite macchine virtuali di Azure e rete virtuale di Azure, tuttavia, Azure Active Directory non è la scelta giusta hello. In alternativa, è opportuno toorun Windows Server Active Directory in macchine virtuali.

applicazioni toolet accedere a informazioni hello in esso contenute, Azure Active Directory fornisce un'API RESTful chiamato Graph di Azure Active Directory. Questa API consente alle applicazioni in esecuzione su tutti gli oggetti directory di accesso di piattaforma e le relazioni di hello tra loro.  Ad esempio, un'applicazione autorizzata potrebbe utilizzare questo toolearn API su un utente appartiene a gruppi di hello e altre informazioni. Le applicazioni è inoltre possono visualizzare le relazioni tra i relativi a utenti sociale grafico-consentendo agli sviluppatori li utilizzano connessioni hello tra persone più intelligente.

Un'altra funzionalità di questo servizio, Azure Active Directory Access Control, rende più semplice per informazioni sull'identità di tooaccept un'applicazione da Facebook, Google, Windows Live ID e altri provider di identità diffusi. Anziché richiedere hello applicazione toounderstand hello dati diversi formati e protocolli utilizzati da uno di questi provider, il controllo di accesso converte tutti gli elementi in un singolo formato comune. Consente inoltre a un'applicazione di accettare le informazioni di accesso da uno o più domini Active Directory. Ad esempio, un fornitore che offre un'applicazione SaaS potrebbe usare utenti toogive Access Control di Azure Active Directory in ogni applicazione di single sign-on toohello clienti.

I servizi directory rappresentano un rinforzo essenziale delle risorse di elaborazione locali. Non dovrebbe essere sorprendente che poiché sono importanti nel cloud hello.

### <a name="multi-factor-authentication"></a>Multi-Factor Authentication
![Azure Multi-Factor Authentication](./media/fundamentals-introduction-to-azure/MFAIntroNew.png)   

*Figura: Multi-Factor Authentication fornisce funzionalità di hello per l'applicazione di tooverify più di un modulo di identificazione*

La protezione è sempre importante. La Multi-Factor Authentication (MFA) garantisce che solo gli utenti stessi possano accedere ai propri account. La MFA (nota anche come autenticazione a due fattori, o "2FA") richiede agli utenti di fornire due di questi tre metodi di verifica dell'identità per gli accessi e le transazioni degli utenti.

* Un'informazione nota (in genere una password)
* Un oggetto che si possiede (un dispositivo attendibile non facile da duplicare, ad esempio un telefono)
* Una caratteristica fisica dell'utente (biometrica)

In modo quando un utente accede, è possibile richiedere tooalso verificare la propria identità con un'app per dispositivi mobili, una telefonata o un messaggio di testo in combinazione con la propria password. Per impostazione predefinita, Azure Active Directory supporta hello uso di password come unico metodo di autenticazione per l'accesso degli utenti. È possibile utilizzare l'autenticazione a più fattori con Azure AD o con applicazioni personalizzate e le directory utilizzando hello MFA SDK. È anche possibile usarla insieme ad applicazioni locali tramite il server Multi-Factor Authentication.

**Scenari di MFA**

Protezione degli accessi ad account sensibili, ad esempio dati di accesso bancari e accesso al codice sorgente quando l'immissione non autorizzata potrebbe comportare un costo elevato sulla proprietà finanziaria o intellettuale.   

## <a name="mobile"></a>Mobile
Se si sta creando un'app per un dispositivo mobile, Azure consente di archiviare dati nel cloud hello, autenticare gli utenti e inviare notifiche push senza che sia necessario toowrite una grande quantità di codice personalizzato.

Mentre è certo che sia possibile compilare back-end hello per un'app per dispositivi mobili usando le macchine virtuali, servizi Cloud o le applicazioni Web, che è possibile dedicare hello di scrittura molto meno tempo sottostante componenti del servizio mediante i servizi di Azure.

### <a name="mobile-apps"></a>App per dispositivi mobili
![App per dispositivi mobili](./media/fundamentals-introduction-to-azure/MobileServicesIntroNew.png)

*Figura: App per dispositivi mobili fornisce funzionalità comunemente richieste dalle applicazioni che si interfacciano con dispositivi mobili.*

App per dispositivi mobili di Azure fornisce molte funzionalità utili che consentono di risparmiare tempo nella creazione di un back-end per un'applicazione per dispositivi mobili. Consente di toodo semplice provisioning e la gestione dei dati archiviati in un Database SQL. Con il codice lato server è possibile usare facilmente opzioni aggiuntive di archiviazione di dati come lo storage BLOB o MongoDB. App per dispositivi mobili fornisce il supporto per le notifiche, anche se in determinati casi è possibile usare gli hub di notifica come descritto in seguito.  Hello è anche un'API REST che l'applicazione per dispositivi mobili può chiamare tooget lavoro svolto. App per dispositivi mobili offre inoltre funzionalità di hello utenti tooauthenticate tramite Microsoft e Active Directory, nonché altri provider di identità noti come Facebook, Twitter e Google.   

È possibile utilizzare altri servizi di Azure come ruoli di lavoro e Bus di servizio e connettere i sistemi tooon locale. È anche possibile utilizzare 3 componenti aggiuntivi di terze parti da hello funzionalità aggiuntive di tooprovide Azure Store (ad esempio SendGrid per la posta elettronica).

Librerie native client per Windows Store, Windows Phone, HTML/JavaScript, iOS e Android rendono toodevelop più semplice per le App in tutte le principali piattaforme per dispositivi mobili. Un'API REST consente si toouse dati di servizi mobili e funzionalità di autenticazione con le applicazioni su piattaforme diverse. Un singolo servizio mobile può supportare più app client in modo da offrire un'esperienza utente coerente su tutti i dispositivi.

Poiché Azure supporta già la scalabilità, è possibile gestire il traffico hello come app diventa più diffusi.  Monitoraggio e la registrazione sono supportati toohelp risolvere i problemi e gestire le prestazioni.

### <a name="notification-hubs"></a>Hub di notifica
![NotificationHubs](./media/fundamentals-introduction-to-azure/NotificationHubsIntroNew.png)  

*Figura: Hub di notifica fornisce le funzionalità comunemente richieste dalle applicazioni che si interfacciano con dispositivi mobili.*

Sebbene sia possibile scrivere codice toodo notifiche in App mobili di Azure, gli hub di notifica è ottimizzato toobroadcast milioni di notifiche push altamente personalizzati in pochi minuti.  Non è necessario tooworry sui dettagli come operatore di telefonia mobile o produttore del dispositivo. Ora è possibile raggiungere singoli utenti o milioni di utenti con una singola chiamata API.

Gli hub di notifica è progettato toowork con qualsiasi back-end. È possibile usare le app mobili di Azure, un back-end personalizzato nel cloud hello in esecuzione su qualsiasi provider o un back-end locale.

**Scenari di Hub di notifica** se si scrive un gioco per dispositivi mobili in cui i lettori impiegato attiva, potrebbe essere necessario toonotify player 2 tale lettore 1 terminato suo turno. Se è sufficiente toodo, è possibile utilizzare solo App per dispositivi mobili. Se si disponesse di 100.000 utenti, ma il gioco e si desidera toosend volta tooeveryone offerta gratuita riservate, gli hub di notifica è preferibile hello.

È possibile inviare ultime notizie, eventi sportivi e prodotto annuncio notifiche toomillions di utenti con bassa latenza. Le aziende possono notificare ai dipendenti nuovi comunicazioni sensibili ora, ad esempio clienti potenziali, pertanto i dipendenti non devono controllare la posta elettronica o altri toostay applicazioni informati tooconstantly. È possibile inviare password monouso richieste per l'autenticazione a più fattori.

## <a name="back-up"></a>Back-up
Ogni organizzazione deve toobackup e ripristinare i dati. È possibile utilizzare Azure toobackup e ripristinare l'applicazione in locale o cloud hello. Azure offre diverse opzioni toohelp in base al tipo di hello di backup.

### <a name="site-recovery"></a>Site Recovery
Azure Site Recovery (in precedenza Gestione ripristino Hyper-V) consentono di proteggere le applicazioni importanti coordinando hello replica e il ripristino tra siti. Il ripristino del sito fornisce applicazioni tooprotect funzionalità basati su Hyper-v, VMWare o SAN tooyour un sito secondario, il sito dell'hoster tooa o tooAzure ed evitare spese hello e dalla complessità di creare e gestire la propria posizione secondaria. Azure crittografa i dati e le comunicazioni e si dispone di opzione hello abilitare la crittografia per i dati a riposo troppo.

Esegue il monitoraggio dello stato di hello dei servizi in modo continuo e consente di automatizzare il ripristino di ordinato hello dei servizi nell'evento hello di interruzione in Data Center principale hello del sito. Macchine virtuali possono essere portate in un servizio di ripristino toohelp modo orchestrato rapidamente, anche per carichi di lavoro complessi a più livelli.

Site Recovery funziona con tecnologie esistenti quali la replica Hyper-V, System Center e SQL Server AlwaysOn. Per informazioni dettagliate, consultare [Panoramica di Azure Site Recovery](site-recovery/site-recovery-overview.md) .

### <a name="azure-backup"></a>Backup di Azure
![Backup di Azure](./media/fundamentals-introduction-to-azure/AzureBackupIntroNew.png)  

*Figura: Backup di Azure esegue il backup dei dati dal server Windows locali in cloud hello.*  

Backup di Azure esegue il backup dei dati dal server locale che esegue Windows Server nel cloud hello. È possibile gestire i backup direttamente da strumenti di backup hello in Windows Server 2012, Windows Server 2012 Essentials o System Center 2012 - Data Protection Manager. In alternativa, è possibile usare un agente di backup specializzato.

La protezione dei dati aumenta perché i backup vengono crittografati prima della trasmissione, archiviati in Azure e protetti con un certificato caricato dall'utente. servizio di Hello utilizza hello stessa protezione a disponibilità elevata e ridondanza dei dati nell'archiviazione di Azure.  È possibile eseguire il backup di file e cartelle in base a una pianificazione regolare oppure immediatamente, eseguendo backup completi o incrementali. Dopo il backup dei dati cloud toohello, gli utenti autorizzati possono facilmente in grado di ripristinare i backup tooany server. Offre inoltre criteri di conservazione dei dati configurabili, la compressione dei dati, di trasferimento dati e la limitazione delle richieste in modo da gestire hello costo toostore e il trasferimento di dati.

**Scenari per Backup di Azure**

Se si usa già Windows Server o System Center, Backup di Azure è una scelta naturale per eseguire il backup del file system del server, di macchine virtuali e di database SQL Server.  Backup di Azure funziona con file crittografati, sparse e compressi. Esistono alcune limitazioni, pertanto è necessario [verifica dei prerequisiti di Azure Backup hello](http://technet.microsoft.com/library/dn296608.aspx) prima.

## <a name="messaging-and-integration"></a>Messaggistica e integrazione
Indipendentemente da quanto accade, spesso è necessario codice toointeract con altro codice.  In alcune situazioni, è sufficiente un messaggio in coda di base. In altri casi, sono necessarie interazioni più complesse. Azure offre alcuni modi diversi toosolve questi problemi. Figura 5 sono illustrate le scelte di hello.

### <a name="queues"></a>Code
![Inoltro del bus di servizio di Azure](./media/fundamentals-introduction-to-azure/QueuesIntroNew.png)

*Figura: le code consentono l'accoppiamento di tipo loose tra parti di un'applicazione e facilitano la scalabilità.*  

L'accodamento si basa su un concetto semplice: un'applicazione colloca un messaggio in una coda e il messaggio viene quindi letto da un'altra applicazione. Se l'applicazione deve solo questo servizio semplice, le code di Azure potrebbe essere la scelta migliore hello.

A causa di hello modo hello che Azure aumento delle dimensioni nel tempo, le code di archiviazione di Azure e code del Bus di servizio forniscono servizi di Accodamento messaggi analoghi. motivi per cui toouse su hello altri motivi di Hello rientrano in white paper tecnico piuttosto hello [code di Azure e code di Service Bus: confronto e Contrapposizioni](http://msdn.microsoft.com/library/azure/hh767287.aspx).  In molti scenari saranno valide entrambe le soluzioni.

**Scenari di coda**

Un utilizzo comune di code è oggi toolet di comunicare con un'istanza del ruolo di lavoro all'interno di un'istanza del ruolo web hello stessa applicazione di servizi Cloud.

Si supponga di creare un'applicazione Azure per la condivisione video. un'applicazione Hello è costituito da codice PHP in esecuzione in un ruolo web che consente agli utenti di caricare e video, insieme a un ruolo di lavoro implementati in c# che traduce caricati video in formati diversi.

Quando un'istanza del ruolo web Ottiene un nuovo video da un utente, è possibile archiviare video hello in un blob, quindi inviare un ruolo di lavoro tooa messaggio tramite una coda che indica la in cui questa nuova toofind video. It di istanza del ruolo di lavoro non ha importanza quale messaggio hello uno verrà quindi lettura dalla coda hello ed eseguire le traduzioni di video hello necessarie in background hello.

Strutturazione di un'applicazione in questo modo consente l'elaborazione asincrona e rende hello tooscale più semplice dell'applicazione, poiché il numero di hello di istanze del ruolo web e istanze del ruolo di lavoro può variare in modo indipendente. Inoltre, è possibile utilizzare la dimensione della coda hello come trigger tooscale hello diversi ruoli di lavoro su e giù. Se il valore è molto elevato vengono aggiunti altri ruoli. Quando ottiene inferiore, è possibile ridurre il numero di hello dell'esecuzione di ruoli toosave money.  

È possibile usare lo stesso criterio tra diverse parti dell'applicazione, anche se non usano ruoli Web e di lavoro.  Consente di parti di hello tooscale su entrambi i lati della coda di hello su e giù come richiesta e richiede il tempo di elaborazione.

### <a name="service-bus"></a>Bus di servizio
Se vengono eseguiti nel cloud hello, nel data center, in un dispositivo mobile o altrove, le applicazioni devono toointeract. obiettivo di Hello del Bus di servizio di Azure è toolet applicazioni che eseguono praticamente qualsiasi scambiano di dati.

In aggiunta toohello code (una) descritte in precedenza, Bus di servizio fornisce inoltre tooother metodi di comunicazione.

#### <a name="service-bus-relay"></a>Inoltro del bus di servizio
![Inoltro del bus di servizio di Azure](./media/fundamentals-introduction-to-azure/ServiceBusRelayIntroNew.png)

*Figura: l’inoltro del bus di servizio consente la comunicazione tra applicazioni su diversi lati di un firewall.*

Bus di servizio consente la comunicazione diretta tramite il servizio di inoltro, fornendo un toointeract in modo sicuro tramite i firewall. Inoltri del Bus di servizio per abilitare applicazioni toocommunicate lo scambio di messaggi tramite un endpoint ospitato nel cloud hello, anziché a livello locale.

**Scenari di Inoltro del bus di servizio**

Le applicazioni che comunicano tramite il bus di servizio possono essere applicazioni Azure o software in esecuzione in altre piattaforme cloud. Le applicazioni in esecuzione all'esterno di hello cloud, tuttavia possono anche essere. Un esempio potrebbe essere una compagnia aerea che implementa servizi di prenotazione in computer all'interno del proprio data center. airline Hello deve tooexpose questi client toomany servizi, incluso archiviazione chioschi aeroporti, i terminali di prenotazione agente e telefoni forse anche i clienti. Bus di servizio toodo potrebbe utilizzare questa operazione, la creazione di varie applicazioni loosely-coupled interazioni tra hello.

#### <a name="service-bus-topics-and-subscriptions"></a>Argomenti del bus di servizio e sottoscrizioni
![Argomenti del bus di servizio di Azure](./media/fundamentals-introduction-to-azure/ServiceBusTopicsSubsIntroNew.png)   
 *Figura: Argomenti di Service Bus consente più App toopost i messaggi e altre applicazioni toosubscribe tooreceive soddisfano criteri specifici.*

Bus di servizio fornisce un meccanismo di pubblicazione e sottoscrizione denominato Argomenti e sottoscrizioni. Con pubblicazione-sottoscrizione, un'applicazione può inviare l'argomento tooa messaggi, mentre altre applicazioni possono creare argomento toothis sottoscrizioni. Questo consente la comunicazione uno-a-molti tra un set di applicazioni, consentendo di hello stesso messaggio di essere letti da più destinatari.

**Argomenti del bus di servizio e scenari di sottoscrizione**

Ogni volta che si imposta in cui sono presenti molti messaggi che sono tutti importanti, ma per vari sistemi downstream toolisten toodiffering subset di tali comunicazioni, l'argomento del Bus di servizio e le sottoscrizioni sono un'ottima scelta.

### <a name="biztalk-services"></a>Servizi BizTalk
![Servizi BizTalk](./media/fundamentals-introduction-to-azure/BizTalkServicesIntroNew.png)   
 *Figura: Servizi BizTalk fornisce formati messaggi nel cloud hello hello possibilità tootransform XML.*

A volte è necessario connettere sistemi che comunicano usando formati di messaggistica diversi. È comune per gli schemi di database diverso toohave di business e XML messaggistica formati, anche quando è disponibile uno standard comune. Anziché scrivere la quantità di codice personalizzato, è possibile utilizzare diversi sistemi toointegrate locale di BizTalk Server.  Servizi BizTalk di Azure fornisce hello stesso tipo di servizio, ma nel cloud hello. È possibile pagare solo ciò che si utilizza e non preoccuparsi scala si dispone di tooon locale.

**Scenari di Servizi BizTalk**

Le interazioni business-to-business (B2B) in genere richiedono questo tipo di conversione.  Ad esempio, una società compilazione aerei esigenze tooorder parti da quest'ultimo è diversi fornitori di parti. numerosi fornitori.  Gli ordini devono essere automatizzato toogo direttamente dai sistemi di generatori di hello aereo nei sistemi di fornitori hello.  Nessuno dei due business desidera toochange sistemi core e i formati di messaggio, e si è molto improbabile che questi formati sono hello stesso. Servizi BizTalk può accettare i messaggi e la conversione tra i nuovi formati di hello in entrambe le direzioni. Entrambi fornitore aereo hello hello lavoro tootranslate o hello fornitori diversi possono, a seconda che richiede più controllo e hello della quantità di conversione necessaria.     

## <a name="compute-assistance"></a>Assistenza per il calcolo
Azure offre assistenza per i servizi che non richiedono toorun tutto il tempo hello.  

### <a name="scheduler"></a>Utilità di pianificazione
![Utilità di pianificazione di Azure](./media/fundamentals-introduction-to-azure/SchedulerIntroNew.png)   
*Figura: Dell'utilità di pianificazione di Azure offre un modo tooschedule processi in un momento specifico per un periodo di tempo specifico.*

In alcuni casi applicazioni sufficiente toorun in un determinato momento. In Azure, è possibile risparmiare con questo tipo di app anziché consentire a un'applicazione semplice mantenere esecuzione 24x7 in attesa di dati tooprocess. Pianificazione di Azure consente tooschedule quando un'applicazione deve essere eseguito in base a intervalli di tempo o un calendario. È affidabile e verificherà che un processo venga eseguito anche se sono presenti errori di rete, di computer e di data center. Utilizzare hello API REST dell'utilità di pianificazione toomanage queste azioni.

Quando si verifica un allarme pianificato, utilità di pianificazione Invia endpoint HTTP o HTTPS messaggi tooa specifico o può inserire un messaggio in una coda di archiviazione.  Pertanto è necessario toohave l'applicazione dispone di un endpoint accessibile o fare in modo che il monitoraggio di una coda di archiviazione. Una volta che ottiene il messaggio hello, quindi è possibile eseguire qualsiasi azione viene programmato per.

**Scenari dell'utilità di pianificazione**

* Azioni ricorrenti delle applicazioni: ad esempio, un servizio potrebbe periodicamente ottenere dati da twitter e raccogliere i dati di hello in un feed regolare.
* Manutenzione quotidiana: elaborazione o eliminazione dei registri, esecuzione di backup e altre attività di pianificazione eseguite a intermittenza.
* Attività eseguite di notte.
* Per le applicazioni Web come l'eliminazione giornaliera dei registri è necessario eseguire attività di manutenzione quotidiane, ad esempio l'esecuzione di backup e altre attività di manutenzione. L'amministratore potrà scegliere toobackup proprio database 1 ore ogni giorno per hello 9 mesi successivi, ad esempio.

Hello API dell'utilità di pianificazione consente toocreate, aggiornare, eliminare, visualizzare e gestire raccolte di processi e i processi pianificati a livello di codice.

## <a name="performance"></a>Prestazioni
Le prestazioni sono sempre importanti per un'applicazione. Le applicazioni tendono tooaccess hello ripetutamente stessi dati. Le prestazioni di tooimprove unidirezionale tookeep una copia di tale applicazione toohello più vicino di dati, la riduzione a icona hello tempo tooretrieve è. A questo scopo, Azure fornisce diversi servizi.

### <a name="azure-caching"></a>Servizio di memorizzazione nella cache di Azure
![Memorizzazione nella cache di Azure](./media/fundamentals-introduction-to-azure/AzureCacheIntroNew.png)   
 **Figura: un'applicazione Azure può memorizzare i dati nella cache e perfino suddividerli in numerosi ruoli di lavoro**

L'accesso ai dati archiviati nei servizi di gestione dati di Azure, ovvero database SQL, tabelle o BLOB, è molto veloce. Ma l'accesso ai dati archiviati in memoria è ancora più rapido. Di conseguenza, mantenere una copia in memoria dei dati utilizzati di frequente consente di migliorare le prestazioni delle applicazioni. È possibile utilizzare toodo di memorizzazione nella cache in memoria di Azure questo.

Un'applicazione di servizi Cloud è possibile archiviare i dati nella cache, quindi recuperare direttamente senza la necessità di tooaccess nell'archivio permanente. cache di Hello può essere gestita all'interno dell'applicazione di macchine virtuali o essere fornito dalle macchine virtuali dedicate esclusivamente toocaching. In entrambi i casi, può essere distribuita cache di hello, con dati hello contiene distribuito tra più macchine virtuali in un Data Center Azure.

Azure offre numerose tecnologie di cache che sono cambiate nel corso del tempo. In ordine di hello sono state introdotte, vi è condivisa, nel ruolo, gestito e cache Redis. la memorizzazione nella cache di Hello condivisa è una tecnologia meno recente e non creare nuove implementazioni con esso. Hello Cache gestita è hello stesse funzionalità delle hello nel ruolo nella cache, ma come servizio gestito all'esterno di hello portale di gestione di Azure. Cache Redis Hello è in anteprima. implementazione di Redis Hello con hello maggior numero di funzionalità ed è consigliata quando si scrive nuovo codice di memorizzazione nella cache.

**Scenari della Cache di Azure**

Un'applicazione che legge ripetutamente un catalogo prodotti potrà trarre vantaggio dall'utilizzo di questo tipo di memorizzazione nella cache, ad esempio, poiché i dati di hello deve sarà disponibile più rapidamente. tecnologia Hello supporta anche il blocco, consentendo di utilizzabile con lettura/scrittura, nonché dati di sola lettura. E applicazioni ASP.NET possono usare i dati della sessione toostore hello servizio con una modifica di configurazione.

### <a name="content-delivery-network"></a>Rete per la distribuzione di contenuti (CDN)
![Rete CDN di Azure](./media/fundamentals-introduction-to-azure/CDNIntroNew.png)   
 **Figura: Copie di un blob possono essere memorizzati nella cache in siti in tutto il mondo hello.**

Si supponga che è necessario che i dati blob toostore accessibili dagli utenti in tutto il mondo hello. Forse è un video di hello più recente mondiali corrispondenza, ad esempio, gli aggiornamenti di driver o un e-book più diffusi. Consente di archiviare una copia dei dati hello in più Data Center di Azure, ma se sono presenti un numero elevato di utenti, probabile che non è sufficiente. Per ottenere prestazioni migliori, è possibile utilizzare hello rete CDN di Azure.

Hello CDN dispone di numerosi siti mondo hello, in grado di archiviazione delle copie dei blob di Azure. Hello prima volta che un utente in una parte di hello world accede a un blob, hello informazioni che contiene vengono copiate da un Data Center di Azure nell'archiviazione locale di rete CDN in tale area geografica. Successivamente, gli accessi da parte di hello world utilizzerà la copia di blob hello memorizzati nella cache nella rete CDN hello-non devono toogo toohello tutte le modalità di hello più vicino al Data Center di Azure. Hello risulta più veloce toofrequently accessibili di accedere ai dati da parte degli utenti in qualsiasi punto della HelloWorld.

**Scenari di rete CDN**

È comune toouse CDN con video toodeliver di servizi multimediali in tutto il mondo. Un video è in genere di grandi dimensioni e richiede una notevole quantità di larghezza di banda.  Servizi media è citato in altre sezioni di questa pagina.

## <a name="big-data-and-big-compute"></a>Big Data e Big Compute
### <a name="hdinsight-hadoop"></a>HDInsight (Hadoop)
![HDInsight](./media/fundamentals-introduction-to-azure/HDInsightIntroNew.png)   
 **Figura: Consente di HDInsight con l'elaborazione bulk hello di enormi quantità di dati**

Per molti anni, è stata eseguita su dati relazionali archiviati in un data warehouse compilato con un DBMS relazionale bulk hello analisi dei dati. Questo tipo di analitica di business è comunque importante e sarà per un toocome molto tempo. Ma cosa accade se i dati di hello desiderati tooanalyze così grandi che i database relazionali appena non è possibile gestirlo? E non relazionali dati hello? ad esempio i log dei server in un data center oppure i dati cronologici relativi agli eventi di un sensore. In questi casi, si verifica un problema relativo ai Big Data. Occorre procedere con un approccio diverso.

la tecnologia dominante Hello oggi per analizzare i dati di grandi dimensioni è Hadoop. Un Apache progetto open source, questa tecnologia archivia i dati utilizzando hello Hadoop Distributed File System (HDFS), quindi consente agli sviluppatori di creare tooanalyze processi MapReduce che i dati. HDFS distribuisce i dati tra più server, quindi i blocchi di esecuzione del processo MapReduce hello su ciascuna di esse, consentendo di dati di grandi dimensioni hello essere elaborati in parallelo.

HDInsight è il nome di hello del servizio basato su Apache Hadoop hello di Azure. HDInsight consente di archiviare i dati in cluster hello e distribuirle tra più macchine virtuali HDFS. Anche hello logica di un processo MapReduce viene distribuita tra le macchine virtuali. Come con Hadoop in locale, i dati sono logica elaborato localmente, hello e dei dati di hello funziona su nella stessa macchina virtuale di hello- e in parallelo per migliorare le prestazioni. HDInsight consente inoltre di archiviare i dati nell'insieme di credenziali di Archiviazione di Azure che utilizza i BLOB.  Utilizzo ASV consente toosave money perché è possibile eliminare il cluster HDInsight quando non è in uso, ma mantenendo i dati nel cloud hello.

HDinsight supporta altri componenti dell'ecosistema di Hadoop hello, tra cui Hive e Pig. Microsoft ha creato i componenti che rendono più semplice toowork con dati prodotti da HDInsight utilizzando gli strumenti BI tradizionali, ad esempio adapter HiveODBC hello ed Esplora dati utilizzabili con Excel.

### <a name="high-performance-computing-big-compute"></a>High-Performance Computing (Big Compute)
Uno dei hello più interessanti modi toouse una piattaforma cloud è toorun elaborazione a elevate prestazioni (HPC) e altre applicazioni "Big Compute". Gli esempi includono specializzate toouse applicazioni compilate engineering hello standard del settore interfaccia MPI (Message Passing), nonché i cosiddette applicazioni imbarazzantemente parallele, i modelli di valutazione dei rischi finanziari.

le tracce di Hello di Big Compute sono l'esecuzione del codice su più computer in hello contemporaneamente. In Azure, questo significa che molte macchine virtuali in esecuzione contemporaneamente, tutti utilizzo toosolve parallelo di un problema. Questa operazione richiede alcune modo tooresources e tooschedule applicazioni, ad esempio, toodistribute il lavoro tra le istanze. Pacchetto HPC gratuito di Microsoft e altre soluzioni di cluster di calcolo possono eseguire anche in Azure, sfruttando di calcolo e l'infrastruttura servizi di Azure tooadd capacità su richiesta tooan locale cluster di calcolo o eseguire applicazioni Big Compute interamente in hello cloud.

Azure offre un intervallo di macchina virtuale di dimensioni di istanza con configurazioni diverse di core CPU, memoria, capacità del disco e altri requisiti di hello toomeet caratteristiche delle diverse applicazioni. Hello A8 introdotto di recente e lavoro istanze A9 anche per molti calcolo intensivo carichi di lavoro e le applicazioni MPI parallele, in particolare, poiché sono caratterizzate da CPU multicore, grandi quantità di memoria e velocità elevata. In determinate configurazioni di istanze di hello usufruire di una rete a bassa latenza e velocità effettiva elevata dell'applicazione nel cloud hello che include la tecnologia di diretto a memoria remota (RDMA) di accesso per la massima efficienza delle applicazioni MPI parallele.

Azure offre inoltre a sviluppatori e partner delle applicazioni Big Compute un set completo di funzionalità di calcolo, servizi, scelte di architettura e strumenti di sviluppo. Azure supporta Big Compute flussi di lavoro personalizzati che includono flussi di lavoro di dati specializzati e processi e delle attività di programmazione di modelli che possono essere ridimensionati toothousands di core di calcolo.

## <a name="media"></a>Contenuti multimediali
![Servizi multimediali di Azure](./media/fundamentals-introduction-to-azure/MediaServicesIntroNew.png)   
 **Figura: Media Services è una piattaforma per le applicazioni che forniscono i video e altri supporti tooclients tutto il mondo hello.**

I video costituiscono gran parte del traffico Internet attuale e questa percentuale è destinata ad aumentare in futuro. Ancora fornendo video sul web hello non è semplice. Un numero elevato di variabili, ad esempio hello codifica algoritmo e hello risoluzione dello schermo dell'utente hello di visualizzazione. Video tende anche toohave picchi nella domanda, ad esempio un picco di sabato quando un numero elevato di utenti decide che preferiscono toowatch un filmato online.

È probabile che i video saranno inclusi in molte delle nuove applicazioni create. Ancora tutte sarà necessario toosolve alcune di hello stessi problemi e rendendo ognuno risolvere questi problemi autonomamente non ha senso. Un approccio migliore è una piattaforma che fornisce soluzioni comuni per molte applicazioni toouse toocreate. E la creazione di questa piattaforma cloud hello presenta alcuni vantaggi deselezionare. Può essere reso disponibile con cadenza pagamento a consumo e può anche gestire variabilità hello della richiesta di applicazioni video spesso trovano ad affrontare.

Servizi multimediali di Azure consente di risolvere questo problema. Offre un set di componenti cloud per semplificare le attività di coloro che creano ed eseguono applicazioni che utilizzano video e altri elementi multimediali.

Come mostrato nella figura hello, servizi multimediali fornisce un set di componenti per le applicazioni che funzionano con video e altre risorse multimediali. Ad esempio, include un supporto di acquisizione video tooupload component in servizi multimediali (in cui archiviato nei blob di Azure), un componente di codifica che supporta vari formati di audio e video, un componente di protezione del contenuto che fornisce gestione dei diritti digitali, un componente per l'inserimento di annunci in un flusso video, i componenti per lo streaming e altro ancora. Partner Microsoft possono anche fornire i componenti per la piattaforma di hello, quindi distribuire tali componenti e della fatturazione per loro conto dispone di Microsoft.

Le applicazioni che utilizzano questa piattaforma possono essere eseguite in Azure o altrove. Ad esempio, un'applicazione desktop per un centro di produzione potrebbe consentire agli utenti caricare servizi tooMedia video, quindi elaborarlo in vari modi. In alternativa, un servizio di gestione del contenuto basato su cloud in esecuzione in Azure potrebbe essere si basano su servizi multimediali tooprocess e distribuire il video. Quando viene eseguito e qualsiasi caso, ogni applicazione sceglie i componenti necessari toouse, accesso tramite le interfacce RESTful.

toodistribute cosa produce, un'applicazione può utilizzare hello rete CDN di Azure, un'altra rete CDN, o appena inviato direttamente bit toousers. Indipendentemente dal modo in cui vengono caricati, i video creati tramite Servizi multimediali possono essere utilizzati da vari sistemi client, tra cui Windows, Macintosh, HTML 5, iOS, Android, Windows Phone, Flash e Silverlight. obiettivo di Hello è toomake è più semplice di applicazioni moderne multimediali di toocreate.

**Riferimenti**

Per una visualizzazione più visiva del funzionamento di servizi multimediali, scaricare hello [servizi multimediali di Azure][Azure Media Services Poster].

## <a name="commerce"></a>E-commerce
aumento della Hello del Software come un servizio è la trasformazione è creazione di applicazioni. e anche il modo in cui queste vengono vendute. Poiché un'applicazione SaaS si trova nel cloud hello, è opportuno che i clienti potenziali devono cercare soluzioni in linea. E questa modifica si applica toodata nonché tooapplications. Perché non devono persone hanno aspetto toohello cloud per i set di dati disponibili in commercio? Microsoft è destinato a entrambi questi problemi con hello [Azure Marketplace](https://azure.microsoft.com/marketplace/).

![E-commerce di Azure](./media/fundamentals-introduction-to-azure/CommerceIntroNew.png)   
 **Figura: Azure Marketplace e Azure Store consentono di trovare e acquistare applicazioni e set di dati commerciali Azure e di usarli come parte delle applicazioni Azure.**

Hello differenza tra due hello è che Marketplace è di fuori di hello portale di gestione di Azure, ma può accedere all'archivio hello all'interno di hello portale. I clienti potenziali possono trovare toofind Azure applicazioni le proprie esigenze. I clienti possono cercare set di dati commerciali, ad esempio dati demografici, dati finanziari, dati geografici e così via. Quando è disponibile un elemento che desiderano, possono accedere, dal fornitore hello, direttamente tramite hello Marketplace o percorsi di archivio web o in alcuni casi dal portale di gestione di hello. Le applicazioni è inoltre possono utilizzare hello API ricerca Bing tramite hello Marketplace, concedere loro accesso toohello risultati delle ricerche di web.

**Scenari di e-commerce**

SendGrid è un'applicazione in Azure Store che consente di posta elettronica toosend hello. Offre funzionalità aggiuntive come la consegna affidabile e statistiche.  È possibile acquistare l'applicazione e i servizi correlati piuttosto che provare toobuild tale infrastruttura.  

## <a name="getting-started"></a>Introduzione
Dopo aver creato passaggio successivo di hello visione, hello toowrite è un'applicazione Azure. Scegliere la lingua, [ottenere hello SDK appropriato](/downloads/)e passare per il. Cloud computing è hello nuovo valore predefinito--per iniziare.

[Azure Media Services Poster]: http://azure.microsoft.com/documentation/infographics/media-services/
