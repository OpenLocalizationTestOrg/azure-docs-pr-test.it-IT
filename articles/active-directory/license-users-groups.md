---
title: gli utenti aaaLicense in Azure Active Directory | Documenti Microsoft
description: Informazioni su come toolicense se stessi e per gli utenti in Azure Active Directory.
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: ae0bc030fa02b79d1dd01ca961b4e96e6b9c470d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-license-users-in-azure-active-directory"></a>Guida introduttiva: Assegnare licenze a utenti in Azure Active Directory
I servizi di Azure AD basati su licenza funzionano attivando una sottoscrizione di Azure Active Directory (Azure AD) nel tenant di Azure. Dopo la sottoscrizione di hello è attiva, funzionalità del servizio gestiti dagli amministratori di Azure AD e utilizzati dagli utenti con licenza. All'acquisto di Enterprise Mobility + Security, Azure AD Premium o Azure AD Basic, il tenant verrà aggiornato con una sottoscrizione di hello, incluso il periodo di validità e prepagato licenze. Le informazioni di sottoscrizione, tra cui hello numero di licenze assegnate o disponibile, sono disponibile tramite hello Azure portale in **Azure Active Directory** dall'apertura hello **licenze** riquadro. Hello **licenze** pannello anche è hello toomanage sul posto migliore le assegnazioni delle licenze.

Anche se ottenere una sottoscrizione è che tutto è necessario tooconfigure a pagamento di funzionalità, è ancora necessario assegnare licenze utente per Active Directory di Azure a pagamento le funzionalità a pagamento. Agli utenti che devono accedere a una funzionalità a pagamento di Azure AD, o che vengono gestiti tramite questa funzionalità, deve essere assegnata una licenza. Un'assegnazione di licenza consiste nell'associazione di un utente a un servizio acquistato, ad esempio Azure AD Premium o Basic oppure Enterprise Mobility + Security.

È possibile utilizzare [assegnazione delle licenze in base al gruppo](active-directory-licensing-whatis-azure-portal.md) tooset le regole come illustrato di seguito hello:
* Tutti gli utenti nella directory ottengono automaticamente una licenza
* Tutti gli utenti con titolo appropriato hello Ottiene una licenza
* È possibile delegare hello decisione tooother responsabili dell'organizzazione hello (tramite [gruppi self-service](active-directory-accessmanagement-self-service-group-management.md))

