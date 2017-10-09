---
title: aaaAzure SDK per le note sulla versione di .NET 2.6
description: Note sulla versione di Azure SDK per .NET 2.6
services: app-service/web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: b45853d5-a2b8-4962-a22d-579cb36ae14c
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: ac613cf20da4f731fab6f35ccbf6dbeaf18c0ec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-26-release-notes"></a>Note sulla versione di Azure SDK per .NET 2.6
Questo documento contiene le note sulla versione di hello per hello Azure SDK per .NET 2.6 versione. 

È possibile sviluppare applicazioni di servizio cloud (PaaS) come destinazione .NET 4.5.2 o .NET 4.6, purché si installare manualmente .NET Framework di destinazione hello in hello ruolo del servizio Cloud con Azure SDK 2.6. Vedere [Installare .NET in un ruolo del servizio cloud](http://go.microsoft.com/fwlink/?LinkID=309796).

## <a name="service-bus-updates"></a>Aggiornamenti al bus di servizio
* Hub eventi: 
  
  * È ora possibile un controllo degli accessi mirato quando si inviano eventi tramite l'esposizione di un endpoint dell'editore aggiuntivo per l'Hub eventi.
  * Aggiunti funzionalità hub tooEvent maggiore stabilità e analisi utilizzo software.
  * Aggiunta del supporto per il protocollo Amqp su WebSocket per la messaggistica e l'Hub eventi.

## <a name="hdinsight-tools-for-visual-studio-updates"></a>Aggiornamenti a HDInsight Tools per Visual Studio
* **Miglioramento per IntelliSense**: suggerimento di metadati remoti
  
    HDInsight Tools per Visual Studio supporta ora il recupero di metadati remoti durante la modifica dello script Hive. Ad esempio, è possibile digitare **selezionare * FROM** e verranno visualizzati tutti i nomi di tabella hello. Inoltre, verranno visualizzati i nomi di colonna hello dopo aver specificato una tabella.
* **Supporto per HDInsight Emulator**
  
    Ora gli strumenti HDInsight per il supporto di Visual Studio connette tooHDInsight emulatore, pertanto è possibile sviluppare gli script Hive in locale senza introdurre alcun costo, quindi eseguire gli script con i cluster HDInsight. 
  
    Per ulteriori informazioni, vedere troppo[manuale](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409).
* **Supporto di HDInsight Tools per Visual Studio per i cluster Hadoop generici** (anteprima)
  
    Strumenti HDInsight per Visual Studio ora supportano i cluster Hadoop generici, pertanto è possibile utilizzare gli strumenti HDInsight per seguenti hello toodo di Visual Studio:
  
  * connettere il cluster di tooyour 
  * Scrivere una query Hive con supporto migliorato per IntelliSense/completamento automatico 
  * visualizzare tutti i processi di hello nel cluster con un'interfaccia utente intuitiva. 
    
    Per ulteriori informazioni, vedere troppo[manuale](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409).

## <a name="in-role-cache-updates"></a>Aggiornamenti alla Cache nel ruolo 
* **Cache nel ruolo** è stato aggiornato toouse **Microsoft Azure Storage SDK** versione 4.3. Fino ad ora, hello **Cache nel ruolo** utilizzava Azure Storage SDK versione 1.7.
  
    I clienti usando Azure SDK 2.5 o seguito aggiornare tooAzure SDK 2.6 e spostare toohello nuova versione di Azure Storage SDK. 
  
    In questa versione di archiviazione di Azure ora 2011-08-18 è pianificato toobe rimosso 1 agosto 2016. Le migrazioni di Cache nel ruolo di Azure SDK 2.5 o di sotto di too2.6 devono essere complete entro questo periodo. Per ulteriori informazioni sul ritiro di hello dell'archiviazione di Azure versione 2011-08-18, vedere [Microsoft Azure Storage Service versione rimozione aggiornamento: estensione too2016](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx).

> [!IMPORTANT]
> Annunciamo hello il 30 novembre 2016, ritiro per servizio Cache gestita di Azure e Cache nel ruolo di Azure. Si consiglia di migrare tooAzure Cache Redis in preparazione per il ritiro. Per altre informazioni sulle date e indicazioni per la migrazione, vedere [Qual è l'offerta di Cache di Azure più adatta alle mie esigenze?](../redis-cache/cache-faq.md#which-azure-cache-offering-is-right-for-me)
> 
> 

## <a name="azure-app-service-tools"></a>Strumenti di Azure App Service
Hello seguenti elementi sono stato aggiornato in versione di hello Azure SDK 2.6.

* Pubblicazione di Azure enhanced tooinclude Azure API App come una destinazione di distribuzione.
* App per le API funzionalità tooenable agli utenti con la creazione di App per le API di provisioning e il provisioning delle funzionalità.
* Server Explorer modificato tooreflect nuovo nodo servizio App, con le app Web, dispositivi mobili e API raggruppati per gruppo di risorse.
* Aggiungere i movimenti di Azure API App Client aggiungere toomost c# progetti che consentirà la generazione automatica di abilitato Swagger API applicazioni in esecuzione nella sottoscrizione di Azure dell'utente.
* Gli strumenti delle app per le API e il nodo App Service in Esplora server sono disponibili solo in Visual Studio 2013. 

## <a name="azure-resource-manager-tools-updates"></a>Aggiornamenti agli strumenti di Gestione risorse di Azure
strumenti di gestione risorse di Azure Hello sono state aggiornate tooinclude modelli di macchine virtuali, rete e archiviazione. esperienza di modifica di Hello JSON è stato aggiornato tooinclude una nuova visualizzazione struttura per modelli e di hello possibilità tooedit hello utilizzo dei frammenti JSON. Modelli distribuiti da Visual Studio utilizzare uno script di PowerShell fornito con il progetto di hello, pertanto tutte le modifiche apportate toohello script verranno utilizzate da Visual Studio.

## <a name="diagnostics-improvements-for-cloud-services"></a>Miglioramenti alla diagnostica per Servizi cloud
Azure SDK 2.6 riporta il supporto per la raccolta di log di diagnostica nell'emulatore di calcolo di Azure hello e il loro trasferimento toodevelopment archiviazione. Registra qualsiasi diagnostica (inclusi i log, Event Tracing for i registri di Windows (ETW), i contatori delle prestazioni, infrastruttura i registri eventi di windows e i registri di traccia dell'applicazione) generato quando un'applicazione hello è in esecuzione nell'emulatore hello possono essere trasferiti toodevelopment tooverify di archiviazione che è in corso la registrazione di diagnostica nel computer locale. 

account di archiviazione di diagnostica Hello può ora essere specificato nel file di configurazione (. cscfg) servizio hello rendendo più semplice account di archiviazione di diagnostica diversi di toouse per ambienti diversi. Esistono alcune differenze sostanziali tra il modo di lavorare in Azure SDK 2.4 e Azure SDK 2.6 la stringa di connessione hello. Per ulteriori informazioni sulla stringa di connessione di toouse hello archiviazione di diagnostica e impatto che i progetti vedere [configurazione della diagnostica per servizi Cloud di Azure](http://go.microsoft.com/fwlink/?LinkID=532784).

## <a name="breaking-changes"></a>Modifiche di rilievo
### <a name="azure-resource-manager-tools"></a>Strumenti di Gestione risorse di Azure
* Hello **progetti distribuzione Cloud** progetto tipo disponibile in Azure SDK 2.5 è stato rinominato troppo hello**il gruppo di risorse di Azure**.
* **Progetti di distribuzione cloud** tipo dei progetti creati in Azure SDK 2.5 hello può essere utilizzato in 2.6 ma la distribuzione del modello da Visual Studio hello avrà esito negativo. Tuttavia, la distribuzione con script di PowerShell hello continuerà a funzionare come in precedenza.  Per informazioni su come toouse **progetti distribuzione Cloud** 2.6 leggere questo [post](http://go.microsoft.com/fwlink/?LinkID=534086).

## <a name="known-issues"></a>Problemi noti
* Raccolta dei log di diagnostica nell'emulatore hello richiede un sistema operativo a 64 bit. I log di diagnostica non verranno raccolti se si usa un sistema operativo a 32 bit. Ciò non influisce su altre funzionalità dell'emulatore. 
* La versione Azure SDK 2.6 rilasciata il 29/04/2015 presenta due problemi: 
  
  * Impossibile caricare l'App universale in Visual Studio 2015 durante l'installazione nel computer di hello Azure SDK 2.6.
  * Debug di un progetto servizio Cloud avrà esito negativo in Visual Studio 2013 e Visual Studio 2015, in cui Visual Studio non risponde e si blocca durante la visualizzazione di una finestra di dialogo con messaggio "Configurazione di diagnostica per l'emulatore".
    
    5/18/2015 è stata rilasciata un' tooAzure aggiornamento SDK 2.6. versione di Hello aggiornato è 2.6.30508.1601; contiene correzioni per i due problemi descritti in precedenza. È possibile identificare compilazione hello di hello SDK dal Pannello di controllo -> programmi e funzionalità -> Strumenti di Microsoft Azure per Microsoft Visual Studio 2013 – v 2.6. colonna della versione di Hello verrà visualizzato il numero di build hello.
    
    Se ancora si trova ad affrontare hello sopra problemi, installare hello versione più recente di hello Azure SDK 2.6 per [Visual Studio 2012](http://go.microsoft.com/fwlink/p/?linkid=323511&clcid=0x409), [VS 2013](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) o [Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409).

## <a name="see-also"></a>Vedere anche
[Supporto e informazioni sul ritiro per hello Azure SDK per .NET e API](https://msdn.microsoft.com/library/azure/dn479282.aspx/)

