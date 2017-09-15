<span data-ttu-id="1befc-101">La procedura per annullare la registrazione di un server di elaborazione varia a seconda dello stato di connessione con il server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="1befc-101">The steps to unregister a process server differs depending on its connection status with the Configuration Server.</span></span>

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a><span data-ttu-id="1befc-102">Annullare la registrazione di un server di elaborazione in stato connesso</span><span class="sxs-lookup"><span data-stu-id="1befc-102">Unregister a process server that is in a connected state</span></span>

1. <span data-ttu-id="1befc-103">Accedere in remoto al server di elaborazione come amministratore.</span><span class="sxs-lookup"><span data-stu-id="1befc-103">Remote into the process server as an Administrator.</span></span>
2. <span data-ttu-id="1befc-104">Avviare il **Pannello di controllo** e aprire **Programmi > Disinstalla un programma**.</span><span class="sxs-lookup"><span data-stu-id="1befc-104">Launch the **Control Panel** and open **Programs > Uninstall a program**</span></span>
3. <span data-ttu-id="1befc-105">Disinstallare il **server di configurazione/elaborazione di Microsoft Azure Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="1befc-105">Uninstall a program by the name **Microsoft Azure Site Recovery Configuration/Process Server**</span></span>
4. <span data-ttu-id="1befc-106">Dopo aver completato il passaggio 3, è possibile disinstallare le **dipendenze del server di configurazione/elaborazione di Microsoft Azure Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="1befc-106">Once step 3 is completed, you can uninstall **Microsoft Azure Site Recovery Configuration/Process Server Dependencies**</span></span>

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a><span data-ttu-id="1befc-107">Annullare la registrazione di un server di elaborazione in stato disconnesso</span><span class="sxs-lookup"><span data-stu-id="1befc-107">Unregister a process server that is in a disconnected state</span></span>

> [!WARNING]
> <span data-ttu-id="1befc-108">Se non è possibile ripristinare la macchina virtuale in cui è stato installato il server di elaborazione, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="1befc-108">Use the below steps should be used if there is no way to revive the virtual machine on which the Process Server was installed.</span></span>

1. <span data-ttu-id="1befc-109">Accedere al server di configurazione come amministratore.</span><span class="sxs-lookup"><span data-stu-id="1befc-109">Log on to your configuration server as an Administrator.</span></span>
2. <span data-ttu-id="1befc-110">Aprire un prompt dei comandi amministrativo e passare alla directory `%ProgramData%\ASR\home\svsystems\bin`.</span><span class="sxs-lookup"><span data-stu-id="1befc-110">Open an Administrative command prompt and browse to the directory `%ProgramData%\ASR\home\svsystems\bin`.</span></span>
3. <span data-ttu-id="1befc-111">Eseguire il comando.</span><span class="sxs-lookup"><span data-stu-id="1befc-111">Now run the command.</span></span>

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. <span data-ttu-id="1befc-112">I dettagli del server di elaborazione verranno eliminati dal sistema.</span><span class="sxs-lookup"><span data-stu-id="1befc-112">This will purge the details of the process server from the system.</span></span>
