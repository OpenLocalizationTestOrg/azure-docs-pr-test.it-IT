---
title: aaaHow tooretain un indirizzo IP virtuale costante per un servizio cloud di Azure | Documenti Microsoft
description: Informazioni su come tooensure che hello indirizzo IP virtuale (VIP) del servizio cloud di Azure non viene modificato.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4a58e2c6-7a79-4051-8a2c-99182ff8b881
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 9e27121797ffb61517b8d2c2661ec44ff7298968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="retain-a-constant-virtual-ip-address-for-an-azure-cloud-service"></a>Mantenere un indirizzo IP virtuale costante per un servizio cloud di Azure
Quando si aggiorna un servizio cloud che è ospitato in Azure, potrebbe essere necessario tooensure che non modifica l'indirizzo IP virtuale (VIP) di hello del servizio hello. Molti servizi di gestione di dominio usano hello sistema DNS (Domain Name) per la registrazione di nomi di dominio. DNS funziona solo se hello VIP rimane hello stesso. È possibile utilizzare hello **pubblicazione guidata** in tooensure strumenti di Azure che hello VIP del servizio cloud non cambia quando si aggiorna. Per ulteriori informazioni sulla gestione dei domini DNS toouse per i servizi cloud, vedere [configurazione di un nome di dominio personalizzato per un servizio cloud di Azure](cloud-services/cloud-services-custom-domain-name.md).

## <a name="publish-a-cloud-service-without-changing-its-vip"></a>Pubblicare un servizio cloud senza modifica dell'indirizzo VIP
Hello VIP di un servizio cloud viene allocato quando viene distribuito per primo è tooAzure in un ambiente specifico, ad esempio ambiente di produzione hello. modifiche di Hello VIP solo se si elimina la distribuzione di hello in modo esplicito o distribuzione di hello viene eliminata in modo implicito dalla distribuzione hello aggiornano del processo. indirizzo VIP hello tooretain, non è necessario eliminare la distribuzione ed è necessario assicurarsi che Visual Studio non viene eliminato automaticamente la distribuzione. 

È possibile specificare le impostazioni di distribuzione in hello **pubblicazione guidata**, che supporta diverse opzioni di distribuzione. È possibile specificare una nuova distribuzione o una distribuzione di aggiornamento, che può essere incrementale o simultanea. Entrambi i tipi di distribuzione di aggiornamento mantengono hello VIP. Per definizioni di questi diversi tipi di distribuzione, vedere [Procedura guidata Pubblica l'applicazione Azure](vs-azure-tools-publish-azure-application-wizard.md). Inoltre, è possibile controllare se la distribuzione precedente hello di un servizio cloud viene eliminata se si verifica un errore. Se tale opzione non impostate correttamente, hello VIP potrebbe cambiare in modo imprevisto.

## <a name="update-a-cloud-service-without-changing-its-vip"></a>Aggiornare un servizio cloud senza modifica dell'indirizzo VIP
1. Creare o aprire un progetto del servizio cloud di Azure in Visual Studio. 

2. In **Esplora**, progetto hello pulsante destro del mouse. Scegliere dal menu di scelta rapida di hello **pubblica**.

    ![Menu Pubblica](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/solution-explorer-publish-menu.png)

3. In hello **pubblica l'applicazione Azure** della finestra di dialogo selezionare hello toowhich di sottoscrizione di Azure si desidera toodeploy. Effettuare l'accesso se necessario, quindi selezionare **Avanti**.

    ![Pagina di accesso Pubblica applicazione Azure](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-signin.png)

4. In hello **impostazioni comuni** scheda, verificare che il nome di hello del toowhich di servizio cloud hello si distribuisce, hello **ambiente**, hello **configurazione della Build**, hello e **Configurazione del servizio** siano tutti corretti.

    ![Scheda delle impostazioni comuni di Pubblica applicazione Azure](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-common-settings.png)

5. In hello **impostazioni avanzate** verificare tale hello **etichetta distribuzione** hello e **account di archiviazione** siano corretti. Verificare che hello **Elimina la distribuzione in caso di errore** casella di controllo è deselezionata e verificare che hello **aggiornamento distribuzione** casella di controllo è selezionata. Per cancellare hello **Elimina la distribuzione in caso di errore** casella di controllo, assicurarsi che il VIP non viene perso se si verifica un errore durante la distribuzione. Selezionando hello **aggiornamento distribuzione** casella di controllo, assicurarsi che la distribuzione non verrà eliminata e il VIP non viene perso quando l'applicazione viene ripubblicata. 

    ![Scheda delle impostazioni avanzate di Pubblica applicazione Azure](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-advanced-settings.png)

6. toofurther specificare la modalità di hello ruoli toobe aggiornato, selezionare **impostazioni** Avanti troppo**aggiornamento distribuzione**. Selezionare **Aggiornamento incrementale** o **Simultaneous update** (Aggiornamento simultaneo) e scegliere **OK**. Scegliere **aggiornamento incrementale** tooupdate ogni istanza dell'applicazione, uno dopo l'altro, in modo che hello applicazione è sempre disponibile. Scegliere **aggiornamento simultaneo** tooupdate tutte le istanze dell'applicazione hello contemporaneamente. L'aggiornamento simultaneo è più veloce, ma il servizio potrebbe non essere disponibile durante il processo di aggiornamento hello. Al termine dell'operazione, scegliere **Avanti**.

    ![Pagina delle impostazioni di distribuzione di Pubblica applicazione Azure](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-deployment-update-settings.png)

7. In hello **pubblica l'applicazione Azure** nella finestra di dialogo **Avanti** finché hello **riepilogo** viene visualizzata la pagina. Verificare le impostazioni e quindi selezionare **Pubblica**.
   
    ![Pagina di riepilogo di Pubblica applicazione Azure](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-summary.png)

## <a name="next-steps"></a>Passaggi successivi
- [Utilizzando Visual Studio pubblicazione Azure guidata applicazione hello](vs-azure-tools-publish-azure-application-wizard.md)

