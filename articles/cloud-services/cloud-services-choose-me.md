---
title: Opzioni di calcolo di Azure - Servizi cloud | Documentazione Microsoft
description: 'Informazioni sulle opzioni di hosting di calcolo di Azure e sul relativo funzionamento: Servizio app, Servizi cloud e Macchine virtuali'
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
ms.assetid: ed7ad348-6018-41bb-a27d-523accd90305
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: e8053b74e0e4d721523f49bcbb9e33b08bb7a1dc
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="should-i-choose-cloud-services-or-something-else"></a>Perché scegliere Servizi cloud
Servizi cloud di Azure è la scelta giusta? In Azure sono disponibili diversi modelli di hosting per l'esecuzione di applicazioni. Ognuno fornisce un diverso set di servizi, pertanto quello da scegliere dipende dalle attività che si tenta di eseguire.

[!INCLUDE [compute-table](../../includes/compute-options-table.md)]

<a name="tellmecs"></a>

## <a name="tell-me-about-cloud-services"></a>Informazioni sui servizi cloud
Servizi cloud è un esempio di [Platform-as-a-Service (PaaS)](https://azure.microsoft.com/overview/what-is-paas/) . Analogamente al [servizio app](../app-service/app-service-web-overview.md), questa tecnologia è stata progettata per supportare applicazioni scalabili, attendibili ed economicamente efficienti. Proprio come un servizio app, i servizi cloud sono ospitati su VM, tuttavia il controllo sulle VM è maggiore. È possibile installare il software personalizzato nelle macchine virtuali del servizio cloud ed accedervi in remoto.

![cs_diagram](./media/cloud-services-choose-me/diagram.png)

Maggiore controllo significa anche minore semplicità d'uso. Pertanto, se non sono necessarie opzioni di controllo aggiuntive, in genere è più semplice e rapido creare ed eseguire un'applicazione Web in App Web in servizio app che non in Servizi cloud.

Sono disponibili due tipi dei servizi cloud. L'unica differenza tra i due è il modo in cui il ruolo è ospitato nella macchina virtuale.

* **Ruolo Web**  
Distribuisce e ospita automaticamente l'app tramite IIS.

* **Ruolo di lavoro**  
Non usa IIS ed esegue l'app autonomamente.

Ad esempio, un'applicazione semplice può usare un solo ruolo Web che serve un sito Web. Un'applicazione più complessa può usare un ruolo Web per la gestione delle richieste in arrivo dagli utenti, quindi passare tali richieste a un ruolo di lavoro per l'elaborazione. Per questa comunicazione è possibile che venga usato il [bus di servizio](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md) o il [servizio di accodamento di Azure](../storage/common/storage-introduction.md).

Come illustrato nella figura precedente, tutte le VM in una singola applicazione vengono eseguite nello stesso servizio cloud. Gli utenti accedono all'applicazione attraverso un indirizzo IP pubblico che esegue automaticamente il bilanciamento del carico delle richieste nelle VM dell'applicazione. La piattaforma [scala e distribuisce](cloud-services-how-to-scale.md) le VM in un'applicazione di Servizi cloud, in modo da evitare un singolo punto di errore hardware.

Anche se le applicazioni sono eseguite nelle macchine virtuali, è importante capire che Servizi cloud fornisce PaaS, non IaaS. La spiegazione seguente aiuta a comprendere meglio il concetto: una tecnologia IaaS, quale Macchine virtuali di Azure, consente di creare e configurare prima di tutto l'ambiente in cui l'applicazione viene eseguita, quindi di distribuire l'applicazione in tale ambiente. L'utente ha la responsabilità di gestire questo ambiente, ad esempio distribuendo nuove versioni con patch del sistema operativo in ogni macchina virtuale. La tecnologia PaaS, invece, consente di procedere come se l'ambiente esistesse già. È sufficiente è distribuire l'applicazione. La gestione della piattaforma in cui viene eseguita l'applicazione, inclusa la distribuzione di nuove versioni del sistema operativo, non è a carico dell'utente.

## <a name="scaling-and-management"></a>Scalabilità e gestione
Se si usa Servizi cloud, non è necessario creare macchine virtuali. Fornire invece un file di configurazione che specifica ad Azure quante macchine virtuali di ogni tipo sono richieste, ad esempio **tre istanze del ruolo Web** e **due istanze del ruolo di lavoro**. Le macchine virtuali vengono poi create automaticamente dalla piattaforma.  L'utente decide le [dimensioni](cloud-services-sizes-specs.md) delle macchine virtuali di supporto, ma non le crea esplicitamente. Se l'applicazione deve gestire un carico maggiore, è possibile richiedere VM aggiuntive e tali istanze verranno create automaticamente da Azure. Se il carico diminuisce, è possibile chiudere tali istanze e interromperne il pagamento.

Un'applicazione di Servizi cloud viene in genere resa disponibile agli utenti mediante un processo in due fasi. Prima di tutto lo sviluppatore [carica l'applicazione](cloud-services-how-to-create-deploy.md) nell'area di gestione temporanea della piattaforma. Quando lo sviluppatore è pronto per l'attivazione dell'applicazione, usa il portale per il passaggio in produzione. Il [passaggio dalla gestione temporanea alla produzione](cloud-services-nodejs-stage-application.md) può essere eseguito senza tempi di inattività, consentendo l'aggiornamento di un'applicazione in esecuzione a una nuova versione senza interferire con l'uso da parte degli utenti.

## <a name="monitoring"></a>Monitoraggio
Servizi cloud offre inoltre funzionalità di monitoraggio. Analogamente a Macchine virtuali di Azure, rileva un server fisico in errore e riavvia le VM in esecuzione su tale server in una nuova macchina. Servizi cloud consente inoltre di rilevare errori di macchine virtuali e applicazioni, non solo errori hardware. A differenza di Macchine virtuali, dispone di un agente in ogni ruolo Web e di lavoro ed è quindi in grado di avviare nuove macchine virtuali e istanze di applicazione in caso di errori.

L'utilizzo della tecnologia PaaS da parte di Servizi cloud comporta anche altre implicazioni, ad esempio il fatto che le applicazioni basate su tale tecnologia devono essere scritte in modo da essere eseguite correttamente in caso di errore di istanze dei ruoli Web o di lavoro. A tale scopo, è necessario che lo stato di un'applicazione di Servizi cloud non venga salvato nel file system delle rispettive macchine virtuali. A differenza delle VM create tramite Macchine virtuali di Azure, le operazioni di scrittura effettuate nelle VM di Servizi cloud non sono persistenti. La persistenza è offerta solo dai dischi dati di Macchine virtuali. È pertanto necessario che tutti gli stati di un'applicazione di Servizi cloud vengano scritti esplicitamente in database SQL, BLOB, tabelle o altre tecnologie di archiviazione esterna. Le applicazioni create in questo modo risulteranno più scalabili e più resistenti agli errori, obiettivi essenziali di Servizi cloud.

## <a name="next-steps"></a>Passaggi successivi
[Creare un'app di servizio cloud in .NET](cloud-services-dotnet-get-started.md)  
[Creare un'app di servizio cloud in Node.js](cloud-services-nodejs-develop-deploy-app.md)  
[Creare un'app di servizio cloud in PHP](../cloud-services-php-create-web-role.md)  
[Creare un'app del servizio cloud in Python](cloud-services-python-ptvs.md)

