---
title: toomigrate aaaHow tooa i singoli utenti con licenza di gruppo in Azure Active Directory | Documenti Microsoft
description: Come tooswitch dal singolo utente licenze licenze basate su toogroup tramite Azure Active Directory
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
ms.openlocfilehash: 25e5c760b7e632ba71edde10d937fe580aa6ed35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-licensed-users-tooa-group-for-licensing-in-azure-active-directory"></a>Come tooadd concesso in licenza gruppo tooa utenti per le licenze in Azure Active Directory

È possibile toousers licenze distribuite esistente in organizzazioni di hello tramite "assegnazione diretta"; vale a dire usando gli script di PowerShell o altre licenze utente tooassign di strumenti. Se si desidera utilizzare in base al gruppo di licenze toomanage licenze nell'organizzazione toostart, occorre una migrazione piano tooseamlessly sostituire soluzioni esistenti con le licenze basate su gruppo.

tookeep cosa più importante di Hello presente è che è consigliabile evitare una situazione in cui la migrazione licenze basate su toogroup gli utenti saranno in perdere temporaneamente le licenze attualmente assegnate. Qualsiasi processo che può comportare la rimozione delle licenze deve essere evitato rischio hello tooremove di perdere l'accesso tooservices e i relativi dati.

## <a name="recommended-migration-process"></a>Processo di migrazione consigliato

1. L'automazione esistente, ad esempio PowerShell, gestisce l'assegnazione di licenze agli utenti e la loro rimozione. Questo processo deve rimanere in esecuzione.

2. Creare un nuovo gruppo di gestione delle licenze (o decidere quali esistente gruppi toouse) e assicurarsi che tutti i necessari agli utenti vengono aggiunti come membri.

3. Assegnare le licenze di hello necessario gruppi toothose; l'obiettivo è quello tooreflect hello stesso in licenza, l'automazione esistente (ad esempio, PowerShell) l'applicazione toothose utenti.

4. Verificare che le licenze siano state applicate tooall utenti in tali gruppi. Questo può essere eseguito controllando lo stato di elaborazione hello in ogni gruppo e controllando i log di controllo.

  - È possibile eseguire un controllo a campione su singoli utenti esaminandone i dettagli della licenza. Verrà visualizzato che essi hanno hello stesso licenze assegnate "direttamente" e "ereditata" dai gruppi.

  - È possibile eseguire uno script di PowerShell troppo[verificare la modalità di assegnazione delle licenze toousers](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).

  - Quando hello licenza del prodotto stesso viene assegnata toohello utente sia direttamente che tramite un gruppo, viene utilizzata solo una licenza utente hello. Di conseguenza non sono licenze aggiuntive migrazione tooperform obbligatorio.

5. Assicurarsi che non ci siano assegnazioni di licenze non riuscite verificando l'assenza di utenti in stato di errore in ogni gruppo. Per altre informazioni, vedere [Identificazione e risoluzione dei problemi relativi alle licenze per un gruppo in Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)

6. Provare a rimuovere assegnazioni diretto hello originale. è possibile toodo, gradualmente in "onde" toomonitor hello innanzitutto risultato in un sottoinsieme di utenti.

  È possibile lasciare hello originale assegnazioni dirette sugli utenti, ma quando gli utenti di hello lasciare i relativi gruppi di licenza ancora manterrà licenza hello originale, probabilmente non si desidera.

## <a name="an-example"></a>Esempio

Si consideri ad esempio un'organizzazione con 1.000 utenti. Tutti gli utenti devono avere licenze di Enterprise Mobility + Security (EMS). 200 utenti in hello reparto finanziario e richiedono licenze di Office 365 Enterprise E3. Uno script di PowerShell, in esecuzione in locale, aggiunge e rimuove le licenze dagli utenti man mano che vengono aggiunti e rimossi. È necessario creare script di hello tooreplace con licenze basate su gruppo in modo hanno le licenze gestite automaticamente da Azure AD.

Ecco il processo di migrazione hello Impossibile sono simili a:

1. Utilizzando hello Azure assegna portale hello EMS licenza toohello **tutti gli utenti** gruppo in Azure AD. Assegnare hello E3 licenza toohello **reparto finanziario** gruppo che contiene tutti gli utenti di hello necessario.

2. Per ogni gruppo, assicurarsi che l'assegnazione della licenza sia stata completata per tutti gli utenti. Pannello toohello passare per ogni gruppo, seleziona **licenze**e controllare lo stato di elaborazione hello nella parte superiore di hello di hello **licenze** blade.

  - Cerca per tooconfirm "modifiche più recenti di licenza sono state applicate tooall utenti" completata.

  - Nella parte superiore del pannello cercare una notifica relativa a eventuali utenti per i quali l'assegnazione della licenza non è riuscita. È possibile che il numero di licenze non sia sufficiente per tutti gli utenti. È anche possibile che alcuni utenti abbiano SKU di licenza in conflitto che impediscono loro di ereditare le licenze di gruppo.

3. Campione controllare alcuni tooverify gli utenti che hanno entrambe hello diretto e licenze di gruppo applicate. Pannello toohello passare per un utente, selezionare **licenze**ed esaminare lo stato di hello di licenze.

  - Si tratta dello stato utente hello previsto durante la migrazione:

      ![Stato previsto per l'utente](media/active-directory-licensing-group-migration-azure-portal/expected-user-state.png)

  Questo conferma che l'utente hello è licenze dirette ed ereditate. Risultano assegnate le licenze sia per **EMS** che per **E3**.

  - Selezionare ogni dettagli tooshow licenza sui servizi hello abilitato. Può essere utilizzato toocheck se hello diretto e abilitare le licenze gruppo esattamente hello stessi piani di servizio per l'utente hello.

      ![Verificare i piani di servizio](media/active-directory-licensing-group-migration-azure-portal/check-service-plans.png)

4. Dopo aver confermato che le licenze dirette e quelle di gruppo sono equivalenti, è possibile iniziare a rimuovere le licenze dirette dagli utenti. È possibile testare questa rimuovendole per i singoli utenti nel portale di hello ed eseguire quindi toohave gli script di automazione che li rimosso in blocco. Di seguito è riportato un esempio di hello stesso utente con licenze diretto hello rimossi tramite il portale di hello. Si noti che lo stato di licenza hello rimane invariato, ma è più visualizzato assegnazioni dirette.

  ![Licenze dirette rimosse](media/active-directory-licensing-group-migration-azure-portal/direct-licenses-removed.png)


## <a name="next-steps"></a>Passaggi successivi

ulteriori informazioni sugli altri scenari per la gestione delle licenze tramite i gruppi, leggere toolearn

* [L'assegnazione gruppo di licenze tooa in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [Che cosa sono le licenze basate sui gruppi in Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
* [Identificazione e risoluzione dei problemi relativi alle licenze per un gruppo in Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Scenari aggiuntivi relativi alle licenze basate sui gruppi in Azure Active Directory](active-directory-licensing-group-advanced.md)
