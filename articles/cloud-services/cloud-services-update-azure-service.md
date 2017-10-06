---
title: aaaHow tooupdate un servizio cloud | Documenti Microsoft
description: "Informazioni su come dei servizi cloud tooupdate in Azure. Informazioni su modalità di prosecuzione tooensure disponibilità di un aggiornamento in un servizio cloud."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c6a8b5e6-5c99-454c-9911-5c7ae8d1af63
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 7e4c8bd46e51a555b4309ea8927d120e8efcf0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-a-cloud-service"></a>Come tooupdate un servizio cloud

L'aggiornamento di un servizio cloud, inclusi i ruoli e il sistema operativo guest, è un processo in tre passaggi. Innanzitutto, i file binari hello e file di configurazione per hello nuovo servizio cloud o versione del sistema operativo deve essere caricato. Successivamente, Azure riserva risorse di calcolo e rete per il servizio cloud hello in base ai requisiti di hello della nuova versione del servizio cloud hello. Infine, Azure esegue una sequenza tooincrementally aggiornamento hello tenant toohello nuova versione di aggiornamento o guest del sistema operativo, mantenendo la disponibilità. Questo articolo illustra i dettagli di hello di quest'ultimo passaggio: hello aggiornamento in sequenza.

## <a name="update-an-azure-service"></a>Aggiornare un servizio di Azure
Azure organizza le istanze del ruolo in raggruppamenti logici chiamati domini di aggiornamento. I domini di aggiornamento sono set logici di istanze del ruolo aggiornate come gruppo.  Gli aggiornamenti di Azure a cloud service uno UD alla volta, consentendo agli altri toocontinue UD del traffico di istanze.

