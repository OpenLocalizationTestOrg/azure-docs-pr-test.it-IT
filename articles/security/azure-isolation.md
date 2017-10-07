---
title: aaaIsolation in hello Cloud pubblico di Azure | Documenti Microsoft
description: "Informazioni sui servizi di calcolo basate su cloud che includono un'ampia selezione di istanze di calcolo e i servizi che possono estendersi su e giù automaticamente toomeet hello esigenze dell'applicazione o dell'organizzazione."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 271e5f0d00abcfd404ce6c50cfb7d1ac26360c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="isolation-in-hello-azure-public-cloud"></a>Isolamento in hello Cloud pubblico di Azure
##  <a name="introduction"></a>Introduzione
### <a name="overview"></a>Panoramica
tooassist e potenziali clienti Azure comprendere e utilizzare hello varie funzionalità correlate alla sicurezza disponibili in e circostante hello piattaforma Azure, Microsoft ha sviluppato una serie di White paper, sicurezza panoramiche, procedure consigliate, e Elenchi di controllo.
intervallo di argomenti in termini di dimensioni e della complessità Hello e vengono aggiornate periodicamente. Questo documento fa parte della serie come riepilogato nella sezione astratta di hello successiva.

### <a name="azure-platform"></a>Piattaforma Azure
Azure è una piattaforma cloud aperta e flessibile del servizio che supporta hello selezione più ampia di sistemi operativi, linguaggi di programmazione, Framework, strumenti, i database e i dispositivi. Ad esempio, è possibile:
- Eseguire contenitori Linux con l'integrazione Docker;
- Compilare app con JavaScript, Python, .NET, PHP, Java e Node.js e
- Compilare back-end per dispositivi iOS, Android e Windows.

Microsoft Azure supporta hello stesse tecnologie milioni di sviluppatori e professionisti IT si basano su già e attendibile.

Quando si compila, o eseguire la migrazione di risorse IT a, un provider di servizi di cloud pubblico, ci si basa sul tooprotect capacità dell'organizzazione che le applicazioni e dati con controlli hello e servizi di hello assicurano toomanage hello del basato su cloud Asset.

Infrastruttura di Azure è progettato da hello tooapplications di funzionalità per l'hosting contemporaneamente milioni di clienti e fornisce una base attendibile in cui le aziende grado di soddisfare le esigenze di sicurezza. Inoltre, Azure offre un'ampia gamma di toocontrol possibilità hello e opzioni di protezione configurabili loro in modo che sia possibile personalizzare sicurezza toomeet hello requisiti delle distribuzioni. Questo documento consente di soddisfare questi requisiti.

### <a name="abstract"></a>Sunto

Microsoft Azure consente di toorun applicazioni e le macchine virtuali (VM) su infrastruttura fisica condivisa. Una delle applicazioni di toorunning hello motivazioni economica principale in un ambiente cloud è hello possibilità toodistribute hello costo risorse condivise tra più clienti. Questa pratica di multi-tenancy aumenta l'efficienza grazie al multiplexing delle risorse tra i diversi clienti a costi ridotti, Purtroppo, introducendo rischi hello condividere altre toorun risorse di infrastruttura e server fisici applicazioni sensibili e le macchine virtuali appartenenti tooan arbitrario e potenzialmente dannoso utente.

In questo articolo descrive come Microsoft Azure fornisce l'isolamento rispetto agli utenti malintenzionati sia non intenzionale e funge da Guida per l'architettura di soluzioni cloud offrendo tooarchitects scelte di isolamento diversi. Questo white paper è incentrata sulla tecnologia hello della piattaforma Azure e i controlli di sicurezza che riguardano il cliente e non tenta tooaddress i contratti di servizio, i modelli dei prezzi e considerazioni sulle procedure consigliate di DevOps.

## <a name="tenant-level-isolation"></a>Isolamento a livello di tenant
Uno dei vantaggi principali di hello del cloud computing è concetto di un'infrastruttura comune condivisa tra i numerosi clienti contemporaneamente, iniziali tooeconomies della scala. Questo concetto è denominato "multi-tenancy". Microsoft si impegna continuamente tooensure che hello l'architettura multi-tenant del Cloud di Microsoft Azure supporta gli standard di sicurezza, la riservatezza, riservatezza, integrità e disponibilità.

In hello abilitata per il cloud all'area di lavoro, un tenant può essere definito come un client o l'organizzazione che possiede e gestisce un'istanza specifica di tale servizio cloud. Con la piattaforma di identità hello è fornita da Microsoft Azure, un tenant è semplicemente un'istanza dedicata di Azure Active Directory (Azure AD) che l'organizzazione riceve e diventa proprietaria quando effettua l'iscrizione a un servizio cloud Microsoft.

Ogni directory di Azure AD è distinta e separata dalle altre directory di Azure AD. Come un edificio ufficio aziendale è un tooonly di bene sicuro specifico dell'organizzazione, una directory di Azure AD è stato inoltre progettato toobe un bene sicuro per l'utilizzo da sola organizzazione. Hello architettura di Azure AD isola le informazioni di identità e i dati cliente combinino con. Questo significa che gli utenti e gli amministratori di una directory di Azure AD non possono accedere accidentalmente o con dolo ai dati presenti in un'altra directory.

