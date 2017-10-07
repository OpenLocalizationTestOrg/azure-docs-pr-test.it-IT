---
title: aaaProvision nuovi tenant in un'applicazione multi-tenant che utilizza Database SQL di Azure | Documenti Microsoft
description: Informazioni su come tooprovision e nuovo catalogo i tenant nell'hello app SaaS Wingtip
keywords: esercitazione database SQL
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: sstein
ms.openlocfilehash: eb26f523305650c2124e36707d187dfcdad06fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="provision-new-tenants-and-register-them-in-hello-catalog"></a>Eseguire il provisioning di nuovi tenant e registrarli nel catalogo di hello

In questa esercitazione, conoscere il provisioning di hello e modelli SaaS catalogo e come vengono implementati in applicazione SaaS Wingtip hello. Creare e inizializzare nuovi database tenant e registrarli nel catalogo di tenant dell'applicazione hello. catalogo Hello è un database che gestisce il mapping di hello tra molti tenant dell'applicazione SaaS hello e i relativi dati. catalogo Hello svolge un ruolo importante indirizzare il database corretto toohello le richieste dell'applicazione.  

In questa esercitazione si apprenderà come:

> [!div class="checklist"]

> * Eseguire il provisioning di un nuovo tenant singolo, con i passaggi dettagliati della relativa implementazione
> * Effettuare il provisioning di un batch di altri tenant


toocomplete completamento di questa esercitazione, assicurarsi che i hello seguenti prerequisiti:

