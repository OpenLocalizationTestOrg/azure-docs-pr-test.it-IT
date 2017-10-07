---
title: requisiti di sistema aaaStorSimple | Documenti Microsoft
description: "Descrive i requisiti relativi a software, rete e alta disponibilità e le procedure consigliate per una soluzione Microsoft Azure StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2b6ca34a-d758-48e7-ab1e-4fdd80cf48d4
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/06/2017
ms.author: alkohli
ms.openlocfilehash: ec0bb5ad2f2d4c9901da2d95147dd9daa178f6b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-software-high-availability-and-networking-requirements"></a>Software, disponibilità elevata e requisiti di rete di StorSimple
## <a name="overview"></a>Panoramica
Benvenuti tooMicrosoft StorSimple di Azure. Questo articolo descrive i requisiti di sistema importanti e procedure consigliate per il dispositivo StorSimple e per l'accesso dispositivo hello client di archiviazione di hello. È consigliabile rivedere attentamente le informazioni di hello prima di distribuire il sistema di StorSimple, quindi fare riferimento tooit come necessarie durante la distribuzione e l'operazione successiva.

i requisiti di sistema Hello includono:

* **Requisiti software per client di archiviazione** -descrive i sistemi operativi supportato hello e eventuali requisiti aggiuntivi per questi sistemi operativi.
* **Requisiti di rete per il dispositivo StorSimple hello** -fornisce informazioni sulle porte hello toobe che è necessario aprire in tooallow il firewall per il traffico iSCSI, cloud o di gestione.
* **Requisiti di disponibilità elevata per StorSimple** : descrive i requisiti di disponibilità elevata e le procedure consigliate per il dispositivo StorSimple e il computer host. 

## <a name="software-requirements-for-storage-clients"></a>Requisiti software per i client di archiviazione
Hello requisiti software seguenti è per i client di archiviazione hello che accedono a un dispositivo StorSimple.

