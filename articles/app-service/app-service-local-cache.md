---
title: Cenni preliminari sulla Cache locale del servizio App aaaAzure | Documenti Microsoft
description: "In questo articolo viene descritto come tooenable, ridimensionamento e query hello stato hello Azure App Service locale della funzionalità di Cache"
services: app-service
documentationcenter: app-service
author: SyntaxC4
manager: yochayk
editor: 
tags: optional
keywords: 
ms.assetid: e34d405e-c5d4-46ad-9b26-2a1eda86ce80
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/04/2016
ms.author: cfowler
ms.openlocfilehash: 220331ac7e15352a434d63266701071024d868c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-local-cache-overview"></a>Panoramica della cache locale del servizio app di Azure
Il contenuto delle app Web di Azure viene memorizzato nell'archiviazione di Azure e presentato in modo permanente come condivisione del contenuto. Questa progettazione è toowork prevista con un'ampia gamma di applicazioni e ha hello gli attributi seguenti:  

* il contenuto di Hello è condiviso tra più istanze di macchina virtuale (VM) di app web hello.
* contenuto di Hello è durevole e può essere modificato da app web in esecuzione.
* File di log e file di dati di diagnostica sono disponibili in hello stesso condivisa cartella del contenuto.
* Pubblicazione di nuovi contenuti direttamente aggiornamenti hello cartella del contenuto. È possibile immediatamente hello Visualizza contenuto dal sito Web di Gestione controllo servizi hello e hello app web in esecuzione (in genere alcune tecnologie, ad esempio ASP.NET riavviare web app in alcune modifiche tooget hello più recente contenuto del file).

Mentre molte app Web usano una o tutte queste funzionalità, alcune richiedono solo un archivio del contenuto di sola lettura ad alte prestazioni da cui possono essere eseguite con disponibilità elevata. Queste applicazioni possono trarre vantaggio da un'istanza di VM di una cache locale specifica.

funzionalità di Cache locale di Azure App Service Hello fornisce una visualizzazione di ruolo web del contenuto. Il contenuto è costituito da una cache di scrittura con rimozione del contenuto di archiviazione creata in modo asincrono all'avvio del sito. Quando la cache di hello è pronta, il sito di hello è disattivati toorun del contenuto memorizzato nella cache di hello. App Web eseguite nella Cache locale sono hello seguenti vantaggi:

* E sono soggetti agli toolatencies che si verificano durante l'accesso a contenuto nell'archiviazione di Azure.
* Sono gli aggiornamenti toohello immune pianificato o tempi di inattività non pianificati e altre interruzioni di soluzioni di archiviazione di Azure che si verificano nel server che servono condivisione contenuto hello.
* Hanno meno riavvii di app a causa di modifiche condivisione toostorage.

## <a name="how-local-cache-changes-hello-behavior-of-app-service"></a>Come Cache locale viene modificato il comportamento di hello del servizio App
* cache di Hello locale è una copia di cartelle di /site e /siteextensions hello dell'app web hello. Viene creato nell'istanza di macchina virtuale locale di hello all'avvio dell'app web. Hello dimensione della cache locale di hello per app web è limitata too300 MB per impostazione predefinita, ma è possibile aumentarlo too2 GB.
* cache locale Hello è lettura / scrittura. Tuttavia, tutte le modifiche verranno annullate quando app web hello sposta le macchine virtuali o ottiene riavviato. Non utilizzare la Cache locale per le applicazioni che archiviano i dati di importanza critica nell'archivio contenuto hello.
* Le applicazioni Web possono continuare toowrite i file di log e dati di diagnostica come avviene attualmente. File di log e dati, tuttavia, archiviati localmente nel hello macchina virtuale. Quindi vengono copiati periodicamente toohello archivio dei contenuti condivisi. archivio dei contenuti condivisi toohello copia Hello è un lavoro migliore - esegue il backup di scrittura potrebbe andare perso a causa di tooa improvviso arresto anomalo del sistema di un'istanza di macchina virtuale.
* Viene apportata una modifica nella struttura di cartelle hello hello LogFiles e le cartelle di dati per le applicazioni web che usano la Cache locale. Esistono le sottocartelle in hello LogFiles e i dati delle cartelle di archiviazione che seguono hello modello di denominazione di "identificatore" + timestamp. Ciascuna delle sottocartelle hello corrisponde tooa istanza della macchina virtuale in cui l'app web hello è in esecuzione o è stata eseguita.  
* Pubblicazione delle modifiche toohello web app tramite uno dei meccanismi di pubblicazione hello pubblicherà toohello archivio dei contenuti condivisi. Infatti, in base alla progettazione vogliamo hello pubblicati contenuto toobe durevole. toorefresh hello cache locale dell'app web hello deve toobe riavviato. Ciò sembra come un passaggio di un numero eccessivo? ciclo di vita hello toomake trasparente, vedere le informazioni di hello più avanti in questo articolo.
* D:\home. punterà toohello cache locale. D:\Local continuerà verso toohello temporaneo VM specifico di archiviazione.
* visualizzazione di contenuto predefinito Hello del sito SCM hello continuerà toobe che di hello archivio del contenuto condiviso.

