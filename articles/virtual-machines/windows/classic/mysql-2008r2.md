---
title: una macchina virtuale di Azure classico aaaCreate esecuzione MySQL | Documenti Microsoft
description: Creare una macchina virtuale di Azure che esegue Windows Server 2012 R2 e hello database MySQL mediante il modello di distribuzione classica hello.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 98fa06d2-9b92-4d05-ac16-3f8e9fd4feaa
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: cynthn
ms.openlocfilehash: 2c9564955c2bab197a8e494e939ce16c0b9bb605
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-created-with-hello-classic-deployment-model-running-windows-server-2016"></a>Installare MySQL in una macchina virtuale creata con il modello di distribuzione classica hello in esecuzione Windows Server 2016
[MySQL](https://www.mysql.com) è un database SQL open source molto diffuso. In questa esercitazione illustra come hello tooinstall ed eseguire **versione community di MySQL 5.7.18** come MySQL Server in una macchina virtuale in esecuzione **Windows Server 2016**. Con altre versioni di MySQL o Windows Server, l'esperienza potrebbe essere leggermente diversa.

Per istruzioni sull'installazione di MySQL in Linux, vedere: [come tooinstall MySQL su Azure](../../linux/mysql-install.md).

> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

## <a name="create-a-virtual-machine-running-windows-server-2016"></a>Creare una macchina virtuale che esegue Windows Server 2016
Se si dispone già di una macchina virtuale in esecuzione Windows Server 2016, è possibile utilizzare questo [esercitazione](./tutorial.md) macchina virtuale di toocreate hello.

## <a name="attach-a-data-disk"></a>Collegamento di un disco dati
Dopo la creazione di macchine virtuali hello, è possibile, facoltativamente, collegare un disco dati. Aggiunta di che un disco dati è consigliato per i carichi di lavoro e tooavoid sta esaurendo lo spazio su hello unità del sistema operativo (c), che include hello del sistema operativo.

Vedere [come tooattach dati disco macchina virtuale di Windows tooa](../attach-managed-disk-portal.md) e seguire le istruzioni di hello per collegare un disco vuoto. Hello host della cache impostazione troppo**Nessuno** o **Read-only**.

## <a name="log-on-toohello-virtual-machine"></a>Accedere alla macchina virtuale toohello
Successivamente, sarà possibile [accedere alla macchina virtuale toohello](./connect-logon.md) , pertanto non è possibile installare MySQL.

## <a name="install-and-run-mysql-community-server-on-hello-virtual-machine"></a>Installare ed eseguire MySQL Community Server nella macchina virtuale hello
Seguire questi passaggi tooinstall, configurare ed eseguire una versione Community hello del MySQL Server:

> [!NOTE]
> Quando si scaricano gli elementi con Internet Explorer, è possibile impostare Internet Explorer hello **configurazione sicurezza avanzata** tooOff e semplificare il processo di download hello. Dal menu di avvio hello, fare clic su amministrazione/Server degli strumenti o locale di gestione Server, quindi fare clic su Internet Explorer **configurazione sicurezza avanzata** e impostare hello configurazione tooOff).
>
>

1. Dopo aver collegato toohello virtual machine tramite Desktop remoto, fare clic su **Internet Explorer** dalla schermata start hello.
2. Seleziona hello **strumenti** pulsante nell'angolo superiore destro di hello (icona rotellina cogged hello) e quindi fare clic su **Opzioni Internet**. Fare clic su hello **sicurezza** scheda, fare clic su hello **siti attendibili** icona, quindi fare clic su hello **siti** pulsante. Aggiungere http://*.mysql.com toohello elenco dei siti attendibili. Fare clic su **Chiudi** e quindi su **OK**.
3. In hello barra indirizzi di Internet Explorer, digitare https://dev.mysql.com/downloads/mysql/.
4. Utilizzare hello MySQL sito toolocate e scaricare hello la versione più recente del programma di installazione di MySQL per Windows hello. Quando si sceglie hello programma di installazione di MySQL, scaricare una versione hello con hello completare il set di file (ad esempio, hello mysql-installazione-community-5.7.18.0.msi con una dimensione di 352.8 MB) e salvare installer hello.
5. Programma di installazione hello ha completato il download, fare clic su **eseguire** toolaunch il programma di installazione.
6. In hello **contratto di licenza** pagina, accettare il contratto di licenza hello e fare clic su **Avanti**.
7. In hello **scelta di un tipo di programma di installazione** pagina, fare clic su tipo di installazione hello desiderato e quindi fare clic su **Avanti**. Hello seguenti passaggi si presuppone che la selezione hello di hello **solo Server** tipo di installazione.
8. Se hello **controllare requisiti** pagina consente di visualizzare, fare clic su **Execute** toolet hello installare i componenti mancanti. Seguire le istruzioni che consentono di visualizzare, ad esempio runtime C++ Redistributable hello.
9. In hello **installazione** pagina, fare clic su **Execute**. Al termine dell'installazione, fare clic su **Next**.

10. In hello **configurazione del prodotto** pagina, fare clic su **Avanti**.

11. In hello **tipo e la rete** , specificare le opzioni connettività e tipo di configurazione desiderata, inclusa la porta TCP hello, se necessario. Fare clic su **Show Advanced Options** (Mostra opzioni avanzate) e quindi su **Next** (Avanti).
    ![](./media/mysql-2008r2/MySQL_TypeNetworking.png)

