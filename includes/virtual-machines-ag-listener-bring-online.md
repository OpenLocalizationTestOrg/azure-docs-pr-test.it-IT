1. In Gestione cluster di failover espandere **Ruoli** e quindi evidenziare il gruppo di disponibilità.  

2. In hello **risorse** scheda, fare doppio clic su nome del listener hello e quindi fare clic su **proprietà**.

3. Fare clic su hello **dipendenze** scheda. Se sono elencate più risorse, verificare che gli indirizzi IP hello OR, not e le dipendenze.  

4. Fare clic su **OK**.

5. Il nome del listener hello destro e quindi fare clic su **in linea**.

6. Dopo aver hello listener è online, su hello **risorse** scheda, fare doppio clic su gruppo di disponibilità hello e quindi fare clic su **proprietà**.
   
    ![Configurare una risorsa del gruppo di disponibilità hello](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. Creare una dipendenza sulla risorsa nome di listener hello (non hello nome indirizzo IP risorse) e quindi fare clic su **OK**.
   
    ![Aggiungere il nome del listener hello dipendenza](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. Avviare SQL Server Management Studio e connettiti toohello replica primaria.

9. Andare troppo**disponibilità elevata AlwaysOn** > **gruppi di disponibilità** > **\<AvailabilityGroupName\>**   >  **Listener del gruppo di disponibilità**.  
    il nome del listener Hello creati in Gestione Cluster di Failover deve essere visualizzato.

10. Il nome del listener hello destro e quindi fare clic su **proprietà**.

11. In hello **porta** , specificare il numero di porta hello del listener del gruppo di disponibilità hello utilizzando hello $EndpointPort utilizzata in precedenza (in questa esercitazione, 1433 è predefinito hello), quindi fare clic su **OK**.

