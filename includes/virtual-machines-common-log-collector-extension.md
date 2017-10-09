
La diagnosi dei problemi con un servizio cloud di Microsoft Azure, è necessario raccogliere i file di log del servizio hello in macchine virtuali quando si verificano problemi di hello. È possibile utilizzare raccolta occasionale di tooperfom hello estensione AzureLogCollector su richiesta di log da uno o più macchine virtuali del servizio Cloud (da ruoli web e ruoli di lavoro) e trasferimento hello raccolti file tooan account di archiviazione di Azure – senza dover accedere in remoto tooany di hello macchine virtuali.

> [!NOTE]
> Le descrizioni per la maggior parte delle informazioni di hello registrata è reperibile all'http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.
> 
> 

Sono disponibili due modalità di raccolta varia tipi hello toobe file raccolti.

* Solo log di agenti guest di Azure (GA). Questa modalità di raccolta include gli agenti guest tooAzure correlati registri hello tutti e altri componenti di Azure.
* Tutti i log (Completa). Questa modalità di raccolta raccoglierà tutti i file in modalità Agenti guest, oltre a:
  
  * log eventi di sistema e dell'applicazione
  * log degli errori HTTP
  * log di IIS
  * log di installazione
  * altri log di sistema

In entrambe le modalità di raccolta, è possono specificare le cartelle di raccolta dati aggiuntivi utilizzando una raccolta di hello seguente struttura:

* **Nome**: nome hello dell'insieme di hello, che verrà utilizzato come nome hello della sottocartella all'interno di hello zip file toobe raccolti.
* **Percorso**: hello toohello cartella percorso nella macchina virtuale hello in cui verrà raccolto il file.
* **SearchPattern**: modello hello di nomi di hello di toobe file raccolti. Il valore predefinito è "*".
* **Ricorsivo**: se il file hello verranno raccolti in modo ricorsivo nella cartella hello.

