---
title: configurazione del dispositivo StorSimple hello aaaModify | Documenti Microsoft
description: "Viene descritto come toouse hello tooreconfigure servizio StorSimple Manager è già stato distribuito un dispositivo StorSimple."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: bb679264-8d46-429c-9ef7-630dc3b4a423
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: v-sharos
ms.openlocfilehash: 10a54c191260bf1baba58d28cdbfa0ed72217f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomodify-your-storsimple-device-configuration"></a>Utilizzare toomodify servizio StorSimple Manager di hello la configurazione del dispositivo StorSimple
## <a name="overview"></a>Panoramica
portale di Azure classico Hello **configura** pagina contiene tutti i parametri di dispositivo hello che è possibile riconfigurare in un dispositivo StorSimple è gestito da un servizio StorSimple Manager. In questa esercitazione viene illustrato come utilizzare hello **configura** hello tooperform pagina attività a livello di dispositivo seguenti:

* Modificare le impostazioni del dispositivo 
* Modificare le impostazioni di tempo 
* Modificare le impostazioni DNS 
* Modificare le interfacce di rete
* Sostituire o riassegnare indirizzi IP

## <a name="modify-device-settings"></a>Modificare le impostazioni del dispositivo
le impostazioni del dispositivo Hello includono nome descrittivo di hello del dispositivo hello e una descrizione di dispositivo hello.

> [!NOTE] 
> È possibile modificare il nome dispositivo hello in hello portale di Azure classico. Dispositivo hello ridenominazione non è supportata.

Un dispositivo StorSimple toohello connesso servizio StorSimple Manager è assegnato un nome predefinito. Hello normalmente riflette il numero di serie hello del dispositivo hello. Ad esempio, un nome di dispositivo predefinito di 15 caratteri, ad esempio 8600-SHX0991003G44HT, indica seguente hello:

* **8600** : indica un modello di dispositivo hello.
* **SHX** : sito di produzione indica hello.
* **0991003** -indica un prodotto specifico.
* **G44HT**: hello ultimi 5 cifre sono numeri di serie univoco toocreate incrementato. Questo potrebbe non essere un insieme sequenziale.

È possibile specificare una descrizione del dispositivo. In genere una descrizione del dispositivo consente di identificare il proprietario di hello e posizione fisica di hello del dispositivo hello. campo Descrizione Hello deve contenere meno di 256 caratteri.

## <a name="modify-time-settings"></a>Modificare le impostazioni di tempo
Il dispositivo deve sincronizzare l'ora in ordine tooauthenticate con provider di servizi di archiviazione cloud. Selezionare il fuso orario dall'elenco a discesa hello e specificare i server di tootwo protocollo NTP (Network Time). server NTP primario Hello è obbligatorio e viene specificato quando si utilizza Windows PowerShell per StorSimple tooconfigure, il dispositivo. È possibile specificare il Server di Windows predefinito di hello **time.windows.com** come server NTP. È possibile visualizzare hello primario configurazione del server NTP tramite hello portale di Azure classico, ma è necessario utilizzare toochange di interfaccia di Windows PowerShell hello è.

configurazione del server NTP secondario Hello è facoltativo. È possibile utilizzare tooconfigure portale classico hello un server NTP secondario. 

Quando si configura il server NTP hello, verificare che la rete consenta hello NTP traffico toopass dal toohello datacenter Internet. Quando si specifica un server NTP pubblico, è necessario assicurarsi che i firewall di rete e altri dispositivi di sicurezza siano configurati tooallow NTP traffico tootravel tooand da hello all'esterno di rete. Se non è consentito il traffico NTP bidirezionale, è necessario utilizzare un server NTP interno (un controller di dominio di Windows fornisce questa funzione). Se il dispositivo non è possibile sincronizzare l'ora, potrebbe non essere in grado di toocommunicate con il provider di archiviazione cloud.