* app SaaS Wingtip Hello viene distribuita. toodeploy in meno di cinque minuti, vedere [Distribuisci ed esplorare l'applicazione SaaS Wingtip hello](sql-database-saas-tutorial.md)
* Azure PowerShell è installato. Per informazioni dettagliate, vedere [Introduzione ad Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

## <a name="introduction-toohello-saas-catalog-pattern"></a>Introduzione toohello modello SaaS catalogo

In un'applicazione SaaS multi-tenant di backup del database, è importante tooknow memorizzazione informazioni per ogni tenant. Nel modello di catalogo hello SaaS, un database del catalogo è hello toohold usato il mapping tra ogni tenant e in cui sono archiviati i dati. app SaaS Wingtip Hello Usa un single-tenant per ogni architettura del database, ma si applica modello di base hello di archiviare i mapping di tenant al database in un catalogo se viene utilizzato un database multi-tenant o single-tenant.

Ogni tenant viene assegnato a una chiave che identifica le nel catalogo di hello e che viene eseguito il mapping di percorso toohello del database appropriato hello. Nell'applicazione SaaS Wingtip hello chiave hello è formata da un hash del nome del tenant hello. Questo consente di parte del nome tenant hello di hello applicazione URL toobe usati chiave hello tooconstruct. Per la chiave del tenant è possibile usare anche altri schemi.  

catalogo Hello consente nome hello o un percorso di hello database toobe modificato con un impatto minimo sull'applicazione hello.  In un modello di database multi-tenant, ciò consente anche di "spostare" un tenant da un database a un altro.  catalogo Hello può essere utilizzato tooindicate anche se un tenant o il database è offline per manutenzione o altre azioni. Ciò viene esaminata in hello [ripristinare esercitazione single-tenant](sql-database-saas-tutorial-restore-single-tenant.md).

Inoltre, catalogo hello, che è in effetti un database di gestione per un'applicazione SaaS, è possibile archiviare metadati aggiuntivi tenant o un database, ad esempio hello livello o edizione di un database, la versione dello schema, il piano di servizio o i contratti di servizio offerti tootenants e altre informazioni che consente la gestione delle applicazioni, il supporto tecnico o processi devops.  

Oltre a hello applicazione SaaS, catalogo hello possibile abilitare gli strumenti di database.  Nell'esempio Wingtip SaaS hello catalogo hello è query tra tenant tooenable usato, esplorata in hello [esercitazione analitica ad hoc](sql-database-saas-tutorial-adhoc-analytics.md). Gestione dei processi tra database viene esaminato in hello [la gestione dello schema](sql-database-saas-tutorial-schema-management.md) e [tenant analitica](sql-database-saas-tutorial-tenant-analytics.md) esercitazioni. 

Nell'applicazione SaaS Wingtip hello catalogo hello viene implementata utilizzando le funzionalità di gestione di partizioni hello di hello [elastico Database Client libreria (EDCL)](sql-database-elastic-database-client-library.md). Consente di Hello EDCL toocreate un'applicazione, gestire e utilizzare una mappa partizioni di database di backup. Una mappa partizioni contiene un elenco di partizioni (database) e il mapping di hello tra database e le chiavi (tenant).  EDCL funzioni possono essere usate da applicazioni o script di PowerShell durante le voci di hello toocreate nella mappa partizioni hello di provisioning del tenant e da applicazioni tooefficiently connettersi toohello database corretto. EDCL memorizza nella cache database del catalogo connessione informazioni toominimize hello traffico toohello e velocizzare l'applicazione hello.  

> [!IMPORTANT]
> i dati di mapping Hello sono accessibili nel database di catalogo hello, ma *non modificarlo*! Modificare i dati di mapping solo tramite le API della libreria client dei database elastici. La modifica diretta dei dati di mapping hello rischi di danneggiamento hello del catalogo e non sono supportati.


## <a name="introduction-toohello-saas-provisioning-pattern"></a>Modello di Provisioning SaaS toohello introduzione

Al momento del caricamento di un nuovo tenant in un'applicazione SaaS che usa un modello di database a tenant singolo, è necessario eseguire il provisioning di un nuovo database tenant.  Deve essere creato nella posizione appropriata hello e il livello di servizio, inizializzato con appropriati dello schema e dati di riferimento e quindi registrati nel catalogo di hello nella chiave del tenant appropriato hello.  

Diversi approcci possono essere utilizzato toodatabase provisioning, che potrebbe includere l'esecuzione di script SQL, la distribuzione di un file bacpac o copia di un database modello 'finale'.  

la strategia di gestione generale dello schema, che devono garantire che vengono effettuato il provisioning di nuovi database con schema più recente di hello è necessario comprendere Hello provisioning approccio adottato.  Ciò viene esaminata in hello [esercitazione Gestione schema](sql-database-saas-tutorial-schema-management.md).  

Hello Wingtip SaaS app disposizioni nuovi tenant copiando un database finale denominato basetenantdb, distribuito nel server di catalogo hello.  Provisioning può essere integrato in un'applicazione hello come parte di un'esperienza di iscrizione e/o supportato in modalità offline mediante script. Questa esercitazione illustra il provisioning tramite PowerShell. gli script di provisioning Hello copiare hello basetenantdb toocreate un nuovo database tenant in un pool elastico, quindi inizializzano con informazioni specifici del tenant e registrarlo nella mappa partizioni di hello catalogo.  Nell'applicazione di esempio hello, i database vengono assegnati nomi in base al nome di tenant hello, ma non si tratta di una parte essenziale del modello di hello: hello catalogo hello consente qualsiasi database di nome toobe assegnato toohello. + 


## <a name="get-hello-wingtip-application-scripts"></a>Ottenere script per l'applicazione hello Wingtip

Hello Wingtip SaaS script e codice sorgente dell'applicazione sono disponibili in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repository github. [I passaggi di script di SaaS Wingtip hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).


## <a name="provision-and-catalog-detailed-walkthrough"></a>Procedura dettagliata per il provisioning e la catalogazione

toounderstand come hello Wingtip applicazione implementa nuovo provisioning del tenant, aggiungere un punto di interruzione e passaggio tramite flusso di lavoro hello durante il provisioning di un tenant:

1. Apri... \\Moduli learning\\ProvisionAndCatalog\\_Demo ProvisionAndCatalog.ps1_ e hello set seguenti parametri:
   * **$TenantName** = nome hello del nuovo aspetto hello (ad esempio, *Bushwillow blu*).
   * **$VenueType** = uno dei tipi di eventi predefiniti hello: *blu*, classicalmusic, danza, jazz, judo, motorracing, con più finalità, opera, rockmusic, calcio.
   * **$DemoScenario** = **1**, impostare troppo**1** troppo*il provisioning di un singolo tenant*.

1. Aggiungere un punto di interruzione posizionando il cursore in qualsiasi punto in 48, hello una riga che afferma: *nuovo Tenant '*e premere **F9**.

   ![punto di interruzione](media/sql-database-saas-tutorial-provision-and-catalog/breakpoint.png)

1. Premere di script hello toorun **F5**.

1. Dopo l'esecuzione dello script hello si interrompe al punto di interruzione hello, premere **F11** toostep codice hello.

   ![punto di interruzione](media/sql-database-saas-tutorial-provision-and-catalog/debug.png)



Tracciare l'esecuzione dello script hello utilizzando hello **Debug** opzioni di menu - **F10** e **F11** toostep su o in funzioni chiamate hello. Per altre informazioni sul debug degli script di PowerShell, vedere [Suggerimenti per l'utilizzo e il debug degli script di PowerShell](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/how-to-debug-scripts-in-windows-powershell-ise).


di seguito Hello non sono tooexplicitly attenersi alla procedura, ma una spiegazione del flusso di lavoro hello che scorrere durante il debug di script hello:

1. **Hello importazione SubscriptionManagement.psm1** modulo che contiene funzioni per la firma in tooAzure e selezionando hello sottoscrizione di Azure in uso.
1. **Hello importazione CatalogAndDatabaseManagement.psm1** modulo che fornisce un catalogo e un tenant a livello di astrazione su hello [gestione di partizioni](sql-database-elastic-scale-shard-map-management.md) funzioni. Si tratta di un modulo importante incapsula gran parte del modello di catalogo hello, che vale la pena considerare.
1. **Recupero dei dettagli di configurazione**. Eseguire Get-configurazione (F11) e la configurazione dell'applicazione hello è specificato. I nomi delle risorse e altri valori specifici dell'app vengono definite qui, ma non modificare questi valori fino a quando non si ha familiarità con gli script hello.
1. **Ottenere l'oggetto catalogo hello**. Eseguire Get-catalogo che compone e restituisce l'oggetto catalogo utilizzato nello script di livello superiore di hello.  Questa funzione usa funzioni di gestione di partizioni importate da **AzureShardManagement.psm1**. oggetto catalogo Hello è costituito dai seguenti hello:
   * $catalogServerFullyQualifiedName viene costruita utilizzando stem standard hello e il nome utente: _catalogo -\<utente\>. database.windows.net_.
   * $catalogDatabaseName viene recuperato dalla configurazione hello: *tenantcatalog*.
   * oggetto $shardMapManager viene inizializzato dai database del catalogo hello.
   * oggetto $shardMap viene inizializzato da hello *tenantcatalog* mappa partizioni nel database di catalogo hello.
   Un oggetto del catalogo è composta da restituito e usato nello script di livello superiore di hello.
1. **Calcolare la nuova chiave tenant di hello**. Una funzione hash è una chiave del tenant hello toocreate utilizzato dal nome di tenant hello.
1. **Verifica se esiste già una chiave del tenant hello**. catalogo Hello viene verificata tooensure hello chiave è disponibile.
1. **viene eseguito il provisioning di database tenant Hello con New-TenantDatabase.** Utilizzare **F11** toostep in e vedere come database hello viene eseguito il provisioning con un [modello di Azure Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md).

nome del database Hello viene costruito da hello tenant nome toomake sia cancellare quale partizione appartiene toowhich tenant. (Altre strategie per la denominazione dei database può essere facilmente utilizzati.) + Un modello di gestione risorse è toocreate utilizzato un database tenant copiando un database finale (baseTenantDB) nel server di catalogo hello. Un approccio alternativo potrebbe essere toocreate un database vuoto e quindi inizializzarlo importando un file bacpac o tooexecute uno script di inizializzazione da un percorso noto.  

il modello di gestione risorse di Hello si trova nella cartella di Modules\Common\ ...\Learning hello: *tenantdatabasecopytemplate.json*

Dopo aver creato il database di tenant hello, è quindi ulteriore **inizializzato con il nome di evento (tenant) hello e il tipo di evento hello**. In questa posizione è possibile eseguire anche altre inizializzazioni.

Hello **database tenant è registrato nel catalogo di hello** con *Aggiungi TenantDatabaseToCatalog* con chiave del tenant hello. Utilizzare **F11** toostep i dettagli di hello:

* database del catalogo Hello viene aggiunta una mappa partizioni toohello (hello elenco database noti).
* viene creato il mapping di tale partizionamento toohello valore della chiave di collegamenti hello Hello.
* Metadati aggiuntivi (nome della struttura hello) sul tenant hello viene aggiunto tabella tenant toohello nel catalogo di hello.  tabella tenant Hello non fa parte dello schema ShardManagement hello e non è installata per hello EDCL.  Questa tabella viene illustrato come database di catalogo hello può essere esteso toosupport di ulteriori dati specifici dell'applicazione.   


Una volta al termine del provisioning, esecuzione restituisce toohello originale *Demo ProvisionAndCatalog* script, che consente di aprire hello **eventi** pagina per il tenant di nuovo hello nel browser hello:

   ![eventi](media/sql-database-saas-tutorial-provision-and-catalog/new-tenant.png)


## <a name="provision-a-batch-of-tenants"></a>Eseguire il provisioning di un batch di tenant

Questo esercizio descrive come effettuare il provisioning di un batch di 17 tenant. Si consiglia che effettuare il provisioning di questo batch di tenant prima di avviare altre esercitazioni Wingtip SaaS, pertanto non esiste più di pochi toowork database con.

1. Apri... \\Moduli learning\\ProvisionAndCatalog\\*Demo ProvisionAndCatalog.ps1* in hello *PowerShell ISE* e modificare hello *$ DemoScenario* too3 parametro:
   * **$DemoScenario** = **3**, modificare anche**3** troppo*il provisioning di un batch di tenant*.
1. Premere **F5** ed eseguire script hello.

script Hello distribuisce un batch di altri tenant. Usa un [modello di Azure Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md) che controlla il batch hello e delega quindi il provisioning di ogni modello di database tooa collegato. L'utilizzo di modelli in questo modo consente Azure Resource Manager toobroker hello processo per lo script di provisioning. Modelli di eseguire il provisioning di database in parallelo in cui è possibile e gestisce i tentativi, se necessario, hello processo generale di ottimizzazione. script Hello è idempotente pertanto, se non riesce o si interrompe per qualsiasi motivo, eseguirlo nuovamente.

### <a name="verify-hello-batch-of-tenants-successfully-deployed"></a>Verificare i batch di hello di tenant distribuito correttamente

* Aprire hello *tenants1* server selezionando tooyour elenco dei server hello [portale di Azure](https://portal.azure.com), fare clic su **database SQL**e verificare batch hello di 17 database aggiuntivi sono ora Nell'elenco di hello:

   ![elenco di database](media/sql-database-saas-tutorial-provision-and-catalog/database-list.png)



## <a name="other-provisioning-patterns"></a>Altri modelli di provisioning

Gli altri modelli di provisioning non inclusi in questa esercitazione includono:

**Pre-provisioning di database.** Hello pre-provisioning modello sfrutta il fatto hello che non si aggiungono i database in un pool elastico di costi aggiuntivi. Fatturazione per il pool elastico hello, hello non database, così i database inattivi senza risorse. Effettuando il pre-provisioning dei database in un pool e allocandoli poi all'occorrenza, il tempo di caricamento dei tenant può essere ridotto significativamente. numero di Hello di pre-provisioning di database potrebbe modificato come tookeep necessari un buffer adatto per hello anticipato velocità di provisioning.

**Provisioning automatico.** Nel modello di provisioning automatico hello, un servizio di provisioning dedicato è server tooprovision utilizzati e i pool database automaticamente in base alle esigenze, inclusi i database di pre-provisioning nel pool elastico, se lo si desidera. E se i database vengono incaricati di deprovisioning ed eliminati, i gap nel pool elastico può essere compilato da hello provisioning del servizio in base alle esigenze. Un servizio di questo tipo può essere semplice o complesso, come nel caso della gestione del provisioning in più aree geografiche, e può includere la configurazione automatica della replica geografica se si usa tale strategia per il ripristino di emergenza. Con modello di provisioning automatico hello, un'applicazione client o script deve inviare un provisioning toobe coda tooa richiesta elaborata hello provisioning del servizio e potrebbe quindi eseguire il polling completamento toodetermine del servizio hello. Se viene utilizzato pre-provisioning, le richieste verrebbero gestite rapidamente con servizio di hello gestiscono il provisioning di un database di sostituzione in esecuzione in background hello.



## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come:

> [!div class="checklist"]

> * Effettuare il provisioning di un nuovo tenant singolo
> * Effettuare il provisioning di un batch di altri tenant
> * Esegui istruzione dettagli hello del tenant di provisioning e registrarli nel catalogo di hello

Provare a hello [esercitazione di monitoraggio delle prestazioni](sql-database-saas-tutorial-performance-monitoring.md).

## <a name="additional-resources"></a>Risorse aggiuntive

* Ulteriori [esercitazioni in cui si basano su hello applicazione SaaS Wingtip](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Libreria client dei database elastici](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-database-client-library)
* [Come tooDebug gli script in Windows PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/how-to-debug-scripts-in-windows-powershell-ise)
