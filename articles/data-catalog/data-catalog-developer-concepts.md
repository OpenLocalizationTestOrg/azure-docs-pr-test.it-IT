---
title: concetti per sviluppatori di catalogo aaaData | Documenti Microsoft
description: I concetti chiave introduzione toohello nel modello concettuale di Azure Data Catalog esposto tramite hello API REST di catalogo.
services: data-catalog
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
tags: 
ms.assetid: 89de9137-a0a4-40d1-9f8d-625acad31619
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: d0b1628ff6c31458cb650efef852244f0c139b1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-developer-concepts"></a>Concetti per sviluppatori del Catalogo dati di Azure
**Catalogo dati di Microsoft Azure** è un servizio cloud completamente gestito che offre funzionalità di individuazione dell'origine dati e di crowdsourcing dei metadati dell'origine dati. Gli sviluppatori possono utilizzare il servizio di hello tramite le relative API REST. Informazioni sui concetti di hello implementati nel servizio hello è importante per gli sviluppatori di integrare toosuccessfully **Azure Data Catalog**.

## <a name="key-concepts"></a>Concetti chiave
Hello **Azure Data Catalog** modello concettuale si basa su quattro concetti chiavi: hello **catalogo**, **utenti**, **asset**e **Annotazioni**.

![concetto][1]

*Figura 1. Modello concettuale semplificato del Catalogo dati di Azure*

### <a name="catalog"></a>Catalogo
Oggetto **catalogo** è contenitore di livello superiore di hello per tutti hello metadati archivia un'organizzazione. Per ogni account Azure è consentito un solo **catalogo**. I cataloghi vengono collegati tooan sottoscrizione di Azure, ma solo uno **catalogo** può essere creato per qualsiasi account di Azure specificato, anche se un account può disporre di più sottoscrizioni.

Un catalogo contiene **utenti** e **asset**.

### <a name="users"></a>Utenti
Gli utenti sono entità di sicurezza che richiedono autorizzazioni tooperform azioni (catalogo di hello, aggiungere, modificare o rimuovere gli elementi e così via) in hello catalogo.

Diversi sono i ruoli disponibili che un utente può avere. Per informazioni sui ruoli, vedere la sezione hello ruoli e l'autorizzazione.

È possibile aggiungere singoli utenti e gruppi di sicurezza.

Il Catalogo dati di Azure usa Azure Active Directory per la gestione delle identità e degli accessi. Ogni utente del catalogo deve essere un membro di hello Active Directory per conto di hello.

### <a name="assets"></a>Asset
Il **catalogo** contiene gli asset di dati. **Asset** sono unità hello di granularità gestita dal catalogo hello.

granularità di Hello di un cespite varia in base origine dati. Per database Oracle o SQL Server un asset può essere una tabella o una vista. Per SQL Server Analysis Services un asset può essere una misura, una dimensione o un indicatore di prestazioni chiave (KPI). Per SQL Server Reporting Services un asset è un report.

Un **Asset** hello cosa si aggiungono o rimuovono da un catalogo. È unità hello del risultato si ottiene da **ricerca**.

L' **asset** è composto dal relativo nome, dal percorso, dal tipo e dalle annotazioni che lo descrivono ulteriormente.

### <a name="annotations"></a>annotazioni
Le annotazioni sono elementi che rappresentano i metadati relativi agli asset.

Descrizioni, tag, schemi, documentazione e così via sono esempi di annotazioni. Un elenco completo dei tipi di asset hello e annotazione sono nella sezione del modello oggetto Asset hello.

## <a name="crowdsourcing-annotations-and-user-perspective-multiplicity-of-opinion"></a>Annotazioni crowdsourcing e prospettiva dell'utente (molteplicità di opinione)
Un aspetto chiave di Azure Data Catalog è una modalità di supporto crowdsourcing hello dei metadati nel sistema hello. Come approccio wiki anziché tooa: in cui è presente un solo parere e hello ultimo quale prevale: modello di Azure Data Catalog hello consente più opinioni toolive side-by-side nel sistema di hello.

Questo approccio riflette hello reale di dati aziendali in cui i diversi utenti possono avere diverse prospettive in un determinato asset:

* Un amministratore del database può fornire informazioni sui contratti di servizio o una finestra di elaborazione disponibili hello per le operazioni ETL bulk
* Un amministratore dei dati può fornire informazioni sulla risorsa di hello business processi toowhich hello applicano o classificazioni hello hello business ha applicato tooit
* Un analista finanziario può fornire informazioni sull'utilizzo di dati hello durante le attività di creazione di report di fine del periodo di tempo

toosupport in questo esempio, ogni utente: hello DBA, amministratore dei dati hello e analista hello: è possibile aggiungere una descrizione tooa singola tabella che è stata registrata nel catalogo di hello. Tutte le descrizioni vengono gestite nel sistema hello e nel portale di Azure Data Catalog hello vengono visualizzate tutte le descrizioni.

Questo modello è applicato toomost elementi hello nel modello a oggetti hello, in modo da tipi di oggetto nel payload JSON hello sono spesso matrici per le proprietà in cui è prevedibile un singleton.

