<span data-ttu-id="7cac2-101">Hello passaggi toounregister un server di elaborazione varia a seconda della relativo stato di connessione con hello del Server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="7cac2-101">hello steps toounregister a process server differs depending on its connection status with hello Configuration Server.</span></span>

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a><span data-ttu-id="7cac2-102">Annullare la registrazione di un server di elaborazione in stato connesso</span><span class="sxs-lookup"><span data-stu-id="7cac2-102">Unregister a process server that is in a connected state</span></span>

1. <span data-ttu-id="7cac2-103">Accedere in remoto i server di elaborazione hello come amministratore.</span><span class="sxs-lookup"><span data-stu-id="7cac2-103">Remote into hello process server as an Administrator.</span></span>
2. <span data-ttu-id="7cac2-104">Avviare hello **Pannello di controllo** e aprire **programmi > Disinstalla un programma**</span><span class="sxs-lookup"><span data-stu-id="7cac2-104">Launch hello **Control Panel** and open **Programs > Uninstall a program**</span></span>
3. <span data-ttu-id="7cac2-105">Disinstalla un programma in base al nome hello **Microsoft Azure Site Recovery/processo di configurazione Server**</span><span class="sxs-lookup"><span data-stu-id="7cac2-105">Uninstall a program by hello name **Microsoft Azure Site Recovery Configuration/Process Server**</span></span>
4. <span data-ttu-id="7cac2-106">Dopo aver completato il passaggio 3, è possibile disinstallare le **dipendenze del server di configurazione/elaborazione di Microsoft Azure Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="7cac2-106">Once step 3 is completed, you can uninstall **Microsoft Azure Site Recovery Configuration/Process Server Dependencies**</span></span>

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a><span data-ttu-id="7cac2-107">Annullare la registrazione di un server di elaborazione in stato disconnesso</span><span class="sxs-lookup"><span data-stu-id="7cac2-107">Unregister a process server that is in a disconnected state</span></span>

> [!WARNING]
> <span data-ttu-id="7cac2-108">Hello di utilizzare i passaggi successivi da utilizzare se è presente alcuna macchina virtuale di modo toorevive hello in cui hello è stato installato Server di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="7cac2-108">Use hello below steps should be used if there is no way toorevive hello virtual machine on which hello Process Server was installed.</span></span>

1. <span data-ttu-id="7cac2-109">Accedere come amministratore del server di configurazione tooyour.</span><span class="sxs-lookup"><span data-stu-id="7cac2-109">Log on tooyour configuration server as an Administrator.</span></span>
2. <span data-ttu-id="7cac2-110">Aprire un prompt dei comandi amministrativo e sfogliare la directory toohello `%ProgramData%\ASR\home\svsystems\bin`.</span><span class="sxs-lookup"><span data-stu-id="7cac2-110">Open an Administrative command prompt and browse toohello directory `%ProgramData%\ASR\home\svsystems\bin`.</span></span>
3. <span data-ttu-id="7cac2-111">A questo punto, eseguire il comando hello.</span><span class="sxs-lookup"><span data-stu-id="7cac2-111">Now run hello command.</span></span>

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. <span data-ttu-id="7cac2-112">Questo ripulisce dettagli hello hello del server di elaborazione dal sistema hello.</span><span class="sxs-lookup"><span data-stu-id="7cac2-112">This will purge hello details of hello process server from hello system.</span></span>
