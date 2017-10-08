---
title: le chiavi SSH aaaUse con Windows per le macchine virtuali Linux | Documenti Microsoft
description: Informazioni su come toogenerate e usare SSH chiavi in una macchina virtuale Linux di Windows computer tooconnect tooa in Azure.
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 2cacda3b-7949-4036-bd5d-837e8b09a9c8
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: danlep
ms.openlocfilehash: 6c44217332538857cc2ca2e85de4b476aa71251c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ssh-keys-with-windows-on-azure"></a>Come chiavi, tooUse SSH tramite Windows in Azure
> [!div class="op_single_selector"]
> * [Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> * [Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
>
>

Quando ci si connettono tooLinux le macchine virtuali (VM) in Azure, è consigliabile utilizzare [crittografia a chiave pubblica](https://wikipedia.org/wiki/Public-key_cryptography) tooprovide un toolog modo più sicuro in tooyour VM Linux. Questo processo prevede uno scambio di chiavi pubblico e privato utilizzando hello sicura shell (SSH) comando tooauthenticate anziché un nome utente e password. Le password sono gli attacchi di forza toobrute vulnerabile, specialmente per le macchine virtuali con connessione Internet, ad esempio server web. Questo articolo fornisce una panoramica delle chiavi SSH come toogenerate hello chiavi appropriate in un computer Windows.

## <a name="overview-of-ssh-and-keys"></a>Panoramica di SSH e delle chiavi
È possibile registrare in modo sicuro in tooyour VM Linux con chiavi pubbliche e private:

* Hello **chiave pubblica** si trova in una VM Linux, o qualsiasi altro servizio che si desidera toouse con crittografia a chiave pubblica.
* Hello **chiave privata** è ciò che si presenti tooyour Linux VM quando si accede, tooverify la tua identità. Sulla chiave privata è necessario mantenere la massima riservatezza, evitando di condividerla.

La chiave pubblica e la chiave privata sono utilizzabili in più VM e servizi. Non è necessaria una coppia di chiavi per ogni macchina virtuale o un servizio che si desidera tooaccess. Per una panoramica più dettagliata, vedere [crittografia a chiave pubblica](https://wikipedia.org/wiki/Public-key_cryptography).

SSH è un protocollo per connessioni crittografate che consente accessi protetti su connessioni non sicure. È un protocollo di connessione predefinito hello per le macchine virtuali Linux ospitate in Azure. Sebbene SSH stesso fornisca una connessione crittografata, l'utilizzo di password con le connessioni SSH lascia attacchi di forza toobrute vulnerabile VM hello o l'individuazione delle password. Un metodo più sicuro e preferito tooa connessione macchina virtuale tramite SSH è tramite le chiavi pubbliche e private, noto anche come chiavi SSH.

Se non si desidera che le chiavi SSH toouse, è possibile comunque accedere tooyour le macchine virtuali Linux con una password. Se la macchina virtuale non è esposto toohello Internet, l'utilizzo di password potrebbe essere sufficiente. Tuttavia, comunque necessario toomanage le password per ogni VM Linux e gestire i criteri password integro e procedure consigliate, ad esempio lunghezza minima della password e aggiornarli regolarmente. utilizzo di Hello di chiavi SSH riduce la complessità di hello della gestione delle credenziali individuali tra più macchine virtuali.

## <a name="windows-packages-and-ssh-clients"></a>Pacchetti Windows e client SSH
Ci si connette tooand gestire macchine virtuali Linux in Azure tramite un **client SSH**. I computer Windows tipicamente non hanno un client SSH installato. Hello aggiornamento Aniversary di Windows 10 aggiunti Bash per Windows e Windows 10 creatori di aggiornamento più recente hello fornisce ulteriori aggiornamenti. Questo sottosistema Windows per Linux consente utilità toorun e l'accesso, ad esempio un client SSH in modo nativo all'interno di una shell Bash. È quindi possibile seguire uno dei documenti di Linux hello, ad esempio [come le coppie di chiavi SSH toogenerate per Linux](mac-create-ssh-keys.md). Bash per Windows è ancora in fase di sviluppo e viene considerato una versione beta. Per altre informazioni su Bash per Windows, vedere [Bash in Ubuntu in Windows](https://msdn.microsoft.com/commandline/wsl/about).

Se si desidera toouse qualcosa diverso da Bash per Windows, comuni SSH Windows client che è possibile installare rientrano nei seguenti pacchetti hello:

* [Git per Windows](https://git-for-windows.github.io/)
* [puTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/)
* [MobaXterm](http://mobaxterm.mobatek.net/)
* [Cygwin](https://cygwin.com/)


## <a name="which-key-files-do-you-need-toocreate"></a>File di chiave che è necessario toocreate?
Azure richiede chiavi pubbliche e private nel formato **ssh-rsa** almeno a 2048 bit. Se si siano gestendo risorse di Azure con modello di distribuzione classica hello, è necessario anche un PEM toogenerate (`.pem` file).

Ecco gli scenari di distribuzione hello e hello tipi di file da utilizzare in ogni:

1. **SSH-rsa** chiavi sono necessari per la distribuzione utilizzando hello [portale di Azure](https://portal.azure.com)e le distribuzioni di gestione risorse usando hello [CLI di Azure](../../cli-install-nodejs.md).
   * Queste chiavi sono in genere tutto ciò che serve alla maggior parte degli utenti.
2. Oggetto `.pem` file sia le macchine virtuali necessarie toocreate mediante la distribuzione classica hello. Queste chiavi sono supportate nelle distribuzioni classica quando si utilizza hello [portale di Azure](https://portal.azure.com) o [CLI di Azure](../../cli-install-nodejs.md).
   * È necessario solo toocreate queste altre chiavi e dei certificati se si gestiscono le risorse create tramite hello modello di distribuzione classica.

## <a name="install-git-for-windows"></a>Installare Git per Windows
sezione precedente Hello elencati diversi pacchetti che includono hello `openssl` strumento per Windows. Questo strumento è chiavi pubbliche e private toocreate necessari. Hello seguente come dettaglio di esempi tooinstall e utilizzare **Git per Windows**, anche se è possibile scegliere qualsiasi pacchetto desiderato. **GIT per Windows** consente di accedere software open source aggiuntivo toosome ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) strumenti e utilità che possono essere utili quando si lavora con le macchine virtuali Linux.

1. Scaricare e installare **Git per Windows** da hello seguente posizione: [https://git-for-windows.github.io/](https://git-for-windows.github.io/).
2. Accettare le opzioni predefinite hello hello durante il processo di installazione solo se è necessario toochange li.
3. Eseguire **Git Bash** da hello **Menu Start** > **Git** > **Git Bash**. console Hello è simile toohello esempio seguente:

    ![Shell Bash di GIT per Windows](./media/ssh-from-windows/git-bash-window.png)

## <a name="create-a-private-key"></a>Creare una chiave privata
1. Nel **Git Bash** finestra, utilizzare `openssl.exe` toocreate una chiave privata. esempio Hello crea una chiave denominata `myPrivateKey` e certificato denominato `myCert.pem`:

    ```bash
    openssl.exe req -x509 -nodes -days 365 -newkey rsa:2048 \
        -keyout myPrivateKey.key -out myCert.pem
    ```

    output di Hello è simile toohello esempio seguente:

    ```bash
    Generating a 2048 bit RSA private key
    .......................................+++
    .......................+++
    writing new private key too'myPrivateKey.key'
    -----
    You are about toobe asked tooenter information that will be incorporated
    into your certificate request.
    What you are about tooenter is what is called a Distinguished Name or a DN.
    There are quite a few fields but you can leave some blank
    For some fields there will be a default value,
    If you enter '.', hello field will be left blank.
    -----
    Country Name (2 letter code) [AU]:
    ```

   Se bash segnala un errore, provare ad aprire una nuova finestra **Git Bash** con privilegi elevati. Eseguire quindi nuovamente hello `openssl` comando.

2. Hello risposta richiesto per il nome di paese, percorso, nome dell'organizzazione, e così via.
3. La nuova chiave privata e certificato vengono creati nella directory di lavoro corrente. Come misura di sicurezza, è necessario impostare le autorizzazioni di hello sulla chiave privata in modo che solo tu abbia accesso:

    ```bash
    chmod 0600 myPrivateKey.key
    ```

4. Hello [nella sezione successiva](#create-a-private-key-for-putty) dettagli utilizzando PuTTYgen tooboth visualizzare e usare la chiave pubblica di hello e creare una chiave privata specifici per l'utilizzo di PuTTY tooSSH tooLinux macchine virtuali. comando che segue Hello genera un file di chiave pubblica denominato `myPublicKey.key` che è possibile utilizzare immediatamente:

    ```bash
    openssl.exe rsa -pubout -in myPrivateKey.key -out myPublicKey.key
    ```

5. Se è necessario anche risorse classica toomanage, convertire hello `myCert.pem` troppo`myCert.cer` (X509 con codifica DER certificato). Eseguire questo passaggio facoltativo solo se è necessario toospecifically gestire risorse classica precedente.

    Convertire il certificato di hello utilizzando hello comando seguente:

    ```bash
    openssl.exe  x509 -outform der -in myCert.pem -out myCert.cer
    ```

## <a name="create-a-private-key-for-putty"></a>Creare una chiave privata per PuTTY
PuTTY è un comune client SSH per Windows. Si è toouse disponibile un client SSH che si desidera. toouse PuTTY, è necessario un ulteriore tipo di chiave di una chiave privata PuTTY (PPK) - toocreate. Se non si desidera toouse PuTTY, ignorare questa sezione.

Hello esempio seguente viene creata la chiave privata aggiuntiva in modo specifico per toouse PuTTY:

1. Utilizzare **Git Bash** tooconvert il privata della chiave in una chiave privata RSA che è possibile comprendere PuTTYgen. esempio Hello crea una chiave denominata `myPrivateKey_rsa` dalla chiave di hello esistente denominato `myPrivateKey`:

    ```bash
    openssl rsa -in ./myPrivateKey.key -out myPrivateKey_rsa
    ```

    Come misura di sicurezza, è necessario impostare le autorizzazioni di hello sulla chiave privata in modo che solo tu abbia accesso:

    ```bash
    chmod 0600 myPrivateKey_rsa
    ```
2. Scaricare ed eseguire PuTTYgen dalla seguente posizione hello: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
3. Fare clic sul menu hello: **File** > **chiave privata di carico**
4. Individuare la chiave privata (`myPrivateKey_rsa` nell'esempio precedente hello). directory predefinita di Hello quando si avvia **Git Bash** è `C:\Users\%username%`. Modificare hello file filtro tooshow **tutti i file (\*.\*)** :

    ![Caricare la chiave privata esistente di hello in PuTTYgen](./media/ssh-from-windows/load-private-key.png)
5. Fare clic su **Apri**. Un messaggio indica che tale chiave hello è stato importato correttamente:

    ![Completare l'importazione della chiave tooPuTTYgen](./media/ssh-from-windows/successfully-imported-key.png)
6. Fare clic su **OK** prompt hello tooclose.
7. la chiave pubblica di Hello viene visualizzata nella parte superiore di hello di hello **PuTTYgen** finestra. Copiare e incollare la chiave pubblica hello portale di Azure o il modello di gestione risorse di Azure quando si crea una VM Linux. È anche possibile fare clic su **Salva la chiave pubblica** toosave un computer tooyour copia:

    ![Salvare un file di chiave pubblica PuTTY](./media/ssh-from-windows/save-public-key.png)

    Hello esempio seguente viene illustrato come è necessario copiare e incollare la chiave pubblica hello portale di Azure quando si crea una VM Linux. la chiave pubblica di Hello in genere verrà quindi archiviata `~/.ssh/authorized_keys` nella nuova VM.

    ![Utilizzare la chiave pubblica quando si crea una macchina virtuale nel portale di Azure hello](./media/ssh-from-windows/use-public-key-azure-portal.png)
8. Quando si torna in **PuTTYgen**, fare clic su **Save private Key**:

    ![Salvare il file di chiave privata PuTTY](./media/ssh-from-windows/save-ppk-file.png)

   > [!WARNING]
   > Un viene richiesto se si desidera toocontinue senza immettere una passphrase per la chiave. Una passphrase è ad esempio una chiave privata associata tooyour di password. Anche se un utente non tooobtain la chiave privata, ancora non sarebbero in grado di tooauthenticate chiave appena hello. È inoltre necessario hello passphrase. Senza una passphrase, se un utente ottiene la chiave privata, possono accedere tooany macchina virtuale o del servizio che utilizza chiave. Creare una passphrase è altamente consigliato. Tuttavia, se si dimentica di hello passphrase, non è toorecover alcun modo il.
   >
   >

    Se si desidera tooenter una passphrase, fare clic su **n**, immettere una passphrase nella finestra principale di PuTTYgen hello e quindi fare clic su **Salva la chiave privata** nuovamente. In caso contrario, fare clic su **Sì** toocontinue senza fornire una passphrase facoltativa hello.
9. Immettere un nome e il percorso di toosave file PPK.

## <a name="use-putty-toossh-tooa-linux-machine"></a>Usare Putty tooSSH tooa computer Linux
PuTTY, come indicato in precedenza, è un comune client SSH per Windows. Si è toouse disponibile un client SSH che si desidera. Hello seguente come dettaglio di passaggi toouse il tooauthenticate chiave privata con la macchina virtuale di Azure tramite SSH. Hello passaggi sono simili in altri client della chiave SSH in termini che necessitano di tooload la connessione SSH di hello tooauthenticate chiave privata.

1. Download e l'esecuzione di putty da hello seguente percorso: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
2. Immettere nome host hello o un indirizzo IP della macchina virtuale dal portale di Azure hello:

    ![Aprire una nuova connessione PuTTY](./media/ssh-from-windows/putty-new-connection.png)
3. Prima di selezionare **Apri**, fare clic sulla scheda **Connessione** > **SSH** > **Aut**. Sfoglia tooand selezionare la chiave privata:

    ![Selezionare la chiave privata PuTTY per l'autenticazione](./media/ssh-from-windows/putty-auth-dialog.png)
4. Fare clic su **aprire** macchina virtuale di tooconnect tooyour

## <a name="next-steps"></a>Passaggi successivi
È anche possibile generare le chiavi pubbliche e private hello [con OS X e Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Per ulteriori informazioni sulla barra rovesciata per Windows e i vantaggi di hello di disporre di strumenti di sistemi operativi disponibili nel computer Windows, vedere [Bash in Ubuntu in Windows](https://msdn.microsoft.com/commandline/wsl/about).

Nel caso di problemi nell'utilizzo di SSH tooconnect tooyour le macchine virtuali Linux, vedere [tooan connessioni risolvere SSH VM Linux di Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