Ad esempio, nel asset hello radice è una matrice di oggetti di descrizione. proprietà di matrice Hello è denominato "descrizione". Un oggetto descrizione ha una proprietà, description. modello di Hello è che ogni utente che la descrizione tipi Ottiene un oggetto descrizione creato per il valore di hello fornito dall'utente hello.

Hello UX quindi è possibile scegliere come toodisplay hello combinazione. Esistono tre diversi modelli per la visualizzazione.

* modello più semplice di Hello è "Mostra tutto". In questo modello, vengono visualizzati tutti gli oggetti hello in una visualizzazione elenco. portale di Azure Data Catalog Hello UX Usa questo modello per una descrizione.
* Un altro modello è "Merge". In questo modello, tutti i valori hello da utenti diversi hello vengono uniti, con i duplicati rimossi. Esempi di questo modello nel portale di Azure Data Catalog hello UX sono proprietà di tag e gli esperti di hello.
* Un terzo modello è "ultima scrittura prevale". In questo modello, viene visualizzato solo hello più recente valore digitato. friendlyName è un esempio di questo modello.

## <a name="asset-object-model"></a>Modello a oggetti asset
Come descritto nella sezione concetti chiave hello, hello **Azure Data Catalog** modello a oggetti sono inclusi elementi, che possono essere attivo o annotazioni. Gli elementi dispongono di proprietà che possono essere obbligatorie o facoltative. Alcune proprietà si applicano tooall elementi. Alcune proprietà si applicano tooall asset. Alcune proprietà si applicano solo i tipi di asset toospecific.

### <a name="system-properties"></a>Proprietà di sistema
<table><tr><td><b>Nome proprietà</b></td><td><b>Tipo di dati</b></td><td><b>Commenti</b></td></tr><tr><td>timestamp</td><td>DateTime</td><td>ultimo elemento di hello ora Hello è stata modificata. Questo campo viene generato dal server di hello quando viene inserito un elemento e ogni volta che viene aggiornato un elemento. Hello valore di questa proprietà viene ignorata per l'input di operazioni di pubblicazione.</td></tr><tr><td>id</td><td>Uri</td><td>Url assoluto dell'elemento hello (sola lettura). È un URI indirizzabile univoco per l'elemento hello hello.  Hello valore di questa proprietà viene ignorata per l'input di operazioni di pubblicazione.</td></tr><tr><td>type</td><td>String</td><td>tipo di Hello di asset hello (sola lettura).</td></tr><tr><td>etag</td><td>String</td><td>Corrispondente toohello versione stringa dell'elemento hello che può essere utilizzato per il controllo della concorrenza ottimistica durante l'esecuzione di operazioni che aggiornano gli elementi nel catalogo di hello. "*" può essere qualsiasi valore toomatch utilizzato.</td></tr></table>

### <a name="common-properties"></a>Proprietà comuni
Queste proprietà si applicano i tipi di tooall radice e tutti i tipi di annotazione.

<table>
<tr><td><b>Nome proprietà</b></td><td><b>Tipo di dati</b></td><td><b>Commenti</b></td></tr>
<tr><td>fromSourceSystem</td><td>Boolean</td><td>Indica se i dati dell'elemento sono derivati da un sistema di origine, ad esempio un database SQL Server o un database Oracle, o creati da un utente.</td></tr>
</table>

### <a name="common-root-properties"></a>Proprietà radice comuni
<p>
Queste proprietà si applicano i tipi di tooall radice.

<table><tr><td><b>Nome proprietà</b></td><td><b>Tipo di dati</b></td><td><b>Commenti</b></td></tr><tr><td>name</td><td>String</td><td>Un nome derivato dalle informazioni di percorso origine dati hello</td></tr><tr><td>dsl</td><td>DataSourceLocation</td><td>In modo univoco descrive l'origine dati hello e uno degli identificatori di hello per asset hello. Vedere la sezione relativa all'identità doppia.  struttura Hello di hello dsl varia in base al protocollo hello e tipo di origine.</td></tr><tr><td>dataSource</td><td>DataSourceInfo</td><td>Per ulteriori dettagli sul tipo hello di asset.</td></tr><tr><td>lastRegisteredBy</td><td>SecurityPrincipal</td><td>Descrive gli utenti hello registrato più di recente l'asset.  Contiene l'id univoco di hello per utente hello (hello upn) sia un nome visualizzato (lastName e firstName).</td></tr><tr><td>containerId</td><td>String</td><td>ID dell'asset di hello contenitore per l'origine dati hello. Questa proprietà non è supportata per il tipo di contenitore hello.</td></tr></table>

