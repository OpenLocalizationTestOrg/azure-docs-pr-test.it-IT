---
title: Desktop remoto con i ruoli Azure aaaUsing | Documenti Microsoft
description: Utilizzo di Desktop remoto con i ruoli Azure
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f5727ebe-9f57-4d7d-aff1-58761e8de8c1
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d35fd421cde8be9e3caa474db95974a54e528bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a>Utilizzo di Desktop remoto con i ruoli Azure
Tramite hello Azure SDK e Servizi Desktop remoto, è possibile accedere a ruoli di Azure e macchine virtuali ospitate da Azure. In Visual Studio è possibile configurare Servizi Desktop remoto da un progetto del servizio cloud di Azure. tooenable di Servizi Desktop remoto, è necessario creare un progetto che contiene uno o più ruoli di lavoro e quindi pubblicarlo tooAzure.

> [!IMPORTANT]
> Accedere a un ruolo di Azure solo per la risoluzione dei problemi o lo sviluppo. Salve a scopo di ogni macchina virtuale è un ruolo specifico nell'applicazione Azure, non toorun toorun altre applicazioni client. Se si desidera toouse toohost Azure una macchina virtuale che è possibile utilizzare per qualsiasi scopo, vedere l'accesso a macchine virtuali di Azure da Esplora Server.
> 
> 

## <a name="tooenable-and-use-remote-desktop-for-an-azure-role"></a>tooenable e utilizzare Desktop remoto per un ruolo di Azure
1. In Esplora soluzioni, aprire il menu di scelta rapida hello per il progetto servizio cloud e quindi scegliere **pubblica**.
   
    Hello **pubblica l'applicazione Azure** procedura guidata viene visualizzata.
   
    ![Comando per la pubblicazione di un progetto di servizio cloud](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. Nella parte inferiore di hello del **impostazioni di pubblicazione di Microsoft Azure** pagina della procedura guidata hello, seleziona hello **Abilita Desktop remoto** per la casella di controllo di tutti i ruoli. 
   
    Hello **configurazione Desktop remoto** viene visualizzata la finestra di dialogo.
3. Nella parte inferiore di hello di hello **configurazione Desktop remoto** finestra di dialogo scegliere hello **altre opzioni** pulsante. 
   
    Verrà visualizzato un elenco a discesa che consente di creare o scegliere un certificato in modo che sia possibile crittografare le informazioni sulle credenziali per la connessione tramite Desktop remoto.
4. Nell'elenco a discesa hello scegliere  **&lt;Crea >**, o sceglierne uno esistente dall'elenco di hello. 
   
    Se si sceglie un certificato esistente, ignorare hello alla procedura seguente.
   
   > [!NOTE]
   > i certificati di Hello necessari per una connessione desktop remoto sono diversi da quelli di hello utilizzato per altre operazioni di Azure. certificato di accesso remoto di Hello deve avere una chiave privata.
   > 
   > 
   
    Hello **Create Certificate** viene visualizzata la finestra di dialogo.
   
   1. Specificare un nome descrittivo per il nuovo certificato di hello e quindi scegliere hello **OK** pulsante. Hello nuovo certificato viene visualizzato nella casella di riepilogo a discesa hello.
   2. In hello **configurazione Desktop remoto** finestra di dialogo, fornire un nome utente e una password.
      
       Non è possibile usare un account esistente. Non specificare l'amministratore come nome utente hello per il nuovo account di hello.
      
      > [!NOTE]
      > Se la password di hello non soddisfa i requisiti di complessità hello, casella di testo password toohello successiva un'icona rossa. la password di Hello debba includere lettere maiuscole, lettere minuscole e i numeri o simboli.
      > 
      > 
   3. Scegliere una data di scadenza account hello e dopo che le connessioni desktop remoto verranno bloccate.
   4. Dopo aver fornito tutti hello le informazioni necessarie, scegliere hello **OK** pulsante.
      
       Diverse impostazioni che abilitano i servizi di accesso remoto vengono aggiunti i file con estensione cscfg e csdef toohello.
5. In hello **impostazioni di pubblicazione di Microsoft Azure** procedura guidata, scegliere hello **OK** quando si è pronti a toopublish il servizio cloud.
   
    Se non si è pronti toopublish, scegliere hello **Annulla** pulsante. salvataggio delle impostazioni di configurazione Hello ed è possibile pubblicare il servizio cloud in un secondo momento.

## <a name="connect-tooan-azure-role-by-using-remote-desktop"></a>Connettersi tooan ruolo Azure tramite Desktop remoto
Dopo aver pubblicato il servizio cloud in Azure, è possibile utilizzare toolog Esplora Server in macchine virtuali hello ospitata da Azure. 

1. In Esplora Server espandere hello **Azure** nodo, quindi espandere il nodo hello di un servizio cloud e uno dei relativi toodisplay ruoli un elenco di istanze.
2. Aprire il menu di scelta rapida hello per un nodo dell'istanza e quindi scegliere **connessione tramite Desktop remoto**.
   
    ![Connessione tramite Desktop remoto](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. Immettere nome utente hello e la password creati in precedenza. L'accesso alla sessione remota è stato completato.

