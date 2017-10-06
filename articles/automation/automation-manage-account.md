---
title: account di automazione di Azure aaaManage | Documenti Microsoft
description: In questo articolo viene descritto come toomanage hello configurazione dell'account di automazione, ad esempio il rinnovo del certificato, l'eliminazione e la configurazione errata.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 75e41f601a138d4e8853aa79dcbab6696a5e9fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-automation-account"></a>Gestire l'account di Automazione di Azure
A un certo punto prima che scada l'account di automazione, sarà necessario toorenew hello certificato. Se si ritiene che hello account RunAs sia stata compromessa, è possibile eliminare e ricrearlo. Questa sezione viene descritto come tooperform queste operazioni.

## <a name="self-signed-certificate-renewal"></a>Rinnovo del certificato autofirmato
il certificato autofirmato Hello creato per l'account RunAs hello scade un anno dalla data di hello di creazione. È possibile rinnovarlo in qualsiasi momento prima della scadenza. Quando si rinnovarlo, certificato valido corrente hello è conservate tooensure che tutti i runbook che vengono messe in coda fino o attivamente in esecuzione e che l'autenticazione con hello account RunAs, non sono influenzati negativamente. certificato Hello rimane valido fino alla relativa data di scadenza.

> [!NOTE]
> Se si utilizza questa opzione è stata configurata l'automazione Run As account toouse un certificato emesso da un'autorità di certificazione dell'organizzazione, certificato aziendale hello verrà sostituito da un certificato autofirmato.

hello toorenew certificati, hello seguenti:

1. Nel portale di Azure hello, aprire l'account di automazione hello.

2. In hello **Account di automazione** pannello in hello **Account proprietà** riquadro, in **impostazioni Account**selezionare **account RunAs**.

    ![Riquadro delle proprietà dell'account di Automazione](media/automation-manage-account/automation-account-properties-pane.png)
3. In hello **account RunAs** Pannello proprietà, seleziona entrambi hello eseguiti come account o hello Classic account RunAs che si desidera che il certificato hello toorenew per.

4. In hello **proprietà** pannello hello account selezionato, fare clic su **Rinnova certificato**.

    ![Rinnovare il certificato per l'account RunAs](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. Mentre viene rinnovato il certificato di hello, è possibile monitorare lo stato di avanzamento hello in **notifiche** dal menu di hello.

## <a name="delete-a-run-as-or-classic-run-as-account"></a>Eliminare un account RunAs o un account RunAs classico
Questa sezione viene descritto come toodelete e ricreare un account RunAs o classico runas. Quando si esegue questa azione, viene mantenuto hello account di automazione. Dopo aver eliminato un account RunAs o classico runas, è possibile crearlo nuovamente in hello portale di Azure.

1. Nel portale di Azure hello, aprire l'account di automazione hello.

2. In hello **account di automazione** in hello account riquadro proprietà, seleziona pannello **account RunAs**.

3. In hello **account RunAs** Pannello proprietà, selezionare entrambi hello account RunAs classico RunAs dell'account che si desidera toodelete. Quindi, nella hello **proprietà** pannello hello account selezionato, fare clic su **eliminare**.

 ![Eliminare un account RunAs](media/automation-manage-account/automation-account-delete-runas.png)

4. Durante l'eliminazione di account hello in corso, è possibile monitorare i progressi di hello in **notifiche** dal menu di hello.

5. Dopo aver eliminato l'account di hello, è possibile crearlo nuovamente su hello **account RunAs** Pannello proprietà selezionando hello opzione create **Azure Account runas**.

 ![Ricreare hello automazione account RunAs](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a>Errore di configurazione
Alcuni elementi di configurazione necessari per toofunction di account RunAs o classico runas hello correttamente potrebbe essere stati eliminati o creati in modo non corretto durante l'installazione iniziale. gli elementi di Hello includono:

* Asset del certificato
* Asset di connessione
* Account RunAs è stato rimosso dal ruolo di collaboratore hello
* Entità servizio o applicazione in Azure AD

In altre istanze di una configurazione errata e hello precedente hello account di automazione rileva hello cambia e visualizza lo stato di *incompleto* su hello **account RunAs** Pannello proprietà per hello account.

![Stato di configurazione Incompleto dell'account RunAs](media/automation-manage-account/automation-account-runas-incomplete-config.png)

Quando si seleziona account RunAs hello, hello account **proprietà** riquadro Visualizza hello seguente messaggio di errore:

![Messaggio di avviso relativo alla configurazione incompleta dell'account RunAs](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png).

Per risolvere rapidamente i problemi di account RunAs, eliminazione e ricreazione account hello.

## <a name="next-steps"></a>Passaggi successivi
* Per ulteriori informazioni sulle entità servizio, vedere troppo[oggetti applicazione e oggetti entità servizio](../active-directory/active-directory-application-objects.md).
* Per ulteriori informazioni sul controllo di accesso basato sui ruoli in automazione di Azure, vedere troppo[controllo di accesso basato sui ruoli in automazione di Azure](automation-role-based-access-control.md).
* Per ulteriori informazioni sui certificati e i servizi di Azure, vedere troppo[panoramica dei certificati per servizi Cloud di Azure](../cloud-services/cloud-services-certs-create.md).
