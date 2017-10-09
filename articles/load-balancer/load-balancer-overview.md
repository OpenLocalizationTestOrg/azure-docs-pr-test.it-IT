---
title: Panoramica di bilanciamento del carico aaaAzure | Documenti Microsoft
description: "Panoramica di funzionalità, architettura e implementazione di Azure Load Balancer. Informazioni sul funzionamento di bilanciamento del carico hello e sfruttato tale opportunità nel cloud hello."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
ms.assetid: 0f313dc0-f007-4cee-b2b9-f542357925a3
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 2376a02f7cbbbed6a90f216419c0c3d30f594272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-load-balancer-overview"></a>Panoramica del servizio di bilanciamento del carico

Bilanciamento del carico di Azure offre prestazioni elevate, disponibilità e la rete tooyour applicazioni. Si tratta di un servizio di bilanciamento del carico di livello 4 (TCP, UDP) che distribuisce il traffico in ingresso tra istanze integre di servizi definiti in un set con carico bilanciato.

Azure Load Balancer può essere configurato per:

* Caricare il saldo in ingresso Internet traffico toovirtual macchine. Questa configurazione è nota come [bilanciamento del carico Internet tra più macchine virtuali o servizi](load-balancer-internet-overview.md).
* Bilanciare il carico del traffico tra macchine virtuali in una rete virtuale, tra macchine virtuali nei servizi cloud o tra computer locali e macchine virtuali in una rete virtuale cross-premise. Questa configurazione è nota come [bilanciamento del carico interno](load-balancer-internal-overview.md).
* Inoltrare il traffico esterno tooa macchina virtuale specifica.

Tutte le risorse nel cloud hello necessario raggiungibile da Internet hello un toobe di indirizzo IP pubblico. infrastruttura di cloud Hello in Azure Usa gli indirizzi IP non instradabili per le risorse. Azure Usa il servizio NAT (Network address translation) con toohello toocommunicate gli indirizzi IP pubblico Internet.

## <a name="azure-deployment-models"></a>Modelli di distribuzione di Azure

È importante toounderstand hello differenze hello Azure classico e Gestione risorse [modelli di distribuzione](../azure-resource-manager/resource-manager-deployment-model.md). Azure Load Balancer viene configurato in modo diverso in ogni modello.

### <a name="azure-classic-deployment-model"></a>Modello di distribuzione classica di Azure

Macchine virtuali distribuite all'interno di un servizio cloud possono essere raggruppati toouse un bilanciamento del carico. In questo modello un indirizzo IP pubblico e un nome di dominio completo (FQDN) assegnati servizio cloud tooa. servizio di bilanciamento del carico Hello porta traduzione e bilancia il carico del traffico di rete hello tramite indirizzo IP pubblico hello per il servizio cloud hello.

Il traffico con carico bilanciato è definito dagli endpoint. Endpoint di traduzione porte hanno una relazione uno a uno tra hello assegnato pubblico porta dell'indirizzo IP pubblico hello e hello locale assegnato servizio toohello su una macchina virtuale specifica. Gli endpoint di bilanciamento del carico hanno una relazione uno-a-molti tra l'indirizzo IP pubblico hello e hello locale porte assegnate toohello services nelle macchine virtuali hello nel servizio cloud hello.

![Bilanciamento del carico di Azure nel modello di distribuzione classica hello](./media/load-balancer-overview/asm-lb.png)

Figura 1: bilanciamento del carico di Azure nel modello di distribuzione classica hello

etichetta del dominio per l'indirizzo IP pubblico hello che utilizza Bilanciamento carico per questo modello di distribuzione hello Hello è \<nome del servizio cloud\>. cloudapp.net. Hello figura seguente illustra hello bilanciamento del carico di Azure in questo modello.

### <a name="azure-resource-manager-deployment-model"></a>Modello di distribuzione di Azure Resource Manager

Nel modello di distribuzione di gestione risorse di hello non è toocreate è necessario un servizio Cloud. servizio di bilanciamento del carico Hello viene creato tooexplicitly instradare il traffico tra più macchine virtuali.

Un indirizzo IP pubblico è una singola risorsa con un'etichetta di dominio (nome DNS). indirizzo IP pubblico Hello è associata a una risorsa di bilanciamento del carico hello. Regole di bilanciamento del carico e delle regole NAT in ingresso utilizzano l'indirizzo IP pubblico hello come hello endpoint Internet per le risorse di hello che ricevono il traffico con bilanciamento del carico di rete.

