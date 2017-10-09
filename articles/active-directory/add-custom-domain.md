---
title: aaaAdd tooAzure un dominio personalizzato AD | Documenti Microsoft
description: Viene illustrato come tooadd un dominio personalizzato in Azure Active Directory.
services: active-directory
author: jeffgilb
manager: femila
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 878cecad364ec47f1c6755d742aaccbce627dc5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-a-custom-domain-name-tooazure-active-directory"></a>Guida introduttiva: Aggiungere un tooAzure di nome di dominio personalizzato Active Directory

Tutte le directory di Azure AD viene fornito con un nome di dominio iniziale nel formato hello *domainname*. c o m. nome di dominio iniziale hello non può essere modificato o eliminato, ma è possibile aggiungere il dominio aziendale nome tooAzure AD anche. Ad esempio, l'organizzazione ha probabilmente altri business toodo utilizzati nomi di dominio e gli utenti che accedono utilizzando il nome di dominio aziendale. Aggiunta di nomi di dominio personalizzato tooAzure AD consente tooassign nomi utente nella directory hello sono tooyour familiarità, ad esempio 'alice@contoso.com.' invece di "alice@*<domain name>*.onmicrosoft.com". il processo di Hello è semplice:

1. Aggiungere directory tooyour nome di dominio personalizzato hello
2. Aggiungere una voce DNS per il nome di dominio di hello al registrar di nomi di dominio hello
3. Verificare il nome di dominio personalizzato hello in Azure AD

## <a name="add-your-custom-domain"></a>Aggiungere il dominio personalizzato
1. Accedi toohello [portale di Azure](https://portal.azure.com) con un account che sia un amministratore globale per la directory di hello.
2. Selezionare **più servizi**, immettere **Azure Active Directory** nella casella di testo hello e quindi selezionare **invio**.
   
   ![Apertura di Gestione utenti](./media/active-directory-domains-add-azure-portal/user-management.png)
3. In hello ***nome directory*** pannello seleziona **i nomi di dominio**.
4. In hello  ***nome directory* -i nomi di dominio** blade, seleziona hello **Aggiungi** comando.
   
   ![Comando Aggiungi hello](./media/active-directory-domains-add-azure-portal/add-command.png)
5. In hello **nome di dominio** pannello, immettere il nome di hello del dominio personalizzato nella casella hello, ad esempio 'contoso.com' e quindi selezionare **Aggiungi dominio**. Essere certi tooinclude hello COM, .net o altre estensioni di livello superiore.
6. In hello ***nome di dominio*** blade (con il nome di dominio personalizzato nel titolo hello), ottenere hello DNS voce informazioni toouse tooverify che l'azienda dispone di nome di dominio personalizzato hello.
   
   ![ottenere informazioni relative alla voce DNS](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

> [!TIP]
> Se si prevede di toofederate locale Windows Server Active Directory con Azure AD, quindi è necessario hello tooselect **intendo tooconfigure questo dominio per single sign-on con il controller di dominio Active Directory locale** casella di controllo quando si esegue lo strumento di hello Azure AD Connect toosynchronize le directory. È inoltre necessario tooregister hello stesso nome di dominio selezionato per la federazione con la directory locale in hello **dominio Azure Active Directory** passaggio nella creazione guidata hello. È possibile visualizzare il passaggio nella creazione guidata hello simile [in queste istruzioni](./connect/active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation). Se non si dispone di strumento di hello Azure AD Connect, è possibile [scaricarlo qui](http://go.microsoft.com/fwlink/?LinkId=615771).

Dopo aver aggiunto il nome di dominio di hello, Azure AD deve verificare che il nome di dominio hello proprietà dell'organizzazione. Prima di Azure AD è possibile eseguire questa verifica, è necessario aggiungere una voce DNS nel file di zona DNS hello hello nome di dominio. Questa attività viene eseguita nel sito Web di hello per nome di dominio per il nome di dominio di hello.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Aggiungere una voce DNS hello presso hello registrar per dominio hello
nome di dominio personalizzato con Azure AD Hello successivo passaggio toouse è file di zona DNS hello tooupdate per dominio hello. Azure AD consente di verificare che il nome di dominio personalizzato hello proprietà dell'organizzazione.

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
4. In hello ***nome di dominio*** blade (vale a dire hello pannello visualizzato con il nuovo nome di dominio nel titolo hello), selezionare **verificare** verifica hello toocomplete.

> [!TIP]
> È possibile aggiungere nomi di dominio personalizzato too900, ma solo uno può essere [impostato come nome di dominio primario hello per le directory di Azure AD](active-directory-domains-manage-azure-portal.md#set-the-primary-domain-name-for-your-azure-ad-directory) utilizzato per impostazione predefinita, quando si creano nuovi account.

È ora possibile usare il nome di dominio personalizzato per creare account utente basati sul cloud o per aggiornare le informazioni degli account utente locali precedentemente sincronizzate. È inoltre possibile modificare sincronizzati in precedenza account utente dominio suffisso informazioni utilizzando [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) o hello [API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="troubleshooting"></a>Risoluzione dei problemi
Se non è possibile verificare un nome di dominio personalizzato, provare a hello risoluzione dei problemi relativi alla procedura seguente:

1. **Attendere un'ora**. I record DNS necessario toopropagate prima di Azure AD è possibile verificare il dominio hello. Questa operazione potrebbe richiedere più di un'ora.
2. **Verificare i record DNS è stato immesso hello e che sia corretto**. Completare il passaggio al sito Web di hello per hello registrar per dominio hello. Azure AD non è possibile verificare il nome di dominio hello se hello voce DNS non è presente in hello file di zona DNS o se non è una corrispondenza esatta con la voce DNS hello fornito ad Azure AD. Se non si dispone di accesso tooupdate i record DNS hello dominio al registrar di nomi di dominio hello, condividere una voce DNS hello con hello persona o team dell'organizzazione che ha l'accesso e chiedere voce DNS di hello tooadd.
3. **Eliminare il nome di dominio di hello da un'altra directory di Azure AD**. Un nome di dominio può essere verificato solo in una directory. Se un nome di dominio è già stato verificato in un'altra directory, è necessario eliminarlo prima di poterlo verificare nella nuova directory. toolearn sull'eliminazione di nomi di dominio, leggere [gestire nomi di dominio personalizzato](active-directory-domains-manage-azure-portal.md).    

## <a name="add-more-custom-domain-names"></a>Aggiungere altri nomi di dominio personalizzati
Se l'organizzazione utilizza più di un nome di dominio personalizzato, ad esempio 'contoso.com' e 'contosobank.com', è possibile aggiungere più backup too900 ripetendo i passaggi di hello in questo articolo per ognuno.

### <a name="learn-more"></a>Altre informazioni
[Panoramica concettuale dei nomi di dominio personalizzati in Azure AD](active-directory-add-domain-concepts.md)

[Gestire i nomi di dominio personalizzati](active-directory-domains-manage-azure-portal.md)


## <a name="next-steps"></a>Passaggi successivi
In questa Guida rapida, si è appreso come tooadd tooAzure un dominio personalizzato AD. 

È possibile utilizzare hello seguente collegamento tooadd un nuovo dominio personalizzato in Azure AD dal portale di Azure hello.

> [!div class="nextstepaction"]
> [Aggiungere un dominio personalizzato](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/QuickStart) 