| Sistemi operativi supportati | Versione richiesta | Requisiti aggiuntivi/note |
| --- | --- | --- |
| Windows Server |2008R2 SP1, 2012, 2012R2, 2016 |I volumi iSCSI StorSimple sono supportati per l'utilizzo in solo hello tipi di dischi Windows seguenti:<ul><li>Volume semplice su disco di base</li><li>Volume semplice e con mirroring su disco dinamico</li></ul>Sono supportati solo hello software iniziatori iSCSI presenti in modo nativo nel sistema operativo hello. Gli iniziatori iSCSI hardware non sono supportati.<br></br>Le funzionalità ODX e di thin provisioning di Windows Server 2012 e 2016 sono supportate se si usa un volume iSCSI StorSimple.<br><br>StorSimple consente di creare volumi di thin provisioning o di provisioning completo. Non è in grado di creare volumi con provisioning parziale.<br><br>La riformattazione di un volume con thin provisioning può richiedere molto tempo. È consigliabile eliminare il volume di hello e quindi crearne uno nuovo anziché riformattare. Tuttavia, se è comunque preferibile tooreformat un volume:<ul><li>Eseguire hello comando prima di ritardi nel recupero dello spazio di hello riformatta tooavoid seguente: <br>`fsutil behavior set disabledeletenotify 1`</br></li><li>Dopo aver completata la formattazione hello, recupero di spazio toore attiva comando che segue hello di utilizzare:<br>`fsutil behavior set disabledeletenotify 0`</br></li><li>Applicare l'hotfix di Windows Server 2012 hello come descritto in [KB 2878635](https://support.microsoft.com/kb/2870270) tooyour computer di Windows Server.</li></ul></li></ul></ul> Se si configura Gestione Snapshot StorSimple o l'adattatore StorSimple per SharePoint, andare troppo[requisiti Software per i componenti facoltativi](#software-requirements-for-optional-components). |
| VMWare ESX |5.5 e 6.0 |Supportato con VMware vSphere come client iSCSI. Funzionalità VAAI-Block supportata con VMware vSphere in dispositivi StorSimple. |
| Linux RHEL/CentOS |5, 6 e 7 |Supporto per client Linux iSCSI con iniziatore Open-iSCSI versioni 5, 6 e 7. |
| Linux |SUSE Linux 11 | |

> [!NOTE]
> IBM AIX attualmente non è supportato con StorSimple.
> 
> 

## <a name="software-requirements-for-optional-components"></a>Requisiti software per i componenti facoltativi
Hello requisiti software seguenti è per hello StorSimple componenti facoltativi (gestione Snapshot StorSimple e adattatore StorSimple per SharePoint).

| Componente | Piattaforma host | Requisiti aggiuntivi/note |
| --- | --- | --- |
| Gestione snapshot StorSimple |Windows Server 2008R2 SP1, 2012, 2012R2 |L'uso di Gestione snapshot StorSimple su Windows Server è necessario per eseguire il backup o il ripristino di dischi dinamici con mirroring e per qualsiasi backup coerente con l'applicazione.<br> StorSimple Snapshot Manager è supportato solo su Windows Server 2008 R2 SP1 (64 bit), Windows 2012 R2 e Windows Server 2012.<ul><li>Se si usa Windows Server 2012, è necessario installare .NET 3.5 o 4.5 prima di installare StorSimple Snapshot Manager.</li><li>Se si usa Windows Server 2008 R2 SP1, è necessario installare Windows Management Framework 3.0 prima di installare StorSimple Snapshot Manager.</li></ul> |
| Adattatore StorSimple per SharePoint |Windows Server 2008R2 SP1, 2012, 2012R2 |<ul><li>L'adattatore StorSimple per SharePoint è supportato solo in SharePoint 2010 e SharePoint 2013.</li><li>Per RBS è necessario SQL Server Enterprise Edition, versioni 2008 R2 o 2012.</li></ul> |

## <a name="networking-requirements-for-your-storsimple-device"></a>Requisiti di rete per il dispositivo StorSimple
Il dispositivo StorSimple è un dispositivo bloccato. Tuttavia, è necessario toobe aperto in tooallow il firewall per iSCSI, cloud e il traffico di gestione porte. Hello nella tabella seguente elenca le porte hello necessarie toobe aperte nel firewall. In questa tabella, *in* o *in ingresso* fa riferimento toohello direzione da cui le richieste client in ingresso accesso al dispositivo. *Out* o *in uscita* fa riferimento toohello direzione in cui il dispositivo StorSimple invia i dati all'esterno, oltre distribuzione hello: ad esempio, in uscita toohello Internet.

| Numero porta<sup>1, 2</sup> | In ingresso/In uscita | Ambito porta | Obbligatoria | Note |
| --- | --- | --- | --- | --- |
| TCP 80 (HTTP)<sup>3</sup> |In uscita |WAN |No |<ul><li>Porta in uscita viene utilizzata per gli aggiornamenti di tooretrieve accesso Internet.</li><li>proxy web in uscita Hello è configurabile dall'utente.</li><li>gli aggiornamenti del sistema tooallow, questa porta deve essere aperta per hello IP fissato dei controller.</li></ul> |
| TCP 443 (HTTPS)<sup>3</sup> |In uscita |WAN |Sì |<ul><li>Porta in uscita viene utilizzata per l'accesso ai dati nel cloud hello.</li><li>proxy web in uscita Hello è configurabile dall'utente.</li><li>gli aggiornamenti del sistema tooallow, questa porta deve essere aperta per hello IP fissato dei controller.</li><li>Questa porta viene inoltre utilizzata in entrambi i controller hello di garbage collection.</li></ul> |
| UDP 53 (DNS) |In uscita |WAN |In alcuni casi; vedere le note. |Questa porta è obbligatoria solo se si usa un server DNS basato su Internet. |
| UDP 123 (NTP) |In uscita |WAN |In alcuni casi; vedere le note. |Questa porta è obbligatoria solo se si usa un server NTP basato su Internet. |
| TCP 9354 |In uscita |WAN |Sì |porta in uscita di Hello è utilizzata da hello StorSimple dispositivo toocommunicate con hello servizio StorSimple Manager. |
| 3260 (iSCSI) |In ingresso |LAN |No |Questa porta è tooaccess utilizzati dati tramite iSCSI. |
| 5985 |In ingresso |LAN |No |Porta in ingresso viene utilizzata da Gestione Snapshot StorSimple toocommunicate con dispositivo StorSimple hello.<br>Questa porta viene utilizzata anche quando ci si connette in remoto tooWindows PowerShell per StorSimple tramite HTTP. |
| 5986 |In ingresso |LAN |No |Questa porta viene utilizzata quando ci si connette in remoto tooWindows PowerShell per StorSimple tramite HTTPS. |

<sup>1</sup> alcuna porta in ingresso non necessario toobe aperto su hello rete Internet pubblica.

<sup>2</sup> se più porte esiste una configurazione gateway, ordine di hello indirizzato il traffico in uscita verrà determinato in base a ordine di routing porta hello descritto in [porta routing](#routing-metric)riportato di seguito.

<sup>3</sup> controller hello gli indirizzi IP fissata del dispositivo StorSimple deve essere instradabile su e in grado di tooconnect toohello Internet, direttamente o tramite hello configurato proxy web. gli indirizzi IP fissata Hello vengono utilizzati per la manutenzione dispositivo toohello gli aggiornamenti di hello. Se il controller del dispositivo hello non può connettersi a Internet tramite hello indirizzi IP fissi toohello, non sarà in grado di tooupdate dispositivo StorSimple.

> [!IMPORTANT]
> Verificare che il firewall hello non modificare o decrittografare tutto il traffico SSL tra il dispositivo di StorSimple hello e Azure.
> 
> 

### <a name="url-patterns-for-firewall-rules"></a>Modelli URL per le regole del firewall
Gli amministratori di rete spesso possono configurare un firewall avanzato regole basate su hello toofilter modelli di hello URL in ingresso e hello il traffico in uscita. Il dispositivo StorSimple e il servizio StorSimple Manager hello dipendono da altre applicazioni di Microsoft, ad esempio Azure Service Bus, Access Control di Azure Active Directory, gli account di archiviazione e server di Microsoft Update. pattern di URL Hello associati a queste applicazioni può essere utilizzato tooconfigure regole del firewall. È importante toounderstand che è possono modificare i modelli di URL hello associati a queste applicazioni. Ciò a sua volta è necessario toomonitor amministratore di rete hello e aggiornare le regole del firewall per StorSimple come e quando richiesto.

È consigliabile impostare le regole del firewall per il traffico in uscita, liberamente nella maggior parte dei casi, in base agli indirizzi IP StorSimple. Tuttavia, è possibile utilizzare informazioni hello sotto tooset avanzate regole del firewall che sono gli ambienti protetti toocreate necessari.

> [!NOTE]
> dispositivo Hello (origine) gli indirizzi IP deve essere sempre impostato interfacce di rete tooall hello abilitato. destinazione Hello gli indirizzi IP devono essere impostato troppo[intervalli IP Data Center di Azure](https://www.microsoft.com/en-us/download/confirmation.aspx?id=41653).
> 
> 

#### <a name="url-patterns-for-azure-portal"></a>Modelli di URL per il portale di Azure
| Modello URL | Componente/funzionalità | Indirizzi IP dispositivo |
| --- | --- | --- |
| `https://*.storsimple.windowsazure.com/*`<br>`https://*.accesscontrol.windows.net/*`<br>`https://*.servicebus.windows.net/*` |Servizio StorSimple Manager<br>Servizio di controllo di accesso<br>Bus di servizio di Azure |Interfacce di rete abilitate per il cloud |
| `https://*.backup.windowsazure.com` |Registrazione del dispositivo |Solo DATA 0 |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Revoca del certificato |Interfacce di rete abilitate per il cloud |
| `https://*.core.windows.net/*` <br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Account di archiviazione di Azure e monitoraggio |Interfacce di rete abilitate per il cloud |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Server di Microsoft Update<br> |Solo indirizzi IP fissi del controller |
| `http://*.deploy.akamaitechnologies.com` |Rete CDN di Akamai |Solo indirizzi IP fissi del controller |
| `https://*.partners.extranet.microsoft.com/*` |Pacchetto di supporto |Interfacce di rete abilitate per il cloud |

#### <a name="url-patterns-for-azure-government-portal"></a>Modelli di URL per il portale di Azure Government
| Modello URL | Componente/funzionalità | Indirizzi IP dispositivo |
| --- | --- | --- |
| `https://*.storsimple.windowsazure.us/*`<br>`https://*.accesscontrol.usgovcloudapi.net/*`<br>`https://*.servicebus.usgovcloudapi.net/*` |Servizio StorSimple Manager<br>Servizio di controllo di accesso<br>Bus di servizio di Azure |Interfacce di rete abilitate per il cloud |
| `https://*.backup.windowsazure.us` |Registrazione del dispositivo |Solo DATA 0 |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Revoca del certificato |Interfacce di rete abilitate per il cloud |
| `https://*.core.usgovcloudapi.net/*` <br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Account di archiviazione di Azure e monitoraggio |Interfacce di rete abilitate per il cloud |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Server di Microsoft Update<br> |Solo indirizzi IP fissi del controller |
| `http://*.deploy.akamaitechnologies.com` |Rete CDN di Akamai |Solo indirizzi IP fissi del controller |
| `https://*.partners.extranet.microsoft.com/*` |Pacchetto di supporto |Interfacce di rete abilitate per il cloud |

### <a name="routing-metric"></a>Metrica di routing
Metrica di routing è associata a interfacce hello e gateway hello che rimandano toohello dati hello specificato reti. Metrica di routing viene utilizzato da hello routing protocol toocalculate hello migliore percorso tooa dato di destinazione, se apprende più percorsi esistano toohello stessa destinazione. Hello inferiore hello routing metrica, hello hello preferenza superiore.

In hello contesto di StorSimple, se più interfacce di rete e i gateway sono configurati il traffico toochannel, metriche di routing hello accedono play toodetermine hello ordine relativo in cui hello ottenere utilizzare interfacce. metriche di routing Hello non possono essere modificate da utente hello. È tuttavia possibile utilizzare hello `Get-HcsRoutingTable` tooprint cmdlet out hello tabella di routing (e le metriche) nel dispositivo StorSimple. Altre informazioni sul cmdlet Get-HcsRoutingTable disponibili in [Risoluzione dei problemi di distribuzione del dispositivo StorSimple](storsimple-troubleshoot-deployment.md).

Hello routing algoritmi metrica è diverso a seconda della versione del software hello in esecuzione sul dispositivo StorSimple.

**Le versioni precedenti tooUpdate 1**

Sono incluse versioni software la versione precedente tooUpdate 1, ad esempio hello GA, 0,1, 0,2 o 0,3. ordine di Hello in base alle metriche di routing è il seguente:

   *Ultima interfaccia di rete 10 GbE configurata > Altra interfaccia di rete 10 GbE > Ultima interfaccia di rete 1 GbE configurata > Altra interfaccia di rete 1 GbE*

**Versioni a partire da Update 1 e 2 di tooUpdate precedente**

Sono comprese le versioni software come 1, 1.1 e 1.2. ordine di Hello in base alle metriche di routing viene stabilito come indicato di seguito:

   *DATA 0 > Ultima interfaccia di rete 10 GbE configurata > Altra interfaccia di rete 10 GbE > Ultima interfaccia di rete 1 GbE configurata > Altra interfaccia di rete 1 GbE*

   In Update 1, metrica di routing hello di DATA 0 viene reso hello più basso; Pertanto, tutti i cloud hello-il traffico viene instradato attraverso DATA 0. Tenere presente questo criterio se sono presenti più interfacce di rete abilitate per il cloud nel dispositivo StorSimple.

**Versioni a partire dall'aggiornamento 2**

Aggiornamento 2 presenta diversi miglioramenti correlati alle reti e le metriche di routing hello sono stato modificato. comportamento di Hello può essere spiegato nel modo seguente.

* Un set di valori predefiniti sono stati assegnati toonetwork interfacce.     
* Si consideri una tabella di esempio illustrata di seguito con i valori assegnati toohello varie interfacce di rete quando vengono cloud abilitato o disabilitato di cloud, ma con un gateway configurato. I valori hello nota assegnati qui sono solo i valori di esempio.

    | Interfaccia di rete | Abilitata per il cloud | Disabilitata per il cloud con gateway |
    |-----|---------------|---------------------------|
    | Data 0  | 1            | -                        |
    | Data 1  | 2            | 20                       |
    | Data 2  | 3            | 30                       |
    | Data 3  | 4            | 40                       |
    | Data 4  | 5            | 50                       |
    | Data 5  | 6            | 60                       |


* l'ordine in cui verrà indirizzato il traffico cloud hello tramite le interfacce di rete hello Hello è:
  
    *Data 0 &gt; Data 1 &gt; Data 2 &gt; Data 3 &gt; Data 4 &gt; Data 5*
  
    Ciò è dovuto hello di esempio seguente.
  
    Si consideri un dispositivo StorSimple con due interfacce di rete abilitate per il cloud, Data 0 e Data 5. Le interfacce da Data 1 a Data 4 sono disabilitate per il cloud ma dispongono di un gateway configurato. ordine di Hello in cui verrà indirizzato il traffico per questo dispositivo sarà:
  
    *Data 0 (1) &gt; Data 5 (6) &gt; Data 1 (20) &gt; Data 2 (30) &gt; Data 3 (40) &gt; Data 4 (50)*
  
    *dove hello numeri racchiuso tra parentesi indicano le metriche di routing rispettivi hello.*
  
    Se non viene Data 0, il traffico cloud hello verrà instradato a Data 5. Dato che un gateway è configurato in tutte le altre reti, se i dati 0 e Data 5 erano toofail, traffico cloud hello verrà sottoposte al Data 1.
* Se un'interfaccia di rete abilitata per il cloud non riesce, vengono quindi 3 tentativi con 30 secondo ritardo tooconnect toohello interfaccia. Se non tutti i tentativi di hello, traffico hello è indirizzato toohello Avanti abilitata per il cloud interfaccia disponibile come determinato dalla tabella di routing hello. Se tutti hello abilitata per il cloud esito negativo di interfacce di rete e dispositivo hello verrà eseguito il failover toohello altri controller (Nessun riavvio in questo caso).
* Se si verifica un errore VIP per un'interfaccia di rete abilitata per iSCSI, verranno eseguiti 3 tentativi con un ritardo di 2 secondi. Questo comportamento ha trascorso hello stesso rispetto alle versioni precedenti hello. Se tutte le interfacce di rete iSCSI hello non riesce, un failover del controller verificherà (accompagnata da un riavvio).
* Viene anche generato un avviso sul dispositivo StorSimple quando si verifica un errore VIP. Per ulteriori informazioni, visitare troppo[avviso riferimento rapido](storsimple-manage-alerts.md).
* Per quanto riguarda i tentativi, iSCSI avrà la precedenza sul cloud.
  
    Prendere in considerazione hello seguente esempio: StorSimple di un dispositivo ha due interfacce di rete abilitate, dati 0 e 1 di dati. Data 0 è abilitata per il cloud, mentre Data 1 è abilitata sia per il cloud che per iSCSI. Nessun'altra interfaccia di rete su questo dispositivo è abilitata per il cloud o iSCSI.
  
    Se ha esito negativo dati 1, esso è l'interfaccia di rete iSCSI ultimo hello, questo comporterà un tooData failover controller 1 hello in altri controller.

### <a name="networking-best-practices"></a>Procedure di rete consigliate
Inoltre toohello sopra requisiti di rete, per ottenere prestazioni ottimali della soluzione StorSimple, hello attenersi toohello procedure consigliate seguenti:

* Verificare che per il dispositivo StorSimple sia sempre disponibile una larghezza di banda dedicata pari a 40 Mbps (o superiore). Non è possibile condividere la larghezza di banda (o allocazione deve essere garantita tramite l'utilizzo di hello dei criteri QoS) con altre applicazioni.
* Verificare la connettività di rete toohello Internet è disponibile in qualsiasi momento. Sporadici o non affidabili Internet connessioni toohello dispositivi, tra cui senza connessione a Internet, qualunque comporterà una configurazione non supportata.
* Isolare il traffico iSCSI e cloud hello dedicati interfacce di rete nel dispositivo per l'accesso iSCSI e cloud. Per ulteriori informazioni, vedere come troppo[modificare interfacce di rete](storsimple-modify-device-config.md#modify-network-interfaces) nel dispositivo StorSimple.
* Evitare di usare una configurazione LACP (Link Aggregation Control Protocol) per le interfacce di rete. Si tratta di una configurazione non supportata.

## <a name="high-availability-requirements-for-storsimple"></a>Requisiti di disponibilità elevata per StorSimple
piattaforma hardware Hello incluso con la soluzione StorSimple hello include funzionalità di disponibilità e affidabilità che costituiscono il fondamento per un'infrastruttura di archiviazione a disponibilità elevata e a tolleranza di errore nel Data Center. Tuttavia, esistono requisiti e procedure consigliate che devono essere conformi a toohelp garantiscono la disponibilità di hello della soluzione StorSimple. Prima di distribuire StorSimple, rivedere attentamente hello seguendo i requisiti e procedure consigliate per il dispositivo StorSimple hello e computer host connessi.

Per ulteriori informazioni sul monitoraggio e gestione hello di componenti hardware del dispositivo StorSimple, andare troppo[utilizzare componenti di hardware toomonitor servizio StorSimple Manager hello e stato](storsimple-monitor-hardware-status.md) e [StorSimple sostituzione dei componenti hardware](storsimple-hardware-component-replacement.md).

### <a name="high-availability-requirements-and-procedures-for-your-storsimple-device"></a>Procedure e requisiti di disponibilità elevata per il dispositivo StorSimple
Hello rivedere attentamente le seguenti informazioni tooensure hello la disponibilità elevata del dispositivo StorSimple.

#### <a name="pcms"></a>PCM
I dispositivi StorSimple includono moduli di alimentazione e raffreddamento (PCM, Power and Cooling Module) ridondanti con supporto per lo swapping a caldo. Ogni PCM dispone di sufficiente servizio tooprovide capacità per l'intero chassis hello. tooensure la disponibilità elevata, entrambi i moduli PCM deve essere installata.

* Connettere la disponibilità del PCM toodifferent power origini tooprovide se l'interruzione dell'alimentazione.
* In caso di errore di un PCM, richiedere immediatamente una sostituzione.
* Rimuovere un PCM non funzionante solo quando si dispone di sostituzione hello e tooinstall pronto è.
* Non rimuovere tutti e due i PCM contemporaneamente. modulo PCM Hello include hello modulo batteria di backup. La rimozione entrambi di hello PCM comporterà un arresto senza protezione batteria e lo stato del dispositivo hello non verrà salvato. Per ulteriori informazioni sulla batteria hello, andare troppo[modulo batteria di backup di manutenzione hello](storsimple-battery-replacement.md#maintain-the-backup-battery-module).

#### <a name="controller-modules"></a>Moduli controller
I dispositivi StorSimple comprendono moduli controller ridondanti con supporto per lo swapping a caldo. i moduli controller Hello operano in modo attivo/passivo. In qualsiasi momento, un modulo controller è attivo e fornisce il servizio, mentre hello altro modulo controller è passivo. modulo controller passivo Hello viene acceso e diventa operativo se il modulo controller attivo hello ha esito negativo o viene rimosso. Ogni modulo controller dispone di sufficiente servizio tooprovide capacità per l'intero chassis hello. Entrambi i moduli controller devono essere installati tooensure la disponibilità elevata.

* Verificare che entrambi i moduli controller siano sempre installati.
* In caso di errore di un modulo controller, richiedere immediatamente una sostituzione.
* Rimuovere un modulo controller non funzionante solo quando si dispone di sostituzione hello e tooinstall pronto è. Rimozione di un modulo per periodi prolungati verrà influiscono sul flusso d'aria hello e pertanto hello raffreddamento del sistema hello.
* Assicurarsi che i moduli controller tooboth di hello rete connessioni sono identici e le interfacce di rete connessa hello hanno una configurazione di rete identiche.
* Se un modulo controller non riesce o deve essere sostituito, assicurarsi che tale hello altro modulo controller è in uno stato attivo prima di sostituire modulo controller non funzionante hello. tooverify che un controller è attivo, andare troppo[controller attivo hello di identificazione sul dispositivo](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device).
* Non rimuovere entrambi i moduli controller in hello contemporaneamente. Se un failover del controller è in corso, non arrestare modulo controller in standby hello o rimuoverlo dal chassis hello.
* Dopo il failover di un controller, attendere almeno cinque minuti prima di rimuovere uno dei moduli.

#### <a name="network-interfaces"></a>Interfacce di rete
Ogni modulo controller del dispositivo StorSimple ha quattro interfacce di rete 1 Gigabit e due interfacce di rete 10 Gigabit Ethernet.

* Assicurarsi che i moduli controller tooboth di hello rete connessioni sono identici e interfacce di rete di hello che le interfacce dei moduli controller hello siano connessi toohave stessa configurazione di rete.
* Quando possibile, distribuire le connessioni di rete tra la disponibilità del servizio di diversi commutatori tooensure nell'evento hello di un errore di dispositivo di rete.
* Quando a scollegare solo hello o hello ultima rimanente interfaccia abilitata per iSCSI (con indirizzi IP assegnati), disabilitare prima interfaccia hello e quindi scollegare i cavi di hello. Se l'interfaccia hello viene scollegato prima volta, causerà hello controller attivo toofail sul controller passivo toohello. Se il controller passivo hello dispone anche le interfacce corrispondenti scollegate, entrambi i controller hello verranno riavviato più volte prima con la consueta risoluzione in un controller.
* Connettersi ad almeno due rete toohello interfacce di dati da ogni modulo controller.
* Se è stato abilitato le interfacce di hello due da 10 GbE, distribuirle tra diversi commutatori.
* Se possibile, usare MPIO nel server tooensure che server hello in grado di tollerare un collegamento, rete o errori dell'interfaccia.

Per ulteriori informazioni sulla rete del dispositivo per la disponibilità elevata e prestazioni, visitare troppo[installare il dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) o [installare del dispositivo 8600 StorSimple](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).

#### <a name="ssds-and-hdds"></a>SSD e HDD
I dispositivi StorSimple includono unità SSD (Solid State Drive) e unità disco rigido protette mediante spazi con mirroring. Utilizzo di spazi con mirroring assicura che il dispositivo hello è errore hello tootolerate in grado di uno o più unità SSD o HDD.

* Accertarsi che tutti i moduli SSD e HDD siano installati.
* In caso di errore di un'unità SSD o HDD, richiedere immediatamente una sostituzione.
* Se un'unità SSD o HDD non riesce o richiede la sostituzione, assicurarsi di rimuovere solo hello unità SSD o HDD che richiede la sostituzione.
* Non rimuovere più di una unità SSD o HDD dal sistema hello in qualsiasi punto nel tempo.
  Un errore di due o più dischi di un determinato tipo (HDD, SSD) o più errori consecutivi in un breve intervallo di tempo possono provocare un problema di funzionamento del sistema e una potenziale perdita di dati. In questo caso, [contattare il supporto tecnico Microsoft](storsimple-contact-microsoft-support.md) per assistenza.
* Durante la sostituzione, monitorare hello **stato Hardware** in hello **manutenzione** pagina per le unità hello hello SSD e HDD. Lo stato di un segno di spunta verde indica che i dischi hello integro o OK, mentre un punto esclamativo rosso indica un errore unità SSD o HDD.
* È consigliabile configurare snapshot nel cloud per tutti i volumi che è necessario tooprotect in caso di errore di sistema.

#### <a name="ebod-enclosure"></a>Chassis EBOD
Il modello di dispositivo StorSimple 8600 include un gruppo di dischi enclosure EBOD (Extended) in enclosure principale toohello di addizione. Uno chassis EBOD contiene controller EBOD e unità HDD protetti mediante spazi con mirroring. Uso di spazi con mirroring assicura che il dispositivo hello è errore hello tootolerate in grado di uno o più dischi rigidi. Hello enclosure EBOD è connesso toohello enclosure principale mediante cavi SAS ridondanti.

* Assicurarsi che entrambi i moduli controller dell'enclosure EBOD, entrambi i cavi SAS e tutte le unità disco rigido hello vengono installati in qualsiasi momento.
* In caso di guasto di un modulo controller dell'enclosure EBOD, richiedere immediatamente una sostituzione.
* Se un modulo controller dell'enclosure EBOD non riesce, verificare che tale hello altro modulo controller è attivo prima di sostituire il modulo non riuscito di hello. tooverify che un controller è attivo, andare troppo[controller attivo hello di identificazione sul dispositivo](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device).
* Durante una sostituzione dei moduli controller EBOD, monitorare costantemente lo stato di hello del componente hello nel servizio StorSimple Manager hello accedendo **manutenzione** > **stato Hardware**.
* Se un cavo SAS non riesce o richiede la sostituzione (supporto di Microsoft deve essere coinvolti toomake determinare), assicurarsi di rimuovere solo i cavi SAS hello che richiede la sostituzione.
* Non simultaneamente rimuovere entrambi i cavi SAS dal sistema hello in qualsiasi punto nel tempo.

### <a name="high-availability-recommendations-for-your-host-computers"></a>Indicazioni sulla disponibilità elevata per i computer host
Leggere attentamente queste procedure consigliate tooensure hello un'elevata disponibilità host connesso tooyour StorSimple dispositivo.

* Configurare StorSimple con [configurazioni cluster di file server a due nodi][1]. Rimuovendo i singoli punti di errore e si crea ridondanza sul lato host hello, hello intera soluzione diventa altamente disponibile.
* Utilizzare condivisioni sempre disponibili (CA) disponibile con Windows Server 2012 (SMB 3.0) per la disponibilità elevata durante il failover dei controller di archiviazione hello. Per ulteriori informazioni sulla configurazione di cluster di file server e condivisioni sempre disponibili con Windows Server 2012, vedere toothis [video dimostrativo](http://channel9.msdn.com/Events/IT-Camps/IT-Camps-On-Demand-Windows-Server-2012/DEMO-Continuously-Available-File-Shares).

## <a name="next-steps"></a>Passaggi successivi
* [Ulteriori informazioni sui Limiti di StorSimple](storsimple-limits.md).
* [Informazioni su come toodeploy la soluzione StorSimple](storsimple-deployment-walkthrough-u2.md).

<!--Reference links-->
[1]: https://technet.microsoft.com/library/cc731844(v=WS.10).aspx
