---
title: aaaAdd nuovi utenti tooAzure Active Directory | Documenti Microsoft
description: Viene illustrato come tooadd nuovi utenti o modificare le informazioni utente in Azure Active Directory.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e3673727-6bec-4fdc-87a4-d65b213c4c3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 72f67ad41022fd19fd94c8e1301943b0db1e57bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-tooazure-active-directory"></a>Aggiungere nuovi utenti o gli utenti con account di Microsoft tooAzure Active Directory
Aggiungere gli utenti toopopulate la directory. Questo articolo viene illustrato come tooadd nuovi utenti nell'organizzazione e come tooadd utenti che dispongono di account Microsoft. Per altre informazioni sull'aggiunta di utenti da altre directory in Azure Active Directory o l'aggiunta di utenti da società partner, vedere [Aggiungere utenti da altre directory o società partner in Azure Active Directory](active-directory-create-users-external.md). Gli utenti aggiunti non dispongono delle autorizzazioni di amministratore per impostazione predefinita, ma è possibile assegnare ruoli toothem in qualsiasi momento.

> [!IMPORTANT]
> Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo. Per la modalità tooadd un utente nell'interfaccia di amministrazione di hello Azure AD, vedere [aggiungere nuovi utenti tooAzure Active Directory](active-directory-users-create-azure-portal.md).

## <a name="add-a-user"></a>Aggiungere un utente
1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com) con un account che sia un amministratore globale per la directory di hello.
2. Selezionare **Active Directory**, quindi selezionare il nome di hello della directory dell'organizzazione.
3. Seleziona hello **utenti** scheda e quindi nella barra dei comandi di hello, selezionare **Aggiungi utente**.
4. In hello **informazioni sull'utente** pagina **tipo di utente**, selezionare:

   * **Nuovo utente nell'organizzazione** : consente di aggiungere un nuovo account utente nella directory.
   * **Utente con un account Microsoft esistente** : aggiunge un consumer account tooyour directory di Microsoft esistente (ad esempio, un account di Outlook)
5. In base al **Tipo di utente**immettere un nome utente, per un nuovo utente, o un indirizzo di posta elettronica, per un utente con un account Microsoft.
6. Utente hello **profilo** pagina, fornire un nome e cognome, un nome descrittivo e un ruolo utente da hello **ruoli** elenco. Per altre informazioni sui ruoli utente e di amministratore, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md). Specificare se troppo**abilitare multi-Factor Authentication** per utente hello.
7. In hello **Ottieni password temporanea** selezionare **crea**.

> [!IMPORTANT]
> Se l'organizzazione utilizza più di un dominio, che è necessario conoscere i seguenti problemi quando si aggiunge un account utente di hello:
>
> * gli account utente tooadd con hello stesso nome dell'entità utente (UPN) tra i domini, **prima** aggiungere, ad esempio, geoffgrisso@contoso.onmicrosoft.com, **seguito da** geoffgrisso@contoso.com.
> * **Non** aggiungere geoffgrisso@contoso.com prima di aggiungere geoffgrisso@contoso.onmicrosoft.com. Questo ordine è importante e può essere complesso tooundo.
>
>

## <a name="change-user-information"></a>Modificare le informazioni utente
È possibile modificare qualsiasi attributo utente, ad eccezione di ID di oggetto hello.

1. Aprire la directory.
2. Seleziona hello **utenti** scheda e il nome visualizzato selezionare hello di hello utente desiderato toochange.
3. Salvare le modifiche e quindi fare clic su **Salva**.

Se l'utente hello che si desidera modificare è sincronizzato con il servizio Active Directory locale, è possibile modificare le informazioni utente hello mediante questa procedura. utente hello toochange, utilizzare gli strumenti di gestione di Active Directory locale.

## <a name="guest-user-management-and-limitations"></a>Gestione e limiti dell'utente guest
Account guest sono utenti da altre directory che sono stati invitati tooyour directory tooaccess SharePoint documenti, applicazioni o altre risorse di Azure. Un account guest nella directory di dispone dell'attributo di UserType sottostante impostato troppo "Guest". Gli utenti standard (in particolare, i membri della directory) hanno l'attributo UserType hello "Member".

Gli utenti guest dispongono di un set limitato di diritti nella directory hello. Questi diritti limitano il possibilità hello per altri utenti nella directory hello informazioni toodiscover guest. Tuttavia, gli utenti guest ancora possono interagire con gli utenti di hello e gruppi associati alle risorse di hello che cui stai lavorando. Gli utenti guest possono:

* Vedere altri utenti e gruppi associati toowhich una sottoscrizione di Azure che sono state assegnate
* Visualizzare i membri di gruppi toowhich che appartengono hello
* Cercare altri utenti nella directory di hello, se si conosce l'indirizzo di posta elettronica completo hello dell'utente hello
* Vedere solo un set limitato di attributi di utenti hello che sono cercare - toodisplay limitato nome, indirizzo di posta elettronica, nome dell'entità utente (UPN) e foto di anteprima
* Ottenere un elenco dei domini verificati nella directory hello
* Consenso tooapplications, concedere loro hello stessi diritti di accesso che dispongono di membri nella directory

## <a name="set-guest-user-access-policies"></a>Impostare i criteri di accesso degli utenti guest
Hello **configura** scheda di una directory include opzioni toocontrol accesso per gli utenti guest. Tali opzioni possono essere modificate unicamente da un amministratore globale di directory nel portale di Azure classico. Al momento non è disponibile alcun metodo di PowerShell o API.

hello tooopen **configura** scheda hello Azure selezionare portale classico **Active Directory**, quindi selezionare il nome di hello della directory hello.

![Scheda Configura in Azure Active Directory][1]

È quindi possibile modificare l'accesso toocontrol hello opzioni per gli utenti guest.

![opzioni di controllo di accesso per gli utenti guest][2]

## <a name="whats-next"></a>Passaggi successivi
* [Aggiungere utenti da altre directory o società partner in Azure Active Directory](active-directory-create-users-external.md)
* [Amministrazione di Azure AD](active-directory-administer.md)
* [Gestire password in Azure AD](active-directory-manage-passwords.md)
* [Gestire gruppi in Azure AD](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
