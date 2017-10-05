---
title: Modificare la configurazione del dispositivo StorSimple | Microsoft Docs
description: "Viene descritto come utilizzare il servizio StorSimple Manager per riconfigurare un dispositivo StorSimple che è già stato distribuito."
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
ms.openlocfilehash: 5bfbeb038dbedae2bf77016abbc19458c3dc22c9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-manager-service-to-modify-your-storsimple-device-configuration"></a>Utilizzare il servizio StorSimple Manager per modificare la configurazione del dispositivo StorSimple
## <a name="overview"></a>Panoramica
La pagina **Configura** del portale di Azure classico contiene tutti i parametri del dispositivo che è possibile riconfigurare in un dispositivo StorSimple gestito da un servizio StorSimple Manager. In questa esercitazione viene illustrato come utilizzare la pagina **Configura** per eseguire le seguenti attività a livello di dispositivo:

* Modificare le impostazioni del dispositivo 
* Modificare le impostazioni di tempo 
* Modificare le impostazioni DNS 
* Modificare le interfacce di rete
* Sostituire o riassegnare indirizzi IP

## <a name="modify-device-settings"></a>Modificare le impostazioni del dispositivo
Le impostazioni del dispositivo includono il nome descrittivo del dispositivo e la descrizione del dispositivo.

> [!NOTE] 
> Non è possibile modificare il nome del dispositivo nel portale di Azure classico. La ridenominazione del dispositivo non è supportata.

Ad un dispositivo StorSimple connesso al servizio StorSimple Manager viene assegnato un nome predefinito. Il nome predefinito riflette in genere il numero di serie del dispositivo. Ad esempio, un nome di dispositivo predefinito che è composto da 15 caratteri, ad esempio 8600-SHX0991003G44HT indica quanto segue:

* **8600** – indica il modello del dispositivo.
* **SHX** – indica il sito di produzione.
* **0991003** -indica un prodotto specifico.
* **G44HT**-le ultime 5 cifre vengono aggiunte per creare numeri di serie univoci. Questo potrebbe non essere un insieme sequenziale.

È possibile specificare una descrizione del dispositivo. Una descrizione del dispositivo in genere consente di identificare il proprietario e il percorso fisico del dispositivo. Il campo descrizione deve contenere meno di 256 caratteri.

## <a name="modify-time-settings"></a>Modificare le impostazioni di tempo
Il dispositivo deve sincronizzare l'ora per l'autenticazione con il provider di servizi di archiviazione cloud. Selezionare il fuso orario dall'elenco a discesa e specificare fino a due server di protocollo NTP (Network Time). Il server NTP primario è obbligatorio e viene specificato quando si utilizza Windows PowerShell per StorSimple per configurare il dispositivo. È possibile specificare il valore predefinito di Windows Server **time.windows.com** come server NTP. È possibile visualizzare la configurazione del server NTP primario tramite il portale di Azure classico, ma è necessario utilizzare l'interfaccia Windows PowerShell per modificarlo.

La configurazione del server NTP secondario è facoltativa. È possibile utilizzare il portale classico per configurare un server NTP secondario. 

Quando si configura il server NTP, assicurarsi che la rete consenta il traffico NTP dal Data Center a Internet. Quando si specifica un server NTP pubblico, è necessario assicurarsi che i firewall di rete e altri dispositivi di sicurezza siano configurati per consentire il traffico NTP da e verso la rete esterna. Se non è consentito il traffico NTP bidirezionale, è necessario utilizzare un server NTP interno (un controller di dominio di Windows fornisce questa funzione). Se il dispositivo non può sincronizzare l'ora, potrebbe non essere in grado di comunicare con il provider di archiviazione cloud.

