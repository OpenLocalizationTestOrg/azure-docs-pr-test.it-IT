

<span data-ttu-id="0dc0d-101">Una macchina virtuale *personalizzata* indica semplicemente una macchina virtuale creata usata una **app in primo piano** dal **Marketplace** poiché esegue gran parte del lavoro per l'utente.</span><span class="sxs-lookup"><span data-stu-id="0dc0d-101">A *custom* virtual machine simply means a virtual machine that you create using a **Featured app** from the **Marketplace** because it does much of the work for you.</span></span> <span data-ttu-id="0dc0d-102">Tuttavia, è comunque possibile fare scelte di configurazione che includono i seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="0dc0d-102">Yet, you can still make configuration choices that include the following items:</span></span>

* <span data-ttu-id="0dc0d-103">Collegare una macchina virtuale a Rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="0dc0d-103">Connecting the virtual machine to a virtual network.</span></span>
* <span data-ttu-id="0dc0d-104">Installare l'agente di macchina virtuale di Azure e le estensioni di macchina virtuale di Azure, ad esempio per antimalware.</span><span class="sxs-lookup"><span data-stu-id="0dc0d-104">Installing the Azure Virtual Machine Agent and Azure Virtual Machine Extensions, such as for antimalware.</span></span>
* <span data-ttu-id="0dc0d-105">Aggiungere la macchina virtuale ai servizi cloud esistenti.</span><span class="sxs-lookup"><span data-stu-id="0dc0d-105">Adding the virtual machine to existing cloud services.</span></span>
* <span data-ttu-id="0dc0d-106">Aggiungere la macchina virtuale a un account di archiviazione esistente.</span><span class="sxs-lookup"><span data-stu-id="0dc0d-106">Adding the virtual machine to an existing Storage account.</span></span>
* <span data-ttu-id="0dc0d-107">Aggiungere una macchina virtuale a un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="0dc0d-107">Adding the virtual machine to an availability set.</span></span>

<!--
> [!IMPORTANT]
> If you want your virtual machine to use a virtual network so you can connect to it directly by host name or set up cross-premises connections, make sure that you specify the virtual network when you create the virtual machine. A virtual machine can be configured to join a virtual network only when you create the virtual machine. For details on virtual networks, see [Azure Virtual Network overview](../articles/virtual-network/virtual-networks-overview.md).
>
>
 -->

> [!IMPORTANT]
> <span data-ttu-id="0dc0d-108">Se si desidera che una macchina virtuale usi una rete virtuale, assicurarsi di specificare la rete quando si crea la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0dc0d-108">If you want your virtual machine to use a virtual network, make sure that you specify the virtual network when you create the virtual machine.</span></span>

> * <span data-ttu-id="0dc0d-109">Due vantaggi dell'uso di una rete virtuale consistono nel collegarsi direttamente alla macchina virtuale e nel configurare connessioni cross-premise.</span><span class="sxs-lookup"><span data-stu-id="0dc0d-109">Two benefits of using a virtual network are connecting directly to the virtual machine and to set up cross-premises connections.</span></span>

> * <span data-ttu-id="0dc0d-110">È possibile configurare una macchina virtuale in modo da aggiungerla a una rete virtuale solo quando viene creata.</span><span class="sxs-lookup"><span data-stu-id="0dc0d-110">A virtual machine can be configured to join a virtual network only when you create the virtual machine.</span></span> <span data-ttu-id="0dc0d-111">Per informazioni dettagliate sulle reti virtuali, vedere [Panoramica di Rete virtuale](../articles/virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0dc0d-111">For details on virtual networks, see [Azure Virtual Network overview](../articles/virtual-network/virtual-networks-overview.md).</span></span>
>
>

## <a name="to-create-the-virtual-machine"></a><span data-ttu-id="0dc0d-112">Per creare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="0dc0d-112">To create the virtual machine</span></span>
