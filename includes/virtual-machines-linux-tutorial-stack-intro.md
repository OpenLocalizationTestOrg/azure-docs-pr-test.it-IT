## <a name="create-a-resource-group"></a><span data-ttu-id="c474c-101">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="c474c-101">Create a resource group</span></span>

<span data-ttu-id="c474c-102">Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="c474c-102">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="c474c-103">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="c474c-103">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="c474c-104">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso.</span><span class="sxs-lookup"><span data-stu-id="c474c-104">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="c474c-105">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c474c-105">Create a virtual machine</span></span>

<span data-ttu-id="c474c-106">Creare una macchina virtuale con hello [creare vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="c474c-106">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="c474c-107">esempio Hello crea una macchina virtuale denominata *myVM* e crea le chiavi SSH se sono già presenti in un percorso chiave predefinito.</span><span class="sxs-lookup"><span data-stu-id="c474c-107">hello following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="c474c-108">toouse uno specifico set di chiavi, utilizzare hello `--ssh-key-value` opzione.</span><span class="sxs-lookup"><span data-stu-id="c474c-108">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="c474c-109">Quando è stato creato hello VM, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="c474c-109">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="c474c-110">Prendere nota di hello `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="c474c-110">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="c474c-111">Questo indirizzo è utilizzato tooaccess hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c474c-111">This address is used tooaccess hello VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```



## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="c474c-112">Aprire la porta 80 per il traffico Web</span><span class="sxs-lookup"><span data-stu-id="c474c-112">Open port 80 for web traffic</span></span> 

<span data-ttu-id="c474c-113">Per impostazione predefinita, nelle VM Linux distribuite in Azure sono consentite solo le connessioni SSH.</span><span class="sxs-lookup"><span data-stu-id="c474c-113">By default, only SSH connections are allowed into Linux VMs deployed in Azure.</span></span> <span data-ttu-id="c474c-114">Poiché questa macchina virtuale è in corso toobe un server web, è necessario tooopen la porta 80 da hello internet.</span><span class="sxs-lookup"><span data-stu-id="c474c-114">Because this VM is going toobe a web server, you need tooopen port 80 from hello internet.</span></span> <span data-ttu-id="c474c-115">Hello utilizzare [az vm aprire porte](/cli/azure/vm#open-port) comando tooopen hello desiderato porta.</span><span class="sxs-lookup"><span data-stu-id="c474c-115">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a><span data-ttu-id="c474c-116">Usare SSH per connettersi alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c474c-116">SSH into your VM</span></span>


<span data-ttu-id="c474c-117">Se non si conosce hello indirizzo IP pubblico della macchina virtuale, esegue hello [elenco public-ip di rete az](/cli/azure/network/public-ip#list) comando:</span><span class="sxs-lookup"><span data-stu-id="c474c-117">If you don't already know hello public IP address of your VM, run hello [az network public-ip list](/cli/azure/network/public-ip#list) command:</span></span>


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

<span data-ttu-id="c474c-118">Comando che segue di hello utilizzare toocreate una sessione SSH con la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="c474c-118">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="c474c-119">Sostituire hello corretto indirizzo IP pubblico della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c474c-119">Substitute hello correct public IP address of your virtual machine.</span></span> <span data-ttu-id="c474c-120">In questo esempio, è l'indirizzo IP hello *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="c474c-120">In this example, hello IP address is *40.68.254.142*.</span></span>

```bash
ssh azureuser@40.68.254.142
```

