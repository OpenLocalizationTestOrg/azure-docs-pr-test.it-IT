---
title: nome di dominio personalizzato aaaAdd tooAzure Active Directory | Documenti Microsoft
description: "Come tooadd della società nomi di dominio Active Directory tooAzure e come tooverify hello nome di dominio."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d97e57c6-578a-4929-8fb8-42e858a711c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 88d5f443cd10b098a9a9ffb3137f5e1ca33b6aad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-domain-name-tooazure-active-directory"></a>Aggiungere un tooAzure di nome di dominio personalizzato Active Directory
> [!div class="op_single_selector"]
> * [Portale di Azure](active-directory-domains-add-azure-portal.md)
> * [portale di Azure classico](active-directory-add-domain.md)
> 

Tramite Azure Active Directory (Azure AD), è possibile aggiungere il dominio aziendale nome tooAzure AD anche. Potrebbe essere un nome di dominio che si utilizza toodo attività organizzazione e gli utenti che accedono utilizzando il nome di dominio aziendale. Aggiunta di hello dominio nome tooAzure AD consente tooassign nomi utente nella directory hello sono tooyour familiarità, ad esempio 'alice@contoso.com.' il processo di Hello è semplice:

1. Aggiungere directory tooyour nome di dominio personalizzato hello
2. Aggiungere una voce DNS per il nome di dominio di hello al registrar di nomi di dominio hello
3. Verificare il nome di dominio personalizzato hello in Azure AD

## <a name="how-do-i-add-a-domain-name"></a>Come è possibile aggiungere un nome di dominio?
1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.
2. Selezionare **più servizi**, immettere **Azure Active Directory** nella casella di testo hello e quindi selezionare **invio**.
   
   ![Apertura di Gestione utenti](./media/active-directory-domains-add-azure-portal/user-management.png)
3. In hello ***nome directory*** pannello seleziona **i nomi di dominio**.
4. In hello  ***nome directory* -i nomi di dominio** blade, seleziona hello **Aggiungi** comando.
   
   ![Comando Aggiungi hello](./media/active-directory-domains-add-azure-portal/add-command.png)
5. In hello **nome di dominio** pannello, immettere il nome di hello del dominio personalizzato nella casella hello, ad esempio 'contoso.com' e quindi selezionare **Aggiungi dominio**. Essere certi tooinclude hello COM, .net o altre estensioni di livello superiore.
6. In hello ***domainname*** blade (vale a dire hello pannello visualizzato con il nuovo nome di dominio nel titolo hello), ottenere informazioni relative alla voce DNS hello che Azure AD utilizzerà tooverify che l'azienda dispone di nome di dominio personalizzato hello.
   
   ![ottenere informazioni relative alla voce DNS](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

Dopo aver aggiunto il nome di dominio di hello, Azure AD deve verificare che il nome di dominio hello proprietà dell'organizzazione. Prima di Azure AD è possibile eseguire questa verifica, è necessario aggiungere una voce DNS nel file di zona DNS hello hello nome di dominio. Questa attività viene eseguita nel sito Web di hello per nome di dominio per il nome di dominio di hello.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Aggiungere una voce DNS hello presso hello registrar per dominio hello
nome di dominio personalizzato con Azure AD Hello successivo passaggio toouse è file di zona DNS hello tooupdate per dominio hello. In questo modo l'azienda dispone di nome di dominio personalizzato hello tooverify di Azure AD.

1. Accedi toohello registrar di nomi di dominio per il dominio hello. Se non si dispone di hello tooupdate accesso voce DNS, chiedere persona hello o team che dispone di questo passaggio toocomplete accesso 2 e toolet che quando viene completato il processo.
2. File di zona DNS hello aggiornamento per il dominio hello aggiungendo la voce DNS hello fornite tooyou da Azure AD. Questa voce DNS consente AD Azure tooverify le proprietà di dominio di hello. Hello voce DNS non modifica eventuali comportamenti, ad esempio routing della posta elettronica o di hosting web.

Per informazioni su questa voce DNS di hello aggiunta, leggere [istruzioni per l'aggiunta di una voce DNS nel Registrar comuni di DNS](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Verificare il nome di dominio hello con Azure AD
Dopo aver aggiunto voce DNS hello, si è pronti tooverify nome di dominio hello con Azure AD.

Un nome di dominio può essere verificato solo dopo avere propagato record DNS hello. La propagazione richiede spesso solo qualche secondo, ma a volte può richiedere più di un'ora. Se la verifica non funziona hello prima volta, riprovare più tardi.

1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.
2. Selezionare **Sfoglia**, gestione degli utenti di immettere nella casella di testo hello e quindi selezionare **invio**.
   
   ![Apertura di Gestione utenti](./media/active-directory-domains-add-azure-portal/user-management.png)
3. In hello **Gestione utenti: i nomi di dominio** pannello, il nome di dominio non verificato selezionare hello che si desidera tooverify.
4. In hello ***domainname*** blade (vale a dire hello pannello visualizzato con il nuovo nome di dominio nel titolo hello), selezionare **verificare** verifica hello toocomplete.

A questo punto è possibile [assegnare nomi utente che includono il nome di dominio personalizzato](active-directory-users-create-azure-portal.md).

## <a name="troubleshooting"></a>Risoluzione dei problemi
Se non è possibile verificare un nome di dominio personalizzato, provare l'esempio hello. Si inizierà con hello più comune e di lavoro verso il basso toohello comune.

1. **Attendere un'ora**. I record DNS necessario toopropagate prima di Azure AD è possibile verificare il dominio hello. Questa operazione potrebbe richiedere più di un'ora.
2. **Verificare i record DNS è stato immesso hello e che sia corretto**. Completare il passaggio al sito Web di hello per hello registrar per dominio hello. Azure AD non è possibile verificare il nome di dominio hello se hello voce DNS non è presente in hello file di zona DNS o se non è una corrispondenza esatta con la voce DNS hello fornito ad Azure AD. Se non si dispone di accesso tooupdate i record DNS hello dominio al registrar di nomi di dominio hello, condividere una voce DNS hello con hello persona o team dell'organizzazione che ha l'accesso e chiedere voce DNS di hello tooadd.
3. **Eliminare il nome di dominio di hello da un'altra directory di Azure AD**. Un nome di dominio può essere verificato solo in una directory. Se un nome di dominio è già stato verificato in un'altra directory, è necessario eliminarlo prima di poterlo verificare nella nuova directory. toolearn sull'eliminazione di nomi di dominio, leggere [gestire nomi di dominio personalizzato](active-directory-domains-manage-azure-portal.md).    

## <a name="add-more-custom-domain-names"></a>Aggiungere altri nomi di dominio personalizzati
Se l'organizzazione utilizza più nomi di dominio personalizzato, ad esempio 'contoso.com' e 'contosobank.com', è possibile aggiungere backup tooa al massimo 900 nomi di dominio. Utilizzare hello stessi passaggi in questo articolo tooadd ogni nome di dominio.

## <a name="next-steps"></a>Passaggi successivi
[Gestire i nomi di dominio personalizzati](active-directory-domains-manage-azure-portal.md)

