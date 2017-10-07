---
title: 'Azure Active Directory Domain Services: Aggiungere un dominio gestito tooa di macchina virtuale Windows Server | Documenti Microsoft'
description: Aggiungere una macchina virtuale di Windows Server servizi di dominio Active Directory tooAzure
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 74dbdb33-05db-4d47-badc-0d7bb6d0c8cb
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1e85833b42bd51f3b3df067d6c5b69253459bec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain"></a>Aggiunta a un dominio gestito di macchina virtuale tooa Windows Server
> [!div class="op_single_selector"]
> * [Portale di Azure classico - Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell - Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

Questo articolo illustra la modalità di gestione di dominio, utilizzando hello portale di Azure classico toojoin una macchina virtuale in esecuzione Windows Server 2012 R2 tooan servizi di dominio Active Directory di Azure.

## <a name="step-1-create-hello-windows-server-virtual-machine"></a>Passaggio 1: Creare una macchina virtuale di Windows Server hello
Attenersi alle istruzioni hello hello [creare una macchina virtuale in esecuzione Windows nel portale di Azure classico hello](../virtual-machines/windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) esercitazione. È importante tooensure che la macchina virtuale appena creata è unita in join toohello stessa rete virtuale in cui è abilitato Servizi di dominio Active Directory di Azure. Hello 'Creazione rapida' opzione è toojoin hello tooa virtuale rete della macchina virtuale non è abilitato. Pertanto, è necessario macchina virtuale toouse hello 'Da raccolta' opzione toocreate hello.

Eseguire hello seguendo i passaggi toocreate una macchina virtuale toohello aggiunti a un rete virtuale in cui è stato abilitato Servizi di dominio Active Directory di Azure.

1. Nel portale di Azure classico, hello barra dei comandi nella parte inferiore di hello della finestra hello hello fare clic su **New**.
2. In **Calcolo** fare clic su **Macchina Virtuale** e quindi su **Da raccolta**.
3. Consente di prima schermata Hello **scegliere un'immagine** per la macchina virtuale dall'elenco di hello delle immagini disponibili. Selezionare l'immagine appropriata hello.

    ![Selezionare l'immagine](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-image.png)
4. seconda schermata Hello consente di scegliere un nome computer, una dimensione e nome utente amministrativo e una password. Utilizzare il livello di hello e dimensioni richieste toorun l'app o il carico di lavoro. nome utente Hello selezionate di seguito è un utente di amministratore locale nel computer di hello. Non immettere in questo campo le credenziali di un account utente di dominio.

    ![Configurare la macchina virtuale](./media/active-directory-domain-services-admin-guide/create-windows-vm-config.png)
5. terza schermata Hello consente di configurare le risorse di rete, archiviazione e la disponibilità. Assicurarsi di selezionare una rete virtuale di hello in cui è abilitato Servizi di dominio Active Directory di Azure da hello **affinità di area/gruppo/rete virtuale** elenco a discesa. Specificare un **nome DNS del servizio Cloud** come appropriato per la macchina virtuale hello.

    ![Selezionare una rete virtuale per la macchina virtuale](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-vnet.png)

   > [!WARNING]
   > Verificare che si aggiunge hello toohello di macchina virtuale stessa rete virtuale in cui è stato abilitato Servizi di dominio Active Directory di Azure. Di conseguenza, macchina virtuale hello possibile vedere dominio hello ed eseguire attività quali l'aggiunta a dominio hello. Se si sceglie una macchina virtuale di toocreate hello in una rete virtuale diversa, connettere la rete virtuale toohello rete virtuale in cui è stato abilitato Servizi di dominio Active Directory di Azure.
   >
   >
6. schermata quarto Hello consente di installare l'agente VM hello e configurare alcune delle estensioni disponibili hello.

    ![Operazione completata](./media/active-directory-domain-services-admin-guide/create-windows-vm-done.png)
7. Dopo la creazione di macchine virtuali hello, portale classico hello Elenca hello nuova macchina virtuale in hello **macchine virtuali** nodo. Macchina virtuale hello sia il servizio cloud vengono avviate automaticamente e il relativo stato viene elencato come **esecuzione**.

    ![Macchina virtuale attiva e in esecuzione](./media/active-directory-domain-services-admin-guide/create-windows-vm-running.png)

## <a name="step-2-connect-toohello-windows-server-virtual-machine-using-hello-local-administrator-account"></a>Passaggio 2: Connettere toohello macchina virtuale di Windows Server utilizzando l'account amministratore locale hello
A questo punto, la macchina virtuale di Windows Server toohello appena creato, toojoin di connessione è il dominio toohello. Utilizzare le credenziali di amministratore locale hello specificata durante la creazione della macchina virtuale di hello, tooconnect tooit.

Eseguire hello seguente macchina virtuale toohello tooconnect di passaggi.

1. Passare troppo**macchine virtuali** nodo nel portale classico hello. Selezionare una macchina virtuale hello creato nel passaggio 1 e fare clic su **Connetti** hello barra dei comandi nella parte inferiore di hello della finestra hello.

    ![Connettere la macchina virtuale di tooWindows](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. portale classico Hello richiede tooopen o salvare un file con estensione 'RDP', che è usato tooconnect toohello virtual machine. Dopo aver terminato il download, fare clic su file hello tooopen.
3. Al prompt dei comandi di hello account di accesso, immettere il **credenziali di amministratore locale**, specificata durante la creazione della macchina virtuale hello. come 'localhost\mahesh' in questo esempio.

A questo punto, è necessario eseguire l'accesso toohello creata la macchina virtuale Windows usando le credenziali di amministratore locale. passaggio successivo Hello è dominio toohello di toojoin hello macchina virtuale.

## <a name="step-3-join-hello-windows-server-virtual-machine-toohello-aad-ds-managed-domain"></a>Passaggio 3: Aggiungere dominio gestito toohello AAD di dominio Active Directory di hello macchina virtuale Windows Server
Eseguire hello seguendo i passaggi toojoin hello Windows macchina virtuale toohello AAD di dominio Active Directory gestito dominio del Server.

1. Connessione toohello Windows Server, come illustrato nel passaggio 2. Dalla schermata Start hello, aprire **Server Manager**.
2. Fare clic su **Server locale** nel riquadro di sinistra hello della finestra di Server Manager hello.

    ![Avviare Server Manager nella macchina virtuale](./media/active-directory-domain-services-admin-guide/join-domain-server-manager.png)
3. Fare clic su **WORKGROUP** in hello **proprietà** sezione. In hello **le proprietà di sistema** pagina delle proprietà, fare clic su **modifica** dominio hello toojoin.

    ![Pagina Proprietà di sistema](./media/active-directory-domain-services-admin-guide/join-domain-system-properties.png)
4. Specificare il nome di dominio hello del dominio servizi di dominio Active Directory di Azure gestito in hello **dominio** casella di testo e fare clic su **OK**.

    ![Specificare hello dominio toobe unita in join](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-domain.png)
5. Si sono tooenter richiesta dominio hello toojoin credenziali. Verificare che si **specificare credenziali hello per toohello di appartiene un utente agli amministratori di controller di dominio di AAD** gruppo. Solo i membri di questo gruppo dispongano di privilegi toojoin macchine toohello gestito dominio.

    ![Specificare le credenziali per l'aggiunta a un dominio](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-credentials.png)
6. È possibile specificare le credenziali in uno dei seguenti modi hello:

   * Formato UPN: specificare il suffisso UPN hello per account utente di hello, come configurato in Azure AD. In questo esempio, il suffisso UPN hello dell'utente hello 'bob' è 'bob@domainservicespreview.onmicrosoft.com'.
   * Formato SAMAccountName: È possibile specificare il nome di account hello in formato SAMAccountName hello. In questo esempio, utente hello 'bob' necessario tooenter 'CONTOSO100\bob'.

     > [!NOTE]
     > **È consigliabile utilizzare credenziali toospecify formato UPN di hello.** Hello SAMAccountName può essere generato automaticamente se il prefisso di nome UPN dell'utente è troppo lungo (ad esempio, 'joereallylongnameuser'). Se più utenti hanno hello stesso prefisso di nome UPN (ad esempio, "bob") nel tenant di Azure AD, il relativo formato SAMAccountName può essere generato automaticamente dal servizio hello. In questi casi, formato UPN hello può essere utilizzato in modo affidabile toolog toohello dominio.
     >
     >
7. Dopo l'aggiunta al dominio ha esito positivo, vengono visualizzati hello seguente messaggio di benvenuto toohello dominio. Riavviare la macchina virtuale hello per hello dominio join operazione toocomplete.

    ![Dominio iniziale toohello](./media/active-directory-domain-services-admin-guide/join-domain-done.png)

## <a name="troubleshooting-domain-join"></a>Risoluzione dei problemi di aggiunta al dominio
### <a name="connectivity-issues"></a>Problemi di connettività
Se macchina virtuale hello è dominio hello toofind non è possibile, fare riferimento toohello risoluzione dei problemi relativi alla procedura seguente:

* Verificare che la macchina virtuale hello sia connesso toohello stessa rete virtuale che è già stato attivato in servizi di dominio. In caso contrario, hello e macchina virtuale non è possibile tooconnect toohello dominio è pertanto dominio hello toojoin non è possibile.
* Se la rete virtuale connessa tooanother macchina virtuale hello è assicurarsi che questa rete virtuale è connessa toohello rete virtuale in cui è stato abilitato Servizi di dominio.
* Provare a dominio hello tooping utilizzando il nome di dominio hello del dominio gestito hello (ad esempio, ' ping contoso100.com'). Se si è pertanto impossibile toodo, provare a indirizzi IP di hello tooping per il dominio di hello visualizzato nella pagina hello in cui è abilitato Servizi di dominio Azure Active Directory (ad esempio, ' ping 10.0.0.4'). Se si è in grado di tooping hello IP indirizzo, ma non di dominio hello, DNS può essere configurato in modo non corretto. Si potrebbero non aver configurato gli indirizzi IP hello del dominio hello come server DNS per la rete virtuale hello.
* Provare a scaricare hello cache del resolver DNS nella macchina virtuale hello ('ipconfig /flushdns').

Se si verifica toohello finestra di dialogo che chiede di dominio di hello toojoin credenziali, problemi di connettività non si dispone.

### <a name="credentials-related-issues"></a>Problemi correlati alle credenziali
Fare riferimento toohello procedura seguente se si verificano problemi con le credenziali e dominio hello toojoin non è possibile.

* Provare a utilizzare credenziali toospecify formato UPN di hello. Hello SAMAccountName per l'account potrebbe essere generato automaticamente se sono presenti più utenti con hello UPN stesso prefisso nel tenant o se il prefisso di nome UPN è troppo lungo. Pertanto, formato SAMAccountName hello per l'account potrebbe essere diverso da ciò che si prevede che o usare nel dominio locale.
* Provare a specificare credenziali di hello toouse di un account utente appartenente al dominio gestito di toohello 'AAD DC Administrators' gruppo toojoin macchine toohello.
* Assicurarsi di aver [abilitata la sincronizzazione delle password](active-directory-ds-getting-started-password-sync.md) in base ai passaggi hello descritti nella Guida introduttiva hello.
* Assicurarsi di usare hello UPN dell'utente hello in base alla configurazione in Azure Active Directory (ad esempio, 'bob@domainservicespreview.onmicrosoft.com') toosign in.
* Assicurarsi di aver atteso un tempo sufficiente per toocomplete di sincronizzazione password come specificato nella Guida introduttiva hello.

## <a name="related-content"></a>Contenuti correlati
* [Guida introduttiva di Azure AD Domain Services](active-directory-ds-getting-started.md)
* [Amministrare un dominio gestito di Servizi di dominio Azure AD](active-directory-ds-admin-guide-administer-domain.md)