numero di domini di aggiornamento predefinito Hello è 5. È possibile specificare un numero diverso di domini di aggiornamento includendo l'attributo upgradeDomainCount hello nel file di definizione del servizio hello (con estensione csdef). Per ulteriori informazioni sull'attributo upgradeDomainCount hello, vedere [WebRole Schema](https://msdn.microsoft.com/library/azure/gg557553.aspx) o [WorkerRole Schema](https://msdn.microsoft.com/library/azure/gg557552.aspx).

Quando si esegue un aggiornamento sul posto di uno o più ruoli nel servizio, Azure Aggiorna set di istanze del ruolo in base toowhich di dominio di aggiornamento toohello che appartengono. Dominio successivo hello passa quindi tutte le istanze di hello in un dato dominio di aggiornamento arrestarli, aggiornarle, riportarle eseguire il backup, gli aggiornamenti di Azure. Arrestando solo le istanze di hello in esecuzione in hello corrente di dominio di aggiornamento, Azure garantisce che si verifica un aggiornamento con hello minimo impatto toohello in esecuzione del servizio. Per ulteriori informazioni, vedere [come continuazione dell'aggiornamento hello](#howanupgradeproceeds) più avanti in questo articolo.

> [!NOTE]
> Mentre i termini di hello **aggiornare** e **aggiornamento** assumere significati leggermente diversi nel contesto di hello Azure, possono essere utilizzate indifferentemente per i processi di hello e le descrizioni delle funzionalità di hello in questo documento.
>
>

Il servizio è necessario definire almeno due istanze di un ruolo per tale ruolo toobe aggiornati sul posto senza tempo di inattività. Se il servizio di hello costituito dal solo un'istanza di un ruolo, il servizio sarà disponibile finché non hello aggiornamento sul posto è terminata.

In questo argomento vengono illustrate le seguenti informazioni sugli aggiornamenti Azure hello:

* [Modifiche consentite al servizio durante un aggiornamento](#AllowedChanges)
* [Come avviene un aggiornamento](#howanupgradeproceeds)
* [Ripristino dello stato precedente di un aggiornamento](#RollbackofanUpdate)
* [Avvio di più operazioni di mutazione durante una distribuzione](#multiplemutatingoperations)
* [Distribuzione di ruoli nei domini di aggiornamento](#distributiondfroles)

<a name="AllowedChanges"></a>

## <a name="allowed-service-changes-during-an-update"></a>Modifiche consentite al servizio durante un aggiornamento
Hello nella tabella seguente viene illustrato come hello consentita modifiche servizio tooa durante un aggiornamento:

| Modifiche consentite toohosting, servizi e ruoli | Aggiornamento sul posto | Gestione temporanea (scambio indirizzi VIP) | Eliminazione e ridistribuzione |
| --- | --- | --- | --- |
| Versione del sistema operativo |Sì |Sì |Sì |
| Livello di attendibilità .NET |Sì |Sì |Sì |
| Dimensioni macchina virtuale<sup>1</sup> |Sì<sup>2</sup> |Sì |Sì |
| Impostazioni di archiviazione locali |Solo aumento<sup>2</sup> |Sì |Sì |
| Aggiungere o rimuovere ruoli in un servizio |Sì |Sì |Sì |
| Numero di istanze di un particolare ruolo |Sì |Sì |Sì |
| Numero o tipo di endpoint per un servizio |Sì<sup>2</sup> |No |Sì |
| Nomi e i valori delle impostazioni di configurazione |Sì |Sì |Sì |
| Valori (ma non nomi) delle impostazioni di configurazione |Sì |Sì |Sì |
| Aggiungere nuovi certificati |Sì |Sì |Sì |
| Modificare i certificati esistenti |Sì |Sì |Sì |
| Distribuire nuovo codice |Sì |Sì |Sì |

<sup>1</sup> modifica delle dimensioni limitate toohello subset di dimensioni disponibili per il servizio cloud hello.

<sup>2</sup> Richiede Azure SDK 1.5 o versioni successive.

> [!WARNING]
> Modifica delle dimensioni della macchina virtuale hello comporta l'eliminazione di dati locali.
>
>

Hello seguenti non è supportato durante un aggiornamento:

* Modifica nome hello di un ruolo. Rimuovere e quindi aggiungere il ruolo di hello con nuovo nome hello.
* Modifica di hello conteggio di aggiornamento del dominio.
* Riduzione delle dimensioni di hello delle risorse locali hello.

Se si eseguono altri aggiornamenti della definizione del servizio tooyour, ad esempio la diminuzione delle dimensioni di hello della risorsa locale, è necessario eseguire invece un aggiornamento di scambio VIP. Per altre informazioni, vedere [Scambiare la distribuzione](https://msdn.microsoft.com/library/azure/ee460814.aspx).

<a name="howanupgradeproceeds"></a>

## <a name="how-an-upgrade-proceeds"></a>Come avviene un aggiornamento
È possibile decidere se si desidera tooupdate tutti i ruoli di hello nel servizio o un singolo ruolo nel servizio hello. In entrambi i casi, tutte le istanze di ogni ruolo in corso l'aggiornamento e appartengono toohello primo dominio di aggiornamento sono arrestate, aggiornate e portate nuovamente online. Dopo aver riportato online, hello istanze nel secondo dominio di aggiornamento hello arrestate, aggiornate e portate online. Un servizio cloud non può avere più di un aggiornamento attivo per volta. aggiornamento di Hello viene sempre eseguita con la versione più recente di hello del servizio cloud hello.

Hello diagramma seguente illustra come avviare l'aggiornamento di hello se si esegue l'aggiornamento di tutti i ruoli di hello nel servizio hello:

![Servizio di aggiornamento](media/cloud-services-update-azure-service/IC345879.png "Servizio di aggiornamento")

Nel diagramma seguente viene illustrato come continuazione dell'aggiornamento hello se si sta aggiornando un solo ruolo:

![Aggiornamento ruolo](media/cloud-services-update-azure-service/IC345880.png "Aggiornamento ruolo")  

Durante un aggiornamento automatico, hello Controller di infrastruttura di Azure valuta periodicamente integrità hello di hello cloud servizio toodetermine quando è sicuro toowalk hello UD successivo. Questa valutazione dell'integrità viene eseguita in base al ruolo e vengono considerate solo le istanze nella versione più recente di hello (ad esempio le istanze da domini di aggiornamento che sono già stati esaminati). Verifica che un numero minimo di istanze del ruolo, per ogni ruolo, abbia raggiunto uno stato finale soddisfacente.

### <a name="role-instance-start-timeout"></a>Timeout dell'avvio dell’istanza del ruolo
Controller di infrastruttura Hello attende 30 minuti per ogni tooreach istanza ruolo stato avviato. Se scade la durata del timeout di hello, Controller di infrastruttura hello continuerà esame toohello successiva istanza del ruolo.

### <a name="impact-toodrive-data-during-cloud-service-upgrades"></a>Dati di impatto toodrive durante gli aggiornamenti del servizio Cloud

Durante l'aggiornamento di un servizio da istanze di toomultiple una singola istanza del servizio verrà ridotto durante l'aggiornamento di hello viene eseguita a causa di toohello modo che Azure consente di aggiornare i servizi. Hello servizio Contratto garantisce la disponibilità del servizio si applica solo tooservices distribuiti con più di un'istanza. Hello elenco seguente descrive come dati hello in ogni unità sono interessati da ogni scenario di aggiornamento del servizio di Azure:

|Scenario|Unità C|Unità D|Unità E|
|--------|-------|-------|-------|
|Riavvio VM|Mantenuta|Mantenuta|Mantenuta|
|Riavvio del portale|Mantenuta|Mantenuta|Eliminata|
|Ricreazione dell'immagine del portale|Mantenuta|Eliminata|Eliminata|
|Aggiornamento sul posto|Mantenuta|Mantenuta|Eliminata|
|Migrazione di un nodo|Eliminata|Eliminata|Eliminata|

Si noti che, in hello sopra l'elenco, hello unità e: rappresenta l'unità radice del ruolo hello e non deve essere hardcoded. Utilizzare invece hello **% RoleRoot %** unità hello toorepresent variabile di ambiente.

toominimize hello tempi di inattività durante l'aggiornamento di un servizio a istanza singola, distribuire un nuovo multi-istanza servizio toohello server di gestione temporanea ed eseguire uno scambio VIP.

<a name="RollbackofanUpdate"></a>

## <a name="rollback-of-an-update"></a>Ripristino dello stato precedente di un aggiornamento
Azure offre flessibilità nella gestione dei servizi durante un aggiornamento consentendo l'avvio di altre operazioni su un servizio, dopo la richiesta di aggiornamento iniziale hello è accettata da hello Controller di infrastruttura di Azure. Un'operazione di rollback può essere eseguita solo quando un aggiornamento (modifica della configurazione) o l'aggiornamento è in hello **in corso** stato sulla distribuzione di hello. Un aggiornamento o l'aggiornamento viene considerato toobe in corso, purché vi sia almeno un'istanza del servizio hello che non è ancora stato aggiornato toohello nuova versione. tootest se è consentito il rollback, controllare il valore di hello del flag RollbackAllowed hello, restituito da [Get Deployment](https://msdn.microsoft.com/library/azure/ee460804.aspx) e [ottenere proprietà del servizio Cloud](https://msdn.microsoft.com/library/azure/ee460806.aspx) operazioni, è impostato tootrue.

> [!NOTE]
> Rende senso toocall Rollback solo in un **sul posto** aggiornamento perché gli aggiornamenti di scambio VIP comportano la sostituzione di un'intera istanza in esecuzione del servizio con un altro.
>
>

Rollback di un aggiornamento in corso ha hello effetti sulla distribuzione di hello seguenti:

* Tutte le istanze di ruolo che non fosse stata aggiornata o aggiornati toohello nuova versione non vengono aggiornate o aggiornate, poiché tali istanze sono già in esecuzione la versione di destinazione hello del servizio hello.
* Le istanze di qualsiasi ruolo che era già stata aggiornata o aggiornato toohello nuova versione del pacchetto del servizio hello (\*con estensione cspkg) hello o file di configurazione del servizio (\*. cscfg) file o entrambi i file sono toohello ripristinato versione pre-aggiornamento di Questi file.

Ciò viene fornita dai hello seguenti caratteristiche:

* Hello [Rollback aggiornamento o l'aggiornamento](https://msdn.microsoft.com/library/azure/hh403977.aspx) operazione, che può essere chiamato su un aggiornamento della configurazione (attivato chiamando [modificare la configurazione di distribuzione](https://msdn.microsoft.com/library/azure/ee460809.aspx)) o un aggiornamento (attivato chiamando [ L'aggiornamento della distribuzione](https://msdn.microsoft.com/library/azure/ee460793.aspx)), purché vi sia almeno un'istanza nel servizio hello che non è ancora stato aggiornato toohello nuova versione.
* Hello Locked ed elemento hello RollbackAllowed, che vengono restituiti come parte del corpo della risposta hello di hello [Get Deployment](https://msdn.microsoft.com/library/azure/ee460804.aspx) e [ottenere proprietà del servizio Cloud](https://msdn.microsoft.com/library/azure/ee460806.aspx) operazioni:

  1. elemento bloccato Hello consente toodetect quando un'operazione di mutazione può essere richiamata su una distribuzione specificata.
  2. Hello RollbackAllowed elemento consente toodetect quando hello [Rollback dell'aggiornamento](https://msdn.microsoft.com/library/azure/hh403977.aspx) operazione può essere chiamata in una distribuzione specificata.

  In ordine tooperform un rollback, non si dispone toocheck sia hello Locked e RollbackAllowed elementi hello. È sufficiente tooconfirm RollbackAllowed viene impostato tootrue. Questi elementi vengono restituiti solo se questi metodi vengono richiamati mediante l'intestazione della richiesta hello impostato troppo "x-ms-version: 2011-10-01" o una versione successiva. Per altre informazioni sul controllo delle versioni delle intestazioni, vedere [Controllo delle versioni di gestione del servizio](https://msdn.microsoft.com/library/azure/gg592580.aspx).

In alcune situazioni un ripristino dello stato precedente di un aggiornamento non è supportato, come nei casi seguenti:

* Riduzione delle risorse locali - se hello aggiornamento aumenta hello risorse locali per un ruolo hello piattaforma Azure non consente il rollback.
* Limiti di quota - se update hello è un'operazione potrebbe non essere più di ridimensionamento è sufficiente calcolo quota toocomplete hello l'operazione di rollback. Ogni sottoscrizione di Azure è una quota associata che specifica hello il numero massimo di core che possono essere utilizzati da tutti i servizi ospitati che appartengono toothat sottoscrizione. Se l'esecuzione di un ripristino dello stato precedente di un determinato aggiornamento farà superare la quota prevista per la sottoscrizione, il ripristino dello stato precedente non verrà abilitato.
* Race condition - se l'aggiornamento iniziale hello è stata completata, non è possibile un rollback.

Un esempio di quando potrebbe essere utile eseguire il rollback di un aggiornamento hello è se si utilizza hello [l'aggiornamento della distribuzione](https://msdn.microsoft.com/library/azure/ee460793.aspx) operazione tasso di hello toocontrol modalità manuale in corrispondenza del quale servizio ospitato un tooyour aggiornamento sul posto principale Azure è implementato.

Durante l'implementazione di hello dell'aggiornamento hello chiamare [l'aggiornamento della distribuzione](https://msdn.microsoft.com/library/azure/ee460793.aspx) in modalità manuale e iniziare toowalk domini di aggiornamento. Se a un certo punto durante il monitoraggio aggiornamento hello, si nota in hello primi domini di aggiornamento che esaminano alcune istanze del ruolo sono diventate non risponde, è possibile chiamare hello [Rollback dell'aggiornamento](https://msdn.microsoft.com/library/azure/hh403977.aspx) operazione sulla distribuzione di hello, che lascia le istanze hello invariati non ancora aggiornate e le istanze di rollback che era stato aggiornato toohello pacchetto del servizio precedente e la configurazione.

<a name="multiplemutatingoperations"></a>

## <a name="initiating-multiple-mutating-operations-on-an-ongoing-deployment"></a>Avvio di più operazioni di mutazione durante una distribuzione
In alcuni casi è opportuno tooinitiate più operazioni di mutazione simultanee in una distribuzione in corso. Ad esempio, è possibile eseguire un aggiornamento del servizio e, durante l'aggiornamento software nel servizio, si desidera toomake alcune modifiche, ad esempio tooroll hello nuovamente l'aggiornamento, si applicano a un altro aggiornamento o anche eliminare la distribuzione di hello. Un caso in cui ciò potrebbe essere necessario è se un aggiornamento del servizio contiene codice anomalo che causa un arresto anomalo toorepeatedly istanza di ruolo aggiornata. In questo caso, hello Controller di infrastruttura di Azure non sarà in grado di toomake lo stato di avanzamento nell'applicazione con l'aggiornamento perché un numero sufficiente di istanze nel dominio aggiornato hello sia integro. Questo stato è tooas di cui si fa riferimento un *distribuzione bloccata*. È possibile sbloccare distribuzione hello rollback hello aggiornamento o l'applicazione di un nuovo aggiornamento sopra hello in mancanza di uno.

Una volta servizio hello tooupdate o aggiornamento hello richiesta iniziale è stato ricevuto da hello Controller di infrastruttura di Azure, è possibile avviare le operazioni di mutazione successive. Ovvero, non si dispone toowait per hello operazione iniziale toocomplete prima di iniziare un'altra operazione di mutazione.

Avviare una seconda operazione di aggiornamento mentre è in corso l'aggiornamento prima di hello eseguirà l'operazione di rollback toohello simile. Se hello secondo aggiornamento è in modalità automatica, hello primo dominio di aggiornamento verrà aggiornato immediatamente, causando tooinstances da più domini di aggiornamento offline hello stesso punto nel tempo.

Hello operazioni di mutazione sono le seguenti: [modificare la configurazione di distribuzione](https://msdn.microsoft.com/library/azure/ee460809.aspx), [l'aggiornamento della distribuzione](https://msdn.microsoft.com/library/azure/ee460793.aspx), [lo stato di distribuzione](https://msdn.microsoft.com/library/azure/ee460808.aspx), [eliminare Distribuzione](https://msdn.microsoft.com/library/azure/ee460815.aspx), e [aggiornamento Rollback](https://msdn.microsoft.com/library/azure/hh403977.aspx).

Due operazioni, [Get Deployment](https://msdn.microsoft.com/library/azure/ee460804.aspx) e [ottenere proprietà del servizio Cloud](https://msdn.microsoft.com/library/azure/ee460806.aspx), restituire i flag bloccato hello che può essere esaminato toodetermine se un'operazione di mutazione può essere richiamata su una distribuzione specificata.

In ordine toocall hello versione di questi metodi che restituisce i flag bloccato hello, è necessario impostare l'intestazione richiesta troppo "x-ms-version: 2011-10-01" o una versione successiva. Per altre informazioni sul controllo delle versioni delle intestazioni, vedere [Controllo delle versioni di gestione del servizio](https://msdn.microsoft.com/library/azure/gg592580.aspx).

<a name="distributiondfroles"></a>

## <a name="distribution-of-roles-across-upgrade-domains"></a>Distribuzione di ruoli nei domini di aggiornamento
Azure distribuisce uniformemente le istanze di un ruolo in un numero di domini di aggiornamento, che può essere configurato come parte del file di definizione (con estensione csdef) hello del servizio. Hello il numero massimo di domini di aggiornamento è 20 e il valore predefinito di hello è 5. Per ulteriori informazioni su come toomodify hello file di definizione del servizio, vedere [dello Schema di definizione del servizio di Azure (File con estensione csdef)](cloud-services-model-and-package.md#csdef).

Se, ad esempio, il ruolo ha dieci istanze, per impostazione predefinita, ogni dominio di aggiornamento contiene due istanze. Se il ruolo dispone di 14 istanze, quindi quattro hello domini di aggiornamento sono contenute tre istanze e un quinto dominio ne contiene due.

Domini di aggiornamento vengono identificati con un indice in base zero: hello primo dominio di aggiornamento con ID 0 e il secondo dominio di aggiornamento hello con ID 1 e così via.

Hello diagramma seguente illustra come un servizio che contiene due ruoli vengono distribuiti quando il servizio di hello definisce due domini di aggiornamento. servizio Hello è in esecuzione otto istanze del ruolo web hello e nove istanze del ruolo di lavoro hello.

![Distribuzione di domini di aggiornamento](media/cloud-services-update-azure-service/IC345533.png "Distribuzione di domini di aggiornamento")

> [!NOTE]
> Si noti che Azure controlla come le istanze vengono allocate nei domini di aggiornamento. Non è possibile toospecify quali istanze siano allocate toowhich dominio.
>
>

## <a name="next-steps"></a>Passaggi successivi
[Come tooManage dei servizi Cloud](cloud-services-how-to-manage.md)  
[Come tooMonitor dei servizi Cloud](cloud-services-how-to-monitor.md)  
[Come tooConfigure dei servizi Cloud](cloud-services-how-to-configure.md)  
