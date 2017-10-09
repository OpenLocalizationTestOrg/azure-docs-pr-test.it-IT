---
title: SDK per le note sulla versione di .NET 2.8 aaaAzure
description: Note sulla versione di Azure SDK per .NET 2.8
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: de7207ff-ba4f-4008-9141-8742fcaa3254
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 2722dcdd27bf9ab65b48e91dcdb545536f987dd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-28-281-and-282"></a>Azure SDK per .NET 2.8, 2.8.1 e 2.8.2
## <a name="overview"></a>Panoramica
In questo articolo contiene note sulla versione di hello (che include i problemi noti e modifiche di rilievo) per hello Azure SDK per .NET 2.8, 2.8.1 e 2.8.2 rilascia. 

Per un elenco completo delle nuove funzionalità e gli aggiornamenti apportati in questa versione, vedere hello [Azure SDK 2.8 per Visual Studio 2013 e Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/) annuncio. 

## <a name="azure-sdk-for-net-28"></a>Azure SDK per .NET 2.8
### <a name="download-azure-sdk-for-net-28"></a>Scaricare Azure SDK per .NET 2.8
[Azure SDK per .NET 2.8 per Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkId=699285) 

[Azure SDK per .NET 2.8 per Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkId=699287)

### <a name="net-452-support"></a>Supporto .NET 4.5.2
#### <a name="known-issues"></a>Problemi noti
Azure .NET SDK 2.8 consente si toocreate .NET 4.5.2 pacchetti del servizio Cloud. Tuttavia 4.5.2 di .NET framework non verrà installato predefinito hello rilasciare le immagini del sistema operativo Guest fino a gennaio 2016 del sistema operativo Guest. Prima di tale data, il framework .NET 4.5.2, sarà disponibile tramite una versione di rilascio del sistema operativo Guest separata – novembre 2015-02. Vedere hello [rilasci del sistema operativo Guest Azure e matrice di compatibilità SDK](../cloud-services/cloud-services-guestos-update-matrix.md) tootrack pagina quando l'immagine di hello verrà rilasciato.  Quando viene rilasciato l'immagine di hello novembre 2015-02 è possibile scegliere toouse quell'immagine aggiornando il servizio Cloud (. cscfg) file di configurazione. Nella configurazione del servizio hello file imposta l'attributo osVersion hello della stringa di toohello elemento ServiceConfiguration hello "WA-GUEST-OS-4.26_201511-02". Se si sceglie tooopt nella toouse questa immagine toohello aggiornamenti automatici del sistema operativo Guest non si verificherà. tooget hello aggiornamenti automatici hello osVersion deve essere impostato troppo "*" e .NET 4.5.2 sarà disponibile solo tramite aggiornamenti automatici nel gennaio 2016.

### <a name="azure-data-factory"></a>Data factory di Azure
#### <a name="known-issues"></a>Problemi noti
Durante un **modello di Data Factory** progetto creazione che coinvolgono dati di esempio, script di PowerShell azure potrebbe non riuscire se è installata nel computer di hello versione di azure power shell dopo 0.9.8.

In ordine toosuccessfully creare questo tipo di progetto, è necessario installare [versione di azure power shell 0.9.8](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi).

### <a name="azure-resource-manager-tools"></a>Strumenti di Gestione risorse di Azure
#### <a name="breaking-changes"></a>Modifiche di rilievo
script di PowerShell di Microsoft project gruppo di risorse di Azure hello Hello è stata aggiornata in questa versione toowork i cmdlet di Azure PowerShell nuovo hello versione 1.0.  Questo nuovo script non funzionerà da con Visual Studio quando si utilizza una versione di hello SDK precedenti too2.8.  

Script da progetti creati in versioni precedenti di hello SDK non verrà eseguito all'interno di Visual Studio quando utilizzando hello 2.8 SDK.  Tutti gli script continuerà toowork all'esterno di Visual Studio con la versione appropriata di hello di hello cmdlet di Azure PowerShell.  

