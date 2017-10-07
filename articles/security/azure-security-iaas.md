---
title: aaaSecurity best practices per IaaS carichi di lavoro in Azure | Documenti Microsoft
description: " migrazione di Hello di carichi di lavoro tooAzure IaaS porta tooreevaluate opportunità del Design "
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 02c5b7d2-a77f-4e7f-9a1e-40247c57e7e2
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: barclayn
ms.openlocfilehash: 9cee1ca6effe9561e51dc8b945e7388ffea169b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="security-best-practices-for-iaas-workloads-in-azure"></a>Procedure consigliate per la sicurezza dei carichi di lavoro IaaS in Azure

Come concetto sull'infrastruttura di tooAzure lo spostamento dei carichi di lavoro è stato avviato come servizio (IaaS), probabilmente realizzare che alcune considerazioni familiarità. protezione degli ambienti virtuali. Quando si sposta tooAzure IaaS, è possibile applicare l'esperienza per proteggere gli ambienti virtuali e utilizzare un nuovo set di opzioni toohelp sicuro le risorse.

Per iniziare, indicante che dovremmo non Prevediamo toobring risorse locali come tooAzure uno a uno. nuove sfide Hello hello nuove opzioni e portare tooreevaluate opportunità esistente deigns, strumenti e processi.

Responsabilità per la sicurezza è basata sul tipo hello del servizio cloud. Hello grafico seguente viene riepilogato il saldo di hello di responsabilità di Microsoft e si:


![Aree di responsabilità](./media/azure-security-iaas/sec-cloudstack-new.png)


Parleremo alcune delle opzioni di hello disponibili in Azure che consentono di soddisfare i requisiti di sicurezza dell'organizzazione. I requisiti di sicurezza possono variare in base al tipo di carico di lavoro. Nessuna di queste procedure consigliate è di per sé sufficiente a proteggere i sistemi. Come qualsiasi altro elemento nella sicurezza, aver toochoose le opzioni appropriate hello e vedere come soluzioni hello possano complementari con l'inserimento di spazi vuoti.

## <a name="use-privileged-access-workstations"></a>Usare workstation con accesso con privilegi

Le organizzazioni spesso rientrano sfruttano toocyberattacks perché gli amministratori di eseguono azioni durante l'utilizzo di account con diritti elevati. Questo avviene di solito in modo non intenzionale, ma perché la configurazione e i processi esistenti lo consentono. La maggior parte degli utenti comprende il rischio di hello delle azioni seguenti da un punto di vista concettuale, ma comunque scegliere toodo li.

In questo esempio, di controllo della posta elettronica e l'esplorazione Internet hello sembra abbastanza innocuo. Ma che potrebbero espongono toocompromise account con privilegi elevati da dannoso attori che possono usare le attività di esplorazione, appositamente messaggi di posta elettronica o altri tooyour enterprise di tecniche toogain accesso. È consigliabile utilizzare hello delle workstation di gestione della protezione per l'esecuzione di tutte le attività di amministrazione di Azure, in modo compromesso tooaccidental l'esposizione di riduzione.

Per le attività sensibili, le workstation con accesso con privilegi offrono un sistema operativo dedicato, protetto dagli attacchi provenienti da Internet e dai vettori di minacce. Separazione di queste attività sensibili e gli account da hello utilizzo giornaliero workstation e dispositivi offre protezione avanzata da attacchi di phishing, applicazione e le vulnerabilità del sistema operativo, diversi attacchi di rappresentazione e attacchi con furto di credenziali come tasto di scelta rapida registrazione e Pass-the-Hash, Pass-the-Ticket.

Hello PAW approccio è un'estensione di hello ben definito e consiglia toouse pratica di un account amministrativo singolarmente assegnato separato da un account utente standard. Una workstation dotata di accesso con privilegi offre un ambiente affidabile per gli account sensibili.

Per altre informazioni e istruzioni sull'implementazione, vedere [Workstation con accesso con privilegi](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/privileged-access-workstations).

## <a name="use-multi-factor-authentication"></a>Usare Multi-Factor Authentication

Hello precedente, il perimetro della rete è stato utilizzato toocontrol accesso toocorporate dati. In un ambiente cloud-first, prima di dispositivi mobili, l'identità è il piano di controllo hello: si utilizzano servizi di tooIaaS toocontrol accesso da qualsiasi dispositivo. Inoltre utilizzarla tooget visibilità e comprendere dove e come i dati vengono utilizzati. La protezione dell'identità digitale hello degli utenti di Azure è fondamenta hello di proteggere le sottoscrizioni di furto di identità e altri cybercrimes.

