## <a name="scenario"></a><span data-ttu-id="22a0c-101">Scenario</span><span class="sxs-lookup"><span data-stu-id="22a0c-101">Scenario</span></span>
<span data-ttu-id="22a0c-102">toobetter illustrare come toocreate una rete virtuale e le subnet, in questo documento verrà utilizzato uno scenario di hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="22a0c-102">toobetter illustrate how toocreate a VNet and subnets, this document will use hello scenario below.</span></span>

![Scenario di una rete virtuale](./media/virtual-networks-create-vnet-scenario-include/vnet-scenario.png)

<span data-ttu-id="22a0c-104">In questo scenario verrà creata una rete virtuale denominata **TestVNet** con blocco CIDR riservato **192.168.0.0./16**.</span><span class="sxs-lookup"><span data-stu-id="22a0c-104">In this scenario you will create a VNet named **TestVNet** with a reserved CIDR block of **192.168.0.0./16**.</span></span> <span data-ttu-id="22a0c-105">La rete virtuale conterrà hello seguenti subnet:</span><span class="sxs-lookup"><span data-stu-id="22a0c-105">Your VNet will contain hello following subnets:</span></span> 

* <span data-ttu-id="22a0c-106">**FrontEnd**, che usa **192.168.1.0/24** come blocco CIDR.</span><span class="sxs-lookup"><span data-stu-id="22a0c-106">**FrontEnd**, using **192.168.1.0/24** as its CIDR block.</span></span>
* <span data-ttu-id="22a0c-107">**BackEnd**, che usa **192.168.2.0/24** come blocco CIDR.</span><span class="sxs-lookup"><span data-stu-id="22a0c-107">**BackEnd**, using **192.168.2.0/24** as its CIDR block.</span></span>

