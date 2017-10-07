---
title: aaaBest procedure consigliate per il servizio App di Azure
description: Informazioni sulle procedure consigliate e la risoluzione dei problemi per il servizio app di Azure.
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: f3359464-fa44-4f4a-9ea6-7821060e8d0d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: dariagrigoriu
ms.openlocfilehash: a1d3127f5a746aa43f7b56b45f17c45df9087bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-app-service"></a>Procedure consigliate per il servizio app di Azure
Questo articolo riepiloga le procedure consigliate per l'uso del [servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714). 

## <a name="colocation"></a>Condivisione dell'area
Quando la composizione di una soluzione, ad esempio un'app web e un database delle risorse di Azure si trovano in effetti hello aree diverse può includere seguente hello:

* Aumento della latenza nella comunicazione tra le risorse
* Gli addebiti di valuta per i dati in uscita trasferire tra aree come indicato in hello [pagina dei prezzi Azure](https://azure.microsoft.com/pricing/details/data-transfers).

Condivisione percorso in hello stessa area è ottimale per le risorse di Azure la composizione di una soluzione, ad esempio un'app web e utilizzare un account di database o nell'archivio dati o contenuto toohold. Quando la creazione di risorse, assicurarsi che si trovano in hello stessa area di Azure, a meno che non si dispone di business specifici o progetta motivo non toobe. È possibile spostare un toohello di applicazione di servizio App stessa area del database mediante l'utilizzo di hello [servizio App di funzionalità di clonazione](app-service-web-app-cloning-portal.md) attualmente disponibili per il piano di servizio App Premium app.   

## <a name="memoryresources"></a>Quando le app usano più memoria del previsto
Quando si nota un'app Usa più memoria del previsto, come indicato tramite il monitoraggio o indicazioni servizio considerare hello [funzionalità di riparazione automatica di servizio App](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites). Una delle opzioni di hello per funzionalità di riparazione automatica hello richiede azioni personalizzate in base a una soglia di memoria. Azioni span spettro hello da tooinvestigation di notifiche di posta elettronica tramite attenuazione tooon posto dump di memoria per il riciclo del processo di lavoro hello. La riparazione automatica può essere configurata tramite il Web. config e tramite un'interfaccia utente intuitiva descritta in questo post di blog hello [estensione del sito di supporto del servizio App](https://azure.microsoft.com/blog/additional-updates-to-support-site-extension-for-azure-app-service-web-apps).   

## <a name="CPUresources"></a>Quando le app usano più CPU del previsto
Quando si nota che una app consuma maggiore utilizzo della CPU previsto o esperienze ripetuto picchi di CPU come indicato tramite il monitoraggio o consigli a scalabilità o la scalabilità hello piano di servizio App. Se l'applicazione viene trovato, la scalabilità verticale è hello unica opzione disponibile, mentre se l'applicazione è senza stato e scalabilità out fornirà maggiore flessibilità e maggiore rischio di scala. 

Per altre informazioni sulle differenze tra le applicazioni "con stato" e quelle "senza stato", guardare il video relativo alla [pianificazione di un'applicazione multilivello end-to-end scalabile nel servizio app Web di Microsoft Azure](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/DEV-B414#fbid=?hashlink=fbid). Per altre informazioni sulla scalabilità del servizio app e sulle opzioni di scalabilità automatica, vedere [Scalare un'app Web nel servizio app di Azure](web-sites-scale.md).  

## <a name="socketresources"></a>Quando si esauriscono le risorse socket
Un motivo comune per esaurire le connessioni TCP in uscita è hello utilizzo delle librerie client che non sono le connessioni TCP tooreuse implementato o nel caso di hello di un protocollo di livello superiore, ad esempio HTTP - Keep-Alive non vengono utilizzati. Consultare la documentazione di hello per ognuna delle librerie di hello App hello in tooensure il piano di servizio App sono configurati o accessibili nel codice per un efficiente riutilizzo delle connessioni in uscita a cui fa riferimento. Seguire anche hello libreria documentazione indicazioni sulla creazione e rilascio o una pulizia tooavoid perdita di connessioni. Anche se queste ricerche di librerie client sono in impatto lo stato di avanzamento può essere mitigata da scalabilità toomultiple istanze.  

## <a name="appbackup"></a>Quando il backup dell'applicazione non viene più eseguito
Hello due cause più comuni sono errore del backup app: configurazione di database non valido e le impostazioni di archiviazione non valido. In genere questi errori si verificano quando sono presenti modifiche toostorage o le risorse del database o le modifiche come tooaccess queste risorse (ad esempio, le credenziali aggiornate per hello database selezionato nelle impostazioni di backup hello). I backup in genere eseguita in una pianificazione e richiedono l'accesso toostorage (per l'output del backup dei file hello) e i database (per la copia e la lettura di contenuto toobe inclusi nel backup hello). risultato dell'esito negativo di una di queste risorse sarebbe tooaccess Hello errore backup coerente. 

Quando si verificano errori di backup, verificare il tipo di errore è il problema più recente toounderstand di risultati. Nel caso di hello di errori di accesso di archiviazione, esaminare e aggiornare le impostazioni di archiviazione hello utilizzate nella configurazione del backup hello. Nel caso di hello di errori di accesso ai database, esaminare e aggiornare le stringhe di connessione come parte delle impostazioni di applicazione; procedere quindi tooupdate tooproperly la configurazione del backup includono database hello necessario. Per ulteriori informazioni sul backup di app, vedere hello [eseguire il backup di un'app web in Azure App Service](web-sites-backup.md) documentazione.

## <a name="nodejs"></a>Quando nuove app Node.js sono distribuiti tooAzure servizio App
Configurazione predefinita di servizio App Azure per le app Node.js è previsto toobest seme hello esigenze delle applicazioni più comuni. Se configurazione per l'app Node.js consente di trarre vantaggio dalle prestazioni di tooimprove ottimizzazione personalizzate o di ottimizzare l'utilizzo di risorse per le risorse di memoria/CPU/rete, è possibile esaminare il procedure consigliate e i passaggi di risoluzione dei problemi. Questo articolo di documentazione descrive le impostazioni di iisnode hello potrebbe essere necessario tooconfigure per app Node.js descrive hello vari scenari o problemi che potrebbe essere esposti l'app e Mostra come tooaddress questi problemi: [procedure consigliate e Guida alla risoluzione dei problemi per le applicazioni di nodo in Azure App Service](app-service-web-nodejs-best-practices-and-troubleshoot-guide.md).   

