---
title: aaaGet avviato con ricerca di Azure in Node.js | Documenti Microsoft
description: Illustra la creazione di un'applicazione di ricerca in un servizio di ricerca cloud ospitato in Azure usando Node.js come linguaggio di programmazione.
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: evboyle
ms.openlocfilehash: e9c7d756c2ea191ee2a285485c90439b96aa73b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a>Introduzione a Ricerca di Azure in Node.js
> [!div class="op_single_selector"]
> * [Portale](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

Informazioni su come toobuild un Node.js personalizzato ricerca applicazione che utilizza la ricerca di Azure per la sua esperienza di ricerca. Questa esercitazione viene utilizzato hello [API REST di Azure ricerca](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello oggetti e operazioni in questo esercizio.

È stato usato [Node.js](https://Nodejs.org) e NPM, [Sublime 3 testo](http://www.sublimetext.com/3)e Windows PowerShell in Windows 8.1 toodevelop e testare questo codice.

toorun in questo esempio, è necessario un servizio di ricerca di Azure, che è possibile iscriversi a in hello [portale di Azure](https://portal.azure.com). Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per istruzioni dettagliate.

## <a name="about-hello-data"></a>Informazioni sui dati hello
Questa applicazione di esempio utilizza i dati di hello [Italia geologiche servizi (USG)](http://geonames.usgs.gov/domestic/download_data.htm)filtro sulle dimensioni di hello lo stato di Rhode Island tooreduce hello set di dati. Verrà utilizzata questa toobuild dati un'applicazione di ricerca che restituisce gli edifici punti di riferimento, ad esempio ospedale un numero e scuole, nonché funzionalità geologiche come flussi e laghi Summit.

In questa applicazione hello **DataIndexer** programma compila e carica hello indice utilizzando un [indicizzatore](https://msdn.microsoft.com/library/azure/dn798918.aspx) costrutto, recupero hello filtrati soltanto set di dati da un Database SQL di Azure pubblico. Connessione e credenziali origine dati online toohello di informazioni viene fornita nel codice programma hello. Non è necessaria ulteriore configurazione.

> [!NOTE]
> In questo set di dati toostay in limite dei documenti di hello disponibile a livello di prezzo 10.000 hello è stato applicato un filtro. Se si utilizza il livello standard di hello, questo limite non si applica. Per altre informazioni sulla capacità per ogni piano tariffario, vedere [Limiti del servizio di ricerca](search-limits-quotas-capacity.md).
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a>Trovare il nome del servizio hello e la chiave api del servizio di ricerca di Azure
Dopo aver creato il servizio di hello, restituire toohello tooget portale hello URL o `api-key`. Connessioni tooyour servizio di ricerca, è necessario disporre sia URL hello e un `api-key` chiamata hello tooauthenticate.

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Nella barra di spostamento hello, fare clic su **servizio di ricerca** toolist il provisioning di tutti i servizi di ricerca di Azure per la sottoscrizione.
3. Selezionare servizio hello da toouse.
4. Nel dashboard del servizio hello, dovrebbe essere riquadri per informazioni essenziali, ad esempio di icona per l'accesso alle chiavi amministratore hello hello.
5. Copiare l'URL del servizio hello, una chiave amministratore e una chiave di query. È necessario in seguito tutti e tre quando vengono aggiunte toohello config.js file.

## <a name="download-hello-sample-files"></a>Scaricare i file di esempio hello
Utilizzare uno dei seguenti approcci toodownload hello-esempio hello.

1. Andare troppo[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).
2. Fare clic su **ZIP di Download**, salvare file con estensione zip hello e quindi estrarre tutti i file hello in esso contenuti.

Tutte le successive modifiche e le istruzioni di esecuzione vengono effettuate sui file in questa cartella.

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a>Aggiornare config.js hello. con l'URL del servizio di ricerca e la chiave API
Utilizzando hello URL e la chiave api copiato in precedenza, specificare l'URL di hello, chiave di amministrazione e della chiave di query nel file di configurazione.

Le chiavi di amministrazione forniscono il controllo completo sulle operazioni del servizio, incluse creazione ed eliminazione di un indice e caricamento di documenti. Al contrario, le chiavi di query sono per le operazioni di sola lettura, in genere utilizzate dalle applicazioni client che si connettono tooAzure ricerca.

In questo esempio, si includono query hello toohelp chiave ribadire hello consigliata per l'utilizzo di una chiave di query hello nelle applicazioni client.

Hello seguente schermata mostra **config.js** aperto in un editor di testo con hello rilevante movimenti delimitato in modo da poter visualizzare in file hello tooupdate con hello valori che è valido per il servizio di ricerca.

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a>Host di un ambiente di runtime per l'esempio hello
esempio Hello richiede un server HTTP, che è possibile installare a livello globale tramite npm.

Utilizzare una finestra di PowerShell per i seguenti comandi hello.

1. Esplorazione delle cartelle toohello contenente hello **package. JSON** file.
2. Digitare `npm install`.
3. Digitare `npm install -g http-server`.

## <a name="build-hello-index-and-run-hello-application"></a>Compilare hello indice ed eseguire un'applicazione hello
1. Digitare `npm run indexDocuments`.
2. Digitare `npm run build`.
3. Digitare `npm run start_server`.
4. Inserire nel browser l'indirizzo `http://localhost:8080/index.html`

## <a name="search-on-usgs-data"></a>Eseguire ricerche sui dati dei servizi geologici degli Stati Uniti
Hello soltanto set di dati include i record che sono rilevante toohello lo stato di Rhode Island. Se si fa clic **ricerca** su una casella di ricerca vuoto, ottenere voci primi 50 hello, hello predefinito.

Immettendo un termine di ricerca offre il motore di ricerca hello qualcosa toogo in. Provare a immettere un nome locale. "Roger Williams" è stato governor prima di hello del Rhode Island. Numerosi parchi, edifici e scuole prendono il suo nome.

![][9]

È inoltre possibile tentare con uno dei termini seguenti:

* Pawtucket
* Pembroke
* goose +cape

## <a name="next-steps"></a>Passaggi successivi
Si tratta di hello prima esercitazione ricerca di Azure in base a Node.js e hello soltanto set di dati. Nel corso del tempo, toodemonstrate questa esercitazione verrà esteso le funzionalità di ricerca aggiuntive è toouse in soluzioni personalizzate.

Se si dispone già delle nozioni di base di Ricerca di Azure, è possibile usare questo esempio come base di prova per i suggerimenti di alternative (query di suggerimento per la digitazione e completamento automatico), filtri ed esplorazione basata su facet. È inoltre possibile migliorare alla pagina dei risultati di ricerca hello aggiungendo i conteggi e l'invio in batch di documenti in modo che gli utenti possono spostarsi tra i risultati di hello.

TooAzure nuova ricerca? È consigliabile tentare altri toodevelop esercitazioni la comprensione di ciò che è possibile creare. Visitare il nostro [pagina della documentazione](https://azure.microsoft.com/documentation/services/search/) toofind più risorse. È inoltre possibile visualizzare i collegamenti di hello nel nostro [elenco Video e un'esercitazione](search-video-demo-tutorial-list.md) tooaccess ulteriori informazioni.

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
