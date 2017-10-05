---
title: Aggiungere nuovi utenti ad Azure Active Directory | Documentazione Microsoft
description: Viene illustrato come aggiungere nuovi utenti in Azure Active Directory.
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
ms.openlocfilehash: 13a7d2d3b991206c45e66872b590bc27a224eead
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="quickstart-add-new-users-to-azure-active-directory"></a>Guida introduttiva: Aggiungere nuovi utenti ad anteprima di Azure Active Directory
In questo articolo viene illustrato come aggiungere nuovi utenti dell'organizzazione in Azure Active Directory (Azure AD) uno per volta, utilizzando il portale di Azure o sincronizzando i dati dell'account utente Windows Server Active Directory locale. 

## <a name="add-cloud-based-users"></a>Aggiungere gli utenti basati su cloud
1. Accedere all'[interfaccia di amministrazione di Azure Active Directory](https://aad.portal.azure.com) con un account di amministratore globale per la directory del tenant.
2. Selezionare **Azure Active Directory** e quindi **Utenti e gruppi**.
3. Nel pannello **Utenti e gruppi** selezionare **Tutti gli utenti** e quindi selezionare **Nuovo utente**.
   ![Selezione del comando Aggiungi](./media/add-users-azure-active-directory/add-user.png)
4. Immettere dettagli per gli utenti, ad esempio **nome** e **nome utente**. La parte del nome di dominio del nome utente deve essere il nome di dominio "[nome dominio]" del nome di dominio predefinito iniziale o un nome di dominio verificato, non federato, [personalizzato, ](add-custom-domain.md)ad esempio "contoso.com".
5. Copiare o comunque annotare la password generata in modo da poterla fornire all'utente al termine del processo.
6. Facoltativamente, è possibile aprire e inserire le informazioni contenute nel pannello **Profilo**, **Gruppi** o **Ruolo della directory** per l'utente. Per altre informazioni sui ruoli utente e di amministratore, vedere [Assegnazione dei ruoli di amministratore in Azure Active Directory](active-directory-assign-admin-roles.md).
7. Nel pannello **Utente** selezionare **Crea**.
8. Distribuire in modo sicuro la password generata al nuovo utente per consentirgli l'accesso.

> [!TIP]
> È inoltre possibile sincronizzare i dati dell'account utente locale Windows Server Active Directory. Le soluzioni di gestione delle identità di Microsoft abbracciano funzionalità locali e basate sul cloud, creando una singola identità utente per l’autenticazione e l’autorizzazione per tutte le risorse, indipendentemente dalla loro ubicazione. Tutto questo viene chiamato Identità ibrida. È possibile utilizzare [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)per integrare le directory locali con Azure Active Directory per gli scenari con identità ibrida. Consente quindi di fornire agli utenti un'identità comune per le applicazioni di Office 365, Azure e SaaS integrate con Azure AD. 

## <a name="delete-users-from-azure-ad"></a>Eliminare gli utenti da Azure Active Directory
1. Accedere all'[interfaccia di amministrazione di Azure Active Directory](https://aad.portal.azure.com) con un account di amministratore globale per la directory del tenant.
2. Selezionare **Utenti e gruppi**.
3. Nel pannello **Utenti e gruppi**, selezionare l'utente da eliminare dall'elenco. 
4. Nel pannello dell'utente selezionare **Panoramica**, quindi nella barra dei comandi selezionare **Elimina**.
   ![Selezione del comando Aggiungi](./media/add-users-azure-active-directory/delete-user.png)


### <a name="learn-more"></a>Altre informazioni 
* [Aggiungere un utente esterno](active-directory-users-create-external-azure-portal.md)

* [Assegnare un utente a un ruolo in Azure AD](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a>Passaggi successivi
In questa guida introduttiva si è appreso come aggiungere nuovi utenti ad Azure AD Premium. 

È possibile usare il collegamento seguente per creare un nuovo utente in Azure AD dal portale di Azure.

> [!div class="nextstepaction"]
> [Aggiungere utenti ad Azure AD](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 