un elenco dei server NTP pubblico, andare toohello toosee [Web server NTP](http://support.ntp.org/bin/view/Servers/WebHome). 

### <a name="what-happens-if-hello-device-is-deployed-in-a-different-time-zone"></a>Cosa accade se il dispositivo di hello viene distribuito in un fuso orario diverso?
Se il dispositivo hello viene distribuito in un fuso orario diverso, verrà modificato hello fuso orario del dispositivo. Dato che tutti i criteri di backup hello utilizzano hello fuso orario del dispositivo, i criteri di backup hello verranno regolato automaticamente in base al nuovo fuso orario di hello. Non è necessario alcun intervento dell'utente.

## <a name="modify-dns-settings"></a>Modificare le impostazioni DNS
Un server DNS viene utilizzato quando il dispositivo tenta toocommunicate con provider di servizi di archiviazione cloud. Per la disponibilità elevata, è necessario tooconfigure entrambi hello primario ed hello server DNS secondari durante la distribuzione iniziale del dispositivo hello. tooreconfigure hello server DNS primario, sarà necessario interfaccia di Windows PowerShell hello toouse nel dispositivo StorSimple.

toomodify hello server DNS secondario, è possibile utilizzare hello portale di Azure classico.

## <a name="modify-network-interfaces"></a>Modificare le interfacce di rete
Il dispositivo dispone di sei interfacce di rete del dispositivo, di cui quattro sono da 1 GbE e due sono da 10 GbE. Queste interfacce sono contrassegnate come DATA 0 - DATA 5. DATA 0, DATA 1, DATA 4 e DATA 5 sono da 1 GbE, mentre DATA 2 e DATA 3 sono interfacce di rete da 10 GbE.

Configurare **impostazioni interfaccia di rete** per ognuna delle hello interfacce toobe utilizzato. tooensure la disponibilità elevata, si consiglia di disporre di almeno due interfacce iSCSI e due interfacce abilitata per il cloud nel dispositivo. È consigliabile, ma non richiesta, la disabilitazione di interfacce inutilizzate.

Quando si configura una delle interfacce di rete hello, è necessario configurare un IP virtuale (VIP).

DATA 0 è abilitata per il cloud per impostazione predefinita. Quando si configura DATA 0, vengono anche tooconfigure necessari due indirizzi IP fissi, uno per ogni controller. Questi indirizzi IP fissi può essere direttamente di controller del dispositivo hello tooaccess usato e sono utili quando si installano aggiornamenti nel dispositivo hello o quando si accede controller hello a scopo di hello di risoluzione dei problemi.

StorSimple 8000 Series Update 1, metrica di routing hello di DATA 0 è impostato toohello più basso; Pertanto, se il dispositivo è in esecuzione StorSimple 8000 Series Update 1, tutto il traffico hello cloud verrà indirizzato tramite DATA 0. Tenere presente questo criterio se sono presenti più interfacce di rete abilitate per il cloud nel dispositivo StorSimple.

> [!NOTE]
> Hello indirizzi IP per il controller hello fissi vengono usati per gestire dispositivi toohello gli aggiornamenti di hello. Pertanto, hello indirizzi IP fissato deve essere instradabile e in grado di tooconnect toohello Internet.
> 
> 

Per ogni interfaccia di rete, viene visualizzato hello seguenti parametri:

* **Velocità** : non è un parametro configurabile dall'utente. DATA 0, DATA 1, DATA 4 e DATA 5 sono sempre da 1 GbE, mentre DATA 2 e DATA 3 sono interfacce di rete da 10 GbE.
  
  > [!NOTE]
  > Velocità e duplex sono sempre sottoposti alla negoziazione automatica. Non sono supportati i frame Jumbo.
  > 
  > 
* **Stato interfaccia** – un'interfaccia può essere abilitata o disabilitata. Se abilitata, il dispositivo hello tenterà interfaccia hello toouse. È consigliabile che solo le interfacce di rete connessa toohello e usati sia attivato. Disabilitare tutte le interfacce che non sono in uso.
* **Tipo di interfaccia** : questo parametro consente tooisolate il traffico iSCSI dal traffico di archiviazione cloud. Questo parametro può essere uno dei seguenti hello:
  
  * **Abilitato per il cloud** – se abilitata, il dispositivo di hello verrà utilizzato toocommunicate questa interfaccia con cloud hello.
  * **abilitato per iSCSI** – se abilitata, il dispositivo di hello verrà utilizzato toocommunicate questa interfaccia con host iSCSI hello.
    
    Si consiglia di isolare il traffico iSCSI dal traffico di archiviazione cloud. Si noti inoltre che se l'host è all'interno di hello stessa subnet del dispositivo, non è necessario tooassign un gateway. Tuttavia, se l'host si trova in una subnet diversa rispetto a un dispositivo, è necessario un gateway tooassign.
* **Indirizzo IP** : può trattarsi di IPv4 o IPv6 o entrambi. Hello IPv4 sia le famiglie di indirizzi IPv6 sono supportate per le interfacce di rete dispositivo hello. Quando si utilizza IPv4, specificare un indirizzo IP a 32 bit (*xxx.xxx.xxx.xxx*) in notazione decimale. Quando si utilizza IPv6, è sufficiente fornire un prefisso a 4 cifre e un indirizzo a 128 bit verrà generato automaticamente per l'interfaccia di rete del dispositivo in base al prefisso.
* **Subnet** – questo fa riferimento toohello la subnet mask e viene configurato tramite l'interfaccia di Windows PowerShell hello.
* **Gateway** – questo è il gateway predefinito hello che deve essere utilizzato da questa interfaccia durante il tentativo di toocommunicate con nodi che non rientrano hello stesso spazio di indirizzi IP (subnet). Hello gateway predefinito deve essere in hello stesso spazio indirizzi (subnet) come indirizzo IP dell'interfaccia hello, come determinato dalla subnet mask di hello.
* **Indirizzo IP fisso** : questo campo è disponibile solo quando si configura hello DATA 0 interfaccia. Per le operazioni, ad esempio gli aggiornamenti o dispositivo hello sulla risoluzione dei problemi, potrebbe essere necessario tooconnect direttamente toohello controller del dispositivo. Hello indirizzo IP fissato può essere utilizzato tooaccess hello attivo sia controller passivo hello del dispositivo.

È possibile riconfigurare Controller 0 e Controller 1 tramite hello portale di Azure classico.

> [!NOTE]
> * tooensure il corretto funzionamento, verificare la velocità di interfaccia hello e duplex nel commutatore hello che ogni interfaccia del dispositivo è connesso a. Le interfacce del commutatore devono essere negoziate oppure configurate per Gigabit Ethernet (1000 Mbps) e devono essere full duplex. Le interfacce funzionanti a velocità più basse o half duplex comportano problemi di prestazioni.
> * toominimize interruzioni e tempi di inattività, si consiglia di abilitare portfast su ogni opzione hello verranno connesso a porte hello interfaccia di rete iSCSI del dispositivo. Ciò garantisce che la connettività di rete può essere stabilita rapidamente in caso di hello di un failover.
> 
> 

## <a name="swap-or-reassign-ips"></a>Sostituire o riassegnare indirizzi IP
Attualmente, se un'interfaccia di rete sul controller hello viene assegnato un indirizzo VIP già in uso (da hello stesso dispositivo o un altro dispositivo in rete hello), quindi controller hello verrà eseguito il failover. Pertanto, è necessario procedura corretta di hello toofollow se si preveda di scambiare gli indirizzi VIP per interfaccia di rete del dispositivo hello, poiché si creerà una situazione IP duplicata.

Eseguire i seguenti passaggi tooswap hello o riassegnare gli indirizzi VIP hello per le interfacce di rete hello:

#### <a name="tooreassign-ips"></a>tooreassign gli indirizzi IP
1. Indirizzo IP non crittografato hello per entrambe le interfacce.
2. Dopo gli indirizzi IP hello siano deselezionati, assegnare nuovi indirizzi IP di hello toohello rispettive interfacce.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[configurare MPIO per il dispositivo StorSimple](storsimple-configure-mpio-windows-server.md).
* Informazioni su come troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

