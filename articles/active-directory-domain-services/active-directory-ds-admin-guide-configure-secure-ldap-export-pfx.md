---
title: aaaConfigure Secure LDAP (LDAPS) in servizi di dominio Active Directory di Azure | Documenti Microsoft
description: Configurare l'accesso LDAP sicuro (LDAPS) per un dominio gestito di Servizi di dominio Azure AD
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 356b28f8392b0e203df9c81177ec842d52866c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Configurare l'accesso LDAP sicuro (LDAPS) per un dominio gestito di Azure AD Domain Services

## <a name="before-you-begin"></a>Prima di iniziare
Assicurarsi di aver completato l'[Attività 1: Ottenere un certificato per l'accesso LDAP sicuro](active-directory-ds-admin-guide-configure-secure-ldap.md).


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a>Attività 2: esportare hello sicura LDAP certificato tooa. File PFX
Prima di iniziare questa attività, assicurarsi di aver ottenuto un certificato LDAP sicuro hello da un'autorità di certificazione pubblica o aver creato un certificato autofirmato.

Eseguire hello alla procedura seguente, hello tooexport LDAPS tooa del certificato. File PFX.

1. Hello premere **avviare** pulsante e digitare **R**. In hello **eseguire** finestra di dialogo, tipo **mmc** e fare clic su **OK**.

    ![Avviare la console di MMC hello](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. In hello **controllo dell'Account utente** richiesto, fare clic su **Sì** toolaunch MMC (Microsoft Management Console) come amministratore.
3. Da hello **File** menu, fare clic su **Aggiungi/Rimuovi Snap-in...** .

    ![Aggiungere lo snap-in tooMMC console](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. In hello **Aggiungi o Rimuovi Snap-in** finestra di dialogo, seleziona hello **certificati** snap-in, fare clic su hello **Aggiungi >** pulsante.

    ![Aggiungere console tooMMC snap-in certificati](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. In hello **snap-in certificati** procedura guidata, selezionare **account Computer** e fare clic su **Avanti**.

    ![Aggiungere lo snap-in certificati per l'account del computer](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. In hello **seleziona Computer** selezionare **computer locale: (hello computer su cui è in esecuzione questa console)** e fare clic su **fine**.

    ![Aggiungere lo snap-in certificati, Seleziona computer](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. In hello **Aggiungi o Rimuovi Snap-in** finestra di dialogo, fare clic su **OK** tooadd hello certificati snap-in tooMMC.

    ![Aggiungere certificati snap-in tooMMC - eseguita](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. Nella finestra MMC hello, fare clic su tooexpand **radice Console**. Dovrebbe essere caricati hello snap-in certificati. Fare clic su **certificati (Computer locale)** tooexpand. Fare clic su hello tooexpand **personale** nodo, seguito da hello **certificati** nodo.

    ![Aprire l'archivio certificati personali](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. Dovrebbe essere hello autofirmato che è stato creato. È possibile esaminare le proprietà di hello di hello certificato tooensure hello identificazione personale corrisponde a quello riportato in windows PowerShell hello al momento della creazione certificato hello.
10. Selezionare hello certificato autofirmato e **destro del mouse su**. Selezionare il menu di scelta rapida hello **tutte le attività** e selezionare **Esporta...** .

    ![Esportare il certificato](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. In hello **esportazione guidata certificati**, fare clic su **Avanti**.

    ![Esportare il certificato, procedura guidata](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. In hello **Esporta chiave privata** selezionare **Sì, Esporta la chiave privata di hello**, fare clic su **Avanti**.

    ![Esportare il certificato, chiave privata](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > È necessario esportare la chiave privata insieme certificato hello hello. Se si specifica un file PFX che contiene la chiave privata per il certificato di hello hello, abilitare l'accesso LDAP sicuro per il dominio gestito ha esito negativo.
    >
    >
13. In hello **formato File di esportazione** selezionare **scambio informazioni personali - PKCS #12 (. PFX)** come formato di file hello per hello certificato esportato.

    ![Esportare il certificato, formato di file](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > Solo hello. Formato di file PFX è supportato. Non esportare toohello certificato hello. Formato file CER.
    >
    >
14. In hello **sicurezza** pagina, seleziona hello **Password** opzione e digitare un hello tooprotect password. File PFX. Prendere nota della password perché sarà necessaria nell'attività successiva hello. Fare clic su **Avanti** tooproceed.

    ![Password per l'esportazione del certificato ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > Prendere nota della password. È necessario durante l'abilitazione di LDAP sicuro per questo dominio gestito in [attività 3: abilitare l'accesso LDAP sicuro per il dominio gestito hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
    >
    >
15. In hello **tooExport File** , specificare il nome di file hello e la posizione in cui si desidera certificato hello tooexport.

    ![Percorso per l'esportazione del certificato](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. Hello seguente pagina, scegliere **fine** file PFX del certificato tooa tooexport hello. Verrà visualizzata nella finestra di conferma quando è stato esportato il certificato di hello.

    ![Esportare il certificato, Fatto](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a>Passaggio successivo
[Attività 3: abilitare l'accesso LDAP sicuro per il dominio gestito hello](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
