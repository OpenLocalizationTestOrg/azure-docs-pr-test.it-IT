---
title: "aaaWhat è automazione di Azure | Documenti Microsoft"
description: "Il valore di automazione di Azure fornisce informazioni e ottenere risposte alle domande toocommon in modo che è possibile iniziare creazione, usando i runbook e Automation DSC per Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "che cos'è l'automazione, Automazione di Azure, esempi di Automazione di Azure"
ms.assetid: 0cf1f3e8-dd30-4f33-b52a-e148e97802a9
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/10/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 1e5a90e272d6b2beb7b5007e2fea2c110dbd79b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-overview"></a>Panoramica di Automazione di Azure
Automazione di Microsoft Azure offre un modo per gli utenti tooautomate hello manuale, con esecuzione prolungata, soggette a errori e ripetute spesso le attività che sono in genere eseguite in un ambiente cloud e aziendali. Consente di risparmiare tempo e aumenta l'affidabilità di hello delle normali attività amministrative e anche le pianifica toobe automaticamente eseguiti a intervalli regolari. È possibile automatizzare i processi utilizzando runbook o automatizzare la gestione della configurazione tramite Configurazione dello stato desiderato. Questo articolo fornisce una breve panoramica su Automazione di Azure e risposte ad alcune domande comuni. Per informazioni più dettagliate su argomenti diversi hello, è possibile consultare tooother articoli in questa libreria.

## <a name="automating-processes-with-runbooks"></a>Automazione di processi con runbook
Un Runbook è un set di attività che eseguono un processo automatico in Automazione di Azure. Potrebbe essere un processo semplice, ad esempio l'avvio di una macchina virtuale e la creazione di una voce di log, o potrebbe essere un runbook complesso che combina altri tooperform runbook più piccoli di un processo complesso con più risorse o anche più cloud e ambienti locali.  

Ad esempio, potrebbe essere un manuale esistente di processo per il troncamento di un database SQL, se sta per raggiungere le dimensioni massime che include più passaggi, ad esempio server toohello connessione, la connessione di database toohello, ottenere hello dimensione corrente del database, controllare se soglia superata troncarlo e notificare l'utente. Invece di eseguire manualmente ognuno di questi passaggi, è possibile creare un Runbook che eseguirà tutte queste attività come un singolo processo. Iniziare hello runbook, forniscono informazioni hello necessarie, ad esempio nome hello SQL server, nome del database e posta elettronica dei destinatari e quindi si trovano durante il processo di hello completa. 

## <a name="what-can-runbooks-automate"></a>Cosa consentono di automatizzare i Runbook?
I Runbook di Automazione di Azure si basano sul flusso di lavoro PowerShell di Windows o su PowerShell di Windows, pertanto consentono di effettuare tutto ciò che è possibile effettuare in PowerShell. Se un'applicazione o un servizio dispongono di un'API, un Runbook permette di utilizzarli. Se si dispone di un modulo di PowerShell per un'applicazione hello, è possibile caricare tale modulo in automazione di Azure e includono i cmdlet nel runbook. I runbook di automazione Azure eseguite in hello cloud di Azure e possono accedere a qualsiasi risorse cloud o le risorse esterne accessibili dal cloud hello. Utilizzando [Runbook Worker ibrido](automation-hybrid-runbook-worker.md), i runbook è possono eseguire nei dati locali alle risorse locali toomanage center. 

