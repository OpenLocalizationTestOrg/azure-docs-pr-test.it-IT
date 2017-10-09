---
title: note sulla versione di SDK per .NET 2.7 e .NET 2.7.1 aaaAzure
description: Note sulla versione di Azure SDK per .NET 2.7 e .NET 2.7.1
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: 877d070a-9bd5-49b3-8fac-6bb5f65c3554
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 8ec72b0f18702e6d811f0cbe4790685be7881d96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-27-and-net-271-release-notes"></a>Note sulla versione di Azure SDK per .NET 2.7 e .NET 2.7.1
## <a name="overview"></a>Panoramica
Questo documento contiene le note sulla versione di hello per hello Azure SDK versione 2.7 .NET. 

documento Hello contiene anche le note sulla versione di hello per hello Azure SDK per .NET 2.7.1 rilasciare.

Azure SDK 2.7 è supportato solo in Visual Studio 2015 e Visual Studio 2013. [Azure SDK 2.6](https://azure.microsoft.com/downloads/) hello ultima supportata SDK per Visual Studio 2012.

Per informazioni dettagliate su questa versione, vedere il [post di annuncio di Azure SDK 2.7](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/) e il [post di annuncio di Azure SDK 2.7.1](http://go.microsoft.com/fwlink/?LinkId=623850).

## <a name="azure-sdk-for-net-27"></a>Azure SDK per .NET 2.7
### <a name="sign-in-improvements-for-visual-studio-2015"></a>Miglioramenti relativi all'accesso per Visual Studio 2015
Azure 2.7 SDK per Visual Studio 2015 supporta nuove funzionalità di gestione identità hello in Visual Studio 2015.  Ciò include il supporto per gli account che accedono ad Azure tramite il controllo degli accessi in base al ruolo, Cloud Solution Provider, DreamSpark e altri tipi di account e sottoscrizioni.

Hello Accedi miglioramenti inclusi in Azure SDK 2.7 sono disponibili solo in Visual Studio 2015. Il supporto per Visual Studio 2013 è incluso in Azure SDK 2.7.1.

### <a name="mobile-sdk"></a>Mobile SDK
Aggiornato **App per dispositivi mobili** tooreflect modelli più recenti [pacchetto NuGet](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) e processo di installazione.

### <a name="service-bus"></a>Bus di servizio
Correzioni di bug e miglioramenti generali. Per informazioni su aggiornamenti e funzionalità, consultare le note sulla versione toohello di hello più recente [NuGet di Service Bus](http://www.nuget.org/packages/WindowsAzure.ServiceBus/).

### <a name="hdinsight-tools"></a>Strumenti HDInsight
In questa versione hello aggiornamenti seguenti sono stati apportati. Questi aggiornamenti sono in anteprima. Per altre informazioni, vedere [questo blog](http://go.microsoft.com/fwlink/?LinkId=619108).

* Grafici di hive per processi Hive su Tez
* Supporto completo di IntelliSense per DML Hive
* Supporto del modello Pig
* Modelli Storm per servizi di Azure

#### <a name="breaking-changes"></a>Modifiche di rilievo
* Vecchio **Storm** progetto deve essere aggiornato quando si utilizza questa versione di hello tools. Per altre informazioni, vedere [questo blog](http://go.microsoft.com/fwlink/?LinkId=619108).
* Visual Studio Web Express non è più supportato. Per altre informazioni, vedere [questo blog](http://go.microsoft.com/fwlink/?LinkId=619108).

### <a name="azure-app-service-tools"></a>Strumenti di Azure App Service
In questa versione hello aggiornamenti seguenti sono stati apportati tooWeb le estensioni degli strumenti. Per altre informazioni, vedere [questo](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/) blog. 

* Aggiunta del supporto per gli account DreamSpark
* Modificare completo tooAzure strumenti apportati toosupport hello nuove API di gestione risorse di Azure
* Aggiunto il supporto per Azure App Service troppo[Cloud Explorer](#cloud_explorer)

#### <a name="known-issues"></a>Problemi noti
I nodi dello slot di distribuzione App Web non vengono visualizzati nel nodo slot hello in Esplora Server e i nodi figlio nello slot di distribuzione Web App non vengono caricati in Cloud Explorer. Questo problema è stato risolto e preparato per la prossima versione SDK hello. 

### <a name="cloud_explorer"></a>Cloud Explorer per Visual Studio 2015
Azure SDK 2.7 include Cloud Explorer per Visual Studio 2015 che consente di tooview le risorse di Azure, controllare le relative proprietà ed eseguire azioni chiave sviluppatore da Visual Studio. 

Cloud explorer supporta la seguente hello:

* Visualizzazioni Gruppo di risorse e Tipo di risorsa delle risorse di Azure 
* Ricerca delle risorse in base al nome (disponibile nella visualizzazione Tipo di risorsa)
* Supporto per le sottoscrizioni e le risorse con Controllo degli accessi in base al ruolo applicato 
* Pannello azione integrato che consente di visualizzare risorse tooselected specifico di azioni per gli sviluppatori. Ad esempio: collegare il debugger remoto per macchine virtuali create utilizzando hello Stack di Resource Manager, visualizzare i dati di diagnostica per via di macchine virtuali.
* Pannello delle proprietà integrato che mostra le proprietà destinate agli sviluppatori comunemente necessarie durante sviluppo e test 
* Cambio rapido di hello account toouse durante l'enumerazione di risorse (usare il comando impostazioni sulla barra degli strumenti) 
* Filtraggio di sottoscrizioni toouse durante l'enumerazione di risorse (usare il comando impostazioni sulla barra degli strumenti) 
* Collegamenti diretti toohello portale di Azure per la gestione delle risorse e gruppi di risorse 

### <a name="azure-resource-manager-tools"></a>Strumenti di Gestione risorse di Azure
Strumenti di gestione risorse di Azure Hello state toowork aggiornato con nuovi tipi di sottoscrizione e basato sui ruoli accesso controllo (RBAC).  Con queste modifiche sono inoltre incluse hello possibilità toouse nuovo account di archiviazione, inoltre archiviazione tooclassic, toostore elementi durante la distribuzione.  

Se si utilizza un progetto di gruppo di risorse di Azure da una versione precedente di hello SDK con hello 2.7 SDK, un nuovo script di distribuzione è necessario toodeploy utilizzando un nuovo account di archiviazione anziché archiviazione classico.  Verrà richiesto prima di apportare modifiche tooyour progetto tooadd hello nuovo script.  script di Hello precedente verrà rinominato e sarà necessario toomanually apportare alcuna modifica toohello nuovo script.

### <a name="storage-explorer-tools"></a>Strumenti di Esplora archivi
* Supporto per la visualizzazione di BLOB di accodamento. Altre informazioni sono disponibili in [questo post di blog](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/04/13/introducing-azure-storage-append-blob.aspx). 
* Supporto per la visualizzazione degli account di archiviazione Premium tramite Esplora server. Esplora server verrà visualizzati solo i BLOB di pagine per gli account di archiviazione premium come se fossero di tipo hello è supportato solo per gli account di archiviazione premium.

### <a name="azure-data-factory-tools-for-visual-studio"></a>Strumenti di Data factory di Azure per Visual Studio
Introduzione agli **strumenti di Data factory di Azure** per Visual Studio. Di seguito sono funzionalità hello abilitato. Per altre informazioni, vedere [questo blog](http://go.microsoft.com/fwlink/?LinkId=617530) .

* **Modello basato su authoring**: selezionare utilizzare le maiuscole/minuscole basato su modelli, i modelli di spostamento dei dati o l'elaborazione dati modelli toodeploy una soluzione di integrazione di dati end-to-end e iniziare pratica rapidamente con Data Factory. 
* **Integrazione con Esplora soluzioni per la creazione e distribuzione di entità Data factory**: creare e distribuire pipeline ed entità correlate come progetti di Visual Studio. 
* **Integrazione con la vista diagramma per l'interazione visual durante la creazione**: creare visivamente le pipeline e set di dati con l'aiuto di hello vista diagramma. 
* **Integrazione con Esplora Server per l'esplorazione e interazione con le entità già distribuite**: sfruttare hello Esplora Server toobrowse già distribuito data factory e le entità corrispondenti. Importare una data factory distribuita o qualsiasi entità (pipeline, servizio collegato, set di dati) nel progetto. 
* **Modifica di JSON con convalida dello schema e IntelliSense avanzato**: configurare e modificare con efficienza documenti JSON delle entità di Data factory con funzionalità IntelliSense avanzate e convalida dello schema 
* **Pubblicazione di un multi-ambiente**: pubblicare toodev pipeline creati, test o l'ambiente di produzione mediante la creazione di file di configurazione separato per ogni ambiente.
* **Supporto dell'elaborazione dei dati basata su Pig, Hive e .NET**: supporto per script Pig e Hive nel progetto di Data factory. Supporto dei riferimenti al progetto C# per la gestione dell'attività .NET.

## <a name="azure-sdk-for-net-271"></a>Azure SDK per .NET 2.7.1
Hello seguente sezione contiene gli aggiornamenti che sono stati introdotti con hello Azure SDK per .NET 2.7.1 rilasciare.

### <a name="hdinsight-tools"></a>Strumenti HDInsight
Per informazioni più dettagliate sugli aggiornamenti degli strumenti di HDInsight, vedere [questo blog](http://go.microsoft.com/fwlink/?LinkId=623831).

* Visualizzazione operatore processo Hive (nuova funzionalità)
  
    comprendere le query Hive migliore, funzionalità Hive Visualizza operatore hello toohelp è stato aggiunto. toosee tutti gli operatori di hello all'interno di un vertice, fare doppio clic sui vertici hello del grafico processi hello. tooview ulteriori dettagli di un operatore specifico, passare il mouse su tale operatore.
* Marcatore errori Hive (nuova funzionalità)
  
    tooenable che tooview hello gli errori grammaticali immediatamente, hello funzionalità Hive indicatore di errore è stato aggiunto. Inoltre, i messaggi di errore sono stati migliorati ed è ora possibile visualizzare gli errori grammaticali dettagliate immediatamente (fino a questa versione, era toosubmit un cluster di toohello script Hive e attendere per qualche tempo prima di ottenere i dettagli del messaggio di errore).  
* Grafico di topologia Storm (nuova funzionalità)
  
    La visualizzazione è molto importante quando si desidera toosee se la topologia di funzioni come previsto. In questa versione è stata aggiunta la visualizzazione per i grafici Storm. È possibile visualizzare metriche importanti hello per la topologia (ad esempio, un colore indica weather un determinato fulmine è "occupato" o meno). È possibile anche fare doppio clic hello fulmine/beccuccio tooview ulteriori dettagli.
* Supporto per i cluster HDInsight che sono stati creati nel portale di Azure (una correzione di bug) hello
  
    È possibile utilizzare Visual Studio tooview e inviare i processi tooall indipendentemente da dove sono stati creati i cluster hello ai cluster HDInsight.
* Supporto avanzato IntelliSense e caricamento più veloce dei metadati Hive (miglioramento)
  
    Sono stati migliorati hello IntelliSense aggiungendo ulteriori suggerimenti descrittivo. Ad esempio, gli alias di tabella ora possono essere suggeriti anche in IntelliSense in modo da facilitare la scrittura della query. Inoltre, sono stati migliorati i metadati Hive hello carica in modo sufficiente richiederà alcuni secondi toolist tutti i database di hello, tabelle e colonne del metastore Hive.

Per informazioni più dettagliate sugli aggiornamenti degli strumenti di HDInsight, vedere [questo blog](http://go.microsoft.com/fwlink/?LinkId=623831).

### <a name="improvements-in-visual-studio-2013"></a>Miglioramenti in Visual Studio 2013
* Azure SDK 2.7.1 consente tooaccess di Visual Studio 2013 gli account di Azure e le sottoscrizioni tramite Dreamspark Role Based Access Control e Cloud Solution Provider.
* Con Azure SDK 2.7.1, hello Cloud Explorer finestra è ora disponibile anche in Visual Studio 2013.

### <a name="known-issues"></a>Problemi noti
L'installazione di hello Azure SDK 2.6 o 2.7.1 per Visual Studio Community 2013 in un non - inglese del sistema operativo verrà visualizzato un avviso che hello inglese e potrebbero non corrispondere le risorse non in lingua inglese di Visual Studio. L'avviso può essere tranquillamente ignorato. Verificherà solo se macchina hello non contiene un'installazione precedente di Visual Studio Community 2013 e si sta installando hello SDK in un non - inglese del sistema operativo. avviso di Hello viene visualizzato dopo l'applicazione di language pack in hello hello RTM risorse tooVisual Studio, ma prima di applicare l'aggiornamento 4. Ignorando l'avviso hello consentirà hello language pack toocontinue e completa l'applicazione hello aggiornamento 4 la versione del language pack in hello contenuto.

I Progetti LightSwitch non sono compatibili con questa versione. Questo problema verrà risolto con hello versione SDK successivo.

## <a name="also-see"></a>Vedere anche
[Post di annuncio di Azure SDK 2.7.1](http://go.microsoft.com/fwlink/?LinkId=623850)

[Post di annuncio di Azure SDK 2.7](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/)

[Supporto e informazioni sul ritiro per hello Azure SDK per .NET e API](https://msdn.microsoft.com/library/azure/dn479282.aspx/)

