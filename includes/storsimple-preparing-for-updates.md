<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a><span data-ttu-id="8026a-101">Preparazione per gli aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="8026a-101">Preparing for updates</span></span>
<span data-ttu-id="8026a-102">È necessario hello tooperform seguendo i passaggi prima di analizzare e applicare l'aggiornamento di hello:</span><span class="sxs-lookup"><span data-stu-id="8026a-102">You will need tooperform hello following steps before you scan and apply hello update:</span></span>

1. <span data-ttu-id="8026a-103">Uno snapshot cloud di dati del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="8026a-103">Take a cloud snapshot of hello device data.</span></span>
2. <span data-ttu-id="8026a-104">Verificare che il controller di indirizzi IP fisso siano instradabile e possano connettersi toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="8026a-104">Ensure that your controller fixed IPs are routable and can connect toohello Internet.</span></span> <span data-ttu-id="8026a-105">Questi indirizzi IP fissi saranno dispositivo tooyour di tooservice utilizzati gli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="8026a-105">These fixed IPs will be used tooservice updates tooyour device.</span></span> <span data-ttu-id="8026a-106">È possibile testare questo eseguendo i seguenti cmdlet su ciascun controller dall'interfaccia di Windows PowerShell hello del dispositivo hello hello:</span><span class="sxs-lookup"><span data-stu-id="8026a-106">You can test this by running hello following cmdlet on each controller from hello Windows PowerShell interface of hello device:</span></span>
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    <span data-ttu-id="8026a-107">**Output di esempio per Test-Connection quando gli indirizzi IP fissi possono connettersi a Internet toohello**</span><span class="sxs-lookup"><span data-stu-id="8026a-107">**Sample output for Test-Connection when fixed IPs can connect toohello Internet**</span></span>

        Controller0>Test-Connection -Source 10.126.173.91 -Destination bing.com

        Source      Destination     IPV4Address      IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200

        Controller0>Test-Connection -Source 10.126.173.91 -Destination  204.79.197.200

        Source      Destination       IPV4Address    IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200

<span data-ttu-id="8026a-108">Dopo questi controlli preliminari su manuali è stata completata, è possibile procedere tooscan e installare gli aggiornamenti di hello.</span><span class="sxs-lookup"><span data-stu-id="8026a-108">After you have successfully completed these manual pre-checks, you can proceed tooscan and install hello updates.</span></span>

