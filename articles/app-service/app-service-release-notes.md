---
title: note sulla versione di SDK per .NET 2.5.1 aaaAzure
description: Note sulla versione di Azure SDK per .NET 2.5.1
services: app-service
documentationcenter: .net,nodejs,java
author: Juliako
manager: erikre
editor: 
ms.assetid: 8d3d815f-bb58-447e-8ff0-f9b9603c7b00
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/10/2016
ms.author: juliako
ms.openlocfilehash: 5ee7688617c966baa409045881c172bbbc55ff63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-251-release-notes"></a>Note sulla versione di Azure SDK per .NET 2.5.1
Questo documento contiene le note sulla versione di hello per hello Azure SDK per .NET 2.5.1 rilasciare. 

## <a name="azure-sdk-for-net-251-release-notes"></a>Note sulla versione di Azure SDK per .NET 2.5.1
di seguito Hello sono nuove funzionalità e gli aggiornamenti in Azure SDK per .NET 2.5.1 hello.

* Nuove funzionalità o scenari correlati troppo**le estensioni degli strumenti Web**. 
  
  * Siti Web di Azure è stato rinominato tooAzure servizio App. Per altre informazioni, vedere [Azure App Service e i servizi di Azure esistenti](../app-service-web/app-service-changes-existing-services.md).
  * Supporto tecnico di Azure API App (anteprima) è stato aggiunto in modo che i clienti possono pubblicare progetti ASP.NET come App per le API e quindi utilizzare hello Aggiungi > movimenti Azure API App Client in progetti toogenerate codice c# basato sulla struttura hello di hello distribuito App per le API. 
  * il nodo siti Web Hello in Esplora Server è stato deprecato anziché il nodo servizio App di Azure hello, che contiene il supporto per la risorsa in base al gruppo di Azure API App, App per dispositivi mobili e App Web di raggruppamento.
  * Supporto tecnico di Azure (anteprima) App per dispositivi mobili è stato aggiunto in modo che i clienti possono creare nuovi progetti di App per dispositivi mobili, aggiungere il controller di App per dispositivi mobili, pubblicare progetti hello e debug delle applicazioni in modalità remota.
  * Aggiungere > movimenti Azure API App Client supporta ora i file JSON Swagger locali, pertanto gli sviluppatori di Web API possono utilizzare NuGets di terze parti come Swashbuckle toogenerate Swagger o modificarla manualmente. In questo modo, client gli sviluppatori possono utilizzare tooconsume funzionalità di generazione di codice hello qualsiasi endpoint Swagger nei progetti c#. 
  * App Web e App per le API di finestre di dialogo di pubblicazione sono state migliorate toosupport hello portale di Azure concetto di raggruppamento di risorse e selezione/creazione di gruppi di risorse di Azure e piani di servizio App sono rappresentati in hello nuova App Web e App per le API provisioning finestra di dialogo. 
  * I nodi di Azure API App Server Explorer forniscono collegamenti toohello che App complete per le API di collegamento hello portale di Azure, nonché altre funzionalità come il flusso di Log e il debug remoto.
    
    Per informazioni sui problemi noti e sulle limitazioni in Azure SDK .NET 2.5.1, vedere [questa](app-service-release-notes.md#known_issues_2_5_1) sezione più avanti nell'articolo.
* Nuove funzionalità o scenari correlati troppo**strumenti HDInsight** in Visual Studio sono abilitati in questa versione. 
  
  * Convalida locale di script Hive. Scegliere il pulsante di script di convalida di hello nella hello barra degli strumenti toosee se sono presenti errori nello script. 
  * Debug migliorato dei processi Hive. È ora possibile eseguire il debug di processi Hive tramite l'accesso ai log Yarn in Visual Studio. Se l'applicazione presenta problemi di prestazioni, l'esame dei log YARN può fornire informazioni utili.
  * (Anteprima pubblica) Completamento automatico di parole chiave e supporto IntelliSense per Hive. toohelp si creano script Hive, gli strumenti HDInsight per Visual Studio aggiungere il completamento automatico (parola chiave) e il supporto IntelliSense per l'Hive.
  * Supporto per Storm. È ora possibile utilizzare gli strumenti HDInsight per Visual Studio toodevelop Storm topologie/Spouts/bulloni in c#. È quindi possibile inviare hello sviluppato cluster Storm tooa di topologia e visualizzare lo stato fulmine/topologia/beccuccio hello. È possibile utilizzare i registri di sistema e cliente effettua l'accesso tootroubleshoot l'elevato numero bulloni/topologie/Spouts. È anche possibile usare asset JAVA esistenti in Storm su HDInsight.
    
    Per altre informazioni, vedere [Introduzione all'uso di HDInsight Hadoop Tools per Visual Studio](../hdinsight/hdinsight-hadoop-visual-studio-tools-get-started.md).

## <a id="known_issues_2_5_1"></a>Problemi noti e limitazioni di Azure SDK per .NET 2.5.1
* App per le API di Azure è visibile come destinazione di sviluppo per app per dispositivi mobili. App Web deve essere la destinazione solo di hello per App per dispositivi mobili fino a una versione successiva. 
* Azure App per le API di provisioning può comportare esito positivo, ma in modo intermittente fail tooupdate hello stato hello nella finestra attività di servizio App di Azure. Soluzione alternativa stato toocheck di hello nuova Azure API App nel portale di Azure hello. 
* L'uso di File > Nuovo progetto > App per le API > F5 può dare luogo a un errore HTTP poiché non è presente un file /index.html predefinito. Soluzione alternativa è toomanually Sfoglia toohello/api/valori URL. 
* Le icone di Esplora server possono apparire appiattite in modo intermittente. Il problema si risolve con il riavvio di VS. 
* Se viene generata un'eccezione durante il provisioning di App Web o App per le API (ad esempio errori di quota superata o nome del gateway Azure API App duplicato), gli errori di hello mostrano alcuni testo JSON non elaborato. 
* Problemi intermittenti di creazione del progetto quando Application Insights è selezionato nel momento della creazione del progetto.
* In alcuni casi, il codice di Azure API App Client hello generato manca spazi dei nomi, è necessario toobe manualmente incluse (o importati automaticamente tramite segnali di Visual Studio) per codice toocompile. 
* Progetti di App per dispositivi mobili devono essere pubblicato tooweb App, ma è necessario selezionare un sito che è stato creato come un'App Mobile nel portale di Azure hello poiché i progetti di App per dispositivi mobili richiedono un database. 
* pagina iniziale di Hello per App per dispositivi mobili viene utilizzato il termine di hello "servizio mobile" anziché "App per dispositivi mobili" 
* Toocreate minuti tooa potrebbe richiedere la creazione del progetto di App per dispositivi mobili. 
* Durante l'App per le API di provisioning (in alcuni casi) errore torna dal hello Azure API reflection che le autorizzazioni di hello non è possibile impostare in modo corretto, mentre hello App per le API sia stato preparato correttamente ed è pronto per l'utilizzo. È possibile impostare manualmente le autorizzazioni utilizzando hello portale di Azure.
* Application Insights non è supportato in modelli di app per le API e di app per dispositivi mobili.
* I progetti di app per le API non possono essere usati insieme a progetti di servizio cloud.
* I modelli di progetti di app per le API sono disponibili solo in C#.
* Utilizzo di App per le API tramite il menu di scelta rapida "Aggiungere Azure API App Client" hello è supportato solo in c#.

