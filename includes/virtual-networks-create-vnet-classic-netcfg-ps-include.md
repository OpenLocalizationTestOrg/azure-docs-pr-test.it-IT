## <a name="how-toocreate-a-virtual-network-using-a-network-config-file-from-powershell"></a>Come toocreate file di una rete virtuale usando una configurazione di rete di PowerShell
Azure Usa un toodefine file xml di sottoscrizione di tooa disponibili tutte le reti virtuali. È possibile scaricare questo file, modificarlo toomodify o eliminare le reti virtuali esistenti e creare nuove reti virtuali. In questa esercitazione, è illustrato come toodownload questo file, denominato tooas file di configurazione (o netcfg) di rete e modificarlo toocreate una nuova rete virtuale. toolearn ulteriori informazioni sui file di configurazione di rete hello, vedere hello [dello schema di configurazione di rete virtuale di Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).

toocreate una rete virtuale con un file netcfg tramite PowerShell, hello completo alla procedura seguente:

1. Se non si è mai usato Azure PowerShell, hello completato i passaggi in hello [come tooInstall e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) articolo, quindi accedi tooAzure e selezionare la sottoscrizione.
2. Dalla console di Azure PowerShell hello, utilizzare hello **Get AzureVnetConfig** cmdlet toodownload hello configurazione file tooa directory di rete nel computer eseguendo hello comando seguente: 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   Output previsto:
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. Aprire il file hello è stato salvato nel passaggio 2 utilizzando qualsiasi applicazione di editor di testo o XML e cercare hello  **<VirtualNetworkSites>**  elemento. Se sono già state create altre reti, ognuna di esse verrà visualizzata con il relativo elemento **<VirtualNetworkSite>** .
4. rete virtuale hello toocreate descritta in questo scenario, aggiungere hello seguente immediatamente sotto hello  **<VirtualNetworkSites>**  elemento:

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
   
5. Salvare i file di configurazione di rete hello.
6. Dalla console di Azure PowerShell hello, utilizzare hello **Set AzureVnetConfig** cmdlet file di configurazione di rete hello a tooupload eseguendo hello comando seguente: 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   Output restituito:
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   Se **Statooperazione** non *Succeeded* in hello restituito l'output, controllare di nuovo il file xml hello per errori e il passaggio di completamento 6.

7. Dalla console di Azure PowerShell hello, utilizzare hello **Get AzureVnetSite** tooverify cmdlet che hello nuova rete è stata aggiunta eseguendo hello comando seguente: 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   Hello restituito output (abbreviato) include hello seguente testo:
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