### <a name="common-non-singleton-annotation-properties"></a>Proprietà comuni di annotazione non singleton
Queste proprietà si applicano a tipi di annotazione non singleton tooall (annotazioni che è consentito toobe multipli per l'asset).

<table>
<tr><td><b>Nome proprietà</b></td><td><b>Tipo di dati</b></td><td><b>Commenti</b></td></tr>
<tr><td>key</td><td>String</td><td>Chiave che identifica in modo univoco l'annotazione hello nella raccolta corrente hello specificato dall'utente. lunghezza della chiave Hello non può superare i 256 caratteri.</td></tr>
</table>

### <a name="root-asset-types"></a>Tipi di asset radice
I tipi di primo livello sono i tipi che rappresentano hello vari tipi di asset di dati che possono essere registrati nel catalogo di hello. Per ogni tipo di radice, è disponibile una visualizzazione, che descrive l'asset e incluse nella visualizzazione hello annotazioni. Nome della visualizzazione da utilizzare nel segmento di url hello corrispondente {view_name} durante la pubblicazione di un asset mediante l'API REST.

<table><tr><td><b>Tipo di asset (nome vista)</b></td><td><b>Proprietà aggiuntive</b></td><td><b>Tipo di dati</b></td><td><b>Annotazioni consentite</b></td><td><b>Commenti</b></td></tr><tr><td>Tabella ("tabelle")</td><td></td><td></td><td>Descrizione<p>FriendlyName<p>Tag<p>Schema<p>ColumnDescription<p>ColumnTag<p> Esperto<p>Preview<p>AccessInstruction<p>TableDataProfile<p>ColumnDataProfile<p>ColumnDataClassification<p>Documentazione<p></td><td>Tabella che rappresenta i dati tabulari.  Ad esempio: tabella SQL, vista SQL, tabella tabulare di Analysis Services, dimensione multidimensionale di Analysis Services, tabella Oracle e così via.   </td></tr><tr><td>Misura ("misure")</td><td></td><td></td><td>Descrizione<p>FriendlyName<p>Tag<p>Esperto<p>AccessInstruction<p>Documentazione<p></td><td>Tipo che rappresenta una misura di Analysis Services.</td></tr><tr><td></td><td>Misura</td><td>Colonna</td><td></td><td>Misura hello che descrivono i metadati</td></tr><tr><td></td><td>isCalculated </td><td>Boolean</td><td></td><td>Specifica se viene calcolata la misura hello o non.</td></tr><tr><td></td><td>measureGroup</td><td>String</td><td></td><td>Contenitore fisico per la misura.</td></tr><td>Indicatore KPI ("indicatori KPI")</td><td></td><td></td><td>Descrizione<p>FriendlyName<p>Tag<p>Esperto<p>AccessInstruction<p>Documentazione</td><td></td></tr><tr><td></td><td>measureGroup</td><td>String</td><td></td><td>Contenitore fisico per la misura.</td></tr><tr><td></td><td>goalExpression</td><td>String</td><td></td><td>Un'espressione numerica MDX o un calcolo che restituisce il valore di destinazione hello di hello indicatore KPI.</td></tr><tr><td></td><td>valueExpression</td><td>String</td><td></td><td>Un'espressione numerica MDX che restituisce il valore effettivo di hello di hello indicatore KPI.</td></tr><tr><td></td><td>statusExpression</td><td>String</td><td></td><td>Un'espressione MDX che rappresenta lo stato di hello di hello KPI in un punto specifico nel tempo.</td></tr><tr><td></td><td>trendExpression</td><td>String</td><td></td><td>Un'espressione MDX che restituisce il valore di hello di hello KPI nel tempo. tendenza Hello può essere qualsiasi criterio basato sul tempo che risulta utile in un contesto aziendale specifico.</td>
<tr><td>Report ("report")</td><td></td><td></td><td>Descrizione<p>FriendlyName<p>Tag<p>Esperto<p>AccessInstruction<p>Documentazione<p></td><td>Tipo che rappresenta un report di SQL Server Reporting Services. </td></tr><tr><td></td><td>assetCreatedDate</td><td>Stringa</td><td></td><td></td></tr><tr><td></td><td>assetCreatedBy</td><td>Stringa</td><td></td><td></td></tr><tr><td></td><td>assetModifiedDate</td><td>Stringa</td><td></td><td></td></tr><tr><td></td><td>assetModifiedBy</td><td>Stringa</td><td></td><td></td></tr><tr><td>Contenitore ("contenitori")</td><td></td><td></td><td>Descrizione<p>FriendlyName<p>Tag<p>Esperto<p>AccessInstruction<p>Documentazione<p></td><td>Questo tipo rappresenta un contenitore di altri asset, ad esempio un database SQL, un contenitore di BLOB di Azure o un modello di Analysis Services.</td></tr></table>

### <a name="annotation-types"></a>Tipi di annotazione
Tipi di annotazioni rappresentano tipi di metadati che possono essere assegnati tooother tipi all'interno del catalogo hello.

<table>
<tr><td><b>Tipo di annotazione (nome della vista annidata)</b></td><td><b>Proprietà aggiuntive</b></td><td><b>Tipo di dati</b></td><td><b>Commenti</b></td></tr>

<tr><td>Descrizione ("descrizioni")</td><td></td><td></td><td>Questa proprietà contiene una descrizione per un asset. Ogni utente del sistema hello è possibile aggiungere i propri descrizione.  Solo tale utente può modificare l'oggetto descrizione hello.  (I proprietari delle risorse e gli amministratori possono eliminare l'oggetto descrizione hello ma non modificarlo). sistema Hello gestisce separatamente le descrizioni degli utenti.  Pertanto, è disponibile una matrice di descrizioni di ciascuna risorsa (uno per ogni utente che ha contribuito le proprie conoscenze sull'asset hello, in aggiunta toopossibly contenente informazioni derivata dall'origine dati hello).</td></tr>
<tr><td></td><td>description</td><td>string</td><td>Una breve descrizione (righe 2-3) dell'asset hello</td></tr>

