---
title: aaaManaging i nomi di dominio personalizzati in Azure Active Directory | Documenti Microsoft
description: Concetti relativi alla gestione e procedure dettagliate per gestire un dominio personalizzato in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cf3523bd-9ee0-439e-963d-ccea038867b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 4b6d06fecf3be0621be51c38a1330eafdc1b4d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a>Gestione dei nomi di dominio personalizzati in Azure Active Directory
Un nome di dominio può essere un identificatore importante per molte risorse della directory, come parte di:

* Un nome utente o un indirizzo di posta elettronica di un utente
* indirizzo Hello per un gruppo
* URI ID app Hello per un'applicazione

Una risorsa in Azure Active Directory (Azure AD) può includere un nome di dominio che è già verificato toobe proprietà directory hello che contiene risorse hello. Solo un amministratore globale può eseguire attività di gestione del dominio in Azure AD.

> [!IMPORTANT]
> Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo. Per modalità toomanage i nomi di dominio nel centro di amministrazione di hello Azure AD, vedere [gestione dei nomi di dominio personalizzati in Azure Active Directory](active-directory-domains-manage-azure-portal.md).

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a>Imposta il nome di dominio primario di hello per le directory di Azure AD
Quando viene creata la directory, nome di dominio iniziale hello, ad esempio "contoso.onmicrosoft.com", è anche il nome di dominio primario hello per le directory. dominio primario Hello è nome di dominio hello predefinito per un nuovo utente quando si crea un nuovo utente in hello [portale di Azure classico](https://manage.windowsazure.com/), o altri portali, ad esempio il portale di amministrazione di Office 365 hello. Questo semplifica il processo di hello per un amministratore toocreate nuovi utenti portale hello.

nome di dominio primario toochange hello per la directory:

1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com/) con un account utente che è un amministratore globale della directory di Azure AD.
2. Selezionare **Active Directory** nella barra di spostamento a sinistra di hello.
3. Aprire la directory.
4. Seleziona hello **domini** scheda.
5. Seleziona hello **modifica primario** pulsante sulla barra dei comandi di hello.
6. Selezionare il dominio hello che si desidera toobe hello nuovo primario dominio per la directory.

È possibile modificare il nome di dominio primario hello per le directory di toobe qualsiasi dominio personalizzato verificato che non sia federato. Modifica hello primario di dominio per la directory non modificherà i nomi utente hello per tutti gli utenti esistenti.

## <a name="add-custom-domain-names-tooyour-azure-ad"></a>Aggiungere tooyour di nomi di dominio personalizzato AD Azure
È possibile aggiungere le directory di Azure AD tooeach nomi too900 dominio personalizzato. Hello processo troppo[aggiungere un nome di dominio personalizzati aggiuntivi](active-directory-add-domain.md) hello uguali per nome di dominio personalizzato prima di hello.

## <a name="add-subdomains-of-a-custom-domain"></a>Aggiungere sottodomini di un dominio personalizzato
Se si desidera tooadd un nome di dominio di terzo livello, ad esempio 'europe.contoso.com' tooyour directory, è necessario aggiungere e verificare il dominio di secondo livello hello, ad esempio contoso.com. sottodominio Hello verrà verificato automaticamente da Azure AD. è stato verificato toosee che hello sottodominio appena aggiunta, aggiornamento hello pagina nel browser hello che elenca i domini hello nella directory.

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a>Quali toodo se si modifica registrazione DNS hello per nome di dominio personalizzato
Se si modifica una registrazione DNS hello per nome di dominio personalizzato, è possibile continuare a toouse il nome di dominio personalizzato con Azure Active Directory stessa senza interruzioni e senza ulteriori operazioni di configurazione. Se si utilizza il nome di dominio personalizzato con Office 365, Intune o altri servizi che si basano sui nomi di dominio personalizzato in Azure Active Directory, consultare la documentazione di toohello per tali servizi.

## <a name="delete-a-custom-domain-name"></a>Eliminare un nome di dominio personalizzato
Se l'organizzazione non usa tale nome di dominio o se è necessario toouse nome di dominio con Azure AD un altro, è possibile eliminare un nome di dominio personalizzato da Azure AD.

toodelete un nome di dominio personalizzato, è innanzitutto necessario assicurarsi che nessuna risorsa nel servizio directory si basa sul nome di dominio hello. Non è possibile eliminare un nome di dominio dalla directory nei casi seguenti:

* Qualsiasi utente che ha un nome utente, un indirizzo di posta elettronica o un indirizzo proxy che includono il nome di dominio di hello.
* Qualsiasi gruppo ha un indirizzo di posta elettronica o l'indirizzo proxy che include il nome di dominio di hello.
* Qualsiasi applicazione in Azure AD dispone una URI ID app che include il nome di dominio di hello.

È necessario modificare o eliminare qualsiasi esempio di risorsa nella directory di Azure AD prima di poter eliminare il nome di dominio personalizzato hello.

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a>Utilizzare nomi di dominio toomanage PowerShell o l'API Graph
La maggior parte delle attività di gestione per i nomi di dominio in Azure Active Directory può anche essere completata usando Microsoft PowerShell oppure a livello di codice usando l'API Graph di Azure AD.

* [Utilizzo di PowerShell toomanage i nomi di dominio in Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Utilizzo di nomi di dominio toomanage API Graph di Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a>Passaggi successivi
* [Informazioni sui nomi di dominio in Azure AD](active-directory-add-domain-concepts.md)
* [Gestire i nomi di dominio personalizzati](active-directory-add-manage-domain-names.md)

