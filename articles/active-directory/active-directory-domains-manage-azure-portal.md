---
title: aaaManaging i nomi di dominio personalizzati in Azure Active Directory | Documenti Microsoft
description: Concetti relativi alla gestione e procedure dettagliate per gestire un nome di dominio in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5063cd0a-dba2-4ba9-aa65-b8117490d73a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: curtand;jeffsta
ms.openlocfilehash: 4719524c4e972f6c981db39f016729da13b37670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a>Gestione dei nomi di dominio personalizzati in Azure Active Directory
Un nome di dominio è una parte importante di molte risorse di directory di identificatore hello: fa parte di un indirizzo di posta elettronica o nome utente per un utente, parte dell'indirizzo hello per un gruppo e possono far parte di URI ID app hello per un'applicazione. Una risorsa in Azure Active Directory (Azure AD) può includere un nome di dominio che è già verificato come di proprietà di directory hello che contiene risorse hello. Solo un amministratore globale può eseguire attività di gestione del dominio in Azure AD.

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a>Imposta il nome di dominio primario di hello per le directory di Azure AD
Quando viene creata la directory, nome di dominio iniziale hello, ad esempio "contoso.onmicrosoft.com", è anche il nome di dominio primario hello. dominio primario Hello è nome di dominio hello predefinito per un nuovo utente quando si crea un nuovo utente. Impostazione di un nome di dominio primario semplifica il processo di hello per un amministratore toocreate nuovi utenti portale hello. nome di dominio primario toochange hello:

1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.
2. Selezionare **più servizi**, immettere **Azure Active Directory** nella casella di testo hello e quindi selezionare **invio**.
   
   ![Apertura di Gestione utenti](./media/active-directory-domains-add-azure-portal/user-management.png)
3. In hello ***nome directory*** pannello seleziona **i nomi di dominio**.
4. In hello  ***nome directory* -i nomi di dominio** pannello, il nome di dominio selezionare hello desideri toomake nome di dominio primario hello.
5. In hello ***nome di dominio*** blade (vale a dire hello pannello visualizzato con il nuovo nome di dominio nel titolo hello), selezionare hello **Make primary** comando. Confermare la scelta quando viene richiesto.
   
   ![Rendere primario un nome di dominio](./media/active-directory-domains-manage-azure-portal/make-primary.png)

È possibile modificare il nome di dominio primario hello per le directory di toobe qualsiasi dominio personalizzato verificato che non sia federato. Modifica hello primario di dominio per la directory non modificherà i nomi utente hello per tutti gli utenti esistenti.

## <a name="add-custom-domain-names-tooyour-azure-ad"></a>Aggiungere tooyour di nomi di dominio personalizzato AD Azure
È possibile aggiungere le directory di Azure AD tooeach nomi too900 dominio personalizzato. Hello processo troppo[aggiungere un nome di dominio personalizzati aggiuntivi](add-custom-domain.md) hello uguali per nome di dominio personalizzato prima di hello.

## <a name="add-subdomains-of-a-custom-domain"></a>Aggiungere sottodomini di un dominio personalizzato
Se si desidera tooadd un nome di dominio di terzo livello, ad esempio 'europe.contoso.com' tooyour directory, è necessario aggiungere e verificare il dominio di secondo livello hello, ad esempio contoso.com. sottodominio Hello verrà verificato automaticamente da Azure AD. è stato verificato toosee che hello sottodominio appena aggiunta, aggiornamento hello pagina nel browser hello che elenca i domini hello.

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a>Quali toodo se si modifica registrazione DNS hello per nome di dominio personalizzato
Se si modifica una registrazione DNS hello per nome di dominio personalizzato, è possibile continuare a toouse il nome di dominio personalizzato con Azure Active Directory stessa senza interruzioni e senza ulteriori operazioni di configurazione. Se si utilizza il nome di dominio personalizzato con Office 365, Intune o altri servizi che si basano sui nomi di dominio personalizzato in Azure Active Directory, consultare la documentazione di toohello per tali servizi.

## <a name="delete-a-custom-domain-name"></a>Eliminare un nome di dominio personalizzato
Se l'organizzazione non usa tale nome di dominio o se è necessario toouse nome di dominio con Azure AD un altro, è possibile eliminare un nome di dominio personalizzato da Azure AD.

toodelete un nome di dominio personalizzato, è innanzitutto necessario assicurarsi che nessuna risorsa nel servizio directory si basa sul nome di dominio hello. Non è possibile eliminare un nome di dominio dalla directory nei casi seguenti:

* Qualsiasi utente che ha un nome utente, un indirizzo di posta elettronica o un indirizzo proxy che include il nome di dominio di hello.
* Qualsiasi gruppo ha un indirizzo di posta elettronica o l'indirizzo proxy che include il nome di dominio di hello.
* Qualsiasi applicazione in Azure AD dispone una URI ID app che include il nome di dominio di hello.

È necessario modificare o eliminare qualsiasi esempio di risorsa nella directory di Azure AD prima di poter eliminare il nome di dominio personalizzato hello.

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a>Utilizzare nomi di dominio toomanage PowerShell o l'API Graph
La maggior parte delle attività di gestione per i nomi di dominio in Azure Active Directory può anche essere completata usando Microsoft PowerShell oppure a livello di codice usando l'API Graph di Azure AD.

* [Utilizzo di PowerShell toomanage i nomi di dominio in Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Utilizzo di nomi di dominio toomanage API Graph di Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a>Passaggi successivi
* [Aggiungere nomi di dominio personalizzati](add-custom-domain.md)

