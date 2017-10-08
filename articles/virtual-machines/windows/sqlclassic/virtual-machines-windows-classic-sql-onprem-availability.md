---
title: "aaaExtend locale tooAzure gruppi di disponibilità AlwaysOn | Documenti Microsoft"
description: "In questa esercitazione Usa le risorse create con il modello di distribuzione classica hello e descrive come toouse hello procedura guidata Aggiungi Replica in SQL Server Management Studio (SSMS) tooadd una replica del gruppo di disponibilità AlwaysOn in Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 7ca7c423-8342-4175-a70b-d5101dfb7f23
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: 51fe117b40d69706b35f30101538a7a36116e128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="extend-on-premises-always-on-availability-groups-tooazure"></a>Estendere tooAzure gruppi di disponibilità AlwaysOn locale
I gruppi di disponibilità AlwaysOn garantiscono un disponibilità elevata per i gruppi di database grazie all'aggiunta di repliche secondarie, che consentono il failover dei database in caso di errore. Possono inoltre essere utilizzati toooffload leggere i carichi di lavoro o attività di backup.

È possibile estendere tooMicrosoft di gruppi di disponibilità locale Azure, il provisioning di uno o più macchine virtuali di Azure con SQL Server e quindi aggiungerli come tooyour repliche locali gruppi di disponibilità.

Questa esercitazione si presuppone di che aver seguito hello:

* Una sottoscrizione di Azure attiva. È possibile [iscriversi per una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* Un gruppo di disponibilità AlwaysOn esistente in locale. Per altre informazioni sui gruppi di disponibilità, vedere [Gruppi di disponibilità AlwaysOn](https://msdn.microsoft.com/library/hh510230.aspx).
* La connettività tra hello locale rete e la rete virtuale di Azure. Per ulteriori informazioni sulla creazione di questa rete virtuale, vedere [crea un sito a sito utilizzando connessione hello del portale di Azure (versione classica)](../../../vpn-gateway/vpn-gateway-howto-site-to-site-classic-portal.md).

> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

## <a name="add-azure-replica-wizard"></a>Procedura guidata Aggiungi replica di Azure
In questa sezione illustra come hello toouse **Aggiungi Replica Azure** tooextend tooinclude di soluzione Azure il gruppo di disponibilità AlwaysOn repliche.

> [!IMPORTANT]
> Hello **Aggiungi Replica Azure** supporta solo macchine virtuali create con modello di distribuzione classica hello. Nuove distribuzioni di macchine Virtuali è consigliabile utilizzare il modello di gestione delle risorse più recente di hello. Se si utilizzano VM con Gestione risorse, è necessario aggiungere manualmente hello secondario replica di Azure utilizzando Transact-SQL commmands (non mostrato qui). Questa procedura guidata non funziona in uno scenario di gestione risorse di hello.

1. In SQL Server Management Studio espandere **Disponibilità elevata AlwaysOn** > **Gruppi di disponibilità** > **[nome del gruppo di disponibilità]**.
2. Fare doppio clic su **Repliche di disponibilità**, quindi fare clic su **Aggiungi Replica**.
3. Per impostazione predefinita, hello **tooAvailability Aggiungi Replica Creazione guidata gruppo** viene visualizzato. Fare clic su **Avanti**.  Se si è scelto di hello **non visualizzare più questa pagina** opzione nella parte inferiore di hello della pagina hello durante un precedente avvio di questa procedura guidata, questa schermata non verrà visualizzato.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742861.png)
4. Sarà richiesto tooconnect tooall esistente repliche. È possibile fare clic su **Connetti...** accanto a ogni replica oppure selezionare **Connetti tutto...** in basso hello hello. Dopo l'autenticazione, fare clic su **Avanti** tooadvance toohello nella schermata successiva.
5. In hello **specifica repliche** pagina più schede vengono elencate nella parte superiore di hello: **repliche**, **endpoint**, **preferenze di Backup**, e **Listener**. Da hello **repliche** scheda, fare clic su **Aggiungi Replica Azure...** toolaunch hello Aggiungi Replica Azure.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742863.png)
6. Selezionare un certificato di gestione di Azure esistente dall'archivio certificati di Windows locale hello se è stato installato prima di. Selezionare o immettere l'id di hello di una sottoscrizione di Azure se è stato utilizzato uno prima. È possibile fare clic su Download toodownload e installare un certificato di gestione di Azure e scaricare hello elenco delle sottoscrizioni con un account Azure.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742864.png)
7. Ogni campo pagina hello con valori che saranno utilizzati toocreate hello Azure Virtual Machine (VM) che ospiterà la replica hello verrà compilato.
   
   | Impostazione | Descrizione |
   | --- | --- |
   | **Immagine** |Selezionare una combinazione di hello desiderato del sistema operativo e SQL Server |
   | **Dimensioni macchina virtuale** |Selezionare dimensione hello della macchina virtuale che meglio si adatta alle esigenze aziendali |
   | **Nome macchina virtuale** |Specificare un nome univoco per hello nuova macchina virtuale. nome Hello deve essere compresa tra 3 e 15 caratteri, può contenere solo lettere, numeri e trattini, deve iniziare con una lettera e terminare con una lettera o un numero. |
   | **Nome utente macchina virtuale** |Specificare un nome utente che verrà configurati come account di amministratore hello su hello VM |
   | **Password amministratore macchina virtuale** |Specificare una password per il nuovo account di hello |
   | **Conferma password** |Conferma password hello del nuovo account di hello |
   | **Rete virtuale** |Specificare hello tale hello deve utilizzare nuova macchina virtuale di rete virtuale di Azure. Per altre informazioni sulle reti virtuali, vedere la pagina di [panoramica sulle reti virtuali](../../../virtual-network/virtual-networks-overview.md). |
   | **Rete virtuale/subnet** |Specificare subnet della rete virtuale hello che hello che nuova macchina virtuale deve usare |
   | **Dominio** |Conferma hello valore già popolato per il dominio hello è corretto |
   | **Nome utente dominio** |Specificare un account che si trova nel gruppo di amministratori locali hello nei nodi del cluster locale hello |
   | **Password** |Specificare la password di hello per nome utente di dominio hello |
