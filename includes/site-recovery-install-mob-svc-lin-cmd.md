1. Copiare hello installer tooa cartella locale (ad esempio, /tmp) hello server che si desidera tooprotect. In un terminale del, eseguire hello seguenti comandi:
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. tooinstall servizio di mobilità, eseguire hello comando seguente:

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. Al termine dell'installazione, è necessario server di configurazione registrati toohello tooget hello servizio di mobilità. Comando che segue di esecuzione hello tooregister hello, servizio di mobilità con server di configurazione.

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a>Riga di comando del programma di installazione del servizio Mobility

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|Parametro|Tipo|Descrizione|Valori possibili|
|-|-|-|-|
|-r |Mandatory|Specifica se installare il servizio Mobility (MS) o MasterTarget (MT)|MS </br> MT|
|-d |Facoltativo|Percorso in cui verrà installato il servizio Mobility|/usr/local/ASR|
|-v|Mandatory|Specifica la piattaforma di hello in cui hello è recupero installato servizio di mobilità </br> </br>- **VMware**: usare questo valore se si installa il servizio Mobility in una macchina virtuale in esecuzione in *host VMware vSphere ESXi*, *host Hyper-V* o *server fisici* </br> - **Azure**: usare questo valore se si installa un agente in una macchina virtuale IaaS di Azure| VMware </br> Azure|
|-q|Facoltativo|Specifica toorun programma di installazione in modalità invisibile all'utente| N/D|


#### <a name="mobility-service-configuration-command-line"></a>Riga di comando di configurazione del servizio Mobility

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|Parametro|Tipo|Descrizione|Valori possibili|
|-|-|-|-|
|-i |Mandatory|Indirizzo IP di hello del Server di configurazione|Qualsiasi indirizzo IP valido|
|-P |Mandatory|File di hello del percorso completo del file in cui è stata salvata hello connessione passphrase|Qualsiasi cartella valida|
