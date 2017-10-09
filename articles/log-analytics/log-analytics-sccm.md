---
title: Configuration Manager tooLog Analitica aaaConnect | Documenti Microsoft
description: Questo articolo illustra i passaggi di hello tooconnect tooLog di Configuration Manager Analitica e avviare l'analisi dei dati.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f2298bd7-18d7-4371-b24a-7f9f15f06d66
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: banders
ms.openlocfilehash: dc50ebc46020a806d99d1a3e3d0e91fd09ad2c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-configuration-manager-toolog-analytics"></a>Connettersi Analitica tooLog di Configuration Manager
È possibile connettersi a System Center Configuration Manager tooLog Analitica nei dati OMS toosync dispositivo insieme. Ciò rende disponibili in OMS i dati provenienti dalla gerarchia di Configuration Manager.

## <a name="prerequisites"></a>Prerequisiti

Log Analytics supporta System Center Configuration Manager Current Branch, versione 1606 e successive.  

## <a name="configuration-overview"></a>Panoramica della configurazione
Hello alla procedura seguente vengono riepilogate hello processo tooconnect Analitica tooLog di Configuration Manager.  

1. Nel portale di gestione Azure hello e Configuration Manager come un'applicazione Web e/o API Web di app, assicurarsi di disporre di hello client ID e la chiave privata del client dalla registrazione hello da Azure Active Directory. Vedere [utilizzare portale toocreate applicazione di Active Directory e dell'entità servizio che possono accedere alle risorse](../azure-resource-manager/resource-group-create-service-principal-portal.md) per informazioni dettagliate su come effettuare questa operazione.
2. Nel portale di gestione di Azure, hello [forniscono la gestione della configurazione (app web registrati hello) con autorizzazione tooaccess OMS](#provide-configuration-manager-with-permissions-to-oms).
3. In Configuration Manager, [aggiungere una connessione tramite connessione guidata OMS hello](#add-an-oms-connection-to-configuration-manager).
4. In Configuration Manager, [aggiornare le proprietà di connessione hello](#update-oms-connection-properties) se chiave segreta hello client o la password scade o si interrompe mai.
5. Con le informazioni dal portale OMS hello, [scaricare e installare Microsoft Monitoring Agent hello](#download-and-install-the-agent) scegliere computer hello in esecuzione sulla connessione del servizio Configuration Manager hello dal ruolo del sistema del sito. agente di Hello invia tooOMS dati di Configuration Manager.
6. In Log Analytics [importare le raccolte da Configuration Manager](#import-collections) come gruppi di computer.
7. In Log Analytics visualizzare i dati da Configuration Manager come [gruppi di computer](log-analytics-computer-groups.md).

È possibile leggere altre informazioni sulla connessione tooOMS di Configuration Manager in [sincronizzare i dati da Configuration Manager toohello Microsoft Operations Management Suite](https://technet.microsoft.com/library/mt757374.aspx).

## <a name="provide-configuration-manager-with-permissions-toooms"></a>Fornire le autorizzazioni tooOMS Configuration Manager
Hello procedura riportata di seguito fornisce hello portale di gestione di Azure con le autorizzazioni tooaccess OMS. In particolare, è necessario concedere hello *ruolo Collaboratore* toousers nel gruppo di risorse hello in ordine tooallow hello Azure Management Portal tooconnect tooOMS di Configuration Manager.

> [!NOTE]
> È necessario specificare le autorizzazioni di accesso a OMS per Configuration Manager. In caso contrario, verrà visualizzato un messaggio di errore quando si utilizza Creazione guidata di configurazione hello in Configuration Manager.
>
>

1. Aprire hello [portale di Azure](https://portal.azure.com/) e fare clic su **Sfoglia** > **Analitica Log (OMS)** blade di tooopen hello Analitica Log (OMS).  
2. In hello **Analitica Log (OMS)** pannello, fare clic su **Aggiungi** tooopen hello **area di lavoro OMS** blade.  
   ![Pannello OMS](./media/log-analytics-sccm/sccm-azure01.png)
3. In hello **area di lavoro OMS** pannello, fornire le seguenti informazioni hello e quindi fare clic su **OK**.

   * **Area di lavoro di OMS**
   * **Sottoscrizione**
   * **Gruppo di risorse**
   * **Posizione**
   * **Piano tariffario**  
     ![Pannello OMS](./media/log-analytics-sccm/sccm-azure02.png)  

     > [!NOTE]
     > esempio Hello precedente crea un nuovo gruppo di risorse. gruppo di risorse Hello è solo utilizzato tooprovide Configuration Manager con le autorizzazioni toohello OMS dell'area di lavoro in questo esempio.
     >
     >
4. Fare clic su **Sfoglia** > **gruppi di risorse** tooopen hello **gruppi di risorse** blade.
5. In hello **gruppi di risorse** pannello, fare clic su gruppo di risorse hello appena creata hello tooopen &lt;nome gruppo di risorse&gt; pannello impostazioni.  
   ![pannello impostazioni gruppo di risorse](./media/log-analytics-sccm/sccm-azure03.png)
6. In hello &lt;nome gruppo di risorse&gt; pannello impostazioni, fare clic su hello tooopen (IAM) di controllo di accesso &lt;nome gruppo di risorse&gt; pannello utenti.  
   ![pannello utenti gruppo di risorse](./media/log-analytics-sccm/sccm-azure04.png)  
7. In hello &lt;nome gruppo di risorse&gt; pannello utenti, fare clic su **Aggiungi** tooopen hello **aggiungere accesso** blade.
8. In hello **aggiungere accesso** pannello, fare clic su **selezionare un ruolo**, quindi selezionare hello **collaboratore** ruolo.  
   ![selezionare un ruolo](./media/log-analytics-sccm/sccm-azure05.png)  
9. Fare clic su **aggiungere utenti**selezionare hello utente di Configuration Manager, fare clic su **selezionare**, quindi fare clic su **OK**.  
   ![aggiungi utenti](./media/log-analytics-sccm/sccm-azure06.png)  

## <a name="add-an-oms-connection-tooconfiguration-manager"></a>Aggiungere un tooConfiguration OMS connection Manager
In ordine tooadd una connessione di OMS, l'ambiente di Configuration Manager deve avere un [punto di connessione del servizio](https://technet.microsoft.com/library/mt627781.aspx) configurato per la modalità online.

1. In hello **amministrazione** area di lavoro di Configuration Manager, selezionare **OMS Connector**. Verrà visualizzata hello **connessione guidata OMS**. Selezionare **Avanti**.
2. In hello **generale** verificare di avere eseguito hello seguenti azioni e i dettagli per ogni elemento, quindi selezionare **Avanti**.

   1. Nel portale di gestione di Azure di hello, Configuration Manager è registrato come applicazione Web e/o API Web app e che sono hello [ID client di registrazione hello](../active-directory/active-directory-integrating-applications.md).
   2. Nel portale di gestione Azure hello, è stata creata una chiave privata dell'app per hello app registrato in Azure Active Directory.  
   3. Nel portale di gestione Azure hello, app web registrati hello aver fornito con autorizzazione tooaccess OMS.  
      ![Pagina generale di creazione guidata tooOMS di connessione](./media/log-analytics-sccm/sccm-console-general01.png)
3. In hello **Azure Active Directory** schermata, configurare il tooOMS le impostazioni di connessione, fornendo il **Tenant** , **ID Client** , e **chiave privata Client**  , quindi selezionare **Avanti**.  
   ![Pagina di connessione tooOMS procedura guidata Azure Active Directory](./media/log-analytics-sccm/sccm-wizard-tenant-filled03.png)
4. Se sono state eseguite hello tutte le altre procedure correttamente, quindi hello informazioni su hello **configurazione della connessione di OMS** schermata verrà visualizzati automaticamente in questa pagina. Le informazioni per le impostazioni di connessione hello devono essere visualizzate le **sottoscrizione di Azure** , **gruppo di risorse** , e **area di lavoro di Operations Management Suite**.  
   ![Pagina di connessione tooOMS guidata OMS Connection](./media/log-analytics-sccm/sccm-wizard-configure04.png)
5. la procedura guidata Hello connette servizio OMS toohello utilizzando aver immesso le informazioni di hello. Selezionare le raccolte di dispositivi hello che desidera toosync con OMS e quindi fare clic su **Aggiungi**.  
   ![Seleziona raccolte](./media/log-analytics-sccm/sccm-wizard-add-collections05.png)
6. Verificare le impostazioni di connessione su hello **riepilogo** schermata, quindi selezionare **Avanti**. Hello **lo stato di avanzamento** schermata mostra lo stato di connessione hello, quindi deve **completa**.

> [!NOTE]
> È necessario connettersi sito di livello superiore OMS toohello nella gerarchia. Se è la connessione a un sito primario OMS tooa autonomo e quindi aggiungere un ambiente tooyour del sito di amministrazione centrale, verranno toodelete e ricreare la connessione di OMS hello nuova gerarchia hello.
>
>

Dopo aver collegato tooOMS di Configuration Manager, è possibile aggiungere o rimuovere le raccolte e visualizzare le proprietà di hello di hello OMS connection.

## <a name="update-oms-connection-properties"></a>Aggiornare le proprietà della connessione OMS
Se una chiave privata client o password mai scade o viene persa, è necessario proprietà di connessione toomanually aggiornamento hello OMS.

1. In Configuration Manager passare troppo**servizi Cloud** , quindi selezionare **OMS Connector** tooopen hello **le proprietà di connessione di OMS** pagina.
2. In questa pagina, fare clic su hello **Azure Active Directory** scheda tooview il **Tenant**, **ID Client**, **scadenza della chiave privata Client**. **Verificare** se la **chiave privata client** è scaduta.

## <a name="download-and-install-hello-agent"></a>Scaricare e installare l'agente di hello
1. Nel portale di OMS hello [file di programma di installazione agente hello Download da OMS](log-analytics-windows-agents.md#download-the-agent-setup-file-from-oms).
2. Utilizzare uno dei seguenti metodi tooinstall hello e configurare l'agente di hello in computer hello hello Configuration Manager service ruolo punto di connessione del sito del sistema:
   * [Installazione dell'agente di hello tramite il programma di installazione](log-analytics-windows-agents.md#install-the-agent-using-setup)
   * [Installazione dell'agente di hello tramite riga di comando hello](log-analytics-windows-agents.md#install-the-agent-using-the-command-line)
   * [Installazione dell'agente di hello tramite DSC in automazione di Azure](log-analytics-windows-agents.md#install-the-agent-using-dsc-in-azure-automation)

## <a name="import-collections"></a>Importare le raccolte
Dopo aver aggiunto un tooConfiguration OMS connection Manager e agente hello installato nel computer di hello in esecuzione sulla connessione del servizio Configuration Manager hello punto ruolo del sistema del sito, hello è tooimport raccolte da Configuration Manager in OMS come i gruppi di computer.

Dopo l'importazione è abilitata, le informazioni di appartenenza raccolta hello viene recuperate ogni 3 ore tookeep hello le appartenenze a raccolte corrente. È possibile scegliere l'importazione di toodisable in qualsiasi momento.

1. Nel portale OMS hello, fare clic su **impostazioni**.
2. Fare clic su hello **gruppi di Computer** scheda e quindi fare clic su hello **SCCM** scheda.
3. Selezionare **Importa appartenenze alla raccolta di Configuration Manager** e fare clic su **Salva**.  
   ![Gruppi di computer - Scheda SCCM](./media/log-analytics-sccm/sccm-computer-groups01.png)

## <a name="view-data-from-configuration-manager"></a>Visualizzare i dati da Configuration Manager
Dopo aver aggiunto un tooConfiguration OMS connection Manager e installare l'agente hello in computer hello hello Configuration Manager service ruolo punto di connessione del sito del sistema, i dati dall'agente hello viene inviati tooOMS. In OMS, le raccolte di Configuration Manager appaiono come [gruppi di computer](log-analytics-computer-groups.md). È possibile visualizzare i gruppi di hello da hello **Configuration Manager** pagina **gruppi di Computer** in **impostazioni**.

Dopo aver hello raccolte vengono importate, è possibile visualizzare il numero di computer con appartenenze a raccolte è stato rilevato. È inoltre possibile visualizzare il numero di hello di raccolte che sono stati importati.

![Gruppi di computer - Scheda SCCM](./media/log-analytics-sccm/sccm-computer-groups02.png)

Quando si fa clic su dei due, verrà visualizzata la ricerca, visualizzazione di tutti di hello importato gruppi o tutti i computer appartenenti al gruppo tooeach. Usando [Ricerca Log](log-analytics-log-searches.md) è possibile avviare un'analisi approfondita dei dati di Configuration Manager.

## <a name="next-steps"></a>Passaggi successivi
* Utilizzare [ricerca nei Log](log-analytics-log-searches.md) tooview informazioni dettagliate sui dati di Configuration Manager.
