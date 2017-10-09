### <a name="configure-a-dns-label-for-hello-public-ip-address"></a>Configurare un'etichetta di DNS per l'indirizzo IP pubblico hello

tooconnect toohello, il motore di Database di SQL Server da hello Internet, è consigliabile creare un'etichetta di DNS per l'indirizzo IP pubblico. È possibile connettersi utilizzando l'indirizzo IP ma hello etichetta DNS crea un Record che è più facile tooidentify e riassunti hello sottostante indirizzo IP pubblico.

> [!NOTE]
> Le etichette DNS non sono necessari se piano tooonly connettersi a SQL Server toohello istanza hello stessa rete virtuale o solo in locale.

toocreate un'etichetta di DNS, selezionare innanzitutto **macchine virtuali** nel portale di hello. Selezionare la macchina virtuale SQL Server di toobring visualizzarne le proprietà.

1. Nella panoramica delle macchine virtuali hello, selezionare il **indirizzo IP pubblico**.

    ![indirizzo ip pubblico](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. Nelle proprietà hello all'indirizzo IP pubblico, espandere **configurazione**.

1. Immettere un nome per l'etichetta DNS. Questo nome è un Record che possono essere utilizzati tooconnect tooyour macchina virtuale SQL Server in base al nome anziché in base all'indirizzo IP direttamente.

1. Fare clic su hello **salvare** pulsante.

    ![etichetta dns](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>Connettersi toohello motore di Database da un altro computer

1. In un computer connesso toohello internet, aprire SQL Server Management Studio (SSMS). Se SQL Server Management Studio non è installato, è possibile scaricarlo [qui](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

1. In hello **connettersi tooServer** o **connettersi tooDatabase motore** della finestra di dialogo Modifica hello **nome Server** valore. Immettere l'indirizzo IP hello o il nome DNS completo della macchina virtuale hello (determinata nell'attività precedente hello). È anche possibile aggiungere una virgola e specificare la porta TCP di SQL Server. ad esempio `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.

1. In hello **autenticazione** , quindi selezionare **autenticazione di SQL Server**.

1. In hello **accesso** casella, il nome del tipo hello di un account di accesso SQL valido.

1. In hello **Password** casella, digitare la password dell'account di accesso hello hello.

1. Fare clic su **Connetti**.

    ![connessione a ssms](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)