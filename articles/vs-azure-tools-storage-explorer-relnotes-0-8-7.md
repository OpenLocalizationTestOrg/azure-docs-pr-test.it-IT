---
title: aaaMicrosoft Azure Storage Explorer 0.8.7 (anteprima) | Documenti Microsoft
description: Note sulla versione di Microsoft Azure Storage Explorer 0.8.7 (anteprima)
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
ms.date: 01/18/2017
ms.author: cawa
ms.openlocfilehash: 9fdd491a3ea838e20f9d4f82c176cfb02fbe306b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-087-preview"></a>Microsoft Azure Storage Explorer 0.8.7 (anteprima)
## <a name="overview"></a>Panoramica
Questo articolo sono contenute le note sulla versione di hello Azure Storage Explorer 0.8.7 versione di anteprima.

[Esplora archivi di Microsoft Azure (anteprima)](./vs-azure-tools-storage-manage-with-storage-explorer.md) è un'applicazione autonoma che consente di utilizzare tooeasily dati di archiviazione di Azure in Windows, macOS e Linux.

## <a name="azure-storage-explorer-087-preview"></a>Azure Storage Explorer 0.8.7 (anteprima)
### <a name="download-azure-storage-explorer-087-preview"></a>Download di Azure Storage Explorer 0.8.7 (anteprima)
- [Azure Storage Explorer 0.8.7 Preview per Windows](https://go.microsoft.com/fwlink/?LinkId=708343)
- [Azure Storage Explorer 0.8.7 Preview per Mac](https://go.microsoft.com/fwlink/?LinkId=708342)
- [Azure Storage Explorer 0.8.7 Preview per Linux](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new-updates"></a>Nuovi aggiornamenti
* È possibile scegliere come conflitti tooresolve all'inizio di hello di un aggiornamento, scaricare o copiare sessione hello **attività** finestra.
* Passare il mouse su un percorso completo di hello toosee scheda della risorsa di archiviazione hello.
* Quando si fa clic su una scheda, sincronizza con posizione nel riquadro di spostamento sinistra hello.

### <a name="fixes"></a>Correzioni
* Corretto: Storage Explorer è ora un'app attendibile in macOS.
* Corretto: Ubuntu 14.04 è supportato nuovamente.
* Problema risolto: Talvolta hello aggiungere Account UI lampeggia quando il caricamento delle sottoscrizioni.
* Problema risolto: A volte non tutte le risorse di archiviazione sono state elencate nel riquadro di spostamento a sinistra di hello.
* Problema risolto: hello azione talvolta visualizzato riquadro azioni vuote.
* Problema risolto: dimensioni della finestra hello dalla sessione chiusa l'ultima volta hello viene ora mantenuta.
* Problema risolto: È possibile aprire più schede per hello stessa risorsa utilizzando il menu di scelta rapida hello.

### <a name="known-issues"></a>Problemi noti
* Accesso rapido funziona solo con gli elementi basati su sottoscrizione. Questa versione non supporta le risorse locali e le risorse collegate tramite chiave o token di firma di accesso condiviso.
* Accesso rapido può richiedere alcuni secondi toonavigate toohello risorsa di destinazione, a seconda di quanti di risorse.
* Più di tre gruppi di BLOB o i file di caricamento in hello stesso tempo può causare errori.
* È possibile eseguire la ricerca in un massimo di 50.000 nodi circa. Se si supera tale limite, le prestazioni potrebbero risultare peggiorate o potrebbero essere generate eccezioni non gestite.
* Per hello primo accesso tramite Esplora archivi hello in macOS, si potrebbero notare più prompt chiede portachiavi hello tooaccess di autorizzazione dell'utente. Si consiglia selezionare **Consenti sempre** in modo prompt hello non viene visualizzato nuovamente

## <a name="previous-releases"></a>Versioni precedenti
### <a name="features"></a>Funzionalità
#### <a name="main-features"></a>Funzionalità principali
* Versioni per macOS, Linux e Windows
* Accedi tooview gli account di archiviazione, raggruppati in base alla sottoscrizione:
    * Possibilità di usare l'account aziendale, l'account Microsoft, 2FA e così via
    * Configurazione e gestione delle impostazioni proxy
    * Rimozione di account tramite la disconnessione
* Collegare gli account tooStorage tramite:
    * Nome e chiave dell'account
    * Endpoint personalizzati (tra cui Azure Cina)
    * URI di firma di accesso condiviso per account di archiviazione
* Supporto di Azure Resource Manager e Archiviazione (versione classica)
* Generazione di chiavi di firma di accesso condiviso per BLOB, contenitori BLOB, code, tabelle o condivisioni file
* Connettere contenitori tooblob, code, tabelle o le condivisioni di file con la chiave di firma di accesso condiviso (SAS)
* Gestione di criteri di accesso archiviati per contenitori BLOB, code, tabelle o condivisioni file
* Archivio di sviluppo locale con l'emulatore di archiviazione (solo Windows)
* Creazione ed eliminazione di contenitori BLOB, code o tabelle
* Visualizzazione di contenitori BLOB $logs e tabelle $metrics
* Ricerca di BLOB, code, tabelle o condivisioni file specifiche
* Account toostorage collegamenti diretti o contenitori, code, tabelle o condivisioni di file per la condivisione e facilmente l'accesso alle risorse
* Ridenominazione di contenitori BLOB, tabelle e condivisioni file
* Toomanage possibilità e configurare le regole CORS
* Possibilità di copiare facilmente chiave primaria e secondaria per gli account di archiviazione
* Controlli di MD5 su caricamento e download per verificare l'integrità e la coerenza dei dati
* Ricerca per i contenitori blob, tabelle, code, condivisioni file o la casella di ricerca hello gli account di archiviazione
* È possibile ora pin utilizzati più frequentemente servizi toohello accesso rapido per semplificare la navigazione
* Possibilità di aprire più editor in schede diverse. A singolo clic tooopen una scheda temporanea. Fare doppio clic su una scheda permanente tooopen. È anche possibile scegliere toomake scheda temporaneo hello è una scheda permanente
* Miglioramenti evidenti a prestazioni e stabilità per operazioni di caricamento e download, soprattutto per file di grandi dimensioni in computer veloci
* Ci stiamo reintroduzione hello avanzata ambito di ricerca e il concetto di hello aggiunto di ambito. Immettere nodo tooa del percorso hello tramite l'icona di hello al passaggio del mouse, fare clic destro -> "Ricerca da qui", oppure manualmente tooscope tale nodo. Una volta con l'ambito, è possibile aggiungere un fine di toohello ricerca termini di ricerca toodeep hello a partire da tale nodo
* Sono stati aggiunti vari temi: Chiaro (impostazione predefinita), Scuro, Nero a contrasto elevato e Bianco a contrasto elevato.
* Passare tooEdit -> temi toochange le preferenze di temi
* In Linux è ora necessario un sistema operativo a 64 bit
* È stato aggiornato il logo
#### <a name="blobs"></a>Blobs
* Visualizzazione di BLOB e spostamento tra directory
* Caricamento, download, eliminazione e copia di BLOB e cartelle
* Aprire e visualizzare il BLOB di testo e immagine contenuto hello
* Visualizzazione e modifica di metadati e proprietà di BLOB
* Ricerca di BLOB in base al prefisso
* Creazione e interruzione di lease per BLOB e contenitori BLOB
* Trascinare ' n' drop tooupload file
* Ridenominazione di BLOB e cartelle
* Possibilità di creare cartelle vuote "virtuali" in contenitori BLOB
* È possibile modificare le proprietà di Blob e file hello
#### <a name="tables"></a>Tabelle
* Consente di visualizzare e di eseguire query sulle entità con ODATA o utilizzare query complesse toocreate generatore di query
* Aggiunta, modifica ed eliminazione di entità
* Importazione ed esportazione di contenuti di tabelle in formato CSV (inclusa l'esportazione dei risultati di query)
* Personalizzazione dell'ordine delle colonne
* Query toosave possibilità
#### <a name="queues"></a>Code
* Anteprima degli ultimi 32 messaggi
* Aggiunta, rimozione dalla coda e visualizzazione di messaggi
* Cancellazione della coda
* È consentito a si toodecide se si desidera tooencode/decodificare i messaggi in coda
#### <a name="file-shares"></a>Condivisioni file
* Visualizzazione di file e spostamento tra directory
* Caricamento, download, eliminazione e copia di file e directory
* Visualizzazione delle proprietà di file
* Ridenominazione di file e directory

### <a name="bug-fixes"></a>Correzioni di bug
* Corretto: problemi di blocco della schermata
* Corretto: sicurezza avanzata

### <a name="known-issues"></a>Problemi noti
* È possibile eseguire la ricerca in un massimo di 50.000 nodi circa. Se si supera tale limite, le prestazioni potrebbero risultare peggiorate. L'installazione di macOS può richiedere autorizzazioni elevate.
* Pannello impostazioni account può indicare che è necessario che le sottoscrizioni di toofilter credenziali tooreenter
* La ridenominazione di BLOB singoli o all'interno di un contenitore BLOB rinominato non mantiene gli snapshot. Tutte le altre proprietà e i metadati di BLOB, file ed entità vengono conservati durante un'operazione di ridenominazione.
* Stack di Azure attualmente non supporta i file, pertanto tentativo hello tooexpand **file** nodo genera un errore
* Per l'installazione di Linux 14.04 è necessaria la versione gcc aggiornata. Hello passaggi seguenti viene illustrato come tooupgrade:

```
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
```

### <a name="previous-versions"></a>Versioni precedenti
#### <a name="october-2016-release-version-085"></a>Versione di ottobre 2016 (versione 0.8.5)
* [Download per Windows](https://go.microsoft.com/fwlink/?LinkId=809306)
* [Download per Mac](https://go.microsoft.com/fwlink/?LinkId=809307)
* [Download per Linux](https://go.microsoft.com/fwlink/?LinkId=809308)