## <a name="prerequisites"></a>Prerequisiti
* È necessario toohave un account di archiviazione per i file zip di estensione toosave generato.
* È necessario assicurarsi che siano in uso i cmdlet di Azure PowerShell v0.8.0 o versioni successive. Per altre informazioni, vedere la pagina relativa ai [Download di Azure](https://azure.microsoft.com/downloads/).

## <a name="add-hello-extension"></a>Aggiungere l'estensione hello
È possibile utilizzare [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlet o [API REST di Gestione servizio](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello estensione AzureLogCollector.

Per i servizi Cloud, i cmdlet Powershell di Azure esistente, hello **Set-AzureServiceExtension**, può essere utilizzato tooenable hello estensione nelle istanze del ruolo del servizio Cloud. Ogni volta che questa estensione viene abilitata tramite questo cmdlet, viene attivata la raccolta di log nelle istanze del ruolo selezionato hello dei ruoli selezionati.

Per le macchine virtuali, i cmdlet Powershell di Azure esistente, hello **Set-AzureVMExtension**, può essere utilizzato tooenable hello estensione nelle macchine virtuali. Ogni volta che questa estensione viene abilitata tramite i cmdlet di hello, viene attivata la raccolta di log in ogni istanza.

Internamente, questa estensione Usa hello PublicConfiguration basata su JSON e PrivateConfiguration. di seguito Hello è layout hello di un file JSON di esempio per la configurazione pubblica e privata.

### <a name="publicconfiguration"></a>PublicConfiguration
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri tooyour storage account with sp=wl",
        "AdditionalData":
        [
          {
                  "Name":  "StorageData",
                  "Location":  "%roleroot%storage",
                  "SearchPattern":  "*.*",
                  "Recursive":  "true"
          },
          {
                "Name":  "CustomDataFolder2",
                "Location":  "c:\customFolder",
                "SearchPattern":  "*.log",
                "Recursive":  "false"
          },
        ]
    }

### <a name="privateconfiguration"></a>PrivateConfiguration
    {

    }

> [!NOTE]
> Per questa estensione non richiede l'uso della configurazione **privateConfiguration**. È possibile specificare solo una struttura vuota per hello **– PrivateConfiguration** argomento.
> 
> 

È possibile seguire una delle due hello seguendo i passaggi tooadd hello AzureLogCollector tooone o più istanze di un servizio Cloud o macchina virtuale di determinati ruoli, quali trigger hello raccolte su ogni toorun VM e inviare file raccolti hello tooAzure account specificato.

## <a name="adding-as-a-service-extension"></a>Aggiunta come estensione del servizio
1. Seguire la sottoscrizione tooyour hello istruzioni tooconnect Azure PowerShell.
2. Specificare nome del servizio hello, slot, ruoli e toowhich le istanze di ruolo desiderato tooadd e abilitare l'estensione AzureLogCollector hello.
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify hello slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified hello roles on which hello extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify hello instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
3. Specificare hello cartella di dati aggiuntivi per il quale verranno raccolti i file (questo passaggio è facoltativo).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > È possibile utilizzare token `%roleroot%` toospecify hello unità radice del ruolo perché non viene usata un'unità fissa.
   > 
   > 
4. Fornire nome account di archiviazione di Azure hello e i file di chiave toowhich raccolti verranno caricati.
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. Chiamare hello SetAzureServiceLogCollector.ps1 (incluso alla fine di hello dell'articolo hello) come estensione AzureLogCollector di hello tooenable indicato di seguito per un servizio Cloud. Una volta completata l'esecuzione di hello, è possibile trovare il file di hello caricato in`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

di seguito Hello è definizione hello di hello parametri script toohello. (Copiati anche sotto.)

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
      [Parameter(Mandatory=$true)]
    [string]   $ServiceName,

    [Parameter(Mandatory=$false)]
    [string[]] $Roles ,

    [Parameter(Mandatory=$false)]
    [string[]] $Instances,

    [Parameter(Mandatory=$false)]
    [string]   $Slot = 'Production',

    [Parameter(Mandatory=$false)]
    [string]   $Mode = 'Full',

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountName,

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountKey,

    [Parameter(Mandatory=$false)]
    [PSObject[]] $AdditionDataLocationList = $null
    )

* *ServiceName*: nome del servizio cloud.
* *Roles*: elenco di ruoli, ad esempio "WebRole1" o "WorkerRole1".
* *Istanze*: un elenco di nomi di istanze del ruolo di hello separati da virgola, utilizzare una stringa con caratteri jolly hello ("*") per tutte le istanze di ruolo.
* *Slot*: nome dello slot. "Production" o "Staging".
* *Mode*: modalità di raccolta. "Full" o "GA".
* *StorageAccountName*: nome dell'account di archiviazione di Azure per l'archiviazione dei dati raccolti.
* *StorageAccountKey*: nome della chiave dell'account di archiviazione di Azure.
* *AdditionalDataLocationList*: un elenco di hello seguente struttura:
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a>Aggiunta come estensione VM
Seguire la sottoscrizione tooyour hello istruzioni tooconnect Azure PowerShell.

1. Specificare il nome di servizio hello, macchina virtuale e la modalità di raccolta hello.
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify hello VM name
        $VMName = "'YourVMName'"
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify hello additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. Fornire nome account di archiviazione di Azure hello e i file di chiave toowhich raccolti verranno caricati.
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. Chiamare hello SetAzureVMLogCollector.ps1 (incluso alla fine di hello dell'articolo hello) come estensione AzureLogCollector di hello tooenable indicato di seguito per un servizio Cloud. Una volta completata l'esecuzione di hello, è possibile trovare il file di hello caricato in https://YouareStorageAccountName.blob.core.windows.net/vmlogs

di seguito Hello è definizione hello di hello parametri script toohello. (Copiati anche sotto.)

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
        [Parameter(Mandatory=$true)]
      [string]   $ServiceName,

      [Parameter(Mandatory=$false)]
      [string] $VMName ,

        [Parameter(Mandatory=$false)]
      [string]   $Mode = 'Full',

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountName,

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountKey,

      [Parameter(Mandatory=$false)]
      [PSObject[]] $AdditionDataLocationList = $null
      )

* ServiceName: nome del servizio cloud.
* Nome di hello VMName di hello macchina virtuale.
* Mode: modalità di raccolta. "Full" o "GA".
* StorageAccountName: nome dell'account di archiviazione di Azure per l'archiviazione dei dati raccolti.
* StorageAccountKey: nome della chiave dell'account di archiviazione di Azure.
* AdditionalDataLocationList: Un elenco di hello seguente struttura:

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a>File script di PowerShell per l'estensione
SetAzureServiceLogCollector.ps1

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Roles ,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Instances = '*',

                  [Parameter(Mandatory=$false)]
                  [string]   $Slot = 'Production',

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject

    if ($Instances -ne $null -and $Instances.Count -gt 0)  #Instances should be seperated by ,
    {
        $instanceText = $Instances[0]
        for ($i = 1;$i -lt $Instances.Count;$i++)
        {
              $instanceText = $instanceText+ "," + $Instances[$i]
          }
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value $instanceText
    }
    else  #For all instances if not specified.  hello value should be a space or *
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value " "
    }

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json
    "publicConfig is:  $publicConfigJSON"

    #we just provide a empty privateConfig object
    $privateconfig = "{
    }"

    if ($Roles -ne $null)
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot -Role $Roles -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }
    else
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot  -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }

    #
    #This is an optional step: generate a sasUri toohello container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "hello container for uploaded file can be accessed using this link:`r`n$sasuri"


SetAzureVMLogCollector.ps1

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string] $VMName ,

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject
    $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value "*"

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(90).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json

    Write-Output "PublicConfigurtion is: \r\n$publicConfigJSON"

    #
    #we just provide a empty privateConfig object
    #
    $privateconfig = "{
    }"

    if ($VMName -ne $null )
    {
          $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
          $VM.VM.OSVirtualHardDisk.OS

          if ($VM.VM.OSVirtualHardDisk.OS -like '*Windows*')
          {
                Set-AzureVMExtension -VM $VM -ExtensionName "AzureLogCollector" -Publisher Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.* | Update-AzureVM -Verbose

                #
                #We will check hello VM status toofind if operation by extension has been completed or not. hello completion of hello operation,either succeed or fail, can be indicated by
                #hello presence of SubstatusList field.
                #
                $Completed = $false
                while ($Completed -ne $true)
                {
                        $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
                        $status = $VM.ResourceExtensionStatusList | Where-Object {$_.HandlerName -eq "Microsoft.WindowsAzure.Compute.AzureLogCollector"}

                        if ( ($status.Code -ne 0) -and ($status.Status -like '*error*'))
                        {
                            Write-Output "Error status is returned: $($Status.ExtensionSettingStatus.FormattedMessage.Message)."
                              $Completed = $true
                        }
                        elseif (($status.ExtensionSettingStatus.SubstatusList -eq $null -or $status.ExtensionSettingStatus.SubstatusList.Count -lt 1))
                        {
                              $Completed = $false
                              Write-Output "Waiting for operation toocomplete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access toohello file, we can generate a read-only SasUri directly toohello file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "hello uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove hello extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, hello extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, hello extension cannot be enabled"
    }

## <a name="next-steps"></a>Passaggi successivi
È ora possibile esaminare o copiare i log da una posizione semplificata.