Per visualizzare un elenco dei server NTP pubblico, visitare il [Web server NTP](http://support.ntp.org/bin/view/Servers/WebHome). 

### <a name="what-happens-if-the-device-is-deployed-in-a-different-time-zone"></a>Cosa accade se il dispositivo viene distribuito in un fuso orario diverso?
Se il dispositivo viene distribuito in un fuso orario diverso, cambia il fuso orario del dispositivo. Dato che tutti i criteri di backup utilizzano il fuso orario del dispositivo, i criteri di backup verranno regolati automaticamente secondo il nuovo fuso orario. Non è necessario alcun intervento dell'utente.

## <a name="modify-dns-settings"></a>Modificare le impostazioni DNS
Un server DNS viene utilizzato quando il dispositivo tenta di comunicare con il provider di servizi di archiviazione cloud. Per la disponibilità elevata, è necessario configurare il database primario e i server DNS secondari durante la distribuzione iniziale del dispositivo. Per riconfigurare il server DNS primario, occorre utilizzare l'interfaccia Windows PowerShell del dispositivo StorSimple.

Per modificare il server DNS secondario, è possibile utilizzare il portale di Azure classico.

## <a name="modify-network-interfaces"></a>Modificare le interfacce di rete
Il dispositivo dispone di sei interfacce di rete del dispositivo, di cui quattro sono da 1 GbE e due sono da 10 GbE. Queste interfacce sono contrassegnate come DATA 0 - DATA 5. DATA 0, DATA 1, DATA 4 e DATA 5 sono da 1 GbE, mentre DATA 2 e DATA 3 sono interfacce di rete da 10 GbE.

Configurare **Impostazioni interfaccia di rete** per ciascuna delle interfacce da utilizzare. Per garantire la disponibilità elevata, si consiglia di disporre di almeno due interfacce di iSCSI e due interfacce abilitate per cloud sul dispositivo. È consigliabile, ma non richiesta, la disabilitazione di interfacce inutilizzate.

Quando si configura una delle interfacce di rete, è necessario configurare un IP virtuale (VIP).

DATA 0 è abilitata per il cloud per impostazione predefinita. Durante la configurazione di DATA 0, è inoltre necessario configurare due indirizzi IP fissi, uno per ogni controller. Questi indirizzi IP fissi possono essere utilizzati per accedere direttamente ai controller dei dispositivi e sono utili quando si installano gli aggiornamenti del dispositivo o quando si accede ai controller per la risoluzione dei problemi.

In StorSimple 8000 serie Update 1 la metrica di routing di DATA 0 è impostata al valore più basso; Pertanto, se il dispositivo sta eseguendo StorSimple 8000 serie Update 1, tutto il traffico cloud verrà indirizzato tramite DATA 0. Tenere presente questo criterio se sono presenti più interfacce di rete abilitate per il cloud nel dispositivo StorSimple.

> [!NOTE]
> Gli indirizzi IP fissi per il controller vengono utilizzati per gestire gli aggiornamenti al dispositivo. Di conseguenza, gli indirizzi IP fissi devono essere instradabili e in grado di connettersi a Internet.
> 
> 

Per ogni interfaccia di rete, vengono visualizzati i seguenti parametri:

* **Velocità** : non è un parametro configurabile dall'utente. DATA 0, DATA 1, DATA 4 e DATA 5 sono sempre da 1 GbE, mentre DATA 2 e DATA 3 sono interfacce di rete da 10 GbE.
  
  > [!NOTE]
  > Velocità e duplex sono sempre sottoposti alla negoziazione automatica. Non sono supportati i frame Jumbo.
  > 
  > 
* **Stato interfaccia** – un'interfaccia può essere abilitata o disabilitata. Se abilitata, il dispositivo tenterà di utilizzare l'interfaccia. Si consiglia di abilitare solo tali interfacce che sono connesse alla rete e utilizzati. Disabilitare tutte le interfacce che non sono in uso.
* **Tipo di interfaccia** : questo parametro consente di isolare il traffico iSCSI dal traffico di archiviazione cloud. Questo parametro può essere uno dei seguenti:
  
  * **Abilitato per il cloud** – quando abilitato, il dispositivo utilizzerà questa interfaccia per comunicare con il cloud.
  * **iSCSI abilitato** – quando abilitato, il dispositivo utilizzerà questa interfaccia per comunicare con l'host iSCSI.
    
    Si consiglia di isolare il traffico iSCSI dal traffico di archiviazione cloud. Si noti inoltre che se l'host è all'interno della stessa subnet del dispositivo, non è necessario assegnare un gateway. Tuttavia, se l'host si trova in una subnet diversa del dispositivo, è necessario assegnare un gateway.
* **Indirizzo IP** : può trattarsi di IPv4 o IPv6 o entrambi. Sono supportate sia le famiglie di indirizzi IPv4 e sia IPv6 per le interfacce di rete del dispositivo. Quando si utilizza IPv4, specificare un indirizzo IP a 32 bit (*xxx.xxx.xxx.xxx*) in notazione decimale. Quando si utilizza IPv6, è sufficiente fornire un prefisso a 4 cifre e un indirizzo a 128 bit verrà generato automaticamente per l'interfaccia di rete del dispositivo in base al prefisso.
* **Subnet** : si riferisce alla subnet mask e viene configurata tramite l'interfaccia Windows PowerShell.
* **Gateway** : si tratta del gateway predefinito che deve essere utilizzato da tale interfaccia durante il tentativo di comunicare con i nodi che non sono nello stesso spazio di indirizzi IP (subnet). Il gateway predefinito deve essere nello stesso spazio degli indirizzi (subnet) dell'interfaccia indirizzo IP, come determinato dalla subnet mask.
* **Indirizzo IP fisso** : questo campo è disponibile solo quando si configura l’interfaccia di DATA 0. Per operazioni come aggiornamenti o risoluzione dei problemi relativi al dispositivo, potrebbe essere necessario connettersi direttamente al controller del dispositivo. L'indirizzo IP fisso può essere utilizzato per accedere al controller attivo e passivo sul dispositivo.

È possibile riconfigurare il Controller 0 e il Controller 1 tramite il portale di Azure classico.

> [!NOTE]
> * Per garantire il corretto funzionamento, verificare la velocità dell'interfaccia e duplex del commutatore a cui ogni interfaccia del dispositivo è connessa. Le interfacce del commutatore devono essere negoziate oppure configurate per Gigabit Ethernet (1000 Mbps) e devono essere full duplex. Le interfacce funzionanti a velocità più basse o half duplex comportano problemi di prestazioni.
> * Per ridurre al minimo le interruzioni e tempi di inattività, è consigliabile abilitare portfast su ciascuna delle porte del commutatore a cui l'interfaccia di rete iSCSI del dispositivo sarà connessa. Ciò garantisce che la connettività di rete può essere stabilita rapidamente in caso di failover.
> 
> 

## <a name="swap-or-reassign-ips"></a>Sostituire o riassegnare indirizzi IP
Attualmente, se a qualsiasi interfaccia di rete nel controller viene assegnato un VIP è in uso (per lo stesso dispositivo o un altro dispositivo di rete), il controller avrà esito negativo. Pertanto, è necessario attenersi alla procedura appropriata se si scambiano indirizzi IP virtuali per l'interfaccia di rete del dispositivo, poiché si creerà una situazione di IP duplicata.

Per sostituire o riassegnare i VIP per qualsiasi interfaccia di rete, procedere come segue:

#### <a name="to-reassign-ips"></a>Per riassegnare indirizzi IP
1. Deselezionare l'indirizzo IP per entrambe le interfacce.
2. Dopo che gli indirizzi IP sono deselezionati, assegnare nuovi indirizzi IP alle rispettive interfacce.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come [Configurare MPIO per il dispositivo StorSimple](storsimple-configure-mpio-windows-server.md).
* Informazioni su come [utilizzare il servizio StorSimple Manager per amministrare il dispositivo StorSimple](storsimple-manager-service-administration.md).