<tr><td>Tag ("tag")</td><td></td><td></td><td>Questa proprietà definisce un tag per un asset. Ogni utente del sistema hello è possibile aggiungere più tag per un asset.  Solo utente di hello che ha creato gli oggetti di Tag possa modificarli.  (I proprietari delle risorse e gli amministratori possono eliminare hello Tag oggetto, ma non modificarlo). sistema Hello gestisce separatamente i tag degli utenti.  Di conseguenza, è disponibile una matrice di oggetti Tag in ogni asset.</td></tr>
<tr><td></td><td>tag</td><td>string</td><td>Un asset di tag descrittivi hello.</td></tr>

<tr><td>FriendlyName ("friendlyName")</td><td></td><td></td><td>Questa proprietà contiene un nome descrittivo per un asset. FriendlyName è un'annotazione singleton - FriendlyName solo uno può essere aggiunto tooan asset.  Solo utente di hello che ha creato l'oggetto FriendlyName possibile modificarlo. (I proprietari delle risorse e gli amministratori possono eliminare hello FriendlyName oggetto, ma non modificarlo). sistema Hello gestisce separatamente i nomi descrittivi degli utenti.</td></tr>
<tr><td></td><td>friendlyName</td><td>string</td><td>Un nome descrittivo dell'asset hello.</td></tr>

<tr><td>Schema ("schema")</td><td></td><td></td><td>Hello Schema descrive la struttura hello dei dati di hello.  Sono elencati i nomi di attributo (colonna, attributo, campo e così via) hello, tipi anche altri metadati.  Queste informazioni sono derivate dall'origine dati hello.  Lo schema è un'annotazione singleton. È possibile aggiungere un solo schema a un asset.</td></tr>
<tr><td></td><td>columns</td><td>Column[]</td><td>Matrice di oggetti colonna. Vengono descritte la colonna hello con informazioni derivate dall'origine dati hello.</td></tr>

<tr><td>ColumnDescription ("columnDescriptions")</td><td></td><td></td><td>Questa proprietà contiene una descrizione per una colonna.  Ogni utente del sistema hello può aggiungere descrizioni di più colonne (al massimo uno per ogni colonna). Solo utente di hello che ha creato gli oggetti ColumnDescription possibile modificarli.  (I proprietari delle risorse e gli amministratori possono eliminare hello ColumnDescription oggetto, ma non modificarlo). sistema Hello gestisce separatamente le descrizioni delle colonne dell'utente.  Pertanto è disponibile una matrice di oggetti ColumnDescription ogni asset (uno per ogni colonna per ogni utente che ha contribuito le proprie conoscenze sulla colonna hello inoltre toopossibly uno che contiene informazioni derivate dall'origine dati hello).  Hello ColumnDescription è strettamente associato toohello dello Schema in modo da ottenere sincronizzato. Hello ColumnDescription potrebbe descrivere una colonna che non esiste nello schema di hello.  È di descrizione di tookeep toohello writer e lo schema di sincronizzazione.  origine dati Hello debba anche le informazioni di descrizione colonne e sono oggetti ColumnDescription aggiuntivi che verranno creati durante l'esecuzione dello strumento hello.</td></tr>
<tr><td></td><td>columnName</td><td>String</td><td>nome di Hello della colonna hello a che questa descrizione fa riferimento.</td></tr>
<tr><td></td><td>description</td><td>String</td><td>una breve descrizione (righe 2-3) della colonna hello.</td></tr>

<tr><td>ColumnTag ("columnTags")</td><td></td><td></td><td>Questa proprietà contiene un tag per una colonna. Ogni utente del sistema hello è possibile aggiungere più tag per una determinata colonna e può aggiungere tag per più colonne. Solo utente di hello che ha creato gli oggetti ColumnTag possibile modificarli. (I proprietari delle risorse e gli amministratori possono eliminare hello ColumnTag oggetto, ma non modificarlo). sistema di Hello mantiene tag colonna questi utenti separatamente.  Di conseguenza, è disponibile una matrice di oggetti ColumnTag in ogni asset.  Hello ColumnTag è strettamente associato toohello schema in modo da ottenere sincronizzato. Hello ColumnTag potrebbe descrivere una colonna che non esiste nello schema di hello.  È attivo toohello writer tookeep colonne tag e dello schema di sincronizzazione.</td></tr>
<tr><td></td><td>columnName</td><td>String</td><td>nome di Hello della colonna hello che intende questo tag.</td></tr>
<tr><td></td><td>tag</td><td>String</td><td>Una colonna dei tag descrittivi hello.</td></tr>

