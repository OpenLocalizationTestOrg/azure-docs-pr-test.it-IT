---
title: aaaCreate un processo di importazione per importazione/esportazione di Azure | Documenti Microsoft
description: Informazioni su come toocreate un'importazione per hello servizio importazione/esportazione di Microsoft Azure.
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a>Creazione di un processo di importazione per hello servizio importazione/esportazione di Azure

La creazione di un processo di importazione per il servizio di importazione/esportazione di Microsoft Azure hello utilizzando hello API REST prevede hello alla procedura seguente:

-   Preparazione delle unità con hello strumento di importazione/esportazione di Azure.

-   Ottenere hello percorso toowhich tooship hello unità.

-   Creazione del processo di importazione hello.

-   Shipping hello unità tooMicrosoft tramite un servizio vettore supportato.

-   Aggiornamento del processo di importazione hello con hello Dettagli spedizione.

 Vedere [tramite servizio di importazione/esportazione di Microsoft Azure hello, dati tooTransfer tooBlob archiviazione](storage-import-export-service.md) per una panoramica del servizio di importazione/esportazione hello e un'esercitazione che illustra come hello toouse [portale di Azure](https://portal.azure.com/) toocreate e gestire l'importazione e i processi di esportazione.

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a>Preparazione delle unità con hello strumento di importazione/esportazione di Azure

Hello passaggi tooprepare unità per un processo di importazione sono hello stesso se si crea hello portale hello jobvia o tramite hello API REST.

Di seguito è riportata una breve panoramica della preparazione dell'unità. Fare riferimento toohello [Azure importazione ExportTool riferimento](storage-import-export-tool-how-to-v1.md) per istruzioni complete. È possibile scaricare lo strumento di importazione/esportazione di Azure hello [qui](http://go.microsoft.com/fwlink/?LinkID=301900).

La preparazione dell'unità comporta:

-   Identificazione hello toobe di dati importati.

-   Identificazione dei blob di destinazione hello in archiviazione di Azure.

-   Utilizzo di hello strumento di importazione/esportazione di Azure toocopy tooone i dati o più dischi rigidi.

 Hello strumento di importazione/esportazione di Azure genererà inoltre un file manifesto per ognuna delle unità hello preparata. Contiene un file manifesto:

-   Enumerazione di tutti i file hello destinato al caricamento e il mapping di hello da tooblobs questi file.

-   Checksum dei segmenti di hello di ogni file.

-   Informazioni su tooassociate hello di proprietà e i metadati con ogni blob.

-   Un elenco di hello azione tootake se dispone di un blob che è in fase di caricamento hello stesso nome di un blob esistente nel contenitore hello. Le opzioni possibili sono: a) sovrascrivere il blob hello con file hello, b) mantenere il blob esistente hello e ignorare il caricamento di file hello, c) aggiungere un nome di toohello suffisso in modo che non è in conflitto con altri file.

## <a name="obtaining-your-shipping-location"></a>Acquisizione della località di spedizione

Prima di creare un processo di importazione, è necessario tooobtain il nome di un'ubicazione di spedizione e l'indirizzo dal chiamante hello [List Locations](/rest/api/storageimportexport/listlocations) operazione. `List Locations` restituirà un elenco di località con gli indirizzi postali. È possibile selezionare un'ubicazione hello elenco restituito e spedire il tuo indirizzo toothat unità disco rigido. È inoltre possibile utilizzare hello `Get Location` hello tooobtain operazione indirizzo per una determinata ubicazione di spedizione direttamente.

 Seguire i passaggi di hello sotto tooobtain ubicazione di spedizione hello:

-   Identificare il nome di hello del percorso hello dell'account di archiviazione. Questo valore è reperibile nella hello **percorso** campo dell'account di archiviazione hello **Dashboard** nel portale di Azure o eseguendo una query utilizzando Gestione servizio hello operazione API hello [ottenere archiviazione Proprietà dell'account](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).

-   Recuperare questo account di archiviazione di percorso hello tooprocess disponibile dal chiamante hello `Get Location` operazione.

-   Se hello `AlternateLocations` proprietà della posizione di hello contiene percorso hello stesso, quindi è corretto toouse questo percorso. In caso contrario, chiamare hello `Get Location` operazione con una delle posizioni alternative hello. percorso originale Hello potrebbe essere chiusa temporaneamente per la manutenzione.

## <a name="creating-hello-import-job"></a>Creazione del processo di importazione hello
processo di importazione hello toocreate, chiamata hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operazione. È necessario hello tooprovide le seguenti informazioni:

-   Un nome per il processo di hello.

-   nome di account di archiviazione Hello.

-   Hello shipping nome dell'ubicazione, ottenuta nel passaggio precedente hello.

-   Un tipo di processo (importazione).

-   indirizzo del mittente Hello dove hello unità devono essere inviate una volta completato il processo di importazione hello.

-   elenco di Hello di unità nel processo di hello. Per ogni unità, è necessario includere le seguenti informazioni che è state ottenute durante il passaggio di Preparazione unità hello hello:

    -   Id dell'unità Hello

    -   chiave di BitLocker Hello

    -   percorso relativo del file manifesto Hello sul disco rigido hello

    -   file manifesto MD5 hash con codifica in base 16 Hello

## <a name="shipping-your-drives"></a>Spedizione delle unità
È necessario fornire l'indirizzo toohello unità che ottenuta nel passaggio precedente hello ed è necessario fornire hello servizio importazione/esportazione con numero di pacchetti hello rilevamento hello.

> [!NOTE]
>  È necessario spedire le unità con un vettore supportato, che fornirà un numero di tracciabilità per il pacchetto.

## <a name="updating-hello-import-job-with-your-shipping-information"></a>Aggiornamento del processo di importazione di hello con le informazioni di spedizione
Dopo aver ottenuto il numero di tracciabilità, chiamare hello [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) hello tooupdate operazione shipping nome del gestore telefonico, il numero di tracciabilità hello per processo hello e numero di conto hello vettore per la spedizione di ritorno. È facoltativamente possibile specificare il numero di hello di unità e hello nonché data di spedizione.

## <a name="next-steps"></a>Passaggi successivi

* [Tramite l'API REST del servizio importazione/esportazione hello](storage-import-export-using-the-rest-api.md)
