## <a name="how-toocreate-a-virtual-network-using-a-network-config-file-from-powershell"></a><span data-ttu-id="cc3a7-101">Come toocreate file di una rete virtuale usando una configurazione di rete di PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc3a7-101">How toocreate a virtual network using a network config file from PowerShell</span></span>
<span data-ttu-id="cc3a7-102">Azure Usa un toodefine file xml di sottoscrizione di tooa disponibili tutte le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="cc3a7-102">Azure uses an xml file toodefine all virtual networks available tooa subscription.</span></span> <span data-ttu-id="cc3a7-103">È possibile scaricare questo file, modificarlo toomodify o eliminare le reti virtuali esistenti e creare nuove reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="cc3a7-103">You can download this file, edit it toomodify or delete existing virtual networks, and create new virtual networks.</span></span> <span data-ttu-id="cc3a7-104">In questa esercitazione, è illustrato come toodownload questo file, denominato tooas file di configurazione (o netcfg) di rete e modificarlo toocreate una nuova rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="cc3a7-104">In this tutorial, you learn how toodownload this file, referred tooas network configuration (or netcfg) file, and edit it toocreate a new virtual network.</span></span> <span data-ttu-id="cc3a7-105">toolearn ulteriori informazioni sui file di configurazione di rete hello, vedere hello [dello schema di configurazione di rete virtuale di Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc3a7-105">toolearn more about hello network configuration file, see hello [Azure virtual network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

<span data-ttu-id="cc3a7-106">toocreate una rete virtuale con un file netcfg tramite PowerShell, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="cc3a7-106">toocreate a virtual network with a netcfg file using PowerShell, complete hello following steps:</span></span>

1. <span data-ttu-id="cc3a7-107">Se non si è mai usato Azure PowerShell, hello completato i passaggi in hello [come tooInstall e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) articolo, quindi accedi tooAzure e selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="cc3a7-107">If you have never used Azure PowerShell, complete hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article, then sign in tooAzure and select your subscription.</span></span>
2. <span data-ttu-id="cc3a7-108">Dalla console di Azure PowerShell hello, utilizzare hello **Get AzureVnetConfig** cmdlet toodownload hello configurazione file tooa directory di rete nel computer eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cc3a7-108">From hello Azure PowerShell console, use hello **Get-AzureVnetConfig** cmdlet toodownload hello network configuration file tooa directory on your computer by running hello following command:</span></span> 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="cc3a7-109">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="cc3a7-109">Expected output:</span></span>
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. <span data-ttu-id="cc3a7-110">Aprire il file hello è stato salvato nel passaggio 2 utilizzando qualsiasi applicazione di editor di testo o XML e cercare hello  **<VirtualNetworkSites>**  elemento.</span><span class="sxs-lookup"><span data-stu-id="cc3a7-110">Open hello file you saved in step 2 using any XML or text editor application, and look for hello **<VirtualNetworkSites>** element.</span></span> <span data-ttu-id="cc3a7-111">Se sono già state create altre reti, ognuna di esse verrà visualizzata con il relativo elemento **<VirtualNetworkSite>** .</span><span class="sxs-lookup"><span data-stu-id="cc3a7-111">If you have any networks already created, each network is displayed as its own **<VirtualNetworkSite>** element.</span></span>
4. <span data-ttu-id="cc3a7-112">rete virtuale hello toocreate descritta in questo scenario, aggiungere hello seguente immediatamente sotto hello  **<VirtualNetworkSites>**  elemento:</span><span class="sxs-lookup"><span data-stu-id="cc3a7-112">toocreate hello virtual network described in this scenario, add hello following XML just under hello **<VirtualNetworkSites>** element:</span></span>

   ```xml
        <VirtualNetworkSite name="TestVNet" Location="East US">
          <AddressSpace>
            <AddressPrefix>192.168.0.0/16</AddressPrefix>
          </AddressSpace>
          <Subnets>
            <Subnet name="FrontEnd">
              <AddressPrefix>192.168.1.0/24</AddressPrefix>
            </Subnet>
            <Subnet name="BackEnd">
              <AddressPrefix>192.168.2.0/24</AddressPrefix>
            </Subnet>
          </Subnets>
        </VirtualNetworkSite>
   ```
   
5. <span data-ttu-id="cc3a7-113">Salvare i file di configurazione di rete hello.</span><span class="sxs-lookup"><span data-stu-id="cc3a7-113">Save hello network configuration file.</span></span>
6. <span data-ttu-id="cc3a7-114">Dalla console di Azure PowerShell hello, utilizzare hello **Set AzureVnetConfig** cmdlet file di configurazione di rete hello a tooupload eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cc3a7-114">From hello Azure PowerShell console, use hello **Set-AzureVnetConfig** cmdlet tooupload hello network configuration file by running hello following command:</span></span> 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="cc3a7-115">Output restituito:</span><span class="sxs-lookup"><span data-stu-id="cc3a7-115">Returned output:</span></span>
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   <span data-ttu-id="cc3a7-116">Se **Statooperazione** non *Succeeded* in hello restituito l'output, controllare di nuovo il file xml hello per errori e il passaggio di completamento 6.</span><span class="sxs-lookup"><span data-stu-id="cc3a7-116">If **OperationStatus** is not *Succeeded* in hello returned output, check hello xml file for errors and complete step 6 again.</span></span>

7. <span data-ttu-id="cc3a7-117">Dalla console di Azure PowerShell hello, utilizzare hello **Get AzureVnetSite** tooverify cmdlet che hello nuova rete è stata aggiunta eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="cc3a7-117">From hello Azure PowerShell console, use hello **Get-AzureVnetSite** cmdlet tooverify that hello new network was added by running hello following command:</span></span> 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   <span data-ttu-id="cc3a7-118">Hello restituito output (abbreviato) include hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="cc3a7-118">hello returned (abbreviated) output includes hello following text:</span></span>
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
