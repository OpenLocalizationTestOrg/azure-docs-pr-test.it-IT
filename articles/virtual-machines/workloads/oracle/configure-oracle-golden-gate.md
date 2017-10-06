---
title: aaaImplement Gate d'oro Oracle in una macchina virtuale Linux di Azure | Documenti Microsoft
description: Implementare rapidamente Oracle Golden Gate nell'ambiente Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: rclaus
ms.openlocfilehash: 320cafd5d23ee472f0af9f92577bc6f432f65778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a>Implementare Oracle Golden Gate in una VM Linux di Azure 

Hello CLI di Azure viene utilizzato toocreate e gestire le risorse di Azure dalla riga di comando hello o negli script. Questa guida descrive come toouse hello Azure CLI toodeploy Oracle 12C del database di immagine della raccolta hello Azure Marketplace. 

Questo documento viene illustrata la procedura dettagliata come toocreate, installare e configurare il controllo d'oro Oracle in una macchina virtuale di Azure.

Prima di iniziare, verificare che tale hello che CLI di Azure è stato installato. Per altre informazioni, vedere [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli) (Guida all'installazione dell'interfaccia della riga di comando di Azure).

## <a name="prepare-hello-environment"></a>Preparare l'ambiente hello

installazione di Oracle d'oro Gate hello tooperform, è necessario toocreate due macchine virtuali di Azure su hello stesso set di disponibilità. immagine del Marketplace Hello è utilizzare toocreate hello macchine virtuali è **Oracle: Oracle-Database-Ee:12.1.0.2:latest**.

Inoltre necessario toobe familiarità con Unix editor vi e avere una conoscenza di base di x11 (Windows X).

di seguito Hello è un riepilogo della configurazione dell'ambiente hello:
> 
> |  | **Sito primario** | **Sito di replica** |
> | --- | --- | --- |
> | **Versione di Oracle** |Oracle 12c Release 2 – (12.1.0.2) |Oracle 12c Release 2 – (12.1.0.2)|
> | **Nome computer** |myVM1 |myVM2 |
> | **Sistema operativo** |Oracle Linux 6.x |Oracle Linux 6.x |
> | **SID Oracle** |CDB1 |CDB1 |
> | **Schema di replica** |TEST|TEST |
> | **Proprietario/replica Golden Gate** |C##GGADMIN |REPUSER |
> | **Processo Golden Gate** |EXTORA |REPORA|


### <a name="sign-in-tooazure"></a>Accedi tooAzure 

