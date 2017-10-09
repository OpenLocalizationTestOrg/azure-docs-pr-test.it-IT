1. <span data-ttu-id="38b11-101">In Gestione cluster di failover espandere **Ruoli** e quindi evidenziare il gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="38b11-101">In Failover Cluster Manager, expand **Roles**, and then highlight your availability group.</span></span>  

2. <span data-ttu-id="38b11-102">In hello **risorse** scheda, fare doppio clic su nome del listener hello e quindi fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="38b11-102">On hello **Resources** tab, right-click hello listener name, and then click **Properties**.</span></span>

3. <span data-ttu-id="38b11-103">Fare clic su hello **dipendenze** scheda. Se sono elencate più risorse, verificare che gli indirizzi IP hello OR, not e le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="38b11-103">Click hello **Dependencies** tab. If multiple resources are listed, verify that hello IP addresses have OR, not AND, dependencies.</span></span>  

4. <span data-ttu-id="38b11-104">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="38b11-104">Click **OK**.</span></span>

5. <span data-ttu-id="38b11-105">Il nome del listener hello destro e quindi fare clic su **in linea**.</span><span class="sxs-lookup"><span data-stu-id="38b11-105">Right-click hello listener name, and then click **Bring Online**.</span></span>

6. <span data-ttu-id="38b11-106">Dopo aver hello listener è online, su hello **risorse** scheda, fare doppio clic su gruppo di disponibilità hello e quindi fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="38b11-106">After hello listener is online, on hello **Resources** tab, right-click hello availability group, and then click **Properties**.</span></span>
   
    ![Configurare una risorsa del gruppo di disponibilità hello](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. <span data-ttu-id="38b11-108">Creare una dipendenza sulla risorsa nome di listener hello (non hello nome indirizzo IP risorse) e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="38b11-108">Create a dependency on hello listener name resource (not hello IP address resources name), and then click **OK**.</span></span>
   
    ![Aggiungere il nome del listener hello dipendenza](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. <span data-ttu-id="38b11-110">Avviare SQL Server Management Studio e connettiti toohello replica primaria.</span><span class="sxs-lookup"><span data-stu-id="38b11-110">Start SQL Server Management Studio, and then connect toohello primary replica.</span></span>

9. <span data-ttu-id="38b11-111">Andare troppo**disponibilità elevata AlwaysOn** > **gruppi di disponibilità** > **\<AvailabilityGroupName\>**   >  **Listener del gruppo di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="38b11-111">Go too**AlwaysOn High Availability** > **Availability Groups** > **\<AvailabilityGroupName\>** > **Availability Group Listeners**.</span></span>  
    <span data-ttu-id="38b11-112">il nome del listener Hello creati in Gestione Cluster di Failover deve essere visualizzato.</span><span class="sxs-lookup"><span data-stu-id="38b11-112">hello listener name that you created in Failover Cluster Manager should be displayed.</span></span>

10. <span data-ttu-id="38b11-113">Il nome del listener hello destro e quindi fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="38b11-113">Right-click hello listener name, and then click **Properties**.</span></span>

11. <span data-ttu-id="38b11-114">In hello **porta** , specificare il numero di porta hello del listener del gruppo di disponibilità hello utilizzando hello $EndpointPort utilizzata in precedenza (in questa esercitazione, 1433 è predefinito hello), quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="38b11-114">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort that you used earlier (in this tutorial, 1433 was hello default), and then click **OK**.</span></span>

