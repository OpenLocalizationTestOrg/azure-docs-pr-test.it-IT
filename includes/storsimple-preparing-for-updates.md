<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a>Preparazione per gli aggiornamenti
È necessario hello tooperform seguendo i passaggi prima di analizzare e applicare l'aggiornamento di hello:

1. Uno snapshot cloud di dati del dispositivo hello.
2. Verificare che il controller di indirizzi IP fisso siano instradabile e possano connettersi toohello Internet. Questi indirizzi IP fissi saranno dispositivo tooyour di tooservice utilizzati gli aggiornamenti. È possibile testare questo eseguendo i seguenti cmdlet su ciascun controller dall'interfaccia di Windows PowerShell hello del dispositivo hello hello:
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    **Output di esempio per Test-Connection quando gli indirizzi IP fissi possono connettersi a Internet toohello**

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

Dopo questi controlli preliminari su manuali è stata completata, è possibile procedere tooscan e installare gli aggiornamenti di hello.

