---
title: 'Azure Active Directory Domain Services: amministrare DNS in domini gestiti | Documentazione Microsoft'
description: Amministrare DNS in domini gestiti di Azure Active Directory Domain Services
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
ms.openlocfilehash: f2085283649eadd3c9e89f708b0eecf10b2d7d70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="administer-dns-on-an-azure-ad-domain-services-managed-domain"></a>Amministrare DNS in un dominio gestito dai Servizi di dominio Azure AD
Azure Active Directory Domain Services include un server DNS (Domain Name Resolution) che fornisce la risoluzione DNS per il dominio gestito hello. In alcuni casi, potrebbe essere necessario tooconfigure DNS nel dominio hello gestito. I record DNS toocreate potrebbe essere necessario per le macchine che non sono toohello aggiunti a un dominio, configurare gli indirizzi IP virtuali per servizi di bilanciamento del carico o del programma di installazione server d'inoltro DNS esterni. Per questo motivo, gli utenti appartenenti al gruppo 'Administrators di controller di dominio di AAD' toohello vengono concessi privilegi di amministrazione di DNS nel dominio gestito hello.

## <a name="before-you-begin"></a>Prima di iniziare
attività di hello tooperform elencate in questo articolo, è necessario:

1. Una **sottoscrizione di Azure**valida.
2. Una **directory di Azure AD** sincronizzata con una directory locale o con una directory solo cloud.
3. **Servizi di dominio AD Azure** deve essere abilitato per la directory hello Azure AD. Se non è ancora fatto, seguire tutte le attività descritte nella hello hello [Guida introduttiva](active-directory-ds-getting-started.md).
4. Oggetto **dominio macchina virtuale** da cui amministrare hello dominio gestito di servizi di dominio Azure Active Directory. Se non si dispone di questo tipo di una macchina virtuale, seguire tutte le attività hello descritte nell'articolo hello intitolata [aggiunta a un dominio gestito di macchina virtuale tooa Windows](active-directory-ds-admin-guide-join-windows-vm.md).
5. Sono necessarie le credenziali di hello di un **gruppo 'Administrators di controller di dominio di AAD' dell'utente account appartenenti toohello** nella directory, tooadminister DNS per il dominio gestito.

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-dns-for-hello-managed-domain"></a>Attività 1: eseguire il provisioning di una macchina virtuale di dominio di tooremotely amministrare DNS per il dominio gestito hello
Domini gestiti di servizi di dominio AD Azure possono essere gestiti in remoto mediante familiari strumenti di amministrazione di Active Directory, ad esempio hello Active Directory amministrativi centro o PowerShell di Active Directory. Analogamente, DNS per il dominio gestito hello possono essere amministrati in remoto mediante strumenti di amministrazione di Server DNS hello.

Gli amministratori di directory di Azure AD non sono controller di privilegi tooconnect toodomain hello dominio gestito tramite Desktop remoto. I membri del gruppo 'Administrators di controller di dominio di AAD' hello possono amministrare DNS per i domini gestiti in remoto mediante strumenti di Server DNS da un computer Windows Server/client che è dominio gestito toohello unita in join. Server DNS possono essere installati come parte della funzionalità facoltativa strumenti di amministrazione remota Server (RSAT) di hello in Windows Server e computer client aggiunti a un dominio toohello gestito.

Hello prima attività è tooprovision una macchina virtuale di Windows Server di dominio gestiti toohello unita in join. Per istruzioni, consultare l'articolo toohello [aggiunta a un dominio gestito servizi di dominio Azure Active Directory di Windows Server macchina virtuale tooan](active-directory-ds-admin-guide-join-windows-vm.md).