Uno dei passaggi di hello più utili che è possibile eseguire toosecure un account è tooenable autenticazione a due fattori. L'autenticazione a due fattori è un modo per l'autenticazione mediante un elemento password tooa aggiunta. Consente di ridurre il rischio di hello di accesso da un utente che gestisce tooget password di un altro utente.

[Azure multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) consente di proteggere toodata di accesso e le applicazioni rispettando richiesta dell'utente per un semplice processo. Offre un'autenticazione avanzata con una gamma di semplici opzioni di verifica, ad esempio una telefonata, un SMS o una notifica dell'app per dispositivi mobili. Gli utenti di scegliere il metodo hello che preferiscono.

toouse modo più semplice di Hello multi-Factor Authentication è hello Microsoft Authenticator app per dispositivi mobili che può essere usato nei dispositivi mobili che eseguono Windows, iOS e Android. Con la versione più recente di hello di integrazione di hello di locale di Active Directory con Azure Active Directory (Azure AD) e Windows 10 [Windows Hello for Business](../active-directory/active-directory-azureadjoin-passport-deployment.md) può essere usato per le risorse trasparente single sign-on tooAzure. In questo caso, il dispositivo Windows 10 hello viene utilizzato come secondo fattore di hello per l'autenticazione.

Per gli account che gestiscono la sottoscrizione di Azure e per gli account che possono accedere toovirtual macchine, utilizzo multi-Factor Authentication fornisce un altro livello di protezione maggiore rispetto all'utilizzo solo di una password. Altre forme di autenticazione a due fattori possono essere altrettanto efficaci, ma più complesse da distribuire se non sono già nell'ambiente di produzione.

Hello schermata seguente mostra alcune delle opzioni di hello disponibili per Azure multi-Factor Authentication:

![Opzioni di Multi-Factor Authentication](./media/azure-security-iaas/mfa-options.png)

## <a name="limit-and-constrain-administrative-access"></a>Limitare e vincolare l'accesso amministrativo

