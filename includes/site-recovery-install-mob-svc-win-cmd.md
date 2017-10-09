1. Copiare la cartella locale di tooa installer hello (ad esempio C:\Temp) nel server di hello che si desidera tooprotect. Eseguire hello seguenti comandi come amministratore a un prompt dei comandi:

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. tooinstall servizio di mobilità, eseguire hello comando seguente:

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. Agente hello deve ora toobe registrato con hello del Server di configurazione.

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a>Argomenti della riga di comando del programma di installazione del servizio Mobility

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| Parametro|Tipo|Descrizione|Valori possibili|
|-|-|-|-|
|/Role|Mandatory|Specifica se installare il servizio Mobility (MS) o MasterTarget (MT)|MS </br> MT|
|/InstallLocation|Facoltativo|Percorso in cui viene installato il servizio Mobility|Qualsiasi cartella nel computer di hello|
|/Platform|Mandatory|Specifica la piattaforma di hello in cui hello è recupero installato servizio di mobilità </br> </br>- **VMware**: usare questo valore se si installa il servizio Mobility in una macchina virtuale in esecuzione in *host VMware vSphere ESXi*, *host Hyper-V* o *server fisici* </br> - **Azure**: usare questo valore se si installa un agente in una macchina virtuale IaaS di Azure| VMware </br> Azure|
|/Silent|Facoltativo|Specifica il programma di installazione di toorun hello in modalità invisibile all'utente| ND|

>[!TIP]
> i log di installazione di Hello sono reperibile nella %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log

#### <a name="mobility-service-registration-command-line-arguments"></a>Argomenti della riga di comando per la registrazione del servizio Mobility

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | Parametro|Tipo|Descrizione|Valori possibili|
  |-|-|-|-|
  |/CSEndPoint |Mandatory|Indirizzo IP hello del server di configurazione| Qualsiasi indirizzo IP valido|
  |/PassphraseFilePath|Mandatory|Percorso di hello passphrase |Qualsiasi percorso file locale o UNC valido|


>[!TIP]
> Hello AgentConfiguration log è reperibile nella %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log
