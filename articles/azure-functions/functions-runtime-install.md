---
title: Funzioni di Runtime Installation aaaAzure | Documenti Microsoft
description: Come tooInstall hello Azure funzioni di Runtime
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 67c6d10b5c0ac43e880d29cff0ae7b099f82bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-functions-runtime-preview"></a>Installare l'anteprima del Runtime di Azure funzioni hello

Se si desidera anteprima di Azure funzioni Runtime hello tooinstall, è necessario seguire questi passaggi:

1. Verificare che il computer passa i requisiti minimi di hello
1. Scaricare hello [programma di installazione di Azure funzioni Runtime Preview](https://aka.ms/azafr). 
1. Installare l'anteprima di Azure funzioni Runtime hello
1. Configurazione di hello completa dell'anteprima di Azure funzioni Runtime hello

## <a name="prerequisites"></a>Prerequisiti

Prima di installare l'anteprima di Azure funzioni Runtime hello, è necessario disporre delle seguenti hello:

1. Un computer che esegue Microsoft Windows Server 2016 o Microsoft Windows 10 Creators Update (Professional o Enterprise Edition).
1. Un'istanza di SQL Server in esecuzione all'interno della rete.  L'edizione minima richiesta è SQL Server Express.

## <a name="install-hello-azure-functions-runtime-preview"></a>Installare l'anteprima del Runtime di Azure funzioni hello

il programma di installazione di Hello Azure funzioni Runtime preview semplificato installazione hello di anteprima di Azure funzioni Runtime hello gestione e i ruoli di lavoro.  È possibile tooinstall hello gestione e il ruolo di lavoro su hello nello stesso computer.  Tuttavia, quando si aggiungono altre funzioni, è necessario distribuire più ruoli di lavoro su computer aggiuntivi toobe in grado di tooscale delle funzioni in più thread di lavoro.

## <a name="install-hello-management-and-worker-role-on-hello-same-machine"></a>Installare Gestione hello e ruolo di lavoro in hello nello stesso computer

1. Eseguire installazione di anteprima di Azure funzioni Runtime hello.

    ![Programma di installazione dell'anteprima del runtime di Funzioni di Azure][1]

1. **Fare clic su Avanti** avanzare oltre hello prima fase del programma di installazione hello
1. Dopo avere letto le condizioni di hello di hello **EULA**, **hello casella di controllo** termini hello tooaccept e **fare clic su Avanti** tooadvance.
1. Ora selezionare hello ruoli si desidera tooinstall su questo computer **ruolo di gestione delle funzioni** e/o **il ruolo di lavoro funzioni** e **fare clic su Avanti**

    ![Programma di installazione dell'anteprima del runtime di Funzioni di Azure - Selezione del ruolo][3]

    > [!NOTE]
    > È possibile installare hello **il ruolo di lavoro funzioni** in molti altri toodo macchine in tal caso, seguire queste istruzioni e selezionare solo **il ruolo di lavoro funzioni** nel programma di installazione hello.

1. **Fare clic su Avanti** toohave hello **il programma di installazione di Azure funzioni Runtime** installare nel computer.
1. Dopo l'installazione completa di hello avvierà hello **dello strumento di configurazione di Runtime di Azure funzioni**.

    ![Programma di installazione dell'anteprima del runtime di Funzioni di Azure - Completato][5]

    > [!NOTE]
    > Se si sta installando in **Windows 10** hello e **contenitore** funzionalità non è stata precedentemente abilitata, hello **Azure funzioni Runtime** programma di installazione richiederà tooreboot installare il hello toocomplete macchina.

## <a name="configure-hello-azure-functions-runtime"></a>Configurare hello Azure funzioni di Runtime

toocomplete hello Azure funzioni Runtime installazione è necessario completare la configurazione hello.

1. Hello **strumento di configurazione di Azure funzioni Runtime** Mostra quali ruoli sono installati nel computer.

    ![Anteprima del runtime di Funzioni di Azure - Strumento di configurazione][6]

1. Fare clic su hello **Database** , immettere hello **dettagli di connessione per l'istanza di SQL Server** e **fare clic su Applica**.  Questa operazione è necessaria in ordine toohello Azure funzioni Runtime toocreate un hello toosupport database Runtime.
    
    ![Anteprima del runtime di Funzioni di Azure - Configurazione del database][7]

1. Fare clic su hello **credenziali** scheda.  In questa schermata è necessario creare due nuove credenziali per l'uso con una condivisione file per l'hosting di tutte le funzioni di Azure.  **Specificare nome utente e Password** combinazioni per hello **proprietario condivisione File** e per hello **utente condivisione File** e fare clic su **applica**.

    ![Anteprima del runtime di Funzioni di Azure - Credenziali][8]

1. Fare clic su hello **condivisione File** scheda.  In questa schermata è necessario specificare i dettagli di hello di hello **percorso di condivisione File**.  È possibile creare la condivisione file o usare una condivisione file esistente e fare clic su **Applica**.  Se si seleziona un nuovo percorso di condivisione File, è necessario specificare una directory per l'utilizzo da hello Azure funzioni di Runtime.
    
    ![Anteprima del runtime di Funzioni di Azure - Condivisione file][9]

1. Fare clic su hello **IIS** scheda.  Questa scheda Mostra i dettagli di hello di siti Web di hello in IIS che hello Azure funzioni Runtime installazione creeranno.  **Fare clic su Applica** toocomplete.

    ![Anteprima del runtime di Funzioni di Azure - IIS][10]

1. Fare clic su hello **servizi** scheda.  Questa scheda Mostra stato hello dei servizi di hello nell'installazione di Runtime di funzioni di Azure.  Se dopo hello configurazione iniziale **servizio di attivazione di Azure funzioni Host** non è in esecuzione fare clic su **avvio del servizio**

    ![Anteprima del runtime di Funzioni di Azure - Configurazione completata][11]

1. Passare infine toohello **portale di Azure funzioni Runtime** come`https://<machinename>/`

    ![Anteprima del runtime di Funzioni di Azure - Portale][12]


<!--Image references-->
[1]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer1.png
[2]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer2-EULA.png
[3]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer3-ChooseRoles.png
[4]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer4-Install.png
[5]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer5-InstallComplete.png
[6]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration1.png
[7]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration2_SQL.png
[8]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration3_Credentials.png
[9]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration4_Fileshare.png
[10]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration5_IIS.png
[11]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration6_Services.png
[12]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal.png