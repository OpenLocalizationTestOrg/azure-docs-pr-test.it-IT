---
title: aaaGuidelines per la distribuzione di Windows Server Active Directory in macchine virtuali di Azure | Documenti Microsoft
description: "Se è noto come servizi di dominio Active Directory toodeploy e Active Directory Federation Services in locale, ottengono le informazioni sul relativo funzionamento in macchine virtuali di Azure."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
ms.assetid: 04df4c46-e6b6-4754-960a-57b823d617fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: femila
ms.openlocfilehash: 9ad5a5f138a6402cbb656d9160545846051207b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="guidelines-for-deploying-windows-server-active-directory-on-azure-virtual-machines"></a>Linee guida per la distribuzione di Active Directory di Windows Server nelle macchine virtuali di Azure
Questo articolo illustra le differenze importanti hello tra Active Directory Federation Services (ADFS) locale e la distribuzione in macchine virtuali di Microsoft Azure e di distribuzione Windows Server Active Directory Domain Services (AD DS).

## <a name="scope-and-audience"></a>Ambito e destinatari
articolo Hello è destinato a utenti già esperti la distribuzione di Active Directory locale. Vengono illustrate le differenze di hello tra la distribuzione di Active Directory in Microsoft Azure le macchine virtuali/reti virtuali e le distribuzioni di Active Directory locale tradizionale. Macchine virtuali di Azure e reti virtuali di Azure fanno parte di un'infrastruttura-as-a-Service (IaaS) offre alle organizzazioni tooleverage le risorse nel cloud hello di elaborazione.