<tr><td>Esperto ("esperti")</td><td></td><td></td><td>Questa proprietà contiene un utente che viene considerato un esperto in set di dati hello. Quando si elencano le descrizioni, Hello opinions(descriptions) a bolle toohello cima degli esperti hello UX. Ogni utente può specificare i propri esperti. Solo tale utente può modificare l'oggetto esperti hello. (I proprietari delle risorse e gli amministratori possono eliminare gli oggetti di esperti di hello ma non modificarlo).</td></tr>
<tr><td></td><td>esperto</td><td>SecurityPrincipal</td><td></td></tr>

<tr><td>Anteprima ("anteprime")</td><td></td><td></td><td>Anteprima Hello contiene uno snapshot di hello primi 20 righe di dati per asset hello. L'anteprima risulta utile solo per alcuni tipi di asset, ad esempio per la tabella ma non per la misura.</td></tr>
<tr><td></td><td>preview</td><td>object[]</td><td>Matrice di oggetti che rappresentano una colonna.  Ogni oggetto ha una proprietà mapping tooa colonna con un valore per tale colonna per la riga hello.</td></tr>

<tr><td>AccessInstruction ("accessInstructions")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>mimeType</td><td>string</td><td>tipo di contenuto hello mime Hello.</td></tr>
<tr><td></td><td>content</td><td>string</td><td>istruzioni di Hello per la modalità di accesso di asset di dati toothis tooget. Hello può essere un URL, un indirizzo di posta elettronica o un set di istruzioni.</td></tr>

<tr><td>TableDataProfile ("tableDataProfiles")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>numberOfRows</td></td><td>int</td><td>numero di Hello di righe nel set di dati hello</td></tr>
<tr><td></td><td>size</td><td>long</td><td>dimensione Hello in byte del set di dati hello.  </td></tr>
<tr><td></td><td>schemaModifiedTime</td><td>string</td><td>Hello ultimo tempo hello schema è stato modificato</td></tr>
<tr><td></td><td>dataModifiedTime</td><td>string</td><td>set di Hello ultimo tempo hello dati è stata modificata (dati è stata aggiunta, modificata o eliminazione)</td></tr>

<tr><td>ColumnsDataProfile ("columnsDataProfiles")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>columns</td></td><td>ColumnDataProfile[]</td><td>Matrice di profili dati della colonna.</td></tr>

<tr><td>ColumnDataClassification ("columnDataClassifications")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>columnName</td><td>String</td><td>nome di Hello della colonna hello che intende questa classificazione.</td></tr>
<tr><td></td><td>classificazione</td><td>String</td><td>classificazione Hello dei dati di hello in questa colonna.</td></tr>

<tr><td>Documentazione ("documentazione")</td><td></td><td></td><td>Un determinato asset può avere solo una documentazione associata.</td></tr>
<tr><td></td><td>mimeType</td><td>string</td><td>tipo di contenuto hello mime Hello.</td></tr>
<tr><td></td><td>content</td><td>string</td><td>contenuto della documentazione di Hello.</td></tr>

</table>

### <a name="common-types"></a>Tipi comuni
Tipi comuni possono essere utilizzati come tipi di hello per le proprietà, ma non sono elementi.

<table>
<tr><td><b>Tipo comune</b></td><td><b>Proprietà</b></td><td><b>Tipo di dati</b></td><td><b>Commenti</b></td></tr>
<tr><td>DataSourceInfo</td><td></td><td></td><td></td></tr>
<tr><td></td><td>sourceType</td><td>string</td><td>Descrive il tipo di hello dell'origine dati.  Ad esempio: SQL Server, database Oracle e così via.  </td></tr>
<tr><td></td><td>objectType</td><td>string</td><td>Descrive il tipo di hello di oggetto origine dati hello. Ad esempio: tabella, vista per SQL Server.</td></tr>

<tr><td>DataSourceLocation</td><td></td><td></td><td></td></tr>
<tr><td></td><td>protocol</td><td>string</td><td>Obbligatorio. Viene descritto un toocommunicate di protocollo utilizzato con l'origine dati hello. Ad esempio: "tds" per SQL Server, "oracle" per Oracle e così via. Fare riferimento troppo[dell'origine dati specifica del riferimento - struttura DSL](data-catalog-dsr.md) per elenco hello dei protocolli attualmente supportati.</td></tr>
<tr><td></td><td>Address</td><td>Dizionario<string, object></td><td>Obbligatorio. L'indirizzo è un set di protocollo toohello specifico di dati corrispondente a cui fa riferimento all'origine dati hello tooidentify utilizzato. i dati degli indirizzi Hello ambito tooa particolare protocollo, ovvero che è significativo senza conoscere il protocollo di hello.</td></tr>
<tr><td></td><td>authentication</td><td>stringa</td><td>Facoltativo. schema di autenticazione Hello utilizzato toocommunicate con l'origine dati hello. Ad esempio, Windows, OAuth e così via.</td></tr>
<tr><td></td><td>connectionProperties</td><td>Dizionario<string, object></td><td>Facoltativo. Informazioni aggiuntive sull'origine dati di tooconnect tooa.</td></tr>

