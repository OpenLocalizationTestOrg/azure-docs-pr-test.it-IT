---
title: formato del file manifesto aaaAzure importazione/esportazione | Documenti Microsoft
description: "Informazioni sul formato hello del file manifesto dell'unità hello che descrive il mapping di hello tra BLOB nell'archiviazione Blob di Azure e i file in un'unità in un processo di importazione o esportazione nel servizio di importazione/esportazione hello."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f3119e1c-2c25-48ad-8752-a6ed4adadbb0
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: d7e5e1990482916f7ff5f891c97343b52e82b2f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-manifest-file-format"></a>Formato del file manifesto del servizio Importazione/Esportazione di Azure
file manifesto dell'unità Hello descrive il mapping di hello tra BLOB nell'archiviazione Blob di Azure e i file nell'unità che costituiscono un processo di importazione o esportazione. Per un'operazione di importazione, i file manifesto hello viene creato come parte del processo di Preparazione unità hello e viene archiviato nell'unità di hello prima unità hello viene inviato toohello data center di Azure. Durante un'operazione di esportazione, manifesto hello viene creato e archiviato nell'unità hello da hello servizio importazione/esportazione di Azure.  
  
Per importare entrambi e i processi di esportazione, file manifesto dell'unità hello viene archiviato in hello importare o esportare unità; non è trasmesso toohello servizio tramite un'operazione API.  
  
di seguito Hello sono formato generale di hello di un file manifesto dell'unità.  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveManifest Version="2014-11-01">  
  <Drive>  
    <DriveId>drive-id</DriveId>  
    import-export-credential  
  
    <!-- First Blob List -->  
    <BlobList>  
      <!-- Global properties and metadata that applies tooall blobs -->  
      [<MetadataPath Hash="md5-hash">global-metadata-file-path</MetadataPath>]  
      [<PropertiesPath   
        Hash="md5-hash">global-properties-file-path</PropertiesPath>]  
  
      <!-- First Blob -->  
      <Blob>  
        <BlobPath>blob-path-relative-to-account</BlobPath>  
        <FilePath>file-path-relative-to-transfer-disk</FilePath>  
        [<ClientData>client-data</ClientData>]  
        [<Snapshot>snapshot</Snapshot>]  
        <Length>content-length</Length>  
        [<ImportDisposition>import-disposition</ImportDisposition>]  
        page-range-list-or-block-list          
        [<MetadataPath Hash="md5-hash">metadata-file-path</MetadataPath>]  
        [<PropertiesPath Hash="md5-hash">properties-file-path</PropertiesPath>]  
      </Blob>  
  
      <!-- Second Blob -->  
      <Blob>  
      . . .  
      </Blob>  
    </BlobList>  
  
    <!-- Second Blob List -->  
    <BlobList>  
    . . .  
    </BlobList>  
  </Drive>  
</DriveManifest>  
  
import-export-credential ::=   
  <StorageAccountKey>storage-account-key</StorageAccountKey> | <ContainerSas>container-sas</ContainerSas>  
  
page-range-list-or-block-list ::=   
  page-range-list | block-list  
  
page-range-list ::=   
    <PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       Hash="md5-hash"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       Hash="md5-hash"/>]  
    </PageRangeList>  
  
block-list ::=  
    <BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       Hash="md5-hash"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       Hash="md5-hash"/>]  
    </BlockList>  

