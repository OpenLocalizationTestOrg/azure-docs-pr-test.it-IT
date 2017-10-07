---
title: aaaAdd il nome di dominio personalizzato e impostare tooAzure federato Accedi Active Directory | Documenti Microsoft
description: "Come tooadd della società nomi di dominio tooAzure tooset di Active Directory backup Accedi federativa tra Azure Active Directory e la soluzione di federazione on-premise"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 27126c7e-e6d6-4ef3-a4fb-f5f0706e749d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 77f8cc87c27871ac96581360762aaa8d24c0eb8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-your-custom-domain-name-tooazure-active-directory"></a>Aggiungere il tooAzure nome di dominio personalizzato Active Directory
È possibile configurare un nome di dominio personalizzato, ad esempio 'contoso.com', in modo che gli utenti in contoso.com possano avere un'esperienza di accesso Single Sign-On federato dalla rete aziendale. Se si dispone già di Active Directory Federation Services (ADFS) o un server di federazione diversi in esecuzione nella rete aziendale, è possibile configurare il nome di dominio personalizzato utilizzando lo strumento Azure AD Connect hello toouse di Azure AD. È possibile utilizzare l'ambiente di Azure AD Connect toodeploy una nuova istanza di ADFS e configurare per federato single sign-on tooAzure Active Directory.

Se non si dispone e non prevede toodeploy AD FS o un altro server federativo, seguire queste istruzioni: [aggiungere tooAzure di nome Active Directory un dominio personalizzato](active-directory-add-domain.md).

## <a name="add-a-custom-domain-name-tooyour-directory"></a>Aggiungere una directory tooyour nome di dominio personalizzato
1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com/) con un account utente che è un amministratore globale della directory di Azure AD.
2. In **Active Directory**, aprire la directory e selezionare hello **domini** scheda.
3. Nella barra dei comandi di hello, selezionare **Aggiungi**, quindi immettere il nome di hello del dominio personalizzato, ad esempio 'contoso.com'. Essere certi tooinclude hello COM, .net o altre estensioni di livello superiore.
4. Seleziona hello **intendo tooconfigure questo dominio per single sign-on con il controller di dominio Active Directory locale** casella di controllo.
5. Selezionare **Aggiungi**.

Eseguire una voce DNS di hello Azure AD Connect strumento tooget hello ad Azure AD utilizzerà dominio hello tooverify. Si noterà una voce DNS hello in hello **dominio Azure Active Directory** passaggio nella creazione guidata hello. È possibile visualizzare il passaggio nella creazione guidata hello simile [in queste istruzioni](connect/active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation). Se non si dispone di strumento di hello Azure AD Connect, è possibile [scaricarlo qui](http://go.microsoft.com/fwlink/?LinkId=615771).

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Aggiungere una voce DNS hello presso hello registrar per dominio hello
nome di dominio personalizzato con Azure AD Hello successivo passaggio toouse è file di zona DNS hello tooupdate per dominio hello. In questo modo l'azienda dispone di nome di dominio personalizzato hello tooverify di Azure AD.

1. Eseguire l'accesso del sito Web toohello per registrar del nome di dominio. Se non si ha accesso toodo questo, chiedere hello persona o team nell'organizzazione che dispone di questo passaggio toocomplete accesso 2 e toolet che quando viene completato il processo.
2. File di zona DNS hello aggiornamento per il dominio hello aggiungendo la voce DNS hello fornite tooyou da Azure AD. Questa voce DNS consente AD Azure tooverify le proprietà di dominio di hello. Hello voce DNS non modifica eventuali comportamenti, ad esempio routing della posta elettronica o di hosting web.

Per informazioni su questo passaggio, vedere [Creare record DNS per Office 365 quando si gestiscono i record DNS](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Verificare il nome di dominio hello con Azure AD
Dopo aver aggiunto voce DNS hello, si è pronti tooverify nome di dominio hello con Azure AD.

dominio di hello tooverify, selezionare **Avanti** su hello **dominio Azure Active Directory** passaggio della procedura guidata di hello Azure AD Connect. Cerca voce DNS hello nel file di zona DNS hello per dominio hello Azure AD. Azure AD verificare il nome di dominio di hello solo dopo aver propagato record DNS hello. La propagazione richiede spesso solo qualche secondo, ma a volte può richiedere più di un'ora. Se la verifica non funziona hello prima volta, riprovare più tardi.

Procedere quindi con hello rimanenti passaggi nella procedura guidata di Azure AD Connect hello. Questo comando sincronizzerà agli utenti il tooAzure di Windows Server AD Active Directory. Gli utenti sincronizzati nel dominio hello che è configurato per la federazione sarà in grado di tooget un single sign-on federato di esperienza derivata dal tooAzure della rete aziendale AD.

## <a name="troubleshooting"></a>Risoluzione dei problemi
Se non è possibile verificare un nome di dominio personalizzato, provare l'esempio hello. Si inizierà con hello più comune e di lavoro verso il basso toohello comune.

1. **Attendere un'ora**. I record DNS necessario toopropagate prima di Azure AD è possibile verificare il dominio hello. Questa operazione potrebbe richiedere più di un'ora.
2. **Verificare i record DNS è stato immesso hello e che sia corretto**. Completare il passaggio al sito Web di hello per hello registrar per dominio hello. Azure AD non è possibile verificare il nome di dominio hello se hello voce DNS non è presente in hello file di zona DNS o se non è una corrispondenza esatta con la voce DNS hello fornito ad Azure AD. Se non si dispone di accesso tooupdate i record DNS hello dominio al registrar di nomi di dominio hello, condividere una voce DNS hello con hello persona o team dell'organizzazione che ha l'accesso e chiedere voce DNS di hello tooadd.
3. **Eliminare il nome di dominio di hello da un'altra directory di Azure AD**. Un nome di dominio può essere verificato solo in una directory. Se un nome di dominio è già stato verificato in un'altra directory, è necessario eliminarlo prima di poterlo verificare nella nuova directory. toolearn sull'eliminazione di nomi di dominio, leggere [gestire nomi di dominio personalizzato](active-directory-add-manage-domain-names.md).

## <a name="add-more-custom-domain-names"></a>Aggiungere altri nomi di dominio personalizzati
Se l'organizzazione utilizza più nomi di dominio personalizzato, ad esempio 'contoso.com' e 'contosobank.com', è possibile aggiungere backup tooa al massimo 900 nomi di dominio. Utilizzare hello stessi passaggi in questo articolo tooadd ogni nome di dominio.

## <a name="next-steps"></a>Passaggi successivi
* [Gestire i nomi di dominio personalizzati](active-directory-add-manage-domain-names.md)
* [Informazioni sui concetti relativi alla gestione dei domini in Azure AD](active-directory-add-domain-concepts.md)
* [Aggiungere informazioni personalizzate distintive dell'azienda alla pagina di accesso e al pannello di accesso](active-directory-add-company-branding.md)
* [Utilizzare PowerShell toomanage i nomi di dominio in Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