### <a name="azure-tenancy"></a>Tenancy di Azure
Azure tenancy (sottoscrizione di Azure) fa riferimento univoco e relazione "customer o fatturazione" tooa [tenant](https://docs.microsoft.com/azure/active-directory/develop/active-directory-howto-tenant) in [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis). L'isolamento a livello di tenant in Microsoft Azure si ottiene usando Azure Active Directory e i [controlli in base al ruolo](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) messi a disposizione da questa applicazione. Ogni sottoscrizione di Azure è associata a una directory di Azure Active Directory (AD).

Gli utenti, gruppi e applicazioni da tale directory possono gestire le risorse nella sottoscrizione di Azure hello. È possibile assegnare i diritti di accesso utilizzando hello portale di Azure, gli strumenti da riga di comando di Azure e le API di gestione di Azure. Un tenant di Azure AD viene isolato in modo logico usando limiti di sicurezza in modo che nessun cliente possa accedere agli altri tenant e comprometterli, intenzionalmente o accidentalmente. Azure AD viene eseguito nei server "bare metal" isolati in un segmento di rete separato, in cui il filtraggio dei pacchetti a livello di host e Windows Firewall bloccano connessioni e traffico indesiderati.

- Accesso toodata in Azure AD richiede l'autenticazione utente tramite un [servizio token di sicurezza (STS)](https://docs.microsoft.com/azure/app-service-web/web-sites-authentication-authorization). Informazioni sull'esistenza, lo stato abilitato e ruolo dell'utente hello viene usate da hello autorizzazione sistema toodetermine se tenant di destinazione toohello hello richiesta di accesso è autorizzato per questo utente in questa sessione.

![Tenancy di Azure](./media/azure-isolation/azure-isolation-fig1.png)


- I tenant sono contenitori discreti che non hanno alcuna relazione tra loro.

- Non è possibile l'accesso da un tenant all'altro, a meno che l'amministratore non lo conceda tramite la federazione o il provisioning degli account utente da altri tenant.

- Accesso fisico tooservers che costituiscono il servizio hello Azure AD e i sistemi back-end tooAzure Active Directory l'accesso diretto, è limitato.

- Gli utenti di Azure Active Directory non dispongono di accedere alle risorse del toophysical o percorsi e pertanto non è possibile per loro toobypass hello RBAC criteri controlli logici indicati seguente.

Per esigenze di diagnostica e manutenzione, è necessario e viene usato un modello operativo che impiega un sistema di elevazione dei privilegi just-in-time. Azure AD Privileged Identity Management (PIM) introduce il concetto di hello di un amministratore idoneo. Gli [amministratori idonei](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure) devono essere utenti che necessitano dell'accesso con privilegi in modo occasionale, non con cadenza quotidiana. ruolo Hello è inattivo fino a quando l'utente hello richiede l'accesso, quindi il completamento di un processo di attivazione e diventare amministratore attivo per un periodo di tempo prestabilito.

![Gestione identità con privilegi di Azure AD](./media/azure-isolation/azure-isolation-fig2.png)

Azure Active Directory ospita ogni tenant nel relativo contenitore protetto, con criteri e autorizzazioni tooand all'interno del contenitore di hello esclusivamente detenute e gestite dai tenant hello.

il concetto di Hello dei contenitori di tenant è eccessivamente integrante nel servizio directory hello in tutti i livelli, da portali tutti hello archiviazione toopersistent modo.

Anche quando i metadati da più tenant di Azure Active Directory vengono archiviati in hello stesso fisico su disco, non vi è alcuna relazione tra i contenitori di hello diverso da quello definito dal servizio di directory hello, che a sua volta è determinato dall'amministratore tenant hello.

### <a name="azure-role-based-access-control-rbac"></a>Controllo degli accessi in base al ruolo di Azure
[Azure Role-Based Access controllo (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) consente di vari componenti disponibili all'interno di una sottoscrizione di Azure è tooshare, fornendo la gestione di accesso granulare per Azure. Azure RBAC consente compiti toosegregate all'interno dell'organizzazione e concedere l'accesso in base quale gli utenti devono tooperform i processi. Invece di concedere a tutti autorizzazioni senza restrizioni per la sottoscrizione o le risorse di Azure, è possibile consentire solo determinate azioni.

Azure RBAC presenta tre ruoli di base che si applicano a tipi di risorse tooall:

- **Proprietario** dispone di accesso completo tooall risorse hello toodelegate destra accesso tooothers inclusi.

- **Collaboratore** possono creare e gestire tutti i tipi di risorse di Azure, ma non è possibile concedere l'accesso tooothers.

- **Lettore** può visualizzare le risorse di Azure esistenti.

![Controllo degli accessi in base al ruolo di Azure](./media/azure-isolation/azure-isolation-fig3.png)

rest Hello dei ruoli RBAC hello in Azure consente la gestione delle risorse di Azure specifiche. Ad esempio, hello ruolo Collaboratore di macchina virtuale consente toocreate utente hello e gestire macchine virtuali. Non viene loro toohello accesso rete virtuale di Azure o subnet hello hello macchina virtuale si connette a.

[Ruoli predefiniti RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) elenco ruoli hello disponibili in Azure. Specifica le operazioni di hello e che ogni ruolo incorporato e concede toousers ambito. Se si cerca toodefine dei ruoli personalizzati per un maggiore controllo, vedere come toobuild [ruoli personalizzati in Azure RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles).

Altre funzionalità di Azure Active Directory includono:
- Azure AD consente alle applicazioni di tooSaaS SSO, indipendentemente dalla relativa posizione. Alcune applicazioni sono federate con Azure AD e altre usano SSO basato su password. Le applicazioni federate possono anche supportare il provisioning utenti e l'[insieme di credenziali delle password](https://www.techopedia.com/definition/31415/password-vault).

- Accesso toodata in [di archiviazione di Azure](https://azure.microsoft.com/services/storage/) è controllata tramite l'autenticazione. Ogni account di archiviazione ha una chiave primaria ([chiave account di archiviazione](https://docs.microsoft.com/azure/storage/storage-create-storage-account), o SAK) e una chiave segreta secondaria (la firma di accesso condiviso hello o SAS).

- Azure AD fornisce l'identità come servizio usando la federazione (con [Active Directory Federation Services](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-azure-adfs)), la sincronizzazione e la replica con le directory locali.

- [Azure multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) è servizio di autenticazione a più fattori hello che richiede l'accesso degli utenti tooverify mediante l'utilizzo di un'app per dispositivi mobili, una telefonata o un messaggio di testo. E può essere utilizzato con Azure AD toohelp sicuro alle risorse locali con il server Azure multi-Factor Authentication hello e con applicazioni personalizzate e le directory utilizzando hello SDK.

- [Servizi di dominio AD Azure](https://azure.microsoft.com/services/active-directory-ds/) consente di aggiungere macchine virtuali di Azure tooan dominio di Active Directory senza distribuire i controller di dominio. È possibile accedere in macchine virtuali toothese con le credenziali aziendali di Active Directory e amministrare le macchine virtuali appartenenti a un dominio usando le linee di base di criteri di gruppo tooenforce sicurezza in tutte le macchine virtuali di Azure.

- [Azure B2C Directory attiva](https://azure.microsoft.com/services/active-directory-b2c/) fornisce un servizio di gestione di identità globale a disponibilità elevata per applicazioni per consumatori che viene ridimensionata toohundreds di milioni di valori Identity. Il servizio può essere integrato tra piattaforme mobili e Web. Consentire agli utenti possono accedere tooall le applicazioni attraverso esperienze di personalizzabile utilizzando gli account di social networking esistenti o creazione di credenziali.

### <a name="isolation-from-microsoft-administrators--data-deletion"></a>Isolamento da amministratori Microsoft ed eliminazione dei dati
Microsoft ha tooprotect misure sicuro dei dati dall'accesso non appropriato o l'utilizzo da persone non autorizzate. Questi processi operativi e i controlli sono supportati da hello [condizioni per i servizi Online](http://aka.ms/Online-Services-Terms), che offrono impegni contrattuali che regolano l'accesso ai dati tooyour.

-   Gli esperti Microsoft non è necessario dati tooyour di accesso predefiniti nel cloud hello. L'accesso viene loro concesso sotto supervisione e solo quando necessario. Viene anche attentamente controllato e registrato e revocato quando non è più necessario.

-   Microsoft può assumere altri servizi di società tooprovide limitati per suo conto. Subappaltatori possono accedere a dati toodeliver solo hello clienti per cui, Microsoft ha assunto li tooprovide e non sono autorizzate a utilizzarle per altri scopi. Inoltre, sono associati contrattualmente toomaintain hello riservatezza delle informazioni dei clienti.

Servizi aziendali con certificazioni controllate, ad esempio ISO/IEC 27001 regolarmente sono controllate da Microsoft e accreditati controllo imprese, di cui eseguono l'esempio controlli tooattest che l'accesso, solo per scopi autorizzati. Il cliente può accedere ai propri dati in qualsiasi momento e per qualunque motivo.

Se si eliminano tutti i dati, Microsoft Azure Elimina i dati di hello, comprese le eventuali copie memorizzate nella cache o di backup. Per i servizi nell'ambito, l'eliminazione verificherà entro 90 giorni dopo la fine di hello hello del periodo di memorizzazione. (Nell'ambito servizi vengono definiti nella sezione di condizioni per l'elaborazione dati hello del nostro [condizioni per i servizi Online](http://aka.ms/Online-Services-Terms).)

Se un'unità disco utilizzata per l'archiviazione si verifica un errore hardware, è in modo sicuro [vengono cancellati o eliminati](https://www.microsoft.com/trustcenter/Privacy/You-own-your-data) prima Microsoft restituisce toohello produttore per la sostituzione o la riparazione. Hello unità hello vengono sovrascritti tooensure che hello dati non può essere recuperati con qualsiasi mezzo.

## <a name="compute-isolation"></a>Isolamento del calcolo
Microsoft Azure fornisce vari basato sul cloud computing servizi che includono un'ampia selezione di istanze di calcolo e servizi che possono estendersi su e giù automaticamente toomeet hello esigenze dell'applicazione o dell'organizzazione. Tali istanza di calcolo e il servizio offrono l'isolamento dei dati di più livelli toosecure senza pregiudicare la flessibilità di hello nella configurazione che richiedono i clienti.

### <a name="hyper-v--root-os-isolation-between-root-vm--guest-vms"></a>Isolamento Hyper-V e del sistema operativo radice tra VM radice e VM guest
La piattaforma di calcolo di Azure si basa sulla virtualizzazione dei computer, ovvero tutto il codice del cliente viene eseguito in una macchina virtuale Hyper-V. In ogni nodo di Azure (o endpoint di rete), sussiste un Hypervisor che viene eseguito direttamente sull'hardware hello e divide un nodo in un numero variabile di macchine virtuali Guest (VM).


![Isolamento Hyper-V e del sistema operativo radice tra VM radice e VM guest](./media/azure-isolation/azure-isolation-fig4.jpg)


Inoltre, ogni nodo è una speciale radice macchina virtuale, che viene eseguito hello del sistema operativo Host. Un limite critico è isolamento hello di hello guest, le macchine virtuali da un altro, gestito da hello hypervisor e sistema operativo radice hello e radice hello VM guest hello macchine virtuali. abbinamento degli hypervisor o la radice del sistema operativo Hello sfrutta decenni Microsoft dell'esperienza di sicurezza del sistema operativo e acquisire informazioni più recenti dal Microsoft Hyper-V, un isolamento forte tooprovide di macchine virtuali guest.

piattaforma Azure Hello Usa un ambiente virtualizzato. Le istanze utente operano come macchine virtuali autonome che non dispone di server di accesso tooa host fisico e viene applicato l'isolamento utilizzando i livelli di privilegio (circolare-0/ring-3) processore fisico.

Livello 0 è hello più privilegiato e 3 è hello almeno. sistema operativo guest Hello in esecuzione in 1 anello con meno privilegi e le applicazioni eseguite hello 3 anello con privilegi minimi. Virtualizzazione delle risorse fisiche comporta tooa netta separazione tra sistema operativo guest e hypervisor, determinando la separazione di sicurezza aggiuntive tra hello due.

Hello Azure hypervisor funziona come un micro-kernel e passa tutte le richieste di accesso hardware dall'host toohello di macchine virtuali guest per l'elaborazione tramite un'interfaccia di memoria condivisa denominata VMBus. Questo impedisce agli utenti di ottenere sistema toohello non elaborato l'accesso in lettura/scrittura/esecuzione e si riduce il rischio di hello di condivisione delle risorse di sistema.

### <a name="advanced-vm-placement-algorithm--protection-from-side-channel-attacks"></a>Algoritmo avanzato di selezione host per le VM e protezione da attacchi side channel
Qualsiasi attacco tra VM prevede due passaggi: inserimento di una macchina virtuale controllata avversario in hello stesso host come vittima hello macchine virtuali e quindi sugli tooeither limite di isolamento hello rubare informazioni riservate vittima o incidere sulle prestazioni per greed o vandalismo. Microsoft Azure fornisce protezione in entrambi i passaggi usando un algoritmo avanzato di selezione host per le VM e la protezione da tutti gli attacchi side channel noti, incluse le VM "noisy neighbor".

### <a name="hello-azure-fabric-controller"></a>Hello Controller di infrastruttura di Azure
Hello Controller di infrastruttura di Azure è responsabile dell'allocazione delle risorse di infrastruttura tootenant i carichi di lavoro e gestisce le comunicazioni unidirezionali dal computer di toovirtual hello host. algoritmo di posizionamento VM Hello del controller di infrastruttura di Azure hello è toopredict sofisticato e praticamente come livello di host fisico.

![Hello Controller di infrastruttura di Azure](./media/azure-isolation/azure-isolation-fig5.png)

Hello hypervisor Azure impone memoria e processo di separazione tra le macchine virtuali e instrada in modo sicuro i tenant tooguest del sistema operativo di traffico di rete. Si elimina così la possibilità di un attacco side channel a livello di VM.

In Azure, è speciale macchina virtuale radice hello: viene eseguito un sistema operativo finalizzato denominato hello radice del sistema operativo che ospita un agente di infrastruttura (FA). /FAS vengono utilizzati in turn toomanage gli agenti guest (GA) guest sistemi operativi in macchine virtuali di clienti. Gestiscono anche i nodi di archiviazione.

raccolta di Azure hypervisor, Hello radice del sistema operativo/FA e macchine virtuali/GAs cliente è costituito da un nodo di calcolo. Gli agenti dell'infrastruttura sono gestiti da un controller di infrastruttura (FC) esterno ai nodi di calcolo e di archiviazione: i cluster di calcolo e di archiviazione vengono gestiti da controller di infrastruttura separati. Se un cliente viene aggiornato il file di configurazione della propria applicazione mentre è in esecuzione, hello FC comunica con hello FA, che quindi contatta GAs, che notifica di modifica della configurazione hello un'applicazione hello. In caso di hello un guasto dell'hardware, hello FC verrà automaticamente trovare hardware disponibile e riavviare hello VM non esiste.

![Controller di infrastruttura di Azure](./media/azure-isolation/azure-isolation-fig6.jpg)

Comunicazione dall'agente di tooan Controller di infrastruttura è unidirezionale. agente Hello implementa un servizio protetto da SSL che risponde solo toorequests dal controller hello. Non consente di stabilire controller toohello connessioni o altri nodi interni con privilegi. Hello FC considera tutte le risposte come se fossero non attendibili.


![Controller di infrastruttura](./media/azure-isolation/azure-isolation-fig7.png)

Isolamento si estende da hello VM radice da macchine virtuali Guest e hello macchine virtuali Guest uno da altro. Anche i nodi di calcolo sono isolati dai nodi di archiviazione per aumentare la protezione.


pacchetto di rete di fornire Hello hypervisor e sistema operativo host hello - filtri toohelp garantire che le macchine virtuali non attendibili non è possibile generare il traffico di spoofing o ricevere il traffico indirizzato non toothem, endpoint dell'infrastruttura tooprotected il traffico diretto o invio/ricezione traffico broadcast appropriato.


### <a name="additional-rules-configured-by-fabric-controller-agent-tooisolate-vm"></a>Le regole aggiuntive configurate per tooIsolate Fabric Controller agente VM
Per impostazione predefinita, tutto il traffico viene bloccato quando viene creata una macchina virtuale e quindi agente controller di infrastruttura hello Configura hello pacchetto filtro tooadd regole e le eccezioni tooallow autorizzato il traffico.

Sono previste due categorie di regole:

-   **Regole di configurazione macchina virtuale o di infrastruttura**: per impostazione predefinita, vengono bloccate tutte le comunicazioni. Vi sono eccezioni tooallow toosend una macchina virtuale e di ricevere il traffico DNS e DHCP. Macchine virtuali è anche possibile inviare traffico toohello "public" internet e inviare traffico tooother macchine virtuali all'interno di hello stessa rete virtuale di Azure e hello server di attivazione del sistema operativo. elenco di macchine virtuali di Hello delle destinazioni in uscita consentite non include le subnet di Azure router, gestione di Azure e altre proprietà di Microsoft.

-   **File di configurazione del ruolo:** definisce hello sono elencati di controllo di accesso (ACL) in ingresso basati sul modello di servizio del tenant hello.

### <a name="vlan-isolation"></a>Isolamento VLAN
In ogni cluster sono presenti tre VLAN:

![Isolamento VLAN](./media/azure-isolation/azure-isolation-fig8.jpg)


-   VLAN principale: Hello interconnessioni nodi non attendibili cliente

-   Hello VLAN FC-contiene FCs attendibile e sistemi di supporto

-   Hello dispositivo VLAN: contiene rete attendibile e altri dispositivi dell'infrastruttura

È consentita la comunicazione da hello VLAN FC toohello VLAN principale, ma non può essere avviato da hello principale VLAN toohello FC VLAN. La comunicazione viene ugualmente bloccata dal dispositivo di toohello principale VLAN hello VLAN. Ciò assicura che anche se un nodo in esecuzione il codice del cliente viene compromessa, non è possibile attacco nodi hello FC o dispositivo le VLAN.

## <a name="storage-isolation"></a>Isolamento dell'archiviazione
### <a name="logical-isolation-between-compute-and-storage"></a>Isolamento logico tra calcolo e archiviazione
Nell'ambito della sua progettazione fondamentale, Microsoft Azure separa il calcolo basato sulle VM dall'archiviazione. Questa separazione consente il calcolo e archiviazione tooscale in modo indipendente, rendendo più semplice tooprovide multi-tenancy e isolamento.

Di conseguenza, viene eseguito di archiviazione di Azure su computer separati con nessun tooAzure di connettività di rete consente di calcolare, ad eccezione logicamente. [Questo](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf) significa che quando viene creato un disco virtuale, lo spazio sul disco non viene allocato per l'intera capacità. Al contrario, viene creata una tabella che esegue il mapping di indirizzi in hello tooareas di disco virtuale su disco fisico hello e tale tabella è inizialmente vuota. **prima volta che un cliente scrive dati nel disco virtuale hello, allocare spazio su disco fisico hello e tooit un puntatore viene inserito nella tabella hello Hello.**
### <a name="isolation-using-storage-access-control"></a>Isolamento tramite il controllo di accesso per l'archiviazione
Il **controllo di accesso in Archiviazione di Azure** ha un modello semplice. Ogni sottoscrizione di Azure può creare uno o più account di archiviazione. Ogni Account di archiviazione dispone di una singola chiave segreta toocontrol utilizzato accesso tooall dati in tale Account di archiviazione.

![Isolamento tramite il controllo di accesso per l'archiviazione](./media/azure-isolation/azure-isolation-fig9.png)

**Accedere ai dati di archiviazione tooAzure (incluse le tabelle)** può essere controllata con un [firma di accesso condiviso (firma di accesso condiviso)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) token che concede l'ambito di accesso. Hello firma di accesso condiviso è stato creato tramite un modello di query (URL), firmato con hello [SAK (chiave Account di archiviazione)](https://msdn.microsoft.com/library/azure/ee460785.aspx). Che [firmato URL](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) possono essere forniti tooanother processo (che è delegata), che può quindi specificare i dettagli hello di query hello e richiesta hello hello del servizio di archiviazione. Una firma di accesso condiviso consente toogrant accesso basato sul tempo tooclients senza rivelare la chiave privata dell'account di archiviazione hello.

Hello SAS significa che è possibile concedere che autorizzazioni, tooobjects in questo account di archiviazione per un determinato periodo di tempo e con un set specificato di autorizzazioni limitate di un client. È possibile concedere queste autorizzazioni limitate senza tooshare le chiavi di accesso di account.

### <a name="ip-level-storage-isolation"></a>Isolamento dell'archiviazione a livello IP
È possibile stabilire firewall e definire un intervallo di indirizzi IP per i client attendibili. Con un intervallo di indirizzi IP, solo i client che hanno un indirizzo IP interno hello definito possono connettersi troppo[di archiviazione di Azure](https://docs.microsoft.com/azure/storage/storage-security-guide).

Dati di archiviazione IP possono essere protetti da utenti non autorizzati tramite un meccanismo di rete che viene utilizzato tooallocate un tunnel dedicato o dedicato di archiviazione tooIP traffico.

### <a name="encryption"></a>Crittografia
Azure offre i tipi di dati tooprotect di crittografia seguenti:
-   Crittografia in transito

-   Crittografia di dati inattivi

#### <a name="encryption-in-transit"></a>Crittografia in transito
La crittografia in transito è un meccanismo di protezione dei dati durante la trasmissione tra le reti. Con Archiviazione di Azure è possibile proteggere i dati con:

-   [Crittografia a livello di trasporto](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-in-transit), ad esempio HTTPS quando si trasferiscono dati all'interno o all'esterno di Archiviazione di Azure.

-   [Crittografia di rete](../storage/common/storage-security-guide.md#using-encryption-during-transit-with-azure-file-shares), ad esempio la crittografia SMB 3.0 per le condivisioni file di Azure.

-   [Crittografia client-side](https://docs.microsoft.com/azure/storage/storage-security-guide#using-client-side-encryption-to-secure-data-that-you-send-to-storage), dati di hello tooencrypt prima di essere trasferiti in toodecrypt e archiviazione dati hello dopo che viene trasferita all'esterno di archiviazione.

#### <a name="encryption-at-rest"></a>Crittografia di dati inattivi
Per molte organizzazioni, [la crittografia dei dati inattivi](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) è un passaggio obbligatorio per assicurare la privacy dei dati, la conformità e la sovranità dei dati. Esistono tre funzionalità di Azure che consentono di crittografare dati inattivi:

-   [La crittografia del servizio di archiviazione](https://docs.microsoft.com/azure/storage/storage-security-guide#encryption-at-rest) consente che il servizio di archiviazione hello crittografa automaticamente i dati durante la scrittura di archiviazione tooAzure toorequest.

-   [Crittografia client-side](https://docs.microsoft.com/azure/storage/storage-security-guide#client-side-encryption) offre inoltre funzionalità hello di crittografia.

-   [Crittografia disco Azure](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) consente tooencrypt hello del sistema operativo dischi e i dischi di dati utilizzati da una macchina virtuale IaaS.

#### <a name="azure-disk-encryption"></a>Azure Disk Encryption
[Crittografia dischi di Azure](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) per le macchine virtuali consente di soddisfare i requisiti di conformità e sicurezza dell'organizzazione, grazie alla possibilità di crittografare i dischi delle macchine virtuali, inclusi i dischi di avvio e di dati, con chiavi e criteri gestiti in [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).

soluzioni di crittografia del disco per Windows Hello è basato su [crittografia unità BitLocker di Microsoft](https://technet.microsoft.com/library/cc732774.aspx), e hello Linux soluzione si basa su [dm crypt](https://en.wikipedia.org/wiki/Dm-crypt).

soluzione Hello supporta hello seguenti scenari per le macchine virtuali IaaS quando sono abilitati in Microsoft Azure:
-   Integrazione dell'insieme di credenziali delle chiavi di Azure.

-   Macchine virtuali di livello Standard: serie A, D, DS, G, GS e così via per VM IaaS

-   Abilitazione della crittografia nelle macchine virtuali IaaS Windows e Linux

-   Disabilitazione della crittografia nel sistema operativo e nelle unità dati per le VM IaaS Windows

-   Disabilitazione della crittografia nelle unità dati per le macchine virtuali IaaS Linux

-   Abilitazione della crittografia in macchine virtuali IaaS in esecuzione nel sistema operativo client Windows

-   Abilitazione della crittografia su volumi con percorsi di montaggio

-   Abilitazione della crittografia nelle macchine virtuali Linux configurate con striping del disco (RAID) tramite [mdadm](https://en.wikipedia.org/wiki/Mdadm)

-   Abilitazione della crittografia nelle macchine virtuali Linux usando [LVM (Logical Volume Manager)](https://msdn.microsoft.com/library/windows/desktop/bb540532) per i dischi di dati

-   Abilitazione della crittografia nelle macchine virtuali Windows configurate usando spazi di archiviazione

-   Sono supportate tutte le aree geografiche pubbliche di Azure

soluzione Hello non supporta i seguenti scenari, le funzionalità e tecnologie in versione di hello hello:

-   VM IaaS del piano Basic

-   Disabilitazione della crittografia in un'unità del sistema operativo per le VM IaaS Linux

-   Macchine virtuali IaaS che vengono creati utilizzando il metodo di creazione hello classico di VM

-   Integrazione con il servizio di gestione delle chiavi locale.

-   File di Azure (file system condiviso), file system di rete (NFS, Network File System), volumi dinamici e macchine virtuali Windows configurate con sistemi RAID basati su software

## <a name="sql-azure-database-isolation"></a>Isolamento del database SQL Azure
Database SQL è un servizio di database relazionale nel cloud di Microsoft hello basata sul motore di Microsoft SQL Server leader sul mercato hello e in grado di gestire carichi di lavoro di importanza critica. Il database SQL di Azure offre isolamento prevedibile dei dati a livello di account, in base all'area geografica e alla rete, con esigenze di amministrazione quasi nulle.

### <a name="sql-azure-application-model"></a>Modello applicativo di SQL Azure

Il database di [Microsoft SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-get-started) è un servizio di database relazionale basato sul cloud che si avvale delle tecnologie SQL Server. Fornisce un servizio di database a disponibilità elevata, scalabile e multi-tenant ospitato da Microsoft nel cloud.

Dal punto di vista dell'applicazione SQL Azure fornisce hello seguente gerarchia: ogni livello è contenuto uno-a-molti dei livelli inferiori.

![Modello applicativo di SQL Azure](./media/azure-isolation/azure-isolation-fig10.png)

sottoscrizione e l'account hello siano management e Microsoft Azure platform concetti tooassociate fatturazione.

Database e server logici sono concetti specifici di SQL Azure e vengono gestiti tramite SQL Azure, con le interfacce OData e TSQL fornite oppure tramite il portale SQL Azure integrato nel portale di Azure.

I server SQL Azure non sono istanze di macchine virtuali o fisiche, ma sono raccolte di database, con criteri di sicurezza e gestione condivisi, archiviate nel cosiddetto database "master logico".

![SQL Azure](./media/azure-isolation/azure-isolation-fig11.png)

I database master logici includono:

-   Account di accesso SQL utilizzato tooconnect toohello server

-   Regole del firewall

Informazioni relative all'uso e della fatturazione per i database di SQL Azure da hello stesso server logico non sono garantiti toobe su hello stessa istanza del fisico in cluster di SQL Azure, ma le applicazioni devono fornire nome database di destinazione hello durante la connessione.

Dalla prospettiva del cliente, un server logico viene creato in un'area geografica grafica, mentre la creazione effettiva hello del server hello viene eseguito in uno dei cluster hello in area hello.

### <a name="isolation-through-network-topology"></a>Isolamento tramite la topologia della rete

Quando viene creato un server logico e il relativo nome DNS è registrato, il nome DNS hello punta toohello cosiddetti indirizzo "Gateway VIP" in hello data center specifico in cui è stata inserita server hello.

Dietro hello VIP (indirizzo IP virtuale), è disponibile una raccolta di servizi senza stato gateway. In generale, i gateway vengono coinvolti quando è necessario coordinare più origini dati, ovvero database master, database utente e così via. Il servizio gateway implementa seguente hello:
-   **Inoltro dei dati tramite connessione TDS.** Ciò include l'individuazione di database utente nel cluster back-end hello, l'implementazione di sequenza di accesso hello e quindi inoltro back e back-end toohello di pacchetti TDS hello.

-   **Gestione database.** Ciò include l'implementazione di una raccolta di operazioni di flussi di lavoro toodo CREATE/ALTER/DROP database. operazioni di database Hello possono essere richiamate da intercettare i pacchetti TDS o esplicita APIs OData.

-   Operazioni CREATE/ALTER/DROP per account di accesso/utenti

-   Operazioni di gestione di server logici tramite API OData

![Isolamento tramite la topologia della rete](./media/azure-isolation/azure-isolation-fig12.png)

livello di Hello dietro il gateway hello viene chiamato "back-end". Questo è in tutti i dati di hello è archiviata in modalità a disponibilità elevata. Ogni blocco di dati è detto toobelong tooa "una partizione" o "unità di failover," ognuno di essi con almeno tre repliche. Le repliche sono archiviate e replicate dal motore di SQL Server e gestite da tooas di sistema spesso definito "infrastruttura" un failover.

In genere, il sistema di back-end hello non comunica sistemi tooother in uscita come misura di sicurezza. Si tratta di sistemi toohello riservata nel livello front-end (gateway) hello. computer gateway Hello privilegi limitati nella superficie di attacco hello toominimize hello macchine back-end come meccanismo di difesa in profondità.

### <a name="isolation-by-machine-function-and-access"></a>Isolamento in base all'accesso e alla funzione della macchina
SQL Azure è composto da servizi in esecuzione in funzioni differenti della macchina. SQL Azure è suddiviso in Database Cloud "back-end" e "front-end" ambienti (Gateway/Management), con il principio generale di hello traffico solo di attivazione back-end e out non. ambiente front-end Hello può comunicare toohello all'esterno di world di altri servizi e in generale, è solo di autorizzazioni limitate in hello back-end (sufficiente toocall hello punti di ingresso è tooinvoke esigenze).

## <a name="networking-isolation"></a>Isolamento della rete
La distribuzione di Azure offre più livelli di isolamento della rete. Hello diagramma seguente illustra vari livelli di isolamento rete che toocustomers fornite da Azure. Tali livelli rappresentano nativa nella piattaforma Azure stesso hello e funzionalità definita dal cliente. In ingresso da Internet hello, DDoS Azure fornisce l'isolamento dagli attacchi su larga scala in Azure. livello successivo di Hello di isolamento è definita dal cliente gli indirizzi IP pubblici (endpoint), vengono utilizzati toodetermine possibile passare il tipo di traffico tramite rete virtuale toohello di hello servizio cloud. L'isolamento nativo della rete virtuale di Azure assicura l'isolamento completo da tutte le altre reti e il flusso di traffico solo tramite percorsi e metodi configurati dall'utente. Questi percorsi e i metodi sono livello successivo hello, dove NSGs UDR e ai dispositivi di rete virtuale possono essere utilizzato toocreate isolamento limiti tooprotect hello le distribuzioni di applicazioni nella rete hello protetto.

![Isolamento della rete](./media/azure-isolation/azure-isolation-fig13.png)

**Isolamento del traffico:** A [rete virtuale](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) è hello limite di isolamento del traffico su hello piattaforma Azure. Macchine virtuali (VM) in una rete virtuale non possono comunicare direttamente in una rete virtuale diversa, anche se entrambe le reti virtuali vengono create da tooVMs hello stesso cliente. L'isolamento è una proprietà essenziale che assicura che le macchine virtuali e le comunicazioni dei clienti rimangano private entro una rete virtuale.

La [subnet](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview#subnets) offre un livello di isolamento aggiuntivo nella rete virtuale in base a un intervallo di indirizzi IP. Gli indirizzi IP nella rete virtuale hello, è possibile suddividere una rete virtuale in più subnet per la sicurezza e dell'organizzazione. Macchine virtuali e PaaS ruolo istanze distribuite toosubnets (uguale o diverso) all'interno di una rete virtuale possono comunicare tra loro senza alcuna configurazione aggiuntiva. È inoltre possibile configurare [il gruppo di sicurezza di rete (NSGs)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview#network-security-groups-nsg) tooallow o negare l'istanza di macchina virtuale tooa il traffico di rete in base alle regole configurate nell'elenco di controllo di accesso (ACL) del gruppo. I gruppi di sicurezza di rete possono essere associati a subnet o singole istanze VM in una subnet. Quando un gruppo è associata a una subnet, regole ACL hello si applicano le istanze VM hello tooall nella subnet.

## <a name="next-steps"></a>Passaggi successivi

- [Opzioni di isolamento della rete per le macchine nelle reti virtuali di Microsoft Azure](https://azure.microsoft.com/blog/network-isolation-options-for-machines-in-windows-azure-virtual-networks/)

Ciò include hello classic front-end e back-end scenario in cui le macchine in una rete di back-end specifico o la subnet potrebbero consentire solo alcuni client o altri computer tooconnect tooa particolare endpoint in base a un elenco di indirizzi IP.

- [Isolamento del calcolo](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)

Microsoft Azure offre un vari servizi di calcolo basate su cloud che includono un'ampia selezione di istanze di calcolo e i servizi che possono estendersi su e giù automaticamente toomeet hello esigenze dell'applicazione o dell'organizzazione.

- [Isolamento dell'archiviazione](https://msenterprise.global.ssl.fastly.net/vnext/PDFs/A01_AzureSecurityWhitepaper20160415c.pdf)

Microsoft Azure separa tra loro il calcolo e l'archiviazione basati sulle VM. Questa separazione consente il calcolo e archiviazione tooscale in modo indipendente, rendendo più semplice tooprovide multi-tenancy e isolamento. Di conseguenza, viene eseguito di archiviazione di Azure su computer separati con nessun tooAzure di connettività di rete consente di calcolare, ad eccezione logicamente. Tutte le richieste vengono eseguite tramite HTTP o HTTPS in base alla scelta del cliente.