Proteggere gli account di hello in grado di gestire la sottoscrizione di Azure è estremamente importante. compromissione Hello di uno di questi account Nega valore hello hello tutti gli altri passaggi che è possibile adottare tooensure hello riservatezza e integrità dei dati. Di recente come illustrato hello [Edward Snowden](https://en.wikipedia.org/wiki/Edward_Snowden) perdita delle informazioni classificate, attacchi interni comportare toohello un rischio elevato sicurezza complessiva di qualsiasi organizzazione.

Valutare i singoli utenti i diritti amministrativi per toothese simile a criteri seguenti:

- Eseguono attività che richiedono privilegi amministrativi?
- La frequenza con cui vengono eseguite attività hello?
- Esiste un motivo specifico perché un altro amministratore per conto del cliente non è possibile eseguire operazioni di hello?

Documentare tutti gli altri privilegi di hello toogranting noti agli approcci alternativi e ogni non è accettabile.

uso di Hello di amministrazione-in-time impedisce esistenza inutili hello degli account con diritti elevati durante i periodi di quando non sono necessari i diritti. Gli account hanno diritti elevati per un periodo di tempo limitato, per permettere agli amministratori di svolgere il proprio lavoro. Quindi, tali diritti vengono rimossi alla fine di hello di uno spostamento o quando un'attività viene completata.

È possibile utilizzare [Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-configure.md) toomanage, monitoraggio e controllo degli accessi nell'organizzazione. Consente di restare informati hello eseguire azioni di singoli utenti dell'organizzazione. Comporta anche amministrazione just-in-time tooAzure AD introducendo il concetto di hello del gruppo amministratori idonei. Questi sono persone che gli account con toobe potenziali hello dispongono dei diritti di amministrazione. Gli utenti di questo tipo possono essere sottoposti a un processo di attivazione e vedersi concedere diritti amministrativi per un periodo di tempo limitato.


## <a name="use-devtest-labs"></a>Usare DevTest Labs

Uso di Azure per esercitazioni pratiche e di ambienti di sviluppo offre la flessibilità di toogain organizzazioni nello sviluppo e test da ritardi di stoccaggio hello tenendo introdotte approvvigionamento di hardware. Sfortunatamente, una mancanza di una certa familiarità con Azure o un toohelp desiderio accelerare l'adozione potrebbe causare hello amministratore toobe eccessivamente permissivo con assegnazione di diritti. Questo rischio potrebbe accidentalmente esporre hello organizzazione toointernal attacchi. perché alcuni utenti potrebbero vedersi concedere un accesso molto più avanzato del necessario.

Hello [Azure DevTest Labs](../devtest-lab/devtest-lab-overview.md) utilizzata dal servizio [gestire il controllo di accesso](../active-directory/role-based-access-control-what-is.md) (RBAC). Utilizzando RBAC, è possibile separare compiti all'interno del team in ruoli che concedono solo livello di hello di accesso necessaria per gli utenti toodo i processi. Il controllo degli accessi in base al ruolo prevede i ruoli predefiniti di proprietario, utente lab e collaboratore, È possibile utilizzare anche i partner di tooexternal questi ruoli tooassign diritti e semplificare notevolmente la collaborazione.

Poiché DevTest Labs utilizza RBAC, è possibile toocreate aggiuntive, [ruoli personalizzati](../devtest-lab/devtest-lab-grant-user-permissions-to-specific-lab-policies.md). DevTest Labs non solo semplifica la gestione di hello di autorizzazioni, semplifica il processo di hello di recupero eseguito il provisioning di ambienti. e permette di gestire altre problematiche tipiche dei team che operano in ambienti di sviluppo e test. Richiede alcune attività di preparazione, ma hello a lungo termine, per facilitare le cose per il team.

Le funzionalità di Azure DevTest Labs includono:

- Opzioni di controllo amministrativo su hello toousers disponibili. messaggio per l'amministratore può gestire centralmente elementi quali dimensioni delle macchine Virtuali consentite, il numero massimo di macchine virtuali e macchine virtuali vengono avviate e di arresto.
- Automazione della creazione dell'ambiente lab.
- Verifica dei costi.
- Distribuzione semplificata di macchine virtuali per attività di collaborazione temporanee.
- Self-Service che consente di laboratorio gli utenti tooprovision tramite modelli.
- Gestione e limitazione dell'utilizzo.

![Utilizzo di DevTest Labs toocreate un lab](./media/azure-security-iaas/devtestlabs.png)

Senza alcun costo aggiuntivo non è associata a utilizzo hello di DevTest Labs. creazione di Hello di labs, criteri, i modelli e gli elementi è disponibile. Si pagano per hello solo le risorse di Azure utilizzate nei propri laboratori, ad esempio macchine virtuali, gli account di archiviazione e reti virtuali.



## <a name="control-and-limit-endpoint-access"></a>Controllare e limitare l'accesso agli endpoint

Hosting labs o sistemi di produzione in Azure significa che i sistemi necessitano toobe accessibile da Internet hello. Per impostazione predefinita, una nuova macchina virtuale di Windows è la porta RDP hello accessibile da Internet hello e una macchina virtuale Linux aperto porta SSH hello. Eseguire operazioni toolimit esposti endpoint è rischio hello toominimize necessarie di accesso non autorizzato.

Tecnologie di Azure consentono di limitare l'endpoint di amministrazione di hello accesso toothose. Ad esempio, è possibile usare i [gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md). Quando si usa Gestione risorse di Azure per la distribuzione, NSGs limitare l'accesso di hello da tutte le reti toojust hello Gestione endpoint (RDP o SSH). Gli NSG sono un po' l'equivalente degli ACL dei router. È possibile utilizzare le comunicazioni di rete tootightly controllo hello tra i vari segmenti della rete di Azure. Ciò è simile toocreating le reti in reti perimetrali o altre reti isolate. Non controllano il traffico di hello, ma sono utili con la segmentazione della rete.


In Azure è possibile configurare una [VPN da sito a sito](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) dalla rete locale. Una VPN site-to-site estende locale cloud toohello di rete. In questo modo è un'altra possibilità toouse NSGs, perché è inoltre possibile modificare hello NSGs toonot consentire l'accesso da un punto qualsiasi rete locale hello. È quindi possibile richiedere che l'amministrazione viene eseguita dal primo toohello connessione rete di Azure tramite VPN.

opzione di Hello site-to-site VPN potrebbe essere molto interessante nei casi in cui si ospitano sistemi di produzione che sono strettamente integrati con le risorse locali in Azure.

In alternativa, è possibile utilizzare hello [point-to-site](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md) opzione nelle situazioni in cui si desidera toomanage sistemi che non è necessario accedere alle risorse di tooon locale. e che possono essere isolati nella relativa rete virtuale di Azure. Gli amministratori possono VPN in hello Azure ospitati ambiente dalla propria workstation amministrative.

>[!NOTE]
>È possibile utilizzare entrambi hello tooreconfigure di opzione VPN che elenchi ACL hello NSGs toonot consentire accesso toomanagement endpoint da hello Internet.

Un'altra opzione che vale la pena considerare è la distribuzione di un [Gateway Desktop remoto](../multi-factor-authentication/multi-factor-authentication-get-started-server-rdg.md), È possibile utilizzare questa distribuzione toosecurely collegare i server Desktop tooRemote su HTTPS, mentre l'applicazione più dettagliate controlla toothose connessioni.

Funzionalità che si avrebbero accesso tooinclude:

- Amministratore opzioni toolimit toorequests di connessioni da sistemi specifici.
- Autenticazione tramite smart card o Azure Multi-Factor Authentication.
- Controllo su quali sistemi un utente può toovia hello gateway di connessione.
- Possibilità di controllare il reindirizzamento a dischi e dispositivi

## <a name="use-a-key-management-solution"></a>Usare una soluzione di gestione delle chiavi

Gestione delle chiavi protetta è essenziale tooprotecting dati nel cloud hello. Con l'[insieme di credenziali delle chiavi di Azure](../key-vault/key-vault-whatis.md), è possibile archiviare in tutta sicurezza le chiavi di crittografia e altri dati segreti, come le password, all'interno di moduli di protezione hardware. Per una maggiore sicurezza, è possibile importare o generare le chiavi in moduli di protezione hardware.

Microsoft elabora le chiavi in moduli di protezione hardware FIPS 140-2 di livello 2 convalidati (hardware e firmware). È possibile monitorare e controllare l'uso delle chiavi con la registrazione di Azure, inviando i log ad Azure o alla propria soluzione SIEM (Security Information and Event Management) per ulteriori analisi e rilevamento delle minacce.

Chiunque abbia una sottoscrizione di Azure può creare e usare insiemi di credenziali delle chiavi. Anche se rappresenta un vantaggio per sviluppatori e amministratori della sicurezza, Key Vault può essere implementato e gestito da un amministratore responsabile della gestione dei servizi di Azure per un'organizzazione.


## <a name="encrypt-virtual-disks-and-disk-storage"></a>Crittografare i dischi virtuali e l'archiviazione su disco

[Crittografia disco Azure](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0) indirizzi hello rischio di esposizione dall'accesso non autorizzato che è possibile ottenere mediante lo spostamento di un disco o il furto di dati. disco Hello può essere collegato tooanother sistema come modalità di esclusione di altri controlli di sicurezza. Usa la crittografia del disco [BitLocker](https://technet.microsoft.com/library/hh831713) in Windows e di data mining-Crypt tooencrypt Linux del sistema operativo e unità dati. Crittografia disco Azure si integra con l'insieme di credenziali chiave toocontrol e gestire chiavi di crittografia hello. È disponibile per le macchine virtuali Standard e le macchine virtuali con Archiviazione Premium.

Per altre informazioni, vedere [Crittografia dischi di Azure per macchine virtuali IaaS Windows e Linux](azure-security-disk-encryption.md).

La [crittografia del servizio di archiviazione di Azure](../storage/common/storage-service-encryption.md) permette di protegge i dati inattivi. È abilitata a livello di account di archiviazione hello. e permette di crittografare i dati man mano che vengono scritti nel data center, per poi decrittografarli automaticamente quando vi si accede. Supporta hello seguenti scenari:

- Crittografia di BLOB in blocchi, BLOB di aggiunta e BLOB di pagine.
- La crittografia dei dischi rigidi virtuali e i modelli archiviati portato tooAzure locale
- Crittografia del sistema operativo sottostante e dei dischi dati per macchine virtuali IaaS create usando i dischi rigidi virtuali.

Prima di procedere con la crittografia del servizio di archiviazione di Azure, occorre tenere presenti due limitazioni:

- non è disponibile per gli account di archiviazione classici;
- permette di crittografare solo i dati scritti dopo aver abilitato la crittografia.

## <a name="use-a-centralized-security-management-system"></a>Usare un sistema di gestione della sicurezza centralizzato

I server devono toobe monitorati per l'applicazione di patch, configurazione, eventi e le attività che potrebbero essere considerate problemi di sicurezza. tooaddress tali problemi, è possibile utilizzare [Centro sicurezza PC](https://azure.microsoft.com/services/security-center/) e [Operations Management Suite Security and Compliance](https://azure.microsoft.com/services/security-center/). Entrambe queste opzioni vanno oltre la configurazione del sistema operativo hello hello. Oltre a fornire il monitoraggio della configurazione di hello di hello infrastruttura, come ad esempio la configurazione di rete e l'utilizzo dell'appliance virtuale sottostante.

## <a name="manage-operating-systems"></a>Gestire i sistemi operativi

In una distribuzione IaaS, si è ancora responsabile della gestione hello dei sistemi di hello distribuiti, proprio come qualsiasi altro server o workstation nell'ambiente in uso. L'applicazione di patch, la protezione avanzata, diritti e qualsiasi altra attività correlate toohello manutenzione del sistema sono ancora responsabilità dell'utente. Per i sistemi che sono strettamente integrati con le risorse locali, è possibile toouse hello gli stessi strumenti e procedure che si usi locale per elementi come i virus, antimalware, l'applicazione di patch e backup.

### <a name="harden-systems"></a>Implementare la protezione avanzata dei sistemi
Tutte le macchine virtuali in Azure IaaS devono essere protette in modo che espongono solo gli endpoint di servizio necessari per le applicazioni installate hello. Per le macchine virtuali Windows, seguire le indicazioni hello pubblicati da Microsoft come linee di base per hello [Security Compliance Manager](https://technet.microsoft.com/solutionaccelerators/cc835245.aspx) soluzione.

Security Compliance Manager è uno strumento gratuito È possibile utilizzare tooquickly configurare e gestire il desktop, tradizionale dei Data Center e cloud pubblici e privati con System Center Configuration Manager e criteri di gruppo.

Security Compliance Manager offre criteri pronti per la distribuzione e pacchetti di configurazione di Gestione configurazione desiderata già testati. Queste baseline si basano sulle [linee guida Microsoft sulla sicurezza](https://technet.microsoft.com/en-us/library/cc184906.aspx) e le procedure consigliate del settore e permettono di gestire eventuali deviazioni della configurazione, rispondere ai requisiti di conformità e ridurre le minacce per la sicurezza.

È possibile utilizzare configurazione corrente di hello tooimport Security Compliance Manager i computer utilizzando due metodi diversi. Il primo consiste nell'importare criteri di gruppo basati su Active Directory. In secondo luogo, è possibile importare la configurazione hello di "master finale" computer di riferimento utilizzando hello [LocalGPO strumento](https://blogs.technet.microsoft.com/secguide/2016/01/21/lgpo-exe-local-group-policy-object-utility-v1-0/) tooback hello locale i criteri di gruppo. È quindi possibile importare i criteri di gruppo locali hello in Security Compliance Manager.

Confrontare le norme tooindustry procedure consigliate, personalizzare e creare nuovi criteri e Desired Configuration Management Pack di configurazione. Le linee di base sono state pubblicate per tutti i sistemi operativi supportati, tra cui l'Aggiornamento dell'anniversario di Windows 10 e Windows Server 2016.


### <a name="install-and-manage-antimalware"></a>Installare e gestire l'antimalware

Per gli ambienti ospitati separatamente dall'ambiente di produzione, è possibile utilizzare un toohelp estensione antimalware proteggere le macchine virtuali e i servizi cloud. che si integra con il [Centro sicurezza di Azure](../security-center/security-center-intro.md).


[Microsoft Antimalware](azure-security-antimalware.md) include caratteristiche come la protezione in tempo reale, l'analisi pianificata, il monitoraggio e aggiornamento malware, l'aggiornamento delle firme e del motore, il reporting di campioni, la raccolta degli eventi di esclusione e il [supporto della PowerShell](https://msdn.microsoft.com/library/dn771715.aspx).

![Antimalware Azure](./media/azure-security-iaas/azantimalware.png)

### <a name="install-hello-latest-security-updates"></a>Installare gli aggiornamenti di sicurezza più recenti hello
Alcuni dei hello carichi di lavoro prima che i clienti spostano tooAzure sono labs e sistemi con accesso esterno. Se le macchine virtuali ospitate da Azure ospitare applicazioni o servizi che devono toobe accessibile toohello Internet, essere implica l'applicazione di patch. Patch oltre hello del sistema operativo. Vulnerabilità senza patch sulle applicazioni di terze parti può anche causare tooproblems che può essere evitata se buona gestione delle patch è attiva.

### <a name="deploy-and-test-a-backup-solution"></a>Distribuire e testare una soluzione di backup

Esattamente come gli aggiornamenti della sicurezza, è necessario un backup hello toobe gestito stesso modo in cui si gestiscono tutte le altre operazioni. Ciò è vero dei sistemi che fanno parte di estensione toohello cloud nell'ambiente di produzione. I sistemi di test e dev devono seguire le strategie di backup che forniscono funzionalità di ripristino che sono simili agli utenti di toowhat hanno acquisito familiarità con, in base alla propria esperienza con gli ambienti on-premise.

I carichi di lavoro spostato tooAzure deve essere integrato con soluzioni di backup esistenti quando possibile. In alternativa, utilizzare [Azure Backup](../backup/backup-azure-arm-vms.md) toohelp soddisfare le esigenze di backup.


## <a name="monitor"></a>Monitorare

[Centro sicurezza PC](../security-center/security-center-intro.md) fornisce la valutazione continuativa dello stato di sicurezza hello di risorse di Azure tooidentify potenziali vulnerabilità nella sicurezza. Un elenco di suggerimenti in modo semplificato il processo di hello di configurazione di controlli necessari.

Tra gli esempi sono inclusi:

- Provisioning toohelp antimalware, identificare e rimuovere il software dannoso.
- Configurazione di sicurezza e gruppi di regole toocontrol traffico toovirtual macchine della rete.
- Firewall applicazione web toohelp difendersi da attacchi che le applicazioni web di destinazione di provisioning.
- Distribuzione di aggiornamenti di sistema mancanti.
- Indirizzamento delle configurazioni del sistema operativo che non corrispondono a hello consiglia le linee di base.

Hello immagine seguente mostra alcune delle opzioni di hello che è possibile abilitare in Centro sicurezza PC.

![Criteri del Centro sicurezza di Azure](./media/azure-security-iaas/security-center-policies.png)

[Operations Management Suite](../operations-management-suite/operations-management-suite-overview.md) è una soluzione Microsoft per la gestione IT basata sul cloud che consente di gestire e proteggere l'infrastruttura locale e cloud. Dato che viene implementato come servizio basato sul cloud, Operations Management Suite può essere distribuito rapidamente e con un investimento minimo in termini di risorse dell'infrastruttura.

Le nuove funzionalità sono disponibili automaticamente, evitando così i costi di manutenzione e aggiornamento continui. Operations Management Suite si integra anche con System Center Operations Manager. Dispone di diversi componenti toohelp migliorare la gestione di carichi di lavoro Azure, tra cui un [Security and Compliance](../operations-management-suite/oms-security-getting-started.md) modulo.

È possibile utilizzare le funzionalità di sicurezza e conformità hello nelle informazioni di Operations Management Suite tooview sulle risorse. informazioni di Hello sono suddivisa in quattro categorie principali:

- **Domini di sicurezza**. Permette di esplorare ulteriormente i record di sicurezza nel tempo. Permette di accedere alla valutazione antimalware, alla valutazione degli aggiornamenti, a informazioni sulla sicurezza di rete, a informazioni su identità e accessi e ai computer che generano eventi di sicurezza. Sfruttare i vantaggi del dashboard di accesso rapido toohello Centro sicurezza di Azure.
- **Problemi rilevanti**: identificare il numero di problemi attivi hello rapidamente e hello gravità di questi problemi.
- **Rilevamenti (anteprima)**. Permette di identificare i modelli di attacco visualizzando gli avvisi di sicurezza relativi alle risorse non appena vengono generati.
- **Minaccia intelligence**: identificazione di attacco hello di modelli di visualizzazione del numero totale di hello del server con traffico IP dannoso in uscita, il tipo di minaccia intenzionale e una mappa che mostra provenienza questi indirizzi IP.
- **Query comuni di sicurezza**: vedere un elenco di sicurezza più comune di hello esegue una query che è possibile utilizzare toomonitor l'ambiente. Quando si fa clic su uno di tali query, hello **ricerca** pannello apre e Visualizza risultati hello per tale query.

Hello schermata riportata di seguito viene illustrato un esempio di informazioni hello visualizzabili Operations Management Suite.

![Baseline della sicurezza di Operations Management Suite](./media/azure-security-iaas/oms-security-baseline.png)



## <a name="next-steps"></a>Passaggi successivi


* [Blog del team di sicurezza di Azure](https://blogs.msdn.microsoft.com/azuresecurity/)
* [Microsoft Security Response Center](https://technet.microsoft.com/library/dn440717.aspx)
* [Procedure consigliate e modelli per la sicurezza di Azure](security-best-practices-and-patterns.md)
