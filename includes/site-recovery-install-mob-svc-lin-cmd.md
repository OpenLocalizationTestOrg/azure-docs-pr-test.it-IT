1. <span data-ttu-id="74853-101">Copiare hello installer tooa cartella locale (ad esempio, /tmp) hello server che si desidera tooprotect.</span><span class="sxs-lookup"><span data-stu-id="74853-101">Copy hello installer tooa local folder (for example, /tmp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="74853-102">In un terminale del, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="74853-102">In a terminal, run hello following commands:</span></span>
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. <span data-ttu-id="74853-103">tooinstall servizio di mobilità, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="74853-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. <span data-ttu-id="74853-104">Al termine dell'installazione, è necessario server di configurazione registrati toohello tooget hello servizio di mobilità.</span><span class="sxs-lookup"><span data-stu-id="74853-104">Once installation is complete, hello Mobility Service needs tooget registered toohello configuration server.</span></span> <span data-ttu-id="74853-105">Comando che segue di esecuzione hello tooregister hello, servizio di mobilità con server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="74853-105">Run hello following command tooregister hello Mobility Service with Configuration server.</span></span>

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a><span data-ttu-id="74853-106">Riga di comando del programma di installazione del servizio Mobility</span><span class="sxs-lookup"><span data-stu-id="74853-106">Mobility Service installer command-line</span></span>

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|<span data-ttu-id="74853-107">Parametro</span><span class="sxs-lookup"><span data-stu-id="74853-107">Parameter</span></span>|<span data-ttu-id="74853-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="74853-108">Type</span></span>|<span data-ttu-id="74853-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="74853-109">Description</span></span>|<span data-ttu-id="74853-110">Valori possibili</span><span class="sxs-lookup"><span data-stu-id="74853-110">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="74853-111">-r</span><span class="sxs-lookup"><span data-stu-id="74853-111">-r</span></span> |<span data-ttu-id="74853-112">Mandatory</span><span class="sxs-lookup"><span data-stu-id="74853-112">Mandatory</span></span>|<span data-ttu-id="74853-113">Specifica se installare il servizio Mobility (MS) o MasterTarget (MT)</span><span class="sxs-lookup"><span data-stu-id="74853-113">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="74853-114">MS</span><span class="sxs-lookup"><span data-stu-id="74853-114">MS</span></span> </br> <span data-ttu-id="74853-115">MT</span><span class="sxs-lookup"><span data-stu-id="74853-115">MT</span></span>|
|<span data-ttu-id="74853-116">-d</span><span class="sxs-lookup"><span data-stu-id="74853-116">-d</span></span> |<span data-ttu-id="74853-117">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="74853-117">Optional</span></span>|<span data-ttu-id="74853-118">Percorso in cui verrà installato il servizio Mobility</span><span class="sxs-lookup"><span data-stu-id="74853-118">Location where Mobility Service will be installed</span></span>|<span data-ttu-id="74853-119">/usr/local/ASR</span><span class="sxs-lookup"><span data-stu-id="74853-119">/usr/local/ASR</span></span>|
|<span data-ttu-id="74853-120">-v</span><span class="sxs-lookup"><span data-stu-id="74853-120">-v</span></span>|<span data-ttu-id="74853-121">Mandatory</span><span class="sxs-lookup"><span data-stu-id="74853-121">Mandatory</span></span>|<span data-ttu-id="74853-122">Specifica la piattaforma di hello in cui hello è recupero installato servizio di mobilità</span><span class="sxs-lookup"><span data-stu-id="74853-122">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="74853-123">- **VMware**: usare questo valore se si installa il servizio Mobility in una macchina virtuale in esecuzione in *host VMware vSphere ESXi*, *host Hyper-V* o *server fisici*</span><span class="sxs-lookup"><span data-stu-id="74853-123">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="74853-124">- **Azure**: usare questo valore se si installa un agente in una macchina virtuale IaaS di Azure</span><span class="sxs-lookup"><span data-stu-id="74853-124">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="74853-125">VMware</span><span class="sxs-lookup"><span data-stu-id="74853-125">VMware</span></span> </br> <span data-ttu-id="74853-126">Azure</span><span class="sxs-lookup"><span data-stu-id="74853-126">Azure</span></span>|
|<span data-ttu-id="74853-127">-q</span><span class="sxs-lookup"><span data-stu-id="74853-127">-q</span></span>|<span data-ttu-id="74853-128">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="74853-128">Optional</span></span>|<span data-ttu-id="74853-129">Specifica toorun programma di installazione in modalità invisibile all'utente</span><span class="sxs-lookup"><span data-stu-id="74853-129">Specifies toorun installer in silent mode</span></span>| <span data-ttu-id="74853-130">N/D</span><span class="sxs-lookup"><span data-stu-id="74853-130">N/A</span></span>|


#### <a name="mobility-service-configuration-command-line"></a><span data-ttu-id="74853-131">Riga di comando di configurazione del servizio Mobility</span><span class="sxs-lookup"><span data-stu-id="74853-131">Mobility Service configuration command-line</span></span>

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|<span data-ttu-id="74853-132">Parametro</span><span class="sxs-lookup"><span data-stu-id="74853-132">Parameter</span></span>|<span data-ttu-id="74853-133">Tipo</span><span class="sxs-lookup"><span data-stu-id="74853-133">Type</span></span>|<span data-ttu-id="74853-134">Descrizione</span><span class="sxs-lookup"><span data-stu-id="74853-134">Description</span></span>|<span data-ttu-id="74853-135">Valori possibili</span><span class="sxs-lookup"><span data-stu-id="74853-135">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="74853-136">-i</span><span class="sxs-lookup"><span data-stu-id="74853-136">-i</span></span> |<span data-ttu-id="74853-137">Mandatory</span><span class="sxs-lookup"><span data-stu-id="74853-137">Mandatory</span></span>|<span data-ttu-id="74853-138">Indirizzo IP di hello del Server di configurazione</span><span class="sxs-lookup"><span data-stu-id="74853-138">IP of hello Configuration Server</span></span>|<span data-ttu-id="74853-139">Qualsiasi indirizzo IP valido</span><span class="sxs-lookup"><span data-stu-id="74853-139">Any valid IP Address</span></span>|
|<span data-ttu-id="74853-140">-P</span><span class="sxs-lookup"><span data-stu-id="74853-140">-P</span></span> |<span data-ttu-id="74853-141">Mandatory</span><span class="sxs-lookup"><span data-stu-id="74853-141">Mandatory</span></span>|<span data-ttu-id="74853-142">File di hello del percorso completo del file in cui è stata salvata hello connessione passphrase</span><span class="sxs-lookup"><span data-stu-id="74853-142">Full file path hello file where hello connection passphrase is saved</span></span>|<span data-ttu-id="74853-143">Qualsiasi cartella valida</span><span class="sxs-lookup"><span data-stu-id="74853-143">Any valid folder</span></span>|