Per quelle che non si ha familiarità con la distribuzione di Active Directory, vedere hello [Guida alla distribuzione di Active Directory](https://technet.microsoft.com/library/cc753963) o [pianificare la distribuzione di ADFS](https://technet.microsoft.com/library/dn151324.aspx) come appropriato.

In questo articolo presuppone che hello familiarità con hello seguenti concetti:

* Distribuzione e gestione di Servizi di dominio Active Directory di Windows Server
* Distribuzione e la configurazione dell'infrastruttura toosupport un dominio Active Directory di Windows Server Active Directory di DNS
* Distribuzione e gestione di AD FS di Windows Server
* Distribuzione, configurazione e gestione di applicazioni relying party, ovvero siti e servizi Web, che possono utilizzare token di AD FS di Windows Server
* Concetti generali macchina virtuale, ad esempio come tooconfigure a virtual machine, virtuali, dischi e le reti virtuali

In questo articolo vengono illustrati requisiti di hello per uno scenario di distribuzione ibrido in cui servizi di dominio di Windows Server Active Directory o AD ADFS vengono distribuiti in parte in locale e in parte in macchine virtuali di Azure. documento Hello innanzitutto descrive le differenze critiche hello tra l'esecuzione di Windows Server di dominio Active Directory e ADFS in macchine virtuali di Azure e locali e aspetti importanti che influiscono sulla progettazione e distribuzione. rest Hello di carta hello illustra le linee guida per ognuno dei punti di decisione hello in modo più dettagliato e come tooapply hello scenari di distribuzione di linee guida toovarious.

In questo articolo non descrive la configurazione hello di [Azure Active Directory](http://azure.microsoft.com/services/active-directory/), che è un servizio basato su REST che fornisce funzionalità di controllo di accesso e gestione di identità per le applicazioni cloud. Azure Active Directory (Azure AD) e Windows Server Active Directory sono, tuttavia, tooprovide insieme toowork progettato una soluzione di gestione delle identità e accessi per IT ibridi attuali le moderne applicazioni e gli ambienti. toohelp comprendere le differenze di hello e le relazioni tra servizi di dominio di Windows Server Active Directory e Azure AD, si consideri il seguente hello:

1. È possibile eseguire servizi di dominio di Windows Server Active Directory nel cloud hello in macchine virtuali di Azure quando si utilizza Azure tooextend Data Center locale nel cloud hello.
2. È possibile utilizzare Azure AD toogive applicazioni single sign-on tooSoftware-as-a-Service (SaaS) agli utenti. Questa tecnologia viene usata ad esempio in Microsoft Office 365, nonché in applicazioni eseguite in Azure o in altre piattaforme cloud.
3. È possibile utilizzare Azure AD (il servizio di controllo di accesso) toolet agli utenti di accesso mediante identità di Facebook, Google, Microsoft e altri tooapplications di provider di identità che sono ospitati in locale o cloud hello.

Per altre informazioni su queste differenze, vedere [Nozioni fondamentali sulla gestione delle identità di Azure](fundamentals-identity.md).

## <a name="related-resources"></a>Risorse correlate
È possibile scaricare ed eseguire hello [valutazione della macchina virtuale Azure](https://www.microsoft.com/download/details.aspx?id=40898). Hello valutazione verrà automaticamente controllare l'ambiente locale e genera un report personalizzato basato su hello materiale sussidiario, vedere toohelp in questo argomento si esegue la migrazione tooAzure ambiente hello.

È consigliabile esaminare innanzitutto hello esercitazioni, guide e video relativi hello seguenti argomenti:

* [Configurare una rete virtuale nel portale di Azure hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)
* [Configurare una VPN Site-to-Site nel portale di Azure hello](../vpn-gateway/vpn-gateway-site-to-site-create.md)
* [Installazione di una nuova foresta Active Directory in una rete virtuale di Azure](active-directory-new-forest-virtual-machine.md)
* [Installare un controller di dominio Active Directory di replica in una rete virtuale di Azure](active-directory-install-replica-active-directory-domain-controller.md)
* [Microsoft Azure IaaS per professionisti IT: (01) Dati fondamentali delle macchine virtuali](https://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/01)
* [Microsoft Azure IaaS per professionisti IT: (05) Creazione di reti virtuali e connettività cross-premise](https://channel9.msdn.com/Series/Windows-Azure-IT-Pro-IaaS/05)

## <a name="introduction"></a>Introduzione
Hello i requisiti essenziali per la distribuzione di Windows Server Active Directory in macchine virtuali di Azure esistono differenze minime dalla distribuzione di macchine virtuali locali (e toosome misura, macchine fisiche). Ad esempio, in hello case directory di Windows Server Active Directory, se i controller di dominio di hello (DC) distribuiti nelle macchine virtuali di Azure sono repliche in un oggetto esistente locale dominio/foresta aziendale e quindi hello distribuzione di Azure può essere sostanzialmente gestita in hello esattamente come si può gestire qualsiasi altro sito Active Directory di Windows Server aggiuntivo. Vale a dire subnet devono essere definite in Windows Server Active Directory, un sito creato, subnet hello toothat sito collegato e connesso tooother siti con collegamenti di sito appropriati. Vi sono, tuttavia, alcune differenze che sono comuni tooall Azure distribuzioni e altre che variano in base toohello specifico scenario di distribuzione. Di seguito sono descritte due differenze fondamentali:

### <a name="azure-virtual-machines-may-need-connectivity-toohello-on-premises-corporate-network"></a>Macchine virtuali di Azure potrebbe essere necessario rete aziendale locale toohello di connettività.
La connessione delle macchine virtuali di Azure tooan indietro locale alla rete aziendale richiede la rete virtuale di Azure, che include un sito a sito o rete privata virtuale (VPN) site-to-point tooseamlessly di componente in grado di connettersi a macchine virtuali di Azure e computer locale. Questo componente VPN è stato possibile abilitare anche membro di dominio locale, tooaccess computer un dominio di Active Directory di Windows Server i cui controller di dominio sono ospitati esclusivamente in macchine virtuali di Azure. È importante toonote, tuttavia, se hello VPN non riesce, l'autenticazione e altre operazioni che dipendono da Windows Server Active Directory avrà inoltre esito negativo. Mentre gli utenti potrebbero essere in grado di toosign utilizzando le credenziali memorizzate nella cache esistente, tutti i peer-to-peer o tentativi di autenticazione client-server per cui i ticket hanno ancora toobe emessi o risultano non aggiornati avranno esito negativo.

Vedere [rete virtuale](http://azure.microsoft.com/documentation/services/virtual-network/) per un video dimostrativo e un elenco di esercitazioni dettagliate, tra cui [configurare una VPN Site-to-Site nel portale di Azure hello](../vpn-gateway/vpn-gateway-site-to-site-create.md).

> [!NOTE]
> È anche possibile distribuire Active Directory di Windows Server in una rete virtuale di Azure senza connettività a una rete locale. Hello in questo argomento, tuttavia, si presuppone che una rete virtuale di Azure viene utilizzata in quanto fornisce funzionalità che sono essenziali tooWindows Server di indirizzamento IP.
> 
> 

### <a name="static-ip-addresses-must-be-configured-with-azure-powershell"></a>Gli indirizzi IP statici devono essere configurati con Azure PowerShell.
Gli indirizzi dinamici vengono allocati per impostazione predefinita, ma utilizzano invece tooassign di cmdlet Set-AzureStaticVNetIP hello un indirizzo IP statico. L'indirizzo IP statico impostato sarà mantenuto durante la correzione del servizio e l'arresto o il riavvio della macchina virtuale. Per altre informazioni, vedere il blog relativo all' [indirizzo IP interno statico per le macchine virtuali](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/).

## <a name="BKMK_Glossary"></a>Termini e definizioni
di seguito Hello è un elenco non esaustivo di termini per varie tecnologie di Azure che verranno fatto riferimento in questo articolo.

* **Macchine virtuali di Azure**: offerta IaaS hello in Azure che consente ai clienti toodeploy macchine virtuali che eseguono praticamente qualsiasi tradizionalmente locale carico di lavoro server.
* **Rete virtuale di Azure**: hello tootheir un servizio in Azure che consente ai clienti di creare e gestire reti virtuali in Azure e collegarle in modo sicuro di rete su infrastruttura di rete locale tramite una rete privata virtuale (VPN).
* **Indirizzo IP virtuale**: indirizzo di un indirizzo IP con connessione internet che è non è associato tooa specifico computer o alla rete scheda di interfaccia. Servizi cloud viene assegnato un indirizzo IP virtuale per ricevere il traffico di rete che viene reindirizzato tooan macchina virtuale di Azure. Un indirizzo IP virtuale è una proprietà di un servizio cloud che può contenere una o più macchine virtuali. Una rete virtuale di Azure può anche contenere uno o più servizi cloud. Gli indirizzi IP virtuali forniscono funzionalità native di bilanciamento del carico.
* **Indirizzo IP dinamico**: indirizzo IP hello è solo interno. Si deve essere configurato come un indirizzo IP statico (usando il cmdlet Set-AzureStaticVNetIP hello) per le macchine virtuali che ospitano i ruoli del server controller di dominio/DNS hello.
* **La correzione del servizio**: hello processo in cui Azure restituisce automaticamente tooa un servizio in esecuzione è stato nuovamente dopo rileva che il servizio hello non è riuscito. Correzione del servizio è uno degli aspetti di hello di Azure che supporta la disponibilità e resilienza. Sebbene poco probabile, risultato hello in un servizio intervento di correzione per un controller di dominio in esecuzione in una macchina virtuale è il riavvio non pianificato di tooan simile, ma con pochi effetti collaterali:
  
  * scheda di rete virtuale Hello in hello VM verrà modificato
  * indirizzo MAC della scheda di rete virtuale hello Hello verrà modificato
  * Hello ID CPU/processore di hello VM verrà modificato
  * Hello configurazione IP della scheda di rete virtuale hello non cambierà purché hello VM è la rete virtuale associata tooa e hello indirizzo IP della macchina virtuale è statico.
  
  Nessuno di questi comportamenti influisce sul Windows Server Active Directory poiché non dipende dall'ID CPU/processore o di indirizzo MAC hello e tutte le distribuzioni di Windows Server Active Directory in Azure sono consigliate toobe eseguire in una rete virtuale di Azure, come illustrato in precedenza .

## <a name="is-it-safe-toovirtualize-windows-server-active-directory-domain-controllers"></a>È sicuro toovirtualize i controller di dominio Active Directory di Windows Server?
La distribuzione di controller di dominio Windows Server Active Directory in macchine virtuali di Azure è soggetto toohello stesse linee guida per l'esecuzione di controller di dominio locale in una macchina virtuale. L'esecuzione di controller di dominio virtualizzati è una procedura sicura, a condizione di seguire le linee guida per il backup e il ripristino dei controller di dominio. Per altre informazioni su vincoli e linee guida per l'esecuzione di controller di dominio virtualizzati, vedere [Esecuzione di controller di dominio in Hyper-V](https://technet.microsoft.com/library/dd363553).

Gli hypervisor forniscono o considerano insignificanti tecnologie che possono causare problemi a molti sistemi distribuiti, tra cui Active Directory di Windows Server. Ad esempio, in un server fisico, è possibile clonare un disco o utilizzare lo stato di metodi non supportati tooroll hello indietro di un server, incluso l'utilizzo di reti SAN e così via, ma questa operazione in un server fisico è molto più difficile del ripristino di uno snapshot della macchina virtuale in un hypervisor. Azure offre funzionalità che possono comportare hello stessa condizione indesiderata. Ad esempio, si devono copiare file VHD di controller di dominio anziché eseguire backup regolari perché il loro ripristino può comportare una funzionalità di ripristino dello snapshot di toousing situazione simile.

Tramite questi rollback vengono introducono bolle USN che possono comportare stati divergenti toopermanently tra i controller di dominio. Questa condizione può comportare problemi come i seguenti:

* Oggetti residui
* Password incoerenti
* Valori di attributi incoerenti
* Mancata corrispondenza dello schema se viene eseguito il rollback di master schema hello

Per altre informazioni sull'impatto sui controller di dominio, vedere la sezione relativa a [USN e rollback di USN](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv.aspx#usn_and_usn_rollback).

A partire da Windows Server 2012, [misure di sicurezza aggiuntive vengono compilate nel dominio Active Directory tooAD](https://technet.microsoft.com/library/hh831734.aspx). Queste misure di sicurezza aiutano a proteggere i controller di dominio virtualizzati dai suddetti problemi hello, purché piattaforma hypervisor sottostante hello supporta VM-GenerationID. Azure supporta VM-GenerationID, ciò significa che i controller di dominio che eseguono Windows Server 2012 o macchine virtuali di Azure in un secondo momento misure di sicurezza aggiuntive di hello.

> [!NOTE]
> È necessario arrestare e riavviare una macchina virtuale in esecuzione ruolo controller di dominio hello in Azure nel sistema operativo guest di hello anziché hello **Arresta** opzione hello Azure Portal. Oggi, l'utilizzo di hello tooshut portale verso il basso di una macchina virtuale comporta hello VM toobe deallocato. Una macchina virtuale deallocata ha il vantaggio di hello di non incorrere in addebiti, ma reimposta anche hello VM-GenerationID, questo non è auspicabile per un controller di dominio. Quando hello VM-GenerationID viene reimpostato, viene inoltre reimpostato hello invocationID del database di hello AD DS, hello pool di RID viene ignorato e SYSVOL è contrassegnato come non autorevole. Per ulteriori informazioni, vedere [tooActive introduzione Directory Domain Services (AD DS) Virtualization](https://technet.microsoft.com/library/hh831734.aspx) e [virtualizzazione sicura di DFSR](http://blogs.technet.com/b/filecab/archive/2013/04/05/safely-virtualizing-dfsr.aspx).
> 
> 

## <a name="why-deploy-windows-server-ad-ds-on-azure-virtual-machines"></a>Perché distribuire Servizi di dominio Active Directory di Windows Server in macchine virtuali di Azure
Molti scenari di distribuzione di Servizi di dominio Active Directory di Windows Server sono particolarmente adatti per la distribuzione come VM in Azure. Si supponga, ad esempio, che si dispone di una società in Europa in cui è necessario tooauthenticate utenti in una posizione remota in Asia. Hello aziendale non è in precedenza distribuito Windows Server Active Directory i controller di dominio in Asia a causa dei costi toohello toodeploy e delle competenze limitate toomanage hello server post-distribuzione. Di conseguenza, le richieste di autenticazione dall'Asia vengono gestite da controller di dominio in Europa con risultati non ottimali. In questo caso, è possibile distribuire un controller di dominio in una macchina virtuale che è stato specificato deve essere eseguita all'interno di hello Data Center di Azure in Asia. Connessione di rete virtuale di Azure connessa direttamente posizione remota toohello migliorerà le prestazioni di autenticazione di tooan di controller di dominio.

Azure è inoltre ideale come siti di ripristino di emergenza un sostituto toootherwise emergenza costosi. Hello costo relativamente basso dell'hosting di un numero esiguo di controller di dominio e una singola rete virtuale in Azure rappresenta un'alternativa interessante.

Infine, è opportuno toodeploy un'applicazione di rete in Azure, ad esempio SharePoint, che richiede Windows Server Active Directory, ma non ha dipendenze hello di rete o hello aziendali Windows Server Active Directory locale. In questo caso, la distribuzione di una foresta isolata in Azure toomeet hello SharePoint requisiti del server è ottimale. Nuovamente, distribuzione di applicazioni di rete che richiedono la connettività toohello on-premise di rete e hello Active Directory aziendale è anche supportata.

> [!NOTE]
> Poiché viene fornita una connessione di livello 3, hello componente VPN che offre connettività tra una rete virtuale di Azure e una rete locale può anche abilitare server membri che eseguono locale tooleverage controller di dominio eseguiti come macchine virtuali di Azure in Azure rete virtuale. Ma se hello VPN è disponibile, la comunicazione tra computer locali e i controller di dominio basati su Azure non funzioneranno, con l'autenticazione e vari altri errori.  
> 
> 

## <a name="contrasts-between-deploying-windows-server-active-directory-domain-controllers-on-azure-virtual-machines-versus-on-premises"></a>Differenze tra la distribuzione di controller di dominio Active Directory di Windows Server in macchine virtuali di Azure e in locale
* Per qualsiasi scenario di distribuzione di Windows Server Active Directory che include più di una singola macchina virtuale, è necessario toouse una rete virtuale di Azure per la coerenza di indirizzi IP. Questa guida presuppone che i controller di dominio siano eseguiti in una rete virtuale di Azure.
* Come per i controller di dominio locali, è consigliabile usare indirizzi IP statici. Un indirizzo IP statico può essere configurato solo tramite Azure PowerShell. Per altre informazioni, vedere il blog relativo all' [indirizzo IP interno statico per le macchine virtuali](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/) . Se si dispone di sistemi di monitoraggio o altre soluzioni che consentono di controllare per la configurazione degli indirizzi IP statici all'interno del sistema operativo guest di hello, è possibile assegnare hello stesso IP indirizzo toohello rete scheda delle proprietà statiche di hello macchina virtuale. Tuttavia in considerazione che della scheda di rete hello verrà annullata hello VM viene sottoposta a correzione del servizio o se è stato arrestato nel portale di hello e relativo indirizzo viene deallocato. In tal caso, indirizzo IP statico hello guest hello sarà necessario toobe reimpostare.
* Distribuzione di macchine virtuali in una rete virtuale non implica (né richiede) rete locale di connettività tooan back; rete virtuale Hello consente semplicemente il possibilità. È necessario creare una rete virtuale per le comunicazioni private tra Azure e la rete locale. È necessario un endpoint VPN nella rete locale hello toodeploy. Hello VPN viene aperta dalla rete locale toohello Azure. Per ulteriori informazioni, vedere [Panoramica di rete virtuale](../virtual-network/virtual-networks-overview.md) e [configurare una VPN Site-to-Site nel portale di Azure hello](../vpn-gateway/vpn-gateway-site-to-site-create.md).

> [!NOTE]
> Un'opzione troppo[creare una VPN point-to-site](../vpn-gateway/vpn-gateway-point-to-site-create.md) è disponibile tooconnect singoli computer basati su Windows direttamente tooan rete virtuale di Azure.
> 
> 

* Indipendentemente dal fatto che venga creata o meno una rete virtuale, Azure addebita il costo del traffico in uscita ma non di quello in entrata. Le diverse opzioni di progettazione di Active Directory di Windows Server possono influire sulla quantità di traffico in uscita generato da una distribuzione. Ad esempio, la distribuzione di un controller di dominio di sola lettura limita il traffico in uscita perché non viene replicato. Ma decisione hello toodeploy RODC toobe soppesata tooperform necessità hello è necessario scrivere operazioni nel controller di dominio di hello e hello [compatibilità](https://technet.microsoft.com/library/cc755190) che applicazioni e servizi nel sito hello abbiano RODC. Per altre informazioni sugli addebiti per il traffico, vedere [Prezzi di Azure](http://azure.microsoft.com/pricing/).
* Mentre il controllo completo sulla quale toouse risorse server per le macchine virtuali in locale, ad esempio RAM, dimensione del disco e così via, in Azure è necessario selezionare da un elenco di dimensioni server preconfigurate. Per un controller di dominio, è necessario un disco dati nel disco del sistema operativo toohello aggiunta nel database di Windows Server Active Directory hello toostore ordine.

## <a name="can-you-deploy-windows-server-ad-fs-on-azure-virtual-machines"></a>Possibilità di distribuire AD FS di Windows Server in macchine virtuali di Azure
Sì, è possibile distribuire ADFS di Windows Server in macchine virtuali di Azure e hello [procedure consigliate per la distribuzione di ADFS](https://technet.microsoft.com/library/dn151324.aspx) locale si applicano ugualmente distribuzione FS tooAD in Azure. Ma alcune procedure consigliate di hello, ad esempio il bilanciamento del carico e disponibilità elevata, richiedono tecnologie superiori rispetto alle quali offerte da ADFS. È necessario specificare dall'infrastruttura sottostante hello. Si esamineranno alcune di queste procedure consigliate e si vedrà come attuarle usando VM di Azure e una rete virtuale di Azure.

1. **Non esporre mai i server (STS) il servizio token di sicurezza direttamente toohello Internet.**
   
    Questo è importante perché hello STS rilascia token di sicurezza. Di conseguenza, i server di servizio token di sicurezza, ad esempio i server ADFS devono essere gestiti con hello stesso livello di protezione di un controller di dominio. Se un servizio token di sicurezza è compromesso, gli utenti malintenzionati hanno hello possibilità tooissue i token di accesso potenzialmente contenenti attestazioni di loro scelta applicazioni di terze parti toorelying e altri server STS nelle organizzazioni trusting.
2. **Distribuire controller di dominio Active Directory per tutti i domini utente nella stessa rete i server ADFS hello hello.**
   
    I server ADFS usano gli utenti tooauthenticate di servizi di dominio Active Directory. Si consiglia di controller di dominio toodeploy sulla stessa rete come server di hello AD FS hello. In questo modo la continuità aziendale nel caso in cui il collegamento hello tra hello rete di Azure e la rete locale viene interrotta e consente di migliorare le prestazioni per gli account di accesso e una latenza più bassa.
3. **Distribuire più nodi ADFS per disponibilità elevata e bilanciamento del carico hello.**
   
    Nella maggior parte dei casi, l'errore hello di un'applicazione abilitata da ADFS è accettabile perché le applicazioni di hello che richiedono i token di sicurezza sono spesso mission-critical. Di conseguenza, e poiché ADFS ora risiede in hello percorso critico tooaccessing ad applicazioni cruciali, servizio di hello AD FS deve essere a disponibilità elevata mediante più proxy AD FS e i server ADFS. distribuzione tooachieve delle richieste, servizi di bilanciamento del carico vengono in genere distribuiti davanti ai proxy ADFS hello Active Directory e i server ADFS hello.
4. **Distribuire uno o più nodi Proxy applicazione Web per l'accesso a Internet.**
   
    Quando gli utenti devono tooaccess applicazioni protette dal servizio di hello AD FS, hello AD FS servizio esigenze toobe disponibili hello internet. Questo risultato viene ottenuto tramite la distribuzione del servizio Proxy applicazione Web di hello. È consigliabile toodeploy più di un nodo per scopi di hello di disponibilità elevata e bilanciamento del carico.
5. **Limitare l'accesso dalle risorse di rete toointernal nodi Proxy applicazione Web hello.**
   
    gli utenti esterni di tooallow tooaccess AD FS da hello internet, è necessario nodi Proxy applicazione Web toodeploy (o Proxy ADFS nelle versioni precedenti di Windows Server). Hello proxy applicazione Web, i nodi sono direttamente esposti toohello Internet. Non sono necessari toobe appartenenti a un dominio e sono solo necessario accedere ai server ADFS toohello AD sulla porta TCP 443 e 80. È consigliabile che tooall comunicazione altri computer (in particolare i controller di dominio) è bloccato.
   
    Questa configurazione si ottiene in genere in locale per mezzo di una rete perimetrale. I firewall utilizzano avviene in modalità di traffico toorestrict operazione dalla rete locale di hello DMZ toohello (solo il traffico da hello specificato gli indirizzi IP e su porte è consentito e tutti gli altri il traffico viene bloccato).

Hello diagramma seguente mostra un tradizionale distribuzione di ADFS in locale.

![Diagramma di una distribuzione tradizionale di Active Directory Federation Services locale](media/active-directory-deploying-ws-ad-guidelines/ADFS_onprem.png)

Tuttavia, poiché Azure non fornisce funzionalità firewall native complete, è necessario il traffico toorestrict toobe utilizzato altre opzioni. Hello nella tabella seguente illustra ogni opzione e i relativi vantaggi e svantaggi.

| Opzione | Vantaggio | Svantaggio |
| --- | --- | --- |
| [ACL di rete di Azure](../virtual-network/virtual-networks-acl.md) |Configurazione iniziale meno costosa e più semplice. |Configurazione di ACL di rete aggiuntiva necessaria se le nuove macchine virtuali vengono aggiunte toohello distribuzione |
| [Barracuda NG firewall](https://www.barracuda.com/products/ngfirewall) |Modalità operativa di tipo elenco elementi consentiti, non richiede alcuna configurazione di ACL di rete. |Costi e complessità maggiori per la configurazione iniziale. |

passaggi di alto livello di Hello toodeploy AD FS in questo caso sono come segue:

1. Creare una rete virtuale con connettività cross-premise usando una VPN o [ExpressRoute](http://azure.microsoft.com/services/expressroute/).
2. Distribuire controller di dominio sulla rete virtuale hello. Questo passaggio è facoltativo ma consigliato.
3. Distribuire i server ADFS di dominio nella rete virtuale hello.
4. Creare un [set con bilanciamento del carico interno](http://azure.microsoft.com/blog/internal-load-balancing/) che include i server ADFS hello e si usa un nuovo indirizzo IP privato all'interno di rete virtuale hello (un indirizzo IP dinamico).
   
   1. Aggiornare DNS toocreate hello FQDN toopoint toohello (dinamico) indirizzo IP privato del set interno con carico bilanciato hello.
5. Creare un servizio cloud (o una rete virtuale separata) per hello nodi Proxy applicazione Web.
6. Distribuire i nodi Proxy applicazione Web hello nel servizio cloud hello o rete virtuale
   
   1. Creare un set esterno con carico bilanciato che include nodi Proxy applicazione Web hello.
   2. Aggiornare hello esterna DNS name (FQDN) toopoint toohello cloud servizio indirizzo IP pubblico (indirizzo IP virtuale hello).
   3. Configurare AD FS proxy toouse hello FQDN che corrisponde a set interno con carico bilanciato toohello per i server di hello AD FS.
   4. Aggiornare i siti web basati su attestazioni toouse hello FQDN esterno per il provider di attestazioni.
7. Limitare l'accesso tra computer tooany Proxy applicazione Web nella rete virtuale di hello AD FS.

traffico toorestrict, set di bilanciamento del carico hello servizio di bilanciamento del carico interno di Azure hello deve toobe configurata per solo tooTCP traffico le porte 80 e 443 e tutti gli altri traffico toohello dinamico indirizzo IP interno del set con carico bilanciato hello viene eliminato.

![Diagramma di ACL di rete AD FS con porte TCP 443 e 80 consentite.](media/active-directory-deploying-ws-ad-guidelines/ADFS_ACLs.png)

Server di traffico toohello AD FS sarebbe consentito solo da hello seguenti origini:

* servizio di bilanciamento del carico interno di Azure Hello.
* indirizzo IP di Hello di amministratore di rete locale hello.

> [!WARNING]
> progettazione di Hello deve impedire ad altre macchine virtuali nella rete virtuale di Azure hello o a tutti i percorsi nella rete locale hello nodi Proxy applicazione Web. Che può essere effettuata da configurare regole firewall nel dispositivo locale hello per le connessioni Expressroute o il dispositivo VPN hello per le connessioni VPN da sito a sito.
> 
> 

Un'opzione toothis svantaggio è hello necessità tooconfigure hello ACL di rete per più dispositivi, tra cui bilanciamento del carico interno, il server ADFS hello e qualsiasi altro server che vengono aggiunte toohello di rete virtuale. Se un dispositivo viene aggiunto toohello distribuzione senza configurare tooit traffico toorestrict ACL di rete, l'intera distribuzione di hello può essere a rischio. Se gli indirizzi IP hello di nodi Proxy applicazione Web hello cambiano, è necessario reimpostare l'ACL di rete hello (ovvero proxy hello deve essere configurato toouse [statico gli indirizzi IP dinamici](http://azure.microsoft.com/blog/static-internal-ip-address-for-virtual-machines/)).

![AD FS in Azure con ACL di rete.](media/active-directory-deploying-ws-ad-guidelines/ADFS_Azure.png)

Un'altra opzione consiste hello toouse [Barracuda NG Firewall](https://www.barracuda.com/products/ngfirewall) traffico toocontrol accessorio tra i server proxy ADFS e hello AD FS. Questa opzione è conforme alle procedure consigliate per la sicurezza e la disponibilità elevata e richiede attività di amministrazione minori dopo l'installazione iniziale di hello perché hello Barracuda NG Firewall offre una modalità elenco amministrazione del firewall e può essere installato direttamente in una rete virtuale di Azure. Che consente di eliminare ACL di rete tooconfigure hello necessario ogni volta che un nuovo server viene aggiunto toohello distribuzione. Questa opzione comporta tuttavia maggiori costi e complessità per la distribuzione iniziale.

In questo caso, vengono distribuite due reti virtuali invece di una, ad esempio rete virtuale 1 e rete virtuale 2. VNet1 contiene proxy hello e VNet2 contiene ruoli STS hello e hello rete connessione toohello indietro alla rete aziendale. VNet1 è pertanto fisicamente (benché virtualmente) isolata dalla prospettiva di VNet2 e, a sua volta, dalla rete aziendale hello. VNet1 è quindi connesso tooVNet2 utilizzando una tecnologia di tunneling speciale nota come trasporto Independent Network Architecture (TINA). il tunnel TINA Hello è collegato tooeach di reti virtuali di hello utilizzando un dispositivo Barracuda NG firewall, ovvero un dispositivo Barracuda su ciascuna delle reti virtuali hello.  Per garantire disponibilità elevata, è consigliabile distribuire due dispositivi barracuda su ogni rete virtuale. uno attivo, hello altro passivo. Offrono funzionalità firewall complesse che permettono di operazione hello toomimic di una rete Perimetrale locale tradizionale in Azure.

![AD FS in Azure con firewall.](media/active-directory-deploying-ws-ad-guidelines/ADFS_Azure_firewall.png)

Per ulteriori informazioni, vedere [ADFS: estendere un toohello applicazione front-end locale in grado di riconoscere attestazioni Internet](#BKMK_CloudOnlyFed).

### <a name="an-alternative-tooad-fs-deployment-if-hello-goal-is-office-365-sso-alone"></a>Una distribuzione alternativo tooAD ADFS se l'obiettivo di hello è solo SSO di Office 365
Se l'obiettivo è solo tooenable Accedi per Office 365 è completa di un'altra alternativa toodeploying AD ADFS. In tal caso, è possibile semplicemente distribuire DirSync con sincronizzazione password in locale e ottenere hello stesso risultato finale con una complessità di distribuzione minima, perché questo approccio non richiede ADFS o Azure.

Hello nella tabella seguente confronta funzionamento dei processi di accesso hello con e senza distribuzione di ADFS.

| Single Sign-On in Office 365 con AD FS e DirSync | Lo stesso Single Sign-On in Office 365 con DirSync e sincronizzazione password |
| --- | --- |
| 1. hello utente effettua l'accesso alla rete aziendale tooa e viene autenticato tooWindows Server Active Directory. |1. hello utente effettua l'accesso alla rete aziendale tooa e viene autenticato tooWindows Server Active Directory. |
| 2. utente di hello tenta tooaccess Office 365 (So @contoso.com). |2. utente di hello tenta tooaccess Office 365 (So @contoso.com). |
| 3. Office 365 reindirizza l'utente di hello tooAzure Active Directory. |3. Office 365 reindirizza l'utente di hello tooAzure Active Directory. |
| 4. Poiché Azure AD non è possibile eseguire l'autenticazione utente hello e rileva l'esistenza di una relazione di trust con ADFS in locale, viene reindirizzato hello utente tooAD ADFS. |4. Azure AD non può accettare direttamente i ticket Kerberos e non esiste alcuna relazione di trust, pertanto richiede che l'utente hello immettere le credenziali. |
| 5. hello utente invia un Kerberos ticket toohello AD STS di ADFS. |5. hello immessi hello stessa password locale e Azure AD la convalida rispetto al nome utente hello e una password sincronizzata tramite DirSync. |
| 6. ADFS Trasforma hello toohello ticket Kerberos richiesto attestazione/formato di token e reindirizza hello utente tooAzure Active Directory. |6. Azure AD reindirizza hello utente tooOffice 365. |
| 7. autenticazione dell'utente di hello tooAzure AD (si verifica un'ulteriore trasformazione). |7. hello utente possa accedere tooOffice 365 e OWA utilizzando il token di Azure AD hello. |
| 8. Azure AD reindirizza hello utente tooOffice 365. | |
| 9. utente hello viene connesso automaticamente tooOffice 365. | |

In hello Office 365 con DirSync con sincronizzazione delle password (non ADFS), single sign-on viene sostituito dallo "stesso sign-on" dove "stesso" significa che gli utenti devono immettere nuovamente le stesse credenziali locali per l'accesso a Office 365. Si noti che questi dati possono essere memorizzati da toohelp browser dell'utente hello ridurre le richieste successive.

### <a name="additional-food-for-thought"></a>Altri elementi di riflessione
* Se si distribuisce un proxy AD FS in una macchina virtuale di Azure, server di connettività toohello AD FS. Se sono locali, è consigliabile utilizzare hello site-to-site VPN connettività fornita da toocommunicate di nodi Proxy applicazione Web di hello rete virtuale tooallow hello con i server ADFS.
* Se si distribuisce un server AD FS su virtuale di Azure del computer, controller di dominio Active Directory Server tooWindows connettività, archivi di attributi e i database di configurazione è necessari e può anche richiedere ExpressRoute o una connessione VPN da sito a sito tra la rete hello Azure virtuale hello e rete locale.
* Gli addebiti vengono applicati traffico tooall da macchine virtuali di Azure (traffico in uscita). Se il costo è un fattore determinante hello, è consigliabile toodeploy nodi di Proxy applicazione Web hello in Azure, lasciando i server ADFS hello in locale. Se i server di hello AD ADFS vengono distribuiti nelle macchine virtuali Azure anche, costi aggiuntivi saranno sostenuti tooauthenticate locale utenti. Traffico in uscita comporta un costo indipendentemente dal fatto che attraversi hello ExpressRoute o hello connessione site-to-site VPN.
* Se si decide server nativo funzionalità Bilanciamento del carico di Azure toouse per la disponibilità elevata dei server ADFS, si noti che il bilanciamento del carico offre probe vengono utilizzati toodetermine hello integrità delle macchine virtuali hello all'interno del servizio cloud hello. In caso di hello macchine virtuali di Azure (come i ruoli di lavoro o tooweb anziché), è necessario utilizzare un probe personalizzato poiché agente hello risponde probe predefiniti toohello non è presente nelle macchine virtuali di Azure. Per semplicità, è possibile utilizzare un probe TCP personalizzato, questo richiede solo che una connessione TCP (un segmento TCP SYN inviato e ha risposto toowith un segmento TCP SYN ACK) sia l'integrità della macchina virtuale toodetermine stabilita correttamente. È possibile configurare hello probe personalizzato toouse qualsiasi toowhich porta TCP che le macchine virtuali sono attivamente in ascolto.

> [!NOTE]
> Macchine virtuali che richiedono hello tooexpose che stesso insieme di porte direttamente toohello Internet (ad esempio la porta 80 e 443) non è possibile condividere hello nello stesso servizio cloud. Si raccomanda di conseguenza, creare un servizio cloud dedicato per i server ADFS di Windows Server in ordine tooavoid possibili sovrapposizioni tra i requisiti delle porte per un'applicazione e ADFS di Windows Server.
> 
> 

## <a name="deployment-scenarios"></a>Scenari di distribuzione
Hello seguente sezione vengono presentate distribuzione comuni scenari toodraw attenzione tooimportant considerazioni che devono essere presi in considerazione. Ogni scenario include i collegamenti toomore dettagli decisioni hello e tooconsider fattori.

1. [Servizi di dominio Active Directory: distribuire un'applicazione compatibile con Servizi di dominio Active Directory senza requisiti per la connettività di rete aziendale](#BKMK_CloudOnly)
   
    Ad esempio, un servizio SharePoint con connessione Internet viene distribuito in una macchina virtuale di Azure. un'applicazione Hello non presenta dipendenze sulle risorse di rete aziendale. Hello applicazione richiedono servizi di dominio di Windows Server Active Directory, ma non richiede hello DS di Windows Server Active Directory aziendale.
2. [ADFS: Estendere un toohello applicazione front-end locale in grado di riconoscere attestazioni Internet](#BKMK_CloudOnlyFed)
   
    Ad esempio, un'applicazione in grado di riconoscere attestazioni distribuita correttamente in locale e utilizzata dagli utenti aziendali deve toobecome accessibile da Internet hello. un'applicazione Hello deve toobe accessibili direttamente tramite Internet hello ai partner aziendali tramite le relative identità aziendali sia agli utenti aziendali esistenti.
3. [Servizi di dominio Active Directory: Distribuire un'applicazione di Windows Server AD DS-aware che richiede una rete aziendale toohello di connettività](#BKMK_HybridExt)
   
    Ad esempio, un'applicazione compatibile con LDAP, che supporta l'autenticazione integrata di Windows e usa Servizi di dominio Active Directory di Windows Server come archivio per i dati di configurazione e del profilo utente, viene distribuita in una macchina virtuale di Azure. È consigliabile che hello tooleverage di applicazione hello DS di Windows Server Active Directory aziendale esistente e fornire accesso single sign-on. un'applicazione Hello non è in grado di riconoscere attestazioni.

### <a name="BKMK_CloudOnly"></a>1. Servizi di dominio Active Directory: distribuire un'applicazione compatibile con Servizi di dominio Active Directory senza requisiti per la connettività di rete aziendale
![Distribuzione di Servizi di dominio Active Directory solo cloud](media/active-directory-deploying-ws-ad-guidelines/ADDS_cloud.png)
**Figura 1**

#### <a name="description"></a>Descrizione
SharePoint è distribuito in una macchina virtuale di Azure e un'applicazione hello non ha dipendenze da risorse di rete aziendale. Hello applicazione richiedono servizi di dominio Windows Server Active Directory ma non *non* richiedono hello DS di Windows Server Active Directory aziendale. Nessun Kerberos o trust federativi sono necessari poiché gli utenti vengono effettuati automaticamente tramite un'applicazione hello nel dominio hello servizi di dominio di Windows Server Active Directory che è ospitato anche in cloud hello in macchine virtuali di Azure.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>Considerazioni sullo scenario e come aree tecnologiche applicano toohello scenario
* [Topologia di rete](#BKMK_NetworkTopology): creare una rete virtuale di Azure senza connettività cross-premise, nota anche come connettività da sito a sito.
* [Configurazione della distribuzione di un controller di dominio](#BKMK_DeploymentConfig): distribuire un nuovo controller di dominio in una nuova foresta Active Directory di Windows Server a dominio singolo. Questo metodo deve essere distribuito insieme ai server DNS di Windows hello.
* [Topologia del sito di Windows Server Active Directory](#BKMK_ADSiteTopology): utilizza sito di Windows Server Active Directory predefinito hello (tutti i computer saranno in nome-predefinito-primo-sito).
* [Indirizzamento IP e DNS](#BKMK_IPAddressDNS):
  
  * Impostare un indirizzo IP statico per hello controller di dominio utilizzando cmdlet Set-AzureStaticVNetIP di Azure PowerShell hello.
  * Installare e configurare DNS di Windows Server nei controller di dominio hello in Azure.
  * Configurare le proprietà di rete virtuale hello con nome hello e l'indirizzo IP di macchina virtuale che ospita i ruoli del server DNS e controller di dominio hello hello.
* [Catalogo globale](#BKMK_GC): hello primo controller di dominio nella foresta hello deve essere un server di catalogo globale. Controller di dominio aggiuntivi deve essere configurato anche come cataloghi globali perché in una foresta a dominio singolo catalogo globale hello non richiede operazioni aggiuntive da hello controller di dominio.
* [Posizione del database hello servizi di dominio di Windows Server Active Directory e SYSVOL](#BKMK_PlaceDB): aggiungere un tooDCs disco dati in esecuzione come macchine virtuali di Azure in ordine toostore hello Active Directory di Windows Server database, registri e SYSVOL.
* [Backup e ripristino](#BKMK_BUR): stabilire dove si desidera toostore backup dello stato del sistema. Se necessario, aggiungere un altro disco toohello macchina virtuale controller di dominio toostore backup dei dati.

### <a name="BKMK_CloudOnlyFed"></a>2 ADFS: estendere un toohello applicazione front-end locale in grado di riconoscere attestazioni Internet
![Federazione con connettività cross-premise](media/active-directory-deploying-ws-ad-guidelines/Federation_xprem.png)
**Figura 2**

#### <a name="description"></a>Descrizione
Un'applicazione in grado di riconoscere attestazioni distribuita correttamente in locale e utilizzata da utenti aziendali esigenze toobecome accessibile direttamente da Internet hello. un'applicazione Hello funge da un database SQL tooa di front-end web in cui memorizza i dati. Hello SQL Server utilizzato da un'applicazione hello sono inoltre presenti nella rete aziendale hello. Due ruoli STS ADFS di Windows Server Active Directory e un bilanciamento del carico sono stati distribuiti in locale tooprovide accesso toohello aziendale gli utenti. a questo punto l'applicazione Hello deve toobe inoltre accessibile direttamente su Internet hello ai partner aziendali tramite le relative identità aziendali sia agli utenti aziendali esistenti.

Toosimplify un impegno e alle esigenze di distribuzione e configurazione soddisfa hello di questo nuovo requisito, si è deciso che altre due web server front-end e due server proxy ADFS di Windows Server installato in macchine virtuali di Azure. Tutte le quattro macchine virtuali sarà esposto direttamente toohello Internet e verrà fornita la rete locale di connettività toohello tramite la funzionalità VPN da sito a sito della rete virtuale Azure.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>Considerazioni sullo scenario e come aree tecnologiche applicano toohello scenario
* [Topologia di rete](#BKMK_NetworkTopology): creare una rete virtuale di Azure e [configurare la connettività cross-premise](../vpn-gateway/vpn-gateway-site-to-site-create.md).
  
  > [!NOTE]
  > Per ognuno dei certificati di ADFS di Windows Server hello, verificare che hello URL definito nel modello di certificato hello e certificati risultanti hello sia raggiungibile da istanze di hello ADFS di Windows Server in esecuzione in Azure. Tale operazione potrebbe richiedere tooparts connettività cross-premise dell'infrastruttura PKI. Ad esempio se l'endpoint di CRL hello è basata su LDAP e ospitati esclusivamente in locale, quindi la connettività cross-premise obbligatorio. Se ciò non è opportuno, potrebbe essere necessario toouse certificati emessi da un'autorità di certificazione i cui CRL sono accessibili su Internet hello.
  > 
  > 
* [Configurazione di servizi cloud](#BKMK_CloudSvcConfig): assicurarsi di avere due servizi cloud per fornire due indirizzi IP virtuali con carico bilanciato. indirizzo IP virtuale Hello del primo servizio cloud sarà indirizzato toohello proxy di ADFS di Windows Server due macchine virtuali sulle porte 80 e 443. Hello proxy ADFS di Windows Server che le macchine virtuali saranno toopoint toohello indirizzo IP configurato di hello locale bilanciamento del carico che risulterà hello ruoli STS ADFS di Windows Server Active Directory. indirizzo IP virtuale Hello del secondo servizio cloud verrà indirizzato toohello due macchine virtuali front-end web hello nuovamente sulle porte 80 e 443. Configurare un probe personalizzato tooensure hello bilanciamento del carico venga indirizzato solo il traffico toofunctioning ADFS di Windows Server proxy e web front-end le macchine virtuali.
* [Configurazione del server federativo](#BKMK_FedSrvConfig): configurare ADFS di Windows Server come protezione toogenerate federation server (STS) i token per la foresta di Active Directory di Windows Server hello creata nel cloud hello. Impostare relazioni di trust federative attestazioni del provider con partner diversi di hello desiderato tooaccept le identità e configurare le relazioni di trust relying party con diverse applicazioni hello desiderato toogenerate i token.
  
    In quasi tutti gli scenari i server proxy AD FS di Windows Server vengono distribuiti in una soluzione con connessione Internet per motivi di sicurezza, mentre le relative controparti federative di AD FS di Windows Server rimangono isolate dalla connettività Internet diretta. Indipendentemente dal proprio scenario di distribuzione, è necessario configurare il servizio cloud con un indirizzo IP virtuale che fornirà un indirizzo IP esposto pubblicamente e una porta che è in grado di tooload bilanciamento tra le due istanze STS ADFS di Windows Server o le istanze di proxy.
* [Configurazione della disponibilità elevata di Windows Server AD FS](#BKMK_ADFSHighAvail): è consigliabile toodeploy una farm ADFS di Windows Server con almeno due server per il failover e bilanciamento del carico. Si potrebbe essere necessario tooconsider utilizzando hello Windows Internal Database (WID) dei dati di configurazione di Windows Server AD FS e utilizzare hello interno funzionalità Bilanciamento del carico delle richieste in ingresso toodistribute Azure in server hello hello farm.

Per ulteriori informazioni, vedere hello [Guida alla distribuzione di Active Directory](https://technet.microsoft.com/library/cc753963).

### <a name="BKMK_HybridExt"></a>3. Servizi di dominio Active Directory: Distribuire un'applicazione di Windows Server AD DS-aware che richiede una rete aziendale toohello di connettività
![Distribuzione di Servizi di dominio Active Directory cross-premise](media/active-directory-deploying-ws-ad-guidelines/ADDS_xprem.png)
**Figura 3**

#### <a name="description"></a>Descrizione
Un'applicazione compatibile con LDAP viene distribuita in una macchina virtuale di Azure. Supporta l'autenticazione integrata di Windows e usa Servizi di dominio Active Directory di Windows Server come archivio per i dati di configurazione e del profilo utente. obiettivo di Hello per hello tooleverage di applicazione hello DS di Windows Server Active Directory aziendale esistente e fornire accesso single sign-on. un'applicazione Hello non è in grado di riconoscere attestazioni. Gli utenti devono inoltre l'applicazione hello tooaccess direttamente da Internet hello. toooptimize per prestazioni e costi, si è deciso di distribuire due controller di dominio aggiuntivi che fanno parte del dominio aziendale hello insieme a un'applicazione hello in Azure.

#### <a name="scenario-considerations-and-how-technology-areas-apply-toohello-scenario"></a>Considerazioni sullo scenario e come aree tecnologiche applicano toohello scenario
* [Topologia di rete](#BKMK_NetworkTopology): creare una rete virtuale di Azure con la [connettività cross-premise](../vpn-gateway/vpn-gateway-site-to-site-create.md).
* [Metodo di installazione](#BKMK_InstallMethod): distribuire controller di dominio di replica dal dominio di Windows Server Active Directory aziendale hello. Per un controller di dominio di replica, è possibile installare servizi di dominio di Windows Server Active Directory in hello VM e, facoltativamente, utilizzare hello installa da supporto funzionalità tooreduce hello quantità di dati che devono toobe replicati toohello nuovo controller di dominio durante l'installazione. Per un'esercitazione, vedere [Installazione di un controller di dominio Active Directory di replica in una rete virtuale di Azure](active-directory-install-replica-active-directory-domain-controller.md). Anche se si utilizza l'installazione da supporto, potrebbe essere più efficiente hello toobuild controller di dominio virtuale locale e spostare hello intero disco rigido virtuale (VHD) toohello cloud anziché replicare servizi di dominio di Windows Server Active Directory durante l'installazione. Per motivi di sicurezza, è consigliabile eliminare hello disco rigido virtuale dalla rete locale hello dopo che è stato copiato tooAzure.
* [Topologia del sito Active Directory di Windows Server](#BKMK_ADSiteTopology): creare un nuovo sito di Azure in Siti e servizi di Active Directory. Creare un hello di toorepresent di oggetto subnet rete virtuale di Azure Active Directory di Windows Server e aggiungere hello subnet toohello sito. Creare un nuovo collegamento di sito che include hello nuovo sito di Azure e il sito di hello in cui hello Azure endpoint VPN della rete virtuale si trova in ordine toocontrol e ottimizza tooand il traffico di Windows Server Active Directory da Azure.
* [Indirizzamento IP e DNS](#BKMK_IPAddressDNS):
  
  * Impostare un indirizzo IP statico per hello controller di dominio utilizzando cmdlet Set-AzureStaticVNetIP di Azure PowerShell hello.
  * Installare e configurare DNS di Windows Server nei controller di dominio hello in Azure.
  * Configurare le proprietà di rete virtuale hello con nome hello e l'indirizzo IP di macchina virtuale che ospita i ruoli del server DNS e controller di dominio hello hello.
* [Controller di dominio con distribuzione geografica](#BKMK_DistributedDCs): configurare reti virtuali aggiuntive in base alle esigenze. Se la topologia del sito di Active Directory richiede un controller di dominio in aree geografiche che corrispondono toodifferent Azure aree, rispetto a quelle desidera toocreate siti di Active Directory, di conseguenza.
* [I controller di dominio di sola lettura](#BKMK_RODC): È possibile distribuire un controller di dominio nel sito di Azure hello, a seconda dei requisiti per l'esecuzione le operazioni di scrittura su hello compatibilità hello e controller di dominio di applicazioni e servizi nel sito di hello con controller. Per ulteriori informazioni sulla compatibilità delle applicazioni, vedere hello [Guida compatibilità dell'applicazione controller di dominio di sola lettura](https://technet.microsoft.com/library/cc755190).
* [Catalogo globale](#BKMK_GC): i cataloghi globali sono necessari tooservice le richieste di accesso in foreste multidominio. Se non si distribuisce un catalogo globale nel sito di Azure hello, si incorrerà in costi di traffico in uscita come le richieste di autenticazione vengono generate query sui cataloghi globali in altri siti. toominimize che il traffico, è possibile abilitare la memorizzazione nella cache di hello Azure sito in Active Directory, siti e servizi di appartenenza a gruppi universali.
  
    Se si distribuisce un catalogo globale, configurare i collegamenti di sito e i costi di collegamenti di sito in modo che GC hello in hello Azure site non sia scelto come un controller di dominio di origine preferito da altri cataloghi globali che devono tooreplicate hello stesse partizioni di dominio parziali.
* [Posizione del database hello servizi di dominio di Windows Server Active Directory e SYSVOL](#BKMK_PlaceDB): aggiungere un tooDCs disco dati in esecuzione in macchine virtuali di Azure in ordine toostore hello Active Directory di Windows Server database, registri e SYSVOL.
* [Backup e ripristino](#BKMK_BUR): stabilire dove si desidera toostore backup dello stato del sistema. Se necessario, aggiungere un altro disco toohello macchina virtuale controller di dominio toostore backup dei dati.

## <a name="deployment-decisions-and-factors"></a>Decisioni e fattori relativi alla distribuzione
Questa tabella riepiloga le aree tecnologiche di Active Directory di Windows Server hello che sono interessate in scenari precedenti hello e hello corrispondente tooconsider decisioni, con collegamenti toomore seguito. Alcune aree tecnologiche potrebbero non essere applicabile tooevery scenario di distribuzione e alcune aree tecnologiche potrebbero essere uno scenario di distribuzione tooa prioritaria rispetto ad altre.

Ad esempio, se si distribuisce una controller di dominio di replica in una rete virtuale e la foresta dispone di un solo dominio, scegliendo toodeploy un server di catalogo globale in questo caso non sarà critica toohello scenario di distribuzione perché non creerà qualsiasi replica aggiuntive requisiti. In hello altra parte, se la foresta hello dispone di più domini, quindi hello decisione toodeploy un catalogo globale in una rete virtuale possono influire sulla larghezza di banda disponibile, prestazioni, l'autenticazione, ricerche nella directory e così via.

| Active Directory di Windows Server in macchine virtuali di Azure | Decisioni | Fattori |
| --- | --- | --- |
| [Topologia di rete](#BKMK_NetworkTopology) |Si crea una rete virtuale? |<li>Requisiti tooaccess alle risorse aziendali</li> <li>Autenticazione</li> <li>Account Management</li> |
| [Configurazione della distribuzione di un controller di dominio](#BKMK_DeploymentConfig) |<li>Distribuire una foresta separata senza trust?</li> <li>Distribuire una nuova foresta con federazione?</li> <li>Distribuire una nuova foresta con trust tra foreste di Active Directory di Windows Server o Kerberos?</li> <li>Estendere la foresta aziendale distribuendo una controller di dominio di replica?</li> <li>Estendere la foresta aziendale distribuendo un nuovo dominio figlio o albero di dominio?</li> |<li>Sicurezza</li> <li>Conformità</li> <li>Costi</li> <li>Resilienza e tolleranza di errore</li> <li>Compatibilità tra le versioni</li> |
| [Topologia del sito Active Directory di Windows Server](#BKMK_ADSiteTopology) |Come si configurare subnet, siti e collegamenti di sito con il traffico di rete virtuale di Azure toooptimize e ridurre al minimo il costo? |<li>Definizioni di sito e subnet</li> <li>Proprietà dei collegamenti di sito e notifica delle modifiche</li> <li>Compressione della replica</li> |
| [Indirizzamento IP e DNS](#BKMK_IPAddressDNS) |Come indirizzi IP tooconfigure e la risoluzione dei nomi? |<li>Utilizzare hello cmdlet Set-AzureStaticVNetIP di utilizzare hello tooassign un indirizzo IP statico</li> <li>Installare il server DNS di Windows Server e configurare le proprietà di rete virtuale hello con nome hello e l'indirizzo IP di macchina virtuale che ospita i ruoli del server DNS e controller di dominio hello hello</li> |
| [Controller di dominio con distribuzione geografica](#BKMK_DistributedDCs) |TooDCs tooreplicate su separati come reti virtuali? |Se la topologia del sito di Active Directory richiede un controller di dominio in aree geografiche corrispondente toodifferent Azure aree, rispetto a quelle desidera toocreate siti di Active Directory, di conseguenza. [Configurare la rete virtuale toovirtual rete connettività](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) tooreplicate tra controller di dominio in reti virtuali separate. |
| [Controller di dominio di sola lettura](#BKMK_RODC) |Usare controller di dominio di sola lettura o scrivibili? |<li>Filtrare gli attributi HBI/PII</li> <li>Filtrare le chiavi private</li> <li>Limitare il traffico in uscita</li> |
| [Catalogo globale](#BKMK_GC) |Installare il catalogo globale? |<li>Per una foresta con dominio singolo, convertire tutti i controller di dominio in cataloghi globali</li> <li>Per una foresta a più domini, i cataloghi globali sono necessari per l'autenticazione</li> |
| [Metodo di installazione](#BKMK_InstallMethod) |Come tooinstall controller di dominio in Azure? |È possibile:  <li>Installare Servizi di dominio Active Directory usando Windows PowerShell o Dcpromo</li> <li>Spostare il disco rigido virtuale di un controller di dominio virtuale locale</li> |
| [Posizione del database hello servizi di dominio di Windows Server Active Directory e SYSVOL](#BKMK_PlaceDB) |Dove toostore servizi di dominio di Windows Server Active Directory di database, log e SYSVOL? |Modificare i valori predefiniti di Dcpromo.exe. Questi file critici di Active Directory *devono* trovarsi su dischi dati di Azure invece che su dischi del sistema operativo che implementano la memorizzazione nella cache in scrittura. |
| [Backup e ripristino](#BKMK_BUR) |Come toosafeguard e il recupero dei dati? |Creare backup dello stato del sistema. |
| [Configurazione del server federativo](#BKMK_FedSrvConfig) |<li>Distribuire una nuova foresta con federazione nel cloud hello?</li> <li>Distribuire ADFS locale ed esporre un proxy nel cloud hello?</li> |<li>Sicurezza</li> <li>Conformità</li> <li>Costi</li> <li>Accesso tooapplications ai partner aziendali</li> |
| [Configurazione di servizi cloud](#BKMK_CloudSvcConfig) |Un servizio cloud viene distribuito in modo implicito hello prima volta che si crea una macchina virtuale. È necessario servizi cloud aggiuntivi toodeploy? |<li>Macchine virtuali o una macchina virtuale richiede l'esposizione diretta toohello Internet?</li> <li> Servizio hello richiede il bilanciamento del carico?</li> |
| [Requisiti del server federativo per l'indirizzamento IP pubblico e privato (confronto tra indirizzo IP dinamico e indirizzo IP virtuale)](#BKMK_FedReqVIPDIP) |<li>Istanza di ADFS di Windows Server hello necessita toobe raggiungibile direttamente da Internet hello?</li> <li>L'applicazione hello distribuita nel cloud hello richiede il proprio indirizzo IP con connessione Internet e la porta?</li> |Creare un servizio cloud per ogni indirizzo IP virtuale necessario per la distribuzione |
| [Configurazione con disponibilità elevata di AD FS di Windows Server](#BKMK_ADFSHighAvail) |<li>Quanti nodi sono necessari nella server farm AD FS di Windows Server?</li> <li>Toodeploy il numero di nodi nella farm Windows Server AD FS proxy?</li> |Resilienza e tolleranza di errore |

### <a name="BKMK_NetworkTopology"></a>Topologia di rete
Coerenza di indirizzi IP hello toomeet ordine e i requisiti DNS di dominio Active Directory di Windows Server Active Directory, è necessario creare toofirst un [rete virtuale di Azure](../virtual-network/virtual-networks-overview.md) e allegare il tooit macchine virtuali. Durante la creazione, è necessario decidere se toooptionally estendere connettività tooyour locali aziendali rete, che connette in modo trasparente virtuali di Azure macchine macchine tooon locali, questa operazione viene eseguita utilizzando le tecnologie VPN tradizionali e richiede l'esposizione di un endpoint VPN sul perimetro di hello della rete aziendale di hello. Hello VPN viene avviata dalla rete aziendale di Azure toohello, non viceversa.

Si noti che i costi aggiuntivi si applicano quando si estende una rete locale di rete virtuale tooyour oltre hello addebiti standard tooeach macchina virtuale. In particolare, vi sono addebiti per il tempo di CPU del gateway di rete virtuale di Azure hello e per il traffico in uscita hello generati da ogni macchina virtuale che comunica con il computer locale tramite VPN hello. Per altre informazioni sugli addebiti per il traffico di rete, vedere [Prezzi di Azure](http://azure.microsoft.com/pricing/).

### <a name="BKMK_DeploymentConfig"></a>Configurazione della distribuzione di un controller di dominio
modalità di Hello configurazione hello controller di dominio dipende dai requisiti di hello per hello del servizio è necessario toorun in Azure. Ad esempio, è possibile distribuire una nuova foresta, isolata dalla propria foresta aziendale, per il testing proof of concept, una nuova applicazione o un altro progetto a breve termine che richiede i servizi di directory ma alle risorse aziendali toointernal non specifiche di accesso.

Il vantaggio, una foresta isolata che con non viene replicato i controller di dominio locale i controller di dominio, causando il traffico di rete in uscita generato dal sistema hello, direttamente riducendo i costi. Per altre informazioni sugli addebiti per il traffico di rete, vedere [Prezzi di Azure](http://azure.microsoft.com/pricing/).

Ad esempio, si supponga che i requisiti sulla privacy per un servizio, ma dipende dal servizio hello tooyour accesso interno Windows Server Active Directory. Se è consentito toohost dati per il servizio di hello in hello cloud, è possibile distribuire un nuovo dominio figlio per la foresta interna in Azure. In questo caso, è possibile distribuire un controller di dominio nuovo dominio figlio hello (senza catalogo globale di hello in problemi di privacy indirizzo toohelp ordine). Questo scenario richiede una rete virtuale per la connettività ai controller di dominio locali, insieme alla distribuzione di un controller di dominio di replica.

Se si crea una nuova foresta, scegliere se toouse [e trust di Active Directory](https://technet.microsoft.com/library/cc771397) o [relazioni di trust federative](https://technet.microsoft.com/library/dd807036). Bilanciare l'esigenza di hello dipende dalla compatibilità, sicurezza, conformità, costo e resilienza. Ad esempio, tootake sfruttare [autenticazione selettiva](https://technet.microsoft.com/library/cc755844) si potrebbe scegliere toodeploy una nuova foresta in Azure e creare un trust di Active Directory di Windows Server tra foresta locale di hello e hello cloud. Se l'applicazione hello è in grado di riconoscere attestazioni, tuttavia, è possibile distribuire trust federativi anziché trust tra foreste di Active Directory. Un altro fattore verrà hello costo tooeither replicate più dati estendendo locale cloud toohello di Windows Server Active Directory o generare più traffico in uscita come risultato dell'autenticazione e il carico di query.

Anche i requisiti di disponibilità e tolleranza di errore influiscono sulla scelta, Ad esempio, se hello collegamento viene interrotto, applicazioni in cui un trust Kerberos o una relazione di trust federativa sono tutti probabilmente completamente suddivisa a meno che non è stata distribuita un'infrastruttura sufficiente in Azure. Configurazioni di distribuzione alternativi, ad esempio i controller di dominio di replica (scrivibile o scrivibili) aumentare hello probabilità di essere in grado di tootolerate malfunzionamenti del collegamento.

### <a name="BKMK_ADSiteTopology"></a>Topologia del sito Active Directory di Windows Server
È necessario toocorrectly definire siti e collegamenti di sito in ordine toooptimize traffico e ridurre il costo. Siti, collegamenti di sito e subnet influiscono sulla topologia di replica hello tra i controller di dominio e il flusso di hello del traffico di autenticazione. Considerare i seguenti addebiti di traffico hello e quindi distribuire e configurare i controller di dominio in base a requisiti toohello del proprio scenario di distribuzione:

* È disponibile una tariffa nominale per ora per il gateway hello stesso:
  
  * Può essere avviato e arrestato nel modo desiderato
  * Se arrestato, macchine virtuali di Azure sono isolate dalla rete aziendale hello
* Il traffico in ingresso è gratuito
* Traffico in uscita viene addebitato in base troppo[Azure prezzi in immediate](http://azure.microsoft.com/pricing/). È possibile ottimizzare le proprietà di collegamento di sito tra siti locali e cloud hello come indicato di seguito:
  
  * Se si utilizza più reti virtuali, configurare i collegamenti di sito hello e i relativi costi in modo appropriato tooprevent servizi di dominio di Windows Server Active Directory da classificare hello Azure del sito su uno in grado di fornire hello stessi livelli di servizio senza alcun costo. È inoltre possibile disattivare Bridge hello tutti i siti di opzione di collegamento (relativa) (che è abilitato per impostazione predefinita). Ciò garantisce che la replica venga eseguita solo tra i siti connessi direttamente. Controller di dominio in siti connessi in modo transitivo non sono più in grado di tooreplicate direttamente tra loro, ma deve essere replicata tramite uno o più siti comuni. Se i siti intermedi hello diventano non disponibili per qualche motivo, è possibile che la replica tra controller di dominio in siti connessi in modo transitivo non verrà eseguita anche se è disponibile la connettività tra i siti di hello. Infine, in cui le sezioni del processo di replica transitiva rimangono utili, creare sito ponti di collegamenti che contengono collegamenti di sito appropriati hello e siti, ad esempio in locale, siti di rete aziendale.
  * [Configurare i costi di collegamento di sito](https://technet.microsoft.com/library/cc794882) tooavoid in modo appropriato il traffico indesiderato. Ad esempio, se **prova sito più vicino successivo** impostazione è abilitata, assicurarsi di rete virtuale che hello siti non sono hello accanto più vicino aumentando il costo di hello associato dell'oggetto collegamento di sito hello che si connette hello Azure sito indietro toohello rete aziendale.
  * Configurare il collegamento di sito [intervalli](https://technet.microsoft.com/library/cc794878) e [pianificazioni](https://technet.microsoft.com/library/cc816906) in base a requisiti tooconsistency e frequenza di modifiche di oggetti. Allineare la pianificazione di replica alla tolleranza della latenza. I controller di dominio vengono replicate solo hello ultimo stato di un valore, in modo decrescente intervallo di replica hello può ridurre i costi se è presente una frequenza di modifica oggetto sufficienti.
* Se la riduzione dei costi è una priorità, assicurarsi che la replica venga pianificata e che la notifica delle modifiche non sia abilitata. Si tratta di configurazione predefinita di hello quando la replica tra siti. Non è importante se si distribuisce un controller di dominio in una rete virtuale perché hello RODC non verrà replicate le modifiche in uscita. Ma se si distribuisce un controller di dominio scrivibile, assicurarsi che il collegamento di sito hello non è configurato tooreplicate aggiornamenti con frequenza non necessaria. Se si distribuisce un server di catalogo globale (GC), assicurarsi che tutti gli altri siti che contiene un catalogo globale vengano replicate le partizioni di dominio da un controller di dominio in un sito connesso con un collegamento di sito di origine o di collegamenti di sito aventi un costo inferiore rispetto a hello catalogo globale nel sito di Azure hello.
* È possibile comunque toofurther ridurre il traffico di rete generato dalla replica tra siti modificando l'algoritmo di compressione della replica hello. algoritmo di compressione Hello è controllata dall'algoritmo di compressione hkey_local_machine\system\currentcontrolset\services\ntds\parameters\replicator della voce del Registro di sistema REG_DWORD hello. valore predefinito di Hello è 3, che mette in correlazione toohello algoritmo di compressione Xpress. È possibile modificare too2 valore hello, quali modifiche hello tooMSZip algoritmo. Nella maggior parte dei casi, ciò consentirà di migliorare la compressione di hello, ma a tale scopo spese hello dell'utilizzo della CPU. Per altre informazioni, vedere l'articolo relativo al [funzionamento della topologia di replica di Active Directory](https://technet.microsoft.com/library/cc755994).

### <a name="BKMK_IPAddressDNS"></a>Indirizzamento IP e DNS
Alle macchine virtuali di Azure vengono allocati "indirizzi con lease DHCP" per impostazione predefinita. Poiché gli indirizzi dinamici di rete virtuale di Azure sono persistenti con una macchina virtuale per la durata di hello della macchina virtuale hello, hello directory di Windows Server Active Directory i requisiti.

Di conseguenza, quando si usa un indirizzo dinamico in Azure, vengono di fatto un indirizzo IP statico poiché è indirizzabile per il periodo di hello di lease hello e periodo hello lease hello è uguale toohello durata del servizio cloud hello.

Tuttavia, indirizzo dinamico hello viene deallocato se hello VM viene chiusa. indirizzo IP di hello tooprevent venga deallocato, è possibile [utilizzare Set-AzureStaticVNetIP tooassign un indirizzo IP statico](http://social.technet.microsoft.com/wiki/contents/articles/23447.how-to-assign-a-private-static-ip-to-an-azure-vm.aspx).

Per la risoluzione dei nomi, distribuire la propria (o utilizzare quella esistente) infrastruttura del server DNS DNS fornito da Azure non soddisfa hello avanzate requisiti di risoluzione dei nomi di dominio Active Directory di Windows Server Active Directory. Ad esempio, non supporta i record SRV dinamici e così via. La risoluzione dei nomi è un elemento di configurazione critico per i controller di domino e i client aggiunti a un dominio. I controller di dominio devono essere in grado di registrare i record di risorse e di risolvere altri record di risorse del controller di dominio.
Per motivi di prestazioni e tolleranza d'errore, è servizio di Server DNS di Windows hello tooinstall ottimale nei controller di dominio hello in esecuzione in Azure. Quindi configurare le proprietà di rete virtuale di Azure hello con nome hello e indirizzo IP del server DNS hello. Avvio di altre macchine virtuali nella rete virtuale hello, le impostazioni del resolver DNS client verranno configurate con il server DNS come parte dell'allocazione di indirizzi IP dinamico hello.

> [!NOTE]
> È possibile unire i domini di Active Directory di Windows Server Active Directory di dominio Active Directory con i tooa computer locale che sono ospitato in Azure direttamente su Internet hello. Hello requisiti delle porte per Active Directory e l'operazione di aggiunta al dominio hello ne esegue il rendering le porte necessarie toodirectly poco espongono hello e lo stato attivo, un intero toohello di controller di dominio Internet.
> 
> 

Le VM registrano il relativo nome DNS automaticamente all'avvio o in caso di modifica di un nome.

Per ulteriori informazioni su questo esempio e un altro esempio che illustra come tooprovision hello prima macchina virtuale e installare di dominio Active Directory su di esso, vedere [installare una nuova foresta di Active Directory in Microsoft Azure](active-directory-new-forest-virtual-machine.md). Per altre informazioni sull'uso di Windows PowerShell, vedere [Come installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) e [Cmdlet di gestione di Azure](/powershell/module/azurerm.compute/#virtual_machines).

### <a name="BKMK_DistributedDCs"></a>Controller di dominio con distribuzione geografica
Azure offre vantaggi quando si ospitano più controller di dominio in reti virtuali diverse:

* Tolleranza di errore multisito
* Uffici toobranch prossimità fisica (latenza più bassa)

Per informazioni sulla configurazione della comunicazione diretta tra reti virtuali, vedere [configurare la connettività di rete di rete virtuale toovirtual](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

### <a name="BKMK_RODC"></a>Controller di dominio di sola lettura
È necessario toochoose se leggere toodeploy-scrivibile o solo i controller di dominio. È possibile toodeploy inclinata lettura perché non è un controllo fisico su di essi, ma i RODC sono progettate toobe distribuito nelle posizioni in cui la sicurezza fisica è a rischio, ad esempio le succursali.

Azure non presenta hello rischi di sicurezza fisica di una succursale, tuttavia lettura potrebbe comunque risultare toobe economicamente più vantaggioso perché funzionalità hello che forniscono sono particolarmente adatte toothese ambienti anche se per motivi molto diversi. Ad esempio, controller non dispone di alcuna replica in uscita e sono tooselectively in grado di popolare i segreti (password). In svantaggio hello, mancanza di hello di questi segreti potrebbe richiedere traffico in uscita su richiesta toovalidate usarle come autentica un utente o computer. I segreti possono però essere prepopolati e memorizzati nella cache in modo selettivo.

Poiché è possibile aggiungere gli attributi che contengono dati sensibili toohello RODC filtrato il set di attributi (/FAs) offre un vantaggio aggiuntivo intorno a problemi di PII e HBI. Hello /FAs è un set personalizzabile di attributi che non sono replicati tooRODCs. Nel caso in cui non sia possibile o non si desidera toostore PII o HBI in Azure, è possibile utilizzare hello /FAs come misura di sicurezza. Per altre informazioni, vedere [set di attributi con filtro per controller di dominio di sola lettura[(https://technet.microsoft.com/library/cc753459)].

Assicurarsi che le applicazioni siano compatibili con lettura Prevedi toouse. Molte applicazioni abilitate per Active Directory di Windows Server funzionano bene con lettura, ma alcune applicazioni possono risultare inefficiente o non riuscire se non hanno accesso tooa controller di dominio scrivibile. Per altre informazioni, vedere la Guida alla [Compatibilità delle applicazioni con i controller di dominio di sola lettura](https://technet.microsoft.com/library/cc755190).

### <a name="BKMK_GC"></a>Catalogo globale
È necessario se toochoose tooinstall un catalogo globale (GC). In una foresta a dominio singolo è necessario configurare tutti i controller di dominio come server di catalogo globale. I costi non aumenteranno perché non vi sarà alcun traffico di replica aggiuntivo.

In una foresta con più domini, i cataloghi globali sono necessari tooexpand Universal appartenenze durante il processo di autenticazione hello. Se non si distribuisce un catalogo globale, i carichi di lavoro nella rete virtuale hello utilizzato per autenticare un controller di dominio in Azure genereranno indirettamente traffico di autenticazione in uscita tooquery cataloghi globali locali durante ogni tentativo di autenticazione.

i costi di Hello associati ai cataloghi globali sono meno prevedibili perché essi viene ospitato ogni dominio (in parte). Se il carico di lavoro hello ospita un servizio con connessione Internet e autentica gli utenti in servizi di dominio di Windows Server Active Directory, i costi di hello potrebbe essere difficile calcolare. toohelp ridurre le query di catalogo globale di fuori del sito cloud hello durante l'autenticazione, è possibile [Abilita Caching appartenenza a gruppo universale](https://technet.microsoft.com/library/cc816928).

### <a name="BKMK_InstallMethod"></a>Metodo di installazione
È necessario come toochoose tooinstall hello, i controller di dominio nella rete virtuale hello:

* Alzare di livello nuovi controller di dominio. Per altre informazioni, vedere [Installare una nuova foresta Active Directory in una rete virtuale di Azure](active-directory-new-forest-virtual-machine.md).
* Spostare hello disco rigido virtuale di un cloud di toohello controller di dominio virtuale locale. In questo caso, è necessario assicurarsi che hello locale controller di dominio virtuale venga "spostato" non "copiato" o "clonato".

Utilizzare macchine virtuali di Azure solo per i controller di dominio (come tooAzure anziché ruolo "web" o "lavoro" le macchine virtuali). Sono durevoli e la durabilità di stato per un controller di dominio è essenziale. Le macchine virtuali di Azure sono progettate per i carichi di lavoro, ad esempio i controller di dominio.

Non utilizzare SYSPREP toodeploy o clonare i controller di dominio. possibilità di Hello tooclone i controller di dominio è solo disponibile a partire da Windows Server 2012. funzionalità di clonazione Hello richiede il supporto per VMGenerationID nell'hypervisor sottostante hello. Hyper-V in Windows Server 2012 e le reti virtuali di Azure supportano entrambi VMGenerationID, come fanno i fornitori di software di virtualizzazione di terze parti.

### <a name="BKMK_PlaceDB"></a>Posizione del database hello servizi di dominio di Windows Server Active Directory e SYSVOL
Selezionare dove toolocate hello database di Windows Server Active Directory, i registri e SYSVOL. Devono essere distribuiti nei dischi dati di Azure.

> [!NOTE]
> Dischi dati di Azure sono vincolate too1 TB.
> 
> 

Per impostazione predefinita, le unità disco dati non memorizzano le scritture nella cache. Unità disco dati che sono collegato tooa VM usare caching write-through. Rende cache write-through che scrittura hello sia eseguito il commit toodurable archiviazione di Azure prima di hello è stata completata dal punto di vista di hello del sistema operativo della macchina virtuale di hello. Fornisce durabilità, spese di hello di scritture leggermente più lente.

Questo è importante per servizi di dominio di Windows Server Active Directory perché la cache del disco write-behind Invalidate le interpretazioni da hello controller di dominio. Servizi di dominio di Windows Server Active Directory tenta toodisable caching in scrittura, ma è attivo toohello disco i/o sistema toohonor è. Errore toodisable caching in scrittura può, in determinate circostanze, introdurre il rollback USN causando oggetti residui e altri problemi.

Come procedura consigliata per i controller di dominio virtuali, hello seguenti:

* Impostare hello preferenze Cache dell'Host su disco di dati di Azure hello per nessuno. In questo modo si evitano problemi di memorizzazione nella cache in scrittura per le operazioni di Servizi di dominio Active Directory.
* Archiviare il database di hello, log e SYSVOL in hello dati stesso disco o dischi dati separano. In genere si tratta di un disco separato dal disco hello utilizzato dal sistema operativo hello stesso. informazioni chiave Hello sono database hello Windows Server Active Directory e SYSVOL non devono essere archiviati in un tipo di disco del sistema operativo Azure. Per impostazione predefinita, hello il processo di installazione di Active Directory consente di installare questi componenti nella cartella % systemroot %, non è consigliata per Azure.

### <a name="BKMK_BUR"></a>Backup e ripristino
Tenere presente quali elementi sono o meno supportati per il backup e ripristino di un controller di dominio in generale e, più in particolare, quelli in esecuzione in una VM. Vedere [Considerazioni sul backup e il ripristino dei controller di dominio virtualizzati](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv#backup_and_restore_considerations_for_virtualized_domain_controllers).

Creare backup dello stato del sistema usando solo software per backup che riconosca specificatamente i requisiti di backup per Servizi di dominio Active Directory di Windows Server, ad esempio Windows Server Backup.

Non copiare o clonare file VHD di controller di dominio invece di eseguire backup regolari. Se è necessario un ripristino e l'operazione viene eseguita usando VHD clonati o copiati senza Windows Server 2012 e un hypervisor supportato, verranno introdotti gap USN.

### <a name="BKMK_FedSrvConfig"></a>Configurazione del server federativo
la configurazione di Hello del server federativi ADFS di Windows Server (STS) dipende in parte che hello applicazioni che si desidera toodeploy in Azure richiedano tooaccess risorse di rete locale.

Se le applicazioni di hello soddisfano hello seguenti criteri, è possibile distribuire applicazioni hello in isolamento dalla rete locale.

* Accettano token di sicurezza SAML
* Sono toohello essere esposte Internet
* Non accedono alle risorse locali

In questo caso, configurare i servizi token di sicurezza di AD FS di Windows Server come segue:

1. Configurare una foresta a dominio singolo isolata in Azure.
2. Fornire l'accesso federato ai toohello foresta configurando una server farm federativa di Windows Server AD FS.
3. Configurare ADFS di Windows Server (server farm federativa e farm proxy server federativo) nella foresta locale hello.
4. Stabilire una relazione di trust federativa tra hello sedi locali e istanze di Azure di Windows Server AD FS.

In hello altra parte, se le applicazioni di hello richiedono tooon locale di accedere alle risorse, è possibile configurare ADFS di Windows Server con un'applicazione hello in Azure come indicato di seguito:

1. Configurare la connettività tra le reti locali e Azure.
2. Configurare una server farm federativa ADFS di Windows Server nella foresta locale hello.
3. Configurare una farm proxy server federativo AD FS di Windows Server in Azure.

Questa configurazione presenta il vantaggio di hello di ridurre l'esposizione di hello delle risorse locali, simile tooconfiguring ADFS di Windows Server con le applicazioni in una rete perimetrale.

Si noti che in entrambi gli scenari è possibile stabilire relazioni di trust con più provider di identità, se è necessaria la collaborazione business-to-business.

### <a name="BKMK_CloudSvcConfig"></a>Configurazione di servizi cloud
Servizi cloud sono necessari se si desidera che una macchina virtuale tooexpose direttamente toohello Internet o tooexpose con una connessione Internet con bilanciamento del carico dell'applicazione. Ciò è possibile perché ogni servizio cloud offre un singolo indirizzo IP virtuale configurabile.

### <a name="BKMK_FedReqVIPDIP"></a>Requisiti del server federativo per l'indirizzamento IP pubblico e privato (confronto tra indirizzo IP dinamico e indirizzo IP virtuale)
Ogni macchina virtuale di Azure riceve un indirizzo IP dinamico. Un indirizzo IP dinamico è un indirizzo privato accessibile solo all'interno di Azure. Nella maggior parte dei casi, tuttavia, sarà necessario tooconfigure un indirizzo IP virtuale per le distribuzioni di Windows Server AD FS. indirizzo IP virtuale Hello è necessario tooexpose toohello gli endpoint ADFS di Windows Server Internet e verrà utilizzato dai partner federati e dai client per l'autenticazione e la gestione continuativa. Un indirizzo IP virtuale è una proprietà di un servizio cloud che contiene una o più macchine virtuali di Azure. Se un'applicazione hello grado di riconoscere attestazioni distribuita in Azure e ADFS di Windows Server è entrambi con connessione Internet e condivisione porte comuni, ognuna richiederà un indirizzo IP virtuale del proprio e sarà pertanto necessario toocreate un servizio cloud per un'applicazione hello e una in secondo luogo, per ADFS di Windows Server.

Per le definizioni di indirizzo IP dinamico e l'indirizzo IP virtuale di hello termini, vedere [termini e definizioni](#BKMK_Glossary).

### <a name="BKMK_ADFSHighAvail"></a>Configurazione con disponibilità elevata di AD FS di Windows Server
Sebbene sia i servizi di federazione ADFS di Windows Server autonomo toodeploy possibili, è consigliabile toodeploy una farm con almeno due nodi per STS ADFS e proxy per gli ambienti di produzione.

Vedere [considerazioni relative alla topologia di AD FS 2.0 deployment](https://technet.microsoft.com/library/gg982489) in hello [AD Guida alla progettazione di ADFS 2.0](https://technet.microsoft.com/library/dd807036) toodecide migliori opzioni di configurazione di distribuzione in base alle esigenze specifiche.

> [!NOTE]
> Nel bilanciamento del carico di ordine tooget per gli endpoint ADFS di Windows Server Active Directory in Azure, configurare tutti i membri della farm ADFS di Windows Server hello in hello stesso servizio cloud e usare hello funzionalità Bilanciamento del carico di Azure per (impostazione predefinita 80) porte HTTP e HTTPS (443 per impostazione predefinita). Per altre informazioni, vedere l'articolo relativo al [probe di bilanciamento del carico di Azure](https://msdn.microsoft.com/library/azure/jj151530).
> Il bilanciamento del carico di rete di Windows Server non è supportato in Azure.
> 
> 

