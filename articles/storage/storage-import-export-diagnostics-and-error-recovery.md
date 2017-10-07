---
title: ripristino aaaDiagnostics e di errore per i processi di importazione/esportazione di Azure | Documenti Microsoft
description: Informazioni su come i processi del servizio tooenable la registrazione dettagliata per importazione/esportazione di Microsoft Azure.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 096cc795-9af6-4335-9fe8-fffa9f239a17
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 48164279e7904c78fed802aa3cff66e589c3f12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a>Diagnostica e ripristino dagli errori per i processi di Importazione/Esportazione di Azure
Per ogni unità elaborata, hello servizio importazione/esportazione di Azure crea un log degli errori nell'account di archiviazione hello associata. È inoltre possibile abilitare la registrazione dettagliata per l'impostazione hello `LogLevel` proprietà troppo`Verbose` quando si chiama hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) o [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operazioni.

 Per impostazione predefinita, i log vengono scritti tooa contenitore denominato `waimportexport`. È possibile specificare un nome diverso dall'impostazione hello `DiagnosticsPath` proprietà quando si chiama hello `Put Job` o `Update Job Properties` operazioni. Hello i log vengono archiviati come BLOB in blocchi con hello convenzione di denominazione seguente: `waies/jobname_driveid_timestamp_logtype.xml`.

 È possibile recuperare hello URI dei log di hello per un processo dal chiamante hello [recupero del processo](/rest/api/storageimportexport/jobs#Jobs_Get) operazione. Hello URI per il log dettagliato hello viene restituito in hello `VerboseLogUri` proprietà per ogni unità, mentre hello URI hello log degli errori viene restituito in hello `ErrorLogUri` proprietà.

È possibile utilizzare hello hello tooidentify dati seguenti problemi di registrazione.

## <a name="drive-errors"></a>Errori delle unità

Hello seguenti elementi viene classificato come errori del disco:

-   Errori di accesso o lettura hello file manifesto

-   Chiavi BitLocker non corrette

-   Errori di lettura/scrittura delle unità

## <a name="blob-errors"></a>Errori del BLOB

Hello seguenti elementi viene classificato come errori di blob:

-   BLOB o nomi non corretti o in conflitto

-   File mancanti

-   BLOB non trovato

-   File troncati (file hello hello disco sono inferiori rispetto a quanto specificato nel manifesto hello)

-   Contenuto dei file danneggiato (per i processi di importazione, rilevato con un checksum MD5 non corrispondente)

-   File di metadati e proprietà BLOB danneggiati (rilevati con un checksum MD5 non corrispondente)

-   Schema errato per le proprietà del blob hello e/o file di metadati

Potrebbero essere presenti i casi in cui alcune parti di un processo di importazione o esportazione non completata correttamente, mentre hello complessiva positivo del processo. In questo caso, è possibile caricare o scaricare hello mancante porzioni di dati hello in rete oppure è possibile creare un nuovo dati hello tootransfer di processo. Vedere hello [riferimento allo strumento di importazione/esportazione di Azure](storage-import-export-tool-how-to-v1.md) toolearn come toorepair hello dati in rete.

## <a name="next-steps"></a>Passaggi successivi

* [Tramite l'API REST del servizio importazione/esportazione hello](storage-import-export-using-the-rest-api.md)
