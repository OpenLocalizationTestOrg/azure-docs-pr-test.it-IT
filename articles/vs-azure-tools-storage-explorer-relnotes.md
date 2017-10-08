---
title: note sulla versione di aaaMicrosoft Esplora archivi Azure (anteprima) | Documenti Microsoft
description: Note sulla versione di Microsoft Azure Storage Explorer (anteprima)
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.devlang: multiple
ms.topic: release-notes
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: cawa
ms.openlocfilehash: 44ff6dc8e2015f4eb71fa13098b832fbbf48ccac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a>Note sulla versione di Microsoft Azure Storage Explorer (anteprima)

Questo articolo contiene una versione di hello release notes per Azure Storage Explorer 0.8.16 (anteprima), nonché le note sulla versione per le versioni precedenti.

[Esplora archivi di Microsoft Azure (anteprima)](./vs-azure-tools-storage-manage-with-storage-explorer.md) è un'applicazione autonoma che consente di utilizzare tooeasily dati di archiviazione di Azure in Windows, macOS e Linux.

## <a name="version-0816-preview"></a>Versione 0.8.16 (anteprima)
21/08/2017

### <a name="download-azure-storage-explorer-0816-preview"></a>Download di Azure Storage Explorer 0.8.16 (anteprima)
- [Azure Storage Explorer 0.8.16 (anteprima) per Windows](https://go.microsoft.com/fwlink/?LinkId=708343)
- [Azure Storage Explorer 0.8.16 (anteprima) per Mac](https://go.microsoft.com/fwlink/?LinkId=708342)
- [Azure Storage Explorer 0.8.16 (anteprima) per Linux](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a>Nuovo
* Quando si apre un blob, Esplora archivi richiederà file hello scaricato tooupload se viene rilevata una modifica
* Esperienza di accesso ad Azure Stack migliorata
* Prestazioni migliorate hello caricamento/scaricamento di molti piccoli file hello stesso tempo


### <a name="fixes"></a>Correzioni
* Per alcuni tipi di blob, scelta troppo "replace" durante un conflitto di caricamento talvolta comporta il caricamento di hello in fase di riavvio. 
* Nella versione 0.8.15 i caricamenti rimangono talvolta bloccati al 99%.
* Durante il caricamento di condivisione file tooa di file, se si sceglie di directory di tooa tooupload che ancora non esiste, il caricamento avrà esito negativo.
* Storage Explorer generava timestamp non corretti per le firme di accesso condiviso e le query di tabella.


Problemi noti
* L'uso di una stringa di connessione con nome e chiave attualmente non funziona. Si verrà risolto nella prossima versione di hello. Fino ad allora è possibile collegarsi con nome e chiave.
* Se si tenta di tooopen un file con un nome di file non valido di Windows, il download di hello comporterà un errore file non trovato.
* Dopo aver fatto clic "Annulla" per un'attività, potrebbe richiedere un po' di tempo per toocancel tale attività. Si tratta di una limitazione della libreria di hello nodo archiviazione di Azure.
* Dopo aver completato il caricamento di un blob, scheda hello che ha avviato il caricamento di hello viene aggiornata. Questa è una modifica dal comportamento precedente e provocherà inoltre toobe ritirato toohello radice del contenitore di hello in.
* Se si sceglie di hello certificati smart card PIN o errato, sarà necessario toorestart in ordine toohave Esplora archivi dimenticare tale decisione.
* impostazioni del Pannello di Hello account potrebbero mostrare che è necessario che le sottoscrizioni di toofilter credenziali tooreenter.
* La ridenominazione di BLOB singoli o all'interno di un contenitore BLOB rinominato non mantiene gli snapshot. Tutte le altre proprietà e i metadati di BLOB, file ed entità vengono conservati durante un'operazione di ridenominazione.
* Sebbene Azure Stack attualmente non supporta le condivisioni file, viene comunque visualizzato un nodo delle condivisioni di file in un account di archiviazione di Azure Stack associato.
* Per gli utenti Ubuntu 14.04, sarà necessario tooensure GCC sia attivo toodate - questa operazione può essere eseguita tramite l'esecuzione di hello i comandi seguenti e quindi riavviare il computer:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* Per gli utenti 17.04 Ubuntu, sarà necessario tooinstall GConf - questo scopo, in esecuzione hello i comandi seguenti e quindi riavviare il computer:

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a>Versione 0.8.14 (anteprima)
22/06/2017

### <a name="download-azure-storage-explorer-0814-preview"></a>Download di Azure Storage Explorer 0.8.14 (anteprima)
* [Download di Azure Storage Explorer 0.8.14 (anteprima) per Windows](https://go.microsoft.com/fwlink/?LinkId=809306)
* [Download di Azure Storage Explorer 0.8.14 (anteprima) per Mac](https://go.microsoft.com/fwlink/?LinkId=809307)
* [Download di Azure Storage Explorer 0.8.14 (anteprima) per Linux](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a>Nuovo

* Too1.7.2 di versione elettronici aggiornato in diversi aggiornamenti critici della protezione sfruttare tootake ordine
* È possibile ora accedere rapidamente nella Guida in linea sulla risoluzione dei problemi hello dal menu di hello?
* [Guida][2]alla risoluzione dei problemi di Storage Explorer
* [Istruzioni] [ 3] sulla connessione di sottoscrizione di Azure Stack tooan

### <a name="known-issues"></a>Problemi noti

* I pulsanti nella finestra di dialogo Conferma cartella delete hello non registra con il clic del mouse hello in Linux. Soluzione alternativa è l'invio di toouse hello
* Se si sceglie di hello certificati smart card PIN o errato, sarà necessario toorestart in ordine toohave Esplora archivi dimenticare decisione hello
* Più di 3 gruppi di BLOB o i file di caricamento in hello stesso tempo può causare errori
* impostazioni del Pannello di account Hello possono indicare che sono necessarie le credenziali di tooreenter nelle sottoscrizioni toofilter ordine
* La ridenominazione di BLOB singoli o all'interno di un contenitore BLOB rinominato non mantiene gli snapshot. Tutte le altre proprietà e i metadati di BLOB, file ed entità vengono conservati durante un'operazione di ridenominazione.
* Sebbene Azure Stack attualmente non supporta le condivisioni file, viene comunque visualizzato un nodo delle condivisioni di file in un account di archiviazione di Azure Stack associato. 
* Di seguito sono Ubuntu 14.04 esigenze di installare le versioni o aggiornare – tooupgrade passaggi:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a>Versioni precedenti

* [Versione 0.8.13](#version-0813)
* [Versione 0.8.12/0.8.11/0.8.10](#version-0812--0811--0810)
* [Versione 0.8.9/0.8.8](#version-089--088)
* [Versione 0.8.7](#version-087)
* [Versione 0.8.6](#version-086)
* [Versione 0.8.5](#version-085)
* [Versione 0.8.4](#version-084)
* [Versione 0.8.3](#version-083)
* [Versione 0.8.2](#version-082)
* [Versione 0.8.0](#version-080)
* [Versione 0.7.20160509.0](#version-07201605090)
* [Versione 0.7.20160325.0](#version-07201603250)
* [Versione 0.7.20160129.1](#version-07201601291)
* [Versione 0.7.20160105.0](#version-07201601050)
* [Versione 0.7.20151116.0](#version-07201511160)


### <a name="version-0813"></a>Versione 0.8.13
12/05/2017

#### <a name="new"></a>Nuovo

* [Guida][2]alla risoluzione dei problemi di Storage Explorer
* [Istruzioni] [ 3] sulla connessione di sottoscrizione di Azure Stack tooan

#### <a name="fixes"></a>Correzioni

* Corretto: il caricamento del file aveva una probabilità elevata di causare un errore di memoria insufficiente
* Corretto: è ora possibile accedere con PIN/smart card
* Corretto: l'azione Apri nel portale ora funziona con Azure China, Azure Germany, Azure US Government e Azure Stack
* Problema risolto: Durante il caricamento di un contenitore di blob tooa cartella, un errore "Operazione non valida" talvolta si verificherebbe
* Corretto: selezionare tutto ciò che è stato disabilitato durante la gestione di snapshot
* Problema risolto: hello metadati del blob di base hello potrebbero essere sovrascritte dopo la visualizzazione delle proprietà hello relativi snapshot

#### <a name="known-issues"></a>Problemi noti

* Se si sceglie di hello certificati smart card PIN o errato, sarà necessario toorestart in ordine toohave Esplora archivi dimenticare decisione hello
* Mentre è stato eseguito lo zoom avanti o indietro, il livello di zoom hello momentaneamente possibile reimpostare livello predefinito toohello
* Più di 3 gruppi di BLOB o i file di caricamento in hello stesso tempo può causare errori
* impostazioni del Pannello di account Hello possono indicare che sono necessarie le credenziali di tooreenter nelle sottoscrizioni toofilter ordine
* La ridenominazione di BLOB singoli o all'interno di un contenitore BLOB rinominato non mantiene gli snapshot. Tutte le altre proprietà e i metadati di BLOB, file ed entità vengono conservati durante un'operazione di ridenominazione.
* Sebbene Azure Stack attualmente non supporta le condivisioni file, viene comunque visualizzato un nodo delle condivisioni di file in un account di archiviazione di Azure Stack associato. 
* Di seguito sono Ubuntu 14.04 esigenze di installare le versioni o aggiornare – tooupgrade passaggi:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a>Versione 0.8.12/0.8.11/0.8.10
07/04/2017

#### <a name="new"></a>Nuovo

* Esplora archivi verrà chiuso automaticamente quando si installa un aggiornamento da una notifica di aggiornamento hello
* L'accesso rapido sul posto fornisce un'esperienza ottimizzata per l'uso con le risorse a cui si accede di frequente
* Nell'editor di hello contenitore Blob, è ora possibile visualizzare un blob con lease appartiene alla macchina virtuale
* È ora possibile comprimere il riquadro di sinistra hello
* Individuazione ora viene eseguito nel hello stesso tempo come download
* Le statistiche di utilizzo nel contenitore Blob, condivisione File e tabella editor toosee hello le dimensioni della risorsa o selezione hello
* È possibile adesso Accedi tooAzure Active Directory (AAD) basato su account di Azure Stack. 
* È possibile ora i file di archivio di caricamento di account di archiviazione di più di 32 MB tooPremium
* Supporto di accessibilità migliorato
* È ora possibile aggiungere Base-64 attendibili i certificati x. 509 SSL per la codifica verrà tooEdit -&gt; i certificati SSL -&gt; importazione certificati

#### <a name="fixes"></a>Correzioni

* Problema risolto: dopo l'aggiornamento delle credenziali dell'account, visualizzazione albero hello sarebbe talvolta viene aggiornata automaticamente
* Corretto: la generazione di una firma di accesso condiviso per le code e le tabelle dell'emulatore dà origine a un URL non valido
* Corretto: gli account di archiviazione premium possono ora essere espansi mentre è abilitato un proxy
* Problema risolto: hello pulsante Applica per gli account di hello pagina di gestione non funziona se si dispone di 0 o 1 account selezionati
* Corretto: il caricamento di BLOB che richiedono le risoluzioni di conflitti potrebbe non andare a buon termine - corretto in 0.8.11 
* Corretto: l'invio di commenti e suggerimenti veniva interrotto nella versione 0.8.11 - corretto in 0.8.12 

#### <a name="known-issues"></a>Problemi noti

* Dopo l'aggiornamento too0.8.10, sarà necessario toorefresh tutte le credenziali.
* Mentre è stato eseguito lo zoom avanti o indietro, il livello di zoom hello può reimpostare momentaneamente livello predefinito toohello.
* Più di 3 gruppi di BLOB o i file di caricamento in hello stesso tempo può causare errori.
* impostazioni del Pannello di Hello account potrebbero mostrare che sono necessarie le credenziali di tooreenter nelle sottoscrizioni toofilter ordine.
* La ridenominazione di BLOB singoli o all'interno di un contenitore BLOB rinominato non mantiene gli snapshot. Tutte le altre proprietà e i metadati di BLOB, file ed entità vengono conservati durante un'operazione di ridenominazione.
* Sebbene Azure Stack attualmente non supporta le condivisioni file, viene comunque visualizzato un nodo delle condivisioni di file in un account di archiviazione di Azure Stack associato. 
* Di seguito sono Ubuntu 14.04 esigenze di installare le versioni o aggiornare – tooupgrade passaggi:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a>Versione 0.8.9/0.8.8
23/02/2017

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a>Nuovo

* Esplora archivi 0.8.9 scaricherà automaticamente una versione più recente di hello per gli aggiornamenti.
* Hotfix: tramite un portale generato tooattach URI SAS che un account di archiviazione comporta un errore.
* È ora possibile creare, gestire e alzare di livello degli snapshot di BLOB.
* È ora possibile accedere tooAzure Cina, Germania Azure e Azure del governo account.
* È ora possibile modificare il livello di zoom hello. Utilizzare opzioni hello tooZoom menu Visualizza di hello In, Zoom indietro e reimposta Zoom.
* I caratteri Unicode sono ora supportati nei metadati dell'utente per file e BLOB.
* Miglioramenti all'accessibilità.
* note sulla versione della versione di Hello Avanti possono essere visualizzati dalla notifica di aggiornamento hello. È inoltre possibile visualizzare hello note sulla versione corrente dal menu di hello.

#### <a name="fixes"></a>Correzioni

* Problema risolto: il numero di versione di hello è ora visualizzato correttamente nel Pannello di controllo in Windows
* Problema risolto: ricerca non è più limitato too50, nodi 000
* Problema risolto: condivisione di file di caricamento tooa ruotato per sempre se la directory di destinazione hello non esisteva
* Corretto: maggiore stabilità per processi di caricamento e download prolungati

#### <a name="known-issues"></a>Problemi noti

* Mentre è stato eseguito lo zoom avanti o indietro, il livello di zoom hello può reimpostare momentaneamente livello predefinito toohello.
* Accesso rapido funziona solo con gli elementi basati su sottoscrizione. Questa versione non supporta le risorse locali e le risorse collegate tramite chiave o token di firma di accesso condiviso.
* Accesso rapido può richiedere alcuni secondi toonavigate toohello risorsa di destinazione, a seconda di quanti di risorse.
* Più di 3 gruppi di BLOB o i file di caricamento in hello stesso tempo può causare errori.

16/12/2016
### <a name="version-087"></a>Versione 0.8.7

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nuovo

* È possibile scegliere come conflitti tooresolve all'inizio di hello di un aggiornamento, scaricare o copiare sessione nella finestra attività hello
* Passare il mouse su un percorso completo di hello toosee scheda della risorsa di archiviazione hello
* Quando si fa clic su una scheda, sincronizzazione con la posizione nel riquadro di spostamento sinistra hello

#### <a name="fixes"></a>Correzioni

* Corretto: Storage Explorer è ora un'app attendibile su Mac
* Corretto: Ubuntu 14.04 è supportato nuovamente
* Problema risolto: Talvolta hello aggiungere l'account dell'interfaccia utente lampeggia quando il caricamento delle sottoscrizioni
* Problema risolto: Talvolta non tutte le risorse di archiviazione sono state elencate nel riquadro di spostamento sinistra hello
* Problema risolto: hello azione talvolta visualizzato il riquadro azioni vuote
* Problema risolto: dimensioni della finestra hello dalla sessione chiusa l'ultima volta hello ora mantenute
* Problema risolto: È possibile aprire più schede per hello stessa risorsa utilizzando il menu di scelta rapida hello

#### <a name="known-issues"></a>Problemi noti

* Accesso rapido funziona solo con gli elementi basati su sottoscrizione. Questa versione non supporta le risorse locali e le risorse collegate tramite chiave o token di firma di accesso condiviso
* Accesso rapido può richiedere alcuni secondi toonavigate toohello risorsa di destinazione, a seconda di quanti di risorse
* Più di 3 gruppi di BLOB o i file di caricamento in hello stesso tempo può causare errori
* È possibile eseguire la ricerca in un massimo di 50.000 nodi circa. Se si supera tale limite, le prestazioni potrebbero risultare peggiorate o potrebbero essere generate eccezioni non gestite
* Per hello primo accesso tramite Esplora archivi hello in macOS, si potrebbero notare più prompt chiede portachiavi tooaccess di autorizzazione dell'utente. È consigliabile che selezionare Consenti sempre in modo non verranno visualizzati prompt hello nuovamente

18/11/2016
### <a name="version-086"></a>Versione 0.8.6

#### <a name="new"></a>Nuovo

* È possibile ora pin utilizzati più frequentemente servizi toohello accesso rapido per semplificare la navigazione
* Possibilità di aprire più editor in schede diverse. A singolo clic tooopen una scheda temporanea. Fare doppio clic su una scheda permanente tooopen. È possibile anche fare clic su toomake scheda temporaneo hello è una scheda permanente
* Sono stati apportati miglioramenti evidenti a prestazioni e stabilità per operazioni di caricamento e download, soprattutto per file di grandi dimensioni in computer veloci
* Possibilità di creare cartelle vuote "virtuali" in contenitori BLOB
* È stato reintrodotto l'ambito di ricerca con la nuova ricerca avanzata con sottostringa, pertanto ora vi sono due opzioni di ricerca: 
    * Globale ricerca - immettere solo un termine di ricerca nella casella di ricerca testo hello
    * La ricerca con ambita, fare clic su hello lente di ingrandimento icona tooa nodo successivo, quindi aggiungere un fine toohello termine di ricerca del percorso di hello, o fare doppio clic su e selezionare "ricerca da"
* Sono stati aggiunti vari temi: Chiaro (impostazione predefinita), Scuro, Nero a contrasto elevato e Bianco a contrasto elevato. Passare tooEdit -&gt; toochange temi le preferenze di temi
* È possibile modificare le proprietà di BLOB e file
* Sono ora supportati i messaggi in coda codificati (base64) e non codificati
* In Linux è ora necessario un sistema operativo a 64 bit. Per questa versione è supportato solo Ubuntu 16.04.1 LTS a 64 bit
* È stato aggiornato il logo

#### <a name="fixes"></a>Correzioni

* Corretto: problemi di blocco della schermata
* Corretto: sicurezza avanzata
* Corretto: a volte venivano visualizzati account collegati doppi
* Corretto: un blob con un tipo di contenuto non definito poteva generare un'eccezione
* Problema risolto: Hello apertura pannello della Query in una tabella vuota non è stato possibile
* Corretto: bug delle variabili in Cerca
* Problema risolto: Aumentato il numero di hello delle risorse caricate dal 50 too100 quando facendo clic su "Più carico"
* Corretto: alla prima esecuzione, se si è effettuato l'accesso a un account, vengono ora selezionate tutte le sottoscrizioni per tale account per impostazione predefinita 

#### <a name="known-issues"></a>Problemi noti

* Questa versione di hello Esplora archivi non vengono eseguite Ubuntu 14.04
* tooopen più schede per la stessa risorsa, non sempre si fare clic su hello hello stessa risorsa. Fare clic su un'altra risorsa e quindi tornare indietro e quindi fare clic su tooopen risorsa originale hello nuovo in un'altra scheda 
* Accesso rapido funziona solo con gli elementi basati su sottoscrizione. Questa versione non supporta le risorse locali e le risorse collegate tramite chiave o token di firma di accesso condiviso
* Accesso rapido può richiedere alcuni secondi toonavigate toohello risorsa di destinazione, a seconda di quanti di risorse
* Più di 3 gruppi di BLOB o i file di caricamento in hello stesso tempo può causare errori
* È possibile eseguire la ricerca in un massimo di 50.000 nodi circa. Se si supera tale limite, le prestazioni potrebbero risultare peggiorate o potrebbero essere generate eccezioni non gestite

03/10/2016
### <a name="version-085"></a>Versione 0.8.5

#### <a name="new"></a>Nuovo

* Possono ora utilizzare generato portale SAS chiavi tooattach tooStorage account e risorse

#### <a name="fixes"></a>Correzioni

* Problema risolto: race condition durante la ricerca talvolta causata toobecome nodi non espandibili
* Problema risolto: "Usa HTTP" non viene eseguita quando la connessione di account tooStorage con chiave e il nome dell'account
* Corretto: le chiavi di firma di accesso condiviso (specialmente quelle generati da portale) restituiscono un errore "barra finale"
* Corretto: problemi di importazione della tabella
    * In alcuni casi la chiave di partizione e la chiave di riga venivano annullate
    * Non è possibile tooread "null", le chiavi di partizione

#### <a name="known-issues"></a>Problemi noti

* È possibile eseguire la ricerca in un massimo di 50.000 nodi circa. Se si supera tale limite, le prestazioni potrebbero risultare peggiorate
* Stack di Azure attualmente non supporta i file, in modo tooexpand file durante il tentativo verrà visualizzato un errore

12/09/2016
### <a name="version-084"></a>Versione 0.8.4

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nuovo

* Generare gli account toostorage di collegamenti diretti, contenitori, le code, tabelle o condivisioni di file per la condivisione e di facile accesso alle risorse di tooyour - Windows e Mac OS supporta
* Ricerca per i contenitori blob, tabelle, code, condivisioni file o la casella di ricerca hello gli account di archiviazione
* È ora possibile raggruppare le clausole nel generatore di query di tabella hello
* Rinominare e copiare/incollare contenitori BLOB, condivisioni file, tabelle, BLOB, cartelle di BLOB, file e directory all'interno di contenitori e account collegati alla firma di accesso condiviso
* Quando vengono ridenominati e copiati contenitori BLOB e condivisioni file, proprietà e metadati vengono mantenuti

#### <a name="fixes"></a>Correzioni

* Corretto: impossibile modificare le voci della tabella se contengono le proprietà di tipo booleano o binario

#### <a name="known-issues"></a>Problemi noti

* È possibile eseguire la ricerca in un massimo di 50.000 nodi circa. Se si supera tale limite, le prestazioni potrebbero risultare peggiorate

03/08/2016
### <a name="version-083"></a>Versione 0.8.3

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nuovo

* Ridenominazione di contenitori, tabelle e condivisioni file
* Migliore esperienza con il Generatore di query
* Query di carico e toosave possibilità
* Gli account o contenitori, le code, tabelle di toostorage di collegamenti diretti, condivisioni file o per la condivisione e facilmente l'accesso alle risorse (solo Windows - macOS supportano sarà presto disponibile!)
* Toomanage possibilità e configurare le regole CORS

#### <a name="fixes"></a>Correzioni

* Corretto: gli account di Microsoft richiedono la riautenticazione ogni 8-12 ore

#### <a name="known-issues"></a>Problemi noti

* Talvolta hello dell'interfaccia utente potrebbe sembrare bloccata, ingrandire la finestra hello consente di risolvere il problema
* L'installazione di macOS potrebbe richiedere autorizzazioni elevate
* Pannello impostazioni account potrebbe mostrare che sono necessarie le credenziali di tooreenter nelle sottoscrizioni toofilter ordine
* Ridenominazione di condivisioni file, i contenitori di blob e tabelle non mantiene i metadati o altre proprietà nel contenitore di hello, ad esempio la quota di condivisione file, il livello di accesso pubblico o criteri di accesso
* La ridenominazione di BLOB singoli o all'interno di un contenitore BLOB rinominato non mantiene gli snapshot. Tutte le altre proprietà e i metadati di BLOB, file ed entità vengono conservati durante un'operazione di ridenominazione
* La copia o la ridenominazione delle risorse non funziona all'interno di account associati alla firma di accesso condiviso

07/07/2016
### <a name="version-082"></a>Versione 0.8.2

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nuovo

* Gli account di archiviazione vengono raggruppati in sottoscrizioni. L'archiviazione e le risorse di sviluppo collegate tramite chiave o firma di accesso condiviso vengono visualizzate nel nodo (locale e collegato)
* Disconnettersi dagli account nel pannello "Impostazioni account Azure"
* Configurare tooenable impostazioni proxy e gestire l'accesso
* Creare e interrompere i lease di blob
* Aprire contenitori BLOB, code, tabelle e i file con un unico clic

#### <a name="fixes"></a>Correzioni

* Corretto: i messaggi in coda con le librerie .NET o Java non vengono decodificati correttamente da base64
* Corretto: le tabelle $metrics non vengono visualizzate per gli account di archiviazione Blob
* Corretto: il nodo delle tabelle non funziona per l'archiviazione locale (sviluppo)

#### <a name="known-issues"></a>Problemi noti

* L'installazione di macOS potrebbe richiedere autorizzazioni elevate

15/06/2016
### <a name="version-080"></a>Versione 0.8.0

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nuovo

* Supporto per condivisione file: visualizzazione, caricamento, download, copia di file e directory, URI della firma di accesso condiviso (creazione e la connessione)
* Esperienza utente migliorata per la connessione tooStorage con URI SAS o le chiavi dell'account
* Risultati della query relativa alla tabella di esportazione
* Riordinamento e personalizzazione delle colonne della tabella
* Visualizzazione dei contenitori BLOB $logs e delle tabelle $metrics per gli account di archiviazione con le metriche abilitate
* Comportamento di esportazione e importazione migliorato, include ora il tipo di valore della proprietà

#### <a name="fixes"></a>Correzioni

* Corretto: il caricamento o il download di BLOB di grandi dimensioni può essere incompleto
* Problema risolto: la modifica, aggiunta o l'importazione di un'entità con un valore numerico ("1") verrà convertito toodouble
* Problema risolto: Nodo della tabella hello tooexpand Impossibile nell'ambiente di sviluppo locale hello

#### <a name="known-issues"></a>Problemi noti

* L tabelle $metrics non sono visibili per gli account di archiviazione Blob
* Coda di messaggi a livello di programmazione può non essere visualizzata correttamente messaggi hello vengono codificati utilizzando la codifica Base64

17/05/2016
### <a name="version-07201605090"></a>Versione 0.7.20160509.0

#### <a name="new"></a>Nuovo

* Migliore gestione degli errori per i crash dell'app

#### <a name="fixes"></a>Correzioni

* Correzione del bug per cui i messaggi sulla barra delle informazioni talvolta non vengono visualizzati quando sono necessarie credenziali di accesso

#### <a name="known-issues"></a>Problemi noti

* Tabelle: Aggiunta, modifica, o l'importazione di un'entità che dispone di una proprietà con un valore numerico in modo ambiguo, ad esempio "1" o "1.0", e hello toosend tenta di utente come un `Edm.String`, il valore di hello, verrà ripristinato tramite client hello API come un EDM

31/03/2016

### <a name="version-07201603250"></a>Versione 0.7.20160325.0

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a>Nuovo

* Supporto tabella: visualizzazione, esecuzione di query, esportazione, importazione e operazioni CRUD per le entità
* Supporto coda: visualizzazione, aggiunta, rimozione dei messaggi dalla coda
* Generazione di URI della firma di accesso condiviso per gli account di archiviazione
* Connessione tooStorage account con l'URI di firma di accesso condiviso
* Aggiornare notifiche per gli aggiornamenti futuri tooStorage Explorer
* Aspetto aggiornato

#### <a name="fixes"></a>Correzioni

* Miglioramenti dell'affidabilità e delle prestazioni

### <a name="known-issues-amp-mitigations"></a>Problemi noti &amp; Prevenzione

* Il download di file BLOB di grandi dimensioni non funziona correttamente. È consigliabile usare AzCopy fino alla risoluzione del problema 
* Le credenziali dell'account non essere recuperate o memorizzate nella cache se hello home directory non è stata trovata o non può essere scritta
* Se è in aggiunta, modifica o l'importazione di un'entità che dispone di una proprietà con un valore numerico in modo ambiguo, ad esempio "1" o "1.0", e utente hello prova toosend come un `Edm.String`, il valore di hello, verrà ripristinato tramite client hello API come un EDM
* Quando si importa il file CSV con i record su più righe, hello possano ottenere abbassate o crittografati

03/02/2016

### <a name="version-07201601291"></a>Versione 0.7.20160129.1

#### <a name="fixes"></a>Correzioni

* Miglioramento delle prestazioni complessive durante il caricamento, il download e la copia di BLOB

14/01/2016

### <a name="version-07201601050"></a>Versione 0.7.20160105.0

#### <a name="new"></a>Nuovo

* Supporto Linux (tooOSX funzionalità parità)
* Aggiunta di contenitori BLOB con la chiave di firma di accesso condiviso (SAS)
* Aggiunta degli account di archiviazione per Azure China
* Aggiunta di account di archiviazione con endpoint personalizzati
* Aprire e visualizzare il BLOB di testo e immagine contenuto hello
* Visualizzazione e modifica di metadati e proprietà di BLOB

#### <a name="fixes"></a>Correzioni

* Problema risolto: il caricamento o download un numero elevato di oggetti BLOB (500 +) in alcuni casi potrebbe essere hello app toohave uno schermo bianco 
* Problema risolto: quando si imposta il livello di accesso pubblico contenitore blob, hello nuovo valore non viene aggiornato finché non si imposta nuovamente lo stato attivo hello nel contenitore hello. Inoltre, finestra di dialogo hello verrà sempre troppo "non accesso pubblica" e non hello corrente il valore effettivo.
* Miglioramenti generali della tastiera/accessibilità e del supporto interfaccia utente
* Wrapping di testo della cronologia di navigazione quando è lungo con spazio
* La finestra di dialogo della firma di accesso condiviso supporta la convalida dell'input
* Archiviazione locale continua toobe disponibile anche se le credenziali utente sono scadute
* Durante l'eliminazione di un contenitore blob aperto Esplora blob hello sul lato destro hello è chiuso

#### <a name="known-issues"></a>Problemi noti

* Di seguito sono necessità di installare Linux versione gcc o aggiornata – tooupgrade passaggi: 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

18/11/2015
### <a name="version-07201511160"></a>Versione 0.7.20151116.0

#### <a name="new"></a>Nuovo

* Versioni per macOS e Windows
* Accedi tooview gli account di archiviazione: utilizzare l'Account aziendale, l'Account Microsoft, 2FA, e così via.
* Archivio di sviluppo locale (usare l'emulatore di archiviazione, solo Windows)
* Supporto di Azure Resource Manager e delle risorse Classic
* Creazione ed eliminazione di BLOB, code o tabelle
* Ricerca di BLOB, code o tabelle specifiche
* Esplorare il contenuto di hello di contenitori di blob
* Visualizzazione e spostamento tra directory
* Caricamento, download ed eliminazione di BLOB e cartelle
* Visualizzazione e modifica di metadati e proprietà di BLOB
* Generazione di chiavi di firma di accesso condiviso
* Gestione e creazione di SAP (Stored Access Policies)
* Ricerca di BLOB in base al prefisso
* Trascinare ' n' rilascio tooupload file o download

#### <a name="known-issues"></a>Problemi noti

* Quando si imposta il livello di accesso pubblico contenitore blob, nuovo valore hello non è aggiornato finché non si imposta nuovamente lo stato attivo hello nel contenitore hello
* Quando si apre a livello di accesso pubblico hello tooset hello finestra di dialogo, non viene sempre "Nessun accesso pubblico" come valore predefinito di hello e non hello effettivo valore corrente
* Impossibile rinominare i BLOB scaricati
* Le voci di log attività rimane talvolta "bloccato" in corso un stato quando si verifica un errore e non viene visualizzato errore hello
* Talvolta gli arresti anomali attiva completamente bianco durante il tentativo di tooupload o scarica un numero elevato di BLOB
* In alcuni casi l'annullamento di un'operazione di copia non funziona
* Durante la creazione di un contenitore (coda/blob o tabella), se è un nome non valido di input e procedere toocreate un altro in un tipo di contenitore diverso non è possibile impostare lo stato attivo sul nuovo tipo di hello
* Impossibile creare una nuova cartella o rinominare una cartella




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md