```

## <a name="manifest-xml-elements-and-attributes"></a>Elementi e attributi XML del manifesto

gli elementi dati Hello e gli attributi del formato XML del manifesto di hello unità vengono specificati in hello nella tabella seguente.  
  
|Elemento XML|Tipo|Descrizione|  
|-----------------|----------|-----------------|  
|`DriveManifest`|Elemento radice|elemento radice di Hello del file manifesto hello. Tutti gli altri elementi nel file hello sono di sotto di questo elemento.|  
|`Version`|Attributo, stringa|versione di Hello del file manifesto hello.|  
|`Drive`|Elemento XML nidificato|Contiene il manifesto di hello per ogni unità.|  
|`DriveId`|String|Identificatore univoco di Hello per unità hello. è stato trovato l'identificatore di unità Hello eseguendo una query su unità hello per il numero di serie. numero di serie di Hello unità è in genere stampato sul hello di fuori di anche unità hello. Hello `DriveID` elemento deve essere presente prima di qualsiasi `BlobList` nel file manifesto hello.|  
|`StorageAccountKey`|String|Necessaria per i processi di importazione se e solo se `ContainerSas` non è specificato. chiave dell'account per l'account di archiviazione Azure hello Hello associata al processo di hello.<br /><br /> Questo elemento viene omesso dal manifesto hello per un'operazione di esportazione.|  
|`ContainerSas`|String|Necessaria per i processi di importazione se e solo se `StorageAccountKey` non è specificato. contenitore di Hello SAS per accedere agli oggetti BLOB hello associato al processo hello. Vedere [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) per il formato. Questo elemento viene omesso dal manifesto hello per un'operazione di esportazione.|  
|`ClientCreator`|String|Specifica il client che ha creato hello XML file hello. Questo valore non viene interpretato dal servizio di importazione/esportazione hello.|  
|`BlobList`|Elemento XML nidificato|Contiene un elenco di blob che fanno parte dell'importazione hello o processo di esportazione. Ogni blob in un elenco condivisioni hello metadati e le stesse proprietà.|  
|`BlobList/MetadataPath`|String|Facoltativo. Specifica hello percorso relativo di un file su disco hello che contiene i metadati predefiniti hello che verranno impostati nei blob hello elenco per un'operazione di importazione. Questi metadati possono essere sostituiti facoltativamente un BLOB alla volta.<br /><br /> Questo elemento viene omesso dal manifesto hello per un'operazione di esportazione.|  
|`BlobList/MetadataPath/@Hash`|Attributo, stringa|Specifica valore hash MD5 codificato in base 16 di hello per file di metadati hello.|  
|`BlobList/PropertiesPath`|String|Facoltativo. Specifica hello percorso relativo di un file su disco hello che contiene proprietà predefinite di hello che verranno impostate nei blob hello elenco per un'operazione di importazione. Queste proprietà possono essere sostituite facoltativamente un BLOB alla volta.<br /><br /> Questo elemento viene omesso dal manifesto hello per un'operazione di esportazione.|  
|`BlobList/PropertiesPath/@Hash`|Attributo, stringa|Specifica valore hash MD5 codificato in base 16 di hello per i file delle proprietà hello.|  
|`Blob`|Elemento XML nidificato|Contiene informazioni su tutti i BLOB in tutti gli elenchi di BLOB.|  
|`Blob/BlobPath`|String|Hello relativo URI toohello blob, a partire dal nome di contenitore hello. Se il blob di hello è in un contenitore radice, deve iniziare con `$root`.|  
|`Blob/FilePath`|String|Specifica hello percorso relativo toohello file hello unità. Per i processi di esportazione, hello blob percorso verrà utilizzato per il percorso di file hello se possibile. *ad esempio*, `pictures/bob/wild/desert.jpg` verranno esportati troppo`\pictures\bob\wild\desert.jpg`. Tuttavia, a causa di limitazioni toohello dei nomi NTFS, un blob può essere esportato tooa file con un percorso simile a quello di percorso blob hello.|  
|`Blob/ClientData`|String|Facoltativo. Contiene i commenti del cliente hello. Questo valore non viene interpretato dal servizio di importazione/esportazione hello.|  
|`Blob/Snapshot`|DateTime|Opzionale per i processi di esportazione. Specifica l'identificatore hello per uno snapshot di blob esportato.|  
|`Blob/Length`|Integer|Specifica una lunghezza totale di hello del blob hello in byte. il valore di Hello potrebbe essere too200 GB per un blob in blocchi e backup too1 TB per un blob di pagine. Per un BLOB di pagine, questo valore deve essere multiplo di 512.|  
|`Blob/ImportDisposition`|String|Facoltativo per i processi di importazione, omesso per i processi di esportazione. Specifica come hello servizio importazione/esportazione deve gestire il caso di hello per un processo di importazione in cui è presente un blob con hello stesso nome esiste già. Se questo valore viene omesso dal manifesto di importazione hello, valore predefinito di hello è `rename`.<br /><br /> i valori Hello per questo elemento includono:<br /><br /> -   `no-overwrite`: Se un blob di destinazione è già presente con hello stesso nome, operazione di importazione hello ignorerà l'importazione di questo file.<br />-   `overwrite`: Qualsiasi blob di destinazione esistente viene completamente sovrascritto dal file appena importato hello.<br />-   `rename`: nuovo blob hello verrà caricato con un nome modificato.<br /><br /> ridenominazione regola Hello è indicato di seguito:<br /><br /> -Se il nome di blob hello non contiene un punto, viene generato un nuovo nome aggiungendo `(2)` toohello nome originale; se il nuovo nome è in conflitto con un nome di blob esistente, quindi `(3)` viene aggiunto al posto di `(2)`e così via.<br />-Se il nome di blob hello contiene un punto, parte hello dopo l'ultimo punto hello viene considerato come nome estensione hello. Toohello simile di sopra di routine, `(2)` viene inserita prima hello ultimo punto toogenerate un nuovo nome; se il nuovo nome hello è ancora in conflitto con un nome di blob esistente, il servizio hello tenta `(3)`, `(4)`e così via, finché una non in conflitto nome è stato trovato.<br /><br /> Di seguito sono riportati alcuni esempi:<br /><br /> blob Hello `BlobNameWithoutDot` verrà rinominato in:<br /><br /> `BlobNameWithoutDot (2)  // if BlobNameWithoutDot exists`<br /><br /> `BlobNameWithoutDot (3)  // if both BlobNameWithoutDot and BlobNameWithoutDot (2) exist`<br /><br /> blob Hello `Seattle.jpg` verrà rinominato in:<br /><br /> `Seattle (2).jpg  // if Seattle.jpg exists`<br /><br /> `Seattle (3).jpg  // if both Seattle.jpg and Seattle (2).jpg exist`|  
|`PageRangeList`|Elemento XML nidificato|Obbligatorio per un BLOB di pagine.<br /><br /> Per un'importazione, operazione specifica un elenco di intervalli di byte di un toobe file importato. Ogni intervallo di pagine è descritta da un offset e lunghezza nel file di origine hello che descrive l'intervallo di pagine hello, insieme a un hash MD5 dell'area di hello. Hello `Hash` è richiesto l'attributo di un intervallo di pagine. servizio Hello convaliderà hash hello dei dati di hello in blob hello corrispondente hash MD5 calcolato hello dall'intervallo di pagine hello. Qualsiasi numero di intervalli di pagine può essere toodescribe utilizzato un file per un'importazione, con dimensioni totali di hello backup too1 TB. Tutti gli intervalli di pagine devono essere ordinati tramite offset e non sono consentite sovrapposizioni.<br /><br /> Per un'operazione di esportazione, specifica un set di intervalli di byte di un blob che sono stati esportati toohello unità.<br /><br /> gli intervalli di pagine Hello loro insieme potrebbero coprire solo intervalli secondari di un blob o un file.  parte rimanente di Hello del file hello non coperto da un intervallo di pagine è prevista e il relativo contenuto può essere indefinito.|  
|`PageRange`|Elemento XML|Rappresenta un intervallo di pagine.|  
|`PageRange/@Offset`|Attributo, valore integer|Specifica di inizio offset hello in file di trasferimento hello e blob hello in hello specificato intervallo di pagine. Questo valore deve essere un multiplo di 512.|  
|`PageRange/@Length`|Attributo, valore integer|Specifica la lunghezza hello hello intervallo di pagine. Questo valore deve essere un multiplo di 512 e non superiore a 4 MB.|  
|`PageRange/@Hash`|Attributo, stringa|Specifica valore hash MD5 codificato in base 16 di hello per intervallo di pagine hello.|  
|`BlockList`|Elemento XML nidificato|Obbligatorio per un BLOB in blocchi con blocchi denominati.<br /><br /> Per un'operazione di importazione, elenco di blocchi di hello specifica un set di blocchi che verranno importati nell'archiviazione di Azure. Per un'operazione di esportazione, elenco di blocchi di hello specifica in ogni blocco è stato archiviato nel file hello su disco di esportazione di hello. Ogni blocco viene descritto tramite un offset nel file hello e una lunghezza di blocco. ogni blocco viene ulteriormente denominato da un attributo ID di blocco e contiene un hash MD5 per il blocco di hello. Backup too50, 000 blocchi possono essere utilizzato toodescribe un blob.  Tutti i blocchi devono essere ordinati tramite offset e nel loro insieme dovrebbero coprire la gamma completa di hello del file hello, *ovvero*, tra i blocchi devono essere presenti gap. Se il blob di hello è non più di 64 MB, ID di blocco hello per ogni blocco deve essere tutti assenti o presentare tutte. Gli ID di blocco sono stringhe con codifica Base64 toobe obbligatorio. Per gli altri requisiti sugli ID del blocco, vedere [Put Block](/rest/api/storageservices/put-block) (Blocco Put).|  
|`Block`|Elemento XML|Rappresenta un blocco.|  
|`Block/@Offset`|Attributo, valore integer|Specifica l'offset di hello inizio blocco specificato hello.|  
|`Block/@Length`|Attributo, valore integer|Specifica il numero di hello di byte nel blocco hello; Questo valore deve essere non più di 4MB.|  
|`Block/@Id`|Attributo, stringa|Specifica una stringa che rappresenta hello ID di blocco per blocco hello.|  
|`Block/@Hash`|Attributo, stringa|Specifica l'hash MD5 codificato in base 16 hello del blocco di hello.|  
|`Blob/MetadataPath`|String|Facoltativo. Specifica hello percorso relativo di un file di metadati. Durante un'importazione dei metadati di hello sono impostato sul blob di destinazione hello. Durante un'operazione di esportazione dei metadati del blob hello viene archiviato nel file di metadati hello nell'unità di hello.|  
|`Blob/MetadataPath/@Hash`|Attributo, stringa|Specifica l'hash MD5 codificato in base 16 hello del file di metadati del blob hello.|  
|`Blob/PropertiesPath`|String|Facoltativo. Specifica hello percorso relativo di un file di proprietà. Durante l'importazione, hello vengono impostate nel blob di destinazione hello. Durante un'operazione di esportazione delle proprietà del blob hello vengono archiviate nel file di proprietà hello nell'unità di hello.|  
|`Blob/PropertiesPath/@Hash`|Attributo, stringa|Specifica l'hash MD5 codificato in base 16 hello del file delle proprietà del blob hello.|  
  
## <a name="next-steps"></a>Passaggi successivi
 
* [Storage Import/Export REST API](/rest/api/storageimportexport/) (API REST di importazione/esportazione dell'archiviazione)
