---
title: 'Azure Active Directory Domain Services: Aggiunta a un dominio gestito tooa di VM RHEL | Documenti Microsoft'
description: Aggiungere una macchina virtuale Red Hat Enterprise Linux servizi di dominio Active Directory tooAzure
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 87291c47-1280-43f8-8fb2-da1bd61a4942
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 41ca2aaf2eefbf9c403d2b834d61a1aa0943d950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-tooa-managed-domain"></a>Aggiunta a un dominio gestito di macchina virtuale tooa Red Hat Enterprise Linux 7
Questo articolo illustra la modalità di gestione dominio toojoin un tooan di macchina virtuale Red Hat Enterprise Linux (RHEL) 7 servizi di dominio Active Directory di Azure.

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a>Eseguire il provisioning di una macchina virtuale di Red Hat Enterprise Linux
Eseguire hello seguente macchina virtuale di tooprovision un RHEL 7 passaggi utilizzando hello portale di Azure.

1. Accedi toohello [portale di Azure](https://portal.azure.com).

    ![Dashboard del portale di Azure](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. Fare clic su **New** su hello sinistro riquadro e tipo **Red Hat** nella barra di ricerca hello come illustrato nella seguente schermata hello. Le voci per Red Hat Enterprise Linux vengono visualizzati nei risultati della ricerca hello. Fare clic su **Red Hat Enterprise Linux 7.2**.

    ![Selezionare RHEL nei risultati](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. risultati della ricerca Hello in hello **tutto** riquadro dovrebbe elencare immagine hello Red Hat Enterprise Linux 7.2. Fare clic su **Red Hat Enterprise Linux 7.2** tooview ulteriori informazioni sull'immagine di macchina virtuale hello.

    ![Selezionare RHEL nei risultati](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. In hello **Red Hat Enterprise Linux 7.2** riquadro, è necessario visualizzare ulteriori informazioni sull'immagine di macchina virtuale hello. In hello **selezionare un modello di distribuzione** elenco a discesa, selezionare **classico**. Quindi fare clic su hello **crea** pulsante.

    ![Visualizzare i dettagli dell'immagine](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. In hello **nozioni di base** pagina di hello **crea macchina virtuale** procedura guidata immettere hello **nome Host** per hello nuova macchina virtuale. Inoltre, specificare un nome utente dell'amministratore locale in hello **nome utente** campo e un **Password**. È anche possibile scegliere toouse un utente di amministratore locale hello tooauthenticate chiave SSH. Selezionare anche un **tariffario** per la macchina virtuale hello.

    ![Creare una macchina virtuale: dettagli di base](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. In hello **dimensioni** pagina di hello **crea macchina virtuale** dimensioni hello procedura guidata, selezionare per la macchina virtuale hello.

    ![Creare una macchina virtuale: selezionare la dimensione](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. In hello **impostazioni** pagina di hello **crea macchina virtuale** account di archiviazione hello procedura guidata, selezionare per la macchina virtuale hello. Fare clic su **rete virtuale** hello toowhich di tooselect hello rete virtuale devono essere distribuiti VM Linux. In hello **rete virtuale** pannello, in cui servizi di dominio Active Directory di Azure è disponibili la rete virtuale selezionare hello. In questo esempio è selezionare una rete virtuale di hello 'MyPreviewVNet'.

    ![Creare una macchina virtuale: selezionare una rete virtuale](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. In hello **riepilogo** pagina di hello **crea macchina virtuale** procedura guidata, rivedere e fare clic su hello **OK** pulsante.

    ![Creare una macchina virtuale: rete virtuale selezionata](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. Distribuzione di hello nuova macchina virtuale basata su immagine hello RHEL 7.2 deve iniziare.

    ![Creare una macchina virtuale: distribuzione avviata](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. Dopo alcuni minuti, macchina virtuale hello deve essere distribuito correttamente e pronto all'uso.

    ![Creare una macchina virtuale: distribuzione completata](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-toohello-newly-provisioned-linux-virtual-machine"></a>Connettersi in remoto macchina virtuale di Linux toohello appena effettuato il provisioning
macchina virtuale Hello RHEL 7.2 è stato eseguito il provisioning in Azure. attività successiva Hello è tooconnect in remoto macchina virtuale toohello.

**Connettere la macchina virtuale di toohello RHEL 7.2** hello di istruzioni nell'articolo hello [come toolog nella macchina virtuale tooa che eseguono Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hello passaggi restanti di hello presuppongono è usare hello SSH PuTTY client tooconnect toohello RHEL macchina virtuale. Per ulteriori informazioni, vedere hello [pagina di Download di PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

1. Hello aprire PuTTY programma.
2. Immettere hello **nome Host** per hello creata la macchina virtuale RHEL. In questo esempio, la macchina virtuale con il nome di host hello 'contoso-rhel.cloudapp .net'. Se non si certi del nome host hello della macchina virtuale, fare riferimento toohello dashboard della macchina virtuale nel portale di Azure hello.

    ![Connessione PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. Accedere a macchina virtuale toohello utilizzando le credenziali di amministratore locale hello specificata durante la creazione della macchina virtuale hello. In questo esempio, abbiamo utilizzato l'account amministratore locale hello "mahesh".

    ![Accesso PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-hello-linux-virtual-machine"></a>Installare i pacchetti richiesti nella macchina virtuale di Linux hello
Dopo aver connessione macchina virtuale toohello hello è pacchetti tooinstall necessari per l'aggiunta a un dominio nella macchina virtuale hello. Eseguire hello alla procedura seguente:

1. **Installare realmd:** pacchetto realmd hello viene utilizzato per l'aggiunta al dominio. Nel terminale PuTTY, digitare hello comando seguente:

    sudo yum install realmd

    ![Installare realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    Dopo alcuni minuti, hello realmd deve ottenere installato nella macchina virtuale hello.

    ![realmd installato](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. **Installare sssd:** pacchetto realmd hello dipende da operazioni di join sssd tooperform dominio. Nel terminale PuTTY, digitare hello comando seguente:

    sudo yum install sssd

    ![Installare sssd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    Dopo alcuni minuti, hello sssd deve ottenere installato nella macchina virtuale hello.

    ![realmd installato](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. **Installare kerberos:** nel terminale PuTTY, digitare hello comando seguente:

    sudo yum install krb5-workstation krb5-libs

    ![Installare kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    Dopo alcuni minuti, hello realmd deve ottenere installato nella macchina virtuale hello.

    ![Kerberos installato](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-hello-linux-virtual-machine-toohello-managed-domain"></a>Aggiunta a dominio gestito toohello hello Linux macchina virtuale
Ora che i pacchetti hello necessario sono installati sulla macchina virtuale di Linux hello, hello è dominio gestito toohello toojoin hello macchina virtuale.

1. Individuare hello dominio gestito di servizi di dominio di AAD. Nel terminale PuTTY, digitare hello comando seguente:

    sudo realm discover CONTOSO100.COM

    ![realm discover](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    Se **individuazione dell'area di autenticazione** è Impossibile toofind dominio gestito, verificare che tale dominio hello sia raggiungibile dalla macchina virtuale hello (ping try). Verificare inoltre che la macchina virtuale hello è stata effettivamente distribuita toohello stessa rete virtuale in cui hello dominio gestito è disponibile.
2. Inizializzare kerberos. Nella finestra terminale PuTTY, digitare hello comando seguente. Assicurarsi di specificare un utente appartenente al gruppo toohello 'AAD Administrators controller di dominio'. Solo questi utenti è possono aggiungere domini gestiti toohello di computer.

    kinit bob@CONTOSO100.COM

    ![kinit ](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    Assicurarsi che si specifica il nome di dominio hello in lettere maiuscole, else kinit ha esito negativo.
3. Dominio toohello hello macchina. Nella finestra terminale PuTTY, digitare hello comando seguente. Specificare hello stesso utente specificato nel precedente passaggio ('kinit') hello.

    sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'

    ![Aggiunta dell'area di autenticazione](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

È necessario ottenere un messaggio ("correttamente registrato macchina nell'area di autenticazione") quando la macchina hello è dominio gestito toohello correttamente unita in join.

## <a name="verify-domain-join"></a>Verificare l'aggiunta a un dominio
È possibile verificare rapidamente se macchina hello è stato dominio gestito toohello correttamente unita in join. Connettersi toohello appena dominio RHEL VM utilizzando SSH e un account utente di dominio e quindi toosee di controllo se l'account utente di hello viene risolto correttamente.

1. Nel PuTTY terminal, hello tipo successivo comando tooconnect toohello appena aggiunti al dominio RHEL virtual machine tramite SSH. Utilizzare un account di dominio appartenente al dominio gestito toohello (ad esempio, 'bob@CONTOSO100.COM' in questo caso.)

    ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net
2. Nella finestra terminale PuTTY, digitare hello successivo comando toosee se home directory di hello è stato inizializzato correttamente.

    pwd
3. Nella finestra terminale PuTTY, digitare hello successivo comando toosee se appartenenze hello sono stati risolti correttamente.

    id

Di seguito è riportato un esempio dell'output di questi comandi:

![Verificare l'aggiunta a un dominio](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a>Risoluzione dei problemi di aggiunta al dominio
Fare riferimento toohello [aggiunta al dominio Troubleshooting](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) articolo.

## <a name="related-content"></a>Contenuti correlati
* [Guida introduttiva di Azure AD Domain Services](active-directory-ds-getting-started.md)
* [Aggiunta a un dominio gestito con servizi di dominio Active Directory di Azure tooan Windows Server macchina virtuale](active-directory-ds-admin-guide-join-windows-vm.md)
* [Come toolog nella macchina virtuale tooa che eseguono Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* [Installazione di Kerberos](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [Red Hat Enterprise Linux 7 - Windows Integration Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
