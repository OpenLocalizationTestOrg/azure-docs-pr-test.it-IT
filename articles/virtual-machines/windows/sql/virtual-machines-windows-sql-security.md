---
title: Considerazioni per SQL Server in Azure aaaSecurity | Documenti Microsoft
description: Questo argomento include linee guida generali per proteggere SQL Server in esecuzione in una macchina virtuale di Azure.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: d710c296-e490-43e7-8ca9-8932586b71da
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/02/2017
ms.author: jroth
ms.openlocfilehash: 14c3d828fa87446da67beea6d28886de254afe15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-sql-server-in-azure-virtual-machines"></a>Considerazioni relative alla sicurezza per SQL Server in Macchine virtuali di Azure

In questo argomento include linee guida di sicurezza generali che consentono di stabilire l'accesso sicuro tooSQL istanze del Server in una macchina virtuale di Azure (VM).

Azure è conforme a diverse normative del settore e standard che consentono di toobuild una soluzione compatibile con SQL Server in esecuzione in una macchina virtuale. Per informazioni sulla conformità alle normative con Azure, vedere il [Centro protezione di Azure](https://azure.microsoft.com/support/trust-center/).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="control-access-toohello-sql-vm"></a>Controllo accesso toohello SQL VM

Quando si crea la macchina virtuale SQL Server, prendere in considerazione come toocarefully controllare chi ha accesso toohello computer e tooSQL Server. In generale, è necessario eseguire il seguente hello:

- Limitare l'accesso tooSQL Server tooonly hello applicazioni e i client che ne hanno necessità.
- Seguire le procedure consigliate per la gestione di account utente e password.

Hello le sezioni seguenti fornisce suggerimenti su pensare per questi punti.

## <a name="secure-connections"></a>Connessioni sicure

Quando si crea una macchina virtuale di SQL Server con un'immagine della raccolta, hello **connettività di SQL Server** offre hello scelta dell'opzione **locale (all'interno di macchina virtuale)**, **privata (all'interno di rete virtuale)** , o **pubblico (Internet)**.

![Connettività di SQL Server](./media/virtual-machines-windows-sql-security/sql-vm-connectivity-option.png)

Per una sicurezza ottimale hello, scegliere l'opzione più restrittiva di hello per lo scenario. Ad esempio, se si esegue un'applicazione che accede a SQL Server su hello stessa macchina virtuale, quindi **locale** è l'opzione più sicura hello. Se si esegue un'applicazione Azure che richiede accesso toohello SQL Server, quindi **privata** consente di proteggere la comunicazione tooSQL Server solo all'interno di hello specificato [rete virtuale di Azure](../../../virtual-network/virtual-networks-overview.md). Se è necessario **pubblica** (internest) accesso toohello macchina virtuale di SQL Server, quindi assicurarsi di toofollow che altre procedure consigliate in questo argomento tooreduce la superficie di attacco.

Hello le opzioni selezionate nel portale di hello utilizzano regole di sicurezza in ingresso su macchine virtuali hello [Network Security Group](../../../virtual-network/virtual-networks-nsg.md) tooallow (gruppo) o negare macchina virtuale tooyour il traffico di rete. È possibile modificare o creare nuove regole in entrata di gruppo porta di SQL Server tooallow traffico toohello (valore predefinito 1433). È anche possibile specificare indirizzi IP specifici che sono consentiti toocommunicate tramite questa porta.

![Regole dei gruppi di sicurezza di rete](./media/virtual-machines-windows-sql-security/sql-vm-network-security-group-rules.png)

Inoltre tooNSG regole toorestrict il traffico di rete, è inoltre possibile utilizzare hello Windows Firewall nella macchina virtuale hello.

Se si utilizza l'endpoint con il modello di distribuzione classica hello, rimuovere tutti gli endpoint nella macchina virtuale hello se non si utilizza. Per istruzioni sull'uso di ACL con gli endpoint, vedere [Gestisci hello ACL su un endpoint](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint). Questo non è necessario per le macchine virtuali che utilizzano hello Gestione risorse.

Infine, è possibile abilitare connessioni crittografate per istanza hello hello il motore di Database di SQL Server nella macchina virtuale di Azure. Configurare l'istanza di SQL server con un certificato firmato. Per ulteriori informazioni, vedere [toohello abilitare connessioni crittografate motore di Database](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine) e [sintassi della stringa di connessione](https://msdn.microsoft.com/library/ms254500.aspx).

## <a name="use-a-non-default-port"></a>Usare una porta diversa da quella predefinita

Per impostazione predefinita, SQL Server è in ascolto sulla porta 1433 che tutti conoscono. Per una maggiore sicurezza, configurare SQL Server toolisten su una porta non predefinito, ad esempio 1401. Se si esegue il provisioning di un'immagine della raccolta di SQL Server in hello portale di Azure, è possibile specificare la porta in hello **impostazioni di SQL Server** blade.

tooconfigure questo dopo il provisioning, sono disponibili due opzioni:

- Per le macchine virtuali di gestione risorse, è possibile selezionare **configurazione di SQL Server** dal pannello della panoramica hello macchina virtuale. Ciò fornisce un'opzione porta hello toochange.

  ![Modificare la porta TCP nel portale](./media/virtual-machines-windows-sql-security/sql-vm-change-tcp-port.png)

- Per le macchine virtuali classiche o per macchine virtuali di SQL Server che non è stato eseguito il provisioning con il portale di hello, è possibile configurare manualmente la porta hello connettendosi in remoto toohello macchina virtuale. Per i passaggi di configurazione hello, vedere [configurare un Server tooListen su una porta TCP specifica](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port). Se si utilizza questa tecnica manuale, è necessario anche tooadd un Windows Firewall regola tooallow il traffico in ingresso sulla porta TCP.

> [!IMPORTANT]
> Specifica di una porta non predefinito è una buona idea se le connessioni internet toopublic aprire la porta di SQL Server.

Quando SQL Server è in ascolto su una porta non predefinito, è necessario specificare la porta hello quando ci si connette. Ad esempio, si consideri uno scenario in cui l'indirizzo IP del server hello è 13.55.255.255 e SQL Server è in ascolto sulla porta 1401. tooconnect tooSQL Server, è possibile specificare `13.55.255.255,1401` nella stringa di connessione hello.

## <a name="manage-accounts"></a>Gestisci account

Per evitare che utenti malintenzionati tooeasily ipotesi account nomi o password. Utilizzare hello toohelp i suggerimenti seguenti:

- Creare un account amministratore locale univoco non denominato **Amministratore**.

- Usare password complesse per tutti gli account. Per ulteriori informazioni su come toocreate una password complessa, vedere [creare una password complessa](https://support.microsoft.com/instantanswers/9bd5223b-efbe-aa95-b15a-2fb37bef637d/create-a-strong-password) articolo.

- Per impostazione predefinita, in Azure viene selezionata l'autenticazione di Windows durante l'installazione della macchina virtuale SQL Server. Pertanto, hello **SA** account di accesso è disabilitato e viene assegnata una password dal programma di installazione. È consigliabile che hello **SA** account di accesso non deve essere utilizzata oppure abilitato. Se è necessario avere un account di accesso SQL, utilizzare una delle seguenti strategie hello:

  - Creare un account SQL con un nome univoco che abbia appartenenza **sysadmin**. È possibile farlo dal portale hello abilitando **l'autenticazione di SQL** durante il provisioning.

    > [!TIP] 
    > Se non si abilita l'autenticazione di SQL Server durante il provisioning, è necessario modificare manualmente la modalità di autenticazione hello troppo**SQL Server e l'autenticazione di Windows**. Per altre informazioni, vedere [Modifica della modalità di autenticazione del server](https://docs.microsoft.com/sql/database-engine/configure-windows/change-server-authentication-mode).

  - Se è necessario utilizzare hello **SA** account di accesso, abilitare hello login dopo il provisioning e assegnare una nuova password complessa.

## <a name="follow-on-premises-best-practices"></a>Seguire le procedure consigliate locali

Inoltre toohello consigliate descritte in questo argomento, è consigliabile rivedere e implementare procedure di sicurezza locali tradizionali hello dove applicabile. Per altre informazioni, vedere [Considerazioni sulla sicurezza per un'installazione di SQL Server](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation).

## <a name="next-steps"></a>Passaggi successivi

Se si è interessati anche alle procedure consigliate relative alle prestazioni, vedere [Procedure consigliate per le prestazioni per SQL Server in Macchine virtuali di Azure](virtual-machines-windows-sql-performance.md).

Per altri argomenti correlati toorunning SQL Server in macchine virtuali di Azure, vedere [SQL Server in macchine virtuali di Azure Panoramica](virtual-machines-windows-sql-server-iaas-overview.md).

