1. Avviare hello Azure Site Recovery UnifiedSetup.exe
2. In **prima di iniziare**selezionare **aggiungere processo aggiuntivo server tooscale distribuzione**.

  ![Aggiungere il server di elaborazione](./media/site-recovery-add-process-server/ps-page-1.png)

3. In **i dettagli di configurazione Server**, specificare l'indirizzo IP hello del Server di configurazione hello e hello passphrase.

  ![Aggiungere il server di elaborazione 2](./media/site-recovery-add-process-server/ps-page-2.png)
4. In **impostazioni Internet**, specificare la modalità Provider in esecuzione nel Server di configurazione di hello, tooAzure il ripristino del sito si connette tramite hello hello Internet.

  ![Aggiungere il server di elaborazione 3](./media/site-recovery-add-process-server/ps-page-3.png)

   * Se si desidera tooconnect proxy hello che è attualmente configurato nel computer di hello, selezionare **Connetti con impostazioni proxy esistenti**.
   * Se si desidera hello Provider tooconnect direttamente, selezionare **Connetti direttamente senza un proxy**.
   * Selezionare se hello esistente proxy richiede l'autenticazione, o se si desidera toouse un proxy personalizzato per la connessione al Provider di hello, **Connetti con impostazioni proxy personalizzate**.

     * Se si utilizza un proxy personalizzato, sono necessarie le credenziali, porta e indirizzo hello toospecify.
     * Se si utilizza un proxy, deve aver già consentito accesso toohello gli URL del servizio.

5. In **controllo dei prerequisiti**, il programma di installazione viene eseguito un toomake controllo assicura che vengano eseguite l'installazione. Se viene visualizzato un avviso su hello **controllo sincronizzazione globale**, verificare che ora hello clock di sistema hello (**data e ora** impostazioni) hello stesso fuso orario hello.

     ![Aggiungere il server di elaborazione 4](./media/site-recovery-add-process-server/ps-page-4.png)

6. In **dettagli sull'ambiente**selezionare se si ha intenzione di macchine virtuali VMware tooreplicate. In caso affermativo, il programma di installazione verifica quindi se è installato PowerCLI 6.0.

     ![Aggiungere il server di elaborazione 5](./media/site-recovery-add-process-server/ps-page-5.png)

7. In **Install Location**, selezionare dove si desidera che i file binari hello tooinstall e archiviazione la cache di hello. unità di Hello selezionata deve avere almeno 5 GB di spazio disponibile su disco, ma è consigliabile un'unità di cache con un minimo di 600 GB di spazio libero.
     ![Aggiungere il server di elaborazione 5](./media/site-recovery-add-process-server/ps-page-6.png)

8. In **Selezione rete**specificare listener hello (scheda di rete e porta SSL) sul quale il Server di configurazione a hello Invia e riceve dati di replica. Porta 9443 è hello predefinita utilizzata per inviare e ricevere il traffico di replica, ma è possibile modificare questo toosuit numero di porta i requisiti dell'ambiente. Nella porta toohello aggiunta 9443, è inoltre possibile aprire la porta 443, che viene utilizzata da un'operazione di replica tooorchestrate server web. Non usare la porta 443 per inviare o ricevere traffico di replica.

     ![Aggiungere il server di elaborazione 6](./media/site-recovery-add-process-server/ps-page-7.png)
9. In **riepilogo**, esaminare le informazioni di hello e fare clic su **installare**. Al termine dell'installazione verrà generata una passphrase. Sarà necessaria quando si abilita la replica, è quindi consigliabile copiarla e conservarla in un luogo sicuro.

     ![Aggiungere il server di elaborazione 7](./media/site-recovery-add-process-server/ps-page-8.png)
