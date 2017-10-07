---
title: aaaAdd nuovi utenti tooAzure Active Directory | Documenti Microsoft
description: Viene illustrato come tooadd nuovi utenti in Azure Active Directory.
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 6ca413c84a7a5238a30fd26fc751d687d827b24a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-new-users-tooazure-active-directory"></a>Guida introduttiva: Aggiungere nuovi utenti tooAzure Active Directory
Questo articolo spiega come tooadd nuovi utenti dell'organizzazione in Azure Active Directory (Azure AD) hello uno alla volta utilizzando hello portale di Azure o sincronizzando l'utente di Windows Server Active Directory locale dell'account dati. 

## <a name="add-cloud-based-users"></a>Aggiungere gli utenti basati su cloud
1. Accedi toohello [centro di amministrazione di Azure Active Directory](https://aad.portal.azure.com) con un account che sia un amministratore globale per la directory di hello.
2. Selezionare **Azure Active Directory** e quindi **Utenti e gruppi**.
3. In hello **utenti e gruppi** pannello seleziona **tutti gli utenti**, quindi selezionare **nuovo utente**.
   ![Comando Aggiungi hello](./media/add-users-azure-active-directory/add-user.png)
4. Immettere i dettagli per l'utente hello, ad esempio **nome** e **nome utente**. Hello parte di nome di dominio del nome utente hello deve essere hello predefinita iniziale dominio nome "[nome dominio].onmicrosoft.com" o verificati, non federata [nome di dominio personalizzato](add-custom-domain.md) , ad esempio "contoso.com".
5. Generato password utente in modo che è possibile fornirlo toohello utente al termine questo processo di copia o hello nota in caso contrario.
6. Facoltativamente, è possibile aprire e compilare informazioni hello in hello **profilo** blade, hello **gruppi** pannello o hello **ruolo della Directory** pannello per l'utente hello. Per altre informazioni sui ruoli utente e di amministratore, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md).
7. In hello **utente** pannello seleziona **crea**.
8. Consente di distribuire in modo sicuro generato hello password toohello nuovo utente in modo che hello utente possa accedere.

> [!TIP]
> È inoltre possibile sincronizzare i dati dell'account utente locale Windows Server Active Directory. Soluzioni di gestione identità Microsoft span locale e le funzionalità basate su cloud, la creazione di una singola identità utente per l'autenticazione e autorizzazione tooall risorse, indipendentemente dalla posizione. Tutto questo viene chiamato Identità ibrida. [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) può essere utilizzato toointegrate le directory locali con Azure Active Directory per gli scenari identità ibrido. In questo modo tooprovide un'identità comune per gli utenti per le applicazioni di Office 365, Azure e SaaS integrata con Azure AD. 

## <a name="delete-users-from-azure-ad"></a>Eliminare gli utenti da Azure Active Directory
1. Accedi toohello [centro di amministrazione di Azure Active Directory](https://aad.portal.azure.com) con un account che sia un amministratore globale per la directory di hello.
2. Selezionare **Utenti e gruppi**.
3. In hello **utenti e gruppi** blade, toodelete utente hello selezionare dall'elenco di hello. 
4. Nel Pannello di hello per l'utente selezionato hello, selezionare **Panoramica**, quindi nella barra dei comandi di hello, selezionare **eliminare**.
   ![Comando Aggiungi hello](./media/add-users-azure-active-directory/delete-user.png)


### <a name="learn-more"></a>Altre informazioni 
* [Aggiungere un utente esterno](active-directory-users-create-external-azure-portal.md)

* [Assegnare un ruolo di utente tooa in Azure AD](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a>Passaggi successivi
In questa Guida rapida, si è appreso come tooadd nuovi utenti tooAzure AD Premium. 

È possibile utilizzare hello seguente collegamento toocreate un nuovo utente in Azure AD dal portale di Azure hello.

> [!div class="nextstepaction"]
> [Aggiungere gli utenti tooAzure AD](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 
