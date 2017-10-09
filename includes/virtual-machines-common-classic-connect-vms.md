

![Macchine virtuali in un servizio cloud autonomo](./media/virtual-machines-common-classic-connect-vms/CloudServiceExample.png)

Se si inseriscono delle macchine virtuali in una rete virtuale, è possibile decidere quanti servizi cloud da toouse per caricare set di bilanciamento del carico e disponibilità. Inoltre, è possibile organizzare le macchine virtuali hello su subnet in hello come locale di rete e connettono hello tooyour di rete virtuale locale rete. Ad esempio:

![Macchine virtuali in una rete virtuale](./media/virtual-machines-common-classic-connect-vms/VirtualNetworkExample.png)

Le reti virtuali sono hello consigliato modo tooconnect le macchine virtuali in Azure. Hello consigliata è tooconfigure ogni livello dell'applicazione in un servizio cloud separato. Tuttavia, potrebbe essere necessario toocombine alcune macchine virtuali da diversi livelli di applicazione in hello stesso cloud tooremain servizio all'interno di massimo hello di 200 servizi cloud per ogni sottoscrizione. tooreview questo e altri limiti, vedere [sottoscrizione Azure e limiti dei servizi, quote e vincoli](../articles/azure-subscription-service-limits.md).

## <a name="connect-vms-in-a-virtual-network"></a>Connettere le macchine virtuali in una rete virtuale
tooconnect le macchine virtuali in una rete virtuale:

1. Creare la rete virtuale di hello in hello [portale di Azure](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) e specificare 'distribuzione classica'.
2. Creare set di hello di servizi cloud per la distribuzione di tooreflect la progettazione per i set di disponibilità e bilanciamento del carico. Nel portale di Azure hello, fare clic su **nuovo > calcolo > servizio Cloud** per ogni servizio cloud.

  In fase di compilazione, i dettagli del servizio cloud hello scegliere hello stesso _gruppo di risorse_ utilizzata con la rete virtuale hello.

3. ogni nuova virtuale toocreate macchina, fare clic su **nuovo > calcolo**, quindi selezionare hello immagine di macchina virtuale appropriata da hello **App in evidenza**.

  Nella macchina virtuale hello **nozioni di base** pannello, scegliere hello stesso _gruppo di risorse_ utilizzata con la rete virtuale hello.

  ![Pannello Nozioni di base della macchina virtuale quando si usa una rete virtuale](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_VN.png)

4. In fase di compilazione hello VM **impostazioni**, scegliere hello corretto _servizio Cloud_ o _rete virtuale_ per hello macchina virtuale.

  Azure selezionerà hello altri elementi in base alla selezione.

  ![Pannello Impostazioni della macchina virtuale quando si usa una rete virtuale](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_VN.png)


## <a name="connect-vms-in-a-standalone-cloud-service"></a>Connettere le macchine virtuali in un servizio cloud autonomo
tooconnect le macchine virtuali in un servizio cloud autonomo:

1. Crea servizio cloud di hello in hello [portale di Azure](http://portal.azure.com). Fare clic su **Nuovo > Calcolo > Servizio cloud**. In alternativa, è possibile creare il servizio cloud hello per la distribuzione quando si crea la prima macchina virtuale.
2. Quando si creano le macchine virtuali hello, scegliere hello stesso gruppo di risorse utilizzato con il servizio cloud hello.

  ![Aggiungere un servizio cloud esistente tooan macchina virtuale](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_SA.png)

3.  In fase di compilazione dettagli VM hello, scegliere il nome di hello del servizio cloud creato nel primo passaggio hello.

  ![Selezione di un servizio cloud per una macchina virtuale](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_SA.png)
