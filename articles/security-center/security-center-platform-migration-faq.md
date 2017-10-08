---
title: domande frequenti sulla migrazione di piattaforma aaaSecurity Center | Documenti Microsoft
description: Questo risposte alle domande su hello migrazione della piattaforma Centro protezione di Azure.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4d1364cd-7847-425a-bb3a-722cb0779f78
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: terrylan
ms.openlocfilehash: fcb14ae83167ef79a60371e4fcb625cf99bee6c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="security-center-platform-migration-faq"></a>Domande frequenti sulla migrazione della piattaforma del Centro sicurezza
A giugno 2017 anticipata, Centro sicurezza di Azure iniziato a utilizzare toocollect e l'archivio dati di Microsoft Monitoring Agent di hello. vedere, più toolearn [migrazione della piattaforma Azure sicurezza Center](security-center-platform-migration.md). Questo risposte alle domande sulla migrazione di piattaforma hello.

## <a name="data-collection-agents-and-workspaces"></a>Raccolta di dati, agenti e aree di lavoro

### <a name="how-is-data-collected"></a>In che modo vengono raccolti i dati?
Centro sicurezza PC utilizza dati di hello Microsoft Monitoring Agent toocollect protezione dalle macchine virtuali. Hello protezione dati includono informazioni sulle configurazioni di sicurezza, che sono utilizzati tooidentify vulnerabilità, e gli eventi di sicurezza sono utilizzati toodetect minacce. Dati raccolti dall'agente hello viene archiviati in un toohello di area di lavoro collegato Log Analitica VM esistente o in una nuova area di lavoro creati dal Centro sicurezza PC. Quando il centro di sicurezza crea una nuova area di lavoro, hello geolocation di hello VM viene preso in considerazione.

> [!NOTE]
> Microsoft Monitoring Agent Hello è hello stesso agente usato da hello Operations Management Suite (OMS), il servizio Registro Analitica e System Center Operations Manager (SCOM).
>
>

Quando la raccolta dei dati è abilitata per hello prima volta o quando vengono eseguita la migrazione delle sottoscrizioni, il Centro sicurezza PC controlla toosee se hello Microsoft Monitoring Agent è già installato come un'estensione di Azure su tutte le macchine virtuali. Se non è installato Microsoft Monitoring Agent hello, quindi verranno Centro sicurezza:

- installare Microsoft Monitoring agent di hello in hello VM
   - Se un'area di lavoro creato dal Centro protezione già esiste in hello geolocation stesso come macchina virtuale, hello hello agent viene connesso toothis dell'area di lavoro
   - Se un'area di lavoro non esiste, Centro sicurezza PC crea un nuovo gruppo di risorse predefinito dell'area di lavoro in tale posizione geografica e la connessione dell'area di lavoro di hello agente toothat. convenzione di denominazione per il gruppo di risorse e dell'area di lavoro hello Hello sono:

       Area di lavoro: DefaultWorkspace-[subscription-ID]-[geo]

       Gruppo di risorse: DefaultResouceGroup-[geo]
- installare una soluzione di centro di sicurezza nell'area di lavoro hello

percorso di Hello dell'area di lavoro hello è basato sulla posizione hello di hello macchina virtuale. vedere, più toolearn [la protezione dei dati](security-center-data-security.md).

> [!NOTE]
> Migrazione tooplatform precedente, il Centro sicurezza PC raccolte dati di protezione dalle macchine virtuali utilizzando hello Azure Monitoring Agent e sono stati memorizzati nell'account di archiviazione. Dopo la migrazione di piattaforma hello, centro di sicurezza Usa hello Microsoft Monitoring Agent e archivio e dell'area di lavoro toocollect hello stessi dati. account di archiviazione Hello può essere rimossa dopo la migrazione di hello.
>
>

### <a name="am-i-billed-for-log-analytics-or-oms-on-hello-workspaces-created-by-security-center"></a>Viene addebitato il costo per Log Analitica o OMS in aree di lavoro hello create dal centro di sicurezza?
No. Le aree di lavoro create dal Centro sicurezza non comportano addebiti di OMS, benché siano configurate per OMS per la fatturazione per nodo. Fatturazione Centro sicurezza PC è sempre basata sul Centro sicurezza PC hello e criteri di soluzioni di protezione installate in un'area di lavoro:

- **Livello gratuito** -Centro sicurezza PC installa soluzione 'SecurityCenterFree' hello nell'area di lavoro predefinito hello. La fatturazione per il livello gratuito hello.
- **Livello standard** : Centro sicurezza PC installa hello 'SecurityCenterFree' e soluzioni 'Security' su hello area di lavoro predefinita.

