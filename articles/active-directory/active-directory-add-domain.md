---
title: nome di dominio personalizzato aaaAdd tooAzure Active Directory | Documenti Microsoft
description: "Come tooadd della società nomi di dominio Active Directory tooAzure e come tooverify hello nome di dominio."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 35a6e20a-9907-432b-9d36-16b916a5c249
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: eb208138f2633aaecc54f68dc947caf80d856d23
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
> 

Hai uno o più nomi di dominio che l'organizzazione utilizza toodo business e gli utenti accedono tooyour rete aziendale usa il nome di dominio aziendale. Ora che si sta usando Azure Active Directory (Azure AD), è possibile aggiungere il dominio aziendale nome tooAzure AD anche. In questo modo è tooassign nomi utente nella directory hello sono tooyour familiarità, ad esempio 'alice@contoso.com.' il processo di Hello è semplice:

1. Aggiungere directory tooyour nome di dominio personalizzato hello
2. Aggiungere una voce DNS per il nome di dominio di hello al registrar di nomi di dominio hello
3. Verificare il nome di dominio personalizzato hello in Azure AD

> [!IMPORTANT]
> Si consiglia di gestire Azure AD usando la hello [centro di amministrazione di Azure AD](https://aad.portal.azure.com) in hello portale di Azure anziché hello portale di Azure classico a cui fa riferimento in questo articolo. Per la modalità tooadd il nome di dominio della società nel centro di amministrazione di hello Azure AD, vedere [l'assegnazione di ruoli di amministratore in Azure Active Directory](active-directory-domains-add-azure-portal.md).

Se si intende tooconfigure il toobe nome di dominio personalizzato utilizzato con Active Directory Federation Services (ADFS) o un servizio token di sicurezza diversi (STS) nella rete aziendale, seguire le istruzioni hello [aggiungere e configurare un dominio per federazione con Azure Active Directory](active-directory-add-domain-federated.md). Ciò è utile se si prevede di toosynchronize utenti dal tooAzure directory aziendale AD, e [sincronizzazione degli hash delle password](active-directory-aadconnectsync-implement-password-synchronization.md) non soddisfano i requisiti.

## <a name="add-a-custom-domain-name-tooyour-directory"></a>Aggiungere una directory tooyour nome di dominio personalizzato
1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com/) con un account utente che è un amministratore globale della directory di Azure AD.
2. In **Active Directory**, aprire la directory e selezionare hello **domini** scheda.
3. Nella barra dei comandi di hello, selezionare **Aggiungi**. Immettere il nome di hello del dominio personalizzato, ad esempio 'contoso.com'. Assicurarsi che tooinclude hello. com, .net o altra estensione di livello superiore, quindi lasciare hello casella di controllo "single sign-on" (federazione) è deselezionata.
4. Selezionare **Aggiungi**.
5. Hello seconda pagina della procedura guidata Aggiungi dominio hello, ottenere hello voce DNS che Azure AD utilizzerà tooverify che l'azienda dispone di nome di dominio personalizzato hello.

Dopo aver aggiunto il nome di dominio di hello, Azure AD deve verificare che il nome di dominio hello proprietà dell'organizzazione. Prima di Azure AD è possibile eseguire questa verifica, è necessario aggiungere una voce DNS nel file di zona DNS hello hello nome di dominio. Questa attività viene eseguita nel sito Web di hello per nome di dominio per il nome di dominio di hello.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Aggiungere una voce DNS hello presso hello registrar per dominio hello
nome di dominio personalizzato con Azure AD Hello successivo passaggio toouse è file di zona DNS hello tooupdate per dominio hello. In questo modo l'azienda dispone di nome di dominio personalizzato hello tooverify di Azure AD.

1. Accedi toohello registrar di nomi di dominio per il dominio hello. Se non si dispone di hello tooupdate accesso voce DNS, chiedere persona hello o team che dispone di questo passaggio toocomplete accesso 2 e toolet che quando viene completato il processo.
2. File di zona DNS hello aggiornamento per il dominio hello aggiungendo la voce DNS hello fornite tooyou da Azure AD. Questa voce DNS consente AD Azure tooverify le proprietà di dominio di hello. Hello voce DNS non modifica eventuali comportamenti, ad esempio routing della posta elettronica o di hosting web.

