### <a name="determine-hello-dns-name-of-hello-virtual-machine"></a>Determinare il nome DNS hello della macchina virtuale hello
tooconnect toohello, il motore di Database di SQL Server da un altro computer, è necessario conoscere hello sistema DNS (Domain Name) nome della macchina virtuale hello. (Si tratta di hello Nome hello internet utilizza tooidentify hello macchina virtuale. È possibile utilizzare l'indirizzo IP di hello, ma l'indirizzo IP hello potrebbe cambiare quando Azure consente di spostare risorse per la ridondanza o la manutenzione. nome DNS Hello sarà stabile perché può essere reindirizzato tooa nuovo indirizzo IP.)  

1. Nel portale di Azure hello (o dal passaggio precedente hello), selezionare **macchine virtuali (classico)**.
2. Selezionare la macchina virtuale di SQL.
3. In hello **macchina virtuale** blade, hello copia **nome DNS** per la macchina virtuale hello.
   
    ![Nome DNS](./media/virtual-machines-sql-server-connection-steps/sql-vm-dns-name.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>Connettersi toohello motore di Database da un altro computer
1. In un computer connesso toohello internet, aprire SQL Server Management Studio.
2. In hello **connettersi tooServer** o **connettersi tooDatabase motore** della finestra di dialogo hello **nome Server** , immettere il nome DNS hello della macchina virtuale hello (determinata hello attività precedente) e un numero di porta endpoint pubblico nel formato hello *Nomedns, NumeroPorta* , ad esempio **mysqlvm.cloudapp.net,57500**.
   
    ![Connessione tramite SQL Server Management Studio](./media/virtual-machines-sql-server-connection-steps/33Connect-SSMS.png)
   
    Se non si ricorda di numero di porta pubblica endpoint hello creato in precedenza, sarà possibile trovarlo in hello **endpoint** area di hello **macchina virtuale** blade.
   
    ![Public Port](./media/virtual-machines-sql-server-connection-steps/sql-vm-port-number.png)
3. In hello **autenticazione** , quindi selezionare **autenticazione di SQL Server**.
4. In hello **accesso** casella, il nome del tipo hello di un account di accesso è stato creato in un'attività precedente.
5. In hello **Password** casella, digitare la password dell'account di accesso di hello creati in un'attività precedente hello.
6. Fare clic su **Connetti**.

