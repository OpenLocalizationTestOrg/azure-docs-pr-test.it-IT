## <a name="scenario"></a><span data-ttu-id="d036c-101">Scenario</span><span class="sxs-lookup"><span data-stu-id="d036c-101">Scenario</span></span>
<span data-ttu-id="d036c-102">Per illustrare meglio come creare una rete virtuale e le relative subnet, in questo documento verrà utilizzato lo scenario seguente.</span><span class="sxs-lookup"><span data-stu-id="d036c-102">To better illustrate how to create a VNet and subnets, this document will use the scenario below.</span></span>

![Scenario di una rete virtuale](./media/virtual-networks-create-vnet-scenario-include/vnet-scenario.png)

<span data-ttu-id="d036c-104">In questo scenario verrà creata una rete virtuale denominata **TestVNet** con blocco CIDR riservato **192.168.0.0./16**.</span><span class="sxs-lookup"><span data-stu-id="d036c-104">In this scenario you will create a VNet named **TestVNet** with a reserved CIDR block of **192.168.0.0./16**.</span></span> <span data-ttu-id="d036c-105">Una rete virtuale conterrà le subnet seguenti:</span><span class="sxs-lookup"><span data-stu-id="d036c-105">Your VNet will contain the following subnets:</span></span> 

* <span data-ttu-id="d036c-106">**FrontEnd**, che usa **192.168.1.0/24** come blocco CIDR.</span><span class="sxs-lookup"><span data-stu-id="d036c-106">**FrontEnd**, using **192.168.1.0/24** as its CIDR block.</span></span>
* <span data-ttu-id="d036c-107">**BackEnd**, che usa **192.168.2.0/24** come blocco CIDR.</span><span class="sxs-lookup"><span data-stu-id="d036c-107">**BackEnd**, using **192.168.2.0/24** as its CIDR block.</span></span>

