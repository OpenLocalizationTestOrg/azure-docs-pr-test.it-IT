## <a name="create-a-resource-group"></a><span data-ttu-id="81bd9-101">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="81bd9-101">Create a resource group</span></span>

<span data-ttu-id="81bd9-102">Creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="81bd9-102">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="81bd9-103">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="81bd9-103">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="81bd9-104">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella località *stati uniti orientali*.</span><span class="sxs-lookup"><span data-stu-id="81bd9-104">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="81bd9-105">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="81bd9-105">Create a virtual machine</span></span>

<span data-ttu-id="81bd9-106">Creare una VM con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="81bd9-106">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="81bd9-107">L'esempio seguente crea una macchina virtuale denominata *myVM* e le chiavi SSH, se non esistono già in un percorso predefinito.</span><span class="sxs-lookup"><span data-stu-id="81bd9-107">The following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="81bd9-108">Per usare un set specifico di chiavi, utilizzare l'opzione `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="81bd9-108">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="81bd9-109">Dopo che la VM è stata creata, l'interfaccia della riga di comando di Azure mostra informazioni simili all'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="81bd9-109">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="81bd9-110">Prendere nota di `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="81bd9-110">Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="81bd9-111">Questo indirizzo viene usato per accedere alla VM.</span><span class="sxs-lookup"><span data-stu-id="81bd9-111">This address is used to access the VM.</span></span>

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



## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="81bd9-112">Aprire la porta 80 per il traffico Web</span><span class="sxs-lookup"><span data-stu-id="81bd9-112">Open port 80 for web traffic</span></span> 

<span data-ttu-id="81bd9-113">Per impostazione predefinita, nelle VM Linux distribuite in Azure sono consentite solo le connessioni SSH.</span><span class="sxs-lookup"><span data-stu-id="81bd9-113">By default, only SSH connections are allowed into Linux VMs deployed in Azure.</span></span> <span data-ttu-id="81bd9-114">Poiché questa macchina virtuale verrà usata come server Web, è necessario aprire la porta 80 da Internet.</span><span class="sxs-lookup"><span data-stu-id="81bd9-114">Because this VM is going to be a web server, you need to open port 80 from the internet.</span></span> <span data-ttu-id="81bd9-115">Usare il comando [az vm open-port](/cli/azure/vm#open-port) per aprire la porta.</span><span class="sxs-lookup"><span data-stu-id="81bd9-115">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span></span>  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a><span data-ttu-id="81bd9-116">Usare SSH per connettersi alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="81bd9-116">SSH into your VM</span></span>


<span data-ttu-id="81bd9-117">Se non si conosce già l'indirizzo IP pubblico della VM, eseguire il comando [az network public-ip list](/cli/azure/network/public-ip#list):</span><span class="sxs-lookup"><span data-stu-id="81bd9-117">If you don't already know the public IP address of your VM, run the [az network public-ip list](/cli/azure/network/public-ip#list) command:</span></span>


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

<span data-ttu-id="81bd9-118">Usare il comando seguente per creare una sessione SSH con la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="81bd9-118">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="81bd9-119">Sostituire l'indirizzo IP pubblico corretto della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="81bd9-119">Substitute the correct public IP address of your virtual machine.</span></span> <span data-ttu-id="81bd9-120">In questo esempio l'indirizzo IP è *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="81bd9-120">In this example, the IP address is *40.68.254.142*.</span></span>

```bash
ssh azureuser@40.68.254.142
```

