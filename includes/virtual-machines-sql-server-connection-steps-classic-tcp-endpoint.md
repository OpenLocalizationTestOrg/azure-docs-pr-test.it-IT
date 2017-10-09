### <a name="create-a-tcp-endpoint-for-hello-virtual-machine"></a>Creare un endpoint TCP per la macchina virtuale hello
In ordine tooaccess, SQL Server da hello internet, una macchina virtuale hello deve avere toolisten un endpoint per la comunicazione TCP in ingresso. Questo passaggio di configurazione di Azure, indirizza in ingresso TCP porta traffico tooa porta TCP è una macchina virtuale toohello accessibile.

> [!NOTE]
> Se ci si connette all'interno di hello stesso servizio o della rete virtuale del cloud, non è toocreate un endpoint accessibile pubblicamente. In tal caso, è possibile continuare il passaggio successivo toohello. Per altre informazioni, vedere [Scenari di connessione](../articles/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-sql-connect.md#connection-scenarios).
> 
> 

1. Nel portale di Azure hello, selezionare **macchine virtuali (classico)**.
2. Quindi selezionare la macchina virtuale di SQL Server.
3. Selezionare **endpoint**, quindi fare clic su hello **Aggiungi** pulsante nella parte superiore di hello del Pannello di endpoint hello.
   
    ![Passaggi all'interno del portale per la creazione dell'endpoint](./media/virtual-machines-sql-server-connection-steps/portal-endpoint-creation.png)
4. In hello **Aggiungi Endpoint** pannello, fornire un **nome** , ad esempio SQLEndpoint.
5. Selezionare **TCP** per hello **protocollo**.
6. Nel campo **Porta pubblica** specificare un numero di porta, ad esempio **57500**.
7. Per **porta privata**, specificare la porta in ascolto di SQL Server che per impostazione predefinita troppo**1433**.
8. Fare clic su **Ok** endpoint hello toocreate.

