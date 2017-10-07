---
title: origini dei dati in Azure Data Catalog aaaRegister | Documenti Microsoft
description: In questo articolo evidenzia la tooregister origini di dati in Azure Data Catalog, inclusi i campi di metadati hello estrazione durante la registrazione.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: bab89906-186f-4d35-9ffd-61b1d903905d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: efc8a852ddc9fb4bbacc7b0280477bd47814936f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-sources-in-azure-data-catalog"></a>Registrare le origini dati in Azure Data Catalog
## <a name="introduction"></a>Introduzione
Azure Data Catalog è un servizio cloud completamente gestito che funge da sistema di registrazione e di individuazione per le origini dati aziendali. In altre parole, Data Catalog permette agli utenti di trovare, comprendere e usare le origini dati e consente alle organizzazioni di ottenere maggior valore dai dati esistenti. primo passaggio toomaking un'origine dati Hello individuabili tramite catalogo dati tooregister di è che l'origine dati.

## <a name="register-data-sources"></a>Registrare le origini dati
La registrazione è il processo di hello di estrazione dei metadati dall'origine dati hello e la copia di tale servizio Catalogo dati di toohello di dati. Hello dati restano in cui risiede e rimane in Criteri di sistema corrente hello e controllo hello degli amministratori di hello.

un'origine dati, tooregister hello seguenti:
1. Nel portale di Azure Data Catalog hello avviare strumento per la registrazione di origine dati di hello catalogo dati. 
2. Accedere con l'account aziendale o dell'istituto di istruzione con hello stesso che si usa toosign nel portale di toohello le credenziali di Azure Active Directory.
3. Selezionare l'origine dati di hello da tooregister.

Per ulteriori informazioni dettagliate, vedere hello [Guida introduttiva di Azure Data Catalog](data-catalog-get-started.md) esercitazione.

Dopo aver registrato origine dati hello, catalogo hello tiene traccia di posizione e indicizza i propri metadati. Gli utenti possono eseguire la ricerca, Sfoglia e individua l'origine dati hello e quindi usare relativo tooit tooconnect percorso tramite l'applicazione hello o lo strumento di propria scelta.

## <a name="supported-data-sources"></a>Origini dati supportate
Per un elenco di origini dati attualmente supportate, vedere [Riferimento per l'origine dati di Azure Data Catalog](data-catalog-dsr.md).

## <a name="structural-metadata"></a>Metadati strutturali
Quando si registra un'origine dati, lo strumento di registrazione hello estrae le informazioni sulla struttura hello degli oggetti hello selezionati. Queste informazioni sono metadati strutturali tooas cui viene fatto riferimento.

Per tutti gli oggetti, questi metadati strutturali includeranno il percorso dell'oggetto hello, in modo che gli utenti individuare dati hello possono utilizzare l'oggetto di informazioni tooconnect toohello negli strumenti client hello di propria scelta. Altri metadati strutturali includono il tipo e il nome dell'oggetto e il nome di colonna/attributo e il tipo di dati.

## <a name="descriptive-metadata"></a>Metadati descrittivi
Inoltre toohello core metadati strutturali estratti dall'origine dati hello, strumento di registrazione di origine dati hello estrae i metadati descrittivi. Per SQL Server Analysis Services e SQL Server Reporting Services, questi metadati viene ricavato dalla proprietà della descrizione hello esposte da questi servizi. Per SQL Server, i valori forniti tramite ms hello\_Descrizione proprietà estesa viene estratto. Per Database Oracle, hello origine dati registrazione strumento estrae hello colonna COMMENTS da hello tutti\_scheda\_Visualizza i commenti.

In aggiunta toohello metadati descrittivi estratti dall'origine dati hello, utenti possono immettere metadati descrittivi mediante strumento di registrazione di origine dati hello. Gli utenti possono aggiungere tag e consentono di identificare gli esperti per gli oggetti hello in corso la registrazione. Tutti questi metadati descrittivi sono copiati servizio Catalogo dati toohello insieme ai metadati strutturali hello.

## <a name="include-previews"></a>Includere le anteprime
Per impostazione predefinita, solo i metadati vengono estratti da origini dati e copiato toohello servizio Catalogo dati, ma comprensione di che un'origine dati è spesso semplificata quando è possibile visualizzare un campione di dati hello in che esso contenuti.

Tramite lo strumento di registrazione hello catalogo dati dell'origine dati, è possibile includere un'anteprima di snapshot dei dati hello in ogni tabella e vista in cui è registrato. Se si scelgono di anteprime tooinclude durante la registrazione, lo strumento di registrazione hello include too20 record da ogni tabella o vista. Lo snapshot viene quindi copiato catalogo toohello insieme ai metadati di hello strutturale e descrittivo.

> [!NOTE]
> Nell'anteprima delle tabelle di grandi dimensioni con un numero elevato di colonne potrebbero essere inclusi meno di 20 record.
>
>

## <a name="include-data-profiles"></a>Includere i profili dei dati
Come anteprime inclusione possono fornire contesto importante per gli utenti di eseguire la ricerca di origini dati nel catalogo dati, tra cui un profilo di dati può rendere più semplice le origini dati toounderstand individuati.

Tramite lo strumento di registrazione hello catalogo dati dell'origine dati, è possibile includere un profilo dati per ogni tabella e vista in cui è registrato. Se si sceglie un profilo dati tooinclude durante la registrazione, lo strumento di registrazione hello include statistiche aggregate sui dati hello in ogni tabella o vista, tra cui:

* numero di Hello di righe e le dimensioni dei dati di hello nell'oggetto hello.
* Data Hello hello di aggiornamento più recente dei dati di hello e lo schema dell'oggetto hello.
* numero di Hello di record null e i valori distinti per le colonne.
* Hello minima, massima, Media e deviazione standard valori per le colonne.

Queste statistiche vengono quindi copiate catalogo toohello insieme ai metadati di hello strutturale e descrittivo.

> [!NOTE]
> Le colonne del testo e della data non includono le statistiche della media o della deviazione standard nel profilo dei dati.
>
>

## <a name="update-registrations"></a>Aggiornare le registrazioni
Registrazione di un'origine dati rende individuabili nel catalogo dati quando si utilizzano i metadati di hello e anteprima facoltativo estratti durante la registrazione. Se l'origine dati hello toobe aggiornate nel catalogo di hello (ad esempio, se hello schema di un oggetto è stato modificato, originariamente escluse tabelle devono essere incluse, oppure da dati hello tooupdate inclusi nelle anteprime hello), è necessario strumento per la registrazione di origine dati hello può essere eseguita nuovamente.

La nuova registrazione di un'origine dati già registrata esegue un'operazione di unione "upsert": gli oggetti esistenti vengono aggiornati e i nuovi oggetti vengono creati. I metadati forniti dagli utenti tramite il portale di catalogo dati hello vengono mantenuti.

## <a name="summary"></a>Riepilogo
Poiché i metadati strutturali e descrittivo copia da un servizio di catalogo toohello origine dati, la registrazione di origine dati hello nel catalogo dati rende più facile toodiscover di hello dati e comprendere. Dopo aver registrato l'origine dati hello, è possibile annotare, gestire e individuandolo utilizzando il portale di catalogo dati hello.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sulla registrazione di origini dati, vedere hello [Guida introduttiva di Azure Data Catalog](data-catalog-get-started.md) esercitazione.