Un indirizzo IP pubblico o privato viene assegnato a macchina virtuale tooa di toohello rete interfaccia risorsa collegata. Una volta un'interfaccia di rete viene aggiunto a pool di indirizzi IP del tooa di bilanciamento del carico back-end, bilanciamento del carico hello è in grado di toosend con bilanciamento del carico di traffico di rete in base alle regole di bilanciamento del carico hello che vengono create.

Hello immagine seguente mostra hello bilanciamento del carico di Azure in questo modello:

![Azure Load Balancer in Resource Manager](./media/load-balancer-overview/arm-lb.png)

Figura 2. Azure Load Balancer in Resource Manager

servizio di bilanciamento del carico Hello può essere gestita tramite Gestione risorse basato su modelli, API e strumenti. toolearn più su Gestione risorse, vedere hello [Panoramica di gestione risorse](../azure-resource-manager/resource-group-overview.md).

## <a name="load-balancer-features"></a>Funzionalità del bilanciamento del carico

* Distribuzione basata su hash

    Il servizio di bilanciamento del carico di Azure usa un algoritmo di distribuzione basato su hash. Per impostazione predefinita, Usa un hash di 5 tuple composto da indirizzo IP di origine, porta di origine, destinazione IP, porta di destinazione e protocollo tipo toomap traffico tooavailable server. La persistenza viene mantenuta solo *all'interno* di una sessione di trasporto. I pacchetti hello sarà stessa sessione TCP o UDP indirizzate toohello stessa istanza dietro a endpoint con bilanciamento del carico hello. Quando hello client chiude e riapre la connessione hello o avvia una nuova sessione da hello stesso IP di origine, hello modifiche della porta di origine. Ciò potrebbe causare hello traffico toogo tooa altro endpoint in un altro Data Center.

    Per altre informazioni dettagliate, vedere [Modalità di distribuzione del servizio di bilanciamento del carico (affinità IP di origine)](load-balancer-distribution-mode.md). Hello immagine seguente mostra la distribuzione basata su hash hello:

    ![Distribuzione basata su hash](./media/load-balancer-overview/load-balancer-distribution.png)

    Figura 3. Distribuzione basata su hash

* Port forwarding

    Il servizio di bilanciamento del carico di Azure consente di controllare la gestione della comunicazione in ingresso. Questa comunicazione include il traffico avviato da host Internet, macchine virtuali in altri servizi cloud o reti virtuali. Questo controllo è rappresentato da un endpoint, detto anche endpoint di input.

    Un endpoint di input è in ascolto su una porta pubblica e inoltra il traffico della porta interna tooan. È possibile mappare hello stesso porte per un endpoint interno o esterno o utilizzare una porta diversa per loro. Ad esempio, si può avere un tooport toolisten di web server configurato 81 mentre mapping degli endpoint pubblici hello è la porta 80. creazione di Hello di un endpoint pubblico genera la creazione di hello di un'istanza del servizio di bilanciamento del carico.

    Quando create usando hello portale di Azure, portale hello crea automaticamente gli endpoint toohello virtual machine hello Remote Desktop Protocol (RDP) e il traffico della sessione di Windows PowerShell remoto. È possibile utilizzare questi endpoint tooremotely amministrare macchina virtuale hello su hello Internet.

* Riconfigurazione automatica

    Il servizio di bilanciamento del carico di Azure si riconfigura immediatamente quando si aumentano o si riducono le istanze. La riconfigurazione, ad esempio, si verifica quando si aumenta hello conteggio delle istanze per i ruoli web/di lavoro in un servizio cloud o quando si aggiungono macchine virtuali in hello stesso con bilanciamento del carico impostato.

