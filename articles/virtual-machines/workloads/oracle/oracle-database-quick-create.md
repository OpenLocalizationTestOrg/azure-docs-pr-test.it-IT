---
title: aaaCreate un database Oracle in una macchina virtuale di Azure | Documenti Microsoft
description: Ottenere rapidamente un database Oracle 12c operativo nell'ambiente Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/17/2017
ms.author: rclaus
ms.openlocfilehash: 83205154c3275d5f57b46c8acfb0cb4e5c68a412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-oracle-database-in-an-azure-vm"></a>Creare un database Oracle in una VM di Azure

Questa guida descrive con hello Azure CLI toodeploy una macchina virtuale di Azure da hello [immagine della raccolta marketplace Oracle](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) in un database Oracle 12C ordine toocreate. Dopo aver distribuito il server di hello, verrà effettuata la connessione via SSH nel database di Oracle hello tooconfigure ordine. 

Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, questa Guida rapida richiede che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando. Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite. 

esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *eastus* percorso.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a>Crea macchina virtuale

toocreate una macchina virtuale (VM), utilizzare hello [creare vm az](/cli/azure/vm#create) comando. 

esempio Hello crea una macchina virtuale denominata `myVM`. Crea anche le chiavi SSH se non esistono già in una posizione predefinita. toouse uno specifico set di chiavi, utilizzare hello `--ssh-key-value` opzione.  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

Dopo aver creato una macchina virtuale hello, CLI di Azure consente di visualizzare informazioni toohello simile esempio seguente. Si noti il valore di hello per `publicIpAddress`. Utilizzare questo hello tooaccess indirizzo macchina virtuale.

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/{snip}/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="connect-toohello-vm"></a>Connettersi toohello VM

toocreate una sessione SSH con hello macchina virtuale, utilizzare hello comando seguente. Sostituire l'indirizzo IP hello con hello `publicIpAddress` valore per la macchina virtuale.

```bash 
ssh <publicIpAddress>
```

## <a name="create-hello-database"></a>Creare database hello

il software Oracle Hello è già installato in un'immagine del Marketplace hello. Creare un database di esempio come segue. 

1.  Passare toohello *oracle* utente avanzato, quindi inizializzare hello listener per la registrazione:

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    output di Hello è simile toohello seguenti:

    ```bash
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written too/u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting too(ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of hello LISTENER
    ------------------------
    Alias                     LISTENER
    Version                   TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Start Date                23-MAR-2017 15:32:08
    Uptime                    0 days 0 hr. 0 min. 0 sec
    Trace Level               off
    Security                  ON: Local OS Authentication
    SNMP                      OFF
    Listener Log File         /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening Endpoints Summary...
    (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))
    hello listener supports no services
    hello command completed successfully
    ```

2.  Crea database hello:

    ```bash
    dbca -silent \
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

    Accetta alcuni database di hello toocreate minuti.

3. Impostare le variabili Oracle

Prima di connettersi, è necessario tooset due variabili di ambiente: *ORACLE_HOME* e *ORACLE_SID*.

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
È anche possibile aggiungere ORACLE_HOME e ORACLE_SID file .bashrc toohello di variabili. Le variabili di ambiente hello futuri accessi salvati. Verificare i seguenti hello istruzioni sono state aggiunte toohello `~/.bashrc` file utilizzando l'editor di propria scelta.

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a>Connettività a Oracle EM Express

Strumento di gestione interfaccia utente grafica che è possibile utilizzare database hello tooexplore, configurare Oracle EM Express. tooconnect tooOracle EM Express, è necessario innanzitutto impostare porta hello in Oracle. 

1. La connessione a database tooyour sqlplus utilizzando:

    ```bash
    sqlplus / as sysdba
    ```

2. Una volta connessi, impostare la porta hello 5502 per Express EM

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. Contenitore hello aprire PDB1 se non è già aperto, ma prima controllare hello lo stato di:

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    output di Hello è simile toohello seguenti:

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. Se hello OPEN_MODE per `PDB1` non è di lettura e scrittura, quindi eseguire hello seguenti comandi tooopen PDB1:

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

È necessario tootype `quit` tooend hello sqlplus sessione e il tipo `exit` toologout dell'utente oracle hello.

## <a name="automate-database-startup-and-shutdown"></a>Automatizzare l'avvio e l'arresto del database

database Oracle Hello per impostazione predefinita non viene avviato automaticamente quando si riavvia hello macchina virtuale. tooset backup hello Oracle database toostart automaticamente, prima di tutto Accedi come radice. Quindi creare e aggiornare alcuni file di sistema.

1. Accedere come utente ROOT
    ```bash
    sudo su -
    ```

2.  Utilizzando l'editor preferito, modificare il file di hello `/etc/oratab` e modificare l'impostazione predefinita hello `N` troppo`Y`:

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  Creare un file denominato `/etc/init.d/dbora` e Incolla hello seguente contenuto:

    ```
    #!/bin/sh
    # chkconfig: 345 99 10
    # Description: Oracle auto start-stop script.
    #
    # Set ORA_HOME toobe equivalent too$ORACLE_HOME.
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle

    case "$1" in
    'start')
        # Start hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        # Remove "&" if you don't want startup as a background process.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" &
        touch /var/lock/subsys/dbora
        ;;

    'stop')
        # Stop hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" &
        rm -f /var/lock/subsys/dbora
        ;;
    esac
    ```

4.  Modificare le autorizzazioni nei file con *chmod* come segue:

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  Creare collegamenti simbolici per l'avvio e l'arresto come segue:

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  tootest le modifiche, riavviare hello VM:

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a>Aprire le porte per la connettività

attività finale Hello è tooconfigure alcuni endpoint esterno. tooset backup hello Azure gruppo di sicurezza di rete che protegge hello VM, terminare la sessione SSH in hello VM (deve avere stato espulso dalla SSH durante il riavvio nel passaggio precedente). 

1.  endpoint di hello tooopen che si utilizzi tooaccess hello Oracle database in modalità remota, creare una regola gruppo di sicurezza di rete con [creare una regola gruppo rete az](/cli/azure/network/nsg/rule#create) come indicato di seguito: 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  endpoint di hello tooopen utilizzare tooaccess Express EM Oracle in modalità remota, creare una regola gruppo di sicurezza di rete con [creare una regola gruppo rete az](/cli/azure/network/nsg/rule#create) come indicato di seguito:

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. Se è necessario ottenere l'indirizzo IP pubblico hello della macchina virtuale con [Mostra public-ip di rete az](/cli/azure/network/public-ip#show) come indicato di seguito:

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  Connettersi a EM Express dal browser. Verificare che il browser sia compatibile con EM Express. È necessario installare Flash. 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

È possibile accedere tramite hello **SYS** account e controllare hello **come sysdba** casella di controllo. Utilizzare password hello **OraPasswd1** che impostato durante l'installazione. 

![Schermata della pagina di accesso Oracle OEM Express hello](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a>Pulire le risorse

Dopo aver esplorazione di un database Oracle in Azure e hello VM non è più necessario, è possibile utilizzare hello [eliminazione gruppo az](/cli/azure/group#delete) comando gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Passaggi successivi

Informazioni su altre [soluzioni Oracle in Azure](oracle-considerations.md). 

Provare a hello [installazione e configurazione di gestione di archiviazione automatica di Oracle](configure-oracle-asm.md) esercitazione.
