---
title: 'Servizio di sincronizzazione Azure AD Connect: impedire eliminazioni accidentali | Documentazione Microsoft'
description: "In questo argomento descrive hello impedire funzionalità eliminazioni accidentali (impedisce l'eliminazione accidentale) in Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b852cb4-2850-40a1-8280-8724081601f7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 159597f8354806fcaea1430e0ff84956338592a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-prevent-accidental-deletes"></a>Servizio di sincronizzazione Azure AD Connect: Impedire eliminazioni accidentali
In questo argomento descrive hello impedire funzionalità eliminazioni accidentali (impedisce l'eliminazione accidentale) in Azure AD Connect.

Quando l'installazione di Azure AD Connect, impedisce accidentale eliminazione è abilitata per impostazione predefinita e configurato toonot consentire un'esportazione con più di 500 eliminazioni. Questa funzionalità è progettata tooprotect sia dalla configurazione accidentale cambia e le modifiche di directory locale tooyour che influirebbe molti utenti e altri oggetti.

## <a name="what-is-prevent-accidental-deletes"></a>Informazioni sulla prevenzione di eliminazioni accidentali
Gli scenari comuni in cui si verificano molte eliminazioni includono:

* Modifica troppo[filtro](active-directory-aadconnectsync-configure-filtering.md) in un'intera [OU](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) o [dominio](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) è deselezionata.
* Vengono eliminati tutti gli oggetti in un'unità organizzativa.
* Un'unità Organizzativa è stata rinominata in modo tutti gli oggetti in essa contenuti sono considerati toobe dall'ambito di sincronizzazione.

valore predefinito di Hello di 500 oggetti può essere modificato con PowerShell tramite `Enable-ADSyncExportDeletionThreshold`. È consigliabile configurare questa dimensione di hello valore toofit dell'organizzazione. Poiché l'utilità di pianificazione sincronizzazione hello viene eseguito ogni 30 minuti, il valore di hello è il numero di hello di eliminazione visualizzato entro 30 minuti.

Se sono presenti troppi toobe eliminazioni staging esportati tooAzure Active Directory, quindi hello di esportazione verrà interrotto e viene visualizzato un messaggio simile al seguente:

![Messaggio di posta elettronica per evitare eliminazioni accidentali](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/email.png)

> *Gentile (contatto tecnico), (Ora) servizio di sincronizzazione delle identità hello rileva che il numero di hello di eliminazione superato soglia di eliminazione configurato hello per (nome organizzazione). È stato inviato un totale di (numero) oggetti per l'eliminazione in questa esecuzione di sincronizzazione delle identità. Questo raggiunta o superata hello configurato valore di soglia di eliminazione di oggetti (numero). È necessario tooprovide conferma che queste operazioni devono essere elaborati prima di procedere sarà. Vedere hello impedendo eliminazioni accidentali per ulteriori informazioni sull'errore hello elencato nel messaggio di posta elettronica.*
>
> 

È inoltre possibile visualizzare lo stato di hello `stopped-deletion-threshold-exceeded` quando si osserva hello **Synchronization Service Manager** dell'interfaccia utente per il profilo di esportazione hello.
![Interfaccia utente di Synchronization Service Manager per evitare eliminazioni accidentali](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/syncservicemanager.png)

Se si tratta di un messaggio inatteso, ricercare la causa e intraprendere eventuali azioni correttive. hello toosee su toobe eliminata, gli oggetti seguenti:

1. Avviare **servizio di sincronizzazione** da hello Menu Start.
2. Andare troppo**connettori**.
3. Seleziona hello connettore con tipo **Azure Active Directory**.
4. In **azioni** toohello a destra, selezionare **spazio connettore ricerca**.
5. Nella finestra popup in hello **ambito**, selezionare **disconnesso perché** e seleziona un orario in hello precedente. Fare clic su **Search**(Cerca). Questa pagina fornisce una visualizzazione di tutti gli oggetti relativi toobe eliminato. Fare clic su ogni elemento, è possibile ottenere informazioni aggiuntive sull'oggetto hello. È anche possibile fare clic su **impostazione colonna** tooadd ulteriori attributi toobe visibile nella griglia hello.

![Spazio connettore di ricerca](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/searchcs.png)

Se si vogliono stabilire tutte le eliminazioni di hello quindi hello seguenti:

1. tooretrieve hello corrente soglia di eliminazione, eseguire il cmdlet PowerShell di hello `Get-ADSyncExportDeletionThreshold`. Indicare un account di amministratore globale di Azure AD e una password. valore predefinito di Hello è 500.
2. tootemporarily disabilitare tale protezione e consentono le eliminazioni passino, eseguire il cmdlet PowerShell di hello: `Disable-ADSyncExportDeletionThreshold`. Indicare un account di amministratore globale di Azure AD e una password.
   ![Credenziali](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/credentials.png)
3. Con hello Azure Active Directory Connector ancora selezionata, selezionare l'azione di hello **eseguire** e selezionare **esportare**.
4. toore-abilitazione della protezione hello, eseguire il cmdlet PowerShell di hello: `Enable-ADSyncExportDeletionThreshold -DeletionThreshold 500`. Sostituire 500 con valore hello che noteranno durante il recupero di soglia di eliminazione corrente hello. Indicare un account di amministratore globale di Azure AD e una password.

## <a name="next-steps"></a>Passaggi successivi
**Argomenti generali**

* [Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione](active-directory-aadconnectsync-whatis.md)
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
