### <a name="open-tcp-ports-in-hello-windows-firewall-for-hello-default-instance-of-hello-database-engine"></a>Porte TCP aperte nel firewall di Windows hello per l'istanza predefinita di hello di hello motore di Database
1. Connessione macchina virtuale toohello con Desktop remoto. Per istruzioni dettagliate sulla connessione toohello VM, vedere [aprire una VM SQL con Desktop remoto](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md#open-the-vm-with-remote-desktop).
2. Una volta effettuato l'accesso, nella schermata Start hello digitare **WF.msc**, quindi premere INVIO.
   
    ![Avviare il programma Firewall hello](./media/virtual-machines-sql-server-connection-steps/12Open-WF.png)
3. In hello **Windows Firewall con sicurezza avanzata**, in hello riquadro sinistro, destro **regole connessioni in entrata**, quindi fare clic su **nuova regola** nel riquadro azioni hello.
   
    ![Nuova regola](./media/virtual-machines-sql-server-connection-steps/13New-FW-Rule.png)
4. In hello **in ingresso Creazione guidata nuova regola** nella finestra di dialogo **tipo di regola**selezionare **porta**e quindi fare clic su **Avanti**.
5. In hello **protocollo e porte** finestra di dialogo, hello predefinito **TCP**. In hello **porte locali specifiche** casella, quindi hello tipo numero di porta dell'istanza hello hello motore di Database (**1433** per l'istanza predefinita di hello o un altro per la porta privata hello nel passaggio endpoint hello).
   
    ![Porta TCP 1433](./media/virtual-machines-sql-server-connection-steps/14Port-1433.png)
6. Fare clic su **Avanti**.
7. In hello **azione** nella finestra di dialogo **Consenti connessione hello**, quindi fare clic su **Avanti**.
   
    **Nota sulla sicurezza:** selezionando **Consenti solo connessione hello sicura** può fornire protezione aggiuntiva. Selezionare questa opzione se si desiderano tooconfigure ulteriori opzioni di sicurezza nell'ambiente in uso.
   
    ![Consentire le connessioni](./media/virtual-machines-sql-server-connection-steps/15Allow-Connection.png)
8. In hello **profilo** nella finestra di dialogo **pubblica**, **privata**, e **dominio**. Quindi fare clic su **Next**.
   
    **Nota sulla sicurezza:** selezionando **pubblica** consente l'accesso tramite internet hello. Se possibile, scegliere un profilo più restrittivo.
   
    ![Profilo Pubblico](./media/virtual-machines-sql-server-connection-steps/16Public-Private-Domain-Profile.png)
9. In hello **nome** nella finestra di dialogo digitare un nome e una descrizione per questa regola e quindi fare clic su **fine**.
   
    ![Nome regola](./media/virtual-machines-sql-server-connection-steps/17Rule-Name.png)

