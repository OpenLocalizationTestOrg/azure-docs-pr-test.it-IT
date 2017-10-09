1. Accedi toohello [portale di Azure classico](http://manage.windowsazure.com).  
2. Nella barra dei comandi hello nella parte inferiore di hello della finestra hello, fare clic su **New**.
3. Fare clic su **Calcolo**, **Macchina virtuale** e quindi su **Da raccolta**.
   
    ![Creare una nuova macchina virtuale][Image1]
4. In hello **SUSE** gruppo, selezionare un'immagine di macchina virtuale OpenSUSE e quindi fare clic su toocontinue freccia hello.
5. In hello prima **configurazione della macchina virtuale** pagina:
   
   * Specificare un **Nome macchina virtuale**, ad esempio "testlinuxvm". nome Hello deve essere compresa tra 3 e 15 caratteri, può contenere solo lettere, numeri e trattini, deve iniziare con una lettera e terminare con una lettera o un numero.
   * Verificare hello **livello** e selezionare un **dimensioni**. livello Hello determina le dimensioni di hello che è possibile scegliere. Hello influisce sulle dimensioni hello costo legato all'utilizzo, nonché opzioni di configurazione, ad esempio il numero di dischi dati di cui è possibile collegare. Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
   * Digitare un **nuovo nome utente**, o accettare l'impostazione predefinita di hello, **azureuser**. Questo nome viene aggiunto un file elenco file toohello.
   * Decidere quale tipo di **autenticazione** toouse. Per linee guida generali relative alle password, vedere [Password complesse](http://msdn.microsoft.com/library/ms161962.aspx).
6. In hello Avanti **configurazione della macchina virtuale** pagina:
   
   * Utilizzare hello predefinito **creare un nuovo servizio cloud**.
   * In hello **nome DNS** , digitare un toouse di nome DNS univoco come parte dell'indirizzo hello, ad esempio "testlinuxvm".
   * In hello **affinità di area/gruppo/rete virtuale** , selezionare un'area in cui verrà ospitata questa immagine virtuale.
   * In **endpoint**, mantenere l'endpoint di hello SSH. È possibile aggiungere altri utenti a questo punto, o aggiungere, modificare o eliminarli dopo la creazione della macchina virtuale hello.
     
     > [!NOTE]
     > Se si desidera toouse una macchina virtuale una rete virtuale, si **deve** specificare la rete virtuale di hello quando si crea una macchina virtuale hello. È possibile aggiungere una rete virtuale della macchina virtuale tooa dopo aver creato una macchina virtuale hello. Per altre informazioni, vedere [Panoramica di Rete virtuale](../articles/virtual-network/virtual-networks-overview.md).
     > 
     > 
7. In hello ultimo **configurazione della macchina virtuale** pagina, mantenere le impostazioni predefinite di hello e quindi fare clic su hello toofinish di segno di spunta.

portale Hello Elenca hello nuova macchina virtuale in **macchine virtuali**. Mentre hello stato viene indicato come **(Provisioning)**, macchina virtuale hello viene configurato. Quando lo stato di hello viene dichiarato come **esecuzione**, è possibile spostare nel passaggio successivo toohello.

## <a name="connect-toohello-virtual-machine"></a>Connettersi toohello macchina virtuale
Si useranno SSH o PuTTY tooconnect toohello macchina virtuale, a seconda del sistema operativo hello Hello che connettersi computer hello:

* Da un computer che esegue Linux, usare SSH. Al prompt dei comandi di hello, digitare:
  
    `$ ssh newuser@testlinuxvm.cloudapp.net -o ServerAliveInterval=180`
  
    Digitare la password dell'utente hello.
* Da un computer che esegue Windows, usare PuTTY. Se si non è installato, scaricarlo da hello [pagina di Download di PuTTY][PuTTYDownload].
  
    Salvare **putty.exe** tooa directory sul computer. Aprire un prompt dei comandi, passare toothat cartella ed eseguire **putty.exe**.
  
    Digitare nome host hello, ad esempio "testlinuxvm.cloudapp.net," e "22" per hello **porta**.
  
    ![Schermata di PuTTY][Image6]  

## <a name="update-hello-virtual-machine-optional"></a>Aggiornare hello macchina virtuale (facoltativo)
1. Dopo avere acquisito una macchina virtuale toohello connesso, è possibile installare facoltativamente le patch e aggiornamenti del sistema. aggiornamento di hello toorun, tipo:
   
    `$ sudo zypper update`
2. Selezionare **Software**, quindi **aggiornamento in linea** gli aggiornamenti disponibili toolist. Selezionare **Accept** toostart hello installazione e applicare tutte le patch disponibili nuova (ad eccezione del fatto hello facoltativi).
3. Al termine dell'installazione fare clic su **Finish**.  Il sistema è ora backup toodate.

[PuTTYDownload]: http://www.puttyssh.org/download.html

[Image1]: ./media/create-and-configure-opensuse-vm-in-portal/CreateVM.png

[Image6]: ./media/create-and-configure-opensuse-vm-in-portal/putty.png
