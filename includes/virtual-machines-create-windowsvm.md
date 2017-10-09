1. Accedi toohello [portale di Azure](https://portal.azure.com).

2. A partire da in alto a sinistra di hello, fare clic su **nuovo > calcolo > Data Center di Windows Server 2016**.

    ![Passare toohello immagini di macchina virtuale di Azure nel portale di hello](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. Scegliere modello di distribuzione classica hello hello Datacenter di Windows Server 2016. Fare clic su Crea.

    ![Schermata che mostra le immagini di macchina virtuale di Azure hello disponibile nel portale di hello](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a>1. Pannello Nozioni di base

Pannello nozioni di base Hello richiede informazioni amministrative per la macchina virtuale hello.

1. Immettere un **nome** per la macchina virtuale hello. Nell'esempio hello _HeroVM_ hello nome della macchina virtuale hello. nome Hello deve essere 1-15 caratteri e non può contenere caratteri speciali.

2. Immettere un **nome utente** e un nome sicuro **Password** che vengono utilizzati toocreate un account locale nella macchina virtuale hello. Hello account locale viene utilizzato in tooand toosign gestire hello macchina virtuale. Nell'esempio hello _azureuser_ è il nome utente hello.

 Hello password deve essere 8-123 caratteri e soddisfare tre hello quattro seguenti i requisiti di complessità: una lettera minuscola, una lettera maiuscola, un numero e un carattere speciale. Sono disponibili altre informazioni sui [requisiti relativi a nome utente e password](../articles/virtual-machines/windows/faq.md).

3. Hello **sottoscrizione** è facoltativo. Un'impostazione comune è "Uso prepagato".

4. Selezionare un oggetto esistente **gruppo di risorse** o nome di tipo hello uno nuovo. Nell'esempio hello _HeroVMRG_ nome hello hello del gruppo di risorse.

5. Selezionare un Data Center Azure **percorso** in cui si desidera toorun VM hello. Nell'esempio hello **Stati Uniti orientali** hello posizione.

6. Al termine, fare clic su **Avanti** toocontinue toohello Avanti blade.

    ![Schermata che mostra le impostazioni di hello in Pannello di hello nozioni di base per la configurazione di una macchina virtuale di Azure](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a>2. Pannello Dimensioni

Pannello dimensioni Hello identifica i dettagli di configurazione hello di hello VM ed elenca varie opzioni che includono del sistema operativo, numero di processori, tipo di archiviazione su disco e costi di utilizzo mensile stimato.  

Scegliere una dimensione di macchina virtuale e quindi fare clic su **selezionare** toocontinue. In questo esempio, _DS1_\__V2 Standard_ è hello dimensione di macchina virtuale.

  ![Schermata del Pannello di dimensioni hello che mostra hello dimensioni delle macchine Virtuali di Azure che è possibile selezionare](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a>3. Pannello Impostazioni

pannello impostazioni Hello richiede le opzioni di archiviazione e rete. È possibile accettare le impostazioni predefinite di hello. Se necessario, Azure crea le voci appropriate.

Se sono state selezionate dimensioni di macchina virtuale che lo supportano, è possibile provare il servizio Archiviazione Premium di Azure selezionando Premium (SSD) nel Tipo di disco.

Al termine delle modifiche, fare clic su **OK**.

## <a name="4-summary-blade"></a>4. Pannello Riepilogo

Pannello riepilogo Hello Elenca le impostazioni di hello specificate in pannelli precedente hello. Fare clic su **OK** quando si è pronti toomake immagine di hello.

 ![Pannello riepilogo report fornendo specificate le impostazioni della macchina virtuale hello](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

Dopo la creazione di macchine virtuali hello, vengono visualizzati hello nuova macchina virtuale nel portale di hello **tutte le risorse**e viene visualizzato un riquadro della macchina virtuale hello nel dashboard di hello. Hello corrispondente cloud storage account e inoltre vengono creati ed elencati. Macchina virtuale hello sia il servizio cloud vengono avviate automaticamente e il relativo stato viene elencato come **esecuzione**.

 ![Configurare gli endpoint di agente di macchine Virtuali e hello della macchina virtuale hello](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
