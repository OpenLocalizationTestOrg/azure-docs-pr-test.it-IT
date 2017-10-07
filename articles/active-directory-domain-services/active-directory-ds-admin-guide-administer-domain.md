---
title: 'Servizi di dominio Azure Active Directory: amministrare un dominio gestito | Documentazione Microsoft'
description: Amministrare i domini gestiti di Servizi di dominio Azure Active Directory
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4fdbc75-3e6b-4e20-8494-5dcc3bf2220a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 11acc79e06163e3193b1aa981f2cd28af812789d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="administer-an-azure-active-directory-domain-services-managed-domain"></a>Amministrare un dominio gestito di Servizi di dominio Azure Active Directory
Questo articolo illustra la modalità di gestione dominio tooadminister un servizi di dominio Azure Active Directory (AD).

## <a name="before-you-begin"></a>Prima di iniziare
attività di hello tooperform elencate in questo articolo, è necessario:

1. Una **sottoscrizione di Azure**valida.
2. Una **directory di Azure AD** sincronizzata con una directory locale o con una directory solo cloud.
3. **Servizi di dominio AD Azure** deve essere abilitato per la directory hello Azure AD. Se non è ancora fatto, seguire tutte le attività descritte nella hello hello [Guida introduttiva](active-directory-ds-getting-started.md).
4. Oggetto **dominio macchina virtuale** da cui amministrare hello dominio gestito di servizi di dominio Azure Active Directory. Se non si dispone di questo tipo di una macchina virtuale, seguire tutte le attività hello descritte nell'articolo hello intitolata [aggiunta a un dominio gestito di macchina virtuale tooa Windows](active-directory-ds-admin-guide-join-windows-vm.md).
5. Sono necessarie le credenziali di hello di un **gruppo 'Administrators di controller di dominio di AAD' dell'utente account appartenenti toohello** nella directory, tooadminister il dominio gestito.

<br>

## <a name="administrative-tasks-you-can-perform-on-a-managed-domain"></a>Attività amministrative che è possibile eseguire in un dominio gestito
I membri del gruppo 'Administrators di controller di dominio di AAD' hello vengono concessi privilegi sul dominio gestito hello che consentono loro tooperform attività, ad esempio:

* Aggiungere computer al dominio gestito toohello.
* Configurare hello incorporato oggetto Criteri di gruppo per i contenitori di hello 'AADDC utenti' e 'AADDC computer' nel dominio gestito hello.
* Amministrare DNS nel dominio gestito hello.
* Creare e amministrare personalizzato unità organizzative (OU) nel dominio gestito hello.
* Miglioramento accesso amministrativo toocomputers aggiunti a un dominio gestito toohello.

## <a name="administrative-privileges-you-do-not-have-on-a-managed-domain"></a>Privilegi amministrativi non disponibili in un dominio gestito
dominio Hello è gestito da Microsoft, incluse le attività, ad esempio l'applicazione di patch, monitoraggio e l'esecuzione di backup. Pertanto, dominio hello è bloccato e non si dispone tooperform privilegi certe attività amministrative di dominio hello. Ecco alcuni esempi di attività che non è possibile eseguire.

* Non vengono concessi privilegi di amministratore di dominio o l'amministratore dell'organizzazione per il dominio gestito hello.
* È possibile estendere schema hello del dominio gestito hello.
* È possibile connettersi controller toodomain per hello dominio gestito tramite Desktop remoto.
* È possibile aggiungere dominio gestito toohello i controller di dominio.

## <a name="task-1---provision-a-domain-joined-windows-server-virtual-machine-tooremotely-administer-hello-managed-domain"></a>Attività 1: eseguire il provisioning di un dominio tooremotely macchina virtuale di Windows Server amministrare dominio gestito hello
Domini gestiti di servizi di dominio AD Azure possono essere gestiti tramite i familiari strumenti di amministrazione di Active Directory, ad esempio Active Directory amministrativi centro hello o PowerShell di Active Directory. Gli amministratori tenant non sono controller di privilegi tooconnect toodomain hello dominio gestito tramite Desktop remoto. Di conseguenza, i membri del gruppo 'Administrators di controller di dominio di AAD' può amministrare hello gestiti in remoto mediante strumenti di amministrazione di Active Directory da un computer Windows Server/client che è dominio gestito toohello unita in join i domini. Strumenti di amministrazione di Active Directory possono essere installati come parte della funzionalità facoltativa strumenti di amministrazione remota Server (RSAT) di hello sui computer Windows Server e client aggiunti a un dominio toohello gestito.

primo passaggio Hello è tooset rapidamente una macchina virtuale di Windows Server che è unita in join toohello gestito dominio. Per istruzioni, consultare l'articolo toohello [aggiunta a un dominio gestito servizi di dominio Azure Active Directory di Windows Server macchina virtuale tooan](active-directory-ds-admin-guide-join-windows-vm.md).

### <a name="remotely-administer-hello-managed-domain-from-a-client-computer-for-example-windows-10"></a>Amministrare in remoto hello di dominio gestiti da un computer client (ad esempio, Windows 10)
istruzioni di Hello in questo articolo utilizzano un hello tooadminister macchina virtuale di Windows Server AAD di dominio Active Directory gestito dominio. Tuttavia, è possibile anche scegliere toouse un toodo di macchina virtuale client (ad esempio, Windows 10) di Windows in modo.

