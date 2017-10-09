---
title: "Ripristino di emergenza di gruppi di disponibilità Server - macchine virtuali di Azure - aaaSQL | Documenti Microsoft"
description: "Questo articolo spiega come raggruppare i tooconfigure disponibilità di SQL Server in macchine virtuali di Azure con una replica in un'area diversa."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 388c464e-a16e-4c9d-a0d5-bb7cf5974689
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: df6238dc61c5a56879c75c9bf7314c618f43c0ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a>Configurare un gruppo di disponibilità AlwaysOn in macchine virtuali di Azure in aree diverse

Questo articolo spiega come tooconfigure una disponibilità di SQL Server Always On gruppo di replica su macchine virtuali di Azure in una posizione remota di Azure. Utilizzare il ripristino di emergenza toosupport questa configurazione.

Questo articolo riguarda tooAzure macchine virtuali in modalità di gestione risorse.

Hello immagine seguente mostra una distribuzione comune di un gruppo di disponibilità in macchine virtuali di Azure:

   ![Gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

In questa distribuzione tutte le macchine virtuali sono in un'unica area di Azure. repliche del gruppo di disponibilità Hello possono avere commit sincrono con failover automatico in SQL-1 e 2 di SQL. toobuild questa architettura, vedere [modello gruppo di disponibilità o esercitazione](virtual-machines-windows-portal-sql-availability-group-overview.md).

Questa architettura è vulnerabile toodowntime se hello regione di Azure diventa inaccessibile. tooovercome questa vulnerabilità, aggiungere una replica in un'area diversa di Azure. Hello diagramma seguente viene presentata la nuova architettura hello:

   ![Ripristino di emergenza del gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

Hello diagramma precedente mostra una nuova macchina virtuale denominata SQL-3. SQL-3 è in un'area di Azure diversa. SQL-3 viene aggiunto toohello Cluster di Failover di Windows Server. SQL-3 può ospitare una replica del gruppo di disponibilità. Si noti infine che hello regione di Azure per SQL-3 è un nuovo servizio di bilanciamento del carico di Azure.

>[!NOTE]
> Un set di disponibilità di Azure è necessario quando più di una macchina virtuale si trova in hello stessa area. Se una macchina virtuale è solo nell'area di hello, hello set di disponibilità non è obbligatorio. È possibile inserire una macchina virtuale in un set di disponibilità solo al momento della creazione. Se macchina virtuale hello è già in un set di disponibilità, è possibile aggiungere una macchina virtuale per un'altra replica in un secondo momento.

In questa architettura, replica hello nell'area remota hello viene normalmente configurato con la modalità di disponibilità con commit asincrono e modalità di failover manuale.

Quando le repliche del gruppo di disponibilità sono nelle macchine virtuali di Azure in aree di Azure diverse, ogni area richiede:

* Un gateway di rete virtuale
* Una connessione gateway di rete virtuale

Hello diagramma seguente mostra come reti hello comunicano tra data center.

   ![Gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
>Questa architettura è soggetta a costi per i dati in uscita replicati tra le aree di Azure. Vedere [Prezzi per la larghezza di banda](http://azure.microsoft.com/pricing/details/bandwidth/).  

## <a name="create-remote-replica"></a>Creare una replica remota

una replica in un data center remoto, toocreate hello i passaggi seguenti:

1. [Creare una rete virtuale nella nuova area hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).

1. [Configurare una connessione di rete virtuale a tramite il portale di Azure hello](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).

   >[!NOTE]
   >In alcuni casi, è possibile la connessione di rete virtuale a toouse PowerShell toocreate hello. Ad esempio, se si utilizzano diversi account di Azure è possibile configurare la connessione hello nel portale di hello. Vedere in questo caso, [configura una rete virtuale multisito connessione usando il portale di Azure di hello](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).

1. [Creare un controller di dominio nella nuova area hello](../../../active-directory/active-directory-new-forest-virtual-machine.md).

   Se il controller di dominio hello nel sito primario di hello non è disponibile, questo controller di dominio fornisce l'autenticazione.

1. [Creare una macchina virtuale di SQL Server nella nuova area hello](virtual-machines-windows-portal-sql-server-provision.md).

1. [Creare un servizio di bilanciamento del carico di Azure in rete hello nella nuova area hello](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).

   Questo servizio di bilanciamento del carico deve:

   - In hello stessa rete e subnet come hello nuova macchina virtuale.
   - Avere un indirizzo IP statico per listener del gruppo di disponibilità hello.
   - Includere un pool back-end costituito solo macchine virtuali hello in hello stessa area come hello bilanciamento del carico.
   - Usare un indirizzo IP specifico toohello TCP porta probe.
   - Dispone di una regola specifica toohello SQL Server in hello di bilanciamento del carico stessa area.  

1. [Aggiungere toohello funzionalità di Clustering di Failover nuovo Server SQL](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).

1. [Dominio hello nuovo SQL Server toohello](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).

1. [Impostare un account di dominio di hello nuovo SQL Server service account toouse](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).

1. [Aggiungere hello toohello di SQL Server nuovo Cluster di Failover di Windows Server](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).

1. Creare una risorsa indirizzo IP nel cluster di hello.

   È possibile creare la risorsa indirizzo IP hello in Gestione Cluster di Failover. Ruolo del gruppo di disponibilità hello destro, fare clic su **Aggiungi risorsa**, **più risorse**, fare clic su **indirizzo IP**.

   ![Creare un indirizzo IP](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   Configurare l'indirizzo IP come segue:

   - Usare la rete hello hello data center remoto.
   - Assegnare l'indirizzo IP hello dal servizio di bilanciamento carico di Azure nuova hello. 

1. Nel nuovo Server SQL in Gestione configurazione SQL Server di hello [abilitare gruppi di disponibilità AlwaysOn](http://msdn.microsoft.com/library/ff878259.aspx).

1. [Porte del firewall Open in hello nuovo Server SQL](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).

   numeri di porta Hello è necessario tooopen variano a seconda dell'ambiente. Aprire le porte per il mirroring di endpoint e Azure hello caricare probe di integrità del servizio di bilanciamento.

1. [Aggiungere un gruppo di disponibilità di replica toohello nella hello nuovo Server SQL](http://msdn.microsoft.com/library/hh213239.aspx).

   Per una replica in un'area di Azure remota, impostarla per la replica asincrona con il failover manuale.  

1. Aggiungere la risorsa indirizzo IP hello come una dipendenza per il cluster di hello listener client accesso punto (nome rete).

   Hello schermata seguente mostra una risorsa cluster di indirizzo IP configurata correttamente:

   ![Gruppo di disponibilità](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   >gruppo di risorse cluster Hello include entrambi gli indirizzi IP. Entrambi gli indirizzi IP sono le dipendenze per punto di accesso client di hello listener. Hello utilizzare **o** operatore nella configurazione delle dipendenze hello cluster.

1. [Impostare i parametri del cluster hello in PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).

Eseguire script di PowerShell hello con il nome di rete cluster hello, indirizzo IP e porta probe configurate nel servizio di bilanciamento del carico hello nella nuova area hello.

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster name for hello network in hello new region (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "<IPResourceName>" # hello cluster name for hello new IP Address resource.
   $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB) in hello new region. This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <nnnnn> # hello probe port you set on hello ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a>Impostare la connessione per più subnet

replica Hello in hello data center remoto fa parte del gruppo di disponibilità hello ma si trova in una subnet diversa. Se la replica diventa la replica primaria di hello, potrebbe verificarsi il timeout di connessione dell'applicazione. Questo comportamento è hello uguale a un gruppo di disponibilità locale in una distribuzione su più subnet. tooallow connessioni dalle applicazioni client, aggiornare la connessione di client hello o configurare la memorizzazione nella cache sulla risorsa nome di rete cluster hello risoluzione dei nomi.

Aggiornare, preferibilmente hello client connessione stringhe tooset `MultiSubnetFailover=Yes`. Vedere [Connessione con MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).

Se non è possibile modificare le stringhe di connessione hello, è possibile configurare la memorizzazione nella cache di risoluzione nome. Vedere [Connection Timeouts in Multi-subnet Availability Group](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/) (Timeout connessione in un gruppo di disponibilità su più subnet).

## <a name="fail-over-tooremote-region"></a>Eseguire il failover tooremote area

tootest listener connettività toohello remoto area, è possibile eseguire il failover regione di hello replica toohello remoto. Durante la replica hello è asincrona, il failover è vulnerabile toopotential perdita di dati. toofail failover senza perdita di dati, impostare toosynchronous modalità di disponibilità hello e tooautomatic modalità di failover hello. Utilizzare hello alla procedura seguente:

1. In **Esplora oggetti**, connettere toohello istanza di SQL Server che ospita la replica primaria hello.
1. In **Gruppi di disponibilità AlwaysOn**, **Gruppi di disponibilità** fare clic con il pulsante destro del mouse sul gruppo di disponibilità e scegliere **Proprietà**.
1. In hello **generale** nella pagina **le repliche di disponibilità**, replica di secondaria hello set in toouse del sito di ripristino di emergenza hello **Commit sincrono** modalità di disponibilità e **Automatico** modalità di failover.
1. Se si dispone di una replica secondaria nello stesso sito come replica primaria per la disponibilità elevata, impostare questa replica troppo**Commit asincrono** e **manuale**.
1. Fare clic su OK.
1. In **Esplora oggetti**destro del mouse il gruppo di disponibilità hello e fare clic su **Mostra Dashboard**.
1. Nel dashboard di hello, verificare che hello replica nel sito di ripristino di emergenza hello è sincronizzata.
1. In **Esplora oggetti**destro del mouse il gruppo di disponibilità hello e fare clic su **Failover...** . SQL Server Management Studio apre una procedura guidata toofail su SQL Server.  
1. Fare clic su **Avanti**e l'istanza di SQL Server selezionare hello nel sito di ripristino di emergenza hello. Fare di nuovo clic su **Avanti** .
1. Connettere toohello istanza di SQL Server nel sito di ripristino di emergenza hello e fare clic su **Avanti**.
1. In hello **riepilogo** pagina, verificare le impostazioni di hello e fare clic su **fine**.

Al termine del test di connettività, spostare dati primario di hello replica primaria tooyour indietro center e impostazioni hello disponibilità modalità indietro tootheir normale funzionamento. Hello nella tabella seguente mostra le impostazioni operative normali hello per architettura hello descritte in questo documento:

| Percorso | Istanza del server | Ruolo | Modalità di disponibilità | Modalità di failover
| ----- | ----- | ----- | ----- | -----
| Data center primario | SQL-1 | Primario | Sincrono | Automatico
| Data center primario | SQL-2 | Secondario | Sincrono | Automatico
| Data center secondario o remoto | SQL-3 | Secondario | Asincrono | Manuale


### <a name="more-information-about-planned-and-forced-manual-failover"></a>Altre informazioni sul failover manuale forzato e pianificato

Per ulteriori informazioni, vedere hello seguenti argomenti:

- [Eseguire un failover manuale pianificato di un gruppo di disponibilità (SQL Server)](http://msdn.microsoft.com/library/hh231018.aspx)
- [Eseguire un failover manuale forzato di un gruppo di disponibilità (SQL Server)](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a>Altri collegamenti

* [Gruppi di disponibilità AlwaysOn](http://msdn.microsoft.com/library/hh510230.aspx)
* [Macchine virtuali di Azure](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [Servizi di bilanciamento del carico di Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [Set di disponibilità di Azure](../manage-availability.md)
