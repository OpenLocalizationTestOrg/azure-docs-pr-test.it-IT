---
title: gruppo aaaRestore un eliminato di Office 365 in Azure Active Directory | Documenti Microsoft
description: Come toorestore un gruppo eliminato, Visualizza i gruppi possono ripristinare e permamnently Elimina un gruppo in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: curtand
ms.openlocfilehash: 4e6650d64aa19f0c909f1c511f48681de8032f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a>Ripristinare un gruppo di Office 365 eliminato in Azure Active Directory

Quando si elimina un gruppo di Office 365 in hello Azure Active Directory (Azure AD), gruppo hello eliminato è mantenuta ma non è visibile per 30 giorni dalla data di eliminazione hello. Si tratta in modo che il gruppo di hello e il relativo contenuto può essere ripristinato se necessario. Questa funzionalità è limitata esclusivamente tooOffice 365 gruppi in Azure AD. Non è disponibile per i gruppi di sicurezza e i gruppi di distribuzione.

> [!NOTE] 
> Non utilizzare `Remove-MsolGroup` perché lo Elimina gruppo hello in modo permanente. Utilizzare sempre `Remove-AzureADMSGroup` gruppo toodelete un Office 365. 

autorizzazioni di Hello necessarie toorestore un gruppo può essere una delle seguenti operazioni hello:

Ruolo  | autorizzazioni 
--------- | ---------
Amministratore della società, supporto partner di livello 2 e amministratori del servizio di InTune | Possono ripristinare qualsiasi gruppo di Office 365 eliminato 
Amministratore dell'account utente e supporto partner di livello 1 | Ripristinare qualsiasi gruppo di Office 365 eliminato, ad eccezione di tali toohello assegnato il ruolo di amministratore della società 
Utente | Possono ripristinare qualsiasi gruppo di Office 365 eliminato che era di loro proprietà 


## <a name="view-hello-deleted-office-365-groups-that-are-available-toorestore"></a>Hello vista eliminata gruppi di Office 365 toorestore disponibili
Hello seguendo i cmdlet può essere utilizzati tooview hello eliminato gruppi tooverify che hello uno o quelli che si è interessati non ancora stati definitivamente eliminati. Questi cmdlet sono parte di hello [modulo Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureAD/). Ulteriori informazioni su questo modulo sono reperibile in hello [Azure Active Directory PowerShell versione 2](/powershell/azure/install-adv2?view=azureadps-2.0) articolo.

1.  Eseguire hello cmdlet toodisplay eliminati tutti i gruppi di Office 365 nel tenant che sono ancora disponibili toorestore seguente.
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  In alternativa, se si conosce objectID hello di un gruppo specifico (ed è possibile ottenerlo dal cmdlet hello nel passaggio 1), esecuzione hello seguente tooverify cmdlet che hello specifico gruppo eliminato non ancora definitivamente eliminato.
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-toorestore-your-deleted-office-365-group"></a>Come toorestore il gruppo di Office 365 eliminato
Dopo avere verificato che tale gruppo hello sia ancora disponibile toorestore, ripristinare il gruppo di hello eliminato con uno di hello alla procedura seguente. Se il gruppo di hello contiene documenti, SP siti o altri oggetti persistenti, potrebbe richiedere fino a too24 ore toofully ripristino un gruppo e il relativo contenuto.

1.  Esecuzione hello seguenti gruppo hello toorestore di cmdlet e il relativo contenuto.
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

In alternativa, hello cmdlet seguente può essere eseguito toopermanently rimuovere il gruppo di hello eliminato.
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a>Come si verifica che l'azione è riuscita?
che è stato ripristinato correttamente un gruppo di Office 365, eseguire hello tooverify `Get-AzureADGroup –ObjectId <objectId>` toodisplay cmdlet informazioni gruppo hello. Dopo il ripristino di hello completamento della richiesta:
- Hello gruppo verrà visualizzato nella barra di spostamento sinistro hello in Exchange
- piano di Hello per gruppo hello apparirà nella pianificazione
- I siti di Sharepoint e tutti i contenuti saranno disponibili
- gruppo Hello è possibile accedere da qualsiasi endpoint di scambio di hello e altri carichi di lavoro di Office 365 che supportano i gruppi di Office 365


## <a name="next-steps"></a>Passaggi successivi
Questi articoli contengono informazioni aggiuntive sui gruppi di Azure Active Directory.

* [Vedere i gruppi esistenti](active-directory-groups-view-azure-portal.md)
* [Gestire le impostazioni di un gruppo](active-directory-groups-settings-azure-portal.md)
* [Gestire i membri di un gruppo](active-directory-groups-members-azure-portal.md)
* [Gestire le appartenenze di un gruppo](active-directory-groups-membership-azure-portal.md)
* [Gestire le regole dinamiche per gli utenti in un gruppo](active-directory-groups-dynamic-membership-azure-portal.md)
