---
title: configurazione del dispositivo serie StorSimple 8000 hello aaaModify | Documenti Microsoft
description: "Viene descritto come toouse hello tooreconfigure servizio di gestione di dispositivi StorSimple un dispositivo StorSimple che è già stato distribuito."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 79711b45eafe732c1eed1e562b05e3837fbc9d03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomodify-your-storsimple-device-configuration"></a>Utilizzare toomodify servizio di gestione di dispositivi StorSimple hello la configurazione del dispositivo StorSimple

## <a name="overview"></a>Panoramica

portale di Azure Hello **le impostazioni del dispositivo** sezione hello **impostazioni** pannello contiene tutti i parametri di dispositivo hello che è possibile riconfigurare in un dispositivo StorSimple è gestito da un gestore di dispositivo StorSimple servizio. In questa esercitazione viene illustrato come utilizzare hello **impostazioni** hello tooperform pannello seguenti attività a livello di dispositivo:

* Modificare il nome descrittivo del dispositivo
* Modificare le impostazioni ora del dispositivo
* Assegnare un DNS secondario
* Modificare le interfacce di rete
* Sostituire o riassegnare indirizzi IP

## <a name="modify-device-friendly-name"></a>Modificare il nome descrittivo del dispositivo

È possibile utilizzare nome del dispositivo hello hello toochange portale Azure e assegnargli un nome descrittivo univoco desiderato. Hello utilizzare **impostazioni generali** pannello nel dispositivo toomodify hello descrittivo il nome del dispositivo. nome descrittivo Hello può contenere i caratteri e può contenere un massimo di 64 caratteri.

> [!NOTE] 
> È possibile modificare solo nome di dispositivo hello nel portale di Azure hello prima del completamento dell'installazione di dispositivi hello. Al termine dell'installazione minima del dispositivo hello, è possibile modificare il nome di dispositivo hello.

![Nome del dispositivo nelle impostazioni generali](./media/storsimple-8000-modify-device-config/modify-general-settings3.png)

Un dispositivo StorSimple toohello connesso il servizio di gestione di dispositivi StorSimple viene assegnato un nome predefinito. Hello normalmente riflette il numero di serie hello del dispositivo hello. Ad esempio, un nome di dispositivo predefinito di 15 caratteri, ad esempio 8600-SHX0991003G44HT, indica seguente hello:

* **8600** : indica un modello di dispositivo hello.
* **SHX** : sito di produzione indica hello.
* **0991003** -indica un prodotto specifico.
* **G44HT**: hello ultimi 5 cifre sono numeri di serie univoco toocreate incrementato. Questo potrebbe non essere un insieme sequenziale.

## <a name="modify-device-description"></a>Modificare la descrizione del dispositivo

Hello utilizzare **impostazioni generali** pannello nella descrizione del dispositivo del dispositivo toomodify hello.

![Descrizione del dispositivo nelle impostazioni generali](./media/storsimple-8000-modify-device-config/modify-general-settings4.png)

In genere una descrizione del dispositivo consente di identificare il proprietario di hello e posizione fisica di hello del dispositivo hello. campo Descrizione Hello deve contenere meno di 256 caratteri.

## <a name="modify-time-settings"></a>Modificare le impostazioni di tempo

Il dispositivo deve sincronizzare l'ora in ordine tooauthenticate con provider di servizi di archiviazione cloud. Hello utilizzare **impostazioni generali** pannello nel dispositivo toomodify hello ora le impostazioni del dispositivo.

