---
title: aaaUsing tooand dati tootransfer di importazione/esportazione di Azure dall'archiviazione blob | Documenti Microsoft
description: Informazioni su come toocreate importare ed esportare i processi nel portale di Azure per il trasferimento di dati tooand dall'archiviazione blob hello.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 668f53f2-f5a4-48b5-9369-88ec5ea05eb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: muralikk
ms.openlocfilehash: 0be486a4badf2127b4613f3e9664e4cd308d3298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-microsoft-azure-importexport-service-tootransfer-data-tooblob-storage"></a>Utilizzare l'archiviazione di hello importazione/esportazione di Microsoft Azure service tootransfer dati tooblob
servizio di importazione/esportazione di Azure Hello consente toosecurely trasferiscono grandi quantità di spazio di archiviazione di blob tooAzure dati da shipping unità disco rigido tooan data center di Azure. È inoltre possibile utilizzare questi dati tootransfer servizio dalle unità disco toohard di archiviazione blob di Azure e spedire tooyour nel sito locale. Questo servizio è adatto in situazioni in cui si desidera tootransfer diversi terabyte (TB) di dati tooor da Azure, ma il caricamento o download tramite rete hello è applicabile a causa della larghezza di banda toolimited o alto i costi di rete.

servizio Hello richiede che l'unità disco rigido deve essere crittografato per la sicurezza hello dei dati con BitLocker. servizio Hello supporta entrambi hello classico e Gestione risorse di Azure gli account di archiviazione (livello standard e sporadico) presenti in tutte le aree di hello di Azure pubblico. È necessario spedire le unità disco rigido tooone dei percorsi di hello supportato specificati più avanti in questo articolo.

In questo articolo altre informazioni sul servizio di importazione/esportazione di Azure hello e come tooship unità per la copia tooand i dati dall'archiviazione Blob di Azure.

## <a name="when-should-i-use-hello-azure-importexport-service"></a>Quando è consigliabile utilizzare il servizio di importazione/esportazione di Azure hello?
È consigliabile utilizzare il servizio di importazione/esportazione di Azure durante il caricamento o il download dei dati in rete hello è troppo lenta o della larghezza di banda di rete aggiuntiva è e dispendioso.

Il servizio può essere usato in scenari simili ai seguenti:

* La migrazione dei dati nel cloud toohello: spostare rapidamente grandi quantità di dati tooAzure e a costi contenuti.
* La distribuzione del contenuto: inviare rapidamente dati tooyour siti dei clienti.
* Backup: Effettuare il backup del toostore dati locale nell'archiviazione blob di Azure.
* Ripristino dei dati: recuperare grandi quantità di dati archiviati nell'archiviazione blob e hanno la sede locale tooyour di consegna.

## <a name="prerequisites"></a>Prerequisiti
In questa sezione sono elencati hello prerequisiti necessari toouse questo servizio. Si consiglia di esaminarli attentamente prima di spedire le unità.