Aprire altre porte per altri componenti in base alle esigenze. Per ulteriori informazioni, vedere [configurazione hello Windows Firewall tooAllow accesso a SQL Server](http://msdn.microsoft.com/library/cc646023.aspx).

### <a name="configure-sql-server-toolisten-on-hello-tcp-protocol"></a>Configurare SQL Server toolisten su hello protocollo TCP

[!INCLUDE [Enable TCP](virtual-machines-sql-server-connection-tcp-protocol.md)]

### <a name="configure-sql-server-for-mixed-mode-authentication"></a>Configurare SQL Server per l'autenticazione in modalità mista
Hello il motore di Database di SQL Server non è possibile utilizzare l'autenticazione di Windows senza l'ambiente di dominio. tooconnect toohello motore di Database da un altro computer, configurare SQL Server per l'autenticazione modalità mista. L'autenticazione in modalità mista consente sia l'autenticazione di SQL Server sia l'autenticazione di Windows.

> [!NOTE]
> Se è stata configurata una Rete virtuale di Azure con un ambiente di dominio configurato, potrebbe non essere necessario configurare l'autenticazione in modalità mista.
> 
> 

1. Durante la macchina virtuale connessa toohello, nella pagina iniziale di hello, digitare **SQL Server Management Studio** e fare clic sull'icona selezionata hello.
   
    Hello prima apertura di Management Studio, è necessario creare l'ambiente di hello utenti Management Studio. L'operazione potrebbe richiedere alcuni istanti.
2. Management Studio presenta hello **connettersi tooServer** la finestra di dialogo. In hello **nome Server** casella, il nome del tipo hello di hello macchina virtuale tooconnect toohello motore di Database con Esplora oggetti hello (anziché il nome di macchina virtuale hello è inoltre possibile utilizzare **(local)** o singolo periodo come hello **nome Server**). Selezionare **l'autenticazione di Windows**, lasciando  ***your_VM_name*\your_local_administrator** in hello **nome utente** casella. Fare clic su **Connetti**.
   
    ![Connettersi tooServer](./media/virtual-machines-sql-server-connection-steps/19Connect-to-Server.png)
3. In SQL Server Management Studio Esplora oggetti fare doppio clic su nome hello dell'istanza di hello di SQL Server (nome della macchina virtuale hello) e quindi fare clic su **proprietà**.
   
    ![Proprietà del server](./media/virtual-machines-sql-server-connection-steps/20Server-Properties.png)
4. In hello **sicurezza** pagina **l'autenticazione Server**selezionare **modalità di autenticazione di Windows e SQL Server**e quindi fare clic su **OK** .
   
    ![Selezione della modalità di autenticazione](./media/virtual-machines-sql-server-connection-steps/21Mixed-Mode.png)
5. Nella finestra di dialogo SQL Server Management Studio hello, fare clic su **OK** tooacknowledge hello requisito toorestart SQL Server.
6. In Esplora oggetti fare clic con il pulsante destro del mouse sul server e quindi scegliere **Riavvia**. (Se SQL Server Agent è in esecuzione, anch'esso dovrà essere riavviato).
   
    ![Riavvia](./media/virtual-machines-sql-server-connection-steps/22Restart2.png)
7. Nella finestra di dialogo SQL Server Management Studio hello, fare clic su **Sì** tooagree che si desidera toorestart SQL Server.

### <a name="create-sql-server-authentication-logins"></a>Creare gli account di accesso di SQL Server
tooconnect toohello motore di Database da un altro computer, è necessario creare almeno un accesso con autenticazione SQL Server.

1. In SQL Server Management Studio Esplora oggetti espandere la cartella hello hello dell'istanza del server in cui si desidera toocreate hello nuovo account di accesso.
2. Pulsante destro del mouse hello **sicurezza** cartella, scegliere troppo**nuovo**e selezionare **account di accesso...** .
   
    ![Nuovo account di accesso](./media/virtual-machines-sql-server-connection-steps/23New-Login.png)
3. In hello **accesso - nuovo** della finestra di dialogo hello **generale** pagina, immettere il nome di hello del nuovo utente hello in hello **nome account di accesso** casella.
4. Selezionare **Autenticazione di SQL Server**.
5. In hello **Password** casella, immettere una password per hello nuovo utente. Immettere nuovamente quella password in hello **Conferma Password** casella.
6. Selezionare opzioni di imposizione hello password necessarie (**Applica criteri password**, **Imponi scadenza password**, e **cambiamento obbligatorio password all'accesso successivo**). Se si utilizza questo account di accesso per se stessi, non è necessaria una modifica della password all'accesso successivo hello toorequire.
7. Da hello **database predefinito** , selezionare un database predefinito per l'account di accesso hello. **master** hello predefinito per questa opzione. Se non è ancora stato creato un database utente, lasciare questa impostazione è troppo**master**.
   
    ![Proprietà account di accesso](./media/virtual-machines-sql-server-connection-steps/24Test-Login.png)
8. Nel caso di accesso di hello prima che si sta creando, è consigliabile toodesignate questo account di accesso come amministratore di SQL Server. In tal caso, hello **i ruoli del Server** controllo pagina **sysadmin**.
   
   > [!NOTE]
   > I membri del ruolo predefinito del server sysadmin di hello sono controllo completo di hello motore di Database. È consigliabile limitare attentamente le appartenenze a questo ruolo.
   > 
   > 
   
   ![sysadmin](./media/virtual-machines-sql-server-connection-steps/25sysadmin.png)
9. Fare clic su OK.

Per ulteriori informazioni sugli account di accesso di SQL Server, vedere [Creazione di un account di accesso](http://msdn.microsoft.com/library/aa337562.aspx).

