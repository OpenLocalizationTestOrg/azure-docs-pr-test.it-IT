---
title: prestazioni hello aaaTesting di un servizio cloud | Documenti Microsoft
description: Test delle prestazioni di hello di un servizio cloud usando il profiler di Visual Studio hello
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7a5501aa-f92c-457c-af9b-92ea50914e24
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 98bd775e6ffcf948e737c5ec26399c81f4770fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service"></a>Test delle prestazioni di hello di un servizio cloud
## <a name="overview"></a>Panoramica
È possibile testare le prestazioni di hello di un servizio cloud in hello seguenti modi:

* Utilizzare diagnostica Azure toocollect informazioni richieste e le connessioni e le statistiche del sito tooreview che mostrano come servizio hello esegue dalla prospettiva del cliente. tooget introduzione, vedere [configurazione della diagnostica per servizi Cloud di Azure e macchine virtuali](http://go.microsoft.com/fwlink/p/?LinkId=623009).
* Utilizzare hello Visual Studio profiler tooget un'analisi approfondita degli aspetti computazionali di hello della modalità di esecuzione del servizio hello. Come descritto in questo argomento, è possibile utilizzare prestazioni toomeasure di hello profiler durante l'esecuzione di un servizio in Azure. Per informazioni su come toouse hello profiler toomeasure prestazioni di un servizio viene eseguito localmente in un emulatore di calcolo, vedere [hello test delle prestazioni di locale a un servizio Cloud Azure in hello emulatore di calcolo tramite hello Profiler di Visual Studio ](http://go.microsoft.com/fwlink/p/?LinkId=262845).

## <a name="choosing-a-performance-testing-method"></a>Scelta di un metodo di test delle prestazioni
### <a name="use-azure-diagnostics-toocollect"></a>Utilizzare toocollect diagnostica Azure:
* Statistiche su pagine Web o servizi, ad esempio richieste e connessioni.
* Statistiche sui ruoli, come la frequenza con cui un ruolo viene riavviato.
* Generale vengono fornite informazioni sull'utilizzo della memoria, ad esempio percentuale hello tempo hello garbage collector non accetta o hello memoria di un ruolo in esecuzione.

### <a name="use-hello-visual-studio-profiler-to"></a>Utilizzare il profiler di Visual Studio hello per:
* Determinare le funzioni che richiedono hello la maggior parte di tempo.
* Misurare la quantità di tempo richiesta da ogni parte di un programma di calcolo intensivo.
* Confrontare rapporti dettagliati delle prestazioni per due versioni di un servizio.
* Analizzare l'allocazione di memoria in modo più dettagliato rispetto a livello di hello delle allocazioni di memoria singoli.
* Analizzare i problemi di concorrenza nel codice multithreading.

Quando si usa il profiler di hello, è possibile raccogliere dati quando un servizio cloud viene eseguito localmente o in Azure.

### <a name="collect-profiling-data-locally-to"></a>Raccogliere localmente dati della profilatura per:
* Test delle prestazioni di hello di una parte di un servizio cloud, quali l'esecuzione di hello del ruolo di lavoro specifico, che non richiede un carico simulato realistico.
* Test delle prestazioni di hello di un servizio cloud in isolamento, in condizioni controllate.
* Testare le prestazioni di hello di un servizio cloud prima di distribuirlo tooAzure.
* Test delle prestazioni di hello di un servizio cloud privatamente, senza disturbare le distribuzioni esistenti di hello.
* Test delle prestazioni di hello del servizio hello senza incorrere in spese per l'esecuzione in Azure.

### <a name="collect-profiling-data-in-azure-to"></a>Raccogliere dati della profilatura in Azure per:
* Test delle prestazioni di hello di un servizio cloud in un carico simulato o reale.
* Utilizzare il metodo di strumentazione hello raccogliere dati di profilatura, come in questo argomento viene descritto più avanti.
* Test delle prestazioni di hello del servizio hello in hello dello stesso ambiente di esecuzione del servizio hello nell'ambiente di produzione.

È in genere simulare un servizi cloud tootest carico normale o condizioni di carico.

## <a name="profiling-a-cloud-service-in-azure"></a>Profilatura di un servizio cloud in Azure
Quando si pubblica un servizio cloud da Visual Studio, è possibile hello servizio profili e specificare le impostazioni di profilatura che consentono che Hello informazioni che si desidera hello. Viene avviata una sessione di profilatura per ogni istanza di un ruolo. Per ulteriori informazioni su come toopublish del servizio da Visual Studio, vedere [pubblicazione servizio Cloud di Azure da Visual Studio tooan](https://msdn.microsoft.com/library/azure/ee460772.aspx).

toounderstand più sulla profilatura delle prestazioni in Visual Studio, vedere [tooPerformance Guida per principianti profilatura](https://msdn.microsoft.com/library/azure/ms182372.aspx) e [l'analisi delle prestazioni dell'applicazione tramite gli strumenti di profilatura](https://msdn.microsoft.com/library/azure/z9z62c29.aspx).

> [!NOTE]
> Quando si pubblica il servizio cloud è possibile abilitare o IntelliTrace o la profilatura. Non è possibile abilitare entrambi.
> 
> 

### <a name="profiler-collection-methods"></a>Metodi di raccolta del profiler
È possibile usare metodi di raccolta diversi per la profilatura, in base ai problemi delle prestazioni:

* **Campionamento CPU** : questo metodo consente di raccogliere statistiche dell'applicazione utili per l'analisi iniziale dei problemi relativi all'utilizzo della CPU. Campionamento CPU è hello metodo consigliato per la maggior parte delle analisi delle prestazioni di avvio. È un impatto significativo in un'applicazione hello che si esegue la profilatura quando si raccolgono dati di campionamento CPU.
* **Strumentazione** : questo metodo consente di raccogliere dati dettagliati sui tempi utili per l'analisi mirata e per l'analisi dei problemi relativi alle prestazioni di input/output. metodo di strumentazione Hello registra ogni voce, uscita e chiamata di funzione delle funzioni hello in un modulo durante un'esecuzione della profilatura. Questo metodo è utile per raccogliere le informazioni di intervallo dettagliati su una sezione del codice e per comprendere l'impatto di hello delle operazioni di input e outpue sulle prestazioni dell'applicazione. Questo metodo è disabilitato per un computer che esegue un sistema operativo a 32 bit. Questa opzione è disponibile solo quando si esegue il servizio di cloud hello in Azure, non in locale nell'emulatore di calcolo hello.
* **Allocazione di memoria .NET** -questo metodo raccoglie dati sull'allocazione di memoria .NET Framework tramite il campionamento hello metodo di profilatura. Hello i dati raccolti includono il numero di hello e le dimensioni degli oggetti allocati.
* **Concorrenza** : questo metodo raccoglie dati sui conflitti delle risorse e dati di esecuzione dei thread e dei processi utili per l'analisi delle applicazioni multithread e multiprocesso. metodo di concorrenza Hello raccoglie i dati per ogni evento che blocca l'esecuzione del codice, ad esempio quando un thread attende bloccato risorse dell'applicazione di accesso tooan toobe liberate. Questo metodo è utile per l'analisi di applicazioni multithread.
* È inoltre possibile abilitare **profilatura interazione tra livelli**, che fornisce informazioni aggiuntive sui tempi di esecuzione hello di ADO.NET sincrone chiama nelle funzioni di applicazioni multilivello che comunicano con uno o più database. È possibile raccogliere dati di interazione tra livelli con uno qualsiasi dei metodi di profilatura hello. Per altre informazioni sulla profilatura dell'interazione tra livelli, vedere [Visualizzazione Interazioni tra livelli](https://msdn.microsoft.com/library/azure/dd557764.aspx).

## <a name="configuring-profiling-settings"></a>Configurazione delle impostazioni di profilatura
Hello seguente figura viene illustrato come tooconfigure le impostazioni di profilatura dalla finestra di dialogo Pubblica l'applicazione Azure hello.

![Configurare le impostazioni di profilatura](./media/vs-azure-tools-performance-profiling-cloud-services/IC526984.png)

> [!NOTE]
> hello tooenable **Abilita profilatura** casella di controllo, è necessario disporre del profiler hello installato nel computer locale di hello che si utilizza toopublish il servizio cloud. Per impostazione predefinita, il profiler di hello viene installato quando si installa Visual Studio.
> 
> 

### <a name="tooconfigure-profiling-settings"></a>tooconfigure impostazioni profiling
1. In Esplora soluzioni, aprire il menu di scelta rapida hello per il progetto Azure e quindi scegliere **pubblica**. Per informazioni dettagliate su come toopublish un servizio cloud, vedere [la pubblicazione di un cloud servizio utilizzando gli strumenti di Azure di hello](http://go.microsoft.com/fwlink/p?LinkId=623012).
2. In hello **pubblica l'applicazione Azure** la finestra di dialogo, scegliere hello **impostazioni avanzate** scheda.
3. la profilatura, tooenable selezionare hello **Abilita profilatura** casella di controllo.
4. tooconfigure le impostazioni di profilatura, scegliere hello **impostazioni** collegamento ipertestuale. verrà visualizzata la finestra di dialogo Impostazioni profilatura di Hello.
5. Da hello **quale metodo di profilatura si sarebbe ad esempio toouse** pulsanti di opzione, scegliere il tipo di hello di profilatura che è necessario.
6. Seleziona hello, i dati di profilatura dell'interazione tra livelli di toocollect hello **Abilita profilatura interazione tra livelli** casella di controllo.
7. impostazioni di hello toosave, scegliere hello **OK** pulsante.
   
    Quando si pubblica l'applicazione, queste impostazioni sono utilizzati toocreate hello sessione per ogni ruolo di profilatura.

## <a name="viewing-profiling-reports"></a>Visualizzare i rapporti sulla profilatura
Viene creata una sessione di profilatura per ogni istanza di un ruolo nel servizio cloud. profilatura segnala tooview di ogni sessione da Visual Studio, è possibile visualizzare una finestra di Esplora Server hello e quindi scegliere un'istanza di un ruolo tooselect nodo di calcolo di Azure hello. È quindi possibile visualizzare i rapporti di profilatura come mostrato nella seguente figura hello hello.

![Visualizzare il rapporto della profilatura da Azure](./media/vs-azure-tools-performance-profiling-cloud-services/IC748914.png)

### <a name="tooview-profiling-reports"></a>tooview rapporti di profilatura
1. tooview hello finestra Esplora Server in Visual Studio, in scegliere hello barra menu Visualizza, Esplora Server.
2. Scegliere il nodo di calcolo di Azure hello e quindi scegliere il nodo di distribuzione di Azure hello per il servizio cloud hello selezionato tooprofile durante la pubblicazione da Visual Studio.
3. profilatura tooview segnala per un'istanza, scegliere il ruolo di hello nel servizio di hello, menu di scelta rapida hello aprire un'istanza specifica, quindi **Visualizza rapporto sulla profilatura**.
   
    Hello rapporto, un file con estensione vsp, è ora scaricato da Azure, e viene visualizzato lo stato di hello del download hello in hello Log attività di Azure. Al termine del download di hello, hello dei rapporti di profilatura viene visualizzato in una scheda nell'editor di hello per Visual Studio denominato <Role name>  *<Instance Number>*  <identifier>con estensione vsp. Dati di riepilogo per i report di hello viene visualizzato.
4. toodisplay diverse visualizzazioni dei report di hello, nell'elenco Vista corrente hello, scegliere il tipo di hello di visualizzazione che si desidera. Per altre informazioni, vedere [Visualizzazioni dei rapporti degli strumenti di profilatura](https://msdn.microsoft.com/library/azure/bb385755.aspx).

## <a name="next-steps"></a>Passaggi successivi
[Debug di servizi cloud](https://msdn.microsoft.com/library/azure/ee405479.aspx)

[Tooan pubblicazione servizio Cloud di Azure da Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx)

