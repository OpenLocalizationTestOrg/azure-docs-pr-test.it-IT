1. Eseguire file di installazione di programma di installazione unificata hello.
2. In **prima di iniziare**selezionare **installare server di configurazione hello e server di elaborazione**.

    ![Prima di iniziare](./media/site-recovery-add-configuration-server/combined-wiz1.png)

3. In **licenza Software di terze parti**, fare clic su **accetto** toodownload e installare MySQL.

    ![Software di terze parti](./media/site-recovery-add-configuration-server/combined-wiz2.png)
4. In **registrazione**, selezionare la chiave di registrazione hello scaricato dall'insieme di credenziali hello.

    ![Registrazione](./media/site-recovery-add-configuration-server/combined-wiz3.png)
5. In **impostazioni Internet**, specificare la modalità Provider in esecuzione nel server di configurazione di hello, tooAzure il ripristino del sito si connette tramite hello hello Internet.

   a. Se si desidera tooconnect proxy hello che è attualmente configurato nel computer di hello, selezionare **connettersi tooAzure ripristino del sito utilizzando un server proxy**.

   b. Se si desidera hello Provider tooconnect direttamente, selezionare **connettersi direttamente tooAzure il ripristino del sito senza un server proxy**.

   c. Selezionare se hello esistente proxy richiede l'autenticazione, o se si desidera toouse un proxy personalizzato per la connessione al Provider di hello, **Connetti con impostazioni proxy personalizzate**.

     * Se si utilizza un proxy personalizzato, sono necessarie le credenziali, porta e indirizzo hello toospecify.
     * Se si utilizza un proxy, è necessario avere già hello URL consentiti descritto in [prerequisiti](#prerequisites).

     ![Firewall](./media/site-recovery-add-configuration-server/combined-wiz4.png)
6. In **controllo dei prerequisiti**, il programma di installazione viene eseguito un toomake controllo assicura che vengano eseguite l'installazione. Se viene visualizzato un avviso su hello **controllo sincronizzazione globale**, verificare che ora hello clock di sistema hello (**data e ora** impostazioni) hello stesso fuso orario hello.

    ![Prerequisiti](./media/site-recovery-add-configuration-server/combined-wiz5.png)
7. In **configurazione MySQL**, creare le credenziali per la registrazione nell'istanza di server MySQL toohello installato.

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz6.png)
8. In **dettagli sull'ambiente**selezionare se si ha intenzione di macchine virtuali VMware tooreplicate. In caso affermativo, il programma di installazione verifica quindi se è installato PowerCLI 6.0.

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz7.png)

9. In **Install Location**, selezionare dove si desidera che i file binari hello tooinstall e archiviazione la cache di hello. unità di Hello selezionata deve avere almeno 5 GB di spazio disponibile su disco, ma è consigliabile un'unità di cache con un minimo di 600 GB di spazio libero.

    ![Percorso di installazione](./media/site-recovery-add-configuration-server/combined-wiz8.png)
10. In **Selezione rete**, specificare i listener di hello (scheda di rete e porta SSL) su quali server di configurazione hello Invia e riceve dati di replica. Porta 9443 è hello predefinita utilizzata per inviare e ricevere il traffico di replica, ma è possibile modificare questo toosuit numero di porta i requisiti dell'ambiente. Nella porta toohello aggiunta 9443, è inoltre possibile aprire la porta 443, che viene utilizzata da un'operazione di replica tooorchestrate server web. Non usare la porta 443 per inviare o ricevere traffico di replica.

    ![Selezione rete](./media/site-recovery-add-configuration-server/combined-wiz9.png)


11. In **riepilogo**, esaminare le informazioni di hello e fare clic su **installare**. Al termine dell'installazione verrà generata una passphrase. Sarà necessaria quando si abilita la replica, è quindi consigliabile copiarla e conservarla in un luogo sicuro.

    ![Riepilogo](./media/site-recovery-add-configuration-server/combined-wiz10.png)

Al termine della registrazione, il server di hello viene visualizzato nella hello **impostazioni** > **server** pannello nell'insieme di credenziali hello.
