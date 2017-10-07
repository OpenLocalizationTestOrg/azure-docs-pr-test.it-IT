---
title: gruppi di Office 365 aaaPreview scadenza in Azure Active Directory | Documenti Microsoft
description: Come i gruppi tooset di scadenza per Office 365 in Azure Active Directory (anteprima)
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.openlocfilehash: a8c99961cff3aad3f4d8b0cc1b2eb8e8a4c9ba95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a>Configurare la scadenza dei gruppi di Office 365 (anteprima)

È ora possibile gestire hello del ciclo di vita dei gruppi di Office 365 tramite l'impostazione di scadenza per i gruppi di Office 365 selezionato. Dopo la scadenza è impostata, i proprietari di tali gruppi sono frequenti toorenew i relativi gruppi se devono comunque gruppi hello. Qualsiasi gruppo di Office 365 che non viene rinnovato sarà eliminato. È possibile ripristinare alcun gruppo di Office 365 è stata eliminata entro 30 giorni per i proprietari del gruppo hello o un amministratore di hello.  


> [!NOTE]
> È possibile impostare la scadenza solo per i gruppi di Office 365.
>
> Per impostare la scadenza per i gruppi di Office 365, è necessario che venga assegnata una licenza di Azure AD Premium a
>   - messaggio per l'amministratore che configura le impostazioni di scadenza hello per tenant hello
>   - Tutti i membri dei gruppi di hello selezionati per questa impostazione

## <a name="set-office-365-groups-expiration"></a>Impostare la scadenza dei gruppi di Office 365

1. Aprire hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) con un account che sia un amministratore globale nel tenant di Azure AD.

2. Aprire Azure AD e selezionare **Utenti e gruppi**.

3. Selezionare **impostazioni gruppo** e quindi selezionare **scadenza** tooopen le impostazioni di scadenza hello.
  
  ![Pannello Scadenza](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. In hello **scadenza** pannello, è possibile:

  * Impostare una durata di un gruppo hello in giorni. È possibile selezionare uno dei set di impostazioni hello valori o un valore personalizzato (dovrebbe essere 31 giorni o più). 
  * Specificare un indirizzo di posta elettronica in cui le notifiche di rinnovo e scadenza hello devono essere inviate quando un gruppo non ha un proprietario. 
  * Selezionare i gruppi di Office 365 che scadono. È possibile abilitare la scadenza per **tutti** gruppi di Office 365, è possibile selezionare tra i gruppi di Office 365 hello o si seleziona **Nessuno** per disabilitare la scadenza per tutti i gruppi.
  * Al termine salvare le impostazioni facendo clic su **Salva**.

Per istruzioni su come toodownload e installare hello scadenza tooconfigure modulo di PowerShell di Microsoft per i gruppi di Office 365 tramite PowerShell, vedere [modulo Azure Active Directory V2 PowerShell - versione di anteprima pubblica 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).

Notifiche di posta elettronica, ad esempio quello vengono inviate a 30 giorni, 15 giorni, i proprietari del gruppo toohello Office 365 e 1 giorno tooexpiration precedente del gruppo di hello.

![Notifica di scadenza tramite posta elettronica](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

quindi è possibile selezionare il proprietario del gruppo Hello **gruppo rinnovo** toorenew hello gruppo Office 365, oppure è possibile selezionare **passare toogroup** membri hello toosee e altri dettagli sulla hello gruppo.

Alla scadenza di un gruppo, il gruppo di hello viene eliminato un giorno alla data di scadenza hello. I proprietari del gruppo toohello Office 365 informa sulla scadenza hello e successiva eliminazione dei relativi gruppi di Office 365 verrà inviata una notifica di posta elettronica, ad esempio quello.

![Notifica tramite posta elettronica per l'eliminazione del gruppo](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

gruppo Hello può essere ripristinato selezionando **ripristino gruppo** o utilizzando i cmdlet di PowerShell, come descritto in [gruppo di ripristino un eliminato di Office 365 in Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/ Active-Directory-Groups-Restore-Azure-Portal).
    
Se il gruppo di hello che si sta ripristinando contiene documenti, siti di SharePoint o altri oggetti permanenti, operazione può richiedere too24 ore toofully ripristino hello gruppo e il relativo contenuto.

> [!NOTE]
> * Quando si distribuiscono le impostazioni di scadenza hello, potrebbero essere presenti alcuni gruppi che sono più vecchi di finestra di scadenza hello. Questi gruppi non vengono eliminati immediatamente, ma sono impostare too30 giorni fino alla scadenza. Hello primo rinnovo notifica tramite posta elettronica viene inviato all'interno di un giorno. Ad esempio, un gruppo è stato creato 400 giorni fa e hello intervallo di scadenza è impostato too180 giorni. Quando si applicano le impostazioni di scadenza, un gruppo è 30 giorni prima di essere eliminate, a meno che lo rinnova proprietario hello.
> * Quando un gruppo dinamico viene eliminato e viene ripristinato, viene considerata un nuovo gruppo e nuovamente popolato regola toohello secondo. Questo processo può richiedere ore too24.

## <a name="next-steps"></a>Passaggi successivi
Questi articoli forniscono informazioni aggiuntive sui gruppi di Azure AD.

* [Vedere i gruppi esistenti](active-directory-groups-view-azure-portal.md)
* [Gestire le impostazioni di un gruppo](active-directory-groups-settings-azure-portal.md)
* [Gestire i membri di un gruppo](active-directory-groups-members-azure-portal.md)
* [Gestire le appartenenze di un gruppo](active-directory-groups-membership-azure-portal.md)
* [Gestire le regole dinamiche per gli utenti in un gruppo](active-directory-groups-dynamic-membership-azure-portal.md)