Per informazioni su questa voce DNS di hello aggiunta, leggere [istruzioni per l'aggiunta di una voce DNS nel Registrar comuni di DNS](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Verificare il nome di dominio hello con Azure AD
Dopo aver aggiunto voce DNS hello, si è pronti tooverify nome di dominio hello con Azure AD.

Se si dispone ancora di hello **Aggiungi dominio** procedura guidata, aprire seleziona **verificare** pagina terzo hello, della creazione guidata hello. Quando si seleziona **verificare**, Azure AD verrà eseguita una ricerca voce DNS hello nel file di zona DNS hello per dominio hello. Azure AD è possibile verificare il nome di dominio hello solo dopo avere propagato record DNS hello. La propagazione richiede spesso solo qualche secondo, ma a volte può richiedere più di un'ora. Se la verifica non funziona hello prima volta, riprovare più tardi.

Se hello **Aggiungi dominio** procedura guidata non è ancora aperta, è possibile verificare il dominio hello in hello [portale di Azure classico](https://manage.windowsazure.com/):

1. Accedere con un account utente amministratore globale per la directory di Azure AD.
2. Aprire la directory e seleziona di hello **domini** scheda.
3. Nome di dominio selezionare hello tooverify desiderati e selezionare **verificare** hello barra dei comandi.
4. Selezionare **verificare** hello della finestra di dialogo toocomplete hello di verifica.

A questo punto è possibile [assegnare nomi utente che includono il nome di dominio personalizzato](active-directory-add-domain-add-users.md).

## <a name="troubleshooting"></a>Risoluzione dei problemi
Se non è possibile verificare un nome di dominio personalizzato, provare l'esempio hello. Si inizierà con hello più comune e di lavoro verso il basso toohello comune.

1. **Attendere un'ora**. I record DNS necessario toopropagate prima di Azure AD è possibile verificare il dominio hello. Questa operazione potrebbe richiedere più di un'ora.
2. **Verificare i record DNS è stato immesso hello e che sia corretto**. Completare il passaggio al sito Web di hello per hello registrar per dominio hello. Azure AD non è possibile verificare il nome di dominio hello se hello voce DNS non è presente in hello file di zona DNS o se non è una corrispondenza esatta con la voce DNS hello fornito ad Azure AD. Se non si dispone di accesso tooupdate i record DNS hello dominio al registrar di nomi di dominio hello, condividere una voce DNS hello con hello persona o team dell'organizzazione che ha l'accesso e chiedere voce DNS di hello tooadd.
3. **Eliminare il nome di dominio di hello da un'altra directory di Azure AD**. Un nome di dominio può essere verificato solo in una directory. Se un nome di dominio è già stato verificato in un'altra directory, è necessario eliminarlo prima di poterlo verificare nella nuova directory. toolearn sull'eliminazione di nomi di dominio, leggere [gestire nomi di dominio personalizzato](active-directory-add-manage-domain-names.md).

## <a name="add-more-custom-domain-names"></a>Aggiungere altri nomi di dominio personalizzati
Se l'organizzazione utilizza più nomi di dominio personalizzato, ad esempio 'contoso.com' e 'contosobank.com', è possibile aggiungere backup tooa al massimo 900 nomi di dominio. Utilizzare hello stessi passaggi in questo articolo tooadd ogni nome di dominio.

## <a name="next-steps"></a>Passaggi successivi
* [Assegnare nomi utente che includono il nome di dominio personalizzato](active-directory-add-domain-add-users.md)
* [Gestire i nomi di dominio personalizzati](active-directory-add-manage-domain-names.md)
* [Informazioni sui concetti relativi alla gestione dei domini in Azure AD](active-directory-add-domain-concepts.md)
* [Aggiungere informazioni personalizzate distintive dell'azienda alla pagina di accesso e al pannello di accesso](active-directory-add-company-branding.md)
* [Utilizzare PowerShell toomanage i nomi di dominio in Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

