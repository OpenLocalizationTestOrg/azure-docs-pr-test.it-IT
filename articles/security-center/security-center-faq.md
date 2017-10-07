---
title: Centro sicurezza PC domande frequenti (FAQ) aaaAzure | Documenti Microsoft
description: Queste FAQ rispondono alle domande sul Centro sicurezza di Azure.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: be2ab6d5-72a8-411f-878e-98dac21bc5cb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: cd0c0f8bdf15cdaf5889f2da5ac3cadf6017a9e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-frequently-asked-questions-faq"></a>Domande frequenti sul Centro sicurezza di Azure
Questo risposte alle domande sul Centro protezione di Azure, un servizio che consente di impedire, rilevare e rispondere toothreats con una maggiore visibilità e controllo sulla protezione hello delle risorse di Microsoft Azure.

> [!NOTE]
> A partire da anticipata giugno 2017, centro di sicurezza verrà utilizzata toocollect Microsoft Monitoring Agent hello e archiviare i dati. vedere, più toolearn [migrazione della piattaforma Azure sicurezza Center](security-center-platform-migration.md). informazioni di Hello in questo articolo rappresentano funzionalità Centro sicurezza dopo la transizione toohello Microsoft Monitoring Agent.
>
>

## <a name="general-questions"></a>Domande generali
### <a name="what-is-azure-security-center"></a>Che cos'è il Centro sicurezza di Azure?
Centro sicurezza di Azure consente di impedire, rilevare e rispondere toothreats con una maggiore visibilità e controllo sulla protezione hello delle risorse di Azure. Offre funzionalità integrate di monitoraggio della sicurezza e gestione dei criteri tra le sottoscrizioni, facilita il rilevamento delle minacce che altrimenti passerebbero inosservate e funziona con un ampio ecosistema di soluzioni di sicurezza.