## <a name="task-2---install-dns-server-tools-on-hello-virtual-machine"></a>Attività 2: strumenti di installazione del Server DNS nella macchina virtuale hello
Eseguire hello seguenti strumenti di amministrazione DNS passaggi tooinstall hello nella macchina virtuale di hello aggiunti a un dominio. Per altre informazioni sull'[installazione e uso degli strumenti di amministrazione remota del server](https://technet.microsoft.com/library/hh831501.aspx), vedere Technet.

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
9. In hello **funzionalità** pagina, fare clic su hello tooexpand **strumenti di amministrazione remota del Server** nodo e quindi fare clic su hello tooexpand **strumenti di amministrazione ruoli** nodo. Selezionare **gli strumenti per Server DNS** funzionalità dall'elenco di hello di strumenti di amministrazione ruoli.

    ![Pagina Funzionalità](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-tools.png)
10. In hello **conferma** pagina, fare clic su **installare** caratteristiche degli strumenti di Server DNS di tooinstall hello nella macchina virtuale hello. Al completamento dell'installazione della funzionalità, fare clic su **Chiudi** tooexit hello **Aggiungi ruoli e funzionalità** procedura guidata.

    ![Pagina di conferma](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-confirmation.png)

## <a name="task-3---launch-hello-dns-management-console-tooadminister-dns"></a>Attività 3 - avviare hello DNS management console tooadminister DNS
Ora che gli strumenti di Server DNS hello funzionalità viene installata in hello macchina virtuale aggiunto a un dominio, è possibile usare hello DNS strumenti tooadminister DNS nel dominio hello gestito.

> [!NOTE]
> È necessario toobe un membro del gruppo di hello 'AAD DC Administrators', tooadminister DNS nel dominio gestito hello.
>
>

1. Dalla schermata Start hello, fare clic su **strumenti di amministrazione**. Dovrebbe essere hello **DNS** console installata nella macchina virtuale hello.

    ![Strumenti di amministrazione - Console DNS](./media/active-directory-domain-services-admin-guide/install-rsat-dns-tools-installed.png)
2. Fare clic su **DNS** console di gestione DNS toolaunch hello.
3. In hello **connettersi tooDNS Server** finestra di dialogo, fare clic su opzione hello intitolata **hello seguenti computer**e immettere il nome di dominio DNS hello del dominio gestito hello (ad esempio, ' contoso100.com').

    ![La Console DNS - connessione toodomain](./media/active-directory-domain-services-admin-guide/dns-console-connect-to-domain.png)
4. Hello DNS Console si connette toohello di dominio gestiti.

    ![Console DNS - amministrare il dominio](./media/active-directory-domain-services-admin-guide/dns-console-managed-domain.png)
5. È ora possibile utilizzare le voci DNS di hello DNS console tooadd per i computer in rete virtuale di hello in cui è stato abilitato Servizi di dominio di AAD.

> [!WARNING]
> Prestare attenzione quando amministrazione DNS per hello gestito dominio utilizzando gli strumenti di amministrazione DNS. Verificare che si **non eliminare o modificare i record DNS di incorporato hello utilizzate dai servizi di dominio nel dominio hello**. I record DNS predefiniti includono record DNS di dominio, record del server dei nomi e altri record usati per l'individuazione dei controller di dominio. Se si modificano questi record, i servizi di dominio vengono interrotti nella rete virtuale hello.
>
>

Vedere hello [strumenti DNS articolo in Technet](https://technet.microsoft.com/library/cc753579.aspx) per ulteriori informazioni sulla gestione di DNS.

## <a name="related-content"></a>Contenuti correlati
* [Guida introduttiva di Azure AD Domain Services](active-directory-ds-getting-started.md)
* [Aggiunta a un dominio gestito con servizi di dominio Active Directory di Azure tooan Windows Server macchina virtuale](active-directory-ds-admin-guide-join-windows-vm.md)
* [Amministrare un dominio gestito di Servizi di dominio Azure AD](active-directory-ds-admin-guide-administer-domain.md)
* [Strumenti di amministrazione DNS](https://technet.microsoft.com/library/cc753579.aspx)
