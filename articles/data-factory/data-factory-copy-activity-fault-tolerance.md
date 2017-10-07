---
title: "tolleranza di errore aaaAdd nell'attività di copia di Azure Data Factory ignorando righe incompatibile | Documenti Microsoft"
description: "Informazioni su come tooadd la tolleranza di errore nell'attività di copia di Azure Data Factory ignorando righe incompatibile durante la copia"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a>Aggiungere la tolleranza di errore all'attività di copia ignorando le righe incompatibili

Azure Data Factory [attività di copia](data-factory-data-movement-activities.md) sono disponibili righe di due modi toohandle incompatibili quando si copiano dati tra archivi dati di origine e sink:

- È possibile interrompere e avere esito negativo copia hello verificato durante l'attività quando sono dati non compatibili (comportamento predefinito).
- È possibile continuare toocopy tutti i dati di hello aggiungendo la tolleranza di errore e ignorare le righe di dati incompatibili. Inoltre, è possibile registrare righe incompatibile hello nell'archiviazione Blob di Azure. È quindi possibile esaminare hello log toolearn hello causa dell'errore hello, correggere i dati di hello sull'origine dati hello e ripetere l'attività di copia hello.

## <a name="supported-scenarios"></a>Scenari supportati
L'attività di copia supporta tre scenari per rilevare, ignorare e registrare i dati incompatibili:

- **Incompatibilità tra hello tipo di dati di origine e il tipo nativo sink hello**

    Ad esempio: copia dati da un file CSV in archiviazione di Blob tooa SQL del database con una definizione di schema che contiene tre **INT** colonne di tipo. righe di file CSV contenenti dati numerici, ad esempio Hello `123,456,789` vengono copiati correttamente archivio sink toohello. Tuttavia, hello righe che contengono valori non numerici, ad esempio `123,456,abc` vengono rilevati come incompatibili e vengono ignorati.

- **Mancata corrispondenza nel numero hello di colonne tra hello origine e sink di hello**

    Ad esempio: copia dati da un file CSV in archiviazione di Blob tooa SQL del database con una definizione di schema che contiene sei colonne. Hello file CSV le righe che contengono sei colonne vengono copiati correttamente archivio sink toohello. righe di file CSV Hello che contengono meno di sei o più colonne vengono rilevate come incompatibile e vengono ignorate.

- **Violazione della chiave primaria per la scrittura di database relazionale tooa**

    Ad esempio: copiare i dati da un database SQL di SQL server tooa. Nel database SQL di sink hello è definita una chiave primaria, ma tale chiave non primaria è definito in hello origine di SQL server. righe Hello duplicato presenti nell'origine hello non possono essere copiato toohello sink. Attività di copia copia solo hello prima riga dei dati di origine hello in sink hello. Hello sorgente successiva le righe che contengono il valore di chiave primaria di hello duplicato vengono rilevate come incompatibile e vengono ignorate.

## <a name="configuration"></a>Configurazione
Hello esempio seguente viene fornito un tooconfigure definizione JSON ignorare hello incompatibili nell'attività di copia:

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },         
    "enableSkipIncompatibleRow": true,           
    "redirectIncompatibleRowSettings": {
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| Proprietà | Descrizione | Valori consentiti | Obbligatorio |
| --- | --- | --- | --- |
| **enableSkipIncompatibleRow** | Specificare se ignorare o meno le righe incompatibili durante la copia. | True<br/>False (impostazione predefinita) | No |
| **redirectIncompatibleRowSettings** | Un gruppo di proprietà che può essere specificato quando si desidera che le righe non compatibile di toolog hello. | &nbsp; | No |
| **linkedServiceName** | servizio collegato Hello del log di hello toostore di archiviazione di Azure che contiene righe hello ignorata. | nome Hello un [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) o [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) servizio, che fa riferimento toohello istanza di archiviazione che si desidera file di log toouse toostore hello collegato. | No |
| **path** | percorso di Hello hello del file di log che contiene hello ignorato righe. | Specificare percorso di archiviazione Blob hello che dati non compatibili di toouse toolog hello. Se non si specifica un percorso, il servizio hello crea un contenitore. | No |

## <a name="monitoring"></a>Monitoraggio
Al termine dell'esecuzione dell'attività hello copia, è possibile visualizzare il numero di hello delle righe ignorate nella sezione monitoraggio hello:

![Monitorare le righe incompatibili ignorate](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

Se si configurano le righe non compatibile di hello toolog, è possibile trovare il file di log hello in questo percorso: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` nel file di log hello, è possibile visualizzare le righe che sono state ignorate hello e hello a causa di incompatibilità hello.

Dati originali hello sia errore corrispondente hello vengono registrate nel file hello. Un esempio di contenuto del file di log hello è come segue:
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni sull'attività di copia di Azure Data Factory, vedere [spostare i dati utilizzando l'attività di copia](data-factory-data-movement-activities.md).