* Monitoraggio del servizio

    Bilanciamento del carico di Azure può probe di integrità hello di hello diverse istanze del server. Quando un probe ha esito negativo toorespond, bilanciamento del carico hello interrompe l'invio di nuove connessioni toohello le istanze di tipo non integro. Ciò non influisce sulle connessioni esistenti.

    Sono supportati tre tipi di probe:

    + **Probe di agente guest (nella piattaforma come un servizio macchine virtuali solo):** agente guest hello macchina virtuale hello prevede l'utilizzo di bilanciamento del carico hello. è in ascolto Hello agente guest e risponde con una risposta HTTP 200 OK solo quando hello istanza è nello stato ready hello (ad esempio hello istanza non è in uno stato ad esempio disponibilità, il riciclo o arresto). Se l'errore dell'agente di hello toorespond con un HTTP 200 OK, segni di bilanciamento carico di hello hello istanza e arresta l'istanza toothat il traffico di invio. servizio di bilanciamento del carico Hello continua istanza hello tooping. Se l'agente guest hello risponde con un HTTP 200, bilanciamento del carico hello invierà nuovamente istanza toothat di traffico. Quando si utilizza un ruolo web, il codice del sito Web viene eseguito in genere w3wp.exe, non è monitorato da hello infrastruttura di Azure né dall'agente guest. Ciò significa che gli errori in w3wp.exe (ad esempio, le risposte HTTP 500) non saranno segnalate toohello l'agente guest e bilanciamento del carico hello non riconoscerà tootake istanza dalla rotazione.
    + **Probe personalizzato HTTP:** questo probe esegue l'override di probe di hello predefinito (agente guest). È possibile utilizzare toocreate la propria integrità hello toodetermine di logica personalizzata hello istanza del ruolo. servizio di bilanciamento del carico Hello regolarmente eseguiranno il probe dell'endpoint (ogni 15 secondi, per impostazione predefinita). istanza di Hello viene considerato toobe nella rotazione se il servizio risponde con un ACK TCP o HTTP 200 entro il periodo di timeout hello (valore predefinito è 31 secondi). Ciò è utile per implementare la propria istanze tooremove logica dalla rotazione del bilanciamento carico di hello. Ad esempio, è possibile configurare hello istanza tooreturn uno stato non-200 se istanza hello è superiore al 90% della CPU. Per i ruoli web che utilizzano w3wp.exe, è anche possibile ottenere automaticamente il monitoraggio del sito Web, poiché gli errori nel codice del sito Web restituiscono un probe di stato non-200 toohello.
    + **Probe personalizzato TCP:** questo probe si basa sulla porta probe ha esito positivo TCP sessione stabilimento tooa definito.

    Per ulteriori informazioni, vedere hello [schema LoadBalancerProbe](https://msdn.microsoft.com/library/azure/jj151530.aspx).

* Source NAT

    Tutti toohello il traffico in uscita viene sottoposto a Internet che ha origine il servizio NAT (SNAT) di origine utilizzando hello stesso indirizzo VIP come hello il traffico in ingresso. Questo processo offre tre importanti vantaggi:

    + In questo modo facile aggiornamento e ripristino di emergenza di servizi, poiché hello che VIP può essere dinamicamente mappato tooanother istanza del servizio hello.
    + Semplifica la gestione dell'elenco di controllo di accesso (ACL). Tali elenchi espressi in termini di VIP non si modificano in caso di ridimensionamento o ridistribuzione dei servizi.

    configurazione di bilanciamento del carico Hello supporta cono completo NAT per UDP. Cono completo NAT è un tipo di NAT dove porta hello consente le connessioni in ingresso da un host esterno (nella richiesta in uscita tooan risposta).

    Per ogni nuova connessione in uscita che avvia una macchina virtuale, una porta in uscita è allocata anche dal servizio di bilanciamento del carico hello. host esterno Hello vede il traffico con una porta virtuale allocata VIP IP. Per gli scenari che richiedono un numero elevato di connessioni in uscita, è consigliabile toouse [indirizzo IP pubblico a livello di istanza](../virtual-network/virtual-networks-instance-level-public-ip.md) indirizzi in modo che le macchine virtuali hello dispongono di un indirizzo IP in uscita dedicato per SNAT. In questo modo si riduce il rischio di hello di esaurimento delle porte.

    Per altre informazioni su questo argomento, vedere l'articolo [le Connessioni in uscita](load-balancer-outbound-connections.md).

### <a name="support-for-multiple-load-balanced-ip-addresses-for-virtual-machines"></a>Supporto per più indirizzi IP con carico bilanciato per le macchine virtuali
È possibile assegnare più di un bilanciamento del carico pubblico tooa set di indirizzi IP delle macchine virtuali. Grazie a questa funzionalità, è possibile ospitare più siti Web SSL e/o più listener gruppo di disponibilità AlwaysOn di SQL Server su hello stesso insieme di macchine virtuali. Per altre informazioni, vedere [Indirizzi VIP multipli per un servizio cloud](load-balancer-multivip.md).

[!INCLUDE [load-balancer-compare-tm-ag-lb-include.md](../../includes/load-balancer-compare-tm-ag-lb-include.md)]

## <a name="limitations"></a>Limitazioni

I pool di back-end di bilanciamento del carico possono contenere qualsiasi SKU VM, ad eccezione del livello Basic.

## <a name="next-steps"></a>Passaggi successivi

- Altre informazioni sulla [Panoramica del bilanciamento del carico Internet](load-balancer-internet-overview.md)

- Altre informazioni sulla [Panoramica del bilanciamento del carico interno](load-balancer-internal-overview.md)

- Creare un [servizio di bilanciamento del carico Internet](load-balancer-get-started-internet-portal.md)

- Informazioni su alcune delle hello altre chiavi [funzionalità di rete](../networking/networking-overview.md) di Azure