## <a name="enable-local-cache-in-app-service"></a>Abilitare la cache locale nel servizio app
La cache locale viene configurata mediante una combinazione di impostazioni delle app riservate. È possibile configurare queste impostazioni delle app usando hello dei seguenti metodi:

* [Portale di Azure](#Configure-Local-Cache-Portal)
* [Gestione risorse di Azure](#Configure-Local-Cache-ARM)

### <a name="configure-local-cache-by-using-hello-azure-portal"></a>Configurare la Cache locale tramite hello portale di Azure
<a name="Configure-Local-Cache-Portal"></a>

La cache locale viene abilitata per ogni app Web con questa impostazione dell'app: `WEBSITE_LOCAL_CACHE_OPTION` = `Always`  

![Impostazioni delle app nel portale di Azure: cache locale](media/app-service-local-cache/app-service-local-cache-configure-portal.png)

### <a name="configure-local-cache-by-using-azure-resource-manager"></a>Configurare la cache locale tramite Azure Resource Manager
<a name="Configure-Local-Cache-ARM"></a>

```

...

{
    "apiVersion": "2015-08-01",
    "type": "config",
    "name": "appsettings",
    "dependsOn": [
        "[resourceId('Microsoft.Web/sites/', variables('siteName'))]"
    ],

"properties": {
        "WEBSITE_LOCAL_CACHE_OPTION": "Always",
        "WEBSITE_LOCAL_CACHE_SIZEINMB": "300"
    }
}

...
```

## <a name="change-hello-size-setting-in-local-cache"></a>Modificare l'impostazione relativa alla dimensione hello nella Cache locale
Per impostazione predefinita, la dimensione della cache locale di hello è **300 MB**. Ciò include /site hello e /siteextensions cartelle che vengono copiate dal hello contenuto archivio, nonché le cartelle di dati e log creata in locale. tooincrease questo limite, usare l'impostazione dell'app hello `WEBSITE_LOCAL_CACHE_SIZEINMB`. È possibile aumentare la dimensione hello troppo alto**2 GB** (2000 MB) per ciascuna applicazione web.

## <a name="best-practices-for-using-app-service-local-cache"></a>Procedure consigliate per l'uso della cache locale del servizio app
È consigliabile utilizzare la Cache locale in combinazione con hello [gli ambienti di Staging](../app-service-web/web-sites-staged-publishing.md) funzionalità.

* Aggiungere hello *sticky* impostazione app `WEBSITE_LOCAL_CACHE_OPTION` con valore hello `Always` tooyour **produzione** slot. Se si utilizza `WEBSITE_LOCAL_CACHE_SIZEINMB`, aggiungerlo come slot di produzione tooyour impostazione permanenti.
* Creare un **gestione temporanea** slot e pubblicare tooyour slot di gestione temporanea. È in genere non impostare hello slot toouse Cache locale tooenable un semplice ciclo di vita di compilazione-distribuzione-test per la gestione temporanea se si ottengono i vantaggi di hello della Cache locale per lo slot di produzione hello di gestione temporanea.
* Testare il sito nello slot di gestione temporanea.  
* Al termine, eseguire un' [operazione di scambio](../app-service-web/web-sites-staged-publishing.md#Swap) tra lo slot di gestione temporanea e lo slot di produzione.  
* Le impostazioni permanenti includono nome e lo slot tooa permanenti. Pertanto quando lo slot di gestione temporanea hello Ottiene scambiato nell'ambiente di produzione, erediterà le impostazioni dell'app di hello Cache locale. Hello appena scambiato slot verranno eseguite sul cache locale hello dopo alcuni minuti e verrà riscaldato come parte di riscaldamento slot dopo lo scambio di produzione. Pertanto, una volta completato lo scambio di slot hello, slot di produzione verrà eseguito sulla cache locale hello.

## <a name="frequently-asked-questions-faq"></a>Domande frequenti
### <a name="how-can-i-tell-if-local-cache-applies-toomy-web-app"></a>Come stabilire se la Cache locale si applica toomy web app
Se l'app web è necessario un archivio contenuti a prestazioni elevate, affidabile, non utilizza dati critici di hello archivio contenuti toowrite in fase di esecuzione ed è inferiore a 2 GB in totale dimensioni, risposte hello sono "yes"! dimensioni totali hello di tooget delle cartelle /site e /siteextensions, è possibile utilizzare l'estensione del sito hello "Utilizzo di disco App Web di Azure".  

### <a name="how-can-i-tell-if-my-site-has-switched-toousing-local-cache"></a>Come stabilire se il sito è stata attivata la toousing Cache locale
Se si utilizza funzionalità della Cache locale hello con gli ambienti di Staging, operazione di scambio hello non verrà completata fino a quando non è riscaldata Cache locale. toocheck se il sito è in esecuzione sulla Cache locale, è possibile controllare variabile di ambiente del processo worker hello `WEBSITE_LOCALCACHE_READY`. Utilizzare le istruzioni di hello in hello [variabile di ambiente del processo di lavoro](https://github.com/projectkudu/kudu/wiki/Process-Threads-list-and-minidump-gcdump-diagsession#process-environment-variable) tooaccess pagina hello variabile di ambiente di processo di lavoro su più istanze.  

### <a name="i-just-published-new-changes-but-my-web-app-does-not-seem-toohave-them-why"></a>Dopo la pubblicazione solo le nuove modifiche, ma l'applicazione web non sembra toohave li. Perché?
Se l'app web Usa la Cache locale, è necessario toorestart le ultime modifiche hello tooget del sito. Evitare di dover sito di produzione tooa toopublish le modifiche? Vedere le opzioni di slot hello hello precedente best practices della sezione.

### <a name="where-are-my-logs"></a>Dove si trovano i log?
Se si usa la cache locale, i log e le cartelle di dati hanno un aspetto leggermente diverso. Tuttavia, hello struttura del rimane sottocartelle hello stesso, ad eccezione del fatto che le sottocartelle hello sono annidate in una sottocartella con hello di formato "identificatore univoco della VM" + timestamp.

### <a name="i-have-local-cache-enabled-but-my-web-app-still-gets-restarted-why-is-that-i-thought-local-cache-helped-with-frequent-app-restarts"></a>È stata abilitata la cache locale ma l'app Web viene ancora riavviata. Perché? Pensavo che la cache locale fosse utile in caso di riavvii frequenti dell'app.
La cache locale consente di evitare i riavvii dell'app Web correlati all'archiviazione. Tuttavia, l'app web potrebbe ancora essere sottoposto a riavvii durante l'aggiornamento pianificato dell'infrastruttura di hello VM. Hello complessivo riavvii di app che si verificano con la Cache locale abilitata devono essere un numero inferiore.

### <a name="does-local-cache-exclude-any-directories-from-being-copied-toohello-faster-local-drive"></a>Cache locale escludere alcuna directory vengano copiati toohello unità più velocemente locale?
Come parte del passaggio hello che copia il contenuto di archiviazione hello qualsiasi cartella denominata archivio verrà esclusi. In questo modo negli scenari in cui il contenuto del sito può contenere un repository di controllo di origine che non può essere necessari nell'operazione tooday giorno dell'app web hello. 
