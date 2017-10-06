---
title: 'Azure Active Directory Domain Services: amministrare Criteri di gruppo in domini gestiti | Microsoft Docs'
description: Amministrare Criteri di gruppo in domini gestiti di Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d56ebf27e3015a7f3385ac5a4ddd77ea2c88387f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="administer-group-policy-on-an-azure-ad-domain-services-managed-domain"></a>Amministrare Criteri di gruppo in un dominio gestito di Azure AD Domain Services
Azure Active Directory Domain Services include predefinite dei criteri di gruppo (GPO) per i contenitori di hello 'AADDC utenti' e 'AADDC computer'. È possibile personalizzare queste tooconfigure oggetti Criteri di gruppo predefinite dei criteri di gruppo nel dominio gestito hello. Inoltre, i membri del gruppo 'Administrators di controller di dominio di AAD' hello è possono creare le proprie unità organizzative personalizzate nel dominio gestito hello. Possono inoltre creare oggetti Criteri di gruppo personalizzato e collegarli personalizzato toothese unità organizzative. Gli utenti appartenenti al gruppo 'Administrators di controller di dominio di AAD' toohello vengono concessi privilegi di amministrazione di criteri di gruppo nel dominio gestito hello.

## <a name="before-you-begin"></a>Prima di iniziare
attività di hello tooperform elencate in questo articolo, è necessario:

1. Una **sottoscrizione di Azure**valida.
2. Una **directory di Azure AD** sincronizzata con una directory locale o con una directory solo cloud.
3. **Servizi di dominio AD Azure** deve essere abilitato per la directory hello Azure AD. Se non è ancora fatto, seguire tutte le attività descritte nella hello hello [Guida introduttiva](active-directory-ds-getting-started.md).
4. Oggetto **dominio macchina virtuale** da cui amministrare hello dominio gestito di servizi di dominio Azure Active Directory. Se non si dispone di questo tipo di una macchina virtuale, seguire tutte le attività hello descritte nell'articolo hello intitolata [aggiunta a un dominio gestito di macchina virtuale tooa Windows](active-directory-ds-admin-guide-join-windows-vm.md).
5. Sono necessarie le credenziali di hello di un **gruppo 'Administrators di controller di dominio di AAD' dell'utente account appartenenti toohello** nella directory, tooadminister criteri di gruppo per il dominio gestito.

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-group-policy-for-hello-managed-domain"></a>Attività 1: eseguire il provisioning di una macchina virtuale di dominio di tooremotely amministrare criteri di gruppo per il dominio gestito hello
Domini gestiti di servizi di dominio AD Azure possono essere gestiti in remoto mediante familiari strumenti di amministrazione di Active Directory, ad esempio hello Active Directory amministrativi centro o PowerShell di Active Directory. Analogamente, è possibile amministrare i criteri di gruppo per il dominio gestito hello in remoto mediante strumenti di amministrazione di criteri di gruppo hello.

Gli amministratori di directory di Azure AD non sono controller di privilegi tooconnect toodomain hello dominio gestito tramite Desktop remoto. I membri del gruppo 'Administrators di controller di dominio di AAD' hello possono amministrare criteri di gruppo per i domini gestiti in modalità remota. Possono utilizzare gli strumenti di criteri di gruppo in un dominio gestito di Windows Server/client computer toohello unita in join. Gli strumenti di criteri di gruppo possono essere installati come parte della funzionalità facoltativa di hello Gestione criteri di gruppo nei computer Windows Server e client aggiunti a un dominio gestito toohello.

Hello prima attività è tooprovision una macchina virtuale di Windows Server di dominio gestiti toohello unita in join. Per istruzioni, consultare l'articolo toohello [aggiunta a un dominio gestito servizi di dominio Azure Active Directory di Windows Server macchina virtuale tooan](active-directory-ds-admin-guide-join-windows-vm.md).

## <a name="task-2---install-group-policy-tools-on-hello-virtual-machine"></a>Attività 2: strumenti di criteri di gruppo installazione nella macchina virtuale hello
Eseguire hello seguendo gli strumenti di amministrazione di criteri di gruppo di passaggi tooinstall hello nella macchina virtuale di hello aggiunti a un dominio.

