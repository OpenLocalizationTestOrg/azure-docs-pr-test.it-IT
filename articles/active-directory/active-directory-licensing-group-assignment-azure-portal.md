---
title: gruppo di tooa aaaAssign licenze in Azure Active Directory | Documenti Microsoft
description: Come tooassign licenze toousers tramite Gestione licenze di Azure Active Directory di gruppo
services: active-directory
keywords: Licenze di Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 148fe1bdd6c7f477a00c1f76bd8fa7d29c7b1f2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="assign-licenses-toousers-by-group-membership-in-azure-active-directory"></a>Assegnare licenze toousers tramite l'appartenenza di gruppo in Azure Active Directory

In questo articolo viene illustrato tramite l'assegnazione categoria tooa licenze degli utenti in Azure Active Directory (Azure AD) e quindi verificare che si è concesso in licenza in modo corretto.

In questo esempio, i tenant hello contiene un gruppo di sicurezza denominato **reparto risorse Umane**. Questo gruppo include tutti i membri del reparto risorse umane hello (circa 1.000 utenti). Si desidera intero reparto toohello licenze tooassign Office 365 Enterprise E3. Hello Yammer Enterprise service inclusa nel prodotto hello deve essere temporaneamente disabilitata fino al reparto hello toostart pronto utilizzarlo. È anche opportuno toodeploy mobilità aziendale + sicurezza licenze toohello nello stesso gruppo di utenti.

> [!NOTE]
> Alcuni servizi Microsoft non sono disponibili in tutte le posizioni. Prima che può essere assegnata una licenza utente tooa, amministratore di hello ha proprietà location di utilizzo hello toospecify utente hello.

> Per l'assegnazione del gruppo di licenze, tutti gli utenti senza specificata una località di utilizzo erediterà percorso hello della directory di hello. Se sono presenti utenti in più posizioni, è consigliabile impostare sempre la località di utilizzo come parte del flusso di creazione utente in Azure Active Directory (ad esempio, tramite configurazione di AAD Connect) - che garantirà il risultato di hello dell'assegnazione delle licenze è sempre corretto e gli utenti non ricevono servizi in posizioni che non sono consentiti.

## <a name="step-1-assign-hello-required-licenses"></a>Passaggio 1: Assegnare le licenze necessarie hello