Accedere alla sottoscrizione di Azure con hello tooyour [accesso az](/cli/azure/#login) comando. Quindi seguire hello le direzioni.

```azurecli
az login
```

### <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando. Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite. 

esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `westus` percorso.

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a>Creare un set di disponibilità

Hello riportata dopo il passaggio è facoltativo ma consigliato. Per altre informazioni, vedere [Linee guida per i set di disponibilità di Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a>Creare una macchina virtuale

Creare una macchina virtuale con hello [creare vm az](/cli/azure/vm#create) comando. 

esempio Hello crea due macchine virtuali denominate `myVM1` e `myVM2`. Creare le chiavi SSH, se non esistono già in una posizione predefinita. toouse uno specifico set di chiavi, utilizzare hello `--ssh-key-value` opzione.

#### <a name="create-myvm1-primary"></a>Creare myVM1 (primaria):
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

Dopo l'hello che macchina virtuale è stata creata, hello CLI di Azure Visualizza informazioni toohello simile esempio seguente. (Prendere nota di hello `publicIpAddress`. Questo indirizzo è utilizzato tooaccess hello VM).

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

#### <a name="create-myvm2-replicate"></a>Creare myVM2 (replica):
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

Prendere nota di hello `publicIpAddress` anche dopo che è stato creato.

### <a name="open-hello-tcp-port-for-connectivity"></a>Aprire la porta TCP hello per la connettività

passaggio successivo Hello è tooconfigure endpoint esterni, che consentono di database di Oracle tooaccess hello in modalità remota. tooconfigure hello endpoint esterni, eseguire hello i comandi seguenti.

#### <a name="open-hello-port-for-myvm1"></a>Aprire la porta hello per myVM1:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

risultati Hello dovrebbero essere simile toohello seguente risposta:

```bash
{
  "access": "Allow",
  "description": null,
  "destinationAddressPrefix": "*",
  "destinationPortRange": "1521",
  "direction": "Inbound",
  "etag": "W/\"bd77dcae-e5fd-4bd6-a632-26045b646414\"",
  "id": "/subscriptions/<subscription-id>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myVmNSG/securityRules/allow-oracle",
  "name": "allow-oracle",
  "priority": 999,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

#### <a name="open-hello-port-for-myvm2"></a>Aprire la porta hello per myVM2:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a>Connettere la macchina virtuale di toohello

Comando che segue di hello utilizzare toocreate una sessione SSH con la macchina virtuale hello. Sostituire l'indirizzo IP hello con hello `publicIpAddress` della macchina virtuale.

```bash 
ssh <publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a>Creare il database di hello in myVM1 (primario)

Hello software Oracle è già installato in un'immagine del Marketplace hello, pertanto la fase successiva hello database hello tooinstall. 

Eseguire software hello come utente avanzato 'oracle' hello:

```bash
sudo su - oracle
```

Crea database hello:

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
Output dovrebbe essere simile toohello seguente risposta:

```bash
Copying database files
1% complete
2% complete
8% complete
13% complete
19% complete
27% complete
Creating and starting Oracle instance
29% complete
32% complete
33% complete
34% complete
38% complete
42% complete
43% complete
45% complete
Completing Database Creation
48% complete
51% complete
53% complete
62% complete
70% complete
72% complete
Creating Pluggable Databases
78% complete
100% complete
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

Impostare le variabili ORACLE_SID e ORACLE_HOME hello.

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

Facoltativamente, è possibile aggiungere file di .bashrc toohello ORACLE_HOME e ORACLE_SID, in modo che queste impostazioni vengono salvate per accessi futuri:

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a>Avviare il listener Oracle
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-hello-database-on-myvm2-replicate"></a>Creare database hello in myVM2 (replica)

```bash
sudo su - oracle
```
Crea database hello:

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
Impostare le variabili ORACLE_SID e ORACLE_HOME hello.

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

Facoltativamente, è possibile ORACLE_HOME e ORACLE_SID toohello .bashrc file aggiunto, in modo che queste impostazioni vengono salvate per accessi futuri.

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a>Avviare il listener Oracle
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a>Configurare Golden Gate 
tooconfigure Gate d'oro, eseguire i passaggi di hello in questa sezione.

### <a name="enable-archive-log-mode-on-myvm1-primary"></a>Abilitare la modalità archivelog in myVM1 (primaria)

```bash
$ sqlplus / as sysdba
SQL> SELECT log_mode FROM v$database;

LOG_MODE
------------
NOARCHIVELOG

SQL> SHUTDOWN IMMEDIATE;
SQL> STARTUP MOUNT;
SQL> ALTER DATABASE ARCHIVELOG;
SQL> ALTER DATABASE OPEN;
```
Abilitare la registrazione forzata e verificare che sia presente almeno un file di registro.

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a>Scaricare il software Golden Gate
toodownload e preparare il software Oracle d'oro Gate hello, hello completo alla procedura seguente:

1. Scaricare hello **fbo_ggs_Linux_x64_shiphome.zip** file hello [pagina di download di Oracle d'oro Gate](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html). In hello Scarica titolo **12.x.x.x di Oracle GoldenGate per Oracle Linux x86-64**, dovrebbe esserci un set di toodownload file con estensione zip.

2. Dopo aver scaricato hello ZIP file tooyour client computer, utilizzare il protocollo Secure di copia (SCP) toocopy hello file tooyour VM:

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. Spostare hello ZIP file toohello **/OPT** cartella. Modificare quindi il proprietario di hello del file hello come segue:

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. Decomprimere il file di hello (installazione hello Linux decomprimere utilità se non è già installato):

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. Modificare l'autorizzazione:

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-hello-client-and-vm-toorun-x11-for-windows-clients-only"></a>Preparare client hello e VM toorun x11 (solo client di Windows)
Si tratta di un passaggio facoltativo. Può essere ignorato se si usa un client Linux o se x11 è già configurato.

1. Download di PuTTY e Xming computer Windows tooyour:

  * [Scaricare PuTTY](http://www.putty.org/)
  * [Scaricare Xming](https://xming.en.softonic.com/)

2.  Dopo aver installato PuTTY, in hello PuTTY cartella (ad esempio, c:\Programmi\Microsoft Files\PuTTY), eseguire puttygen.exe (Generatore di chiavi di PuTTY).

3.  Nel generatore di chiavi PuTTY:

  - toogenerate hello un chiave, seleziona **genera** pulsante.
  - Copiare il contenuto di hello della chiave di hello (**Ctrl + C**).
  - Seleziona hello **Salva la chiave privata** pulsante.
  - Ignorare l'avviso hello visualizzata e quindi seleziona **OK**.

    ![Schermata della pagina di hello PuTTY generatore di chiavi](./media/oracle-golden-gate/puttykeygen.png)

4.  Nella macchina virtuale eseguire questi comandi:

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. Creare un file denominato **authorized_keys**. Incollare il contenuto di hello della chiave di hello in questo file e quindi salvare il file hello.

  > [!NOTE]
  > chiave di Hello deve contenere la stringa hello `ssh-rsa`. Inoltre, il contenuto di hello della chiave hello deve essere una singola riga di testo.
  >  

6. Avviare PuTTY. In hello **categoria** riquadro, selezionare **connessione** > **SSH** > **Auth**. In hello **file di chiave privata per l'autenticazione** passare toohello chiave generata in precedenza.

  ![Schermata della pagina di impostare la chiave privata hello](./media/oracle-golden-gate/setprivatekey.png)

7. In hello **categoria** riquadro, selezionare **connessione** > **SSH** > **X11**. Selezionare quindi hello **inoltro X11 Enable** casella.

  ![Schermata della pagina attiva X11 hello](./media/oracle-golden-gate/enablex11.png)

8. In hello **categoria** riquadro andare troppo**sessione**. Immettere le informazioni host hello e quindi selezionare **aprire**.

  ![Schermata della pagina della sessione hello](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a>Installare il software Golden Gate

tooinstall Oracle d'oro Gate, hello completo alla procedura seguente:

1. Accedere come oracle. (Deve essere in grado di toosign in senza che venga richiesta una password.) Assicurarsi che Xming sia in esecuzione prima di iniziare l'installazione di hello.
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. Selezionare 'Oracle GoldenGate for Oracle Database 12c'. Selezionare quindi **Avanti** toocontinue.

  ![Schermata della pagina di installazione selezionare hello programma di installazione](./media/oracle-golden-gate/golden_gate_install_01.png)

3. Modificare il percorso di software hello. Selezionare quindi hello **avvia Gestione** e immettere il percorso di database hello. Selezionare **Avanti** toocontinue.

  ![Schermata della pagina di installazione selezionare hello](./media/oracle-golden-gate/golden_gate_install_02.png)

4. Cambiare directory inventario hello e quindi selezionare **Avanti** toocontinue.

  ![Schermata della pagina di installazione selezionare hello](./media/oracle-golden-gate/golden_gate_install_03.png)

5. In hello **riepilogo** selezionare **installare** toocontinue.

  ![Schermata della pagina di installazione selezionare hello programma di installazione](./media/oracle-golden-gate/golden_gate_install_04.png)

6. Potrebbe essere richiesta toorun uno script come 'radice'. In questo caso, aprire una sessione separata, ssh toohello tooroot sudo, macchina virtuale, quindi eseguire script hello. Selezionare **OK** per continuare.

  ![Schermata della pagina di installazione selezionare hello](./media/oracle-golden-gate/golden_gate_install_05.png)

7. Al termine dell'installazione di hello, selezionare **Chiudi** processo hello toocomplete.

  ![Schermata della pagina di installazione selezionare hello](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a>Configurare il servizio in myVM1 (primaria)

1. Creare o aggiornare il file tnsnames.ora hello:

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. Creare hello d'oro Gate proprietario e agli account utente.

  > [!NOTE]
  > account del proprietario Hello deve contenere il prefisso di C# #.
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA tooC##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. Creare account utente di prova d'oro Gate hello:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. Configurare hello Estrai parametro file.

 Avviare l'interfaccia della riga di comando di hello gate finale (ggsci):

  ```bash
  $ sudo su - oracle
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> DBLOGIN USERID test@pdb1, PASSWORD test
  Successfully logged into database  pdb1
  GGSCI>  ADD SCHEMATRANDATA pdb1.test
  2017-05-23 15:44:25  INFO    OGG-01788  SCHEMATRANDATA has been added on schema test.
  2017-05-23 15:44:25  INFO    OGG-01976  SCHEMATRANDATA for scheduling columns has been added on schema test.

  GGSCI> EDIT PARAMS EXTORA
  ```
5. Aggiungere hello seguente toohello Estrai file dei parametri (mediante comandi vi). Premere il tasto Esc, ':wq!' file toosave. 

  ```bash
  EXTRACT EXTORA
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTRAIL ./dirdat/rt  
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT 
  LOGALLSUPCOLS
  UPDATERECORDFORMAT COMPACT
  TABLE pdb1.test.TCUSTMER;
  TABLE pdb1.test.TCUSTORD;
  ```
6. REGISTER EXTRACT - estrazione integrata:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. Configurare i checkpoint di estrazione e avviare l'estrazione in tempo reale:

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request tooMANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
In questo passaggio si trovare hello avvio SCN, che verrà utilizzato in un secondo momento, in un'altra sezione:

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> SELECT current_scn from v$database;
  CURRENT_SCN
  -----------
      1857887
  SQL> EXIT;
  ```

  ```bash
  $ ./ggsci
  GGSCI> EDIT PARAMS INITEXT
  ```

  ```bash
  EXTRACT INITEXT
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTASK REPLICAT, GROUP INITREP
  TABLE pdb1.test.*, SQLPREDICATE 'AS OF SCN 1857887'; 
  ```

  ```bash
  GGSCI> ADD EXTRACT INITEXT, SOURCEISTABLE
  ```

### <a name="set-up-service-on-myvm2-replicate"></a>Configurare il servizio in myVM2 (replica)


1. Creare o aggiornare il file tnsnames.ora hello:

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. Creare un account di replica:

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba toorepuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. Creare un account dell'utente di test di Golden Gate:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. REPLICAT parametro tooreplicate le modifiche al file: 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  Contenuto del file dei parametri REPORA:

  ```bash
  REPLICAT REPORA
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/repora.dsc, PURGE, MEGABYTES 100
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT
  DBOPTIONS INTEGRATEDPARAMS(parallelism 6)
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;
  ```

5. Configurare un checkpoint replicat:

  ```bash
  GGSCI> ADD REPLICAT REPORA, INTEGRATED, EXTTRAIL ./dirdat/rt
  GGSCI> EDIT PARAMS INITREP

  ```

  ```bash
  REPLICAT INITREP
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/tcustmer.dsc, APPEND
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;   
  ```

  ```bash
  GGSCI> ADD REPLICAT INITREP, SPECIALRUN
  ```

### <a name="set-up-hello-replication-myvm1-and-myvm2"></a>Configurare la replica di hello (myVM1 e myVM2)

#### <a name="1-set-up-hello-replication-on-myvm2-replicate"></a>1. Configurare la replica di hello in myVM2 (replica)

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
Aggiornare il file hello seguente hello:

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
Quindi riavviare il servizio di gestione hello:

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-hello-replication-on-myvm1-primary"></a>2. Configurare la replica di hello in myVM1 (primario)

Avviare il caricamento iniziale hello e controllare gli errori:

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-hello-replication-on-myvm2-replicate"></a>3. Configurare la replica di hello in myVM2 (replica)

Modificare hello numero SCN con hello ottenuto prima di:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
replica Hello è iniziata ed è possibile eseguirne il test tramite l'inserimento di nuove tabelle tooTEST di record.


### <a name="view-job-status-and-troubleshooting"></a>Visualizzare lo stato del processo e le informazioni di risoluzione dei problemi

#### <a name="view-reports"></a>Visualizzazione dei report
tooview segnala myVM1, eseguire hello seguenti comandi:

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
tooview segnala myVM2, eseguire hello seguenti comandi:

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a>Visualizzare stato e cronologia
stato tooview e cronologia myVM1, eseguire hello seguenti comandi:

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

stato tooview e cronologia myVM2, eseguire hello seguenti comandi:

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
Questo completa hello installazione e configurazione del controllo d'oro in Oracle linux.


## <a name="delete-hello-virtual-machine"></a>Eliminare la macchina virtuale hello

Quando non è più necessario, è possibile hello comando seguente gruppo di risorse utilizzato tooremove hello VM e tutte le relative risorse.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Passaggi successivi

[Creare esercitazioni per macchine virtuali a disponibilità elevata](../../linux/create-cli-complete.md)

[Esplorare gli esempi dell'interfaccia della riga di comando per la distribuzione della VM](../../linux/cli-samples.md)
