Hello passaggi toounregister un server di elaborazione varia a seconda della relativo stato di connessione con hello del Server di configurazione.

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a>Annullare la registrazione di un server di elaborazione in stato connesso

1. Accedere in remoto i server di elaborazione hello come amministratore.
2. Avviare hello **Pannello di controllo** e aprire **programmi > Disinstalla un programma**
3. Disinstalla un programma in base al nome hello **Microsoft Azure Site Recovery/processo di configurazione Server**
4. Dopo aver completato il passaggio 3, è possibile disinstallare le **dipendenze del server di configurazione/elaborazione di Microsoft Azure Site Recovery**.

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a>Annullare la registrazione di un server di elaborazione in stato disconnesso

> [!WARNING]
> Hello di utilizzare i passaggi successivi da utilizzare se è presente alcuna macchina virtuale di modo toorevive hello in cui hello è stato installato Server di elaborazione.

1. Accedere come amministratore del server di configurazione tooyour.
2. Aprire un prompt dei comandi amministrativo e sfogliare la directory toohello `%ProgramData%\ASR\home\svsystems\bin`.
3. A questo punto, eseguire il comando hello.

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. Questo ripulisce dettagli hello hello del server di elaborazione dal sistema hello.