### <a name="how-do-i-get-azure-security-center"></a>In che modo è possibile accedere al Centro sicurezza di Azure?
Centro sicurezza di Azure è abilitata con la sottoscrizione di Microsoft Azure, accessibile da hello [portale di Azure](https://azure.microsoft.com/features/azure-portal/). ([Accedi al portale toohello](https://portal.azure.com)selezionare **Sfoglia**e lo scorrimento troppo**Centro sicurezza PC**).  

## <a name="billing"></a>Fatturazione
### <a name="how-does-billing-work-for-azure-security-center"></a>Come funziona la fatturazione per il Centro sicurezza di Azure?
Il Centro sicurezza è disponibile in due livelli:

Hello **livello gratuito** offre una visibilità in stato protezione hello le risorse di Azure, i criteri di sicurezza di base, consigli sulla sicurezza e l'integrazione con prodotti e servizi dei partner.

Hello **livello Standard** aggiunge minaccia avanzata funzionalità di rilevamento, tra cui minaccia intelligence, l'analisi del comportamento, il rilevamento di anomalie, eventi di sicurezza e i report di attribuzione di minaccia. livello Standard Hello è gratuito per hello 60 giorni prima. È consigliabile scegliere servizio di hello toouse toocontinue oltre 60 giorni, verranno automaticamente toocharge per servizio hello.  tooupgrade, tariffario selezionare in hello [criteri di sicurezza](security-center-policies.md#set-security-policies). vedere, più toolearn [Centro sicurezza PC prezzi](security-center-pricing.md).

## <a name="permissions"></a>Autorizzazioni
Centro sicurezza di Azure Usa [controllo di accesso basato sui ruoli (RBAC)](../active-directory/role-based-access-control-configure.md), che fornisce [ruoli predefiniti](../active-directory/role-based-access-built-in-roles.md) che può essere assegnato toousers, gruppi e i servizi in Azure.

Centro sicurezza PC valuta configurazione hello di problemi di sicurezza di risorse tooidentify e vulnerabilità. Centro sicurezza PC, visualizzare solo le informazioni correlate tooa risorse quando l'utente viene assegnato hello ruolo di proprietario, collaboratore o lettore per il gruppo hello sottoscrizione o la risorsa a cui appartiene una risorsa.

Vedere [autorizzazioni nel Centro protezione Azure](security-center-permissions.md) toolearn informazioni sui ruoli e le operazioni consentite in Centro sicurezza PC.

## <a name="data-collection"></a>Raccolta dei dati
Centro sicurezza PC raccoglie i dati da tooassess le macchine virtuali lo stato di protezione, fornire consigli sulla sicurezza e ricevere un avviso toothreats. La prima volta che si accede al Centro sicurezza, la raccolta dati viene abilitata in tutte le macchine virtuali della sottoscrizione. È inoltre possibile abilitare la raccolta dei dati hello criterio Centro sicurezza PC.

### <a name="how-do-i-disable-data-collection"></a>Come si disabilita la raccolta dati?
Se si utilizza livello Centro protezione Azure Free hello, è possibile disabilitare la raccolta dei dati dalle macchine virtuali in qualsiasi momento. Raccolta dati è obbligatorio per le sottoscrizioni nel livello Standard hello. È possibile disabilitare la raccolta dei dati per una sottoscrizione in hello criteri di sicurezza. ([Accedi al portale di Azure toohello](https://portal.azure.com)selezionare **Sfoglia**selezionare **Centro sicurezza PC**e selezionare **criteri**.)  Quando si seleziona una sottoscrizione, un nuovo pannello viene aperto e fornisce l'opzione tooturn hello off **la raccolta dei dati**.

### <a name="how-do-i-enable-data-collection"></a>Come si abilita la raccolta dati?
È possibile abilitare la raccolta dei dati per la sottoscrizione di Azure in hello criteri di sicurezza. raccolta di dati tooenable. [Accedi al portale di Azure toohello](https://portal.azure.com)selezionare **Sfoglia**selezionare **Centro sicurezza PC**e selezionare **criteri**. Impostare **la raccolta dei dati** troppo**su**.

### <a name="what-happens-when-data-collection-is-enabled"></a>Cosa accade quando si abilita la raccolta dati?
Quando la raccolta dei dati è abilitata, hello Microsoft Monitoring Agent è automaticamente disponibile in tutte esistenti e supportate nuove macchine virtuali distribuite nella sottoscrizione hello.

### <a name="does-hello-monitoring-agent-impact-hello-performance-of-my-servers"></a>Non hello prestazioni hello impatto dell'agente di monitoraggio di my Server?
agente Hello utilizza una quantità nominale delle risorse di sistema e deve avere un impatto minimo sulle prestazioni di hello. Per ulteriori informazioni sulla riduzione delle prestazioni e dell'agente di hello e l'estensione, vedere hello [Guida alla pianificazione e le operazioni](security-center-planning-and-operations-guide.md#data-collection-and-storage).

### <a name="where-is-my-data-stored"></a>Dove vengono archiviati i dati?
I dati raccolti dall'agente vengono archiviati in un'area di lavoro di Log Analytics esistente associata alla sottoscrizione o in una nuova area di lavoro. Per altre informazioni, vedere [Sicurezza dei dati](security-center-data-security.md).

## <a name="using-azure-security-center"></a>Utilizzo del Centro sicurezza di Azure
### <a name="what-is-a-security-policy"></a>Cosa sono i criteri di sicurezza?
Un criterio di sicurezza definisce il set di hello di controlli che sono consigliati per le risorse all'interno di hello specificato sottoscrizione. Nel centro di sicurezza di Azure, definire criteri per le sottoscrizioni di Azure in base della società tooyour requisiti di protezione e riservatezza dei dati di hello in ogni sottoscrizione o tipo hello delle applicazioni.

criteri di sicurezza Hello abilitati nelle indicazioni relative alla sicurezza unità Centro sicurezza di Azure e monitoraggio. toolearn informazioni sui criteri di sicurezza, vedere [il monitoraggio dello stato di sicurezza nel Centro protezione Azure](security-center-monitoring.md).

### <a name="who-can-modify-a-security-policy"></a>Chi può modificare i criteri di sicurezza?
toomodify un criterio di sicurezza, è necessario essere un amministratore della sicurezza o un proprietario o collaboratore della sottoscrizione.

toolearn tooconfigure un criterio di sicurezza, vedere [l'impostazione di criteri di sicurezza nel Centro protezione Azure](security-center-policies.md).

### <a name="what-is-a-security-recommendation"></a>Che cos'è un suggerimento per la sicurezza?
Centro sicurezza di Azure consente di analizzare lo stato di sicurezza hello delle risorse di Azure. Quando vengono identificate potenziali vulnerabilità di sicurezza, vengono creati i suggerimenti. Guida di indicazioni Hello è illustrato il processo di hello di configurazione hello necessario controllo. Alcuni esempi:

* Provisioning di antimalware toohelp identificare e rimuovere il software dannoso
* Configurazione [gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md) e regole macchine toovirtual di traffico toocontrol
* Provisioning di un toohelp di firewall applicazione web difendersi da attacchi diretti alle applicazioni web
* Distribuzione degli aggiornamenti di sistema mancanti
* Indirizzamento delle configurazioni del sistema operativo che non corrispondono a hello consiglia le linee di base

Qui vengono visualizzati solo i suggerimenti abilitati in Criteri di sicurezza.

### <a name="how-can-i-see-hello-current-security-state-of-my-azure-resources"></a>È possibile vedere stato di protezione delle risorse di Azure corrente hello?
Hello **Panoramica Centro di sicurezza** pannello Mostra hello generali di sicurezza dell'ambiente ripartito per applicazioni e dati, archiviazione, rete e calcolo. Ciascun tipo di risorsa presenta un indicatore che visualizza l'eventuale rilevamento di potenziali vulnerabilità di sicurezza. Fare clic su ogni sezione Visualizza un elenco di problemi di sicurezza identificati da Centro sicurezza PC, insieme a un inventario delle risorse di hello nella sottoscrizione.

### <a name="what-triggers-a-security-alert"></a>Che cosa attiva un avviso di sicurezza?
Centro sicurezza di Azure automaticamente raccoglie, analizza e integra queste dati del log da risorse di Azure, rete hello e soluzioni partner come i firewall e antimalware. Quando vengono rilevate minacce, viene creato un avviso di sicurezza. Ad esempio, è compreso il rilevamento di:

* Macchine virtuali compromesse in comunicazione con indirizzi IP dannosi noti
* Malware avanzato rilevato mediante i report degli errori di Windows
* Attacchi di forza bruta contro le macchine virtuali
* Avvisi di sicurezza da soluzioni di sicurezza integrata dei partner, ad esempio antimalware o Web application firewall

### <a name="whats-hello-difference-between-threats-detected-and-alerted-on-by-microsoft-security-response-center-versus-azure-security-center"></a>Qual è la differenza hello tra minacce rilevate e ricevere un avviso su da Microsoft Security Response Center e Centro sicurezza di Azure?
Hello Microsoft Security Response Center (MSRC) esegue un monitoraggio seleziona sicurezza di rete di Azure hello e dell'infrastruttura e riceve threat intelligence ed evitare eventuali abusi reclamo di terze parti. Quando MSRC diventa tenere presente che i dati dei clienti eseguiti da una parte di illecito o non autorizzata o utilizzo del cliente hello di Azure non è conforme con le condizioni di hello per utilizzare accettabile, un gestore degli eventi imprevisti di protezione notifica al cliente di hello. Notifica si verifica in genere inviando una sicurezza toohello di posta elettronica, contatti specificati nel Centro sicurezza di Azure o hello proprietario della sottoscrizione di Azure, se non viene specificato un contatto di sicurezza.

Centro di sicurezza è un servizio di Azure che monitora l'ambiente di Azure del cliente hello e applica analitica tooautomatically continuamente rilevare un'ampia gamma di attività potenzialmente dannose. I rilevamenti vengono rilevati come avvisi di sicurezza nel dashboard di hello Centro sicurezza PC.

### <a name="which-azure-resources-are-monitored-by-azure-security-center"></a>Quali risorse di Azure vengono monitorate dal Centro sicurezza di Azure?
Centro sicurezza di Azure monitora hello seguendo le risorse di Azure:

* Macchine virtuali (VM) (inclusi i [Servizi cloud](../cloud-services/cloud-services-choose-me.md))
* Reti virtuali di Azure
* Servizio di SQL Azure
* Account di archiviazione di Azure
* App Web di Azure in un [ambiente del servizio app](../app-service/app-service-app-service-environments-readme.md)
* Soluzioni partner integrate con la sottoscrizione di Azure, ad esempio un Web application firewall, nelle VM e nell' [ambiente del servizio app](../app-service/app-service-app-service-environments-readme.md)

## <a name="virtual-machines"></a>Macchine virtuali
### <a name="what-types-of-virtual-machines-are-supported"></a>Quali tipi di macchine virtuali sono supportati?
Monitoraggio e le indicazioni sono disponibili per le macchine virtuali (VM) create utilizzando entrambi hello [classica e modelli di distribuzione di gestione risorse](../azure-classic-rm.md).

Per l'elenco delle piattaforme supportate vedere [Supported platforms in Azure Security Center](security-center-os-coverage.md) (Piattaforme supportate nel Centro sicurezza di Azure).

### <a name="why-doesnt-azure-security-center-recognize-hello-antimalware-solution-running-on-my-azure-vm"></a>Motivo per cui Centro sicurezza di Azure non riconosce i soluzione antimalware hello in esecuzione nella macchina virtuale Azure?
Il Centro sicurezza di Azure dispone di visibilità sull'antimalware installato tramite le estensioni di Azure. Ad esempio, Centro sicurezza PC non è in grado di toodetect antimalware che è stato pre-installato in un'immagine fornita o se è installato antimalware le macchine virtuali tramite i processi (ad esempio i sistemi di Gestione configurazione).

### <a name="why-do-i-get-hello-message-missing-scan-data-for-my-vm"></a>Perché viene visualizzato il messaggio hello "Dati di analisi mancanti" per la macchina virtuale?
Questo messaggio viene visualizzato quando non sono presenti dati di analisi per una macchina virtuale. Dopo aver abilitata la raccolta dei dati nel Centro protezione di Azure può richiedere del tempo (meno di un'ora) per l'analisi dei dati toopopulate. Dopo il popolamento iniziale di hello di dati di analisi, è possibile ricevere questo messaggio perché non sono presenti dati di analisi affatto o non sono presenti dati di analisi di recente. Le analisi non saranno popolate per le macchine virtuali con stato arrestato. Questo messaggio potrebbe essere visualizzato anche se i dati di analisi non sono popolata recente (in base ai criteri di conservazione hello di agente di Windows hello, che ha un valore predefinito di 30 giorni).

### <a name="why-do-i-get-hello-message-vm-agent-is-missing"></a>Perché viene visualizzato il messaggio hello "Agente della macchina virtuale è mancante?"
Hello agente della macchina virtuale deve essere installato in macchine virtuali tooenable la raccolta dei dati. Hello agente VM viene installato per impostazione predefinita per le macchine virtuali distribuite da hello Azure Marketplace. Per informazioni su come tooinstall hello agente di macchine Virtuali in altre macchine virtuali, vedere hello post di blog [agente VM ed estensioni](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/).
