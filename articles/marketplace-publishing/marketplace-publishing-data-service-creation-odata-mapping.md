---
title: aaaGuide toocreating un servizio dati per hello Marketplace | Documenti Microsoft
description: Istruzioni dettagliate su come toocreate, certificare e distribuire un servizio dati per acquistano su hello Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 3a632825-db5b-49ec-98bd-887138798bc4
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: deb2e52dd03f5beb2ad6a927bd2d03e47d20b691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="mapping-an-existing-web-service-tooodata-through-csdl"></a>Mapping di un tooOData del servizio web esistente tramite CSDL
> [!IMPORTANT]
> **In questo momento non stiamo più caricando nuovi editori di servizi dati. I nuovi servizi dati non saranno approvati per l'elencazione.** Se si dispone di un'applicazione SaaS di business si desidera toopublish in AppSource è possibile trovare ulteriori informazioni [qui](https://appsource.microsoft.com/partners). Se si utilizzano applicazioni IaaS sviluppatore del servizio si sarebbe ad esempio toopublish in Azure Marketplace è possibile trovare ulteriori informazioni [qui](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

In questo articolo viene fornita una panoramica su come toouse un toomap CSDL un tooan servizio esistente servizio compatibile OData. Viene spiegato come toocreate hello documento di mapping (CSDL) che trasforma una richiesta di input hello del client di hello tramite una chiamata al servizio e hello output client toohello (backup dei dati) tramite un feed di OData compatibile. Microsoft Azure Marketplace espone gli utenti finali toohello servizi protocollo OData hello. I servizi dei provider di contenuti (proprietari di dati) vengono esposti in varie forme, ad esempio REST, SOAP e così via.

## <a name="what-is-a-csdl-and-its-structure"></a>Che cos'è un CSDL e la relativa struttura?
Un file CSDL (Conceptual Schema Definition Language) è una specifica definizione come servizio web toodescribe o il database del servizio in comune XML lettera toohello Azure Marketplace.

Panoramica semplice di hello **del flusso di richiesta:**

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

Hello **il flusso di dati** in hello opposto direzione:

  `Client <- Azure Marketplace <- Content Provider’s WebService`

**Figura 1** diagrammi come un client potrebbe ottenere i dati da un provider di contenuti (servizio) attraverso hello Azure Marketplace.  Hello CSDL viene utilizzato dalla richiesta di hello Mapping o la trasformazione componente toohandle hello e passare dati tra i servizi del provider di hello contenuti e hello richiesta client.

*Figura 1: Flusso dettagliato richiedano provider toocontent client tramite Azure Marketplace*

  ![disegno](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

Per informazioni generali su protocollo OData hello al quale hello compilazione estensioni di Azure Marketplace, Atom Pub e Atom, vedere: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)

L'estratto di codice di sopra del collegamento: *"hello hello Open Data protocol (OData a cui si fa riferimento successivamente tooas) mira protocollo tooprovide basato su REST per operazioni in stile CRUD (Create, Read, Update e Delete) su risorse esposte come servizi di dati. Un "servizio dati" è un endpoint in cui i dati sono esposti da una o più "raccolte", ciascuna con zero o più "voci", costituite da coppie nome-valore tipizzate. OData viene pubblicato da Microsoft in standard OASIS (Organization for hello Advancement of Structured Information Standards) in modo che qualsiasi utente che desidera toocan creare server, client o gli strumenti di senza restrizioni o royalty."*

### <a name="three-critical-pieces-that-have-toobe-defined-by-hello-csdl-are"></a>Tre importanti che sono definiti da hello CSDL toobe sono:
* Hello **endpoint** di Provider di servizi di hello hello Web indirizzo (URI) di hello servizio
* Hello **parametri dati** passati come input toohello Provider di servizi le definizioni di hello dei parametri di hello inviati servizio del Provider contenuto toohello toohello tipo di dati.
* **Schema** di dati hello restituiti toohello richiesta servizio hello schema dell'hello dati inviati dal servizio del Provider di hello contenuto, inclusi i tipi di contenitore, raccolte e alle tabelle, variabili o colonne e dati.

Hello seguente diagramma mostra una panoramica del flusso di hello dalla quale client hello immette hello OData istruzione (servizio di chiamata toohello del provider di contenuti web) toogetting hello risultati/backup dei dati.

  ![disegno](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a>Passaggi:
1. Il client invia richiesta tramite chiamata al servizio con i parametri di Input definiti in XML toohello Azure Marketplace
2. CSDL è usato toovalidate hello chiamata del servizio.
   * Hello formattato nella chiamata di servizio viene poi inviata toohello servizio provider di contenuto tramite hello Azure Marketplace
3. esegue Hello Webservice e vengono eseguite azioni di hello di hello verbo Http (ad esempio, GET) dati hello restituiti tooAzure Marketplace in hello richiesta dei dati (se presente) è espone in formato XML toohello Client utilizzando hello Mapping definito nel file CSDL hello.
4. Hello Client verrà inviato dati hello (se presente) in formato XML o JSON

## <a name="definitions"></a>Definizioni
### <a name="odata-atom-pub"></a>OData ATOM Pub
Impostare un ATOM pub toohello estensione in cui ogni voce rappresenta una riga di un risultato. parte di contenuto Hello della voce hello è toocontain avanzata hello valori di riga hello – come coppie chiave-valore. Sono disponibili ulteriori informazioni all'indirizzo: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)

### <a name="csdl---conceptual-schema-definition-language"></a>CSDL - Conceptual Schema Definition Language
Consente di definire le funzioni (SPROC) e le entità che vengono esposte tramite un database. Sono disponibili ulteriori informazioni all'indirizzo: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)  

> [!TIP]
> Fare clic su hello **altre versioni** elenco a discesa e selezionare una versione, se non viene visualizzato articolo hello.
> 
> 

### <a name="edm---entry-data-model"></a>EDM - Entry Data Model, Modello di dati di movimento
* Panoramica: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* Anteprima: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* Tipi di dati: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

Hello seguente hello dettagliate tooRight sinistro flusso dal quale client hello immette hello OData istruzione (servizio di chiamata toohello del provider di contenuti web) toogetting hello risultati/backup dei dati:

  ![disegno](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a>Nozioni di base su CSDL
Un file CSDL (Conceptual Schema Definition Language) è una specifica definizione come servizio web toodescribe o il database del servizio in comune XML lettera toohello Azure Marketplace. Descrive CSDL hello critico pezzi che **consente il passaggio di hello dei dati dall'origine dati di hello toohello Azure Marketplace.** parti principali di Hello sono descritti di seguito:

* Informazioni sull'interfaccia che descrivono tutte le funzioni disponibili pubblicamente (nodo FunctionImport)
* Informazioni sul tipo di dati per tutte le richieste di messaggi (input) e risposte ai messaggi (output) (nodi EntityContainer/EntitySet/EntityType)
* Informazioni su toobe protocollo di trasporto hello di associazione utilizzato (nodo intestazione)
* Informazioni sull'indirizzo per l'individuazione di hello specificato del servizio (BaseURI attributo)

In breve, hello CSDL rappresenta un contratto di indipendente dalla piattaforma e linguaggio tra richiedente del servizio hello e provider di servizi di hello. Utilizza hello CSDL, un client può individuare un servizio di database o del servizio web e richiamare le relative funzioni disponibili pubblicamente.

### <a name="relating-a-csdl-tooa-database-or-a-collection"></a>Relativo a un Database di tooa CSDL o una raccolta
**Hello specifica CSDL**

CSDL è la grammatica XML che descrive un servizio Web. Specifica Hello è diviso 4 elementi principali: EntitySet, FunctionImport; Spazio dei nomi ed EntityType.

toomake toounderstand di più facile Questa astrazione consente di collegare una tabella tooa CSDL.

Tenere presente:

  CSDL rappresenta un contratto indipendente dalla piattaforma e linguaggio tra hello **richiedente del servizio** hello e **provider di servizi**. Il CSDL consente al **client** di individuare un **servizio Web o del database** e richiamare una qualsiasi delle relative **funzioni** disponibili pubblicamente.

Per hello un servizio dati costituito da quattro parti di un file CSDL può essere considerato in termini di un Database, tabelle, colonne e Stored Procedure.

Con riferimento a quanto segue per un servizio dati:

* EntityContainer  ~=  database
* EntitySet  ~=  tabella
* EntityType  ~= colonne
* FunctionImport  ~=  Stored Procedure

**Verbi HTTP consentiti**

* GET-restituisce i valori da db hello (restituisce una raccolta)
* POST-utilizzate toopass dati tooand facoltativo i valori restituiti da db hello (creazione di una nuova voce nella raccolta di hello, id o URI restituito)
* ELIMINARE – Elimina i dati hello DB (Elimina una raccolta)
* PUT: consente di aggiornare i dati in un database (sostituire una raccolta o crearne una)

## <a name="metadatamapping-document"></a>Documento metadati/mapping
documento di metadati e mapping Hello è toomap utilizzato in modo che può essere esposto come un servizio web OData dal sistema di hello Azure Marketplace di servizi web esistenti di un provider di contenuti. Si basa su CSDL e implementa alcune estensioni tooCSDL tooaccommodate hello esigenze di REST basato su servizi web esposti tramite Azure Marketplace. vengono trovate estensioni di Hello in hello [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) dello spazio dei nomi.

Segue un esempio di hello CSDL: (copia e Incolla hello esempio CSDL in un editor XML seguente e modificare toomatch il servizio.  Incollare in CSDL Mapping nella scheda DataService durante la creazione del servizio in hello [portale di pubblicazione di Azure Marketplace](https://publish.windowsazure.com)).

**Condizioni:** hello riguardanti CSDL termini toohello [portale pubblicazione](https://publish.windowsazure.com) termini dell'interfaccia utente (PPUI).

* Offrono "Title" hello PPUI correlato tooMyWebOffer
* MyCompany in hello PPUI si riferisce troppo**nome visualizzato editore** in hello [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) dell'interfaccia utente
* L'API correlata tooa Web o un servizio dati (un piano di hello PPUI)

**Gerarchia:** una società (provider di contenuti) è titolare delle offerte con piani, ossia servizi, che si allineano a un'API.

### <a name="webservice-csdl-example"></a>Esempio di CSDL di WebService
Si connette tooa servizio che espone un endpoint dell'applicazione web (ad esempio, un'applicazione c#)

        <?xml version="1.0" encoding="utf-8"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyWebOffer" Alias="MyOffer" xmlns="http://schemas.microsoft.com/ado/2009/08/edm" xmlns:d="http://schemas.microsoft.com/dallas/2010/04" >
        <!-- EntityContainer groups all hello web service calls together into a single offering. Every web service call has a FunctionImport definition. -->
          <EntityContainer Name="MyOffer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
        @Name is used as reference by FunctionImport @EntitySet. And is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition near hello bottom of this file. -->
            <EntitySet Name="MyEntities" EntityType="MyOffer.MyEntityType" />
        <!-- Add a FunctionImport for every service method. Multiple FunctionImports can share a single return type (EntityType). -->
        <!-- ReturnType is either Raw() for a stream or Collection() for an Atom feed. Ex. of Raw: ReturnType=”Raw(text/plain)” -->
        <!—EntitySet is hello entityset defined above, and is needed if ReturnType is not Raw -->
        <!-- BaseURI attribute defines hello service call, replace & with hello encode value (&amp;).
        In hello input name value pairs {param} represents passed in value.
        Or hello value can be hard coded as with AccountKey. -->
        <!-- AllowedHttpMethods optional (default = “GET”), allows hello CSDL toospecifically specify hello verb of hello service, “Get”, “Post”, “Put”, or “Delete”. -->
        <!-- EncodeParameterValues, True encodes hello parameter values, false does not. -->
        <!-- BaseURI is translated into an URITemplate which defines how hello web service call is exposed toomarketplace customers.
        Ex. https://api.datamarket.azure.com/mycompany/MyOfferPlan?name={name}
        BaseURI is XML encoded, hello {...} point toohello parameters defined below.
        Marketplace will read hello parameters from this URITemplate and fill hello values into hello corresponding parameters of hello BaseUri or RequestBody (below) during calls tooyour service.  
        It is okay for @d:BaseUri tooinclude information only for Marketplace consumption, it will not be exposed tooend users. i.e. hello hardcoded AccountKey in hello above BaseURI does not show up in hello client facing URITemplate. -->
            <FunctionImport Name="MyWebServiceMethod"
                            EntitySet="MyEntities"
                            ReturnType="Collection(MyOffer.MyEntityType)"
        d:AllowedHttpMethods="GET"
        d:EncodeParameterValues="true"
        d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <!-- Definition of hello RequestBody is only required for HTTP POST requests and is optional for HTTP GET requests. -->
        <d:RequestBody d:httpMethod="POST">
                <!-- Use {} for placeholders tooinsert parameters. -->
                <!-- This example uses SOAP formatting, but any POST body can be used. -->
            <!-- This example shows how toopass userid and password via hello header -->
                <![CDATA[<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:MyOffer="http://services.organization.net/MyServicePath">
                  <soapenv:Header/>
                  <soapenv:Body>
                    <MyOffer:ws_MyWebServiceMethod>
                      <myWebServiceMethodRequest>
                        <!--This information is not exposed tooend users. -->
                        <UserId>userid</UserId>
                        <Password>password</Password>
                        <!-- {name} is replaced with hello value read from @d:UriTemplate above -->
                        <Name>{name}</Name>
                        <!-- Parameters can be used more than once and are not limited tooappearing as hello value of an element -->
                        <CustomField Name="{name}" />
                        <MyField>Static content</MyField>
                      </myWebServiceMethodRequest>
                    </MyOffer:ws_MyWebServiceMethod>
                  </soapenv:Body>
                </soapenv:Envelope>      
              ]]>
        </d:RequestBody>
        <!-- Title, Rights and Description are optional and used toospecify values tooinsert into hello ATOM feed returned toohello end user.  You can specify hello element toocontain a fixed message by providing a value for hello element (this is hello default value).  @d:Map is an XPath expression that points into hello response returned by your service and is optional.  -->
        <d:Title d:Map="/MyResponse/Title">Default title.</d:Title>
        <d:Rights>© My copyright. This is a fixed response. It is okay tooalso add a d:Map attribute toooverride this text.</d:Rights>
        <d:Description d:Map="/MyResponse/Description"></d:Description>
        <d:Namespaces>
        <d:Namespace d:Prefix="p"  d:Uri="http://schemas.organization.net/2010/04/myNamespace" />
        <d:Namespace d:Prefix="p2" d:Uri="http://schemas.organization.net/2010/04/MyNamespace2" />
        </d:Namespaces>
        <!-- Parameters of hello web service call:
        @Name should match exactly (case sensitive) hello {…} placeholders in hello @d:BaseUri, @d:UriTemplate, and d:RequestBody, i.e. “name” parameter in above BaseURI.
        @Mode is always "In", compatibility with CSDL
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx
        @d:Nullable indicates whether hello parameter is required.
        @d:Regex - optional, attribute toodescribe hello string, limiting unwanted input at hello entry of hello system
        @d:Description - optional, is used by Service Explorer as help information
        @d:SampleValues - optional, is used by Service Explorer as help information. Multiple Sample values are separated by '|', e.g. "804735132|234534224|23409823234"
        @d:Enum - optional for string type. Contains an enumeration of possible values separated by a '|', e.g. d:enum="english|metric|raw". Will be converted in a dropdown list in hello Service Explorer.
        -->
        <Parameter name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="A name that cannot contain any spaces or non-alpha non-English characters"
        d:Enum="George|John|Thomas|James"
        d:SampleValues="George"/>
        <Parameter Name=" AccountKey" Mode="In" Type="String" d:Nullable="false" />

        <!-- d:ErrorHandling is an optional element. Use it define standardized errors by evaluating hello service response. -->
        <d:ErrorHandling>
        <!-- Any number of d:Condition elements are allowed, they are evaluated in hello order listed.
        @d:Match is an Xpath query on hello service response, it should return true or false where true indicates an error.
        @d:httpStatusCode is hello error code tooreturn if an response matches hello error.
        @d:errorMessage is hello user friendly message tooreturn when an error occurs.
        -->
        <d:Condition d:Match="/Result/ErrorMessage[text()='Invalid token']" d:HttpStatusCode="403" d:ErrorMessage="User cannot connect toohello service." />
        </d:ErrorHandling>
           </FunctionImport>

            <!-- hello EntityContainer defines hello output data schema -->
        </EntityContainer>
        <!-- hello EntityType @d:Map defines hello repeating node (an XPath query) in hello response (output data schema). -->
        <!-- If these nodes are outside a namespace, add hello prefix in hello xpath. -->
        <!--
        @Name - define your user readable name, will become an XML element in hello ATOM feed, so comply with hello XML element naming restrictions (no spaces or other illegal characters).
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx.
        @d:Map uses an Xpath query toopoint at hello location tooextract hello content from your services response.
        hello "." is relative toohello repeating node in hello EntityType @d:Map Xpath expression.
        -->
            <EntityType Name="MyEntityType" d:Map="/MyResponse/MyEntities">
        <Property Name="ID"    d:IsPrimaryKey="True" Type="Int32"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="Amount"    Type="Double"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="City"    Type="String"    Nullable="false" d:Map="./City"/>
        <Property Name="State"    Type="String"    Nullable="false" d:Map="./State"/>
        <Property Name="Zip"    Type="Int32"    Nullable="false" d:Map="./Zip"/>
        <Property Name="Updated"    Type="DateTime"    Nullable="false" d:Map="./Updated"/>
        <Property Name="AdditionalInfo" Type="String" Nullable="true"
        d:Map="./Info/More[1]"/>
            </EntityType>
        </Schema>

> [!TIP]
> Visualizzare ulteriori esempi di servizio Web di CSDL nell'articolo hello [esempi di mapping esistente web servizio tooOData tramite CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)
> 
> 

### <a name="dataservice-csdl-example"></a>Esempio di CSDL di DataService
Stabilisce la connessione del servizio tooa che viene esposto da una vista o tabella di database come un endpoint di esempio seguente vengono illustrati due API per i dati di base basato su API CSDL (possibile utilizzare viste anziché tabelle).

        <?xml version="1.0"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyDataOffer" Alias="MyOffer" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ado/2009/08/edm">
        <!-- EntityContainer groups all hello data service calls together into a single offering. Every web service call has a FunctionImport definition. -->
        <EntityContainer Name="MyOfferContainer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
            Think of hello EntitySet as a Service
        @Name is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition (returned set of table columns). -->
        <EntitySet Name="CompanyInfoEntitySet" EntityType="MyOffer.CompanyInfo" />
        <EntitySet Name="ProductInfoEntitySet" EntityType="MyOffer.ProductInfo" />
        </EntityContainer>
        <!-- EntityType defines result (output); hello table (or view) and columns toobe returned by hello data service.)
            Map is hello schema.tabel or schema.view
            dals.TableName is hello table Name
            Name is hello name identifier for hello EntityType and hello Name of hello service exposed toohello client via hello UI.
            dals:IsExposed determines if hello table schema is exposed (generally true).
            dals:IsView (optional) true if this is based on a view rather than a table
            dals:TableSchema is hello schema name of hello table/view
        -->
        <EntityType
        Map="[dbo].[CompanyInfo]"
        dals:TableName="CompanyInfo"
        Name="CompanyInfo"
        dals:IsExposed="true"
        dals:IsView="false"
        dals:TableSchema="dbo"
        xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <!-- Property defines hello column properties and hello output of hello service.
            dals:ColumnName is hello name of hello column in hello table /view.
            Type is hello emd.SimpleType
            Nullable determines if NULL is a valid output value
            dals.CharMaxLenght is hello maximum length of hello output value
            Name is hello name of hello Property and is exposed toohello client facing UI
            dals:IsReturned is hello Boolean that determines if hello Service exposes this value toohello client.
            IsQueryable is hello Boolean that determines if hello column can be used in a database query
            (For data Services: tooimprove Performance make sure that columns marked ISQueryable=”true” are in an index.)
            dals:OrdinalPosition is hello numerical position x in hello table or hello View, where x is from 1 toohello number of columns in hello table.
            dals:DatabaseDataType is hello data type of hello column in hello database, i.e. SQL data type dals:IsPrimaryKey indicates if hello column is hello Primary key in hello table/view.  (hello columns marked ISPrimaryKey are used in hello Order by clause when returning data.)
        -->
        <Property dals:ColumnName="data" Type="String" Nullable="true" dals:CharMaxLength="-1" Name="data" dals:IsReturned="true" dals:IsQueryable="false" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="ticker" Type="String" Nullable="true" dals:CharMaxLength="10" Name="ticker" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        <EntityType Map="[dbo].[ProductInfo]" dals:TableName="ProductInfo" Name="ProductInfo" dals:IsExposed="true" dals:IsView="false" dals:TableSchema="dbo" xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <Property dals:ColumnName="companyid" Type="Int32" Nullable="true" Name="companyid" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="product" Type="String" Nullable="true" dals:CharMaxLength="50" Name="product" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        </Schema>

## <a name="see-also"></a>Vedere anche
* Se è interessati a learning e informazioni sui nodi specifici di hello e i relativi parametri, leggere questo articolo [nodi Mapping di dati del servizio OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) per le definizioni e le spiegazioni, esempi e il contesto casi di utilizzo.
* Se si è interessati a esaminare alcuni esempi, leggere questo articolo [esempi di Mapping di dati del servizio OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee codice di esempio e comprendere la sintassi di codice e il contesto.
* toohello tooreturn previsto percorso per la pubblicazione toohello un servizio dati Azure Marketplace, leggere questo articolo [Guida alla pubblicazione di dati del servizio](marketplace-publishing-data-service-creation.md).