12. In hello **account e ruoli** , specificare una password complessa di radice MySQL. Aggiungere altri account utente di MySQL in base alle esigenze, quindi fare clic su **Next**.

    ![](./media/mysql-2008r2/MySQL_AccountsRoles_Filled.png)
13. In hello **servizio Windows** pagina, specificare le impostazioni predefinite di toohello di modifiche per l'esecuzione di hello MySQL Server come servizio Windows in base alle esigenze e quindi fare clic su **Avanti**.

    ![](./media/mysql-2008r2/MySQL_WindowsService.png)
14. le scelte di comandi hello Hello **plug-in ed estensioni** pagina sono facoltativi. Fare clic su **Avanti** toocontinue.
15. In hello **opzioni avanzate** pagina, specificare le opzioni di toologging modifiche in base alle esigenze e quindi fare clic su **Avanti**.

    ![](./media/mysql-2008r2/MySQL_AdvOptions.png)
16. In hello **Applica configurazione Server** pagina, fare clic su **Execute**. Dopo aver completato i passaggi di configurazione di hello, fare clic su **fine**.
17. In hello **configurazione del prodotto** pagina, fare clic su **Avanti**.
18. In hello **installazione completata** pagina, fare clic su **Log di copia tooClipboard** se si desidera tooexamine in un secondo momento e quindi fare clic su **fine**.
19. Dalla schermata start hello digitare **mysql**, quindi fare clic su **Client della riga di comando di MySQL 5.7**.
20. Immettere la password radice hello specificato nel passaggio 12, e viene visualizzata con un prompt dei comandi in cui è possibile emettere comandi tooconfigure MySQL. Per informazioni dettagliate hello di comandi e sintassi, vedere [manuali di riferimento di MySQL](https://dev.mysql.com/doc/refman/5.7/en/server-configuration.html).

    ![](./media/mysql-2008r2/MySQL_CommandPrompt.png)
21. È anche possibile configurare impostazioni predefinite di configurazione server, ad esempio hello base e le directory dei dati e le unità. Per altre informazioni, vedere [6.1.2 Server Configuration Defaults](https://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html) (Impostazioni predefinite per la configurazione del server 6.1.2).

## <a name="configure-endpoints"></a>Configurare gli endpoint

Per hello MySQL servizio toobe tooclient disponibile computer hello Internet, è necessario configurare un endpoint per la porta TCP hello e creare una regola Firewall di Windows. valore di porta predefinito Hello su quali MySQL Server hello servizio è in ascolto per i client di MySQL è 3306. È possibile specificare un'altra porta, purché sia coerenza con il valore di hello fornito in hello porta hello **tipo e la rete** (passaggio 11 della procedura precedente hello).

> [!NOTE]
> Per la produzione, è consigliabile hello implicazioni di sicurezza di apportare hello MySQL Server service tooall disponibile computer su Internet hello. È possibile definire set hello di indirizzi IP di origine che sono consentiti endpoint hello toouse con un elenco di controllo di accesso (ACL). Per ulteriori informazioni, vedere [come configurare gli endpoint di tooSet tooa macchina virtuale](setup-endpoints.md).
>
>

un endpoint per il servizio MySQL Server hello tooconfigure:

1. Nel portale di Azure hello, fare clic su **macchine virtuali (classico)**, fare clic sul nome della macchina virtuale MySQL hello e quindi fare clic su **endpoint**.
2. Nella barra dei comandi di hello, fare clic su **Aggiungi**.
3. In hello **aggiungere endpoint** , digitare un nome univoco per **nome**.
4. Selezionare **TCP** come protocollo di hello.
5. Digitare il numero di porta hello, ad esempio **3306**, sia in **porta pubblica** e **porta privata**, quindi fare clic su **OK**.

## <a name="add-a-windows-firewall-rule-tooallow-mysql-traffic"></a>Aggiungere un tooallow regola Windows Firewall del traffico di MySQL
tooadd una regola Windows Firewall che consenta il traffico di MySQL da hello Internet, eseguire hello seguente comando in un _prompt dei comandi di Windows PowerShell con privilegi elevati_ nella macchina virtuale di hello MySQL server.

    New-NetFirewallRule -DisplayName "MySQL57" -Direction Inbound –Protocol TCP –LocalPort 3306 -Action Allow -Profile Public

## <a name="test-your-remote-connection"></a>Testare la connessione remota
tootest hello di in esecuzione la connessione remota toohello macchina virtuale di Azure MySQL Server del servizio, è necessario fornire il nome DNS hello del servizio cloud hello contenente hello VN.

1. Nel portale di Azure hello, fare clic su **macchine virtuali (classico)**, fare clic sul nome della macchina virtuale server MySQL hello e quindi fare clic su **Panoramica**.
2. Dal dashboard macchina virtuale hello, si noti hello **nome DNS** valore. Di seguito è fornito un esempio:

   ![](media/mysql-2008r2/MySQL_DNSName.png)
3. Da un computer locale che esegue MySQL o hello client MySQL, eseguire hello successivo comando toolog in come un utente di MySQL.

     mysql -u <yourMysqlUsername> -p -h <yourDNSname>

   Ad esempio, utilizzando hello nome utente di MySQL _dbadmin3_ hello e _testmysql.cloudapp.net_ nome DNS per la macchina virtuale hello, è possibile avviare MySQL mediante hello comando seguente:

     mysql -u dbadmin3 -p -h testmysql.cloudapp.net

## <a name="next-steps"></a>Passaggi successivi
toolearn più sull'esecuzione di MySQL, vedere hello [documentazione di MySQL](http://dev.mysql.com/doc/).
