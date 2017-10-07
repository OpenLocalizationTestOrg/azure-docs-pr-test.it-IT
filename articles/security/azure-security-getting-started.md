---
title: aaaGetting avviato con la protezione di Microsoft Azure | Documenti Microsoft
description: "Questo articolo fornisce una panoramica delle funzionalità di sicurezza di Microsoft Azure e considerazioni generali per le organizzazioni che esegue la migrazione di provider di cloud tooa asset."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 8d8a0088-c85a-48e7-bd04-2bc7b78b0691
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: yurid
ms.openlocfilehash: c61dd99ffd0143bc7b165367dadadc977ffcf47b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-microsoft-azure-security"></a>Introduzione alla sicurezza in Microsoft Azure
Quando si compila o provider di cloud tooa asset IT di eseguire la migrazione, ci si basa sul tooprotect capacità dell'organizzazione che le applicazioni e dati con controlli di hello assicurano toomanage hello delle risorse basati su cloud e servizi hello.

Infrastruttura di Azure è progettato da hello tooapplications di funzionalità per l'hosting contemporaneamente milioni di clienti e fornisce una base attendibile in cui le aziende grado di soddisfare le esigenze di sicurezza. Inoltre, Azure offre un'ampia gamma di toocontrol possibilità hello e opzioni di protezione configurabili loro in modo che sia possibile personalizzare sicurezza toomeet hello requisiti delle distribuzioni.

In questa panoramica sulla sicurezza in Azure si esamineranno:

* Servizi di Azure e funzionalità che è possibile usare toohelp proteggere i servizi e i dati all'interno di Azure.
* Di proteggere i dati e le applicazioni come Microsoft protegge hello toohelp dell'infrastruttura di Azure.

## <a name="identity-and-access-management"></a>Gestione delle identità e dell'accesso
Controllo dell'infrastruttura di accesso tooIT, dati e applicazioni è fondamentale. Microsoft Azure offre queste funzionalità tramite servizi come Azure Active Directory (Azure AD), Archiviazione di Azure e il supporto per svariati standard e API.

[Azure AD](../active-directory/active-directory-whatis.md) è un repository di identità e un motore che fornisce l'autenticazione, l'autorizzazione e il controllo di accesso per gli utenti, i gruppi e gli oggetti di un'organizzazione. Azure AD offre inoltre agli sviluppatori una gestione delle identità efficace toointegrate nelle proprie applicazioni. I protocolli standard di settore come [SAML 2.0](https://en.wikipedia.org/wiki/SAML_2.0), [WS-Federation](https://msdn.microsoft.com/library/bb498017.aspx) e [OpenID Connect](http://openid.net/connect/) rendono l'accesso possibile in piattaforme quali .NET, Java, Node.js e PHP.