<tr><td>SecurityPrincipal</td><td></td><td></td><td>back-end Hello non esegue alcuna convalida delle proprietà fornita con AAD durante la pubblicazione.</td></tr>
<tr><td></td><td>upn</td><td>string</td><td>Indirizzo e-mail univoco dell'utente. Deve essere specificato se objectId non viene specificato o nel contesto di hello della proprietà "lastRegisteredBy", in caso contrario è facoltativo.</td></tr>
<tr><td></td><td>objectId</td><td>Guid</td><td>Identità AAD del gruppo di utenti o di sicurezza. Facoltativo. Deve essere specificato se upn non viene fornito. In caso contrario, è facoltativo.</td></tr>
<tr><td></td><td>firstName</td><td>string</td><td>Nome dell'utente (per scopi di visualizzazione). Facoltativo. Valido solo nel contesto di hello della proprietà "lastRegisteredBy". Non può essere specificato quando si fornisce l'entità di sicurezza per "ruoli", "autorizzazioni" ed "esperti".</td></tr>
<tr><td></td><td>lastName</td><td>string</td><td>Cognome dell'utente (per scopi di visualizzazione). Facoltativo. Valido solo nel contesto di hello della proprietà "lastRegisteredBy". Non può essere specificato quando si fornisce l'entità di sicurezza per "ruoli", "autorizzazioni" ed "esperti".</td></tr>

<tr><td>Colonna</td><td></td><td></td><td></td></tr>
<tr><td></td><td>name</td><td>string</td><td>Nome della colonna hello o un attributo.</td></tr>
<tr><td></td><td>type</td><td>string</td><td>tipo di dati della colonna hello o un attributo. tipi consentiti Hello dipendono dai dati sourceType dell'asset hello.  È supportato un solo subset di tipi.</td></tr>
<tr><td></td><td>maxLength</td><td>int</td><td>Hello la lunghezza massima consentita per la colonna hello o un attributo. Derivata dall'origine dati. Solo tipi di origine toosome applicabile.</td></tr>
<tr><td></td><td>precision</td><td>byte</td><td>precisione Hello per colonna hello o un attributo. Derivata dall'origine dati. Solo tipi di origine toosome applicabile.</td></tr>
<tr><td></td><td>isNullable</td><td>Boolean</td><td>Indica se la colonna hello è toohave un valore null o meno consentito. Derivata dall'origine dati. Solo tipi di origine toosome applicabile.</td></tr>
<tr><td></td><td>expression</td><td>string</td><td>Se il valore di hello è una colonna calcolata, questo campo contiene l'espressione hello esprime valore hello. Derivata dall'origine dati. Solo tipi di origine toosome applicabile.</td></tr>

<tr><td>ColumnDataProfile</td><td></td><td></td><td></td></tr>
<tr><td></td><td>columnName </td><td>string</td><td>nome di Hello della colonna hello</td></tr>
<tr><td></td><td>type </td><td>string</td><td>tipo di Hello della colonna hello</td></tr>
<tr><td></td><td>Min </td><td>string</td><td>valore minimo di Hello nel set di dati hello</td></tr>
<tr><td></td><td>max </td><td>string</td><td>valore massimo di Hello nel set di dati hello</td></tr>
<tr><td></td><td>avg </td><td>double</td><td>valore medio di Hello nel set di dati hello</td></tr>
<tr><td></td><td>stdev </td><td>double</td><td>deviazione standard di Hello per set di dati hello</td></tr>
<tr><td></td><td>nullCount </td><td>int</td><td>conteggio Hello di valori null nel set di dati hello</td></tr>
<tr><td></td><td>distinctCount  </td><td>int</td><td>conteggio di Hello di valori distinct nel set di dati hello</td></tr>


</table>

