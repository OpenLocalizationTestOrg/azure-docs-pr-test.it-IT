1. <span data-ttu-id="bff2d-101">Copiare la cartella locale di tooa installer hello (ad esempio C:\Temp) nel server di hello che si desidera tooprotect.</span><span class="sxs-lookup"><span data-stu-id="bff2d-101">Copy hello installer tooa local folder (for example, C:\Temp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="bff2d-102">Eseguire hello seguenti comandi come amministratore a un prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="bff2d-102">Run hello following commands as an administrator at a command prompt:</span></span>

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. <span data-ttu-id="bff2d-103">tooinstall servizio di mobilità, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="bff2d-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. <span data-ttu-id="bff2d-104">Agente hello deve ora toobe registrato con hello del Server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="bff2d-104">Now hello agent needs toobe registered with hello Configuration Server.</span></span>

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a><span data-ttu-id="bff2d-105">Argomenti della riga di comando del programma di installazione del servizio Mobility</span><span class="sxs-lookup"><span data-stu-id="bff2d-105">Mobility Service installer command-line arguments</span></span>

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| <span data-ttu-id="bff2d-106">Parametro</span><span class="sxs-lookup"><span data-stu-id="bff2d-106">Parameter</span></span>|<span data-ttu-id="bff2d-107">Tipo</span><span class="sxs-lookup"><span data-stu-id="bff2d-107">Type</span></span>|<span data-ttu-id="bff2d-108">Descrizione</span><span class="sxs-lookup"><span data-stu-id="bff2d-108">Description</span></span>|<span data-ttu-id="bff2d-109">Valori possibili</span><span class="sxs-lookup"><span data-stu-id="bff2d-109">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="bff2d-110">/Role</span><span class="sxs-lookup"><span data-stu-id="bff2d-110">/Role</span></span>|<span data-ttu-id="bff2d-111">Mandatory</span><span class="sxs-lookup"><span data-stu-id="bff2d-111">Mandatory</span></span>|<span data-ttu-id="bff2d-112">Specifica se installare il servizio Mobility (MS) o MasterTarget (MT)</span><span class="sxs-lookup"><span data-stu-id="bff2d-112">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="bff2d-113">MS</span><span class="sxs-lookup"><span data-stu-id="bff2d-113">MS</span></span> </br> <span data-ttu-id="bff2d-114">MT</span><span class="sxs-lookup"><span data-stu-id="bff2d-114">MT</span></span>|
|<span data-ttu-id="bff2d-115">/InstallLocation</span><span class="sxs-lookup"><span data-stu-id="bff2d-115">/InstallLocation</span></span>|<span data-ttu-id="bff2d-116">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="bff2d-116">Optional</span></span>|<span data-ttu-id="bff2d-117">Percorso in cui viene installato il servizio Mobility</span><span class="sxs-lookup"><span data-stu-id="bff2d-117">Location where Mobility Service is installed</span></span>|<span data-ttu-id="bff2d-118">Qualsiasi cartella nel computer di hello</span><span class="sxs-lookup"><span data-stu-id="bff2d-118">Any folder on hello computer</span></span>|
|<span data-ttu-id="bff2d-119">/Platform</span><span class="sxs-lookup"><span data-stu-id="bff2d-119">/Platform</span></span>|<span data-ttu-id="bff2d-120">Mandatory</span><span class="sxs-lookup"><span data-stu-id="bff2d-120">Mandatory</span></span>|<span data-ttu-id="bff2d-121">Specifica la piattaforma di hello in cui hello è recupero installato servizio di mobilità</span><span class="sxs-lookup"><span data-stu-id="bff2d-121">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="bff2d-122">- **VMware**: usare questo valore se si installa il servizio Mobility in una macchina virtuale in esecuzione in *host VMware vSphere ESXi*, *host Hyper-V* o *server fisici*</span><span class="sxs-lookup"><span data-stu-id="bff2d-122">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="bff2d-123">- **Azure**: usare questo valore se si installa un agente in una macchina virtuale IaaS di Azure</span><span class="sxs-lookup"><span data-stu-id="bff2d-123">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="bff2d-124">VMware</span><span class="sxs-lookup"><span data-stu-id="bff2d-124">VMware</span></span> </br> <span data-ttu-id="bff2d-125">Azure</span><span class="sxs-lookup"><span data-stu-id="bff2d-125">Azure</span></span>|
|<span data-ttu-id="bff2d-126">/Silent</span><span class="sxs-lookup"><span data-stu-id="bff2d-126">/Silent</span></span>|<span data-ttu-id="bff2d-127">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="bff2d-127">Optional</span></span>|<span data-ttu-id="bff2d-128">Specifica il programma di installazione di toorun hello in modalità invisibile all'utente</span><span class="sxs-lookup"><span data-stu-id="bff2d-128">Specifies toorun hello installer in silent mode</span></span>| <span data-ttu-id="bff2d-129">ND</span><span class="sxs-lookup"><span data-stu-id="bff2d-129">NA</span></span>|

>[!TIP]
> <span data-ttu-id="bff2d-130">i log di installazione di Hello sono reperibile nella %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span><span class="sxs-lookup"><span data-stu-id="bff2d-130">hello setup logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span></span>

#### <a name="mobility-service-registration-command-line-arguments"></a><span data-ttu-id="bff2d-131">Argomenti della riga di comando per la registrazione del servizio Mobility</span><span class="sxs-lookup"><span data-stu-id="bff2d-131">Mobility Service registration command-line arguments</span></span>

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | <span data-ttu-id="bff2d-132">Parametro</span><span class="sxs-lookup"><span data-stu-id="bff2d-132">Parameter</span></span>|<span data-ttu-id="bff2d-133">Tipo</span><span class="sxs-lookup"><span data-stu-id="bff2d-133">Type</span></span>|<span data-ttu-id="bff2d-134">Descrizione</span><span class="sxs-lookup"><span data-stu-id="bff2d-134">Description</span></span>|<span data-ttu-id="bff2d-135">Valori possibili</span><span class="sxs-lookup"><span data-stu-id="bff2d-135">Possible values</span></span>|
  |-|-|-|-|
  |<span data-ttu-id="bff2d-136">/CSEndPoint</span><span class="sxs-lookup"><span data-stu-id="bff2d-136">/CSEndPoint</span></span> |<span data-ttu-id="bff2d-137">Mandatory</span><span class="sxs-lookup"><span data-stu-id="bff2d-137">Mandatory</span></span>|<span data-ttu-id="bff2d-138">Indirizzo IP hello del server di configurazione</span><span class="sxs-lookup"><span data-stu-id="bff2d-138">IP address of hello configuration server</span></span>| <span data-ttu-id="bff2d-139">Qualsiasi indirizzo IP valido</span><span class="sxs-lookup"><span data-stu-id="bff2d-139">Any valid IP address</span></span>|
  |<span data-ttu-id="bff2d-140">/PassphraseFilePath</span><span class="sxs-lookup"><span data-stu-id="bff2d-140">/PassphraseFilePath</span></span>|<span data-ttu-id="bff2d-141">Mandatory</span><span class="sxs-lookup"><span data-stu-id="bff2d-141">Mandatory</span></span>|<span data-ttu-id="bff2d-142">Percorso di hello passphrase</span><span class="sxs-lookup"><span data-stu-id="bff2d-142">Location of hello passphrase</span></span> |<span data-ttu-id="bff2d-143">Qualsiasi percorso file locale o UNC valido</span><span class="sxs-lookup"><span data-stu-id="bff2d-143">Any valid UNC or local file path</span></span>|


>[!TIP]
> <span data-ttu-id="bff2d-144">Hello AgentConfiguration log è reperibile nella %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span><span class="sxs-lookup"><span data-stu-id="bff2d-144">hello AgentConfiguration logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span></span>