Per altre informazioni sui prezzi, vedere [Prezzi di Centro sicurezza](https://azure.microsoft.com/pricing/details/security-center/). Hello prezzi indirizzi della pagina Modifica toosecurity archiviazione dei dati e ripartito fatturazione a partire da giugno 2017.

> [!NOTE]
> Hello OMS piano tariffario di aree di lavoro creati dal Centro sicurezza PC non influisce sulla fatturazione Centro sicurezza PC.
>
>

### <a name="can-i-delete-hello-default-workspaces-created-by-security-center"></a>È possibile eliminare le aree di lavoro di hello predefinito creati dal centro di sicurezza?
**L'area di lavoro predefinita hello di eliminazione non è consigliata.** Centro sicurezza PC utilizza dati hello predefiniti aree di lavoro toostore protezione dalle macchine virtuali.  Se si elimina un'area di lavoro, il Centro sicurezza PC è Impossibile toocollect questi dati e alcune raccomandazioni sulla sicurezza e gli avvisi non sono disponibili

toorecover, hello rimuovere Microsoft Monitoring Agent nell'area di lavoro collegati toohello eliminato hello macchine virtuali. Centro sicurezza PC consente di reinstallare agente hello e crea nuove aree di lavoro predefinito.

### <a name="what-if-hello-microsoft-monitoring-agent-was-already-installed-as-an-extension-on-hello-vm"></a>Cosa accade se hello Microsoft Monitoring Agent è già stato installato come estensione nelle VM hello?
Centro sicurezza PC non esegue l'override di aree di lavoro toouser con le connessioni esistenti. Centro sicurezza PC archivia i dati di protezione da macchine Virtuali nell'area di lavoro hello hello è già connesso.

### <a name="what-if-i-had-a-microsoft-monitoring-agent-installed-on-hello-machine-but-not-as-an-extension"></a>Cosa accade se ha un agente di monitoraggio di Microsoft installato sul computer hello ma non come un'estensione?
Se hello Microsoft Monitoring Agent è installato direttamente in hello VM (non come un'estensione di Azure), il Centro sicurezza PC non installerà hello Microsoft Monitoring Agent e il monitoraggio della protezione sarà limitato.

### <a name="what-is-hello-impact-of-removing-these-extensions"></a>Qual è hello impatto della rimozione di queste estensioni?
Se si rimuove l'estensione Microsoft Monitoring hello, Centro sicurezza PC non è di tipo dati di sicurezza in grado di toocollect da hello VM e alcuni consigli sulla sicurezza e gli avvisi non sono disponibili. Entro 24 ore, il Centro sicurezza PC determina che hello VM manca estensione hello e reinstalla hello estensione.

### <a name="how-do-i-stop-hello-automatic-agent-installation-and-workspace-creation"></a>Come interrompere l'installazione dell'agente automatico hello e la creazione dell'area di lavoro?
È possibile disattivare la raccolta dei dati per le sottoscrizioni nei criteri di sicurezza hello ma questa operazione è sconsigliata. La disattivazione della raccolta di dati limita le raccomandazioni e gli avvisi del Centro sicurezza. Raccolta dati è obbligatorio per le sottoscrizioni nel piano tariffario Standard hello. raccolta dei dati toodisable:

1. Se la sottoscrizione è configurata per il livello Standard hello, aprire hello i criteri di protezione per la sottoscrizione e selezionare hello **libero** livello.

   ![Piano tariffario ][1]

2. Successivamente, disattivare la raccolta di dati selezionando **Off** su hello **criteri di sicurezza: la raccolta dei dati** blade.

   ![Raccolta dei dati][2]

### <a name="how-do-i-remove-oms-extensions-installed-by-security-center"></a>Come si rimuovono le estensioni di OMS installate dal Centro sicurezza?
È possibile rimuovere manualmente hello Microsoft Monitoring Agent. Questa operazione non è consigliata perché limita le raccomandazioni e gli avvisi del Centro sicurezza.

> [!NOTE]
> Se la raccolta dei dati è abilitata, il Centro sicurezza PC reinstallerà agente hello dopo averlo rimosso.  È necessario toodisable di raccolta dati prima di rimuovere manualmente l'agente di hello. Vedere [come evitare la creazione di area di lavoro e l'installazione automatica di agenti hello?](#how-do-i-stop-the-automatic-agent-installation-and-workspace-creation?) per istruzioni su come disabilitare la raccolta dei dati.
>
>

toomanually rimuovere agente hello:

1.  Nel portale di hello aprire **Analitica Log**.
2.  Nel pannello Log Analitica hello, selezionare un'area di lavoro:
3.  Selezionare ogni macchina virtuale che non desiderati toomonitor e selezionare **Disconnect**.

   ![Rimuovere l'agente di hello][3]

> [!NOTE]
> Se una VM Linux dispone già di un agente OMS non di estensione, la rimozione di estensione hello comporta anche l'agente hello e cliente hello tooreinstall è.
>
>

## <a name="existing-oms-customers"></a>Clienti di OMS esistenti

### <a name="does-security-center-override-any-existing-connections-between-vms-and-workspaces"></a>Il Centro sicurezza esegue l'override di eventuali connessioni esistenti tra le macchine virtuali e le aree di lavoro?
Se una macchina virtuale già hello Microsoft Monitoring Agent installato come un'estensione di Azure, il Centro sicurezza PC non esegue l'override connessione hello all'area di lavoro esistente. Centro sicurezza PC utilizza invece l'area di lavoro esistente hello.

Una soluzione di Centro sicurezza PC è installato nell'area di lavoro hello se non già presente e soluzione hello è applicato toohello solo le macchine virtuali pertinenti. Quando si aggiunge una soluzione, viene distribuito automaticamente da tooall Windows e Linux gli agenti connessi tooyour Log Analitica area di lavoro predefinita. [Soluzione Targeting](../operations-management-suite/operations-management-suite-solution-targeting.md), che è una funzionalità OMS, consente un ambito tooapply tooyour soluzioni.

Se hello Microsoft Monitoring Agent è installato direttamente in hello VM (non come un'estensione di Azure), il Centro sicurezza PC non installerà hello Microsoft Monitoring Agent e il monitoraggio della protezione è limitato.

### <a name="what-should-i-do-if-i-suspect-that-hello-data-platform-migration-broke-hello-connection-between-one-of-my-vms-and-my-workspace"></a>Cosa fare se si sospetta che la migrazione di piattaforma dati hello annullino connessione hello tra una delle macchine virtuali e l'area di lavoro?
Questo problema non si dovrebbe verificare. Se verificano, quindi [creare una richiesta di supporto tecnico di Azure](../azure-supportability/how-to-create-azure-support-request.md) e includono i seguenti dettagli hello:

- ID di risorsa di Azure Hello di hello interessati VM
- ID di risorsa di Azure Hello dell'area di lavoro hello configurato sull'estensione hello prima hello connessione è stata interrotta
- agente Hello e la versione installata in precedenza

### <a name="does-security-center-install-solutions-on-my-existing-oms-workspaces-what-are-hello-billing-implications"></a>Il Centro sicurezza installa soluzioni nelle aree di lavoro di OMS esistenti? Quali sono i costi di fatturazione hello?
Quando il Centro sicurezza PC identifica una macchina virtuale è già connesso tooa dell'area di lavoro che è stato creato, il Centro sicurezza PC consente alle soluzioni in questa area di lavoro in base a livello di prezzo tooyour. Hello soluzioni viene applicato toohello solo macchine virtuali di Azure pertinenti, tramite [soluzione destinazione](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting), pertanto rimane fatturazione hello hello stesso.

- **Livello gratuito** -Centro sicurezza PC installa soluzione 'SecurityCenterFree' hello nell'area di lavoro hello. La fatturazione per il livello gratuito hello.
- **Livello standard** : Centro sicurezza PC installa hello 'SecurityCenterFree' e soluzioni 'Security' su hello dell'area di lavoro.

   ![Soluzioni nell'area di lavoro predefinita][4]

> [!NOTE]
> soluzione 'Security' in Log Analitica Hello è hello sicurezza & soluzione di controllo in OMS.
>
>

### <a name="i-already-have-workspaces-in-my-environment-can-i-use-them-toocollect-security-data"></a>Si dispone già di aree di lavoro nell'ambiente, è possibile utilizzare tali dati di protezione toocollect?
Se una macchina virtuale già hello Microsoft Monitoring Agent installato come un'estensione di Azure, il Centro sicurezza PC utilizza hello connesso area di lavoro esistente. Una soluzione di Centro sicurezza PC è installato nell'area di lavoro hello se non già presente e soluzione hello è applicato toohello solo macchine virtuali pertinenti tramite [soluzione destinazione](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solution-targeting).

Centro sicurezza PC installa Microsoft Monitoring Agent hello in macchine virtuali, Usa hello aree di lavoro predefinito creato dal Centro sicurezza PC. Non appena i clienti saranno in grado di tooconfigure vengono utilizzate le aree di lavoro.

### <a name="i-already-have-security-solution-on-my-workspaces-what-are-hello-billing-implications"></a>Nelle aree di lavoro è già presente una soluzione di sicurezza. Quali sono i costi di fatturazione hello?
soluzione di sicurezza e controllo Hello è tooenable utilizzate funzionalità di livello Standard di centro di sicurezza per le macchine virtuali di Azure. Se soluzione di sicurezza e controllo hello è già installato in un'area di lavoro, il Centro sicurezza PC utilizza soluzione esistente hello. La fatturazione rimane invariata.

## <a name="next-steps"></a>Passaggi successivi
toolearn informazioni sulla migrazione della piattaforma hello Centro sicurezza PC, vedere

- [Migrazione della piattaforma del Centro sicurezza di Azure](security-center-platform-migration.md)
- [Guida alla risoluzione dei problemi del Centro sicurezza di Azure](security-center-troubleshooting-guide.md)

<!--Image references-->
[1]: ./media/security-center-platform-migration-faq/pricing-tier.png
[2]: ./media/security-center-platform-migration-faq/data-collection.png
[3]: ./media/security-center-platform-migration-faq/remove-the-agent.png
[4]: ./media/security-center-platform-migration-faq/solutions.png
