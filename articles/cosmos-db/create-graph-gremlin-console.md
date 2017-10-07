---
title: 'Esercitazione su Azure Cosmos DB: Creare, eseguire query e attraversare nella console Gremlin di Apache TinkerPop | Microsoft Docs'
description: Un toocreates Guida introduttiva di Azure Cosmos DB vertici, bordi e le query che utilizzano l'API Graph di Azure Cosmos DB hello.
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: terminal
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: denlee
ms.openlocfilehash: 9de64c97fec89c45cecba9e14214db472ec76f57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-query-and-traverse-a-graph-in-hello-gremlin-console"></a>Azure Cosmos DB: Crea, query e attraversare un grafico nella console Gremlin hello

Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft. Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello. 

Questa Guida introduttiva illustra come hello toocreate un account Azure Cosmos DB, il database e graph (contenitore) tramite il portale di Azure e quindi utilizzare hello [Gremlin Console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) da [Apache TinkerPop](http://tinkerpop.apache.org) toowork con API (anteprima) i dati del grafico. In questa esercitazione è creare ed eseguire query di vertici e bordi, aggiornando una proprietà di vertici, eseguire una query vertici, attraversano il grafico hello ed eliminare un vertice.

![Azure DB Cosmos dalla console di Apache Gremlin hello](./media/create-graph-gremlin-console/gremlin-console.png)

console Gremlin Hello è Groovy/Java in base e viene eseguito in Windows, Mac e Linux. È possibile scaricarlo da hello [TinkerPop Apache sito](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip).

## <a name="prerequisites"></a>Prerequisiti

È necessario un toocreate sottoscrizione di Azure, un account Azure Cosmos DB toohave per questa Guida rapida.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

È inoltre necessario hello tooinstall [Gremlin Console](http://tinkerpop.apache.org/). Usare la versione 3.2.5 o successiva.

## <a name="create-a-database-account"></a>Creare un account di database

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Aggiungere un grafo

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a id="ConnectAppService"></a>La connessione di servizio app tooyour
1. Prima di avviare hello Gremlin Console, creare o modificare file di configurazione remote secure.yaml hello nella directory apache-tinkerpop-gremlin-console-3.2.5/conf hello.
2. Immettere le configurazioni per *Hosts*, *Port*, *Username*, *Password*, *ConnectionPool* e *Serializer*:

    Impostazione|Valore consigliato|Descrizione
    ---|---|---
    hosts|[***.graphs.azure.com]|Vedere lo screenshot di seguito. Questo è il valore URI Gremlin hello nella pagina di panoramica hello del portale di Azure, tra parentesi quadre, hello finali hello: 443 / rimosso.<br><br>Questo valore può anche essere recuperato dalla scheda chiavi hello, usando il valore URI hello rimozione https://, la modifica di documenti toographs, nonché hello finali: 443 /.
    port|443|Impostare too443.
    username|*Nome utente*|risorse del form hello Hello `/dbs/<db>/colls/<coll>` in `<db>` è il nome del database e `<coll>` è il nome della raccolta.
    password|*Chiave primaria*| Vedere il secondo screenshot di seguito. Si tratta della chiave primaria, che è possibile recuperare dalla pagina chiavi hello del portale di Azure, nella casella di chiave primaria hello hello. Utilizzare il pulsante di copia hello sul lato sinistro di hello del valore di hello toocopy casella hello.
    connectionPool|{enableSsl: true}|Impostazione del pool di connessioni per SSL.
    serializer|{ className: org.apache.tinkerpop.gremlin.<br>driver.ser.GraphSONMessageSerializerV1d0,<br> config: { serializeResultToString: true }}|Impostare il valore di toothis ed eliminare qualsiasi `\n` interruzioni di riga quando si incolla in valore hello.

    Per il valore di host hello, copiare hello **Gremlin URI** valore hello **Panoramica** pagina: ![visualizzare e copiare valore URI Gremlin hello nella pagina di panoramica hello in hello portale di Azure](./media/create-graph-gremlin-console/gremlin-uri.png)

    Per il valore di password hello, copiare hello **chiave primaria** da hello **chiavi** pagina: ![visualizzare e copiare la chiave primaria nel portale di Azure hello chiavi pagina](./media/create-graph-gremlin-console/keys.png)


3. In terminale, eseguire `bin/gremlin.bat` o `bin/gremlin.sh` toostart hello [Gremlin Console](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).
4. In terminale, eseguire `:remote connect tinkerpop.server conf/remote-secure.yaml` servizio app di tooconnect tooyour.

    > [!TIP]
    > Se viene visualizzato l'errore hello `No appenders could be found for logger` assicurarsi di aver aggiornato il valore del serializzatore hello nel file remoto secure.yaml hello come descritto nel passaggio 2. 

L'installazione è riuscita. Ora che è stata completata l'installazione di hello, iniziamo esegue alcuni comandi della console.

Provare un comando count () semplice. Digitare segue hello in console hello al prompt dei comandi hello:
```
:> g.V().count()
```

> [!TIP]
> Hello preavviso `:>` che precede hello `g.V().count()` testo? 
>
> Ciò fa parte del comando hello che è necessario tootype. È importante quando si utilizza console Gremlin hello con Azure Cosmos DB.  
>
> L'omissione di questo `:>` prefisso indica comando hello di hello console tooexecute localmente, spesso su un grafico in memoria.
> Usando questa `:>` indica hello console tooexecute un comando remoto, in questo caso contro DB Cosmos (ovvero emulatore localhost hello, o un > istanza di Azure).


## <a name="create-vertices-and-edges"></a>Creare vertici e archi

Per iniziare, aggiungere cinque vertici per le persone per *Thomas*, *Mary Kay*, *Robin*, *Ben* e *Jack*.

Input (Thomas):

```
:> g.addV('person').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44).property('userid', 1)
```

Output:

```
==>[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d,label:person,type:vertex,properties:[firstName:[[id:f02a749f-b67c-4016-850e-910242d68953,value:Thomas]],lastName:[[id:f5fa3126-8818-4fda-88b0-9bb55145ce5c,value:Andersen]],age:[[id:f6390f9c-e563-433e-acbf-25627628016e,value:44]],userid:[[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d|userid,value:1]]]]
```
Input (Mary Kay):

```
:> g.addV('person').property('firstName', 'Mary Kay').property('lastName', 'Andersen').property('age', 39).property('userid', 2)

```

Output:

```
==>[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e,label:person,type:vertex,properties:[firstName:[[id:ea0604f8-14ee-4513-a48a-1734a1f28dc0,value:Mary Kay]],lastName:[[id:86d3bba5-fd60-4856-9396-c195ef7d7f4b,value:Andersen]],age:[[id:bc81b78d-30c4-4e03-8f40-50f72eb5f6da,value:39]],userid:[[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e|userid,value:2]]]]

```

Input (Robin):

```
:> g.addV('person').property('firstName', 'Robin').property('lastName', 'Wakefield').property('userid', 3)
```

Output:

```
==>[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e,label:person,type:vertex,properties:[firstName:[[id:ec65f078-7a43-4cbe-bc06-e50f2640dc4e,value:Robin]],lastName:[[id:a3937d07-0e88-45d3-a442-26fcdfb042ce,value:Wakefield]],userid:[[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e|userid,value:3]]]]
```

Input (Ben):

```
:> g.addV('person').property('firstName', 'Ben').property('lastName', 'Miller').property('userid', 4)

```

Output:

```
==>[id:ee86b670-4d24-4966-9a39-30529284b66f,label:person,type:vertex,properties:[firstName:[[id:a632469b-30fc-4157-840c-b80260871e9a,value:Ben]],lastName:[[id:4a08d307-0719-47c6-84ae-1b0b06630928,value:Miller]],userid:[[id:ee86b670-4d24-4966-9a39-30529284b66f|userid,value:4]]]]
```

Input (Jack):

```
:> g.addV('person').property('firstName', 'Jack').property('lastName', 'Connor').property('userid', 5)
```

Output:

```
==>[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469,label:person,type:vertex,properties:[firstName:[[id:4250824e-4b72-417f-af98-8034aa15559f,value:Jack]],lastName:[[id:44c1d5e1-a831-480a-bf94-5167d133549e,value:Connor]],userid:[[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469|userid,value:5]]]]
```


Aggiungere quindi gli archi per le relazioni tra le persone.

Input (Thomas -> Mary Kay):

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Mary Kay'))
```

Output:

```
==>[id:c12bf9fb-96a1-4cb7-a3f8-431e196e702f,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:0d1fa428-780c-49a5-bd3a-a68d96391d5c,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

Input (Thomas -> Robin):

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Robin'))
```

Output:

```
==>[id:58319bdd-1d3e-4f17-a106-0ddf18719d15,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:3e324073-ccfc-4ae1-8675-d450858ca116,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

Input (Robin -> Ben):

```
:> g.V().hasLabel('person').has('firstName', 'Robin').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Ben'))
```

Output:

```
==>[id:889c4d3c-549e-4d35-bc21-a3d1bfa11e00,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:40fd641d-546e-412a-abcc-58fe53891aab,outV:3e324073-ccfc-4ae1-8675-d450858ca116]
```

## <a name="update-a-vertex"></a>Aggiornare un vertice

Consente di aggiornare hello *Thomas* vertice con una nuova durata di *45*.

Input:
```
:> g.V().hasLabel('person').has('firstName', 'Thomas').property('age', 45)
```
Output:

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

## <a name="query-your-graph"></a>Eseguire query sul grafo

È ora possibile eseguire diverse query sul grafo.

Innanzitutto, provare una query con un filtro tooreturn solo gli utenti che hanno più di 40 anni fa.

Input (query con filtro):

```
:> g.V().hasLabel('person').has('age', gt(40))
```

Output:

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

Successivamente, si hello primo nome del progetto per gli utenti di hello che hanno più di 40 anni fa.

Input (query con filtro + query di proiezione):

```
:> g.V().hasLabel('person').has('age', gt(40)).values('firstName')
```

Output:

```
==>Thomas
```

## <a name="traverse-your-graph"></a>Attraversare il grafo

Consente di attraversare hello grafico tooreturn tutti gli elementi Friend di Thomas.

Input (amici di Thomas):

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person')
```

Output: 

```
==>[id:f04bc00b-cb56-46c4-a3bb-a5870c42f7ff,label:person,type:vertex,properties:[firstName:[[id:14feedec-b070-444e-b544-62be15c7167c,value:Mary Kay]],lastName:[[id:107ab421-7208-45d4-b969-bbc54481992a,value:Andersen]],age:[[id:4b08d6e4-58f5-45df-8e69-6b790b692e0a,value:39]]]]
==>[id:91605c63-4988-4b60-9a30-5144719ae326,label:person,type:vertex,properties:[firstName:[[id:f760e0e6-652a-481a-92b0-1767d9bf372e,value:Robin]],lastName:[[id:352a4caa-bad6-47e3-a7dc-90ff342cf870,value:Wakefield]]]]
```

Successivamente, iniziamo livello successivo di hello di vertici. Attraversare hello grafico tooreturn tutti i tuoi amici hello di amici di Thomas.

Input (amici degli amici di Thomas):

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```
Output:

```
==>[id:a801a0cb-ee85-44ee-a502-271685ef212e,label:person,type:vertex,properties:[firstName:[[id:b9489902-d29a-4673-8c09-c2b3fe7f8b94,value:Ben]],lastName:[[id:e084f933-9a4b-4dbc-8273-f0171265cf1d,value:Miller]]]]
```

## <a name="drop-a-vertex"></a>Eliminare un vertice

Eliminare ora un vertice dal database di graph hello.

Input (eliminazione del vertice Jack):

```
:> g.V().hasLabel('person').has('firstName', 'Jack').drop()
```

## <a name="clear-your-graph"></a>Cancellare il grafo

Infine, si cancella il database di hello di tutti i vertici e bordi.

Input:

```
:> g.E().drop()
:> g.V().drop()
```

Congratulazioni. Questa esercitazione sull'API Graph di Azure Cosmos DB è stata completata.

## <a name="review-slas-in-hello-azure-portal"></a>Esaminare i contratti di servizio nel portale di Azure hello

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Pulire le risorse

Se non si ha intenzione toocontinue toouse questa app, eliminare tutte le risorse create da questa Guida rapida hello portale di Azure con hello alla procedura seguente:  

1. Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello è stato creato. 
2. Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.

## <a name="next-steps"></a>Passaggi successivi

In questa Guida rapida, si è appreso come toocreate un account Azure Cosmos DB, creare un grafico utilizzando hello Esplora dati, creare i vertici e bordi e attraversare il grafico utilizzando console Gremlin hello. È ora possibile creare query più complesse e implementare la potente logica di attraversamento dei grafi usando Gremlin. 

> [!div class="nextstepaction"]
> [Eseguire query con Gremlin](tutorial-query-graph.md)
