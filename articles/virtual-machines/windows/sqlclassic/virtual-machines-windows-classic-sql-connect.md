---
title: aaaConnect tooa macchina virtuale di SQL Server in Azure (versione classica) | Documenti Microsoft
description: Informazioni su come tooconnect tooSQL Server in esecuzione in una macchina virtuale in Azure. Questo argomento viene utilizzato il modello di distribuzione classica hello. scenari di Hello diversi a seconda della configurazione di rete hello e il percorso di hello del client hello.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: 416948af-454f-4cfe-8fd2-7cf971cbd3e9
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: jroth
experimental_id: d51f3cc6-753b-4e
ms.openlocfilehash: 4fff3936ad0bcfd3a56855a8436991e19b92522b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-classic-deployment"></a>Connettersi tooa macchina virtuale di SQL Server in Azure (distribuzione classica)
> [!div class="op_single_selector"]
> * [Gestione risorse](../sql/virtual-machines-windows-sql-connect.md)
> * [Classico](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a>Panoramica
In questo argomento viene descritto come tooconnect tooyour SQL Server dell'istanza in esecuzione in una macchina virtuale di Azure. Illustra alcuni [scenari di connettività generali](#connection-scenarios) e quindi descrive la [procedura dettagliata per la configurazione della connettività di SQL Server in una macchina virtuale di Azure](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).

> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Se si utilizzano VM Resource Manager, vedere [connessione macchina virtuale di SQL Server in Azure tramite Gestione risorse di tooa](../sql/virtual-machines-windows-sql-connect.md).

## <a name="connection-scenarios"></a>Scenari di connessione
modo Hello un client si connette a Server in esecuzione in una macchina virtuale varia a seconda della posizione di hello del client hello e configurazione di rete della macchina/hello tooSQL. Tali scenari includono:

* [Connessione Server tooSQL in hello stesso servizio cloud](#connect-to-sql-server-in-the-same-cloud-service)
* [Connettersi tooSQL Server su hello internet](#connect-to-sql-server-over-the-internet)
* [Connettersi tooSQL Server in hello stessa rete virtuale](#connect-to-sql-server-in-the-same-virtual-network)

> [!NOTE]
> Prima di connettersi con uno di questi metodi, è necessario seguire hello [di passaggi di questo tipo di connettività tooconfigure articolo](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).
> 
> 

### <a name="connect-toosql-server-in-hello-same-cloud-service"></a>Connessione Server tooSQL in hello stesso servizio cloud
Più macchine virtuali possono essere create in hello stesso servizio cloud. toounderstand virtuale macchine scenario, vedere [come tooconnect le macchine virtuali con un servizio cloud o di rete virtuale](../classic/connect-vms.md#connect-vms-in-a-standalone-cloud-service). Questo scenario è quando un client in una macchina virtuale tenta tooconnect tooSQL Server in esecuzione in un'altra macchina virtuale in hello stesso servizio cloud.

In questo scenario, è possibile connettersi utilizzando hello VM **nome** (illustrato anche come **nome Computer** o **hostname** nel portale di hello). Questo è il nome di hello fornite per la macchina virtuale hello durante la creazione. Ad esempio, se è denominato VM SQL **mysqlvm**, una VM client in hello nello stesso servizio cloud è possibile utilizzare hello tooconnect di stringa di connessione seguente:

    "Server=mysqlvm;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

### <a name="connect-toosql-server-over-hello-internet"></a>Connettersi tooSQL Server su Internet hello
Se si desidera motore di database di SQL Server tooconnect tooyour da hello Internet, è necessario creare un endpoint della macchina virtuale per la comunicazione TCP in ingresso. Questo passaggio di configurazione di Azure, indirizza in ingresso TCP porta traffico tooa porta TCP è una macchina virtuale toohello accessibile.

tooconnect su hello internet, è necessario utilizzare DNS nome e hello VM endpoint numero di porta hello della macchina virtuale (configurato più avanti in questo articolo). hello toofind nome DNS, passare toohello Azure portale e selezionare **macchine virtuali (classico)**. Selezionare quindi la macchina virtuale. Hello **nome DNS** viene visualizzato in hello **Panoramica** sezione.

Si consideri ad esempio una macchina virtuale classica denominata **mysqlvm** con nome DNS **mysqlvm7777.cloudapp.net** ed endpoint di macchina virtuale **57500**. Supponendo che la connettività configurata correttamente, hello seguente stringa di connessione potrebbe essere macchina virtuale di hello tooaccess utilizzati da qualsiasi posizione su hello internet:

    "Server=mycloudservice.cloudapp.net,57500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

Sebbene in questo modo la connettività per i client su internet di hello, ciò non implica che tutti gli utenti possono connettersi tooyour SQL Server. I client esterni avere toohello correttezza del nome utente e password. Per una maggiore sicurezza, non utilizzare la porta 1433 noto hello per endpoint di macchina virtuale pubblico hello. E, se possibile, provare ad aggiungere un ACL nei client endpoint toorestrict traffico solo toohello autorizzati. Per istruzioni sull'uso di ACL con gli endpoint, vedere [Gestisci hello ACL su un endpoint](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

> [!NOTE]
> È importante toonote quando si utilizza questa tecnica toocommunicate con SQL Server, tutti i dati in uscita da hello Data Center di Azure è soggetto toonormal [prezzi sui trasferimenti di dati in uscita](https://azure.microsoft.com/pricing/details/data-transfers/).
> 
> 

### <a name="connect-toosql-server-in-hello-same-virtual-network"></a>Connettersi tooSQL Server in hello stessa rete virtuale
[rete virtuale](../../../virtual-network/virtual-networks-overview.md) supporta scenari aggiuntivi. È possibile connettere le macchine virtuali nella stessa rete virtuale, anche se tali macchine virtuali presenti in servizi cloud diversi hello. Con una [VPN da sito a sito](../../../vpn-gateway/vpn-gateway-site-to-site-create.md)è possibile creare un'architettura ibrida che connette le macchine virtuali a computer e reti locali.

Reti virtuali consente inoltre di toojoin dominio tooa macchine virtuali di Azure. Si tratta di hello solo modo toouse l'autenticazione di Windows tooSQL Server. Hello altri scenari di connessione richiedono l'autenticazione di SQL con nomi utente e password.

Se si intende tooconfigure un ambiente di dominio e l'autenticazione di Windows, non è necessaria la seguente procedura hello toouse in questo endpoint pubblico di articolo tooconfigure hello o hello l'autenticazione di SQL e gli account di accesso. In questo scenario, è possibile connettersi tooyour istanza di SQL Server specificando il nome della macchina virtuale di SQL Server hello nella stringa di connessione hello. Hello di esempio seguente si presuppone che anche l'autenticazione di Windows è stata configurata e che tale utente di hello è stata concessa l'istanza di SQL Server di accesso toohello.

    "Server=mysqlvm;Integrated Security=true"

## <a name="steps-for-configuring-sql-server-connectivity-in-an-azure-vm"></a>Procedura per la configurazione della connettività di SQL Server in una macchina virtuale di Azure
Hello alla procedura seguente viene illustrato come istanza di SQL Server toohello tooconnect su hello internet utilizzando SQL Server Management Studio (SSMS). Tuttavia, hello stessi passaggi si applicano toomaking la macchina virtuale di SQL Server accessibile per le applicazioni, in esecuzione sia in locale e in Azure.

Prima di poter connettersi toohello istanza di SQL Server da un'altra macchina virtuale o hello internet, è necessario completare hello seguenti attività, come descritto nelle sezioni hello che seguono:

* [Creare un endpoint TCP per la macchina virtuale hello](#create-a-tcp-endpoint-for-the-virtual-machine)
* [Aprire le porte TCP in hello Windows firewall](#open-tcp-ports-in-the-windows-firewall-for-the-default-instance-of-the-database-engine)
* [Configurare SQL Server toolisten su hello protocollo TCP](#configure-sql-server-to-listen-on-the-tcp-protocol)
* [Configurare SQL Server per l'autenticazione in modalità mista](#configure-sql-server-for-mixed-mode-authentication)
* [Creare gli account di accesso di SQL Server](#create-sql-server-authentication-logins)
* [Determinare il nome DNS hello della macchina virtuale hello](#determine-the-dns-name-of-the-virtual-machine)
* [Connettersi toohello motore di Database da un altro computer](#connect-to-the-database-engine-from-another-computer)

percorso di connessione Hello hello seguente diagramma di riepilogo:

![Connessione macchina virtuale di SQL Server tooa](../../../../includes/media/virtual-machines-sql-server-connection-steps/SQLServerinVMConnectionMap.png)

[!INCLUDE [Connect tooSQL Server in a VM Classic TCP Endpoint](../../../../includes/virtual-machines-sql-server-connection-steps-classic-tcp-endpoint.md)]

[!INCLUDE [Connect tooSQL Server in a VM](../../../../includes/virtual-machines-sql-server-connection-steps.md)]

[!INCLUDE [Connect tooSQL Server in a VM Classic Steps](../../../../includes/virtual-machines-sql-server-connection-steps-classic.md)]

## <a name="next-steps"></a>Passaggi successivi
Se inoltre si intende toouse gruppi di disponibilità AlwaysOn per la disponibilità elevata e ripristino di emergenza, è consigliabile implementare un listener. I client di database si connettono listener toohello anziché direttamente tooone hello istanze di SQL Server. Hello listener route client toohello replica primaria nel gruppo di disponibilità hello. Per altre informazioni, vedere l'articolo relativo alla [configurazione di un listener di ILB per gruppi di disponibilità AlwaysOn in Azure](../classic/ps-sql-int-listener.md).

È importante tooreview sicurezza hello tutte le procedure consigliate per SQL Server in esecuzione in una macchina virtuale di Azure. Per altre informazioni, vedere [Considerazioni relative alla sicurezza per SQL Server in Macchine virtuali di Azure](../sql/virtual-machines-windows-sql-security.md).

[Esplorare hello percorso di apprendimento](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) for SQL Server in macchine virtuali di Azure. 

Per altri argomenti correlati toorunning SQL Server in macchine virtuali di Azure, vedere [SQL Server in macchine virtuali di Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

