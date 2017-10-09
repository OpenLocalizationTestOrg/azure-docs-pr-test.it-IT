#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a>endpoint pubblici toocreate nel dispositivo cloud hello

1. Accedi toohello portale di Azure.
2. Andare troppo**macchine virtuali**, quindi selezionare e fare clic sulla macchina virtuale hello che viene usato come dispositivo di cloud.
    
3. È necessario toocreate rete sicurezza gruppo () regola toocontrol hello flusso di traffico da e verso la macchina virtuale. Eseguire hello seguendo i passaggi toocreate una regola di gruppo.
    1. Selezionare **Gruppo di sicurezza di rete**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. Fare clic su hello predefinito rete gruppo di sicurezza viene presentato.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. Selezionare **Regole di sicurezza in ingresso**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. Fare clic su **+ Aggiungi** toocreate una regola di sicurezza in ingresso.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        Nel pannello regole di sicurezza in ingresso Aggiungi di hello:

        1. Per hello **nome**, digitare quanto segue di hello assegnare un nome per l'endpoint di hello: WinRMHttps.
        
        2. Per hello **priorità**, selezionare un numero minore di 1000 (priorità hello per regola predefinita hello). Valore più alto hello, una priorità inferiore hello.

        3. Set hello **origine** troppo**qualsiasi**.

        4. Per hello **servizio**selezionare **WinRM**. Hello **protocollo** viene impostata automaticamente troppo**TCP** hello e **intervallo di porte** è troppo**5986**.

        5. Fare clic su **OK** regola hello toocreate.

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. Il passaggio finale consiste tooassociate la sicurezza della rete di gruppo con una subnet o un'interfaccia di rete specifici. Eseguire hello seguendo i passaggi tooassociate il gruppo di sicurezza di rete con una subnet.
    1. Andare troppo**subnet**.
    2. Fare clic su **+ Associa**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. Selezionare la rete virtuale e quindi selezionare la subnet appropriata hello.
    4. Fare clic su **OK** regola hello toocreate.

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

Dopo aver creata la regola hello, è possibile visualizzare il relativo indirizzo IP virtuale pubblico (VIP) di dettagli toodetermine hello. Registrare tale indirizzo.


