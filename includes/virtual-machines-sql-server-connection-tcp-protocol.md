1. Durante la macchina virtuale di toohello connesso con desktop remoto, eseguire la ricerca di **Configuration Manager**:

    ![Apertura di SQL Server Management Studio](./media/virtual-machines-sql-server-connection-tcp-protocol/sql-server-configuration-manager.png)

1. In Gestione configurazione SQL Server nel riquadro della console hello espandere **configurazione di rete SQL Server**.

1. Nel riquadro della console hello, fare clic su **protocolli per MSSQLSERVER** (nome istanza predefinito hello). Nel riquadro dei dettagli di hello, fare doppio clic su **TCP** e fare clic su **abilitare** se non è già abilitato.

    ![Abilitazione del protocollo TCP](./media/virtual-machines-sql-server-connection-tcp-protocol/enable-tcp.png)

1. Nel riquadro della console hello, fare clic su **servizi di SQL Server**. Nel riquadro dei dettagli di hello, fare doppio clic su  **SQL Server (*nome dell'istanza*) * * (istanza predefinita di hello è **SQL Server (MSSQLSERVER)**), quindi fare clic su **riavviare** , istanza di hello toostop e riavvio di SQL Server.

    ![Riavvio del motore di database](./media/virtual-machines-sql-server-connection-tcp-protocol/restart-sql-server.png)

1. Chiudere Gestione configurazione SQL Server.

Per ulteriori informazioni sull'abilitazione di protocolli per hello il motore di Database di SQL Server, vedere [abilitare o disabilitare un protocollo di rete Server](http://msdn.microsoft.com/library/ms191294.aspx).