basato su REST API Graph consente agli sviluppatori tooread Hello e scrittura directory toohello da qualsiasi piattaforma. Grazie al supporto per [OAuth 2.0](http://oauth.net/2/), gli sviluppatori possono creare applicazioni Web e per dispositivi mobili che possano integrarsi con API Web Microsoft e di terze parti, per creare API Web personalizzate e sicure. Sono disponibili librerie client open source per .NET, Windows Store, iOS e Android, con altre librerie in fase di sviluppo.

### <a name="how-azure-enables-identity-and-access-management"></a>Come Azure abilita la gestione delle identità e dell'accesso
Azure AD può essere usato come directory cloud autonoma dell'organizzazione oppure come soluzione integrata con l'implementazione di Active Directory locale esistente. Alcune funzionalità di integrazione includono la sincronizzazione della directory e Single Sign-On (SSO), Questi estendono reach hello le identità locali esistenti nel cloud hello e migliorare l'esperienza utente e di amministrazione di hello.

Alcune delle altre funzionalità di gestione delle identità e dell'accesso includono:

* Azure AD abilita [SSO](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) tooSaaS applicazioni, indipendentemente dalla relativa posizione. Alcune applicazioni sono federate con Azure AD e altre usano SSO basato su password. Le applicazioni federate possono anche supportare il provisioning utenti e l'insieme di credenziali delle password.
* Accesso toodata in [di archiviazione di Azure](https://azure.microsoft.com/services/storage/) è controllata tramite l'autenticazione. Ogni account di archiviazione ha una chiave primaria ([chiave account di archiviazione](https://msdn.microsoft.com/library/azure/ee460785.aspx), o SAK) e una chiave segreta secondaria (la firma di accesso condiviso hello o SAS).
* Azure AD fornisce l'identità come servizio usando la federazione (con [Active Directory Federation Services](../active-directory/fundamentals-identity.md)), la sincronizzazione e la replica con le directory locali.
* [Azure multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) è servizio di autenticazione a più fattori hello che richiede l'accesso degli utenti tooverify mediante l'utilizzo di un'app per dispositivi mobili, una telefonata o un messaggio di testo. E può essere utilizzato con Azure AD toohelp sicuro alle risorse locali con il server Azure multi-Factor Authentication hello e con applicazioni personalizzate e le directory utilizzando hello SDK.
* [Servizi di dominio AD Azure](https://azure.microsoft.com/services/active-directory-ds/) consente di aggiungere macchine virtuali di Azure tooa dominio senza distribuire i controller di dominio. È possibile accedere in macchine virtuali toothese con le credenziali aziendali di Active Directory e amministrare le macchine virtuali appartenenti a un dominio usando le linee di base di criteri di gruppo tooenforce sicurezza in tutte le macchine virtuali di Azure.
* [Azure B2C Directory attiva](https://azure.microsoft.com/services/active-directory-b2c/) fornisce un servizio di gestione di identità globale a disponibilità elevata per applicazioni per consumatori che viene ridimensionata toohundreds di milioni di valori Identity. Il servizio può essere integrato tra piattaforme mobili e Web. Consentire agli utenti possono accedere tooall le applicazioni attraverso esperienze di personalizzabile tramite gli account di social networking esistenti o creando nuove credenziali.

## <a name="data-access-control-and-encryption"></a>Controllo di accesso ai dati e crittografia
Microsoft utilizza i principi di hello della separazione dei compiti e [privilegio](https://en.wikipedia.org/wiki/Principle_of_least_privilege) nel corso di operazioni di Azure. Accesso toodata dal personale del supporto tecnico di Azure richiede l'autorizzazione esplicita e viene concesso in base che viene registrata e controllata "just-in-time", quindi revocato dopo il completamento di engagement hello.

Azure offre anche diverse funzionalità per la protezione dei dati in transito e inattivi, tra cui la crittografia per dati, file, applicazioni, servizi, comunicazioni e unità. È possibile non solo crittografare le informazioni prima di inserirle in Azure, ma anche archiviare le chiavi nei data center locali.

![Microsoft Antimalware in Azure](./media/azure-security-getting-started/sec-azgsfig1.PNG)

### <a name="azure-encryption-technologies"></a>Tecnologie di crittografia di Azure
È possibile raccogliere informazioni sull'ambiente di accesso amministrativo tooyour sottoscrizione utilizzando [Azure AD Reporting](../active-directory/active-directory-reporting-audit-events.md). È possibile configurare [Crittografia unità BitLocker](https://technet.microsoft.com/library/cc732774.aspx) nei VHD contenenti informazioni riservate in Azure.

Altre funzionalità di Azure che consentono di proteggere i dati tookeep includono:

* Gli sviluppatori di applicazioni è possono compilare la crittografia nelle applicazioni hello distribuiscono in Azure mediante Windows hello [CryptoAPI](https://msdn.microsoft.com/library/ms867086.aspx) e .NET Framework.
* Controllare completamente chiavi hello con crittografia lato client per l'archiviazione Blob di Azure. il servizio di archiviazione Hello mai vede chiavi hello e non è in grado di decrittografare dati hello.
* [Azure Rights Management (Azure RMS)](https://technet.microsoft.com/library/jj585026.aspx) (con hello [RMS SDK](https://msdn.microsoft.com/library/dn758244.aspx)) fornisce i file e prevenzione della perdita di dati e di crittografia a livello di dati tramite la gestione basata su criteri di accesso.
* Azure supporta la [crittografia a livello di tabella e a livello di colonna (TDE/CLE)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/12/recommendations-for-using-cell-level-encryption-in-azure-sql-database.aspx) nelle macchine virtuali di SQL Server e supporta i server di gestione delle chiavi locali di terze parti nei data center.
* Chiavi dell'Account di archiviazione, firme di accesso condiviso, i certificati di gestione e le altre chiavi sono univoci tooeach tenant di Azure.
* Azure [StorSimple](http://www.microsoft.com/server-cloud/products/storsimple/overview.aspx) archiviazione ibrido crittografa i dati tramite una coppia di chiavi pubblica/privata 128 bit prima di caricarlo tooAzure archiviazione.
* Azure supporta e utilizzi diversi meccanismi di crittografia, tra cui SSL/TLS, IPsec e AES, a seconda di trasporti, i contenitori e i tipi di dati hello.

## <a name="virtualization"></a>Virtualizzazione
piattaforma Azure Hello Usa un ambiente virtualizzato. Le istanze utente funzionano come le macchine virtuali autonome che non dispone di server di accesso tooa host fisico, e l'isolamento viene applicato tramite fisico [livelli di privilegi processore (circolare-0/ring-3)](https://en.wikipedia.org/wiki/Protection_ring).

Livello 0 è hello più privilegiato e 3 è hello almeno. sistema operativo guest Hello in esecuzione in 1 anello con meno privilegi e le applicazioni eseguite hello 3 anello con privilegi minimi. Virtualizzazione delle risorse fisiche comporta tooa netta separazione tra sistema operativo guest e hypervisor, determinando la separazione di sicurezza aggiuntive tra hello due.

Hello Azure hypervisor funziona come un micro-kernel e passa tutte le richieste di accesso hardware dall'host toohello di macchine virtuali guest per l'elaborazione tramite un'interfaccia di memoria condivisa denominata VMBus. Questo impedisce agli utenti di ottenere sistema toohello non elaborato l'accesso in lettura/scrittura/esecuzione e si riduce il rischio di hello di condivisione delle risorse di sistema.

![Microsoft Antimalware in Azure](./media/azure-security-getting-started/sec-azgsfig2.PNG)

### <a name="how-azure-implements-virtualization"></a>Come Azure implementa la virtualizzazione
Azure Usa un firewall hypervisor (filtro di pacchetti) che viene implementato nell'hypervisor hello e configurato da un agente di controller di infrastruttura. Ciò consente di proteggere i tenant da accesso non autorizzato. Per impostazione predefinita, tutto il traffico viene bloccato quando viene creata una macchina virtuale e quindi agente controller di infrastruttura hello Configura hello pacchetto filtro tooadd *regole e le eccezioni* tooallow autorizzato il traffico.

In questo caso sono previste due categorie di regole:

* **Regole di configurazione macchina virtuale o di infrastruttura**: per impostazione predefinita, vengono bloccate tutte le comunicazioni. Vi sono eccezioni tooallow toosend una macchina virtuale e di ricevere il traffico DNS e DHCP. Macchine virtuali possono inoltre inviare traffico toohello "public" internet e inviare traffico tooother macchine virtuali all'interno del cluster hello e server di attivazione del sistema operativo hello. elenco di macchine virtuali di Hello delle destinazioni in uscita consentite non include le subnet di Azure router, gestione di Azure, eseguire il backup finale e altre proprietà di Microsoft.
* **File di configurazione del ruolo**: definisce hello sono elencati di controllo di accesso (ACL) in ingresso basati sul modello di servizio del tenant hello. Ad esempio, se un tenant dispone di un front-end Web sulla porta 80 in una determinata macchina virtuale, Azure verrà tooall la porta 80 TCP IP se si sta configurando un endpoint in hello [modello di distribuzione classica Azure](../azure-resource-manager/resource-manager-deployment-model.md). Se macchina virtuale hello dispone di un ruolo back-end o di lavoro in esecuzione, quindi aprirla hello lavoro ruolo toohello macchina virtuale solo all'interno di hello stesso tenant.

## <a name="isolation"></a>Isolamento
Un altro requisito di protezione cloud importante è la separazione tooprevent trasferimento autorizzato o non intenzionale di informazioni tra le distribuzioni in un'architettura multi-tenant condivisa.

Azure implementa il [controllo di accesso alla rete](https://azure.microsoft.com/blog/network-isolation-options-for-machines-in-windows-azure-virtual-networks/) e la separazione tramite l'isolamento VLAN, gli ACL, i servizi di bilanciamento del carico e i filtri IP. Limita il traffico esterno in ingresso tooports e nelle macchine virtuali che definiscono i protocolli. Azure implementa tooprevent spoofing filtrando il traffico di rete e limita i componenti della piattaforma tootrusted traffico in ingresso e in uscita. Nei dispositivi di protezione perimetrale vengono implementati criteri di flusso che rifiutano il traffico per impostazione predefinita.

![Microsoft Antimalware in Azure](./media/azure-security-getting-started/sec-azgsfig3.PNG)

Network Address Translation (NAT) viene utilizzato tooseparate traffico della rete interna da traffico esterno. Il traffico interno non è instradabile all'esterno. Gli [indirizzi IP virtuali](http://blogs.msdn.com/b/cloud_solution_architect/archive/2014/11/08/vips-dips-and-pips-in-microsoft-azure.aspx) instradabili all'esterno vengono convertiti in indirizzi [IP dinamici interni](http://blogs.msdn.com/b/cloud_solution_architect/archive/2014/11/08/vips-dips-and-pips-in-microsoft-azure.aspx) instradabili solo in Azure.

Proteggere tramite firewall tramite ACL traffico esterno tooAzure le macchine virtuali nei router, servizi di bilanciamento del carico e commutatori di livello 3. Sono consentiti solo protocolli noti specifici. Gli ACL sono provenienti dalle macchine virtuali guest tooother VLAN utilizzata per la gestione del traffico toolimit sul posto. Inoltre, il traffico filtrato tramite i filtri IP hello del sistema operativo host ulteriori limiti hello traffico sui livelli di collegamento e la rete sia dati.

### <a name="how-azure-implements-isolation"></a>Come Azure implementa l'isolamento
Hello Controller di infrastruttura di Azure è responsabile dell'allocazione delle risorse di infrastruttura tootenant i carichi di lavoro e gestisce le comunicazioni unidirezionali dal computer di toovirtual hello host. Hello hypervisor Azure impone memoria e processo di separazione tra le macchine virtuali e instrada in modo sicuro i tenant tooguest del sistema operativo di traffico di rete. Azure implementa l'isolamento anche per tenant, archiviazione e reti virtuali.

* Ogni tenant di Azure AD viene isolato in modo logico usando i limiti di sicurezza.
* Gli account di archiviazione di Azure sono tooeach univoco sottoscrizione e l'accesso deve essere autenticato tramite una chiave di account di archiviazione.
* Le reti virtuali vengono isolate in modo logico con una combinazione di indirizzi IP privati univoci, firewall e ACL IP. Servizi di bilanciamento del carico indirizzare traffico toohello appropriati i tenant in base alle definizioni di endpoint.

## <a name="virtual-networks-and-firewalls"></a>Reti virtuali e firewall
Hello [reti virtuali e distribuite](http://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx) nella Guida di Azure, assicurarsi che il traffico di rete privata è logicamente isolato dal traffico in altre reti virtuali di Azure.

![Microsoft Antimalware in Azure](./media/azure-security-getting-started/sec-azgsfig4.PNG)

La sottoscrizione può contenere più reti private isolate e includere firewall, servizi di bilanciamento del carico e Network Address Translation.

Azure offre tre livelli principali di separazione di rete in ogni Azure toologically segregate traffico del cluster. [Reti locali virtuali](https://azure.microsoft.com/services/virtual-network/) (VLAN) vengono utilizzate il traffico dei clienti tooseparate da rest hello di hello rete di Azure. Toohello accesso rete di Azure dall'esterno del cluster di hello è limitato tramite servizi di bilanciamento del carico.

Tooand il traffico di rete da macchine virtuali deve passare attraverso il commutatore virtuale di hello hypervisor. componente di filtro IP Hello nel sistema operativo radice hello isola hello radice macchina virtuale le macchine virtuali guest hello e le macchine virtuali guest hello uno da altro. Esegue il filtro di comunicazione toorestrict il traffico tra i nodi di un tenant e hello pubblico (basati su Internet nella configurazione del servizio del cliente hello), li adeguatamente dagli altri tenant.

filtro IP Hello impedisce che le macchine virtuali guest da:

* Generare traffico falsificato.
* Ricezione di traffico non risolti toothem.
* Endpoint dell'infrastruttura tooprotected indirizzando il traffico.
* Inviare o ricevere traffico broadcast non appropriato.

È possibile inserire le macchine virtuali nelle [reti virtuali di Azure](https://azure.microsoft.com/documentation/services/virtual-network/). Queste reti virtuali sono simili reti toohello configuri in ambienti on-premise, in cui sono in genere associati a un commutatore virtuale. Macchine virtuali connesse toohello stessa rete virtuale può comunicare tra loro senza alcuna configurazione aggiuntiva. È anche possibile configurare subnet diverse nella rete virtuale.

È possibile utilizzare hello seguenti comunicazioni protette toohelp tecnologie di rete virtuale di Azure nella rete virtuale:

* [**Gruppi di sicurezza di rete (NSG)**](../virtual-network/virtual-networks-nsg.md). È possibile utilizzare un tooone traffico toocontrol di gruppo o più istanze di macchine virtuali nella rete virtuale. Un NSG contiene le regole di controllo di accesso che consentono o negano il traffico in base alla direzione del traffico, al protocollo, all’indirizzo e alla porta di origine e all’indirizzo e alla porta di destinazione.
* [**Routing definito dall'utente**](../virtual-network/virtual-networks-udr-overview.md). È possibile controllare hello il routing dei pacchetti tramite un dispositivo virtuale tramite la creazione di route definite dall'utente che specificano l'hop successivo di hello per i pacchetti che passano dello strumento di protezione di tooa subnet specifica toogo tooa rete virtuale.
* [**Inoltro IP**](../virtual-network/virtual-networks-udr-overview.md). Un dispositivo di sicurezza di rete virtuale deve essere in grado di tooreceive il traffico in ingresso che non è indirizzato tooitself. il traffico di una macchina virtuale tooreceive tooallow inoltrate tooother destinazioni, è abilitare l'inoltro IP per la macchina virtuale hello.
* [**Tunneling forzato**](../vpn-gateway/vpn-gateway-about-forced-tunneling.md). Il tunneling forzato consente di reindirizzare o "forzare" tutto il traffico associato a Internet generato da macchine virtuali in un percorso locale della rete virtuale tooyour indietro tramite un tunnel VPN da sito a sito per l'ispezione e controllo
* [**ACL endpoint**](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). È possibile controllare i computer in cui sono consentiti le connessioni in ingresso dalla macchina virtuale di hello Internet tooa nella rete virtuale mediante la definizione di ACL dell'endpoint.
* [**Soluzioni di sicurezza di rete dei partner**](https://azure.microsoft.com/marketplace/). Esistono numerose soluzioni di sicurezza di rete dei partner che è possibile accedere da hello Azure Marketplace.

### <a name="how-azure-implements-virtual-networks-and-firewalls"></a>Come Azure implementa le reti virtuali e i firewall
Per impostazione predefinita, Azure implementa firewall con filtro dei pacchetti in tutte le macchine virtuali host e guest. Le immagini del sistema operativo Windows da hello Azure Marketplace dispone anche di Windows Firewall è abilitato per impostazione predefinita. Servizi di bilanciamento del carico nel perimetro hello delle comunicazioni di controllo di Azure pubblico reti basato su IP ACL gestiti dagli amministratori di clienti.

Se Azure sposta i dati di un cliente durante le normali operazioni o durante un'emergenza, l'azione viene eseguita su canali di comunicazioni crittografati privati. Le altre funzionalità usati da Azure toouse nel firewall e reti virtuali sono:

* **Firewall host nativo**: Azure Service Fabric e Archiviazione di Azure vengono eseguiti in un sistema operativo nativo senza hypervisor, Di conseguenza hello windows firewall è configurato con hello precedente due set di regole. Archiviazione esegue prestazioni toooptimize nativo.
* **Firewall host**: firewall host hello è tooprotect hello host sistema operativo eseguito hello hypervisor. le regole di Hello sono l'unico controller di infrastruttura servizio hello tooallow programmati e passare sistema operativo dell'host caselle tootalk toohello su una porta specifica. Hello altre eccezioni sono risposta DHCP tooallow e le risposte DNS. Azure Usa un file di configurazione di computer che ha un modello di regole firewall per sistema operativo host hello hello. host Hello stesso è protetto da attacchi esterni tramite una comunicazione toopermit di Windows firewall configurate solo da origini autenticate, note.
* **Firewall guest**: replica regole hello nel filtro di pacchetti commutatore di macchina virtuale di hello ma programmati nel software diverso (ad esempio parte di Windows Firewall hello del sistema operativo guest hello). firewall di macchina virtuale guest Hello può essere configurato toorestrict comunicazioni tooor dalla macchina virtuale guest di hello, anche se è consentita la comunicazione di hello dalle configurazioni host hello filtro dell'indirizzo IP. Ad esempio, è possibile scegliere di comunicazione di toorestrict firewall per la macchina virtuale guest toouse hello tra due le reti virtuali che sono stati configurati tooconnect tooone un altro.
* **Firewall di archiviazione (FW)**: firewall hello nel front-end di archiviazione hello filtri toobe traffico solo sulle porte 80/443 e le altre porte necessarie utilità. firewall Hello back-end di archiviazione hello limita le comunicazioni toocome solo dal server front-end di archiviazione.
* **Gateway di rete virtuale**: hello [il Gateway di rete virtuale di Azure](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md) funge da gateway cross-premise hello connessione i carichi di lavoro nella rete virtuale di Azure tooyour siti locali. È necessario tooconnect siti tooon locali tramite [dei tunnel VPN IPsec site-to-site](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md), o tramite [ExpressRoute](../expressroute/expressroute-introduction.md) circuiti. Per i tunnel VPN IPsec/IKE gateway hello eseguire handshake IKE e stabilire il tunnel VPN S2S IPsec hello tra reti virtuali hello e siti locali. I gateway di rete virtuale terminano anche le [VPN da punto a sito](../vpn-gateway/vpn-gateway-point-to-site-create.md).

## <a name="secure-remote-access"></a>Accesso remoto sicuro
Dati archiviati nel cloud hello devono avere sufficiente misure di sicurezza abilitati tooprevent exploit e mantenere la riservatezza e integrità durante il transito. Queste misure includono controlli di rete associati ai meccanismi di gestione delle identità e dell'accesso controllabile e basata su criteri di un'organizzazione.

Tecnologia di crittografia incorporata consente tooencrypt le comunicazioni all'interno e tra le distribuzioni, tra le aree di Azure e dal Data Center di Azure tooon locale. Amministratore accesso toovirtual macchine tramite [sessioni di desktop remoto](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), [remoto Windows PowerShell](http://blogs.technet.com/b/heyscriptingguy/archive/2013/09/07/weekend-scripter-remoting-the-cloud-with-windows-azure-and-powershell.aspx), e hello portale di Azure verrà sempre crittografato.

toosecurely estendere locale datacenter toohello cloud, Azure mette a disposizione [VPN site-to-site](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md) e [VPN point-to-site](../vpn-gateway/vpn-gateway-point-to-site-create.md), oltre a collegamenti dedicati con [ExpressRoute](../expressroute/expressroute-introduction.md)(tooAzure connessioni alle reti virtuali tramite VPN sono crittografate).

### <a name="how-azure-implements-secure-remote-access"></a>Come Azure implementa l'accesso remoto sicuro
Connessioni toohello portale di Azure deve sempre essere autenticato e richiedono SSL/TLS. È possibile configurare Gestione protetta tooenable certificati di gestione. I protocolli di sicurezza standard del settore, ad esempio [SSTP](https://technet.microsoft.com/magazine/2007.06.cableguy.aspx) e [IPsec](https://en.wikipedia.org/wiki/IPsec) sono completamente supportati.

[Azure ExpressRoute](../expressroute/expressroute-introduction.md) consente di creare connessioni private tra i data center di Azure e l'infrastruttura disponibile localmente o in un ambiente con percorso condiviso. Le connessioni ExpressRoute non sfruttano hello rete Internet pubblica. Offrono più affidabilità, maggiore velocità, latenze più basse e maggiore sicurezza dei normali collegamenti basati su Internet. In alcuni casi, il trasferimento di dati tra dispositivi locali e Azure usando connessioni ExpressRoute può produrre vantaggi significativi in termini di costi.

## <a name="logging-and-monitoring"></a>Registrazione e monitoraggio
Azure offre accesso autenticato di eventi relativi alla sicurezza che generano un audit trail ed è tootampering toobe resistenti decodificati. Sono incluse le informazioni sul sistema, ad esempio i registri eventi di sicurezza nelle macchine virtuali dell'infrastruttura di Azure e in Azure AD. Il monitoraggio degli eventi di sicurezza include la raccolta di eventi, ad esempio le modifiche in indirizzi IP di server DHCP o DNS. tooports tentativi di accesso, i protocolli o indirizzi IP che sono bloccati per impostazione predefinita; modifiche nelle impostazioni di firewall o di criteri di sicurezza. creazione di account o gruppo. e processi imprevisti o installazione del driver.

![Microsoft Antimalware in Azure](./media/azure-security-getting-started/sec-azgsfig5.PNG)

I log di controllo che registrano le attività e l'accesso utente con privilegi, i tentativi di accesso autorizzato e non autorizzato, le eccezioni di sistema e gli eventi di sicurezza delle informazioni vengono conservati per un periodo di tempo stabilito. conservazione Hello dei registri è a propria discrezione, perché si configura la raccolta di log e i propri requisiti di conservazione tooyour.

### <a name="how-azure-implements-logging-and-monitoring"></a>Come Azure implementa la registrazione e il monitoraggio
Azure consente di distribuire gli agenti di gestione (agente di gestione) e Monitor di sicurezza di Azure (ASM) calcolo tooeach agenti, l'archiviazione o il nodo fabric in gestione nativa o virtuale. Ogni agente di gestione è configurato tooauthenticate tooa servizio team account di archiviazione con un certificato ottenuto dall'archivio di certificati di Azure hello e rollforward preconfigurato diagnostica e account di archiviazione toohello dati evento. Questi agenti non sono macchine virtuali distribuite toocustomers.

Gli amministratori di Azure di accedere ai log tramite un portale web per l'accesso autenticato e controllato toohello log. Un amministratore può analizzare, filtrare e correlare i log. gli account di archiviazione team Hello servizio di Azure per i log siano protetti da toohelp accesso amministratore diretto impediscono contro eventuali manomissioni log.

Microsoft raccoglie i log dai dispositivi di rete utilizzando il protocollo di Syslog hello e dai server host utilizzando Microsoft Audit Collection Services (ACS). Questi log vengono inseriti in un database di log dal quale vengono generati avvisi relativi a eventi sospetti. messaggio per l'amministratore può accedere e analizzare questi registri.

[Diagnostica di Azure](https://msdn.microsoft.com/library/azure/gg433048.aspx) è una funzionalità di Azure che permette toocollect i dati di diagnostica da un'applicazione in esecuzione in Azure. Si tratta dei dati di diagnostica per il debug, la risoluzione dei problemi, la valutazione delle prestazioni, il monitoraggio dell'utilizzo delle risorse, l'analisi del traffico, la pianificazione della capacità e il controllo. Dopo la raccolta dei dati di diagnostica hello, può essere trasferito tooan account di archiviazione di Azure per la persistenza. I trasferimenti possono essere pianificati o su richiesta.

## <a name="threat-mitigation"></a>Prevenzione delle minacce
In aggiunta tooisolation, la crittografia e applicazione di filtri, Azure utilizza un numero di meccanismi di attenuazione di minacce e processi tooprotect infrastruttura e dei servizi. Sono inclusi controlli interni e le tecnologie utilizzate toodetect e correzione delle minacce avanzate, ad esempio DDoS, l'escalation dei privilegi e hello [OWASP primi 10](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project).

controlli di sicurezza Hello e processi di gestione dei rischi Microsoft di toosecure sul posto dell'infrastruttura cloud ridurre hello rischio di problemi di protezione. In hello si verifica l'evento imprevisto, team di gestione eventi imprevisti di protezione (SIM) hello all'interno del team di Microsoft Online Services di sicurezza e conformità (OSSC) hello è pronto toorespond in qualsiasi momento.

### <a name="how-azure-implements-threat-mitigation"></a>Come Azure implementa la prevenzione delle minacce
Azure dispone di controlli di sicurezza in attenuazione delle minacce tooimplement sul posto e anche i clienti toohelp minacce potenziali nei propri ambienti. Hello elenco seguente vengono riepilogate le funzionalità di prevenzione minaccia hello offerte da Azure:

* [Azure Antimalware](azure-security-antimalware.md) è abilitato per impostazione predefinita in tutti i server dell'infrastruttura. Facoltativamente è possibile abilitarlo nelle macchine virtuali.
* Microsoft gestisce monitoraggio tra server, reti e applicazioni minacce toodetect continuo e impedire gli attacchi. Avvisi automatizzati notifica agli amministratori di comportamenti anomali, consentendo di azione correttiva tootake delle minacce interne ed esterne.
* È possibile distribuire le soluzioni di sicurezza di terze parti all'interno delle sottoscrizioni, ad esempio i Web application firewall di [Barracuda](https://techlib.barracuda.com/ng54/deployonazure).
* Microsoft test toopenetration approccio include "[gruppo rosso](http://download.microsoft.com/download/C/1/9/C1990DBA-502F-4C2A-848D-392B93D9B9C3/Microsoft_Enterprise_Cloud_Red_Teaming.pdf)," che implica professionisti della sicurezza Microsoft attaccare i sistemi di produzione in tempo reale (non-cliente) in Azure tootest difesa reali, avanzate , minacce persistenti.
* Sistemi di distribuzione integrata gestire hello distribuzione e installazione delle patch di protezione tra hello piattaforma Azure.

## <a name="next-steps"></a>Passaggi successivi
[Centro protezione di Azure](https://azure.microsoft.com/support/trust-center/)

[Blog del team di sicurezza di Azure](http://blogs.msdn.com/b/azuresecurity/)

[Microsoft Security Response Center](https://technet.microsoft.com/library/dn440717.aspx)

[Blog di Active Directory](http://blogs.technet.com/b/ad/)