È possibile [installare strumenti di amministrazione remota Server (RSAT)](http://social.technet.microsoft.com/wiki/contents/articles/2202.remote-server-administration-tools-rsat-for-windows-client-and-windows-server-dsforum2wiki.aspx) in una macchina virtuale di Windows client seguendo le istruzioni di hello su TechNet.

## <a name="task-2---install-active-directory-administration-tools-on-hello-virtual-machine"></a>Attività 2: strumenti di amministrazione di Active Directory di installazione nella macchina virtuale hello
Eseguire hello seguenti strumenti di amministrazione di Active Directory di passaggi tooinstall hello nella macchina virtuale di hello aggiunti a un dominio. Per altre [informazioni sull'installazione e l'utilizzo degli strumenti di amministrazione remota del server](https://technet.microsoft.com/library/hh831501.aspx), vedere Technet.

1. Passare troppo**macchine virtuali** nodo hello portale di Azure classico. Selezionare una macchina virtuale hello creato nell'attività 1 e fare clic su **Connetti** hello barra dei comandi nella parte inferiore di hello della finestra hello.

    ![Connettere la macchina virtuale di tooWindows](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. portale classico Hello richiede tooopen o salvare un file con estensione 'RDP', che è usato tooconnect toohello virtual machine. Dopo aver terminato il download, fare clic su file hello tooopen.
3. Al prompt di accesso hello, utilizzare le credenziali di hello di un utente appartenente gruppo 'Administrators di controller di dominio di AAD' toohello. Ad esempio, utilizziamo 'bob@domainservicespreview.onmicrosoft.com' in questo caso.
4. Dalla schermata Start hello, aprire **Server Manager**. Fare clic su **Aggiungi ruoli e funzionalità** nel riquadro centrale di hello della finestra di Server Manager hello.

    ![Avviare Server Manager nella macchina virtuale](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. In hello **prima di iniziare** pagina di hello **Aggiunta guidata ruoli e funzionalità**, fare clic su **Avanti**.

    ![Pagina Prima di iniziare](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. In hello **tipo di installazione** , mantenere hello **installazione basata su ruoli o basata su funzionalità** opzione selezionata e fare clic su **Avanti**.

    ![Pagina Tipo di installazione](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. In hello **selezione Server** pagina, selezionare la macchina virtuale corrente hello dal pool di server hello e fare clic su **Avanti**.

    ![Pagina Selezione dei server](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. In hello **i ruoli del Server** pagina, fare clic su **Avanti**. Questa pagina viene ignorata perché l'installazione di ruoli in server hello è stiamo non.
9. In hello **funzionalità** pagina, fare clic su hello tooexpand **strumenti di amministrazione remota del Server** nodo e quindi fare clic su hello tooexpand **strumenti di amministrazione ruoli** nodo. Selezionare **di dominio Active Directory e gli strumenti di AD LDS** funzionalità dall'elenco di hello di strumenti di amministrazione ruoli.

    ![Pagina Funzionalità](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-ad-tools.png)
10. In hello **conferma** pagina, fare clic su **installare** tooinstall hello Active Directory e AD LDS funzionalità nella macchina virtuale hello. Al completamento dell'installazione della funzionalità, fare clic su **Chiudi** tooexit hello **Aggiungi ruoli e funzionalità** procedura guidata.

    ![Pagina di conferma](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-confirmation.png)

## <a name="task-3---connect-tooand-explore-hello-managed-domain"></a>Attività 3: connettere tooand esplorare dominio gestito hello
Ora che sono installati strumenti di amministrazione di Active Directory hello hello dominio unito macchina virtuale, è possibile utilizzare questi strumenti tooexplore e amministrare dominio gestito hello.

> [!NOTE]
> È necessario toobe un membro del gruppo 'Administrators di controller di dominio di AAD' hello, hello tooadminister gestiti dominio.
>
>

1. Dalla schermata Start hello, fare clic su **strumenti di amministrazione**. Dovrebbe essere hello AD installati strumenti di amministrazione sulla macchina virtuale hello.

    ![Strumenti di amministrazione installati nel server](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. Fare clic su **Centro di amministrazione di Active Directory**.

    ![Centro di amministrazione di Active Directory](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. dominio hello tooexplore, fare clic sul nome di dominio hello nel riquadro di sinistra hello (ad esempio, ' contoso100.com'). Si noti che due contenitori si chiamano rispettivamente "AADDC Computers" e "AADDC Users".

    ![Centro di amministrazione di Active Directory - Visualizza dominio](./media/active-directory-domain-services-admin-guide/adac-domain-view.png)
4. Fare clic sul contenitore hello chiamato **AADDC utenti** toosee tutti gli utenti e gruppi appartenenti toohello gestiti dominio. In questo contenitore verranno visualizzati gli account utente e gruppi del tenant Azure Active Directory. Si noti che in questo esempio, un account utente per l'utente hello chiamato "bob" e il gruppo 'Administrators di controller di dominio di AAD' sono disponibili in questo contenitore.

    ![Centro di amministrazione di Active Directory - Utenti del dominio](./media/active-directory-domain-services-admin-guide/adac-aaddc-users.png)
5. Fare clic sul contenitore hello chiamato **AADDC computer** computer hello toosee aggiunti a un dominio gestito toothis. Verrà visualizzata una voce per la macchina virtuale corrente hello, ovvero toohello aggiunti a un dominio. Gli account computer per tutti i computer aggiunti toohello servizi di dominio Azure Active Directory dominio gestiti vengono archiviati nel contenitore 'AADDC computer'.

    ![Centro di amministrazione di Active Directory - Computer aggiunti al dominio](./media/active-directory-domain-services-admin-guide/adac-aaddc-computers.png)

<br>

## <a name="related-content"></a>Contenuti correlati
* [Guida introduttiva di Azure AD Domain Services](active-directory-ds-getting-started.md)
* [Aggiunta a un dominio gestito con servizi di dominio Active Directory di Azure tooan Windows Server macchina virtuale](active-directory-ds-admin-guide-join-windows-vm.md)
* [Distribuire strumenti di amministrazione remota del server](https://technet.microsoft.com/library/hh831501.aspx)