8. Fare clic su **OK** toovalidate le impostazioni di distribuzione hello.
9. In seguito vengono visualizzate le condizioni di licenza. Leggere e fare clic su **OK** se si accettano toothese termini.
10. Hello **specifica repliche** nuovamente visualizzata la pagina. Verificare le impostazioni di hello per replica di Azure nuova hello in hello **repliche**, **endpoint**, e **preferenze di Backup** schede. Modificare le impostazioni toomeet i requisiti aziendali.  Per ulteriori informazioni sui parametri hello contenuti in queste schede, vedere [pagina specifica repliche (nuovo guidata gruppo di disponibilità guidata/Aggiungi Replica)](https://msdn.microsoft.com/library/hh213088.aspx). Si noti che non è possibile creare listener tramite scheda Listener hello per gruppi di disponibilità che contengono le repliche di Azure. Inoltre, se un listener è già stato creato hello toolaunching precedente procedura guidata, si riceverà un messaggio che indica che non è supportato in Azure. Verranno esaminati come listener toocreate hello **creare un listener del gruppo di disponibilità** sezione.
    
     ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742865.png)
11. Fare clic su **Avanti**.
12. Selezione metodo di sincronizzazione dati hello desiderato toouse su hello **seleziona sincronizzazione dati iniziale** pagina e fare clic su **Avanti**. Nella maggior parte degli scenari, selezionare **Sincronizzazione dati completa**. Per altre informazioni sui metodi di sincronizzazione dei dati, vedere [Pagina Seleziona sincronizzazione dati iniziale (procedure guidate Gruppi di disponibilità AlwaysOn)](https://msdn.microsoft.com/library/hh231021.aspx).
13. Esaminare i risultati di hello sui hello **convalida** pagina. Correggere i problemi in sospeso ed eseguire nuovamente la convalida di hello se necessario. Fare clic su **Avanti**.
    
     ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742866.png)
14. Rivedere le impostazioni di hello in hello **riepilogo** pagina, quindi fare clic su **fine**.
15. Avvia il processo di provisioning Hello. Quando la procedura guidata hello viene completato correttamente, fare clic su **Chiudi** tooexit procedura guidata hello.

> [!NOTE]
> Hello Aggiungi Replica Azure crea un file di log in Users\User Name\AppData\Local\SQL Server\AddReplicaWizard. Questo file di log può essere le distribuzioni di replica di Azure utilizzati tootroubleshoot non riuscita. Se ha esito negativo hello procedura guidata, l'esecuzione di qualsiasi azione, vengano eseguito il rollback di tutte le operazioni precedenti, inclusa l'eliminazione di hello effettuato il provisioning di macchine Virtuali.
> 
> 

## <a name="create-an-availability-group-listener"></a>Creare un listener del gruppo di disponibilità
Dopo aver creato il gruppo di disponibilità di hello, creare un listener per i client tooconnect toohello repliche. I listener indirizzano in ingresso hello tooeither connessioni primaria o una replica secondaria di sola lettura. Per altre informazioni sui listener, vedere [Configurare un listener ILB per gruppi di disponibilità AlwaysOn in Azure](../classic/ps-sql-int-listener.md).

## <a name="next-steps"></a>Passaggi successivi
In hello toousing aggiunta **Aggiungi Replica Azure** tooextend tooAzure il gruppo di disponibilità AlwaysOn, è anche possibile spostare alcuni carichi di lavoro di SQL Server tooAzure completamente. tooget introduzione, vedere [Provisioning di una macchina virtuale di SQL Server in Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).

Per altri argomenti correlati toorunning SQL Server in macchine virtuali di Azure, vedere [SQL Server in macchine virtuali di Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