### <a name="storage-account"></a>Account di archiviazione
È necessario disporre di una sottoscrizione di Azure esistente e uno o più account toouse hello importazione/esportazione di servizio di archiviazione. Ogni processo può essere utilizzato tootransfer tooor di dati da un solo account di archiviazione. In altre parole, un singolo processo di importazione/esportazione non può estendersi su più account di archiviazione. Per informazioni sulla creazione di un nuovo account di archiviazione, vedere [come un Account di archiviazione tooCreate](storage-create-storage-account.md#create-a-storage-account).

### <a name="blob-types"></a>Tipi di BLOB
È possibile utilizzare anche i dati di importazione/esportazione di Azure del servizio toocopy**blocco** BLOB o **pagina** BLOB. Al contrario, usando questo servizio è possibile esportare solo BLOB in **blocchi**, BLOB di **pagine** o BLOB di **aggiunta** da Archiviazione di Azure.

### <a name="job"></a>Job
processo di hello toobegin di importazione tooor esportazione dall'archiviazione Blob, creare innanzitutto un processo. che potrà essere un processo di importazione o un processo di esportazione:

* Creare un processo di importazione se si desidera dati tootransfer tooblobs locale sono presenti account di archiviazione Azure.
* Creare un processo di esportazione quando si desidera tootransfer dati attualmente archiviati come BLOB nelle unità toohard account di archiviazione che vengono spediti tooyou.s quando si crea un processo, è notificare hello importazione/esportazione di servizio che si spedirà uno o più dischi rigidi tooan Azure centro dati.

* Per un processo di importazione, si spediranno dischi rigidi contenenti i dati.
* Per un processo di esportazione, si spediranno dischi rigidi vuoti.
* Spedire i dischi rigidi too10 per processo.

È possibile creare un'importazione o esportazione processo utilizzando il portale di Azure hello o hello [API REST di importazione/esportazione di archiviazione di Azure](/rest/api/storageimportexport).

### <a name="waimportexport-tool"></a>Strumento WAImportExport
Hello primo passaggio per la creazione di un **importare** processo è tooprepare le unità che verranno inviate per l'importazione. tooprepare le unità, è necessario connettersi server locale tooa e hello esecuzione dello strumento WAImportExport nel server locale hello. Questo strumento WAImportExport facilita la copia unità toohello dati, la crittografia dei dati hello hello unità con BitLocker e generazione di file journal di unità hello.

file journal Hello archiviano informazioni di base del processo e l'unità, ad esempio il numero di serie di unità e il nome di account di archiviazione. Questo file di registrazione non viene archiviato nell'unità di hello. Viene usato durante la creazione del processo di importazione. La procedura dettagliata sulla creazione dei processi è riportata più avanti in questo articolo.

lo strumento WAImportExport Hello è compatibile solo con sistema operativo di Windows a 64 bit. Vedere hello [del sistema operativo](#operating-system) sezione per specifiche versioni del sistema operativo supportato.

Scaricare una versione più recente di hello di hello [strumento WAImportExport](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExportV2.zip). Per ulteriori informazioni sull'utilizzo hello strumento WAImportExport, vedere hello [hello tramite lo strumento WAImportExport](storage-import-export-tool-how-to.md).

>[!NOTE]
>**La versione precedente:** è possibile [scaricare WAImportExpot V1](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip) versione di hello strumento e fare riferimento troppo[Guida di utilizzo di WAImportExpot V1](storage-import-export-tool-how-to-v1.md). La versione WAImportExpot V1 dello strumento hello forniscono supporto per **preparazione dei dischi, i dati pre-già scritti su disco toohello**. È necessario anche toouse WAImportExpot V1 strumento se hello solo chiave disponibili chiave SAS.

>

### <a name="hard-disk-drives"></a>Unità disco rigido
Per l'utilizzo con servizio di importazione/esportazione hello sono supportati solo da 2,5 pollici unità SSD o 2,5" o 3,5" SATA II o unità disco rigido interno III. Un singolo processo di importazione/esportazione può interessare un massimo di 10 unità disco rigido o SSD e ogni unità disco rigido o SSD può avere qualsiasi dimensione. Numero elevato di unità distribuibili tra più processi ed non è disponibile alcun limite sul numero di hello dei processi che possono essere creati. 

Per i processi di importazione, verrà elaborati solo hello primo volume di dati nell'unità di hello. volume di dati Hello deve essere formattato con NTFS.

> [!IMPORTANT]
> Questo servizio non supporta i dischi rigidi esterni dotati di un adattatore USB incorporato. Inoltre, non è possibile utilizzare il disco di hello all'interno di maiuscole e minuscole hello di un disco rigido esterno; non inviare unità disco rigido esterno.
> 
> 

Di seguito è che un elenco degli adattatori USB esterni utilizzati toocopy dati toointernal HDD. Anker 68UPSATAA - 02BU Anker 68UPSHHDS BU Startech SATADOCK22UE Orico 6628SUS3-C-BK (serie 6628) Alloggiamento di espansione dell'unità rigida esterna Thermaltake BlacX Hot Swap SATA (USB 2.0 ed eSATA)

### <a name="encryption"></a>Crittografia
dati Hello in unità hello devono essere crittografati con crittografia unità BitLocker. che protegge i dati mentre sono in transito.

Per i processi di importazione, sono disponibili due crittografia hello tooperform di modi. primo modo Hello è toospecify hello quando si utilizzano file CSV di set di dati durante l'esecuzione dello strumento WAImportExport hello durante la preparazione dell'unità. Hello secondo metodo è tooenable crittografia unità BitLocker manualmente unità hello e specificare la chiave di crittografia hello in hello driveset CSV durante l'esecuzione riga di comando dello strumento WAImportExport durante la preparazione dell'unità.

Per i processi di esportazione dopo i dati vengono copiati toohello unità, servizio hello crittograferà unità hello con BitLocker prima di distribuirlo tooyou indietro. chiave di crittografia Hello verrà fornito tooyou tramite hello portale di Azure.  

### <a name="operating-system"></a>Sistema operativo
È possibile utilizzare uno dei seguenti a 64 bit i sistemi operativi tooprepare hello disco rigido utilizzando hello strumento WAImportExport prima di consegnare hello unità tooAzure hello:

Windows 7 Enterprise, Windows 7 Ultimate, Windows 8 Pro, Windows 8 Enterprise, Windows 8.1 Pro, Windows 8.1 Enterprise, Windows 10<sup>1</sup>, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2. Tutti questi sistemi operativi supportano la funzionalità Crittografia unità BitLocker.

### <a name="locations"></a>Località
Hello servizio importazione/esportazione di Azure supporta la copia tooand dati da tutti gli account di archiviazione di Azure pubblico. È possibile fornire tooone unità disco rigido di hello posizioni seguenti. Se l'account di archiviazione in una posizione pubblica di Azure che non viene specificata in questo caso, verrà fornito durante la creazione di un'ubicazione di spedizione alternativo hello processo tramite hello portale di Azure o hello API REST di importazione/esportazione.

Località di spedizione supportate:

* Stati Uniti Orientali
* Stati Uniti occidentali
* Stati Uniti orientali 2
* Stati Uniti occidentali 2
* Stati Uniti centrali
* Stati Uniti centro-settentrionali
* Stati Uniti centro-meridionali
* Stati Uniti centro-occidentali
* Europa settentrionale
* Europa occidentale
* Asia orientale
* Asia sudorientale
* Australia orientale
* Australia sudorientale
* Giappone occidentale
* Giappone orientale
* India centrale
* India meridionale
* India occidentale
* Canada centrale
* Canada orientale
* Brasile meridionale
* Corea centrale
* US Gov Virginia
* Governo degli Stati Uniti - Iowa
* Dipartimento della difesa Stati Uniti orientali
* Dipartimento della difesa Stati Uniti centrali
* Cina orientale
* Cina settentrionale
* Regno Unito meridionale

### <a name="shipping"></a>Spedizione
**Spedizione unità toohello datacenter:**

Quando si crea un processo di importazione o esportazione, verrà fornito che un indirizzo di spedizione di uno di hello supportati percorsi tooship le unità. Hello indirizzo fornito per la spedizione verrà dipendono dalla posizione hello dell'account di archiviazione, ma potrebbe non essere hello stesso come il percorso di account di archiviazione.

È possibile utilizzare i vettori come FedEx, DHL, gruppo di continuità o hello US Postal Service tooship toohello l'unità indirizzo di spedizione.

**Unità di spedizione dal centro dati hello:**

Quando si crea un processo di importazione o esportazione, è necessario fornire un indirizzo del mittente per Microsoft toouse quando shipping hello unità esegue il backup al termine del processo. Assicurarsi di che fornire un indirizzo valido restituito tooavoid ritardi nell'elaborazione.

È possibile utilizzare un vettore di propria scelta nel disco rigido di ordine tooforward ship hello. vettore Hello deve disporre di rilevamento appropriato nella catena di toomaintain di ordine di custodia. È necessario fornire anche un vettore FedEx o DHL valido toobe numero di account utilizzato da Microsoft per la spedizione hello unità nuovamente. Un numero di account FedEx è obbligatorio per la spedizione delle unità da hello Stati Uniti e ubicazioni in Europa. Per la restituzione di unità da località in Asia e in Australia è necessario un numero di account DHL. Se non è già disponibile, è possibile creare un account del vettore [FedEx](http://www.fedex.com/us/oadr/), per Stati Uniti ed Europa o [DHL](http://www.dhl.com/), per Asia e Australia. Se si dispone già di un numero di account vettore, verificare che sia valido.

I pacchetti di spedizione, è necessario seguire termini hello [condizioni di servizio di Microsoft Azure](https://azure.microsoft.com/support/legal/services-terms/).

> [!IMPORTANT]
> Si noti che i supporti fisici hello che si potrebbero essere necessario toocross internazionali bordi. Si è responsabile di garantire che i supporti fisici e i dati vengono importati e/o esportati in base alle leggi applicabili in materia hello. Prima di consegnare supporti fisici hello, controllare con tooverify i consulenti che i supporti e i dati possono essere legalmente toohello spediti identificato data center. Ciò consentirà di tooensure raggiunge Microsoft in modo tempestivo. Ad esempio, i pacchetti che si intersecano i confini internazionali deve toobe una fattura commerciale accompagnato dal pacchetto hello (tranne se oltrepassare i bordi all'interno dell'Unione europea). È possibile stampare una copia piena fattura commerciale di hello dal sito Web di vettore. Esempi di fattura commerciale sono [fattura commerciale DHL](http://invoice-template.com/wp-content/uploads/dhl-commercial-invoice-template.pdf) e [fattura commerciale FedEx](http://images.fedex.com/downloads/shared/shipdocuments/blankforms/commercialinvoice.pdf). Assicurarsi che Microsoft non è stato indicato come utilità di esportazione hello.
> 
> 

## <a name="how-does-hello-azure-importexport-service-work"></a>Come funziona il servizio di importazione/esportazione di Azure hello?
È possibile trasferire dati tra il sito locale e l'archiviazione blob di Azure tramite il servizio di importazione/esportazione di Azure hello la creazione di processi e la spedizione delle unità disco rigido tooan data center di Azure. Ogni unità disco rigido spedita è associata a un singolo processo. Ogni processo è associato a un singolo account di archiviazione. Hello revisione [sezione Prerequisiti](#pre-requisites) attentamente toolearn sulle specifiche di hello di questo servizio, ad esempio supportato blob tipi, tipi di disco, percorsi e spedizione.

In questa sezione è descrivere in un hello di livello elevato passaggi della procedura di importazione e i processi di esportazione. Più avanti in hello [sezione introduttiva](#quick-start), si forniscono istruzioni dettagliate toocreate un'importazione e processo di esportazione.

### <a name="inside-an-import-job"></a>Analisi di un processo di importazione
In generale, un processo di importazione prevede hello alla procedura seguente:

* Determinare hello toobe di dati importati e hello numero di unità, che sarà necessario.
* Identificare hello blob posizione di destinazione dei dati nell'archiviazione Blob.
* Utilizzare lo strumento WAImportExport toocopy hello tooone i dati o altre unità disco rigido e crittografati con BitLocker.
* Creare un processo di importazione nell'account di archiviazione di destinazione utilizzando hello portale di Azure o hello API REST di importazione/esportazione. Se si utilizza hello portale di Azure, caricare il file journal dell'unità di hello.
* Specificare indirizzo hello e numero toobe account vettore usato per hello unità indietro tooyou di spedizione.
* L'indirizzo fornito durante la creazione del processo di spedizione toohello unità disco rigido hello di spedizione.
* Aggiornare il recapito di hello nei dettagli processo di importazione hello numero di tracciabilità e inviare il processo di importazione hello.
* Unità vengono ricevute ed elaborate in hello data center di Azure.
* Le unità vengono fornite tramite il vettore account toohello indirizzo mittente fornito nel processo di importazione hello.
  
    ![Figura 1: importazione del flusso di processo](./media/storage-import-export-service/importjob.png)

### <a name="inside-an-export-job"></a>Analisi di un processo di esportazione
In generale, un processo di esportazione comporta hello alla procedura seguente:

* Determinare hello dati toobe esportato e numero di unità, che sarà necessario hello.
* Identificare i BLOB di origine hello o i percorsi di contenitore dei dati nell'archiviazione Blob.
* Creare un processo di esportazione nell'account di archiviazione di origine utilizzando hello portale di Azure o hello API REST di importazione/esportazione.
* Specificare hello BLOB di origine o il processo di esportazione i percorsi di contenitore dei dati in hello.
* Numero account indirizzo e la gestione delle spedizioni restituito hello per toobe utilizzate della spedizione hello unità indietro tooyou fornito.
* L'indirizzo fornito durante la creazione del processo di spedizione toohello unità disco rigido hello di spedizione.
* Aggiornare il recapito di hello nei dettagli processo di esportazione hello numero di tracciabilità e inviare il processo di esportazione hello.
* unità Hello vengono ricevute ed elaborate in hello data center di Azure.
* Hello unità crittografate con BitLocker. Hello chiavi sono disponibili tramite hello portale di Azure.  
* unità Hello vengono fornite tramite il vettore account toohello indirizzo mittente fornito nel processo di importazione hello.
  
    ![Figura 2: esportazione del flusso di processo](./media/storage-import-export-service/exportjob.png)

### <a name="viewing-your-job-and-drive-status"></a>Visualizzazione dello stato dei processi e delle unità
È possibile tenere traccia dello stato di hello dell'importazione o i processi di esportazione da hello portale di Azure. Fare clic su hello **importazione/esportazione** scheda. Nella pagina hello verrà visualizzato un elenco dei processi.

![Visualizzare lo stato dei processi](./media/storage-import-export-service/jobstate.png)

Verrà visualizzato uno dei seguenti stati dei processi in base alla posizione nell'unità nel processo di hello hello.

| Stato processo | Descrizione |
|:--- |:--- |
| Creating | Dopo aver creato un processo, lo stato viene impostato tooCreating. Mentre il processo di hello è in stato di creazione di hello, hello servizio importazione/esportazione presuppone hello unità non sono stati spediti toohello datacenter. Un processo può rimanere in stato di creazione hello per le settimane tootwo, dopo il quale viene eliminato automaticamente dal servizio hello. |
| Spedizione | Dopo aver inviato il pacchetto, è necessario aggiornare hello registrando informazioni di hello portale di Azure.  Questo si trasformerà il processo di hello in "Shipping". processo Hello rimarrà in stato di spedizione hello per le settimane tootwo. 
| Ricevuto | Dopo la ricezione di tutte le unità al data center di hello, verrà impostato lo stato del processo hello toohello ricevuti. |
| Transferring | Dopo l'avvio dell'elaborazione per almeno un'unità, verrà impostato lo stato del processo hello toohello trasferimento. Vedere Stati delle unità hello sezione riportata di seguito per informazioni dettagliate. |
| Packaging | Una volta completata l'elaborazione di tutte le unità, hello processo verrà impostato nello stato di creazione di pacchetti hello fino a quando non hello unità spedita tooyou indietro. |
| Completed | Dopo che tutte le unità sono stati spediti toohello indietro cliente, se il processo di hello è stata completata senza errori, quindi hello processo verrà impostato toohello nello stato completato. Hello processo verrà automaticamente eliminato dopo 90 giorni in hello nello stato completato. |
| Chiuso | Dopo che tutte le unità sono stati spediti toohello indietro cliente, se sono state apportate eventuali errori durante l'elaborazione di hello del processo di hello, quindi hello processo verrà impostato lo stato chiuso toohello. Hello processo verrà automaticamente eliminato dopo 90 giorni in stato di chiusura hello. |

tabella Hello riportata di seguito descrive hello del ciclo di vita di una singola unità durante la transizione a un processo di importazione o esportazione. stato corrente di Hello di ogni unità in un processo è ora visibile da hello portale di Azure.
Hello nella tabella seguente viene descritto ogni stato di ogni unità in un processo può attraversare.

| Stato dell'unità | Descrizione |
|:--- |:--- |
| Specificata | Per un processo di importazione, quando viene creato il processo di hello dal portale di Azure hello hello iniziale stato per un'unità è hello specificato. Per un processo di esportazione, poiché viene specificata alcuna unità quando viene creato il processo di hello, stato iniziale dell'unità hello è stato ricevuto hello. |
| Ricevuto | unità Hello passa stato Received toohello quando l'operatore del servizio di importazione/esportazione hello ha elaborato le unità ricevute dalla società per un processo di importazione di spedizione hello hello. Per un processo di esportazione, lo stato iniziale dell'unità di hello è stato ricevuto hello. |
| MaiRicevuta | unità di Hello sposta lo stato di NeverReceived toohello quando hello pacchetto per un processo raggiunge, ma il pacchetto di hello non contiene unità hello. Un'unità può inoltre passare a questo stato se sono trascorsi due settimane dal servizio hello ha ricevuto le informazioni di spedizione hello, ma il pacchetto di hello non è ancora arrivato al data center di hello. |
| Transferring | Un'unità passerà stato trasferimento toohello quando il servizio hello inizia tootransfer dati hello tooWindows di unità di archiviazione di Azure. |
| Completed | Quando il servizio hello ha trasferito tutti i dati di hello senza errori, un'unità passerà toohello nello stato completato.
| CompletataPiùInformazioni | Un'unità passerà toohello CompletedMoreInfo stato quando hello servizio ha rilevato alcuni problemi durante la copia dei dati da o toohello unità. Hello informazioni possono includere errori, avvisi o messaggi informativi su sovrascrittura dei BLOB.
| Rispedita | unità di Hello Sposta toohello ShippedBack stato quando è stato spedito dall'indirizzo mittente toohello hello data center back. |

Questa immagine dal portale di Azure hello Visualizza lo stato di unità hello di un processo di esempio:

![Visualizza stato dell'unità](./media/storage-import-export-service/drivestate.png)

Hello nella tabella seguente vengono descritti gli stati di errore dell'unità di hello e hello azioni eseguite per ogni stato.

| Stato dell'unità | Evento | Risoluzione/Passaggio successivo |
|:--- |:--- |:--- |
| MaiRicevuta | Un'unità che è contrassegnata come NeverReceived (perché non è stato ricevuto come parte della spedizione del processo di hello) arriva in un'altra spedizione. | team addetto alle operazioni Hello sposterà hello unità toohello stato Received. |
| N/D | Un'unità che non fa parte di qualsiasi processo arriva al centro dati hello come parte di un altro processo. | unità di Hello verrà contrassegnata come aggiuntiva e verrà restituito toohello cliente quando viene completato il processo di hello associato al pacchetto originale hello. |

### <a name="time-tooprocess-job"></a>Processo tooprocess timer
quantità Hello tempo tooprocess un processo di importazione/esportazione varia a seconda di diversi fattori, ad esempio il tempo di spedizione, tipo di processo, di tipo e le dimensioni di hello dati copiati e hello dimensione dei dischi hello fornito. Hello servizio importazione/esportazione non dispone di un contratto di servizio, ma dopo la ricezione di dischi hello servizio hello cercando toocomplete hello copia in 7 giorni too10. È possibile utilizzare lo stato del processo hello API REST tootrack hello più da vicino. È una percentuale completa del parametro nell'operazione di elencare i processi che fornisce un'indicazione dello stato di avanzamento copia hello. Raggiungere toous se è necessario un toocomplete stima un processo di importazione/esportazione critici ora.

### <a name="pricing"></a>Prezzi
**Tariffa di gestione delle unità**

Esiste una tariffa di gestione per ogni unità elaborata come parte del processo di importazione o esportazione. Visualizzare i dettagli di hello in hello [prezzi di importazione/esportazione di Azure](https://azure.microsoft.com/pricing/details/storage-import-export/).

**Costi di spedizione**

Quando si effettua la spedizione tooAzure unità, si paga hello vettore toohello costo di spedizione. Quando Microsoft restituisce hello unità tooyou, hello le spese di spedizione viene addebitato conto vettore toohello fornite in fase di creazione del processo di hello.

**Costi di transazione**

Non ci sono costi di transazione quando si importano dati nell'archiviazione BLOB. costi di uscita standard di Hello sono applicabili quando si esportano dati dall'archiviazione blob. Per altre informazioni sui costi della transazione, vedere [Dettagli prezzi dei trasferimenti di dati.](https://azure.microsoft.com/pricing/details/data-transfers/)

## <a name="quick-start"></a>Avvio rapido
Questa sezione fornisce istruzioni dettagliate per la creazione di un processo di importazione ed esportazione. Verificare che sia conforme a tutti di hello [prerequisiti](#pre-requisites) prima di procedere.

> [!IMPORTANT]
> servizio Hello supporta un account di archiviazione standard per importare o esportare processo e non supporta gli account di archiviazione premium. 
> 
> 
## <a name="create-an-import-job"></a>Creare un processo di importazione
Creare un tooyour di dati toocopy processo importazione account di archiviazione di Azure da dischi rigidi da uno o più unità contenenti i data center di dati specificato toohello di spedizione. processo di importazione Hello fornisce dettagli sulle unità disco rigido, copia dati toobe, account di archiviazione di destinazione e il servizio di importazione/esportazione di Azure toohello informazioni di spedizione. La creazione di un processo di importazione è un processo in tre fasi. Preparare le unità utilizzando lo strumento WAImportExport hello. In secondo luogo, inviare un processo di importazione utilizzando hello portale di Azure. In terzo luogo, spedire hello unità toohello indirizzo fornito durante hello processo creazione e all'aggiornamento, informazioni sulla spedizione nei dettagli del processo di spedizione.   

### <a name="prepare-your-drives"></a>Preparare le unità
Hello primo passaggio durante l'importazione di dati tramite il servizio di importazione/esportazione di Azure hello è tooprepare le unità utilizzando lo strumento WAImportExport hello. Eseguire operazioni di hello seguenti tooprepare le unità.

1. Identificare hello toobe di dati importati. Potrebbe trattarsi di directory e file autonomi nel server locale hello o una condivisione di rete.  
2. Determinare il numero di hello di unità, che sarà necessario a seconda della dimensione totale dei dati di hello. Ottenere hello richiesto numero di unità SSD da 2,5 pollici 2,5" o 3,5" dischi rigidi SATA II o III.
3. Identificare l'account di archiviazione di destinazione hello, contenitore, directory virtuali e BLOB.
4.  Determinare la directory hello e/o i file autonomi che saranno copiato tooeach unità disco rigido.
5.  Creazione di file CSV per set di dati e driveset hello.
    
    **File CSV del set di dati**
    
    Di seguito è riportato un esempio di file CSV del set di dati:
    
    ```
    BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
    "F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
    "F:\50M_original\","containername/",BlockBlob,rename,"None",None 
    ```
   
    In hello sopra riportato, 100M_1.csv.txt saranno copiati toohello radice del contenitore di hello denominato "containername". Se il nome di contenitore hello "containername" non esiste, verrà creato uno. Tutti i file e cartelle in 50M_original sarà toocontainername in modo ricorsivo copiato. La struttura delle cartelle verrà mantenuta.

    Altre informazioni, vedere [preparazione file CSV di set di dati hello](storage-import-export-tool-preparing-hard-drives-import.md#prepare-the-dataset-csv-file).
    
    **Tenere presente**: per impostazione predefinita, verranno importati i dati di hello come BLOB in blocchi. È possibile utilizzare i dati di campo valore tooimport BlobType hello come un BLOB di pagine. Ad esempio, se si importano file di dischi rigidi virtuali che verranno montati come dischi in una VM di Azure, è necessario importarli come BLOB di pagine.

    **File CSV del driveset**

    valore Hello driveset hello flag è viene eseguito il mapping di un file CSV che contiene l'elenco di hello dischi toowhich hello lettere di unità affinché hello strumento toocorrectly selezionare elenco hello di dischi toobe preparato. 

    Di seguito è riportato hello del file CSV driveset:
    
    ```
    DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
    G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
    H,Format,SilentMode,Encrypt,
    ```

    In hello esempio precedente, si presuppone che i due dischi collegati e base volumi NTFS con lettera di volume G:\ e H:\ sono stati creati. strumento Hello formato e disco hello che ospita H:\ e non formattare o crittografare disco hello hosting volume G:\ crittografare.

    Altre informazioni, vedere [preparazione file CSV di hello driveset](storage-import-export-tool-preparing-hard-drives-import.md#prepare-initialdriveset-or-additionaldriveset-csv-file).

6.  Hello utilizzare [strumento WAImportExport](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip) toocopy tooone i dati o più dischi rigidi.
7.  È possibile specificare "Encrypt" nel campo crittografia drivset CSV tooenable crittografia unità BitLocker hello unità disco rigido. In alternativa, è possibile anche attivare BitLocker manualmente nel disco rigido di hello e specificare "AlreadyEncrypted" e immettere chiave hello hello driveset CSV durante l'esecuzione dello strumento hello.

8. Non modificare i dati di hello hello unità disco o file journal hello dopo aver completato la preparazione del disco.

> [!IMPORTANT]
> Ogni unità disco rigido preparata darà luogo a un file journal. Quando si crea il processo di importazione hello utilizzando hello portale di Azure, è necessario caricare tutti i file journal hello delle unità hello che fanno parte di tale processo di importazione. Le unità senza i file journal non saranno elaborate.
> 
>

Di seguito sono comandi hello ed esempi per la preparazione dell'unità disco rigido di hello utilizzando lo strumento WAImportExport.

Lo strumento WAImportExport comando PrepImport per hello innanzitutto copiare le directory di sessione toocopy e/o file con una nuova sessione di copia:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**Esempio 1 di importazione**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

In ordine troppo**aggiungere altre unità**, una possibile creare un nuovo file driveset ed eseguire il comando hello come indicato di seguito. Per la copia successive sessioni toohello unità disco diverse rispetto a quella specificata nel file CSV InitialDriveset, specificare un nuovo file CSV driveset e fornirlo come parametro di valore toohello "AdditionalDriveSet". Hello utilizzare **stesso file journal** assegnare un nome e un **nuovo ID di sessione**. formato di Hello del file CSV AdditionalDriveset è lo stesso formato InitialDriveSet.

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AdditionalDriveSet:<driveset.csv>
```

**Esempio 2 di importazione**
```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3  /AdditionalDriveSet:driveset-2.csv
```

In ordine tooadd dati aggiuntivi toohello driveset stesso, lo strumento WAImportExport PrepImport comando può essere chiamato per copia successive sessioni toocopy ulteriori file/directory: per copia successive sessioni toohello stesso disco rigido unità specificata CSV InitialDriveset file, specificare hello **stesso file journal** assegnare un nome e un **nuovo ID di sessione**; è presente alcuna chiave account di archiviazione di necessario tooprovide hello.

```
WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] DataSet:<dataset.csv>
```

**Esempio 3 di importazione**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

Visualizzare ulteriori dettagli sull'utilizzo dello strumento WAImportExport hello in [Preparazione unità disco rigido per l'importazione](storage-import-export-tool-preparing-hard-drives-import.md).

Inoltre, fare riferimento toohello [rigidi tooprepare del flusso di lavoro per un processo di importazione di esempio](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md) per istruzioni dettagliate.  

### <a name="create-hello-import-job"></a>Creare il processo di importazione hello
1. Dopo aver preparato l'unità, passare tooyour account di archiviazione nel portale di Azure hello e visualizzare hello Dashboard. In **Riepilogo rapido** fare clic **su Crea processo di importazione**. Rivedere i passaggi di hello e selezionare hello tooindicate di casella di controllo che è stato preparato l'unità e di disporre il file journal di unità hello è disponibile.
2. Nel passaggio 1, fornire le informazioni di contatto per hello responsabile questo processo di importazione e un indirizzo valido. Se si desiderano toosave dati di log dettagliato per il processo di importazione hello, verificare troppo opzione hello**Salva log dettagliato di hello nel contenitore blob 'waimportexport'**.
3. Nel passaggio 2, caricare il file journal di unità hello ottenuto durante il passaggio di Preparazione unità hello. È necessario un file tooupload per ogni unità preparata.
   
   ![Creare il processo di importazione - Passaggio 3](./media/storage-import-export-service/import-job-03.png)
4. Nel passaggio 3, immettere un nome descrittivo per il processo di importazione hello. Si noti che il nome di hello che immesso può contenere solo lettere minuscole, numeri, trattini e caratteri di sottolineatura, deve iniziare con una lettera e non può contenere spazi. Si utilizzerà hello nome scelto tootrack i processi mentre sono in corso e una volta completati.
   
   Successivamente, selezionare l'area del data center dall'elenco di hello. area del data center Hello indicherà dati hello al centro e indirizzo toowhich è necessario spedire il pacchetto. Domande frequenti su hello seguito per ulteriori informazioni, vedere.
5. Nel passaggio 4 hello riepilogo selezionare il vettore di ritorno e immettere il numero di account del vettore. Microsoft utilizzerà questo tooyou indietro account tooship hello unità al termine del processo di importazione.
   
   Se si dispone del numero di tracciabilità, selezionare il vettore recapito dall'elenco hello e immettere il numero di tracciabilità.
   
   Se non è un rilevamento numero ancora, scegliere **le informazioni di spedizione per questo processo di importazione verranno fornite dopo la spedizione del pacchetto**, quindi completare il processo di importazione hello.
6. Restituisce il numero di tracciabilità dopo che è stato spedito il pacchetto, tooenter toohello **importazione/esportazione** pagina per l'account di archiviazione nel portale di Azure hello, selezionare il processo dall'elenco di hello e scegliere **informazionisullaspedizione**. Spostarsi tra la procedura guidata hello e immettere il numero di tracciabilità nel passaggio 2.
   
    Se hello numero di tracciabilità non viene aggiornato entro due settimane di creazione del processo di hello, processo hello scadrà.
   
    Se è in stato di creazione, spedizione o trasferimento hello hello processo, è possibile aggiornare anche il numero di account vettore nel passaggio 2 della procedura guidata hello. Una volta hello è in stato di creazione di pacchetti hello, è possibile aggiornare il numero di account del vettore per tale processo.
7. È possibile rilevare lo stato di avanzamento del processo nel dashboard del portale hello. Vedere cosa significa ogni stato del processo nella sezione precedente hello [visualizzando lo stato del processo](#viewing-your-job-status).

## <a name="create-an-export-job"></a>Creare un processo di esportazione
Creare un hello toonotify processo di esportazione del servizio di importazione/esportazione che si spedirà uno o più i dati di toohello unità vuote center in modo che i dati possono essere esportati da unità toohello account di archiviazione e le unità hello fornito quindi tooyou.

### <a name="prepare-your-drives"></a>Preparare le unità
Per preparare le unità per un processo di esportazione si consiglia di eseguire i controlli preliminari seguenti:

1. Controllare il numero di hello di dischi richiesti utilizzando il comando di PreviewExport dello strumento WAImportExport hello. Per altre informazioni, vedere l'articolo sull' [anteprima dell'uso del disco per un processo di esportazione](https://msdn.microsoft.com/library/azure/dn722414.aspx). Consente di visualizzare l'anteprima dell'uso delle unità per i BLOB hello che è selezionata, in base alle dimensioni di hello di hello unità verrà toouse.
2. Verificare che è possibile lettura/scrittura disco rigido toohello forniti per il processo di esportazione hello.

### <a name="create-hello-export-job"></a>Creare il processo di esportazione hello
1. toocreate un processo di esportazione passare tooyour account di archiviazione nel portale di Azure hello e visualizzare hello Dashboard. In **Quick Glance**, fare clic su **creare un processo di esportazione** e procedere con la procedura guidata hello.
2. Nel passaggio 2, fornire le informazioni di contatto per hello responsabile questo processo di esportazione. Se si desiderano toosave dati di log dettagliato per il processo di esportazione hello, verificare troppo opzione hello**Salva log dettagliato di hello nel contenitore blob 'waimportexport'**.
3. Nel passaggio 3, specificare quali blob desiderato tooexport dal vuota tooyour account di archiviazione di dati di unità o unità. È possibile scegliere tooexport tutti i dati blob nell'account di archiviazione hello, oppure è possibile specificare che i BLOB o set di BLOB tooexport.
   
   toospecify tooexport un blob, utilizzare hello **uguale a** selettore e specificare i blob di toohello hello percorso relativo, a partire dal nome di contenitore hello. Utilizzare *$root* contenitore radice di hello toospecify.
   
   toospecify tutti i BLOB a partire da un prefisso, utilizzare hello **inizia con** selettore e specificare il prefisso hello, a partire da una barra '/'. prefisso Hello potrebbe essere il prefisso di hello del nome del contenitore hello, nome del contenitore completo hello o nome del contenitore completo hello seguito da hello prefisso del nome blob hello.
   
   Hello nella tabella seguente vengono illustrati esempi di percorsi blob validi:
   
   | Selettore | Percorso BLOB | Descrizione |
   | --- | --- | --- |
   | Starts With |/ |Esporta tutti i BLOB nell'account di archiviazione hello |
   | Starts With |/$root/ |Esporta tutti i BLOB nel contenitore radice hello |
   | Starts With |/book |Esporta tutti i BLOB in qualsiasi contenitore che inizia con il prefisso **book** |
   | Starts With |/music/ |Esporta tutti i BLOB nel contenitore **music** |
   | Starts With |/music/love |Esporta nel contenitore **music** tutti i BLOB che iniziano con il prefisso **love** |
   | Troppo uguale|$root/logo.bmp |Blob di esportazioni **logo. bmp** in un contenitore radice hello |
   | Troppo uguale|videos/story.mp4 |Esporta il BLOB **story.mp4** nel contenitore **video** |
   
   È necessario fornire percorsi blob hello in formati validi tooavoid errori durante l'elaborazione, come illustrato in questa schermata.
   
   ![Creare il processo di esportazione - Passaggio 3](./media/storage-import-export-service/export-job-03.png)
4. Nel passaggio 4, immettere un nome descrittivo per il processo di esportazione hello. nome Hello che immesso può contenere solo lettere minuscole, numeri, trattini e caratteri di sottolineatura, deve iniziare con una lettera e non può contenere spazi.
   
   area del data center Hello indicherà hello data center toowhich è necessario spedire il pacchetto. Domande frequenti su hello seguito per ulteriori informazioni, vedere.
5. Nel passaggio 5, hello riepilogo selezionare il vettore di ritorno e immettere il numero di account del vettore. Microsoft utilizzerà questo account tooship le unità di eseguire il backup tooyou una volta completato il processo di esportazione.
   
   Se si dispone del numero di tracciabilità, selezionare il vettore recapito dall'elenco hello e immettere il numero di tracciabilità.
   
   Se non è un rilevamento numero ancora, scegliere **le informazioni di spedizione per questo processo di esportazione verrà fornito dopo la spedizione del pacchetto**, quindi completare il processo di esportazione hello.
6. Restituisce il numero di tracciabilità dopo che è stato spedito il pacchetto, tooenter toohello **importazione/esportazione** pagina per l'account di archiviazione nel portale di Azure hello, selezionare il processo dall'elenco di hello e scegliere **informazionisullaspedizione**. Spostarsi tra la procedura guidata hello e immettere il numero di tracciabilità nel passaggio 2.
   
    Se hello numero di tracciabilità non viene aggiornato entro due settimane di creazione del processo di hello, processo hello scadrà.
   
    Se è in stato di creazione, spedizione o trasferimento hello hello processo, è possibile aggiornare anche il numero di account vettore nel passaggio 2 della procedura guidata hello. Una volta hello è in stato di creazione di pacchetti hello, è possibile aggiornare il numero di account del vettore per tale processo.
   
   > [!NOTE]
   > Se toobe blob hello esportata è in uso in fase di hello di copia toohard unità, il servizio di importazione/esportazione di Azure avrà uno snapshot dello snapshot di hello hello blob e di copia.
   > 
   > 
7. Nel dashboard di hello in hello portale di Azure, è possibile monitorare lo stato di avanzamento del processo. Vedere significato di ogni stato del processo nella sezione precedente hello in "visualizzando lo stato del processo".
8. Dopo aver ricevuto le unità hello con i dati esportati, è possibile visualizzare e copiare le chiavi BitLocker hello generate dal servizio hello per le unità. Passare tooyour account di archiviazione nel portale di Azure hello e fare clic sulla scheda importazione/esportazione di hello. Selezionare il processo di esportazione dall'elenco hello e fare clic sul pulsante Visualizza chiavi hello. le chiavi BitLocker Hello vengono visualizzati come illustrato di seguito:
   
   ![Visualizzare le chiavi BitLocker per il processo di esportazione](./media/storage-import-export-service/export-job-bitlocker-keys.png)

Visitare la sezione Domande frequenti su hello sotto come copre domande più comuni di hello riscontrati quando si utilizza questo servizio.

## <a name="frequently-asked-questions"></a>Domande frequenti

**È possibile copiare l'archiviazione di File di Azure tramite il servizio di importazione/esportazione di Azure hello?**

No, hello servizio importazione/esportazione di Azure supporta solo BLOB in blocchi e BLOB di pagine. Tutti gli altri tipi di archiviazione non sono supportati, inclusa l'archiviazione di file, di tabelle e di code di Azure.

**È disponibile per le sottoscrizioni di CSP servizio importazione/esportazione di Azure hello?**

Il servizio di importazione/esportazione di Azure supporta le sottoscrizioni CSP.

**È possibile ignorare il passaggio di Preparazione unità di hello per un processo di importazione o è possibile preparare un'unità senza copiare?**

Qualsiasi unità di cui si desidera tooship per l'importazione di dati deve essere preparato tramite lo strumento WAImportExport Azure hello. È necessario utilizzare l'unità di WAImportExport strumento toocopy dati toohello hello.

**È necessario tooperform qualsiasi preparazione del disco durante la creazione di un processo di esportazione?**

No, ma alcuni controlli preliminari sono consigliati Controllare il numero di hello di dischi richiesti utilizzando il comando di PreviewExport dello strumento WAImportExport hello. Per altre informazioni, vedere l'articolo sull' [anteprima dell'uso del disco per un processo di esportazione](https://msdn.microsoft.com/library/azure/dn722414.aspx). Consente di visualizzare l'anteprima dell'uso delle unità per i BLOB hello che è selezionata, in base alle dimensioni di hello di hello unità verrà toouse. Anche verificare che è possibile leggere da e scrittura toohello rigido forniti per hello processo di esportazione.

**Cosa accade se accidentalmente inviare un'unità HDD che non è conforme toohello requisiti supportati?**

Hello data center di Azure restituirà unità hello che non è conforme tooyou requisiti toohello supportato. Se solo alcune delle unità hello nel pacchetto hello soddisfa i requisiti di supporto di hello, le unità verranno elaborati e unità hello che non soddisfano i requisiti di hello verranno restituite tooyou.

**È possibile annullare il processo?**

È possibile annullare un processo quando lo stato è Creating o Shipping.

**Quanto tempo è possibile visualizzare lo stato di hello dei processi completati nel portale di Azure hello?**

È possibile visualizzare lo stato di hello dei processi completati per impostare i giorni too90. I processi completi vengono eliminati dopo 90 giorni.

**Se si desidera tooimport o si esportano più di 10 unità, cosa fare?**

Un'importazione o esportazione processo può fare riferimento solo 10 unità in un singolo processo per il servizio di importazione/esportazione hello. Se si desidera tooship più di 10 unità, è possibile creare più processi. Le unità associate a hello stesso processo deve essere consegnato insieme in hello stesso pacchetto.
Microsoft offre informazioni e assistenza nel caso in cui la capacità venga distribuita su più processi di importazione di dischi. Per altre informazioni, contattare bulkimport@microsoft.com

**Hello servizio formato hello unità prima di restituirli?**

No. Tutte le unità vengono crittografate con BitLocker.

**È possibile acquistare da Microsoft unità per i processi di importazione/esportazione?**

No. Sarà necessario tooship unità personalizzate sia per importare ed esportare i processi.

* * Come è possibile accedere ai dati importati da questo servizio? * *

dati Hello con l'account di archiviazione di Azure accessibili tramite il portale di Azure hello o utilizzando uno strumento autonomo denominato Esplora archivi. https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-manage-with-storage-explorer 

**Al termine del processo di importazione hello, cosa verrà my dati aspetto nell'account di archiviazione hello? Verrà mantenuta la gerarchia delle directory?**

Quando si prepara un disco rigido per un processo di importazione, destinazione hello viene specificato dal campo DstBlobPathOrPrefix hello nel set di dati CSV. Questo è il contenitore di destinazione hello in hello toowhich di account di archiviazione dati dal disco rigido hello viene copiati. In questo contenitore di destinazione, directory virtuali vengono create per le cartelle dal disco rigido hello e BLOB vengono creati per i file. 

**Se hello è file già presenti nel mio account di archiviazione, il servizio hello sovrascriverà BLOB esistente nel mio account di archiviazione?**

Quando si prepara l'unità di hello, è possibile specificare se i file di destinazione hello devono essere sovrascritti o ignorati usando il campo di hello nel file CSV di set di dati denominato Disposition: < rinominare | no-overwrite | sovrascrivere >. Per impostazione predefinita, il servizio hello verrà rinominare i nuovi file hello anziché sovrascrivere un BLOB esistente.

**È compatibile con sistemi operativi a 32 bit dello strumento WAImportExport hello?**
No. lo strumento WAImportExport Hello è compatibile solo con sistemi operativi Windows a 64 bit. Consultare la sezione sistemi operativi toohello hello [prerequisiti](#pre-requisites) per un elenco completo delle versioni del sistema operativo supportate.

**È consigliabile includere un elemento diverso dalla hello unità disco rigido nel pacchetto?**

Spedire solo i dischi rigidi. Non inserire oggetti come cavi di alimentazione o cavi USB.

**È necessario tooship le unità tramite FedEx o DHL?**

Spedire le unità toohello data center mediante qualsiasi vettore noti come FedEx, DHL, gruppo di continuità o ci servizio postale. Tuttavia, per la spedizione hello unità indietro tooyou dal centro dati hello, è necessario specificare un numero di account FedEx in hello negli Stati Uniti e Unione europea, o un numero di account DHL in Asia hello e aree di Australia.

**Vi sono restrizioni in merito alla spedizione internazionale delle unità?**

Si noti che i supporti fisici hello che si potrebbero essere necessario toocross internazionali bordi. Si è responsabile di garantire che i supporti fisici e i dati vengono importati e/o esportati in base alle leggi applicabili in materia hello. Prima di consegnare supporti fisici hello, rivolgersi il tooverify consulenti che i supporti e i dati possono essere legalmente toohello spediti identificato data center. Ciò consentirà di tooensure raggiunge Microsoft in modo tempestivo.

**Quando si crea un processo, hello indirizzo di spedizione è un percorso diverso dalla posizione dell'account di archiviazione. Cosa devo fare?**

Alcuni percorsi di account di archiviazione sono mappate tooalternate indirizzi di spedizione. Ubicazioni di spedizione disponibili in precedenza possono essere anche percorsi tooalternate temporaneamente mappato. Verificare sempre hello indirizzo fornito durante la creazione del processo prima della spedizione delle unità per la spedizione.

**Quando si distribuisce l'unità, vettore hello chiede hello data center contatto indirizzo e numero di telefono. Cosa devo fornire?**

Hello numero di telefono e controller di dominio indirizzo viene fornito come parte della creazione del processo.

**È possibile utilizzare le cassette postali PST toocopy hello importazione/esportazione di Azure del servizio e tooO365 dati SharePoint**

Consultare troppo[tooOffice dati SharePoint 365 o file di importazione PST](https://technet.microsoft.com/library/ms.o365.cc.ingestionhelp.aspx).

**È possibile utilizzare toocopy servizio di importazione/esportazione di Azure hello my toohello offline backup servizio Backup di Azure?**

Consultare troppo[flusso di lavoro di Backup Offline in Azure Backup](../../backup/backup-azure-backup-import-export.md).

**Che cos'è hello massimo un numero di unità disco rigido per una sola spedizione?**

Qualsiasi numero di unità disco rigido può trovarsi in una spedizione e se i dischi hello appartengono toomultiple processi è consigliabile troppo un) dispone di dischi hello identificati con nomi di processo corrispondente hello. b) i processi di hello aggiornamento con un numero di tracciabilità provvisto di -1, e così via-2.
  
**Che cos'è hello massimo Blob in blocchi e Blob di paging supportati dal disco importazione/esportazione?**

La dimensione massima dei BLOB in blocchi è circa 4768 TB o 5.000.000 MB.
La dimensione massima di un BLOB di pagine è 1 TB.

**Importazione/Esportazione di Microsoft Azure supporta la crittografia AES 256?**

Servizio di importazione/esportazione di Azure per impostazione predefinita vengono crittografate con crittografia bitlocker AES 128, ma può essere maggiore tooAES 256 crittografando manualmente con bitlocker prima che i dati vengono copiati. 

Se si usa [WAImportExpot V1](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip), di seguito viene indicato un comando di esempio
```
WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>] 
```
Se si utilizza [strumento WAImportExport](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip) specificare "AlreadyEncrypted" e immettere la chiave hello in hello driveset CSV.
```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
```
## <a name="next-steps"></a>Passaggi successivi

* [Impostazione dello strumento WAImportExport hello](storage-import-export-tool-how-to.md)
* [Trasferimento dati con hello utilità della riga di comando AzCopy](storage-use-azcopy.md)
* [Esempio di API REST del servizio Importazione/Esportazione di Azure](https://azure.microsoft.com/documentation/samples/storage-dotnet-import-export-job-management/)

