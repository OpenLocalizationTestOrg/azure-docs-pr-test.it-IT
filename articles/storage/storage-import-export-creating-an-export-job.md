---
title: aaaCreate un'esportazione processo di importazione/esportazione di Azure | Documenti Microsoft
description: Informazioni su come toocreate un'esportazione del processo per il servizio di importazione/esportazione di Microsoft Azure hello.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a>Creazione di un processo di esportazione per hello servizio importazione/esportazione di Azure
La creazione di un processo di esportazione per il servizio di importazione/esportazione di Microsoft Azure hello utilizzando hello API REST prevede hello alla procedura seguente:

-   Selezione di hello BLOB tooexport.

-   Acquisizione di una località di spedizione.

-   Creazione del processo di esportazione hello.

-   Spedizione tooMicrosoft le unità vuote tramite un servizio vettore supportato.

-   Aggiornamento del processo di esportazione hello con informazioni sul pacchetto hello.

-   Ricezione di hello unità da Microsoft.

 Vedere [tramite servizio di importazione/esportazione di Azure hello, dati tooTransfer tooBlob archiviazione](storage-import-export-service.md) per una panoramica del servizio di importazione/esportazione hello e un'esercitazione che illustra come hello toouse [portale di Azure](https://portal.azure.com/) toocreate e gestire l'importazione e i processi di esportazione.

## <a name="selecting-blobs-tooexport"></a>Selezione di BLOB tooexport
 toocreate un processo di esportazione, sarà necessario tooprovide un elenco di blob che si desidera tooexport dall'account di archiviazione. Esistono alcuni modi tooselect BLOB toobe esportate:

-   È possibile utilizzare un tooselect percorso blob relativo a un singolo blob e tutti i relativi snapshot.

-   È possibile utilizzare un tooselect percorso blob relativo di un singolo blob esclusi i relativi snapshot.

-   È possibile utilizzare un percorso blob relativo e un tooselect tempo snapshot un singolo snapshot.

-   È possibile utilizzare un tooselect prefisso blob tutti i BLOB e snapshot con hello prefisso specificato.

-   È possibile esportare tutti i BLOB e snapshot nell'account di archiviazione hello.

 Per ulteriori informazioni sulla specifica BLOB tooexport, vedere hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operazione.

## <a name="obtaining-your-shipping-location"></a>Acquisizione della località di spedizione
Prima di creare un processo di esportazione, è necessario tooobtain il nome di un'ubicazione di spedizione e l'indirizzo dal chiamante hello [ottenere percorso](https://portal.azure.com) o [List Locations](/rest/api/storageimportexport/listlocations) operazione. `List Locations` restituirà un elenco di località con gli indirizzi postali. È possibile selezionare un'ubicazione hello elenco restituito e spedire il tuo indirizzo toothat unità disco rigido. È inoltre possibile utilizzare hello `Get Location` hello tooobtain operazione indirizzo per una determinata ubicazione di spedizione direttamente.

Seguire i passaggi di hello sotto tooobtain ubicazione di spedizione hello:

-   Identificare il nome di hello del percorso hello dell'account di archiviazione. Questo valore è reperibile nella hello **percorso** campo dell'account di archiviazione hello **Dashboard** classica hello portale o eseguendo una query utilizzando Gestione servizio hello operazione API [ottenere Proprietà Account di archiviazione](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).

-   Recuperare questo account di archiviazione percorso hello che sono disponibili tooprocess hello chiamante `Get Location` operazione.

-   Se hello `AlternateLocations` proprietà della posizione di hello contiene percorso hello stesso, quindi è corretto toouse questo percorso. In caso contrario, chiamare hello `Get Location` operazione con una delle posizioni alternative hello. percorso originale Hello potrebbe essere chiusa temporaneamente per la manutenzione.

## <a name="creating-hello-export-job"></a>Creazione del processo di esportazione hello
 processo di esportazione hello toocreate, chiamata hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operazione. È necessario hello tooprovide le seguenti informazioni:

-   Un nome per il processo di hello.

-   nome di account di archiviazione Hello.

-   Hello shipping nome dell'ubicazione, ottenuto nel passaggio precedente hello.

-   Un tipo di processo (esportazione).

-   indirizzo del mittente Hello dove hello unità devono essere inviate al termine il processo di esportazione hello.

-   Hello toobe elenco di BLOB (o prefissi di blob) esportato.

## <a name="shipping-your-drives"></a>Spedizione delle unità
 Successivamente, utilizzare hello strumento di importazione/esportazione di Azure toodetermine hello numero di unità che è necessario toosend, in base a BLOB hello selezionati toobe esportato e hello dimensioni dell'unità. Vedere hello [riferimento allo strumento di importazione/esportazione di Azure](storage-import-export-tool-how-to-v1.md) per informazioni dettagliate.

 Unità di hello pacchetto in un singolo pacchetto e spedirle toohello indirizzo ottenuto nel hello passaggio precedente. Si noti hello tenere traccia del numero del pacchetto per il passaggio successivo hello.

> [!NOTE]
>  È necessario spedire le unità con un vettore supportato, che fornirà un numero di tracciabilità per il pacchetto.

## <a name="updating-hello-export-job-with-your-package-information"></a>Aggiornamento del processo di esportazione di hello con le informazioni sul pacchetto
 Dopo aver ottenuto il numero di tracciabilità, chiamare hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operazione tooupdated hello vettore nome e il numero di hello processo di rilevamento. È possibile specificare facoltativamente il numero di hello di unità, l'indirizzo restituito hello e data di spedizione hello.

## <a name="receiving-hello-package"></a>Ricezione di pacchetti hello
 Dopo il processo di esportazione è stato elaborato, le unità verranno restituite tooyou con i dati crittografati. È possibile recuperare la chiave di BitLocker hello per ognuna delle unità hello dal chiamante hello [recupero del processo](/rest/api/storageimportexport/jobs#Jobs_Get) operazione. È quindi possibile sbloccare l'unità hello hello chiave. file manifesto dell'unità di Hello su ciascuna unità contiene hello elenco di file in unità hello, come indirizzo blob originale hello per ogni file.

## <a name="next-steps"></a>Passaggi successivi

* [Tramite l'API REST del servizio importazione/esportazione hello](storage-import-export-using-the-rest-api.md)