## <a name="asset-identity"></a>Identità di asset
Azure Data Catalog Usa "protocol" e le proprietà di identità dall'elenco di proprietà "address" hello dell'identità hello oggetto DataSourceLocation "dsl" proprietà toogenerate di hello, che viene utilizzato tooaddress hello asset all'interno di hello catalogo.
Ad esempio, hello "" Tabular ha le proprietà di identità "server", "database", "schema" e "oggetto". le combinazioni di Hello del protocollo di hello e le proprietà di identità hello sono utilizzati toogenerate hello identità di hello Asset di tabella di SQL Server.
Azure Data Catalog offre vari protocolli di origine dati predefiniti, che sono elencati nella [specifica di riferimento per l'origine dati: struttura DSL](data-catalog-dsr.md).
Hello set di protocolli supportati può essere esteso a livello di codice (fare riferimento a riferimento API REST di catalogo tooData). Gli amministratori di hello catalogo possono registrare i protocolli dell'origine dati personalizzata. Hello nella tabella seguente descrive le proprietà necessarie di hello tooregister un protocollo personalizzato.

### <a name="custom-data-source-protocol-specification"></a>Specifica del protocollo di origine dati personalizzato
<table>
<tr><td><b>Tipo</b></td><td><b>Proprietà</b></td><td><b>Tipo di dati</b></td><td><b>Commenti</b></td></tr>

<tr><td>DataSourceProtocol</td><td></td><td></td><td></td></tr>
<tr><td></td><td>namespace</td><td>string</td><td>spazio dei nomi Hello del protocollo hello. Namespace deve essere da 1 too255 caratteri, contenere uno o più parti non vuote separate da punto (.). Ogni parte deve essere compresa tra 1 too255 caratteri, iniziare con una lettera e contenere solo lettere e numeri.</td></tr>
<tr><td></td><td>name</td><td>string</td><td>nome Hello del protocollo hello. Nome deve contenere da 1 too255 caratteri, iniziare con una lettera e contenere solo lettere, numeri e hello trattino (-).</td></tr>
<tr><td></td><td>identityProperties</td><td>DataSourceProtocolIdentityProperty[]</td><td>Elenco di proprietà Identity, deve contenere almeno una proprietà, ma non oltre 20. Ad esempio: "server", "database", "schema", "oggetto" è le proprietà di identità del protocollo "td" hello.</td></tr>
<tr><td></td><td>identitySets</td><td>DataSourceProtocolIdentitySet[]</td><td>Elenco di set di identità. Definisce i set di proprietà Identity che rappresentano l'identità valida dell'asset. Deve contenere almeno un set, ma non oltre 20. Ad esempio: {"server", "database", "schema" e "object"} è un set di identità del protocollo "tds", che definisce l'identità dell'asset Tabella di SQL Server.</td></tr>

<tr><td>DataSourceProtocolIdentityProperty</td><td></td><td></td><td></td></tr>
<tr><td></td><td>name</td><td>string</td><td>nome di Hello della proprietà hello. Nome deve essere compresa tra 1 too100 caratteri, iniziare con una lettera e può contenere solo lettere e numeri.</td></tr>
<tr><td></td><td>type</td><td>string</td><td>tipo di Hello della proprietà hello. Valori supportati: "bool", boolean", "byte", "guid", "int", "integer", "long", "string", "url"</td></tr>
<tr><td></td><td>ignoreCase</td><td>bool</td><td>Indica se deve essere ignorato il caso quando si usa il valore della proprietà. Può essere specificato solo per le proprietà di tipo "string". Il valore predefinito è False.</td></tr>
<tr><td></td><td>urlPathSegmentsIgnoreCase</td><td>bool[]</td><td>Indica se deve essere ignorato case per ogni segmento di percorso dell'url hello. Può essere specificato solo per le proprietà di tipo "url". Il valore predefinito è [false].</td></tr>

<tr><td>DataSourceProtocolIdentitySet</td><td></td><td></td><td></td></tr>
<tr><td></td><td>name</td><td>string</td><td>nome Hello del set di identità hello.</td></tr>
<tr><td></td><td>properties</td><td>string[]</td><td>Hello elenco delle proprietà di identità inclusi in questa identità del set. Non può contenere duplicati. Ogni proprietà a cui fa riferimento il set di identità deve essere definita nell'elenco di hello di "identityProperties" del protocollo hello.</td></tr>

</table>

## <a name="roles-and-authorization"></a>Ruoli e autorizzazione
Catalogo dati di Microsoft Azure offre funzionalità di autorizzazione per le operazioni CRUD su asset e annotazioni.

## <a name="key-concepts"></a>Concetti chiave
Hello Azure Data Catalog utilizza due meccanismi di autorizzazione:

* Autorizzazione basata sui ruoli
* Autorizzazione basata sulle autorizzazioni

### <a name="roles"></a>Ruoli
Sono disponibili tre ruoli: **Amministratore**, **Proprietario** e **Collaboratore**.  Ogni ruolo dispone di ambito e diritti, che sono riepilogati nella tabella seguente hello.

<table><tr><td><b>Ruolo</b></td><td><b>Ambito</b></td><td><b>Diritti</b></td></tr><tr><td>Amministratore</td><td>Catalogo (tutti gli asset/annotazioni in hello catalogo)</td><td>Read Delete ViewRoles

ChangeOwnership ChangeVisibility ViewPermissions</td></tr><tr><td>Proprietario</td><td>Ogni asset (elemento radice)</td><td>Read Delete ViewRoles

ChangeOwnership ChangeVisibility ViewPermissions</td></tr><tr><td>Collaboratore</td><td>Ogni singolo asset e annotazione</td><td>Aggiornamento di lettura eliminare ViewRoles Nota: tutti i diritti di hello vengono revocati se hello destro del mouse su lettura elemento hello viene revocata da hello collaboratore</td></tr></table>

> [!NOTE]
> **Lettura**, **aggiornamento**, **eliminare**, **ViewRoles** i diritti sono applicabili tooany elemento (annotazione o asset) durante **TakeOwnership**, **ChangeOwnership**, **ChangeVisibility**, **ViewPermissions** sono solo toohello applicabile asset di radice.
> 
> **Eliminare** destra Applica tooan elemento ed eventuali elementi secondari o un singolo elemento sottostante. Ad esempio, l'eliminazione di un asset comporta l'eliminazione delle annotazioni dell'asset.
> 
> 

### <a name="permissions"></a>Autorizzazioni
L'autorizzazione è come un elenco di voci di controllo di accesso. Ogni voce di controllo di accesso assegna set di entità di sicurezza tooa diritti. Le autorizzazioni possono essere specificate solo in un asset (vale a dire come elemento radice) e applicano asset toohello e gli elementi secondari.

Durante la hello **Azure Data Catalog** solo anteprima **lettura** destra è supportato in hello autorizzazioni elenco tooenable scenario toorestrict la visibilità di un asset.

Per impostazione predefinita sono tutti gli utenti autenticati **lettura** destro del mouse per qualsiasi elemento nel catalogo di hello a meno che non è limitata visibilità toohello set di entità nelle autorizzazioni hello.

## <a name="rest-api"></a>API REST
**INSERIRE** e **POST** le richieste di voci di visualizzazione può essere utilizzato toocontrol ruoli e autorizzazioni: nel payload tooitem aggiunta, è possibile specificare due proprietà di sistema **ruoli** e  **autorizzazioni**.

> [!NOTE]
> **autorizzazioni** solo elemento radice di tooa applicabile.
> 
> **Proprietario** elemento radice di tooa applicabile solo ruolo.
> 
> Per impostazione predefinita quando viene creato un elemento nel catalogo di hello relativo **collaboratore** è impostato l'utente attualmente autenticato toohello. Se l'elemento deve essere aggiornabile da parte degli utenti, **collaboratore** deve essere impostato troppo&lt;Everyone&gt; entità di sicurezza speciale in hello **ruoli** quando l'elemento è di proprietà prima pubblicazione ( Fare riferimento toohello di esempio seguente). **Collaboratore** non può essere modificato e rimane uguale hello durante la durata di un elemento (anche **amministratore** o **proprietario** privo di hello toochange destra hello  **Collaboratore**). Hello solo valore supportato per l'impostazione esplicita di hello di hello **collaboratore** è &lt;Everyone&gt;: **collaboratore** può essere solo un utente che ha creato un elemento o &lt; Tutti gli utenti&gt;.
> 
> 

### <a name="examples"></a>esempi
**Impostare collaboratore troppo&lt;Everyone&gt; durante la pubblicazione di un elemento.**
L'entità di sicurezza speciale &lt;Tutti&gt; ha come objectId "00000000-0000-0000-0000-000000000201".
  **POST**: https://api.azuredatacatalog.com/catalogs/default/views/tables/?api-version=2016-03-30

> [!NOTE]
> Alcune implementazioni di client HTTP possono eseguire di nuovo automaticamente le richieste di tooa risposta 302 dal server hello, ma in genere rimuovere intestazioni di autorizzazione dalla richiesta hello. Poiché l'intestazione di autorizzazione hello toomake necessarie richieste tooAzure catalogo dati, è necessario verificare l'intestazione di autorizzazione hello è ancora disponibile quando una nuova emissione di un percorso di reindirizzamento tooa di richiesta specificato da Azure Data Catalog. Hello codice di esempio seguente viene illustrato utilizzando l'oggetto .NET HttpWebRequest hello.
> 
> 

**Corpo**

    {
        "roles": [
            {
                "role": "Contributor",
                "members": [
                    {
                        "objectId": "00000000-0000-0000-0000-000000000201"
                    }
                ]
            }
        ]
    }

  **Assegnare i proprietari e limitare la visibilità di un elemento radice esistente**: **PUT** https://api.azuredatacatalog.com/catalogs/default/views/tables/042297b0...1be45ecd462a?api-version=2016-03-30

    {
        "roles": [
            {
                "role": "Owner",
                "members": [
                    {
                        "objectId": "c4159539-846a-45af-bdfb-58efd3772b43",
                        "upn": "user1@contoso.com"
                    },
                    {
                        "objectId": "fdabd95b-7c56-47d6-a6ba-a7c5f264533f",
                        "upn": "user2@contoso.com"
                    }
                ]
            }
        ],
        "permissions": [
            {
                "principal": {
                    "objectId": "27b9a0eb-bb71-4297-9f1f-c462dab7192a",
                    "upn": "user3@contoso.com"
                },
                "rights": [
                    {
                        "right": "Read"
                    }
                ]
            },
            {
                "principal": {
                    "objectId": "4c8bc8ce-225c-4fcf-b09a-047030baab31",
                    "upn": "user4@contoso.com"
                },
                "rights": [
                    {
                        "right": "Read"
                    }
                ]
            }
        ]
    }

> [!NOTE]
> Inserire non è necessario un payload dell'elemento nel corpo di hello toospecify: PUT possono essere utilizzati tooupdate solo ruoli e/o le autorizzazioni.
> 
> 

<!--Image references-->
[1]: ./media/data-catalog-developer-concepts/concept2.png