> [!TIP]
> Per informazioni dettagliate su toogroups di assegnazione di licenza, tra cui avanzate scenari e Office 365 licenze scenari, vedere [assegnare licenze toousers tramite l'appartenenza di gruppo in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md).

## <a name="assign-licenses-toousers-and-groups"></a>Assegnare licenze toousers e gruppo
Utilizza una sottoscrizione attiva, si deve innanzitutto assegnare una licenza tooyourself e si aggiorna il tooensure browser che vengono visualizzate tutte le funzionalità di hello previsto incluse con la sottoscrizione. passaggio successivo Hello è tooassign licenze toohello utenti devono accedere alle funzionalità di Azure AD toopaid. Le licenze tooassign un modo semplice è tooassign toogroups di licenze di utenti anziché tooindividuals. Quando si assegna licenze tooa gruppo, tutti i membri del gruppo vengono assegnati una licenza. Se gli utenti vengono aggiunti o rimossi dal gruppo di hello, licenza hello viene automaticamente assegnato o rimosso. 

> [!NOTE]
> Alcuni servizi Microsoft non sono disponibili in tutte le posizioni. Prima di può essere assegnata una licenza utente tooa, messaggio per l'amministratore deve specificare hello **località di utilizzo** proprietà per utente hello. È possibile impostare questa proprietà in **utente** &gt; **profilo** &gt; **impostazioni** in hello portale di Azure. Quando si utilizza l'assegnazione del gruppo di licenze, qualsiasi utente il cui percorso di utilizzo non è specificato eredita percorso hello della directory di hello.

tooassign una licenza, in **Azure Active Directory** &gt; **licenze** &gt; **tutti i prodotti**, selezionare uno o più prodotti, quindi **Assegnare** hello barra dei comandi.

![Selezionare un tooassign di licenza](media/license-users-groups/select-license-to-assign.png)

È possibile utilizzare hello **utenti e gruppi** toochoose pannello più utenti o gruppi o servizio toodisable piani nel prodotto hello. Utilizzare la casella di ricerca hello in toosearch superiore per i nomi utente e gruppo.

![Selezionare un utente o un gruppo per l'assegnazione di licenze](media/license-users-groups/select-user-for-license-assignment.png)

Quando si assegna licenze tooa gruppo, può richiedere del tempo prima che tutti gli utenti ereditano licenza hello in base alle dimensioni di hello del gruppo di hello. È possibile controllare lo stato di elaborazione hello in hello **gruppo** pannello, hello **licenze** riquadro.

![Stato di assegnazione delle licenze](media/license-users-groups/license-assignment-status.png)

Durante l'assegnazione di licenze di Azure AD, possono verificarsi errori di assegnazione, che però sono relativamente rari quando si gestiscono prodotti Azure AD ed Enterprise Mobility + Security. I potenziali errori di assegnazione sono limitati a:
- Conflitto di assegnazione: quando un utente è stato precedentemente assegnato una licenza che non è compatibile con la licenza corrente di hello. In questo caso, l'assegnazione di nuova licenza hello richiede la rimozione di hello corrente.
- Superato le licenze disponibili: quando il numero di hello degli utenti in gruppi assegnati supera le licenze disponibili hello, lo stato di assegnazione di un utente riflette tooassign un errore a causa di toomissing licenze.

### <a name="azure-ad-b2b-collaboration-licensing"></a>Licenze per Collaborazione B2B di Azure AD

Collaborazione B2B consente agli utenti guest tooinvite in Azure AD tenant tooprovide accesso tooAzure AD servizi e le risorse di Azure si rende disponibile.  

Non è previsto alcun addebito per invitare gli utenti B2B e assegnando loro tooan applicazione in Azure AD. Le applicazioni too10 per guest 3 report di base e di utente sono anche gratuito per gli utenti di collaborazione B2B. Se l'utente guest dispone di licenze appropriate assegnate nel tenant di Azure AD del partner di hello, essi verrà anche licenza in quelle in uso.

Non è obbligatorio, ma se si desidera tooprovide accedere alle funzionalità di Azure AD toopaid, devono avere la licenza agli utenti guest B2B con le licenze di Azure Active Directory appropriate. Un tenant con Azure Active Directory a pagamento licenza invitare possa assegnare diritti utente di collaborazione B2B utenti guest tooan cinque aggiuntive invitati toohello tenant. Per scenari e informazioni, vedere [Linee guida sulla Collaborazione B2B di Azure Active Directory](active-directory-b2b-licensing.md).

## <a name="view-assigned-licenses"></a>Visualizzare licenze assegnate

In **Azure Active Directory** &gt; **Licenze** &gt; **Tutti i prodotti** è visualizzato un riepilogo delle licenze assegnate e disponibili.

![Visualizzare il riepilogo delle licenze](media/license-users-groups/view-license-summary.png)

Quando si seleziona un prodotto specifico, è disponibile un elenco dettagliato di utenti e gruppi assegnati. Hello **utenti con licenza** sono elencati tutti gli utenti che attualmente utilizzano una licenza e se la licenza hello è stata assegnata direttamente toohello utente o se viene ereditato da un gruppo.

![Visualizzare i dettagli delle licenze](media/license-users-groups/view-license-detail.png)

Analogamente, hello **concesso in licenza gruppi** sono elencati tutti i gruppi di licenze toowhich sono state assegnate. Selezionare un utente o gruppo hello di tooopen **licenze** pannello, che mostra tutte le licenze assegnate toothat oggetto.

## <a name="remove-a-license"></a>Rimuovere una licenza

tooremove una licenza, visitare toohello utente o gruppo e aprire hello **licenze** riquadro. Selezionare hello licenza e fare clic su **rimuovere**.

![Rimuovere una licenza](media/license-users-groups/remove-license.png)

Impossibile rimuovere direttamente ereditate da utente hello da un gruppo di licenze. In alternativa, è possibile rimuovere utente hello dal gruppo di hello da cui si sta ereditando licenza hello.


## <a name="next-steps"></a>Passaggi successivi
In questa Guida rapida, si è appreso come tooassign licenze toousers e gruppi nella directory di Azure AD. 

È possibile utilizzare hello seguente collegamento tooconfigure sottoscrizione le assegnazioni delle licenze in Azure AD dal portale di Azure hello.

> [!div class="nextstepaction"]
> [Assegnare licenze di Azure AD](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Overview) 