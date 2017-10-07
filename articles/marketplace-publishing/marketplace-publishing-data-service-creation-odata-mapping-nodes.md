---
title: aaaGuide toocreating un servizio dati per hello Marketplace | Documenti Microsoft
description: Istruzioni dettagliate su come toocreate, certificare e distribuire un servizio dati per acquistano su hello Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 107baab2-5828-4158-abdf-59a580c80d37
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: e3d88412389d43d104662dc4434363b6ad9475f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-nodes-schema-for-mapping-an-existing-web-service-tooodata-through-csdl"></a>Informazioni hello nodi schema per il mapping di un tooOData del servizio web esistente tramite CSDL
> [!IMPORTANT]
> **In questo momento non stiamo più caricando nuovi editori di servizi dati. I nuovi servizi dati non saranno approvati per l'elencazione.** Se si dispone di un'applicazione SaaS di business si desidera toopublish in AppSource è possibile trovare ulteriori informazioni [qui](https://appsource.microsoft.com/partners). Se si utilizzano applicazioni IaaS sviluppatore del servizio si sarebbe ad esempio toopublish in Azure Marketplace è possibile trovare ulteriori informazioni [qui](https://azure.microsoft.com/marketplace/programs/certified/).
>
>

Questo documento consentirà di chiarire la struttura di nodi hello per il mapping di un tooCSDL protocollo OData. È importante toonote che la struttura di nodi hello è ben formato XML. Pertanto, durante la progettazione del mapping a OData è possibile applicare gli schemi radice, padre e figlio.

## <a name="ignored-elements"></a>Elementi ignorati
di seguito Hello sono hello elevata livello elementi CSDL (nodi XML) che non verranno utilizzate dal back-end di hello Azure Marketplace durante l'importazione di hello dei metadati del servizio web hello toobe. Tali elementi possono essere presenti, ma vengono ignorati.

| Elemento | Scope |
| --- | --- |
| Using |nodo Hello, nodi figlio e tutti gli attributi |
| Documentation |nodo Hello, nodi figlio e tutti gli attributi |
| ComplexType |nodo Hello, nodi figlio e tutti gli attributi |
| Association |nodo Hello, nodi figlio e tutti gli attributi |
| Property esteso |nodo Hello, nodi figlio e tutti gli attributi |
| EntityContainer |Solo hello attributi seguenti vengono ignorati: *estende* e *AssociationSet* |
| Schema |Solo hello attributi seguenti vengono ignorati: *Namespace* |
| FunctionImport |Solo hello attributi seguenti vengono ignorati: *modalità* (valore predefinito di ln presume) |
| EntityType |Solo hello sottonodi seguenti vengono ignorati: *chiave* e *PropertyRef* |

Hello di seguito è riportate hello modifiche (aggiunte e gli elementi ignorati) toohello vari nodi XML CSDL in modo dettagliato.

## <a name="functionimport-node"></a>Nodo FunctionImport
Un nodo di FunctionImport rappresenta un URL (punto di ingresso) che espone un utente finale toohello di servizio. nodo Hello consente che descrive come è stato risolto hello URL, quali parametri sono toohello disponibili per l'utente finale e come questi parametri sono forniti.

Per informazioni dettagliate su questo nodo, vedere [qui][Elemento FunctionImport (CSDL)](https://msdn.microsoft.com/library/cc716710.aspx)

Hello seguenti sono attributi aggiuntivi hello (o le aggiunte tooattributes) che vengono esposti dal nodo FunctionImport hello:

**d:baseUri** -modello URI hello hello REST risorsa tooMarketplace esposto. Marketplace utilizza hello modello tooconstruct query hello servizio web REST. modello URI Hello contiene segnaposto per i parametri di hello in forma di hello di {parameterName}, dove parameterName è il nome di hello del parametro hello. Esempio: apiVersion={apiVersion}.
I parametri sono consentiti tooappear come parametri URI o come parte del percorso dell'URI hello. Nel caso di hello di aspetto hello nel percorso hello sono sempre obbligatori (non può essere contrassegnato come nullable). *Esempio:*`d:BaseUri="http://api.MyWeb.com/Site/{url}/v1/visits?start={start}&amp;end={end}&amp;ApiKey=3fadcaa&amp;Format=XML"`

**Nome** -nome hello di hello funzione importata.  Non può essere hello come gli altri nomi definiti in hello CSDL.  Esempio: Name="GetModelUsageFile"

**EntitySet** *(facoltativo)* - se la funzione hello restituisce una raccolta di tipi di entità, un valore di hello di hello **EntitySet** deve essere una raccolta di hello toowhich set di entità di hello appartiene. In caso contrario, hello **EntitySet** attributo non deve essere utilizzato. *Esempio:*`EntitySet="GetUsageStatisticsEntitySet"`

**ReturnType** *(facoltativo)* -specifica il tipo di hello di elementi restituiti da hello URI.  Non utilizzare questo attributo se la funzione hello non restituisce un valore. di seguito Hello sono tipi hello è supportato:

* **Collection (<Entity type name>)**: specifica una raccolta di tipi di entità definiti. nome Hello è presente nell'attributo del nome del nodo di EntityType hello hello. Un esempio è Collection(WXC.HourlyResult).
* **Non elaborato (<mime type>)**: specifica di un documento/blob non elaborato restituiti toohello utente. Un esempio è Raw(image/jpeg). Altri esempi:

  * ReturnType="Raw(text/plain)"
  * ReturnType="Collection(sage.DeleteAllUsageFilesEntity)"*

**d:paging** -specifica la modalità di gestione di paging da hello risorsa REST. Hello parametro valori vengono utilizzati all'interno delle parentesi creazioni di un ramo, ad esempio, la pagina = {$page} & itemsperpage = {$size} hello le opzioni disponibili sono:

* **None:** il paging non è disponibile
* **Skip:** il paging è espresso tramite “skip” e “take” logici (top). Ignora balzo take e gli elementi M ha quindi restituisce hello Avanti N elementi. Valore parametro: $skip
* **Take:** Take restituisce hello Avanti N elementi. Valore parametro: $take
* **PageSize:** il paging viene espresso tramite una pagina e una dimensione logiche (elementi per pagina). Pagina rappresenta pagina hello corrente viene restituito. Valore parametro: $page
* **Dimensioni:** dimensioni rappresentano il numero di hello di elementi restituiti per ogni pagina. Valore parametro: $size

**d:AllowedHttpMethods** *(facoltativo)* -specifica il verbo è gestito da risorsa REST hello. Inoltre, limita toohello accettati verbo specificato valore.  Valore predefinito = POST.  *Esempio:* `d:AllowedHttpMethods="GET"` hello opzioni disponibili sono:

* **GET:** utilizzato in genere dati tooreturn
* **POST:** utilizzato in genere tooinsert nuovi dati
* **PUT:** utilizzato in genere dati tooupdate
* **ELIMINAZIONE:** toodelete dati utilizzati

I nodi figlio aggiuntive (non descritte nella documentazione relativa a CSDL hello) nel nodo FunctionImport hello sono:

**d:RequestBody** *(facoltativo)* -richiesta hello corpo viene utilizzato tooindicate che hello richiesta è previsto un toobe corpo inviato. I parametri possono essere specificati nel corpo di richiesta hello. e sono espressi all'interno di parentesi graffe, ad esempio {nomeParametro}. Questi parametri sono mappati da hello input dell'utente nel corpo di hello che viene trasferita toohello contenuto servizio provider. elemento requestBody Hello dispone di un attributo con nome httpMethod. attributo Hello consente a due valori:

* **POST:** utilizzato se la richiesta hello è una richiesta HTTP POST
* **GET:** utilizzato se hello richiesta HTTP GET

    Esempio:

        `<d:RequestBody d:httpMethod="POST">
        <![CDATA[
        <req1:Request xmlns:r1="http://schemas.mysite.com//generic/requests/1" Version="1.0">
        <req1:Query>{Query}</req1:Query><req1:AppId>D453474</req1:AppId>
        <req:DestinationSchemas><req1:Schema>Generic.RequestResponse[1.0]</req1:Schema>
        </req1:DestinationSchemas>
        </req1: Request>
        ]]>
        </d:RequestBody>`

**d:namespaces** e **d:Namespace** -questo nodo vengono descritti gli spazi dei nomi hello definiti in hello XML restituito dall'importazione di funzioni hello (endpoint dell'URI). Hello XML restituito dal servizio back-end hello potrebbe contenere un numero qualsiasi di spazi dei nomi toodifferentiate hello contenuti viene restituito. **Tutti questi spazi dei nomi, se utilizzati nelle query XPath d:Map o d:Match necessario toobe elencati.** nodo d:Namespaces Hello contiene un elenco o un set di nodi d:Namespace. Ognuno di essi sono elencati uno spazio dei nomi utilizzato nella risposta del servizio back-end hello. di seguito Hello sono attributo hello del nodo d:Namespace hello:

* **d:prefix:** hello prefisso per lo spazio dei nomi di hello, come illustrato nel hello XML risultati restituiti dal servizio hello, ad esempio f:FirstName, f:LastName, dove f è il prefisso hello.
* **d:URI:** hello URI completo dello spazio dei nomi hello utilizzato nel documento risultato hello. Rappresenta il valore di hello tale prefisso hello viene risolto tooat runtime.

**d:ErrorHandling** *(facoltativo)* : questo nodo contiene le condizioni per la gestione degli errori. Ciascuna delle condizioni di hello viene convalidata risultato hello restituito dal servizio del provider di hello contenuti. Se corrisponde a una condizione hello proposto codice di errore HTTP un messaggio di errore viene restituito toohello dati gestito dall'utente.

**d:ErrorHandling** *(facoltativo)* e **d:Condition** *(facoltativo)* -un nodo di condizione contiene una condizione che viene controllata hello risultato restituito da servizio del provider di Hello contenuti. di seguito Hello sono hello **obbligatorio** attributi:

* **d:Match:** XML di output dell'espressione XPath che verifica se il valore un nodo specificato è presente nel provider di contenuti hello. Hello XPath viene eseguito un output di hello e deve restituire true se la condizione di hello è una corrispondenza o false in caso contrario.
* **d:HttpStatusCode:** hello codice di stato HTTP che deve essere restituiti da Marketplace in hello hello case condizione corrispondenze. Marketplace signalizes utente toohello errori tramite i codici di stato HTTP. Un elenco dei codici di stato HTTP è disponibile all'indirizzo http://en.wikipedia.org/wiki/HTTP_status_code
* **d:ErrorMessage:** messaggio di errore hello toohello restituito – con codice di stato HTTP hello: per l'utente finale. Deve trattarsi di un messaggio di errore descrittivo che non contiene segreti.

**d:Title** *(facoltativo)* -consente di descrivere titolo hello della funzione hello. il valore di Hello di hello titolo proviene da

* Hello mappa facoltativo attributo (un xpath) che specifica in cui titolo hello toofind in risposta hello restituito dalla richiesta di servizio hello.
* - Oppure - titolo hello specificato come valore del nodo hello.

**d:Rights** *(facoltativo)* -hello diritti (ad esempio copyright) associati alla funzione hello. il valore di Hello per i diritti di hello proviene da:

* Hello mappa facoltativo attributo (un xpath) che specifica in cui toofind diritti di hello in risposta hello restituito dalla richiesta di servizio hello.
* - Oppure - diritti hello specificati come valore del nodo hello.

**d:Description** *(facoltativo)* : una breve descrizione per la funzione hello. il valore di Hello per descrizione hello proviene da

* Hello mappa facoltativo attributo (un xpath) che specifica in cui descrizione hello toofind in risposta hello restituito dalla richiesta di servizio hello.
* - O -descrizione hello specificato come valore del nodo hello.

**d:EmitSelfLink** - *vedere l'esempio riportato in precedenza relativo a FunctionImport per 'Paging' tramite i dati restituiti*

**d:EncodeParameterValue** -tooOData estensione facoltativa

**d:QueryResourceCost** -tooOData estensione facoltativa

**d:map** -tooOData estensione facoltativa

**d:Headers** -tooOData estensione facoltativa

**d:Headers** -tooOData estensione facoltativa

**d:Value** -tooOData estensione facoltativa

**d:HttpStatusCode** -tooOData estensione facoltativa

**d:ErrorMessage** -tooOData estensione facoltativa

## <a name="parameter-node"></a>Nodo Parameter
Questo nodo rappresenta un parametro che viene esposto come parte del modello di URI hello / corpo che è stato specificato nel nodo FunctionImport hello della richiesta.

Viene individuata una pagina di documento di dettagli utili informazioni sul nodo "Elemento di parametro" hello in [qui](http://msdn.microsoft.com/library/ee473431.aspx) (hello utilizzare **versione altri** tooselect elenco a discesa una versione diversa, se necessario tooview hello documentazione). *Esempio:*`<Parameter Name="Query" Nullable="false" Mode="In" Type="String" d:Description="Query" d:SampleValues="Rudy Duck" d:EncodeParameterValue="true" MaxLength="255" FixedLength="false" Unicode="false" annotation:StoreGeneratedPattern="Identity"/>`

| Attributo | Obbligatorio | Valore |
| --- | --- | --- |
| Name |Sì |nome di Hello del parametro hello. Fa distinzione tra maiuscole e minuscole.  Maiuscole / minuscole BaseUri hello. **Esempio:**`<Property Name="IsDormant" Type="Byte" />` |
| Tipo |Sì |tipo di parametro Hello. il valore di Hello deve essere un **EDMSimpleType** o un tipo complesso che è nell'ambito di hello del modello di hello. Per ulteriori informazioni, vedere "6 Tipi di parametri e proprietà supportati".  Fa distinzione tra maiuscole e minuscole. Il primo carattere è maiuscolo, gli altri sono minuscoli.  Vedere anche [Tipi del modello concettuale][CollegamentoParametroMSDN](http://msdn.microsoft.com/library/bb399548.aspx). **Esempio:** `<Property Name="LimitedPartnershipID " Type="Int32" />` |
| Mode |No |**In**, Out o InOut a seconda se il parametro hello è un input, output o parametro di input/output. In Azure Marketplace è disponibile solo "In". **Esempio:** `<Parameter Name="StudentID" Mode="In" Type="Int32" />` |
| MaxLength |No |lunghezza del parametro hello Hello massima consentita. **Esempio:**`<Property Name="URI" Type="String" MaxLength="100" FixedLength="false" Unicode="false" />` |
| Precision |No |precisione Hello del parametro hello. **Esempio:**`<Property Name="PreviousDate" Type="DateTime" Precision="0" />` |
| Scalabilità |No |scala Hello del parametro hello. **Esempio:**`<Property Name="SICCode" Type="Decimal" Precision="10" Scale="0" />` |

di seguito Hello sono attributi hello che sono stati aggiunti specifica CSDL toohello:

| Attributo | Descrizione |
| --- | --- |
| **d:Regex** *(facoltativo)* |Valore di input hello toovalidate di utilizzare un'istruzione di regex per il parametro hello. Se il valore di input hello non corrisponde al valore di hello istruzione hello viene rifiutata. In questo modo toospecify anche un set di valori possibili, ad esempio ^ [0-9] +? $ tooonly Consenti numeri. **Esempio:** "&lt;Parameter Name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="Nome senza spazi né caratteri non appartenenti all'alfabeto inglese" d:SampleValues="George |
| **d:Enum***(facoltativo)* |Elenco di valori validi per il parametro hello separati da una pipe. tipo di Hello di valori hello deve tipo hello definito toomatch del parametro hello. Esempio: "english |
| **d: Nullable***(facoltativo)* |Consente di definire se un parametro può essere null. valore predefinito di Hello è: true. Tuttavia, i parametri che vengono esposti come parte del percorso hello nel modello URI hello non possono essere null. Quando l'attributo hello è impostato toofalse per questi parametri: l'input dell'utente hello viene sottoposto a override. **Esempio:**`<Parameter Name="BikeType" Type="String" Mode="In" Nullable="false"/>` |
| **d:SampleValue** *(facoltativo)* |Un valore di esempio toodisplay come un Client di toohello nota in hello dell'interfaccia utente.  È possibile elencare tooadd separati diversi valori tramite una pipe, ad esempio ' un |

## <a name="entitytype-node"></a>Nodo EntityType
Questo nodo rappresenta uno dei tipi di hello che vengono restituiti dall'utente finale di toohello Marketplace. Contiene inoltre il mapping di hello dall'output di hello restituito da valori restituiti per l'utente finale toohello toohello del servizio del provider di hello contenuti.

Sono disponibili informazioni dettagliate su questo nodo nella [qui](http://msdn.microsoft.com/library/bb399206.aspx) (hello utilizzare **versione altri** tooselect elenco a discesa una versione diversa, se necessario tooview hello documentazione.)

| Nome attributo | Obbligatorio | Valore |
| --- | --- | --- |
| Name |Sì |nome Hello hello del tipo di entità. **Esempio:**`<EntityType Name="ListOfAllEntities" d:Map="//EntityModel">` |
| BaseType |No |nome Hello di un altro tipo di entità hello tipo di base del tipo di entità hello che viene definito. **Esempio:**`<EntityType Name="PhoneRecord" BaseType="dqs:RequestRecord">` |

di seguito Hello sono attributi hello che sono stati aggiunti specifica CSDL toohello:

**d:map** -espressione XPath eseguita sull'output di hello del servizio. Hello presupposto è che output hello del servizio contiene un set di elementi che si ripetono, come un ATOM feed in cui è presente un set di nodi di ingresso che si ripetono. Ognuno di questi nodi ripetuti contiene un record. Hello XPath è toopoint specificato nel singolo nodo ripetuto hello nel risultato di servizio del provider di hello contenuto che contiene i valori hello di un singolo record. Output di esempio dal servizio hello:

        `<foo>
          <bar> … content … </bar>
          <bar> … content … </bar>
          <bar> … content … </bar>
        </foo>`

espressione XPath Hello sarebbe /foo/bar perché ogni nodo barra hello è hello ripetute output nodo hello e contenuto effettivo hello restituito toohello dati gestito dall'utente.

**Key** : questo attributo viene ignorato da Marketplace. I servizi Web basati su REST, in genere, non espongono una chiave primaria.

## <a name="property-node"></a>Nodo Property
Questo nodo contiene una proprietà del record di hello.

Sono disponibili informazioni dettagliate su questo nodo nella [http://msdn.microsoft.com/library/bb399546.aspx](http://msdn.microsoft.com/library/bb399546.aspx) (hello utilizzare **versione altri** tooselect elenco a discesa una versione diversa, se necessario tooview hello documentazione.) *Esempio:* `<EntityType Name="MetaDataEntityType" d:Map="/MyXMLPath">
        <Property Name="Name"     Type="String" Nullable="true" d:Map="./Service/Name" d:IsPrimaryKey="true" DefaultValue=”Joe Doh” MaxLength="25" FixedLength="true" />
        ...
        </EntityType>`

| AttributeName | obbligatori | Valore |
| --- | --- | --- |
| Name |Sì |nome di Hello della proprietà hello. |
| Tipo |Sì |tipo di Hello hello del valore della proprietà. tipo di valore di proprietà Hello deve essere un **EDMSimpleType** o un tipo complesso (indicato da un nome completo) all'interno dell'ambito del modello di hello. Per ulteriori informazioni, vedere i tipi di modello concettuale (CSDL). |
| Nullable |No |**True** (valore predefinito di hello) o **False** a seconda se la proprietà hello può avere un valore null. Nota: In hello versione di CSDL indicati da hello [http://schemas.microsoft.com/ado/2006/04/edm](http://schemas.microsoft.com/ado/2006/04/edm) dello spazio dei nomi, una proprietà di tipo complesso deve avere Nullable = "False". |
| DefaultValue |No |valore predefinito di Hello della proprietà hello. |
| MaxLength |No |lunghezza massima di Hello hello del valore della proprietà. |
| FixedLength |No |**True** o **False** a seconda se il valore di proprietà hello verrà archiviato come una stringa di lunghezza fiexed. |
| Precision |No |Si riferisce toohello il numero massimo di cifre tooretain in valore numerico hello. |
| Scalabilità |No |Numero massimo di posizioni decimali tooretain in valore numerico hello. |
| Unicode |No |**True** o **False** a seconda che il valore di proprietà hello essere archiviati come una stringa Unicode. |
| Collation |No |Stringa che specifica l'ordinamento sequenza toobe utilizzato nell'origine dati hello hello. |
| ConcurrencyMode |No |**Nessuna** (valore predefinito di hello) o **Fixed**. Se il valore di hello è troppo**Fixed**, verrà utilizzato il valore di proprietà hello nei controlli di concorrenza ottimistica. |

di seguito Hello sono attributi aggiuntivi hello che sono stati aggiunti specifica CSDL toohello:

**d:map** -espressione XPath eseguita su servizio hello di output e consente di estrarre una proprietà di output di hello. Hello XPath specificato è relativo toohello nodo selezionato in XPath del nodo di EntityType hello ripetuto. È inoltre possibile toospecify un tooallow XPath assoluto, tra cui una risorsa statica in ogni hello output nodi, come ad esempio una dichiarazione di copyright presente solo una volta in hello servizio originale di output, ma deve essere presente in ognuna delle righe hello hello OData output. Esempio dal servizio hello:

        `<foo>
          <bar>
           <baz0>… value …</baz0>
           <baz1>… value …</baz1>
           <baz2>… value …</baz2>
          </bar>
        </foo>`

espressione XPath Hello sarebbe nodo baz0 di ./bar/baz0 tooget hello dal servizio del provider di hello contenuti.

**d:CharMaxLength** -per il tipo di stringa, è possibile specificare la lunghezza massima di hello. Vedere Esempio di CSDL di DataService

**d:IsPrimaryKey** -indica se la colonna hello è chiave primaria di hello nella tabella/vista hello. Vedere Esempio di CSDL di DataService.

**d:isExposed** -determina se viene esposta schema della tabella hello (in genere true). Vedere Esempio di CSDL di DataService

**d:IsView** *(facoltativo)* : true se si basa su una vista anziché su una tabella.  Vedere Esempio di CSDL di DataService

**d:Tableschema** : vedere Esempio di CSDL di DataService

**d:ColumnName** -nome hello hello colonne nella tabella/vista hello.  Vedere Esempio di CSDL di DataService

**d:IsReturned** -è valore booleano che determina se hello servizio espone questo client toohello valore hello.  Vedere Esempio di CSDL di DataService

**d:IsQueryable** -è hello valore booleano che determina se la colonna hello è possibile utilizzare in una query di database.   Vedere Esempio di CSDL di DataService

**d:OrdinalPosition** -è hello posizione della colonna numerica dell'aspetto, x, nella tabella di hello o visualizzazione di hello, dove x è di 1 toohello numero di colonne nella tabella hello.  Vedere Esempio di CSDL di DataService

**d:DatabaseDataType** -hello tipo di dati della colonna hello nel database di hello, ad esempio il tipo di dati SQL. Vedere Esempio di CSDL di DataService

## <a name="supported-parametersproperty-types"></a>Tipi di parametri e proprietà supportati
di seguito Hello sono tipi di hello è supportato per i parametri e proprietà. C'è distinzione tra maiuscole e minuscole.

| Tipi primitivi | Descrizione |
| --- | --- |
| Null |Rappresenta l'assenza di hello di un valore |
| Boolean |Rappresenta hello concetto matematico di logica a valori binari |
| Byte |Valore intero senza segno a 8 bit |
| DateTime |Rappresenta una data e un'ora con valori compresi tra le ore 0:00:00 del 1° gennaio 1753 d. C. e le 23:59:59 del dicembre 9999 d.C. |
| Decimale |Rappresenta valori numerici con precisione e scalabilità fisse. Questo tipo può descrivere un valore numerico compreso tra 10 negativo ^ 255 + 1 toopositive 10 ^ -1 a 255 |
| Double |Rappresenta un numero a virgola mobile con precisione a 15 cifre che può rappresentare valori compresi approssimativamente tra approssimativo compreso tra ± 2,23e -308 e ± 1,79e +308. **Utilizzare Decimal a causa di tooExel esportazione problema** |
| Single |Rappresenta un numero a virgola mobile con precisione a 7 cifre che può rappresentare valori compresi approssimativamente tra approssimativo compreso tra ± 1,18e -38 e ± 3,40e +38. |
| Guid |Rappresenta un valore di identificatore univoco a 16 byte (128 bit) |
| Int16 |Rappresenta un valore intero con segno a 16 bit |
| Int32 |Rappresenta un valore intero con segno a 32 bit |
| Int64 |Rappresenta un valore intero con segno a 64 bit |
| String |Rappresenta dati di tipo carattere a lunghezza fissa o variabile |

## <a name="see-also"></a>Vedere anche
* Se si è interessati alla comprensione hello l'intero processo di mapping di OData e lo scopo, leggere questo articolo [Mapping di dati del servizio OData](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definizioni, strutture e le istruzioni.
* Se si è interessati a esaminare alcuni esempi, leggere questo articolo [esempi di Mapping di dati del servizio OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee codice di esempio e comprendere la sintassi di codice e il contesto.
* toohello tooreturn previsto percorso per la pubblicazione toohello un servizio dati Azure Marketplace, leggere questo articolo [Guida alla pubblicazione di dati del servizio](marketplace-publishing-data-service-creation.md).
