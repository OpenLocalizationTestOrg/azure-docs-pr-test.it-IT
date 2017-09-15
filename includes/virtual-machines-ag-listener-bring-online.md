1. <span data-ttu-id="5bc9e-101">In Gestione cluster di failover espandere **Ruoli** e quindi evidenziare il gruppo di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="5bc9e-101">In Failover Cluster Manager, expand **Roles**, and then highlight your availability group.</span></span>  

2. <span data-ttu-id="5bc9e-102">Nella scheda **Risorse** fare clic con il pulsante destro del mouse sul nome del listener e scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="5bc9e-102">On the **Resources** tab, right-click the listener name, and then click **Properties**.</span></span>

3. <span data-ttu-id="5bc9e-103">Selezionare la scheda **Dipendenze** .</span><span class="sxs-lookup"><span data-stu-id="5bc9e-103">Click the **Dependencies** tab.</span></span> <span data-ttu-id="5bc9e-104">Se sono presenti più risorse elencate, verificare che gli indirizzi IP abbiano dipendenze OR anziché AND.</span><span class="sxs-lookup"><span data-stu-id="5bc9e-104">If multiple resources are listed, verify that the IP addresses have OR, not AND, dependencies.</span></span>  

4. <span data-ttu-id="5bc9e-105">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="5bc9e-105">Click **OK**.</span></span>

5. <span data-ttu-id="5bc9e-106">Fare clic con il pulsante destro del mouse sul nome del listener e quindi scegliere **Porta online**.</span><span class="sxs-lookup"><span data-stu-id="5bc9e-106">Right-click the listener name, and then click **Bring Online**.</span></span>

6. <span data-ttu-id="5bc9e-107">Quando il listener è online, nella scheda **Risorse** fare clic con il pulsante destro del mouse sul gruppo di disponibilità e quindi scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="5bc9e-107">After the listener is online, on the **Resources** tab, right-click the availability group, and then click **Properties**.</span></span>
   
    ![Configurare la risorsa del gruppo di disponibilità](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. <span data-ttu-id="5bc9e-109">Creare una dipendenza nella risorsa nome del listener, non il nome della risorsa indirizzo IP, e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="5bc9e-109">Create a dependency on the listener name resource (not the IP address resources name), and then click **OK**.</span></span>
   
    ![Aggiungere una dipendenza al nome del listener](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. <span data-ttu-id="5bc9e-111">Avviare SQL Server Management Studio e connettersi alla replica primaria.</span><span class="sxs-lookup"><span data-stu-id="5bc9e-111">Start SQL Server Management Studio, and then connect to the primary replica.</span></span>

9. <span data-ttu-id="5bc9e-112">Passare a **Disponibilità elevata AlwaysOn** > **Gruppi di disponibilità** > **\<AvailabilityGroupName\>** > **Listener gruppo di disponibilità**.</span><span class="sxs-lookup"><span data-stu-id="5bc9e-112">Go to **AlwaysOn High Availability** > **Availability Groups** > **\<AvailabilityGroupName\>** > **Availability Group Listeners**.</span></span>  
    <span data-ttu-id="5bc9e-113">Verrà visualizzato il nome del listener creato in Gestione cluster di failover.</span><span class="sxs-lookup"><span data-stu-id="5bc9e-113">The listener name that you created in Failover Cluster Manager should be displayed.</span></span>

10. <span data-ttu-id="5bc9e-114">Fare clic con il pulsante destro del mouse sul nome del listener e quindi su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="5bc9e-114">Right-click the listener name, and then click **Properties**.</span></span>

11. <span data-ttu-id="5bc9e-115">Nella casella **Porta** specificare il numero di porta per il listener del gruppo di disponibilità usando il valore di $EndpointPort usato in precedenza e quindi fare clic su **OK**. In questa esercitazione 1433 era l'impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="5bc9e-115">In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort that you used earlier (in this tutorial, 1433 was the default), and then click **OK**.</span></span>