Hello 2.8 SDK richiede la versione 1.0 di hello cmdlet di Azure PowerShell.  Tutte le altre versioni di hello SDK richiedono la versione 0.9.8 di hello cmdlet di Azure PowerShell.  Per altre informazioni, vedere [questo](http://go.microsoft.com/fwlink/?LinkID=623011) blog.

### <a name="web-tools-extensions"></a>Estensioni degli strumenti Web
#### <a name="known-issues"></a>Problemi noti
Hello seguenti problemi verrà risolti nelle hello successivo al rilascio.

* Il cloud del Servizio app e i movimenti di Esplora Server per gli ambienti di non produzione (ad esempio Azure Cina o i clienti di Azure Stack) non funzionano. Per pubblicano i clienti in queste aree interessati, il download di hello profilo dal portale di Azure hello abiliterà il possibilità pubblicazione. Una versione futura sarà in grado di ripristinare i movimenti, ad esempio "Collegare il debugger" e "Visualizzare i log di flusso" per Azure Cina e i clienti di Stack. 
* I clienti potrebbero riscontrare errori durante il servizio App è in una regione diversa da Stati Uniti orientali la creazione quando hello App Insights istanza toowhich che si sta distribuendo. In questi scenari, la creazione di un servizio App nel portale di hello e download hello profilo di pubblicazione verrà abilitare scenari di pubblicazione. 

### <a name="azure-hdinsight-tools"></a>Strumenti di Azure HDInsight
#### <a name="new-updates"></a>Nuovi aggiornamenti
* È possibile eseguire una query Hive nel cluster hello tramite HiveServer2 con quasi alcun overhead e verificare il processo di hello effettua l'accesso in tempo reale.
* Nuovo Hive esecuzione visualizzazione attività è possibile esaminare il processo più approfondito, utilizzando hello ulteriori dettagli e identificare i potenziali problemi.

Per altre informazioni, vedere [Azure SDK 2.8 per Visual Studio 2013 e Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/). 

## <a name="azure-sdk-for-net-281"></a>Azure SDK per .NET 2.8.1
### <a name="known-issues-for-visual-studio-2013-and-visual-studio-2015"></a>Problemi noti per Visual Studio 2013 e Visual Studio 2015
1. Trigger di processo Web pubblica tooslots verrà Mostra e errore e non impostare una pianificazione, che effettuerà il push tooAzure processo Web hello. I clienti che hanno bisogno di un processo pianificato hello Azure Portal tooset pianificazione hello quindi è possono utilizzare per hello processo Web. 
2. I clienti di Python potrebbero riscontrare problemi di debugger. Team servizio sta apportando una correzione per questo, ma se i clienti sono interessati, consentono, Microsoft conosce nei forum hello o sul blog di annuncio hello o sezione commenti note sulla versione. 
3. I clienti che si trovano in determinate aree, ad esempio l'India meridionale, riscontreranno errori durante il provisioning del servizio app Questo comportamento è coerente con il portale di hello e i clienti che hanno avuto questo problema possono utilizzare hello toorequest portale Azure accesso toopublish toothese aree geografiche. Una volta che lo richiedono accesso toothese aree utilizzando dovrebbe funzionare hello provisioning del portale Azure. 

## <a name="azure-sdk-for-net-282"></a>Azure SDK per .NET 2.8.2
Dopo l'installazione di hello degli strumenti hello 2.8.2, i clienti potrebbero riscontrare hello seguente problema.         

* Se si usa Windows 10 e non è installato Internet Explorer, è possibile che venga visualizzato l'errore "Impossibile trovare Internet Explorer".
  problema di hello tooresolve, installare Internet Explorer utilizzando hello Aggiungi o Rimuovi finestra di dialogo componenti di Windows.

Se si rileva questo problema, utilizzare una trasmissione-smile hello funzionalità tooreport è.

Per altre informazioni, vedere [questo post](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-2-for-net/) .

## <a name="other-updates"></a>Altri aggiornamenti
Per altri aggiornamenti, vedere [post di annuncio di Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).

## <a name="also-see"></a>Vedere anche
[Post di annuncio di Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)

[Supporto e informazioni sul ritiro per hello Azure SDK per .NET e API](https://msdn.microsoft.com/library/azure/dn479282.aspx)

