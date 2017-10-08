---
title: aaaConnect tooa macchina virtuale di SQL Server (gestione delle risorse) | Documenti Microsoft
description: Informazioni su come tooconnect tooSQL Server in esecuzione in una macchina virtuale in Azure. Questo argomento viene utilizzato il modello di distribuzione classica hello. scenari di Hello diversi a seconda della configurazione di rete hello e il percorso di hello del client hello.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: 7b127c14c37b9a72c19ed17f8b1dad61c7bc2d38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-resource-manager"></a>Connettersi tooa macchina virtuale di SQL Server in Azure (gestione delle risorse)
> [!div class="op_single_selector"]
> * [Gestione risorse](virtual-machines-windows-sql-connect.md)
> * [Classico](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a>Panoramica

In questo argomento viene descritto come tooconnect tooyour SQL Server dell'istanza in esecuzione in una macchina virtuale di Azure. Illustra alcuni [scenari di connettività generali](#connection-scenarios) e quindi descrive la [procedura dettagliata per la configurazione della connettività di SQL Server in una macchina virtuale di Azure](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Per una procedura dettagliata completa del provisioning e della connettività, vedere [Provisioning di una macchina virtuale di SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).

## <a name="connection-scenarios"></a>Scenari di connessione

modo Hello un client si connette a Server in esecuzione in una macchina virtuale varia a seconda della posizione di hello del client hello e configurazione di rete hello tooSQL.

Se si esegue il provisioning di una VM SQL Server in hello portale di Azure, è possibile hello che specifica il tipo di hello di **connettività SQL**.

![Opzione di connettività SQL pubblica durante il provisioning](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

Le opzioni per la connettività sono:

| Opzione | Descrizione |
|---|---|
| **Pubblica** | Connettersi tooSQL Server su hello internet |
| **Privata** | Connettersi tooSQL Server in hello stessa rete virtuale |
| **Locale** | Connettersi tooSQL Server in locale hello stessa macchina virtuale | 

Nelle sezioni seguenti Hello viene hello **pubblica** e **privata** opzioni in modo più dettagliato.

## <a name="connect-toosql-server-over-hello-internet"></a>Connettersi tooSQL Server su Internet hello

Se si desidera motore di database di SQL Server tooconnect tooyour da hello Internet, selezionare **pubblica** per hello **connettività SQL** nel portale di hello durante il provisioning del tipo. portale Hello hello automaticamente i passaggi seguenti:

* Abilita protocollo TCP/IP hello per SQL Server.
* Configura hello di tooopen una regola firewall la porta TCP di SQL Server (valore predefinito 1433).
* Abilita l'autenticazione di SQL Server, necessaria per l'accesso pubblico.
* Configura gruppo di sicurezza di rete hello hello traffico TCP tooall delle macchine Virtuali su hello porta SQL Server.

> [!IMPORTANT]
> le immagini di macchina virtuale Hello per SQL Server Developer hello e le edizioni Express non abilitano automaticamente il protocollo TCP/IP hello. Per le edizioni Developer ed Express, è necessario utilizzare Gestione configurazione SQL Server troppo[abilitare manualmente il protocollo TCP/IP hello](#manualtcp) dopo la creazione di hello macchina virtuale.

Qualsiasi client con accesso a internet può connettersi toohello istanza di SQL Server specificando l'indirizzo IP pubblico hello della macchina virtuale hello o qualsiasi etichetta DNS assegnato l'indirizzo IP toothat. Se la porta di SQL Server hello è 1433, non è necessario toospecify nella stringa di connessione hello. Hello seguente stringa di connessione si connette tooa VM SQL con un'etichetta DNS di `sqlvmlabel.eastus.cloudapp.azure.com` utilizzando l'autenticazione di SQL (è anche possibile usare indirizzi IP pubblici hello).

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

Sebbene in questo modo la connettività per i client su internet di hello, ciò non implica che tutti gli utenti possono connettersi tooyour SQL Server. I client esterni avere toohello correttezza del nome utente e password. Tuttavia, per maggiore sicurezza, è possibile evitare la porta 1433 noto hello. Ad esempio, se è stato configurato toolisten di SQL Server sulla porta 1500 e stabilito firewall appropriate e regole di gruppo di sicurezza di rete, è Impossibile connettersi aggiungendo hello porta numero toohello nome del Server. Hello esempio seguente viene modificato hello precedente tramite l'aggiunta di un numero di porta personalizzato, **1500**, nome del server toohello:

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> Quando si esegue una query SQL Server in una macchina virtuale su hello internet, tutti i dati in uscita da hello Azure datacenter è soggetto toonormal [prezzi sui trasferimenti di dati in uscita](https://azure.microsoft.com/pricing/details/data-transfers/).

## <a name="connect-toosql-server-within-a-virtual-network"></a>Connettersi tooSQL Server all'interno di una rete virtuale

Quando si sceglie **privata** per hello **connettività SQL** tipo nel portale di hello Azure consente di configurare la maggior parte delle impostazioni di hello identiche troppo**pubblica**. Hello una differenza è che non sia presente alcuna regola tooallow di rete sicurezza gruppo di fuori del traffico sulla porta di SQL Server hello (valore predefinito 1433).

> [!IMPORTANT]
> le immagini di macchina virtuale Hello per SQL Server Developer hello e le edizioni Express non abilitano automaticamente il protocollo TCP/IP hello. Per le edizioni Developer ed Express, è necessario utilizzare Gestione configurazione SQL Server troppo[abilitare manualmente il protocollo TCP/IP hello](#manualtcp) dopo la creazione di hello macchina virtuale.

La connettività privata viene spesso usata in combinazione con una [rete virtuale](../../../virtual-network/virtual-networks-overview.md), che consente diversi scenari. È possibile connettere le macchine virtuali nella stessa rete virtuale, anche se tali macchine virtuali presenti in diversi gruppi di risorse hello. Con una [VPN da sito a sito](../../../vpn-gateway/vpn-gateway-site-to-site-create.md)è possibile creare un'architettura ibrida che connette le macchine virtuali a computer e reti locali.

Reti virtuali abilitare anche toojoin è il dominio di tooa macchine virtuali di Azure. Si tratta di hello solo modo toouse l'autenticazione di Windows tooSQL Server. Hello altri scenari di connessione richiedono l'autenticazione di SQL con nomi utente e password.

Supponendo che è stato configurato DNS nella rete virtuale, è possibile connettersi tooyour istanza di SQL Server specificando il nome del computer hello macchina virtuale SQL Server nella stringa di connessione hello. Hello di esempio seguente, inoltre si presuppone che anche l'autenticazione di Windows è stata configurata e tale utente di hello è stata concessa l'istanza di SQL Server di accesso toohello.

```
Server=mysqlvm;Integrated Security=true
```

## <a id="change"></a>Modificare le impostazioni di connettività SQL

È possibile modificare le impostazioni di connettività hello per la macchina virtuale di SQL Server nel portale di Azure hello.

1. Nel portale di Azure hello, selezionare **macchine virtuali**.

2. Selezionare la VM di SQL Server.

3. In **Impostazioni** fare clic su **Configurazione di SQL Server**.

4. Hello modifica **il livello di connettività SQL** tooyour necessaria l'impostazione. Facoltativamente, è possibile utilizzare questo hello toochange area porta SQL Server o le impostazioni di autenticazione di SQL Server hello.

   ![Modificare la connettività SQL](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. Attendere alcuni minuti per hello toocomplete di aggiornamento.

   ![Notifica dell'aggiornamento della VM SQL](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <a id="manualtcp"></a>Abilitare TCP/IP per SQL Server Developer Edition ed Express Edition

Quando si modificano le impostazioni di connettività di SQL Server, Azure non si attiva automaticamente il protocollo TCP/IP hello per le edizioni Express e SQL Server Developer Edition. passaggi Hello riportati di seguito viene illustrato come toomanually abilitare TCP/IP in modo che è possibile connettersi in remoto utilizzando un indirizzo IP.

Connettere innanzitutto il computer di SQL Server toohello con desktop remoto.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

Successivamente, abilitare il protocollo TCP/IP hello con **Gestione configurazione SQL Server**.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a>Connettersi con SSMS

Hello passaggi seguenti mostrano come toocreate etichetta di un DNS facoltativo per la macchina virtuale di Azure e connettono con SQL Server Management Studio (SSMS).

[!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a>Passaggi successivi

istruzioni di provisioning toosee insieme a questi passaggi di connettività, vedere [Provisioning di una macchina virtuale di SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).

Per altri argomenti correlati toorunning SQL Server in macchine virtuali di Azure, vedere [SQL Server in macchine virtuali di Azure](virtual-machines-windows-sql-server-iaas-overview.md).