1. Accedi toohello [ **portale di Azure** ](https://portal.azure.com) con un account amministratore. licenze toomanage, account hello devono essere un amministratore dell'account utente o ruolo amministratore globale.

2. Selezionare **più servizi** in hello riquadro di spostamento a sinistra e quindi selezionare **Azure Active Directory**. È possibile aggiungere questo tooFavorites pannello o aggiungerlo toohello dashboard del portale.

3. In hello **Azure Active Directory** pannello seleziona **licenze**. Verrà aperto un pannello in cui è possibile visualizzare e gestire tutti i prodotti multilicenza nel tenant di hello.

4. In **tutti i prodotti**, selezionare sia Office 365 Enterprise E3 ed Enterprise Mobility + Security selezionando i nomi dei prodotti hello. assegnazione di hello toostart, seleziona **assegnare** nella parte superiore di hello del pannello hello.

   ![Tutti i prodotti, assegnare una licenza](media/active-directory-licensing-group-assignment-azure-portal/all-products-assign.png)

5. In hello **assegnare licenze** pannello, fare clic su **utenti e gruppi** tooopen hello **utenti e gruppi** blade. Cercare il nome del gruppo di hello *reparto risorse Umane*, selezionare il gruppo di hello e quindi essere tooconfirm che facendo clic su **selezionare** nella parte inferiore di hello del pannello hello.

   ![Selezionare un gruppo](media/active-directory-licensing-group-assignment-azure-portal/select-a-group.png)

6. In hello **assegnare licenze** pannello, fare clic su **opzioni di assegnazione (facoltativo)**, che consente di visualizzare tutti i piani di servizio incluso in hello due prodotti che è selezionate in precedenza. Trovare **Enterprise Yammer** e trasformarlo **Off** toodisable che dalla licenza del prodotto hello del servizio. Confermare facendo **OK** in fondo hello **opzioni assegnazione**.

   ![Opzioni di assegnazione](media/active-directory-licensing-group-assignment-azure-portal/assignment-options.png)

7. assegnazione di hello toocomplete, su hello **assegnare licenze** pannello, fare clic su **assegnare** nella parte inferiore di hello del pannello hello.

8. Viene visualizzata una notifica nell'angolo superiore destro hello che mostra lo stato di hello e il risultato del processo di hello. Se gruppo toohello di hello assegnazione non è stato possibile completare (ad esempio, a causa di licenze già esistente nel gruppo hello), fare clic su dettagli di tooview hello notifica di errore hello.

Ora è stato specificato un modello di licenza per il gruppo di reparto risorse Umane hello. Un processo in background in Azure AD è stato avviato tooprocess tutti i membri esistenti di tale gruppo. Questa operazione iniziale potrebbe richiedere del tempo, a seconda delle dimensioni correnti di hello del gruppo di hello. Nel passaggio successivo hello, si verrà descrivono come tooverify tale hello processo è stato completato e determinare se ulteriore attenzione è obbligatorio tooresolve problemi.

> [!NOTE]
> È possibile avviare hello stessa assegnazione da un percorso alternativo: **utenti e gruppi** in Azure AD. Andare troppo**Azure Active Directory** > **utenti e gruppi** > **tutti i gruppi di**. Quindi trovare il gruppo di hello, selezionarla e andare toohello **licenze** hello scheda **assegnare** pulsante sopra pannello hello apre il pannello di assegnazione di licenza hello.

## <a name="step-2-verify-that-hello-initial-assignment-has-finished"></a>Passaggio 2: Verificare che l'assegnazione iniziale hello è terminata

1. Andare troppo**Azure Active Directory** > **utenti e gruppi** > **tutti i gruppi di**. Quindi trovare hello **reparto risorse Umane** gruppo che sono state assegnate licenze.

2. In hello **reparto risorse Umane** blade di gruppo, selezionare **licenze**. Ciò consente di verificare rapidamente se licenze completamente assegnate toousers e se sono presenti errori che è necessario toolook in. Hello le seguenti informazioni sono disponibile:

   - Elenco delle licenze dei prodotti che sono attualmente assegnati toohello gruppo. Selezionare una voce tooshow hello servizi specifici che sono state abilitate e toomake cambia.

   - Stato hello più recente licenza che sono state apportate modifiche toohello gruppo (se vengono elaborate le modifiche di hello o se il completamento dell'elaborazione per tutti i membri utente).

   - Informazioni sugli utenti che sono in stato di errore perché non possono essere assegnate licenze toothem.

   ![Opzioni di assegnazione](media/active-directory-licensing-group-assignment-azure-portal/assignment-errors.png)

3. Per informazioni più dettagliate sull'elaborazione delle licenze, vedere **Azure Active Directory** > **Utenti e gruppi** > *nome gruppo* > **Log di controllo**. Si noti hello le attività seguenti:

   - Attività: **avviare l'applicazione di gruppo basato su licenza toousers**. Questo viene registrato quando il sistema hello preleva hello modifiche di assegnazione delle licenze nel gruppo hello e avvia l'applicazione tooall membri di un utente. Contiene informazioni sulla modifica apportata hello.

   - Attività: **terminare l'applicazione di gruppo basato su licenza toousers**. Viene registrata al termine dell'elaborazione di tutti gli utenti nel gruppo hello sistema hello. Contiene un riepilogo di quanti utenti sono stati elaborati correttamente e il numero di utenti a cui non è stato possibile assegnare le licenze di gruppo.

   [Leggere questa sezione](./active-directory-licensing-group-advanced.md#use-audit-logs-to-monitor-group-based-licensing-activity) toolearn informazioni su come i log di controllo possono essere utilizzato tooanalyze apportate da in base al gruppo di licenze.

## <a name="step-3-check-for-license-problems-and-resolve-them"></a>Passaggio 3: Controllare i problemi relativi alle licenze e risolverli

1. Andare troppo**Azure Active Directory** > **utenti e gruppi** > **tutti i gruppi di**e trovare hello **reparto risorse Umane**gruppo che sono state assegnate licenze.
2. In hello **reparto risorse Umane** blade di gruppo, selezionare **licenze**. notifica di Hello sopra pannello hello indica che sono presenti 10 utenti che non possono essere assegnate al licenze. Facendo clic su di essa viene aperto un elenco di tutti gli utenti che presentano un errore di licenza per questo gruppo.
3. Hello **Impossibile assegnazioni** colonna indica che non possono essere assegnate agli utenti di toohello entrambe le licenze. Hello **primi motivo dell'errore** colonna contiene causa hello dell'errore di hello. In questo caso si tratta di **Piani di servizio in conflitto**.

   ![N. assegnazioni con errori](media/active-directory-licensing-group-assignment-azure-portal/failed-assignments.png)

4. Selezionare un hello tooopen utente **licenze** blade. Questo pannello Mostra tutte le licenze attualmente assegnate toohello utente. In questo esempio hello utente dispone di licenza di Office 365 Enterprise E1 hello che è stata ereditata da hello **gli utenti** gruppo. È in conflitto con licenza hello E3 che hello tooapply sistema ha tentato di hello **reparto risorse Umane** gruppo. Di conseguenza, nessuna delle licenze hello da tale gruppo è stata assegnata toohello utente.

   ![Visualizzare le licenze per un utente](media/active-directory-licensing-group-assignment-azure-portal/user-license-view.png)

5. toosolve questo conflitto, Rimuovi utente hello hello **gli utenti** gruppo. Dopo che Azure AD elaborato modifica hello, hello **reparto risorse Umane** correttamente assegnazione delle licenze.

   ![Licenza assegnata correttamente](media/active-directory-licensing-group-assignment-azure-portal/license-correctly-assigned.png)

## <a name="next-steps"></a>Passaggi successivi

toolearn ulteriori informazioni su funzionalità hello impostato per la gestione delle licenze tramite i gruppi, vedere hello seguenti articoli:

* [Che cosa sono le licenze basate sui gruppi in Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
* [Identificazione e risoluzione dei problemi relativi alle licenze per un gruppo in Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Come singoli toomigrate concesso in licenza agli utenti in base toogroup licenze in Azure Active Directory](active-directory-licensing-group-migration-azure-portal.md)
* [Scenari aggiuntivi relativi alle licenze basate sui gruppi in Azure Active Directory](active-directory-licensing-group-advanced.md)
