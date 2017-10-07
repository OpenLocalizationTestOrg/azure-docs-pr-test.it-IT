---
title: Opzioni - servizi Cloud di calcolo aaaAzure | Documenti Microsoft
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
ms.openlocfilehash: e7f109a54c61cc2f37644d39a61d2d932a374587
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="should-i-choose-cloud-services-or-something-else"></a>Perché scegliere Servizi cloud
Rappresenta la scelta di hello servizi Cloud di Azure per si? In Azure sono disponibili diversi modelli di hosting per l'esecuzione di applicazioni. Ognuno di essi fornisce un set diverso di servizi, pertanto quello che si sceglie dipende esattamente cosa si cerca toodo.

[!INCLUDE [compute-table](../../includes/compute-options-table.md)]

<a name="tellmecs"></a>

## <a name="tell-me-about-cloud-services"></a>Informazioni sui servizi cloud
Servizi cloud è un esempio di [Platform-as-a-Service (PaaS)](https://azure.microsoft.com/overview/what-is-paas/) . Ad esempio [servizio App](../app-service-web/app-service-web-overview.md), questa tecnologia è progettato toosupport applicazioni scalabili e affidabili e toooperate economico. Esattamente come un servizio App è ospitato in macchine virtuali, pertanto sono troppo servizi Cloud, tuttavia, si dispone di maggiore controllo sulla hello macchine virtuali. È possibile installare il software personalizzato nelle macchine virtuali del servizio cloud ed accedervi in remoto.

![cs_diagram](./media/cloud-services-choose-me/diagram.png)

Maggiore controllo significa anche minore semplicità d'uso. A meno che non si necessita di hello controllo ulteriori opzioni, è in genere più rapida e semplice tooget un'applicazione web attivo e in esecuzione nelle App Web nel servizio App confrontati tooCloud servizi.

Sono disponibili due tipi dei servizi cloud. Hello l'unica differenza tra hello due è la modalità in cui è ospitato il ruolo nella macchina virtuale hello.

* **Ruolo Web**  
Distribuisce e ospita automaticamente l'app tramite IIS.

* **Ruolo di lavoro**  
Non usa IIS ed esegue l'app autonomamente.

Ad esempio, un'applicazione semplice può usare un solo ruolo Web che serve un sito Web. Un'applicazione più complessa potrebbe utilizzare un toohandle ruolo web le richieste in arrivo degli utenti, quindi passare tali richieste tooa ruolo di lavoro per l'elaborazione. Per questa comunicazione è possibile che venga usato il [bus di servizio](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md) o il [servizio di accodamento di Azure](../storage/common/storage-introduction.md).

Come hello suggerito nella figura precedente, tutte le macchine virtuali di hello in una singola applicazione eseguita in hello stesso servizio cloud. Un'applicazione hello accesso utenti tramite un singolo indirizzo IP pubblico, con le richieste automaticamente con carico bilanciato tra le macchine virtuali dell'applicazione hello. piattaforma Hello [Ridimensiona e distribuisce](cloud-services-how-to-scale.md) hello macchine virtuali in un'applicazione di servizi Cloud in modo da evitare un singolo punto di errore hardware.

Anche se le applicazioni eseguite in macchine virtuali, è importante toounderstand che i servizi Cloud fornisce PaaS, non IaaS. Ecco un modo toothink su di esso: con IaaS, ad esempio macchine virtuali di Azure, prima creare e configurare l'applicazione viene eseguita nell'ambiente di hello, quindi distribuire l'applicazione in questo ambiente. Si è responsabili della gestione gran parte del mondo, eseguire operazioni quali la distribuzione di nuove versioni con patch del sistema operativo hello in ogni macchina virtuale. Nelle soluzioni PaaS, al contrario, è come se l'ambiente di hello esiste già. Toodo è la distribuzione dell'applicazione. Gestione della piattaforma hello che cui viene eseguita, inclusa la distribuzione di nuove versioni del sistema operativo hello, viene gestita automaticamente.

## <a name="scaling-and-management"></a>Scalabilità e gestione
Se si usa Servizi cloud, non è necessario creare macchine virtuali. In alternativa, è fornire un file di configurazione che indica a Azure quante si desidera, ad esempio **tre istanze dei ruoli web** e **due istanze del ruolo worker**, e piattaforma hello verranno creati automaticamente.  L'utente decide le [dimensioni](cloud-services-sizes-specs.md) delle macchine virtuali di supporto, ma non le crea esplicitamente. Se l'applicazione deve toohandle un carico maggiore, è possibile richiedere più macchine virtuali e Azure crea le istanze. Se diminuisce il carico di hello, è possibile arrestare tali istanze e interrompere il pagamento per tali.

Un'applicazione di servizi Cloud è in genere eseguita toousers disponibile tramite un processo in due fasi. Uno sviluppatore prima [caricamenti hello applicazione](cloud-services-how-to-create-deploy.md) toohello piattaforma di gestione temporanea di area. Quando sono pronto per sviluppatori di hello in tempo reale di un'applicazione hello toomake, utilizzano gestione temporanea di hello tooswap portale Azure con la produzione. Questo [commutatore tra gestione temporanea e produzione](cloud-services-nodejs-stage-application.md) può essere eseguita senza tempi di inattività, che consente di essere aggiornato tooa nuova versione senza alterare i relativi utenti di un'applicazione in esecuzione.

## <a name="monitoring"></a>Monitoraggio
Servizi cloud offre inoltre funzionalità di monitoraggio. Come macchine virtuali di Azure, rileva un errore server fisico e si riavvia le macchine virtuali hello che erano in esecuzione su tale server per una nuova macchina. Servizi cloud consente inoltre di rilevare errori di macchine virtuali e applicazioni, non solo errori hardware. A differenza di macchine virtuali, dispone di un agente all'interno di ogni ruolo web e di lavoro e pertanto è in grado di toostart nuove macchine virtuali e istanze dell'applicazione quando si verificano errori.

Hello PaaS natura dei servizi Cloud presenta altre implicazioni, troppo. Uno dei più importante hello è che le applicazioni create su questa tecnologia devono essere scritto toorun correttamente quando qualsiasi istanza del ruolo web o di lavoro ha esito negativo. Questa operazione, un Cloud di servizi dell'applicazione non deve gestire lo stato in tooachieve hello file system del proprio macchine virtuali. A differenza delle macchine virtuali create con macchine virtuali di Azure, scritture effettuate tooCloud macchine virtuali di servizi non sono permanenti. non c'è niente un disco dati di macchine virtuali. Un servizi Cloud, è necessario in modo esplicito scrivere tooSQL di stato tutti i Database, invece, BLOB, tabelle, o un altro dispositivo di archiviazione esterno. Compilazione di applicazioni in questo modo le rende tooscale più semplice e più resistenti toofailure, entrambi gli obiettivi importanti di servizi Cloud.

## <a name="next-steps"></a>Passaggi successivi
[Creare un'app di servizio cloud in .NET](cloud-services-dotnet-get-started.md)  
[Creare un'app di servizio cloud in Node.js](cloud-services-nodejs-develop-deploy-app.md)  
[Creare un'app di servizio cloud in PHP](../cloud-services-php-create-web-role.md)  
[Creare un'app del servizio cloud in Python](cloud-services-python-ptvs.md)

