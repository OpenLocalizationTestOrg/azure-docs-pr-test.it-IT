
1. <span data-ttu-id="9aa54-101">Accedi tooyour sottoscrizione di Azure seguendo i passaggi di hello elencati [connettersi tooAzure da hello Azure CLI 1.0](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="9aa54-101">Sign in tooyour Azure subscription using hello steps listed in [Connect tooAzure from hello Azure CLI 1.0](../articles/xplat-cli-connect.md).</span></span>

2. <span data-ttu-id="9aa54-102">Verificare di disporre in modalità di distribuzione classica hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9aa54-102">Make sure you are in hello Classic deployment mode as follows:</span></span>

    ```azurecli
    azure config mode asm
    ```

3. <span data-ttu-id="9aa54-103">Scoprire immagine Linux hello che si desidera tooload dalle immagini disponibili hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9aa54-103">Find out hello Linux image that you want tooload from hello available images as follows:</span></span>

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    <span data-ttu-id="9aa54-104">In una finestra del prompt dei comandi di Windows usare **find** anziché grep.</span><span class="sxs-lookup"><span data-stu-id="9aa54-104">In a Windows command-prompt window, use **find** instead of grep.</span></span>
   
4. <span data-ttu-id="9aa54-105">Utilizzare `azure vm create` toocreate una macchina virtuale con immagine di Linux hello dall'elenco precedente hello.</span><span class="sxs-lookup"><span data-stu-id="9aa54-105">Use `azure vm create` toocreate a VM with hello Linux image from hello previous list.</span></span> <span data-ttu-id="9aa54-106">Questo passaggio crea un servizio cloud e un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9aa54-106">This step creates a cloud service and storage account.</span></span> <span data-ttu-id="9aa54-107">È possibile connettersi questo servizio cloud di esistente tooan macchina virtuale con un `-c` opzione.</span><span class="sxs-lookup"><span data-stu-id="9aa54-107">You could also connect this VM tooan existing cloud service with a `-c` option.</span></span> <span data-ttu-id="9aa54-108">Creare un toolog endpoint SSH nella macchina virtuale di Linux toohello con hello `-e` opzione.</span><span class="sxs-lookup"><span data-stu-id="9aa54-108">Create an SSH endpoint toolog in toohello Linux virtual machine with hello `-e` option.</span></span> <span data-ttu-id="9aa54-109">esempio Hello crea una macchina virtuale denominata `myVM` utilizzando hello `Ubuntu-14_04_4-LTS` immagine hello `West US` posizione e aggiunge un nome utente `ops`:</span><span class="sxs-lookup"><span data-stu-id="9aa54-109">hello following example creates a VM named `myVM` using hello `Ubuntu-14_04_4-LTS` image in hello `West US` location, and adds a user name `ops`:</span></span>
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    <span data-ttu-id="9aa54-110">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="9aa54-110">hello output is similar toohello following example:</span></span>

    ```azurecli
    info:    Executing command vm create
    + Looking up image b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB
    + Looking up cloud service
    info:    cloud service myVM not found.
    + Creating cloud service
    + Retrieving storage accounts
    + Creating VM
    info:    vm create command OK
    ```
   
   > [!NOTE]
   > <span data-ttu-id="9aa54-111">Per una macchina virtuale Linux, è necessario fornire hello `-e` opzione `vm create`.</span><span class="sxs-lookup"><span data-stu-id="9aa54-111">For a Linux virtual machine, you must provide hello `-e` option in `vm create`.</span></span> <span data-ttu-id="9aa54-112">Non è possibile tooenable SSH dopo che è stata creata la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="9aa54-112">It is not possible tooenable SSH after hello virtual machine has been created.</span></span> <span data-ttu-id="9aa54-113">Per ulteriori dettagli su SSH, leggere [come tooUse SSH con Linux in Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9aa54-113">For more details on SSH, read [How tooUse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

5. <span data-ttu-id="9aa54-114">È possibile verificare gli attributi di hello di hello VM utilizzando hello `azure vm show` comando.</span><span class="sxs-lookup"><span data-stu-id="9aa54-114">You can verify hello attributes of hello VM by using hello `azure vm show` command.</span></span> <span data-ttu-id="9aa54-115">Hello seguente esempio vengono restituite informazioni per la macchina virtuale denominata hello `myVM`:</span><span class="sxs-lookup"><span data-stu-id="9aa54-115">hello following example lists information for hello VM named `myVM`:</span></span>

    ```azurecli   
    azure vm show myVM
    ```

6. <span data-ttu-id="9aa54-116">Avviare la macchina virtuale con hello `azure vm start` comando come segue:</span><span class="sxs-lookup"><span data-stu-id="9aa54-116">Start your VM with hello `azure vm start` command as follows:</span></span>

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="9aa54-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9aa54-117">Next steps</span></span>
<span data-ttu-id="9aa54-118">Per informazioni dettagliate su tutti questi comandi di macchina virtuale di Azure CLI 1.0, leggere hello [Using hello Azure CLI 1.0 con l'API della distribuzione classica hello](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="9aa54-118">For details on all these Azure CLI 1.0 virtual machine commands, read hello [Using hello Azure CLI 1.0 with hello Classic deployment API](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

