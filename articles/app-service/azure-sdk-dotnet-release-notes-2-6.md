---
title: Note sulla versione di Azure SDK per .NET 2.6
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
ms.openlocfilehash: 21817b09440fc98a54dc45c9129d104b01fa387d
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="azure-sdk-for-net-26-release-notes"></a>Note sulla versione di Azure SDK per .NET 2.6
Questo documento contiene le note sulla versione per Azure SDK per .NET 2.6. 

Azure SDK 2.6 permette di sviluppare applicazioni dei servizi cloud (PaaS) che fanno riferimento a .NET 4.5.2 o .NET 4.6, purché si installi manualmente la versione di .NET Framework di destinazione nel Ruolo servizio cloud. Vedere [Installare .NET in un ruolo del servizio cloud](http://go.microsoft.com/fwlink/?LinkID=309796).

## <a name="service-bus-updates"></a>Aggiornamenti al bus di servizio
* Hub eventi: 
  
  * È ora possibile un controllo degli accessi mirato quando si inviano eventi tramite l'esposizione di un endpoint dell'editore aggiuntivo per l'Hub eventi.
  * Maggiore stabilità e altri miglioramenti aggiunti alla funzionalità Hub eventi.
  * Aggiunta del supporto per il protocollo Amqp su WebSocket per la messaggistica e l'Hub eventi.

## <a name="hdinsight-tools-for-visual-studio-updates"></a>Aggiornamenti a HDInsight Tools per Visual Studio
* **Miglioramento per IntelliSense**: suggerimento di metadati remoti
  
    HDInsight Tools per Visual Studio supporta ora il recupero di metadati remoti durante la modifica dello script Hive. Ad esempio, se si digita **SELECT * FROM** verranno visualizzati tutti i nomi di tabella. Dopo avere specificato una tabella verranno anche visualizzati i nomi di colonna.
* **Supporto per HDInsight Emulator**
  
    HDInsight Tools per Visual Studio supporta ora la connessione all'emulatore di HDInsight. È quindi possibile sviluppare localmente gli script Hive, senza incremento dei costi, quindi eseguire gli script nei cluster HDInsight. 
  
    Per altre informazioni, fare riferimento a [questo manuale](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409).
* **Supporto di HDInsight Tools per Visual Studio per i cluster Hadoop generici** (anteprima)
  
    HDInsight Tools per Visual Studio supporta ora i cluster Hadoop generici. È quindi possibile usare HDInsight Tools per Visual Studio per eseguire le operazioni seguenti:
  
  * Connettersi al cluster 
  * Scrivere una query Hive con supporto migliorato per IntelliSense/completamento automatico 
  * Visualizzare tutti i processi del cluster con un'interfaccia utente intuitiva 
    
    Per altre informazioni, fare riferimento a [questo manuale](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409).

## <a name="in-role-cache-updates"></a>Aggiornamenti alla Cache nel ruolo 
* La **Cache nel ruolo** è stata aggiornata per usare l'**SDK di Archiviazione di Microsoft Azure** versione 4.3. Fino ad ora, la **Cache nel ruolo** ha usato Azure Storage SDK versione 1.7.
  
    I clienti che usano Azure SDK 2.5 o versioni precedenti devono effettuare l'aggiornamento ad Azure SDK 2.6 e passare alla nuova versione di Azure Storage SDK. 
  
    In questo momento Archiviazione di Azure versione 2011-08-18 è pianificato per essere rimosso il 1 agosto 2016. Le migrazioni di Cache nel ruolo da Azure SDK 2.5 o versioni precedenti alla versione 2.6 devono essere complete a questo punto. Per ulteriori informazioni sul ritiro di Azure Storage versione 2011-08-18, vedere [Aggiornamento della rimozione della versione del servizio di archiviazione di Microsoft Azure: estensione al 2016](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx).

> [!IMPORTANT]
> Microsoft annuncia per il 30 novembre 2016 il ritiro del Servizio cache gestita di Azure e di Cache nel ruolo di Azure. Si consiglia di eseguire la migrazione a Cache Redis di Azure in preparazione a tale ritiro. Per altre informazioni sulle date e indicazioni per la migrazione, vedere [Qual è l'offerta di Cache di Azure più adatta alle mie esigenze?](../redis-cache/cache-faq.md#which-azure-cache-offering-is-right-for-me)
> 
> 

## <a name="azure-app-service-tools"></a>Strumenti di Azure App Service
Gli elementi seguenti sono stati aggiornati nella versione Azure SDK 2.6.

* Pubblicazione di Azure migliorata per includere le app per le API Azure come destinazione di distribuzione.
* Funzionalità di provisioning delle app per le API per offrire la funzionalità di creazione e provisioning delle app per le API agli utenti.
* Esplora server modificato per riflettere il nuovo nodo App Service, con app Web, mobili e per le API raggruppate in base a Gruppo di risorse.
* Gesto Aggiungi client di app per le API di Azure aggiunto alla maggior parte dei progetti C# che permetteranno la generazione automatica di app per le API abilitate per Swagger in esecuzione nella sottoscrizione di Azure di un utente.
* Gli strumenti delle app per le API e il nodo App Service in Esplora server sono disponibili solo in Visual Studio 2013. 

## <a name="azure-resource-manager-tools-updates"></a>Aggiornamenti agli strumenti di Gestione risorse di Azure
Gli strumenti di Gestione risorse di Azure sono stati aggiornati per includere i modelli per Macchine virtuali, Rete e Archiviazione. L'esperienza di modifica JSON è stata aggiornata per includere una nuova visualizzazione struttura per i modelli e la possibilità di modificare i modelli usando frammenti di codice JSON. I modelli distribuiti da Visual Studio usano uno script PowerShell fornito con il progetto, quindi eventuali modifiche apportate allo script verranno usate da Visual Studio.

## <a name="diagnostics-improvements-for-cloud-services"></a>Miglioramenti alla diagnostica per Servizi cloud
Azure SDK 2.6 rende di nuovo disponibile il supporto per la raccolta di log di diagnostica nell'emulatore di calcolo di Azure e per il trasferimento dei log nell'archiviazione per lo sviluppo. Eventuali log di diagnostica (inclusi i log di traccia dell'applicazione, i log ETW (Event Tracing for Windows), i contatori delle prestazioni, i log di infrastruttura e i registri eventi di Windows) generati durante l'esecuzione dell'applicazione nell'emulatore possono essere trasferiti all'archiviazione per lo sviluppo per verificare il funzionamento corretto della registrazione di diagnostica nella macchina locale. 

È ora possibile specificare l'account di archiviazione della diagnostica nel file di configurazione del servizio (con estensione cscfg), semplificando l'uso di diversi account di archiviazione della diagnostica per diversi ambienti. Il funzionamento della stringa di connessione presenta alcune differenze sostanziali tra Azure SDK 2.4 e Azure SDK 2.6. Per altre informazioni su come usare la stringa di connessione dell'archiviazione di Diagnostica e sul relativo impatto sui progetti, vedere [Configurazione della diagnostica per i servizi cloud e le macchine virtuali di Azure](http://go.microsoft.com/fwlink/?LinkID=532784).

## <a name="breaking-changes"></a>Modifiche di rilievo
### <a name="azure-resource-manager-tools"></a>Strumenti di Gestione risorse di Azure
* Il tipo di progetto **Progetti distribuzione cloud** disponibile in Azure SDK 2.5 è stato rinominato in **Gruppo di risorse di Azure**.
* **Progetti distribuzione cloud** di progetti creati in Azure SDK 2.5 può essere usato in 2.6 ma la distribuzione del modello da Visual Studio avrà esito negativo. La distribuzione con lo script di PowerShell, tuttavia, funziona ancora correttamente.  Per informazioni su come usare **Progetti distribuzione cloud** in 2.6, leggere questo [post](http://go.microsoft.com/fwlink/?LinkID=534086).

## <a name="known-issues"></a>Problemi noti
* Per la raccolta di log di diagnostica nell'emulatore è necessario un sistema operativo a 64 bit. I log di diagnostica non verranno raccolti se si usa un sistema operativo a 32 bit. Ciò non influisce su altre funzionalità dell'emulatore. 
* La versione Azure SDK 2.6 rilasciata il 29/04/2015 presenta due problemi: 
  
  * Non è possibile caricare l'app universale in Visual Studio 2015 durante l'installazione di Azure SDK 2.6 nel computer.
  * Il debug di un progetto di servizio cloud ha esito negativo in Visual Studio 2013 e Visual Studio 2015: Visual Studio non risponde e si blocca, mostrando una finestra di dialogo con il messaggio "Configurazione della diagnostica per l'emulatore".
    
    Il 18/05/2015 è stato rilasciato un aggiornamento di Azure SDK 2.6. La versione aggiornata è la 2.6.30508.1601 e contiene correzioni per i due problemi descritti in precedenza. È possibile identificare la build dell'SDK tramite Pannello di controllo -> Programmi e funzionalità -> Strumenti di Microsoft Azure per Microsoft Visual Studio 2013 – v 2.6. Nella colonna relativa alla versione verrà visualizzato il numero di build.
    
    Se i problemi illustrati persistono, installare la versione più recente di Azure SDK 2.6 per [VS 2012](http://go.microsoft.com/fwlink/p/?linkid=323511&clcid=0x409), [VS 2013](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) o [VS 2015](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409).

## <a name="see-also"></a>Vedere anche
[Informazioni sul Supporto e il Ritiro di Azure SDK per .NET e API](https://msdn.microsoft.com/library/azure/dn479282.aspx/)

