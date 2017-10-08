---
title: aaaDeploy SAP IDE EHP7 SP3 per 6.0 ERP SAP in Azure | Documenti Microsoft
description: Distribuire SAP IDES EHP7 SP3 per SAP ERP 6.0 in Azure
services: virtual-machines-windows
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 626c1523-1026-478f-bd8a-22c83b869231
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 09/16/2016
ms.author: hermannd
ms.openlocfilehash: 26d88c7b48a91d35602464c4f89ca7a30502c4b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a>Distribuire SAP IDES EHP7 SP3 per SAP ERP 6.0 in Azure
Questo articolo viene descritto come toodeploy un SAP sistema IDE in esecuzione con SQL Server e del sistema operativo di Windows hello in Azure tramite hello libreria Appliance di Cloud SAP (SAP CAL) 3.0. schermate di Hello illustrati hello dettagliate. toodeploy una soluzione diversa, attenersi alla stessa procedura hello.

toostart con hello CAL SAP, andare toohello [SAP Cloud accessorio libreria](https://cal.sap.com/) sito Web. SAP anche dispone di un blog sui hello new [SAP Cloud accessorio libreria 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience). 

> [!NOTE]
Come di 29 maggio 2017, è possibile utilizzare modelli di distribuzione Azure Resource Manager hello inoltre distribuzione classica preferito meno toohello modello toodeploy hello CAL SAP. È consigliabile utilizzare il nuovo modello di distribuzione di gestione delle risorse di hello e ignorare il modello di distribuzione classica hello.

Se è già stato creato un account di SAP CAL che Usa modello classico hello, *toocreate è necessario un altro account di SAP CAL*. Questo account deve tooexclusively distribuire in Azure utilizzando il modello di gestione risorse hello.

Dopo l'accesso toohello CAL SAP, prima pagina hello in genere ti toohello **soluzioni** pagina. soluzioni Hello offerte su hello CAL SAP sono costantemente, pertanto potrebbe essere tooscroll abbastanza soluzione hello toofind desiderata. soluzioni basate su Windows IDE SAP Hello evidenziato che sono disponibile esclusivamente in Azure viene illustrato il processo di distribuzione hello:

![Soluzioni SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-hello-sap-cal"></a>Creare un account in hello CAL SAP
1. toosign in toohello CAL SAP per hello prima volta, utilizzare S utente SAP o altre registrate con SAP dall'utente. Definire quindi un account di SAP CAL utilizzato da dispositivi di toodeploy hello CAL SAP in Azure. Nella definizione di account hello, è necessario:

    a. Selezionare il modello di distribuzione hello in Azure (classica o gestione delle risorse).

    b. Immettere la sottoscrizione di Azure. Un account di SAP CAL può essere assegnato solo sottoscrizione tooone. Se è necessario più di una sottoscrizione, è necessario toocreate un altro account di SAP CAL.
    
    c. Assegnare hello SAP CAL autorizzazione toodeploy alla sottoscrizione di Azure.

    > [!NOTE]
    passaggi successivi Hello mostrano come toocreate una licenza CAL SAP account per le distribuzioni di gestione risorse. Se hai già un account di SAP CAL che è il modello di distribuzione classica toohello collegato, si *necessario* toofollow questi toocreate passaggi un nuovo account di SAP CAL. il nuovo account di SAP CAL Hello deve toodeploy nel modello di gestione risorse di hello.

2. una nuova licenza CAL di SAP toocreate account hello **account** pagina vengono visualizzate due opzioni per Azure: 

    a. **Microsoft Azure (versione classica)** è il modello di distribuzione classica hello e non è più preferito.

    b. **Microsoft Azure** è il nuovo modello di distribuzione di gestione delle risorse di hello.

    ![Account SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    Selezionare toodeploy nel modello di gestione risorse di hello, **Microsoft Azure**.

    ![Account SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

3. Immettere hello Azure **ID sottoscrizione** che sono disponibili nel portale di Azure hello. 

    ![ID sottoscrizione di SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

4. tooauthorize hello CAL SAP toodeploy nella sottoscrizione di Azure hello è definito, fare clic su **Authorize**. Hello seguente pagina viene visualizzata nella scheda del browser hello:

    ![Accesso ai servizi cloud di Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

5. Se più di un utente è elencato, scegliere hello account Microsoft collegato toobe hello coadministrator di hello Azure sottoscrizione selezionata. Hello seguente pagina viene visualizzata nella scheda del browser hello:

    ![Conferma dei servizi cloud di Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

6. Fare clic **Accept**. Se viene concessa l'autorizzazione di hello, definizione di account di SAP CAL viene visualizzato nuovamente. Dopo un breve periodo di tempo, un messaggio di conferma che il processo di autorizzazione hello ha avuto esito positivo.

7. hello tooassign appena creati SAP CAL account tooyour utente, immettere il **ID utente** nella casella di testo a destra hello hello e fare clic su **Aggiungi**. 

    ![Associazione toouser account](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

8. Fare clic su account utente di hello utilizzare toosign toohello CAL SAP, tooassociate **revisione**. 

9. associazione di hello toocreate tra l'utente e l'account di SAP CAL hello appena creato, fare clic su **crea**.

    ![Associazione tooaccount dell'utente](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

È stato creato un account SAP CAL in grado di:

- Utilizzare il modello di distribuzione del hello Gestione risorse.
- Distribuire i sistemi SAP nella sottoscrizione di Azure.

> [!NOTE]
Prima di poter distribuire soluzioni SAP IDE hello basate su Windows e SQL Server, potrebbe essere necessario toosign per una sottoscrizione di SAP CAL. In caso contrario, la soluzione hello potrebbe essere visualizzato come **bloccato** nella pagina di panoramica hello.

### <a name="deploy-a-solution"></a>Distribuire una soluzione
1. Dopo aver impostato un account di SAP CAL, selezionare **hello soluzione SAP IDE su Windows e SQL Server** soluzione. Fare clic su **Crea istanza**e verificare le condizioni di utilizzo e condizioni hello. 

2. In hello **la modalità di base: Crea istanza** pagina, è necessario:

    a. Immettere un **nome** di istanza.

    b. Selezionare un'**area** di Azure. Potrebbe essere necessario un tooget sottoscrizione SAP CAL offerte più aree di Azure.

    c.  Immettere master hello **Password** per soluzione hello, come illustrato:

    ![Modalità SAP CAL di base: creare un'istanza](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

3. Fare clic su **Crea**. Dopo alcuni minuti, a seconda delle dimensioni di hello e la complessità della soluzione hello (Buongiorno CAL SAP fornisce una stima), lo stato di hello viene visualizzato come attivo e pronto all'uso: 

    ![Istanze di SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

4. gruppo di risorse toofind hello e tutti gli oggetti che sono stati creati da hello CAL SAP, visitare toohello portale di Azure. macchina virtuale Hello disponibili a partire dalla stessa istanza di nome specificato in hello SAP CAL hello.

    ![Oggetti del gruppo di risorse](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

5. Nel portale di SAP CAL hello, istanze toohello distribuito, fare clic su **Connetti**. verrà visualizzata la finestra di Hello successiva finestra popup. 

    ![Connettersi toohello istanza](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

6. Prima di poter utilizzare uno dei sistemi distribuito toohello tooconnect di hello opzioni, fare clic su **Guida introduttiva**. i nomi di documentazione Hello hello utenti per ciascuno dei metodi di connettività hello. le password Hello per gli utenti vengono impostate toohello password master che è definito all'inizio di hello hello processo di distribuzione. Nella documentazione di hello, sono elencati altri utenti più funzionalità e le relative password, che è possibile utilizzare toosign in toohello distribuita del sistema.

    ![Documentazione di benvenuto di SAP](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

In poche ore un sistema SAP IDES integro verrà distribuito in Azure.

Se è stata acquistata una sottoscrizione CAL SAP, SAP supporta distribuzioni tramite hello CAL SAP in Azure. coda di supporto Hello è BC-VCM-CAL.