## <a name="getting-runbooks-from-hello-community"></a>Ottenere i runbook dalla community di hello
Hello [raccolta Runbook](automation-runbook-gallery.md#runbooks-in-runbook-gallery) contiene i runbook dalla community di Microsoft e hello che è possibile utilizzare senza modificato nell'ambiente in uso oppure personalizzarli per le proprie esigenze. Sono anche utili tooas riferimenti toolearn come toocreate runbook personalizzati. È anche possibile contribuire propria raccolta toohello runbook che si ritiene che altri utenti possono trovare utili. 

## <a name="creating-runbooks-with-azure-automation"></a>Creazione di Runbook con Automazione di Azure
È possibile [creare runbook personalizzati](automation-creating-importing-runbook.md) da file temporanei o modificare i runbook hello [raccolta Runbook](http://msdn.microsoft.com/library/azure/dn781422.aspx) per i propri requisiti. Sono disponibili quattro diversi [tipi di runbook](automation-runbook-types.md) tra cui è possibile scegliere in base alle esigenze e all'uso di PowerShell. Se si preferisce toowork direttamente con hello codice PowerShell, è quindi possibile utilizzare un [runbook PowerShell](automation-runbook-types.md#powershell-runbooks) o [runbook del flusso di lavoro di PowerShell](automation-runbook-types.md#powershell-workflow-runbooks) modificare offline o con hello [testuale editor](http://msdn.microsoft.com/library/azure/dn879137.aspx) in hello portale di Azure. Se si preferisce tooedit un runbook senza essere esposti toohello codice sottostante, quindi è possibile creare un [runbook grafico](automation-runbook-types.md#graphical-runbooks) utilizzando hello [editor grafico](automation-graphical-authoring-intro.md) in hello portale di Azure. 

Se si preferisce guardare il video tooreading, Sono esaminati hello seguito video dalla sessione di Microsoft Ignite in maggio 2015. Nota: Sebbene hello concetti e le funzionalità descritte in questo video siano corrette, che automazione di Azure è molto avanzato poiché in questo video è stato registrato, ora con un'interfaccia utente più estesa nel portale di Azure hello e supporta le funzionalità aggiuntive.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3451/player]
> 
> 

## <a name="automating-configuration-management-with-desired-state-configuration"></a>Automazione della gestione della configurazione con Configurazione dello stato desiderato
[PowerShell DSC](https://technet.microsoft.com/library/dn249912.aspx) è una piattaforma di gestione che consente di toomanage, distribuire e applicare una configurazione per gli host fisici e macchine virtuali usando una sintassi dichiarativa di PowerShell. È possibile definire configurazioni su un server centrale DSC Pull che i computer di destinazione possono recuperare e applicare automaticamente. DSC fornisce un set di cmdlet di PowerShell che è possibile utilizzare le risorse e configurazioni toomanage.  

[Automation DSC per Azure](automation-dsc-overview.md) è una soluzione basata su cloud per DSC PowerShell che fornisce i servizi necessari per gli ambienti aziendali.  È possibile gestire le risorse DSC in automazione di Azure e applicare le configurazioni toovirtual o computer fisici che li recuperano da un Server di Pull DSC in hello cloud di Azure.  Fornisce inoltre servizi di creazione report che informano di eventi importanti, ad esempio quando i nodi hanno deviato dalla configurazione assegnata e quando una nuova configurazione è stata applicata. 

## <a name="creating-your-own-dsc-configurations-with-azure-automation"></a>Creazione di configurazioni personalizzate DSC con Automazione di Azure
[Le configurazioni DSC](automation-dsc-overview.md) specificare lo stato di hello desiderato di un nodo.  Più nodi è possono applicare hello stesso tooassure di configurazione che mantengono un stato identico.  È possibile creare una configurazione usando qualsiasi editor di testo sul computer locale e quindi importarla in Automazione di Azure dove è possibile compilarla e applicarvi nodi.

## <a name="getting-modules-and-configurations"></a>Recupero di moduli e configurazioni
È possibile ottenere [moduli PowerShell](automation-runbook-gallery.md#modules-in-powershell-gallery) contenente i cmdlet che è possibile utilizzare i runbook e le configurazioni DSC da hello [PowerShell Gallery](http://www.powershellgallery.com/). È possibile avviare la raccolta dal portale di Azure hello e importare moduli direttamente in automazione di Azure, oppure è possibile scaricare e importarli manualmente. È possibile installare i moduli di hello direttamente dal portale di Azure hello, ma è possibile scaricarli installarli come si farebbe con qualsiasi altro modulo. 

## <a name="example-practical-applications-of-azure-automation"></a>Applicazioni pratiche di esempio di Automazione di Azure
Di seguito sono solo alcuni esempi di che cosa sono hello tipi di scenari di automazione con automazione di Azure. 

* Creare e copiare le macchine virtuali in diverse sottoscrizioni di Azure. 
* Pianificare le copie dei file da un contenitore di archiviazione Blob di Azure tooan computer locale. 
* Automatizzare le funzioni di sicurezza, ad esempio negare le richieste da un client quando viene rilevato un attacco Denial of service. 
* Garantire che i computer si allineino continuamente con i criteri di sicurezza configurati.
* Gestire la distribuzione continua del codice dell'applicazione tra cloud e infrastruttura locale. 
* Creare una foresta di Active Directory in Azure per l'ambiente lab. 
* Troncare una tabella in un database SQL se il DB sta per raggiungere le dimensioni massime. 
* Aggiornare in remoto le impostazioni dell'ambiente per un sito Web di Azure. 

## <a name="how-does-azure-automation-relate-tooother-automation-tools"></a>Correlazione di strumenti di automazione tooother automazione di Azure
[Service Management Automation (SMA)](http://technet.microsoft.com/library/dn469260.aspx) è previsto tooautomate attività di gestione nel cloud privato hello. Viene installato in locale nel data center come componente di [Microsoft Azure Pack](https://www.microsoft.com/en-us/server-cloud/). SMA e automazione di Azure usano hello stesso formato di runbook basato su Windows PowerShell e il flusso di lavoro di Windows PowerShell, ma non supporta SMA [runbook grafici](automation-graphical-authoring-intro.md).  

[System Center 2012 Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) è stato progettato per consentire l'automazione delle risorse locali. Utilizza un formato di runbook diverso da quello di automazione di Azure e Service Management Automation e dispone di un runbook toocreate interfaccia grafica senza richiedere alcuno script. I Runbook dello strumento sono composti da attività di Integration Pack scritti specificatamente per Orchestrator. 

## <a name="where-can-i-get-more-information"></a>Dove è possibile ottenere ulteriori informazioni?
Un'ampia gamma di risorse sono disponibili per toolearn per ulteriori informazioni sull'automazione di Azure e la creazione di runbook personalizzati. 

* **Automazione di Azure di MSDN Library** è il punto in cui ci si trova in questo momento. articoli di Hello in questa libreria forniscono la documentazione completa sulla configurazione di hello e amministrazione di automazione di Azure e per la creazione di runbook personalizzati. 
* [cmdlet di Azure PowerShell](http://msdn.microsoft.com/library/jj156055.aspx) fornisce informazioni per l'automazione di operazioni di Azure con Windows PowerShell. I runbook utilizzano toowork questi cmdlet con risorse di Azure. 
* [Blog di gestione](https://azure.microsoft.com/blog/tag/azure-automation/) sono disponibili informazioni più recenti hello in automazione di Azure e altre tecnologie di gestione di Microsoft. È necessario sottoscrivere toothis blog toostay backup toodate con hello più recente dal team di automazione di Azure hello. 
* [Forum di automazione](http://go.microsoft.com/fwlink/p/?LinkId=390561) consente toopost problemi risolti da Microsoft e della community di automazione hello toobe di automazione di Azure. 
* [cmdlet di Automazione di Azure](https://msdn.microsoft.com/library/mt244122.aspx) fornisce informazioni per l'automazione delle attività di amministrazione. Contiene gli account di automazione toomanage cmdlet, risorse, i runbook, DSC.

## <a name="can-i-provide-feedback"></a>È possibile fornire commenti e suggerimenti?
**Gli utenti sono invitati a fornire commenti e suggerimenti.** Se si è in cerca di una soluzione Runbook o di un modulo di integrazione di Automazione di Azure, inviare una richiesta di script in Script Center. In caso di commenti o suggerimenti oppure di richieste di funzionalità per Automazione di Azure, è possibile pubblicarle nell'apposito [forum](http://feedback.windowsazure.com/forums/34192--general-feedback). Grazie. 

