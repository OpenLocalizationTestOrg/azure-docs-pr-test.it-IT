---
title: aaaDeploy S/4HANA SAP o BW/4HANA in una macchina virtuale di Azure | Documenti Microsoft
description: Distribuire SAP S/4HANA o BW/4HANA in una macchina virtuale di Azure
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a>Distribuire SAP S/4HANA o BW/4HANA in Azure
In questo articolo viene descritto come toodeploy S/4HANA in Azure utilizzando hello libreria Appliance di Cloud SAP (SAP CAL) 3.0. toodeploy altre soluzioni basate su SAP HANA, ad esempio BW/4HANA, seguono hello stessi passaggi.

> [!NOTE]
Per ulteriori informazioni su hello CAL SAP, visitare toohello [SAP Cloud accessorio libreria](https://cal.sap.com/) sito Web. SAP include anche un blog sui hello [SAP Cloud accessorio libreria 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).

> [!NOTE]
Come di 29 maggio 2017, è possibile utilizzare modelli di distribuzione Azure Resource Manager hello inoltre distribuzione classica preferito meno toohello modello toodeploy hello CAL SAP. È consigliabile utilizzare il nuovo modello di distribuzione di gestione delle risorse di hello e ignorare il modello di distribuzione classica hello.

## <a name="step-by-step-process-toodeploy-hello-solution"></a>Soluzione di hello toodeploy passaggi della procedura guidata

Hello sequenza degli screenshot seguente mostra come toodeploy S/4HANA in Azure utilizzando hello CAL SAP. il processo di Hello funziona hello allo stesso modo di altre soluzioni, ad esempio BW/4HANA.

Hello **soluzioni** pagina vengono illustrati alcuni dei hello soluzioni basate su SAP HANA CAL disponibili in Azure. **SAP S/4HANA 1610 FPS01, Fully-Activated accessorio** nella riga centrale hello:

![Soluzioni SAP CAL](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a>Creare un account in hello CAL SAP
1. toosign in toohello CAL SAP per hello prima volta, utilizzare S utente SAP o altre registrate con SAP dall'utente. Definire quindi un account di SAP CAL utilizzato da dispositivi di toodeploy hello CAL SAP in Azure. Nella definizione di account hello, è necessario:

    a. Selezionare il modello di distribuzione hello in Azure (classica o gestione delle risorse).

    b. Immettere la sottoscrizione di Azure. Un account di SAP CAL può essere assegnato solo sottoscrizione tooone. Se è necessario più di una sottoscrizione, è necessario toocreate un altro account di SAP CAL.

    c. Assegnare hello SAP CAL autorizzazione toodeploy alla sottoscrizione di Azure.

    > [!NOTE]
    passaggi successivi Hello mostrano come toocreate una licenza CAL SAP account per le distribuzioni di gestione risorse. Se hai già un account di SAP CAL che è il modello di distribuzione classica toohello collegato, si *necessario* toofollow questi toocreate passaggi un nuovo account di SAP CAL. il nuovo account di SAP CAL Hello deve toodeploy nel modello di gestione risorse di hello.

2. Creare un nuovo account SAP CAL. Hello **account** pagina sono disponibili tre opzioni Azure: 

    a. **Microsoft Azure (versione classica)** è il modello di distribuzione classica hello e non è più preferito.

    b. **Microsoft Azure** è il nuovo modello di distribuzione di gestione delle risorse di hello.

    c. **Windows Azure gestito da 21Vianet** è un'opzione in Cina che utilizza il modello di distribuzione classica hello.

    Selezionare toodeploy nel modello di gestione risorse di hello, **Microsoft Azure**.

    ![Dettagli dell'account SAP CAL](./media/cal-s4h/s4h-pic-2a.png)

3. Immettere hello Azure **ID sottoscrizione** che sono disponibili nel portale di Azure hello.

   ![Account SAP CAL](./media/cal-s4h/s4h-pic3c.png)

4. tooauthorize hello CAL SAP toodeploy nella sottoscrizione di Azure hello è definito, fare clic su **Authorize**. Hello seguente pagina viene visualizzata nella scheda del browser hello:

   ![Accesso ai servizi cloud di Internet Explorer](./media/cal-s4h/s4h-pic4c.png)

5. Se più di un utente è elencato, scegliere hello account Microsoft collegato toobe hello coadministrator di hello Azure sottoscrizione selezionata. Hello seguente pagina viene visualizzata nella scheda del browser hello:

   ![Conferma dei servizi cloud di Internet Explorer](./media/cal-s4h/s4h-pic5a.png)

6. Fare clic **Accept**. Se viene concessa l'autorizzazione di hello, definizione di account di SAP CAL viene visualizzato nuovamente. Dopo un breve periodo di tempo, un messaggio di conferma che il processo di autorizzazione hello ha avuto esito positivo.

7. hello tooassign appena creati SAP CAL account tooyour utente, immettere il **ID utente** nella casella di testo a destra hello hello e fare clic su **Aggiungi**.

   ![Associazione toouser account](./media/cal-s4h/s4h-pic8a.png)

8. Fare clic su account utente di hello utilizzare toosign toohello CAL SAP, tooassociate **revisione**. 
 
9. associazione di hello toocreate tra l'utente e l'account di SAP CAL hello appena creato, fare clic su **crea**.

   ![Associazione dell'account utente tooSAP CAL](./media/cal-s4h/s4h-pic9b.png)

È stato creato un account SAP CAL in grado di:

- Utilizzare il modello di distribuzione del hello Gestione risorse.
- Distribuire i sistemi SAP nella sottoscrizione di Azure.

È ora possibile avviare toodeploy S/4HANA alla sottoscrizione di utente in Azure.

> [!NOTE]
Prima di continuare, determinare se sono disponibili quote core di Azure per macchine virtuali di serie H di Azure. In un momento hello, hello SAP CAL utilizza toodeploy H serie macchine virtuali di Azure alcune delle soluzioni basate su SAP HANA hello. È possibile tuttavia che la sottoscrizione di Azure in uso non abbia quote core per la serie H. In questo caso, potrebbe essere necessario toocontact supporto tecnico di Azure tooget una quota di almeno 16 core H serie.

> [!NOTE]
Quando si distribuisce una soluzione hello CAL SAP in Azure, si noterà che è possibile scegliere una sola area di Azure. toodeploy in aree di Azure diverso da hello uno suggeriti da hello CAL SAP, è necessario toopurchase una sottoscrizione CAL da SAP. Inoltre potrebbe essere necessario un messaggio con SAP toohave tooopen il toodeliver account abilitato CAL in aree di Azure diverso da quelli suggeriti inizialmente hello.

### <a name="deploy-a-solution"></a>Distribuire una soluzione

Consente di distribuire una soluzione da hello **soluzioni** pagina di hello CAL SAP. Hello CAL SAP dispone di due sequenze toodeploy:

- Una sequenza di base che usa uno toobe di sistema di hello toodefine, pagina distribuito
- Una sequenza avanzata, che offre opzioni specifiche per le dimensioni delle macchine virtuali 

Viene descritto come hello qui toodeployment di percorso di base.

1. In hello **dettagli Account** pagina, è necessario:

    a. Selezionare un account SAP CAL. (Utilizzare un account che sia associato toodeploy con modello di distribuzione di gestione risorse di hello).

    b. Immettere un **nome** di istanza.

    c. Selezionare un'**area** di Azure. Hello SAP CAL suggerisce una regione. Se occorre un'altra area di Azure e non si dispone di una sottoscrizione CAL SAP, è necessario tooorder una licenza CAL sottoscrizione con SAP.

    d. Immettere un master **Password** per soluzione hello di otto o nove caratteri. Hello password viene utilizzata per gli amministratori di hello dei diversi componenti hello.

   ![Modalità SAP CAL di base: creare un'istanza](./media/cal-s4h/s4h-pic10a.png)

2. Fare clic su **crea**, nella finestra di messaggio hello che viene visualizzato, fare clic su **OK**.

   ![Dimensioni delle macchine virtuali supportate da SAP CAL](./media/cal-s4h/s4h-pic10b.png)

3. In hello **chiave privata** la finestra di dialogo, fare clic su **archivio** toostore hello chiave privata hello CAL SAP. Fare clic su toouse password di protezione per la chiave privata di hello **scaricare**. 

   ![Chiave privata SAP CAL](./media/cal-s4h/s4h-pic10c.png)

4. Hello lettura CAL SAP **avviso** messaggio e fare clic su **OK**.

   ![Avviso di SAP CAL](./media/cal-s4h/s4h-pic10d.png)

    Distribuzione di hello viene ora eseguita. Dopo alcuni minuti, a seconda delle dimensioni di hello e la complessità della soluzione hello (Buongiorno CAL SAP fornisce una stima), lo stato di hello è visualizzato come attivo e pronto all'uso.

5. macchine virtuali di hello toofind raccolte con hello altre risorse associate in un gruppo di risorse, visitare il portale di Azure toohello: 

   ![Oggetti CAL SAP distribuiti nel nuovo portale di hello](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. Nel portale di SAP CAL hello, viene visualizzato lo stato di hello come **Active**. soluzione toohello tooconnect, fare clic su **Connetti**. Diverse opzioni tooconnect toohello diversi componenti vengono distribuiti all'interno di questa soluzione.

   ![Istanze di SAP CAL](./media/cal-s4h/active_solution.png)

7. Prima di poter utilizzare uno dei sistemi distribuito toohello tooconnect di hello opzioni, fare clic su **Guida introduttiva**. 

   ![Connettersi toohello istanza](./media/cal-s4h/connect_to_solution.png)

    i nomi di documentazione Hello hello utenti per ciascuno dei metodi di connettività hello. le password Hello per gli utenti vengono impostate toohello password master che è definito all'inizio di hello hello processo di distribuzione. Nella documentazione di hello, sono elencati altri utenti più funzionalità e le relative password, che è possibile utilizzare toosign in toohello distribuita del sistema. 

    Ad esempio, se si utilizza hello SAPGUI sia preinstallato nel computer Desktop remoto di Windows hello, hello sistema S/4 potrebbe essere simile al seguente:

   ![SM50 in hello preinstallato SAPGUI](./media/cal-s4h/gui_sm50.png)

    O se si utilizza hello DBACockpit, istanza hello potrebbe essere simile al seguente:

   ![SM50 in hello DBACockpit SAPGUI](./media/cal-s4h/dbacockpit.png)

In poche ore un'appliance SAP S/4 integra verrà distribuita in Azure.

Se è stata acquistata una sottoscrizione CAL SAP, SAP supporta distribuzioni tramite hello CAL SAP in Azure. coda di supporto Hello è BC-VCM-CAL.







