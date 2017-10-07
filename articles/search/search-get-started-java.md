---
title: aaaGet avviato con ricerca di Azure in Java | Documenti Microsoft
description: Un cloud ospitato toobuild ricerca come applicazione in Azure con Java come linguaggio di programmazione.
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 8b4df3c9-3ae5-4e3a-b4bb-74b516a91c8e
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 07/14/2016
ms.author: evboyle
ms.openlocfilehash: 5476a2103f3b60fe6ec78ff3d3fdba9fcff55c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-java"></a>Introduzione a Ricerca di Azure in Java
> [!div class="op_single_selector"]
> * [Portale](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

Informazioni su come un linguaggio personalizzato toobuild ricerca applicazione che utilizza la ricerca di Azure per la sua esperienza di ricerca. Questa esercitazione viene utilizzato hello [API REST di Azure ricerca](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello oggetti e operazioni in questo esercizio.

toorun in questo esempio, è necessario un servizio di ricerca di Azure, che è possibile iscriversi a in hello [portale Azure](https://portal.azure.com). Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per istruzioni dettagliate.

È utilizzato hello seguente toobuild software e di test in questo esempio:

* [Eclipse IDE per sviluppatori Java EE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar). Essere certi toodownload hello EE versione. Uno dei passaggi di verifica hello richiede una funzionalità che è disponibile solo in questa edizione.
* [JDK 8u40](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Apache Tomcat 8.0](http://tomcat.apache.org/download-80.cgi)

## <a name="about-hello-data"></a>Informazioni sui dati hello
Questa applicazione di esempio utilizza i dati di hello [Italia geologiche servizi (USG)](http://geonames.usgs.gov/domestic/download_data.htm)filtro sulle dimensioni di hello lo stato di Rhode Island tooreduce hello set di dati. Verrà utilizzata questa toobuild dati un'applicazione di ricerca che restituisce gli edifici punti di riferimento, ad esempio ospedale un numero e scuole, nonché funzionalità geologiche come flussi e laghi Summit.

In questa applicazione hello **SearchServlet.java** programma compila e carica hello indice utilizzando un [indicizzatore](https://msdn.microsoft.com/library/azure/dn798918.aspx) costrutto, recupero hello filtrati soltanto set di dati da un Database SQL di Azure pubblico. Le credenziali predefinite e l'origine dati online toohello informazioni di connessione sono incluse nel codice programma hello. In termini di accesso ai dati, non è necessaria alcuna ulteriore configurazione.

> [!NOTE]
> In questo set di dati toostay in limite dei documenti di hello disponibile a livello di prezzo 10.000 hello è stato applicato un filtro. Se si utilizza il livello standard di hello, questo limite non si applica ed è possibile modificare questo toouse di codice un set di dati più grande. Per ulteriori informazioni sulla capacità per ogni livello di prezzo, vedere [Limiti e vincoli](search-limits-quotas-capacity.md).
> 
> 

## <a name="about-hello-program-files"></a>Informazioni sui file di programma hello
Hello elenco seguente vengono descritti i file hello esempio toothis pertinente.

* Search.jsp: Fornisce l'interfaccia utente di hello
* SearchServlet.java: Fornisce i metodi (simile tooa controller MVC)
* SearchServiceClient.java: gestisce le richieste HTTP 
* SearchServiceHelper.java: una classe di supporto che fornisce metodi statici
* Document.Java: Fornisce il modello di dati di hello
* config.Properties: imposta l'URL del servizio di ricerca hello e la chiave api
* Pom.xml: una dipendenza Maven

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a>Trovare il nome del servizio hello e la chiave api del servizio di ricerca di Azure
Tutte le chiamate API REST in ricerca di Azure è necessario disporre URL del servizio hello e una chiave api. 

1. Accedi toohello [portale Azure](https://portal.azure.com).
2. Nella barra di spostamento hello, fare clic su **servizio di ricerca** toolist tutti i servizi di ricerca di Azure hello effettuato il provisioning per la sottoscrizione.
3. Selezionare servizio hello da toouse.
4. Nel dashboard del servizio hello, si noterà riquadri per informazioni essenziali e icona per l'accesso alle chiavi amministratore hello hello.
   
      ![][3]
5. Copiare l'URL del servizio hello e una chiave amministratore. Saranno necessari in un secondo momento, quando vengono aggiunte toohello **config.properties** file.

## <a name="download-hello-sample-files"></a>Scaricare i file di esempio hello
1. Andare troppo[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) su GitHub.
2. Fare clic su **ZIP di Download**, salvare toodisk di file con estensione zip hello e quindi estrarre tutti i file hello in esso contenuti. Prendere in considerazione l'estrazione hello di file in toomake di area di lavoro del linguaggio è più semplice progetto di hello toofind in un secondo momento.
3. file di esempio Hello sono di sola lettura. Fare clic sulla proprietà della cartella e attributo di sola lettura non crittografato hello.

Tutte le successive modifiche e le istruzioni di esecuzione verranno effettuate sui file in questa cartella.  

## <a name="import-project"></a>Importare il progetto
1. In Eclipse scegliere **File** > **Importa** > **Generale** >  **Progetti esistenti nell'area di lavoro**.
   
    ![][4]
2. In **directory principale selezionare**, toohello cartella contenente file di esempio. Selezionare la cartella hello che contiene una cartella di hello. Project. progetto Hello dovrebbe essere visualizzati in hello **progetti** elenco come un elemento selezionato.
   
    ![][12]
3. Fare clic su **Finish**.
4. Utilizzare **Esplora progetti** tooview e modificare file hello. Se non è già aperto, fare clic su **finestra** > **Mostra visualizzazione** > **Esplora progetti** o utilizzare tooopen di scelta rapida hello è.

## <a name="configure-hello-service-url-and-api-key"></a>Configurare l'URL del servizio hello e la chiave api
1. In **Esplora progetti**, fare doppio clic su **config.properties** tooedit le impostazioni di configurazione hello contenente il nome di server hello e la chiave api.
2. Fare riferimento toohello passaggi più indietro in questo articolo, in cui è possibile trovare hello URL del servizio e la chiave api in hello [portale Azure](https://portal.azure.com), i valori hello tooget ora immetterà **config.properties**.
3. In **config.properties**, sostituire "Chiave Api" con hello chiave api per il servizio. Successivamente, il nome del servizio (hello primo componente del hello URL http://servicename.search.windows.net) sostituisce la "nome del servizio" hello stesso file.
   
    ![][5]

## <a name="configure-hello-project-build-and-runtime-environments"></a>Configurare gli ambienti di progetto, compilazione e runtime hello
1. In Project Explorer di Eclipse fare clic sul progetto hello > **proprietà** > **facet progetto**.
2. Selezionare **Dynamic Web Module**, **Java** e **JavaScript**.
   
    ![][6]
3. Fare clic su **Apply**.
4. Selezionare **Finestra** > **Preferenze** > **Server** > **Runtime Environments (Ambienti di runtime)** > **Aggiungi..**.
5. Espandere Apache e selezionare la versione di hello del server Apache Tomcat hello che è installato in precedenza. In questo sistema è installata la versione 8.
   
    ![][7]
6. Nella pagina successiva di hello, specificare directory di installazione di Tomcat hello. In un computer Windows, sarà probabilmente C:\Programmi\Microsoft Files\Apache Software Foundation\Tomcat *versione*.
7. Fare clic su **Fine**.
8. Selezionare **Finestra** > **Preferenze** > **Java** > **Installed JREs (JRE installati)** > **Aggiungi**.
9. In **Add JRE** (Aggiungi JRE) selezionare **Standard VM (VM standard)**.
10. Fare clic su **Avanti**.
11. Nella definizione dell'ambiente JRE, nella home di JRE, fare clic su **Directory**.
12. Passare troppo**programmi** > **Java** e selezionare hello JDK è installato in precedenza. È importante tooselect hello JDK come hello JRE.
13. In JREs installato, scegliere hello **JDK**. Le impostazioni dovrebbero essere simile toohello seguente schermata.
    
    ![][9]
14. Facoltativamente, selezionare **finestra** > **Browser Web** > **Internet Explorer** tooopen un'applicazione hello in una finestra del browser esterno. L’utilizzo di un browser esterno offre una migliore esperienza di applicazione Web.
    
    ![][8]

Attività di configurazione hello è stata completata. Successivamente, è possibile compilare ed eseguire il progetto di hello.

## <a name="build-hello-project"></a>Compilare il progetto hello
1. In Esplora progetti, fare doppio clic su nome progetto hello e scegliere **runas** > **compilazione Maven...**  progetto hello tooconfigure.
   
    ![][10]
2. In Edit Configuration, in Goals, digitare "clean install", quindi fare clic su **Run**.

I messaggi di stato sono finestra della console toohello output. Dovrebbe essere progetto hello che indica di COMPILAZIONI COMPLETATE compilato senza errori.

## <a name="run-hello-app"></a>Eseguire app hello
In questo ultimo passaggio, si eseguirà un'applicazione hello in un ambiente di runtime del server locale.

Se ancora non è stato specificato un ambiente di runtime del server in Eclipse, è necessario prima di tutto toodo.

1. In Project Explorer espandere **WebContent**.
2. Fare clic con il pulsante destro del mouse su **Search.jsp** > **Esegui come** > **Esegui come controllo server**. Selezionare server Apache Tomcat hello e quindi fare clic su **eseguire**.

> [!TIP]
> Se si utilizza un toostore non predefinito dell'area di lavoro del progetto, è necessario toomodify **Run Configuration** toopoint toohello progetto percorso tooavoid un errore di avvio del server. In Esplora progetti fare clic con il pulsante destro del mouse su **Search.jsp** > **Esegui come** > **Configurazione di esecuzione**. Selezionare server Apache Tomcat hello. Fare clic su **Arguments**. Fare clic su **dell'area di lavoro** o **File System** tooset hello contenente il progetto hello.
> 
> 

Quando si esegue un'applicazione hello, verrà visualizzato una finestra del browser, che fornisce una casella di ricerca per l'immissione di condizioni.

Attendere circa un minuto prima di scegliere **ricerca** toogive hello servizio ora toocreate e carico hello l'indice. Se si verifica un errore HTTP 404, è sufficiente toowait un po' più lungo prima di riprovare.

## <a name="search-on-usgs-data"></a>Eseguire ricerche sui dati dei servizi geologici degli Stati Uniti
Hello soltanto set di dati include i record che sono rilevante toohello lo stato di Rhode Island. Se si fa clic **ricerca** su una casella di ricerca vuoto, si otterrà voci primi 50 hello, hello predefinito.

Immettendo un termine di ricerca fornisce il motore di ricerca hello qualcosa toogo su. Provare a immettere un nome locale. "Roger Williams" è stato governor prima di hello del Rhode Island. Numerosi parchi, edifici e scuole prendono il suo nome.

![][11]

È inoltre possibile tentare con uno dei termini seguenti:

* Pawtucket
* Pembroke
* goose +cape

## <a name="next-steps"></a>Passaggi successivi
Si tratta di hello prima esercitazione ricerca di Azure basato su Java e hello soltanto set di dati. Nel corso del tempo, toodemonstrate questa esercitazione verrà esteso le funzionalità di ricerca aggiuntive è toouse in soluzioni personalizzate.

Se si dispone già di alcuni concetti di base in ricerca di Azure, è possibile utilizzare questo esempio come un springboard per ulteriore sperimentazione, forse aumento hello [pagina ricerca](search-pagination-page-layout.md), o l'implementazione di [navigazione con facet](search-faceted-navigation.md). È inoltre possibile migliorare alla pagina dei risultati di ricerca hello aggiungendo i conteggi e l'invio in batch di documenti in modo che gli utenti possono spostarsi tra i risultati di hello.

TooAzure nuova ricerca? È consigliabile tentare altri toodevelop esercitazioni la comprensione di ciò che è possibile creare. Visitare il nostro [pagina della documentazione](https://azure.microsoft.com/documentation/services/search/) toofind più risorse. È inoltre possibile visualizzare i collegamenti di hello nel nostro [elenco Video e un'esercitazione](search-video-demo-tutorial-list.md) tooaccess ulteriori informazioni.

<!--Image references-->
[1]: ./media/search-get-started-java/create-search-portal-1.PNG
[2]: ./media/search-get-started-java/create-search-portal-21.PNG
[3]: ./media/search-get-started-java/create-search-portal-31.PNG
[4]: ./media/search-get-started-java/AzSearch-Java-Import1.PNG
[5]: ./media/search-get-started-java/AzSearch-Java-config1.PNG
[6]: ./media/search-get-started-java/AzSearch-Java-ProjectFacets1.PNG
[7]: ./media/search-get-started-java/AzSearch-Java-runtime1.PNG
[8]: ./media/search-get-started-java/AzSearch-Java-Browser1.PNG
[9]: ./media/search-get-started-java/AzSearch-Java-JREPref1.PNG
[10]: ./media/search-get-started-java/AzSearch-Java-BuildProject1.PNG
[11]: ./media/search-get-started-java/rogerwilliamsschool1.PNG
[12]: ./media/search-get-started-java/AzSearch-Java-SelectProject.png