1. Passare troppo**macchine virtuali** nodo hello portale di Azure classico. Selezionare una macchina virtuale hello creato nell'attività 1 e fare clic su **Connetti** hello barra dei comandi nella parte inferiore di hello della finestra hello.

    ![Connettere la macchina virtuale di tooWindows](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. portale classico Hello richiede tooopen o salvare un file con estensione 'RDP', che è usato tooconnect toohello virtual machine. Dopo aver terminato il download, fare clic su file hello.
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
9. In hello **funzionalità** pagina, seleziona hello **Gestione criteri di gruppo** funzionalità.

    ![Pagina Funzionalità](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management.png)
10. In hello **conferma** pagina, fare clic su **installare** funzionalità di gestione criteri di gruppo tooinstall hello nella macchina virtuale hello. Al completamento dell'installazione della funzionalità, fare clic su **Chiudi** tooexit hello **Aggiungi ruoli e funzionalità** procedura guidata.

    ![Pagina di conferma](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management-confirmation.png)

## <a name="task-3---launch-hello-group-policy-management-console-tooadminister-group-policy"></a>Attività 3 - avviare hello Group Policy management console tooadminister criteri di gruppo
È possibile utilizzare console Gestione criteri di gruppo di hello in hello dominio macchina virtuale tooadminister criteri di gruppo nel dominio gestito hello.

> [!NOTE]
> È necessario un membro del gruppo di hello 'AAD DC Administrators', criteri di gruppo nel dominio gestito hello tooadminister toobe.
>
>

1. Dalla schermata Start hello, fare clic su **strumenti di amministrazione**. Dovrebbe essere hello **Gestione criteri di gruppo** console installata nella macchina virtuale hello.

    ![Avviare Gestione Criteri di gruppo](./media/active-directory-domain-services-admin-guide/gp-management-installed.png)
2. Fare clic su **Gestione criteri di gruppo** console Gestione criteri di gruppo di toolaunch hello.

    ![Console Criteri di gruppo](./media/active-directory-domain-services-admin-guide/gp-management-console.png)

## <a name="task-4---customize-built-in-group-policy-objects"></a>Attività 4: personalizzare gli Oggetti Criteri di gruppo predefiniti
Esistono due predefinite dei criteri di gruppo (GPO) - uno per i contenitori 'AADDC utenti' e 'AADDC computer' hello nel dominio gestito. È possibile personalizzare i criteri di gruppo tooconfigure questi oggetti Criteri di gruppo nel dominio gestito hello.

1. In hello **Gestione criteri di gruppo** console, fare clic su hello tooexpand **foresta: contoso100.com** e **domini** criteri di gruppo di nodi toosee hello per il dominio gestito.

    ![Oggetti Criteri di gruppo predefiniti](./media/active-directory-domain-services-admin-guide/builtin-gpos.png)
2. È possibile personalizzare questi criteri di gruppo tooconfigure oggetti Criteri di gruppo predefiniti nel dominio gestito. Fare doppio clic su hello oggetto Criteri di gruppo e fare clic su **modifica...**  incorporato hello toocustomize: oggetto Criteri di gruppo. lo strumento di configurazione di criteri di gruppo Hello consente si toocustomize hello oggetto Criteri di gruppo.

    ![Modificare gli oggetti Criteri di gruppo predefiniti](./media/active-directory-domain-services-admin-guide/edit-builtin-gpo.png)
3. È ora possibile usare hello **Editor Gestione criteri di gruppo** console predefinite hello tooedit: oggetto Criteri di gruppo. Ad esempio, hello seguente schermata mostra come toocustomize hello oggetto Criteri di gruppo predefinito di 'AADDC computer'.

    ![Personalizzare un oggetto Criteri di gruppo predefinito](./media/active-directory-domain-services-admin-guide/gp-editor.png)

## <a name="task-5---create-a-custom-group-policy-object-gpo"></a>Attività 5: creare un Oggetto Criteri di gruppo (GPO) personalizzato
È possibile creare o importare i propri oggetti criteri di gruppo personalizzati. È anche possibile collegare personalizzato oggetti Criteri di gruppo tooa personalizzato OU creati nel dominio gestito. Per ulteriori informazioni sulla creazione di unità organizzative personalizzate, consultare l'articolo su come [creare un'Unità organizzativa in un dominio gestito](active-directory-ds-admin-guide-create-ou.md).

> [!NOTE]
> È necessario un membro del gruppo di hello 'AAD DC Administrators', criteri di gruppo nel dominio gestito hello tooadminister toobe.
>
>

1. In hello **Gestione criteri di gruppo** console fare clic su tooselect personalizzato unità organizzativa (OU). Fare doppio clic su unità Organizzativa hello e fare clic su **crea un oggetto Criteri di gruppo in questo dominio e crea qui un collegamento...** .

    ![Creare un Oggetto Criteri di gruppo personalizzato](./media/active-directory-domain-services-admin-guide/gp-create-gpo.png)
2. Specificare un nome per hello nuovo oggetto Criteri di gruppo e fare clic su **OK**.

    ![Specificare il nome dell'Oggetto Criteri di gruppo](./media/active-directory-domain-services-admin-guide/gp-specify-gpo-name.png)
3. Un nuovo oggetto Criteri di gruppo viene creato e collegato personalizzato tooyour unità Organizzativa. Fare doppio clic su hello oggetto Criteri di gruppo e fare clic su **modifica...**  dal menu di hello.

    ![Oggetto Criteri di gruppo appena creato](./media/active-directory-domain-services-admin-guide/gp-gpo-created.png)
4. È possibile personalizzare l'oggetto Criteri di gruppo appena creato hello utilizzando hello **Editor Gestione criteri di gruppo**.

    ![Personalizzare il nuovo Oggetto Criteri di gruppo](./media/active-directory-domain-services-admin-guide/gp-customize-gpo.png)


Ulteriori informazioni sull'uso della [console di Gestione Criteri di gruppo](https://technet.microsoft.com/library/cc753298.aspx) sono disponibili su TechNet.

## <a name="related-content"></a>Contenuti correlati
* [Guida introduttiva di Azure AD Domain Services](active-directory-ds-getting-started.md)
* [Aggiunta a un dominio gestito con servizi di dominio Active Directory di Azure tooan Windows Server macchina virtuale](active-directory-ds-admin-guide-join-windows-vm.md)
* [Amministrare un dominio gestito di Servizi di dominio Azure AD](active-directory-ds-admin-guide-administer-domain.md)
* [Console Gestione Criteri di gruppo](https://technet.microsoft.com/library/cc753298.aspx)