![Descrizione del dispositivo nelle impostazioni generali](./media/storsimple-8000-modify-device-config/modify-general-settings2.png)

 Selezionare il fuso orario dall'elenco a discesa hello. È possibile specificare i server di protocollo NTP (Network Time) tootwo:

 - **Server NTP primario** -configurazione hello è obbligatorio e viene specificato quando si utilizza Windows PowerShell per StorSimple tooconfigure, il dispositivo. È possibile specificare il Server di Windows predefinito di hello **time.windows.com** come server NTP. È possibile visualizzare hello primario configurazione del server NTP tramite hello portale di Azure, ma è necessario utilizzare toochange di interfaccia di Windows PowerShell hello è. Hello utilizzare `Set-HcsNTPClientServerAddress` server NTP primario di cmdlet toomodify hello del dispositivo. Per ulteriori informazioni, visitare toosynxtax per cmdlet [Set-HcsNTPClientServerAddress] (https://technet.microsoft.com/library/dn688138.aspx).

- **Server NTP secondario** -configurazione hello è facoltativa. È possibile utilizzare hello portale tooconfigure un server NTP secondario.

Quando si configura il server NTP hello, verificare che la rete consenta hello NTP traffico toopass dal toohello datacenter Internet. Quando si specifica un server NTP pubblico, è necessario assicurarsi che i firewall di rete e altri dispositivi di sicurezza siano configurati tooallow NTP traffico tootravel tooand da hello all'esterno di rete. Se non è consentito il traffico NTP bidirezionale, è necessario utilizzare un server NTP interno (un controller di dominio di Windows fornisce questa funzione). Se il dispositivo non è possibile sincronizzare l'ora, potrebbe non essere in grado di toocommunicate con il provider di archiviazione cloud.

un elenco dei server NTP pubblico, andare toohello toosee [Web server NTP](http://support.ntp.org/bin/view/Servers/WebHome).

### <a name="what-happens-if-hello-device-is-deployed-in-a-different-time-zone"></a>Cosa accade se il dispositivo di hello viene distribuito in un fuso orario diverso?

Se il dispositivo hello viene distribuito in un fuso orario diverso, verrà modificato hello fuso orario del dispositivo. Dato che tutti i criteri di backup hello utilizzano hello fuso orario del dispositivo, i criteri di backup hello verranno regolato automaticamente in base al nuovo fuso orario di hello. Non è necessario alcun intervento dell'utente.

## <a name="modify-dns-settings"></a>Modificare le impostazioni DNS

Un server DNS viene utilizzato quando il dispositivo tenta toocommunicate con provider di servizi di archiviazione cloud. Hello utilizzare **le impostazioni di rete** pannello nel tooview dispositivo e modificare le impostazioni DNS hello configurato. 

![Impostazioni DNS nelle impostazioni di rete](./media/storsimple-8000-modify-device-config/modify-network-settings1.png)

Per la disponibilità elevata, è necessario tooconfigure entrambi hello primario ed hello server DNS secondari durante la distribuzione iniziale del dispositivo hello.

**Server DNS primario** -utilizzare hello Windows PowerShell per StorSimple toofirst specificare server DNS primario hello durante l'installazione iniziale di hello. È possibile riconfigurare i server DNS primario hello solo tramite l'interfaccia di Windows PowerShell di hello. Hello utilizzare `Set-HcsDNSClientServerAddress` cmdlet toomodify hello server DNS primario del dispositivo. Per ulteriori informazioni, consultare toosynxtax [Set-HcsDNSClientServerAddress](https://technet.microsoft.com/library/dn688138.aspx) cmdlet.

**Server DNS secondario** -toomodify hello server DNS secondario, utilizzare hello `Set-HcsDNSClientServerAddress` cmdlet nell'interfaccia di Windows PowerShell hello del dispositivo hello o **le impostazioni di rete** pannello del dispositivo StorSimple in hello Azure portale.

toomodify hello server DNS secondario nel portale di Azure, eseguire hello alla procedura seguente.

1. Passare il servizio di gestione di dispositivi StorSimple tooyour. Hello l'elenco di dispositivi, selezionare e fare clic sul dispositivo.

2. In hello **impostazioni** pannello andare troppo**le impostazioni del dispositivo > rete**. Verrà visualizzata hello **le impostazioni di rete** blade. Fare clic sul riquadro **Impostazioni DNS**. Modificare l'indirizzo IP server hello secondario DNS.

    ![Modificare l'indirizzo IP del server DNS secondario](./media/storsimple-8000-modify-device-config/modify-secondary-dns1.png)

4. Dalla barra dei comandi di hello, fare clic su **salvare** alla richiesta di conferma, fare clic su **OK**.

    ![Salvare e confermare le modifiche](./media/storsimple-8000-modify-device-config/modify-secondary-dns-2.png)



## <a name="modify-network-interfaces"></a>Modificare le interfacce di rete

Il dispositivo dispone di sei interfacce di rete del dispositivo, di cui quattro sono da 1 GbE e due sono da 10 GbE. Queste interfacce sono contrassegnate come DATA 0 - DATA 5. DATA 0, DATA 1, DATA 4 e DATA 5 sono da 1 GbE, mentre DATA 2 e DATA 3 sono interfacce di rete da 10 GbE.

Hello utilizzare **le impostazioni di rete** pannello tooconfigure ogni di hello interfacce toobe utilizzato.

![Configurare le interfacce di rete in Impostazioni di rete](./media/storsimple-8000-modify-device-config/modify-network-settings3.png)

tooensure la disponibilità elevata, si consiglia di disporre di almeno due interfacce iSCSI e due interfacce abilitata per il cloud nel dispositivo. È consigliabile, ma non richiesta, la disabilitazione di interfacce inutilizzate.

Per ogni interfaccia di rete, viene visualizzato hello seguenti parametri:

* **Velocità** : non è un parametro configurabile dall'utente. DATA 0, DATA 1, DATA 4 e DATA 5 sono sempre da 1 GbE, mentre DATA 2 e DATA 3 sono interfacce di rete da 10 GbE.
  
  > [!NOTE]
  > Velocità e duplex sono sempre sottoposti alla negoziazione automatica. Non sono supportati i frame Jumbo.
  
* **Stato interfaccia** – un'interfaccia può essere abilitata o disabilitata. Se abilitata, il dispositivo hello tenterà interfaccia hello toouse. È consigliabile che solo le interfacce di rete connessa toohello e usati sia attivato. Disabilitare tutte le interfacce che non sono in uso.
* **Tipo di interfaccia** : questo parametro consente tooisolate il traffico iSCSI dal traffico di archiviazione cloud. Questo parametro può essere uno dei seguenti hello:
  
  * **Abilitato per il cloud** – se abilitata, il dispositivo di hello verrà utilizzato toocommunicate questa interfaccia con cloud hello.
  * **abilitato per iSCSI** – se abilitata, il dispositivo di hello verrà utilizzato toocommunicate questa interfaccia con host iSCSI hello.
    
    Si consiglia di isolare il traffico iSCSI dal traffico di archiviazione cloud. Si noti inoltre che se l'host è all'interno di hello stessa subnet del dispositivo, non è necessario tooassign un gateway. Tuttavia, se l'host si trova in una subnet diversa rispetto a un dispositivo, è necessario un gateway tooassign.
* **Indirizzo IP** : quando si configura una delle interfacce di rete hello, è necessario configurare un IP virtuale (VIP). L'IP virtuale può essere IPv4 o IPv6 o entrambi. Hello IPv4 sia le famiglie di indirizzi IPv6 sono supportate per le interfacce di rete dispositivo hello. Quando si utilizza IPv4, specificare un indirizzo IP a 32 bit (*xxx.xxx.xxx.xxx*) in notazione decimale. Quando si utilizza IPv6, è sufficiente fornire un prefisso a 4 cifre e un indirizzo a 128 bit verrà generato automaticamente per l'interfaccia di rete del dispositivo in base al prefisso.
* **Subnet** – questo fa riferimento toohello la subnet mask e viene configurato tramite l'interfaccia di Windows PowerShell hello.
* **Gateway** – questo è il gateway predefinito hello che deve essere utilizzato da questa interfaccia durante il tentativo di toocommunicate con nodi che non rientrano hello stesso spazio di indirizzi IP (subnet). Hello gateway predefinito deve essere in hello stesso spazio indirizzi (subnet) come indirizzo IP dell'interfaccia hello, come determinato dalla subnet mask di hello.
* **Indirizzo IP fisso** : questo campo è disponibile solo quando si configura hello DATA 0 interfaccia. Per le operazioni, ad esempio gli aggiornamenti o dispositivo hello sulla risoluzione dei problemi, potrebbe essere necessario tooconnect direttamente toohello controller del dispositivo. Hello indirizzo IP fissato può essere utilizzato tooaccess hello attivo sia controller passivo hello del dispositivo.

> [!NOTE]
> * tooensure il corretto funzionamento, verificare la velocità di interfaccia hello e duplex nel commutatore hello che ogni interfaccia del dispositivo è connesso a. Le interfacce del commutatore devono essere negoziate oppure configurate per Gigabit Ethernet (1000 Mbps) e devono essere full duplex. Le interfacce funzionanti a velocità più basse o half duplex comportano problemi di prestazioni.
> * toominimize interruzioni e tempi di inattività, si consiglia di abilitare portfast su ogni opzione hello verranno connesso a porte hello interfaccia di rete iSCSI del dispositivo. Ciò garantisce che la connettività di rete può essere stabilita rapidamente in caso di hello di un failover.

### <a name="configure-data-0"></a>Configurare DATA 0

DATA 0 è abilitata per il cloud per impostazione predefinita. Quando si configura DATA 0, vengono anche tooconfigure necessari due indirizzi IP fissi, uno per ogni controller. Questi indirizzi IP fissi può essere direttamente di controller del dispositivo hello tooaccess usato e sono utili quando si installano aggiornamenti nel dispositivo hello o quando si accede controller hello a scopo di hello di risoluzione dei problemi.

È possibile riconfigurare hello fissato controller IP tramite Pannello impostazioni 0 dei dati hello.

![Configurare l'interfaccia di rete - DATA 0](./media/storsimple-8000-modify-device-config/modify-network-settings2.png)

> [!NOTE]
> Hello indirizzi IP per il controller hello fissi vengono usati per gestire dispositivi toohello gli aggiornamenti di hello. Pertanto, hello indirizzi IP fissato deve essere instradabile e in grado di tooconnect toohello Internet.

### <a name="configure-data-1---data-5"></a>Configurare DATA 1 - DATA 5

Per i dati di 1 - interfacce di rete 5 di dati, è possibile configurare tutte le impostazioni di rete hello come illustrato nella seguente schermata hello:

![Configurare le interfacce di rete DATA 1 - DATA 5](./media/storsimple-8000-modify-device-config/modify-network-settings4.png)


## <a name="swap-or-reassign-ips"></a>Sostituire o riassegnare indirizzi IP

Attualmente, se un'interfaccia di rete sul controller hello viene assegnato un indirizzo VIP già in uso (da hello stesso dispositivo o un altro dispositivo in rete hello), quindi controller hello verrà eseguito il failover. Se si scambiano o si riassegnano i VIP per un'interfaccia di rete del dispositivo, è necessario seguire una procedura appropriata poiché si potrebbe creare una situazione con IP duplicati.

Eseguire i seguenti passaggi tooswap hello o riassegnare gli indirizzi VIP hello per le interfacce di rete hello:

#### <a name="tooreassign-ips"></a>tooreassign gli indirizzi IP

1. Indirizzo IP non crittografato hello per entrambe le interfacce.
2. Dopo gli indirizzi IP hello siano deselezionati, assegnare nuovi indirizzi IP di hello toohello rispettive interfacce.

## <a name="next-steps"></a>Passaggi successivi

* Informazioni su come troppo[configurare MPIO per il dispositivo StorSimple](storsimple-8000-configure-mpio-windows-server.md).
* Informazioni su come troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

