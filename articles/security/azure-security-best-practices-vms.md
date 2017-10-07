---
title: procedure ottimali di protezione macchina virtuale aaaAzure | Documenti Microsoft
description: Questo articolo fornisce un'ampia gamma di protezione ottimali consigliate toobe utilizzati in macchine virtuali in Azure.
services: security
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 5e757abe-16f6-41d5-b1be-e647100036d8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: b03bcc75fde6d49897f9a7f6f15aec87456edd0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-vm-security"></a>Procedure consigliate per la sicurezza delle VM di Azure

Nella maggior parte dei scenari di servizio (IaaS), infrastruttura [macchine virtuali di Azure (VM)](https://docs.microsoft.com/en-us/azure/virtual-machines/) è carico di lavoro principale hello per le organizzazioni che utilizzano cloud computing. Ciò è particolarmente evidente in [scenari ibridi](https://social.technet.microsoft.com/wiki/contents/articles/18120.hybrid-cloud-infrastructure-design-considerations.aspx) in tooslowly di organizzazioni si desidera eseguire la migrazione cloud toohello i carichi di lavoro. In questi scenari, seguire hello [considerazioni generali sulla sicurezza per IaaS](https://social.technet.microsoft.com/wiki/contents/articles/3808.security-considerations-for-infrastructure-as-a-service-iaas.aspx)e applicare security best practices tooall le macchine virtuali.

Questo articolo tratta varie procedure consigliate di sicurezza per le VM derivate da esperienze dei nostri clienti e nostre esperienze dirette con le VM stesse.

Hello procedure consigliate si basano su un consenso parere e lavorare con funzionalità della piattaforma Azure corrente e set di funzionalità. Poiché opinioni e le tecnologie possono cambiare nel tempo, contiamo tooupdate in questo articolo regolarmente tooreflect tali modifiche.

Per ogni procedura consigliata, hello spiegato:

* Quali consigliata hello è.
* Perché è una buona idea tooenable è.
* Come è possibile ottenere informazioni di tooenable è.
* Ciò che accadrebbe se non si riesce tooenable è.
* Alternative possibili toohello consigliata.

articolo Hello esamina hello seguenti procedure ottimali di protezione VM:

* Autenticazione e controllo di accesso della VM
* Disponibilità e accesso alla rete della VM
* Protezione dei dati inattivi nelle VM tramite l'applicazione della crittografia
* Gestire gli aggiornamenti della VM
* Gestire le condizioni di sicurezza della VM
* Monitorare le prestazioni della VM

## <a name="vm-authentication-and-access-control"></a>Autenticazione e controllo di accesso della VM

Hello primo passaggio per proteggere la macchina virtuale è tooensure che solo gli utenti autorizzati siano in grado di tooset di nuove macchine virtuali. È possibile utilizzare [criteri di gestione risorse di Azure](../azure-resource-manager/resource-manager-policy.md) tooestablish convenzioni per le risorse dell'organizzazione, creare criteri personalizzati e applicare tooresources questi criteri, ad esempio [gruppi di risorse](../azure-resource-manager/resource-group-overview.md).

Macchine virtuali che appartengono naturalmente il gruppo di risorse tooa ereditano i criteri. Sebbene questo approccio è consigliato toomanaging VM, è possibile anche i criteri di controllo accesso tooindividual VM utilizzando [il controllo di accesso basato sui ruoli (RBAC)](../active-directory/role-based-access-control-configure.md).

Quando si abilita criteri di gestione risorse e l'accesso VM toocontrol RBAC, consente di migliorare la sicurezza complessiva di macchina virtuale. Si consiglia di consolidare le macchine virtuali con hello del ciclo di vita stesso in hello stesso gruppo di risorse. Usando i gruppi di risorse è possibile distribuire, monitorare ed eseguire il rollup dei costi di fatturazione per le risorse. tooenable utenti tooaccess e configurare le macchine virtuali, utilizzare un [approccio con privilegi minimi](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-ds/plan/security-best-practices/implementing-least-privilege-administrative-models). E quando si assegna privilegi toousers, pianificare hello toouse seguenti ruoli predefiniti di Azure:

- [Macchina virtuale collaboratore](../active-directory/role-based-access-built-in-roles.md#virtual-machine-contributor): può gestire le macchine virtuali, ma non hello virtuale toowhich account di rete o di archiviazione sono connessi.
- [Collaboratore alla macchina virtuale classica](../active-directory/role-based-access-built-in-roles.md#classic-virtual-machine-contributor): può gestire macchine virtuali create utilizzando il modello di distribuzione classica hello, ma non hello virtuale rete o archiviazione account toowhich hello sono connesse le macchine virtuali.
- [Gestore sicurezza](../active-directory/role-based-access-built-in-roles.md#security-manager): può gestire i componenti di sicurezza, i criteri di sicurezza e le VM.
- [Utente DevTest Labs](../active-directory/role-based-access-built-in-roles.md#devtest-labs-user): può visualizzare tutti gli elementi e connettere, avviare, riavviare e arrestare le VM.

Non condividere account e password tra gli amministratori e non riutilizzare le password per più account utente o servizi, in particolare quelle dei social media o di altre attività non amministrative. Idealmente, è consigliabile usare [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) tooset di modelli di macchine virtuali in modo sicuro. Usando questo approccio, è possibile potenziare le scelte di distribuzione e applicare le impostazioni di sicurezza per la distribuzione di hello.

Le organizzazioni che non applicano il controllo di accesso ai dati sfruttando funzionalità come il controllo degli accessi in base al ruolo potrebbero concedere più privilegi del necessario agli utenti. Dati toocertain di accesso utente appropriato direttamente possono compromettere i dati.

## <a name="vm-availability-and-network-access"></a>Disponibilità e accesso alla rete della VM

Se la macchina virtuale esegue applicazioni critiche che richiedono la disponibilità elevata toohave, si consiglia di utilizzare più macchine virtuali. Per una migliore disponibilità, creare almeno due macchine virtuali in hello [set di disponibilità](../virtual-machines/windows/tutorial-availability-sets.md).

[Bilanciamento del carico di Azure](../load-balancer/load-balancer-overview.md) richiede inoltre che macchine virtuali con carico bilanciato appartengono toohello stesso set di disponibilità. Se queste macchine virtuali devono essere accessibile da Internet hello, è necessario configurare un [bilanciamento del carico con connessione Internet](../load-balancer/load-balancer-internet-overview.md).

Quando le macchine virtuali sono esposto toohello Internet, è importante che si [controllo di flusso del traffico di rete con rete sicurezza gruppi](../virtual-network/virtual-networks-nsg.md). Poiché NSGs possono essere applicati toosubnets, è possibile ridurre il numero di hello di NSGs raggruppando le risorse in base alla subnet e quindi l'applicazione NSGs toohello subnet. scopo di Hello è un livello di isolamento rete, che è possibile effettuare correttamente la configurazione di hello toocreate [sicurezza di rete](../best-practices-network-security.md) funzionalità in Azure.

È inoltre possibile utilizzare funzionalità di accesso alla VM (JIT) hello-in-time dal Centro sicurezza di Azure toocontrol che dispone di accesso remoto tooa macchina virtuale specifica e la durata.

Le organizzazioni che non applicano restrizioni di accesso alla rete VM con connessione tooInternet sono esposti a rischi toosecurity, ad esempio un attacco di forza bruta Remote Desktop Protocol (RDP).

## <a name="protect-data-at-rest-in-your-vms-by-enforcing-encryption"></a>Protezione dei dati inattivi nelle VM di Azure tramite l'applicazione della crittografia

[La crittografia dei dati inattivi](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) è un passaggio obbligatorio per assicurare la privacy, la conformità e la sovranità dei dati. [Crittografia disco Azure](../security/azure-security-disk-encryption.md) consente tooencrypt gli amministratori IT Windows e i dischi di macchina virtuale IaaS di Linux. Crittografia disco combina le funzionalità di BitLocker di Windows hello standard del settore e hello Linux dm crypt funzionalità tooprovide crittografia del volume per hello del sistema operativo e i dischi dati hello.

È possibile applicare la crittografia del disco toohelp salvaguardare la toomeet dati i requisiti di sicurezza e conformità dell'organizzazione. L'organizzazione deve considerare usando la crittografia toohelp attenuare i rischi correlati toounauthorized l'accesso ai dati. Si consiglia inoltre di crittografare l'unità prima di scrivere i dati sensibili toothem.

Essere tooencrypt che il tooprotect di volumi di dati macchina virtuale all'indirizzo rest nell'account di archiviazione di Azure. Proteggere le chiavi di crittografia hello e il segreto tramite [insieme credenziali chiavi Azure](https://azure.microsoft.com/en-us/documentation/articles/key-vault-whatis/).

Le organizzazioni che non impongono la crittografia dei dati sono altri problemi di integrità toodata esposto. Ad esempio, gli utenti non autorizzati o non autorizzati potrebbero intercettare i dati negli account compromesso o ottenere l'accesso non autorizzato toodata codificata in ClearFormat. Oltre a portare in tali rischi, toocomply con dei regolamenti del settore, le aziende devono dimostrare che si stanno esercitando molta attenzione e utilizzando la protezione corretta controlla tooenhance la protezione dati.

toolearn ulteriori informazioni su crittografia del disco, vedere [Azure crittografia disco per Windows e le macchine virtuali IaaS Linux](azure-security-disk-encryption.md).


## <a name="manage-your-vm-updates"></a>Gestire gli aggiornamenti della VM

Perché macchine virtuali di Azure, come tutti in locale le macchine virtuali, sono previsti toobe gestita dall'utente, Azure non push toothem gli aggiornamenti di Windows. Tuttavia sono incoraggiati tooleave hello impostazione automatica di Windows Update abilitato. Un'altra opzione consiste toodeploy [Windows Server Update Services (WSUS)](https://technet.microsoft.com/windowsserver/bb332157.aspx) o un altro prodotto di gestione degli aggiornamenti adatto su un'altra macchina virtuale o locale. Sia WSUS che Windows Update mantengono aggiornate le VM. È inoltre consigliabile utilizzare una scansione tooverify prodotto che tutte le macchine virtuali IaaS sono backup toodate.

Le immagini predefinite fornite da Azure sono hello tooinclude regolarmente aggiornata più recente di arrotondamento degli aggiornamenti di Windows. Tuttavia, non è garantito che le immagini di hello saranno aggiornate in fase di distribuzione. Sono possibili leggeri ritardi (di non più di alcune settimane) dopo i rilasci. Cercare e installare tutti gli aggiornamenti di Windows deve essere innanzitutto hello di ogni distribuzione. Questa misura è tooapply particolarmente importante quando si distribuiscono le immagini che derivano dall'utente o la propria libreria. Le immagini sono fornite come parte di hello Azure Marketplace vengono aggiornate automaticamente per impostazione predefinita.

Le organizzazioni che non applicano i criteri di aggiornamento software sono più toothreats esposto che sfruttano le vulnerabilità noto in precedenza predefinite. Oltre ai rischi di tali rischi, toocomply con dei regolamenti del settore, le aziende devono dimostrare che si stanno esercitando molta attenzione e utilizzando toohelp controlli di sicurezza corrette garantire la sicurezza hello del relativo carico di lavoro si trova nel cloud hello.

È importante tooemphasize che le procedure consigliate per Data Center tradizionali di aggiornamento software e IaaS di Azure presentano molte analogie. È pertanto consigliabile valutare il tooinclude macchine virtuali criteri aggiornamento corrente di software.

## <a name="manage-your-vm-security-posture"></a>Gestire le condizioni di sicurezza della VM

Minacce Cyber si evolvono e proteggere le macchine virtuali richiede potente funzionalità di monitoraggio che possono rapidamente rilevare le minacce, impedire l'accesso non autorizzato alle risorse di tooyour, gli avvisi vengono generati e ridurre i falsi positivi. condizioni di sicurezza Hello per un carico di lavoro è costituito da tutti gli aspetti di sicurezza di hello macchina virtuale, da accesso rete toosecure di gestione per l'aggiornamento.

condizioni di sicurezza toomonitor hello del [Windows](../security-center/security-center-virtual-machine.md) e [le macchine virtuali Linux](../security-center/security-center-linux-virtual-machine.md), utilizzare [Centro sicurezza di Azure](../security-center/security-center-intro.md). Nel Centro protezione di Azure, proteggere le macchine virtuali sfruttando hello seguenti funzionalità:

* Applicare le impostazioni di sicurezza del sistema operativo con le regole di configurazione consigliate
* Identificare e scaricare gli aggiornamenti critici e di sicurezza del sistema che potrebbero mancare
* Consigli per la protezione antimalware degli endpoint di distribuzione
* Convalidare la crittografia del disco
* Valutare e correggere le vulnerabilità
* Rilevare le minacce

Il Centro sicurezza può monitorare attivamente le minacce e le minacce potenziali sono esposte in **Avvisi sicurezza**. Le minacce correlate sono aggregate in un'unica visualizzazione denominata **Evento imprevisto della sicurezza**.

toounderstand come centro di sicurezza consentono di identificare le potenziali minacce in macchine virtuali all'interno di Azure, guardare hello video seguente:

<iframe src="https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Security-Center-in-Incident-Response/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

Le organizzazioni che non applicano una condizione di protezione elevata per le proprie macchine virtuali continuino di potenziali tentativi dai controlli di sicurezza stabilito toocircumvent utenti non autorizzati.

## <a name="monitor-vm-performance"></a>Monitorare le prestazioni della VM

L'uso improprio delle risorse può essere un problema quando i processi della VM utilizzano più risorse di quanto dovrebbero. Problemi di prestazioni con una macchina virtuale possono provocare interruzioni tooservice, che viola il principio di sicurezza hello di disponibilità. Per questo motivo, è accesso VM toomonitor imperativo non solo obbligatoriamente, mentre si sta verificando un problema, ma anche in modo proattivo, rispetto alle prestazioni di base come misurati durante il normale funzionamento.

Analizzando [i file di log di diagnostica di Azure](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/), è possibile monitorare le risorse della VM e identificare i potenziali problemi che potrebbero compromettere le prestazioni e la disponibilità. Hello estensione diagnostica di Azure fornisce funzionalità di monitoraggio e diagnostica nelle macchine virtuali basate su Windows. È possibile abilitare queste funzionalità, includendo l'estensione hello come parte di hello [modello di Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md).

È inoltre possibile utilizzare [Monitor Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) toogain visibilità dello stato della risorsa.

Le organizzazioni che non eseguono il monitoraggio delle prestazioni delle macchine Virtuali sono toodetermine non è possibile sia determinate modifiche nei modelli di prestazioni normali o anomali. Se hello VM che utilizza più risorse rispetto al normale, un'anomalia di questo tipo potrebbe indicare un potenziale attacco da una risorsa esterna o compromesso in esecuzione un processo in hello macchina virtuale.
