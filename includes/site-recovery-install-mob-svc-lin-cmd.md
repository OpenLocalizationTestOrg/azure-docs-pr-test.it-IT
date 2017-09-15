1. <span data-ttu-id="f5419-101">Copiare il programma di installazione in una cartella locale (ad esempio /tmp) sul server che si vuole proteggere.</span><span class="sxs-lookup"><span data-stu-id="f5419-101">Copy the installer to a local folder (for example, /tmp) on the server that you want to protect.</span></span> <span data-ttu-id="f5419-102">Eseguire i comandi seguenti in un terminale:</span><span class="sxs-lookup"><span data-stu-id="f5419-102">In a terminal, run the following commands:</span></span>
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. <span data-ttu-id="f5419-103">Per installare il servizio Mobility, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f5419-103">To install Mobility Service, run the following command:</span></span>

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. <span data-ttu-id="f5419-104">Al termine dell'installazione è necessario registrare il servizio Mobility nel server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f5419-104">Once installation is complete, the Mobility Service needs to get registered to the configuration server.</span></span> <span data-ttu-id="f5419-105">Eseguire questo comando per registrare il servizio Mobility nel server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="f5419-105">Run the following command to register the Mobility Service with Configuration server.</span></span>

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a><span data-ttu-id="f5419-106">Riga di comando del programma di installazione del servizio Mobility</span><span class="sxs-lookup"><span data-stu-id="f5419-106">Mobility Service installer command-line</span></span>

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|<span data-ttu-id="f5419-107">Parametro</span><span class="sxs-lookup"><span data-stu-id="f5419-107">Parameter</span></span>|<span data-ttu-id="f5419-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="f5419-108">Type</span></span>|<span data-ttu-id="f5419-109">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f5419-109">Description</span></span>|<span data-ttu-id="f5419-110">Valori possibili</span><span class="sxs-lookup"><span data-stu-id="f5419-110">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="f5419-111">-r</span><span class="sxs-lookup"><span data-stu-id="f5419-111">-r</span></span> |<span data-ttu-id="f5419-112">Mandatory</span><span class="sxs-lookup"><span data-stu-id="f5419-112">Mandatory</span></span>|<span data-ttu-id="f5419-113">Specifica se installare il servizio Mobility (MS) o MasterTarget (MT)</span><span class="sxs-lookup"><span data-stu-id="f5419-113">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="f5419-114">MS</span><span class="sxs-lookup"><span data-stu-id="f5419-114">MS</span></span> </br> <span data-ttu-id="f5419-115">MT</span><span class="sxs-lookup"><span data-stu-id="f5419-115">MT</span></span>|
|<span data-ttu-id="f5419-116">-d</span><span class="sxs-lookup"><span data-stu-id="f5419-116">-d</span></span> |<span data-ttu-id="f5419-117">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="f5419-117">Optional</span></span>|<span data-ttu-id="f5419-118">Percorso in cui verrà installato il servizio Mobility</span><span class="sxs-lookup"><span data-stu-id="f5419-118">Location where Mobility Service will be installed</span></span>|<span data-ttu-id="f5419-119">/usr/local/ASR</span><span class="sxs-lookup"><span data-stu-id="f5419-119">/usr/local/ASR</span></span>|
|<span data-ttu-id="f5419-120">-v</span><span class="sxs-lookup"><span data-stu-id="f5419-120">-v</span></span>|<span data-ttu-id="f5419-121">Mandatory</span><span class="sxs-lookup"><span data-stu-id="f5419-121">Mandatory</span></span>|<span data-ttu-id="f5419-122">Specifica la piattaforma in cui viene installato il servizio Mobility</span><span class="sxs-lookup"><span data-stu-id="f5419-122">Specifies the platform on which the Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="f5419-123">- **VMware**: usare questo valore se si installa il servizio Mobility in una macchina virtuale in esecuzione in *host VMware vSphere ESXi*, *host Hyper-V* o *server fisici*</span><span class="sxs-lookup"><span data-stu-id="f5419-123">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="f5419-124">- **Azure**: usare questo valore se si installa un agente in una macchina virtuale IaaS di Azure</span><span class="sxs-lookup"><span data-stu-id="f5419-124">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="f5419-125">VMware</span><span class="sxs-lookup"><span data-stu-id="f5419-125">VMware</span></span> </br> <span data-ttu-id="f5419-126">Azure</span><span class="sxs-lookup"><span data-stu-id="f5419-126">Azure</span></span>|
|<span data-ttu-id="f5419-127">-q</span><span class="sxs-lookup"><span data-stu-id="f5419-127">-q</span></span>|<span data-ttu-id="f5419-128">Facoltativo</span><span class="sxs-lookup"><span data-stu-id="f5419-128">Optional</span></span>|<span data-ttu-id="f5419-129">Specifica l'esecuzione del programma di installazione in modalità non interattiva</span><span class="sxs-lookup"><span data-stu-id="f5419-129">Specifies to run installer in silent mode</span></span>| <span data-ttu-id="f5419-130">N/D </span><span class="sxs-lookup"><span data-stu-id="f5419-130">N/A</span></span>|


#### <a name="mobility-service-configuration-command-line"></a><span data-ttu-id="f5419-131">Riga di comando di configurazione del servizio Mobility</span><span class="sxs-lookup"><span data-stu-id="f5419-131">Mobility Service configuration command-line</span></span>

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|<span data-ttu-id="f5419-132">Parametro</span><span class="sxs-lookup"><span data-stu-id="f5419-132">Parameter</span></span>|<span data-ttu-id="f5419-133">Tipo</span><span class="sxs-lookup"><span data-stu-id="f5419-133">Type</span></span>|<span data-ttu-id="f5419-134">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f5419-134">Description</span></span>|<span data-ttu-id="f5419-135">Valori possibili</span><span class="sxs-lookup"><span data-stu-id="f5419-135">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="f5419-136">-i</span><span class="sxs-lookup"><span data-stu-id="f5419-136">-i</span></span> |<span data-ttu-id="f5419-137">Mandatory</span><span class="sxs-lookup"><span data-stu-id="f5419-137">Mandatory</span></span>|<span data-ttu-id="f5419-138">Indirizzo IP del server di configurazione</span><span class="sxs-lookup"><span data-stu-id="f5419-138">IP of the Configuration Server</span></span>|<span data-ttu-id="f5419-139">Qualsiasi indirizzo IP valido</span><span class="sxs-lookup"><span data-stu-id="f5419-139">Any valid IP Address</span></span>|
|<span data-ttu-id="f5419-140">-P</span><span class="sxs-lookup"><span data-stu-id="f5419-140">-P</span></span> |<span data-ttu-id="f5419-141">Mandatory</span><span class="sxs-lookup"><span data-stu-id="f5419-141">Mandatory</span></span>|<span data-ttu-id="f5419-142">Percorso completo del file in cui viene salvata la passphrase di connessione</span><span class="sxs-lookup"><span data-stu-id="f5419-142">Full file path the file where the connection passphrase is saved</span></span>|<span data-ttu-id="f5419-143">Qualsiasi cartella valida</span><span class="sxs-lookup"><span data-stu-id="f5419-143">Any valid folder</span></span>|
