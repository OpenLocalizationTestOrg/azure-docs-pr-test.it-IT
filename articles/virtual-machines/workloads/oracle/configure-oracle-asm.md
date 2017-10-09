---
title: aaaSet di Oracle ASM in una macchina virtuale Linux di Azure | Documenti Microsoft
description: Attivare e mettere in funzione rapidamente Oracle ASM nell'ambiente Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/19/2017
ms.author: rclaus
ms.openlocfilehash: d6a7046638e919876477d46943faabcb1872acac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a>Configurare Oracle ASM su una macchina virtuale Linux in Azure  

Le macchine virtuali di Azure offrono un ambiente di elaborazione completamente configurabile e flessibile. In questa esercitazione vengono illustrate la distribuzione di macchina virtuale di Azure basic combinata con hello installazione e configurazione di Oracle automatizzata Storage Management (ASM).  Si apprenderà come:

> [!div class="checklist"]
> * Creare e connettersi a Oracle Database VM tooan
> * Installare e configurare Oracle Automated Storage Management
> * Installare e configurare l'infrastruttura di Oracle Grid
> * Inizializzare l'installazione di Oracle ASM
> * Creare un database Oracle gestito da ASM


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="prepare-hello-environment"></a>Preparare l'ambiente hello

### <a name="create-a-resource-group"></a>Creare un gruppo di risorse

toocreate un gruppo di risorse, utilizzare hello [gruppo az creare](/cli/azure/group#create) comando. Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite. In questo esempio, un gruppo di risorse denominato *myResourceGroup* in hello *eastus* area.

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a>Creare una macchina virtuale

toocreate una macchina virtuale basata sull'immagine di Oracle Database hello e configurarlo toouse Oracle ASM, usare hello [creare vm az](/cli/azure/vm#create) comando. 

Hello seguente viene creata una macchina virtuale denominata myVM che è una dimensione Standard_DS2_v2 con quattro dischi dati collegati di 50 GB. Se non esistono già nel percorso della chiave predefinita hello, crea anche le chiavi SSH.  toouse uno specifico set di chiavi, utilizzare hello `--ssh-key-value` opzione.  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

Dopo aver creato una macchina virtuale hello, CLI di Azure consente di visualizzare informazioni toohello simile esempio seguente. Si noti il valore di hello per `publicIpAddress`. Utilizzare questo hello tooaccess indirizzo macchina virtuale.

   ```azurecli
   {
     "fqdns": "",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
     "location": "eastus",
     "macAddress": "00-0D-3A-36-2F-56",
     "powerState": "VM running",
     "privateIpAddress": "10.0.0.4",
     "publicIpAddress": "13.64.104.241",
     "resourceGroup": "myResourceGroup"
   }
   ```

### <a name="connect-toohello-vm"></a>Connettersi toohello VM

toocreate una sessione SSH con hello VM e configurare impostazioni aggiuntive, usare hello comando seguente. Sostituire l'indirizzo IP hello con hello `publicIpAddress` valore per la macchina virtuale.

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a>Installare Oracle ASM

tooinstall Oracle ASM, hello completo alla procedura seguente. 

Per altre informazioni sull'installazione di Oracle ASM, vedere [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html) (Download di Oracle ASMLib per Oracle Linux 6).  

1. È necessario toologin come radice in ordine toocontinue con installazione ASM:

   ```bash
   sudo su -
   ```
   
2. Eseguire questi comandi aggiuntivi componenti Oracle ASM tooinstall:

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. Verificare che Oracle ASM sia installato:

   ```bash
   rpm -qa |grep oracleasm
   ```

    output di Hello di questo comando deve includere hello seguenti componenti:

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. ASM richiede specifici utenti e ruoli in ordine toofunction correttamente. Hello seguenti comandi di Crea gruppi e account utente prerequisito hello: 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. Verificare che utenti e gruppi siano stati creati correttamente:

   ```bash
   id grid
   ```

    Hello output di questo comando deve includere seguente hello utenti e gruppi:

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. Creare una cartella per l'utente *griglia* e modificare il proprietario di hello:

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a>Configurare Oracle ASM

Per questa esercitazione, è l'utente predefinito hello *griglia* e il gruppo predefinito hello è *asmadmin*. Verificare che hello *oracle* l'utente faccia parte del gruppo asmadmin hello. tooset installazione Oracle ASM, hello completo alla procedura seguente:

1. Impostazione dei driver di hello Oracle ASM libreria include la definizione utente predefinito hello (griglia) e il gruppo predefinito (asmadmin) nonché configurazione toostart unità hello all'avvio del sistema (selezione y) e tooscan per i dischi di avvio (selezione y). È necessario tooanswer hello richieste da hello comando seguente:

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   output di Hello di questo comando dovrebbe essere simile toohello seguente, l'arresto con richieste toobe ha risposto.

    ```bash
   Configuring hello Oracle ASM library driver.

   This will configure hello on-boot properties of hello Oracle ASM library
   driver. hello following questions will determine whether hello driver is
   loaded on boot and what permissions it will have. hello current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user tooown hello driver interface []: grid
   Default group tooown hello driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. Configurazione del disco Visualizza hello:
   ```bash
   cat /proc/partitions
   ```

   output di Hello di questo comando dovrebbe essere simile toohello seguente elenco di dischi disponibili

   ```bash
   8       16   14680064 sdb
   8       17   14678976 sdb1
   8        0   52428800 sda
   8        1     512000 sda1
   8        2   51915776 sda2
   8       48   52428800 sdd
   8       64   52428800 sde
   8       80   52428800 sdf
   8       32   52428800 sdc
   11       0       1152 sr0
   ```

3. Formattare il disco *dev/sdc* eseguendo hello comando seguente e rispondere alle hello prompt con:
   - *n* per una nuova partizione
   - *p* per una partizione primaria
   - *1* partizione prima di hello tooselect
   - Premere `enter` per primo cilindro di hello predefinito
   - Premere `enter` per ultimo cilindro di hello predefinito
   - Premere *w* tabella di partizione toohello toowrite hello modifiche  

   ```bash
   fdisk /dev/sdc
   ```
   
   Utilizza le risposte hello riportate sopra, output di hello per comando fdisk hello dovrebbe essere simile hello seguenti:

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide toowrite them.
   After that, of course, hello previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   hello device presents a logical sector size that is smaller than
   hello physical sector size. Aligning tooa physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off hello mode (command 'c') and change display units to
           sectors (command 'u').

   Command (m for help): n
   Command action
     e   extended
     p   primary partition (1-4)
   p
   Partition number (1-4): 1
   First cylinder (1-6527, default 1):
   Using default value 1
   Last cylinder, +cylinders or +size{K,M,G} (1-6527, default 6527):
   Using default value 6527

   Command (m for help): w
   hello partition table has been altered!

   Calling ioctl() toore-read partition table.
   Syncing disks.
   ```

4. Ripetizione hello precedente comando fdisk per `/dev/sdd`, `/dev/sde`, e `/dev/sdf`.

5. Controllare la configurazione disco hello:

   ```bash
   cat /proc/partitions
   ```

   output di Hello del comando hello dovrebbe essere simile hello seguente:

   ```bash
   major minor  #blocks  name

     8       16   14680064 sdb
     8       17   14678976 sdb1
     8       32   52428800 sdc
     8       33   52428096 sdc1
     8       48   52428800 sdd
     8       49   52428096 sdd1
     8       64   52428800 sde
     8       65   52428096 sde1
     8       80   52428800 sdf
     8       81   52428096 sdf1
     8        0   52428800 sda
     8        1     512000 sda1
     8        2   51915776 sda2
     11       0    1048575 sr0
   ```

6. Controllare lo stato del servizio Oracle ASM hello e avviare il servizio Oracle ASM hello:

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   output di Hello del comando hello dovrebbe essere simile hello seguente:
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing hello Oracle ASMLib driver:                     [  OK  ]
   Scanning hello system for Oracle ASMLib disks:               [  OK  ]
   ```

7. Creare dischi Oracle ASM:

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   output di Hello del comando hello dovrebbe essere simile hello seguente:

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. Elencare i dischi Oracle ASM:

   ```bash
   service oracleasm listdisks
   ```   

   output di Hello del comando hello deve includere off hello dischi ASM Oracle seguenti:

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. Modificare le password hello per gli utenti di radice, oracle e griglia hello. **Prendere nota di queste nuove password** come vengano utilizzati in un secondo momento durante l'installazione di hello.

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. Modificare le autorizzazioni di cartella hello:

   ```bash
   chmod -R 775 /opt 
   chown grid:oinstall /opt 
   chown oracle:oinstall /dev/sdc1 
   chown oracle:oinstall /dev/sdd1 
   chown oracle:oinstall /dev/sde1 
   chown oracle:oinstall /dev/sdf1 
   chmod 600 /dev/sdc1 
   chmod 600 /dev/sdd1 
   chmod 600 /dev/sde1 
   chmod 600 /dev/sdf1
   ```

## <a name="download-and-prepare-oracle-grid-infrastructure"></a>Scaricare e preparare Oracle Grid Infrastructure

toodownload e preparare il software Oracle griglia infrastruttura hello, hello completo alla procedura seguente:

1. Scaricare l'infrastruttura di griglia di Oracle da hello [pagina di download di Oracle ASM](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html). 

   Nell'area download di hello intitolato **Oracle Database 12C versione 1 griglia infrastruttura (12.1.0.2.0) per Linux x86-64**, scaricare i file con estensione zip hello due.

2. Dopo aver scaricato hello ZIP file tooyour client computer, è possibile utilizzare il protocollo Secure di copia (SCP) toocopy hello file tooyour VM:

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. SSH nuovamente la macchina virtuale di Oracle in Azure in file con estensione zip ordine toomove hello in hello /OPT cartella. Quindi, modificare il proprietario di hello del file hello:

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. Decomprimere i file hello. (Installazione hello Linux decomprimere strumento se non è già installato)
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. Modificare l'autorizzazione:
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. Aggiornare lo spazio di swapping configurato. Componenti di una griglia Oracle è necessario almeno 6,8 GB di spazio di swapping tooinstall griglia. dimensioni file di scambio Hello predefinite per le immagini di Oracle Linux in Azure sono solo a 2048MB. È necessario tooincrease `ResourceDisk.SwapSizeMB` in hello `/etc/waagent.conf` riavviare servizio WALinuxAgent hello per effetto di tootake hello aggiornata le impostazioni e dei file. Poiché si tratta di un file di sola lettura, è necessario l'accesso in scrittura tooenable autorizzazioni file toochange.

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   Cercare `ResourceDisk.SwapSizeMB` e modificare il valore di hello troppo**8192**. Sarà necessario toopress `insert` tooenter modalità di inserimento, tipo di valore hello **8192** e quindi premere `esc` tooreturn toocommand modalità. le modifiche di hello toowrite e file hello quit, digitare `:wq` e premere `enter`.
   
   > [!NOTE]
   > È consigliabile utilizzare sempre `WALinuxAgent` tooconfigure spazio di swapping in modo che viene sempre creato hello temporaneo disco locale (disco temporaneo) per ottenere prestazioni ottimali. Per ulteriori informazioni, vedere [come tooadd uno scambio di file in macchine virtuali Linux Azure](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).

## <a name="prepare-your-local-client-and-vm-toorun-x11"></a>Preparare il client locale e VM toorun x11
La configurazione di Oracle ASM richiede un'interfaccia grafica toocomplete hello installazione e configurazione. Usiamo hello x11 protocollo toofacilitate questa installazione. Se si utilizza un sistema client (Mac o Linux) che dispone già di X11 funzionalità abilitato e configurato, è possibile ignorare questa configurazione e tooWindows esclusivo macchine del programma di installazione. 

1. [Scaricare PuTTY](http://www.putty.org/) e [scaricare Xming](https://xming.en.softonic.com/) tooyour computer di Windows. Installazione di hello toocomplete di entrambe le applicazioni con i valori predefiniti di hello prima di procedere sarà necessario.

2. Dopo aver installato PuTTY, aprire un prompt dei comandi, modificare in hello PuTTY cartella (ad esempio, c:\Programmi\Microsoft Files\PuTTY) ed eseguire `puttygen.exe` in ordine toogenerate una chiave.

3. Nel generatore di chiavi PuTTY:
   
   1. Generare una chiave selezionando hello `Generate` pulsante.
   2. Copiare il contenuto di hello della chiave di hello (Ctrl + C).
   3. Seleziona hello `Save private key` pulsante.
   4. Ignorare l'avviso hello sulla protezione chiave hello con una passphrase e quindi selezionare `OK`.

   ![Screenshot del generatore di chiavi PuTTY](./media/oracle-asm/puttykeygen.png)

4. Nella macchina virtuale eseguire questi comandi:

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. Creare un file denominato `authorized_keys`. Incollare il contenuto di hello della chiave di hello in questo file e quindi salvare il file hello.

   > [!NOTE]
   > chiave di Hello deve contenere la stringa hello `ssh-rsa`. Inoltre, il contenuto di hello della chiave hello deve essere una singola riga di testo.
   >  

6. Nel sistema client, avviare PuTTY. In hello **categoria** riquadro andare troppo**connessione** > **SSH** > **Auth**. In hello **file di chiave privata per l'autenticazione** passare toohello chiave generata in precedenza.

   ![Schermata delle opzioni di autenticazione SSH hello](./media/oracle-asm/setprivatekey.png)

7. In hello **categoria** riquadro andare troppo**connessione** > **SSH** > **X11**. Seleziona hello **inoltro X11 Enable** casella di controllo.

   ![Schermata di hello SSH X11 opzioni di inoltro](./media/oracle-asm/enablex11.png)

8. In hello **categoria** riquadro andare troppo**sessione**. Immettere la macchina virtuale ASM Oracle `<publicIPaddress>` nella hello host Nome finestra di dialogo, inserire un nuovo `Saved Session` nome e quindi fare clic su `Save`.  Dopo il salvataggio, fare clic su `open` macchina virtuale di Oracle ASM tooyour tooconnect.  Hello prima connessione è un avviso nel Registro di sistema non è stato memorizzato nella cache sistema remoto hello. Fare clic su `yes` tooadd e continuare.

   ![Schermata delle opzioni di sessione PuTTY hello](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a>Installare Oracle Grid Infrastructure

tooinstall Oracle griglia infrastruttura, hello completo alla procedura seguente:

1. Accedere come utente **grid**. (Deve essere in grado di toosign in senza che venga richiesta una password.) 

   > [!NOTE]
   > Se si esegue Windows, assicurarsi di che aver avviato Xming prima di iniziare l'installazione di hello.

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   Verrà visualizzata la finestra Oracle Grid Infrastructure 12c Release 1 Installer (Programma di installazione di Oracle Grid Infrastructure 12c versione 1). (Potrebbe richiedere alcuni minuti per hello installer toostart).

2. In hello **seleziona un'opzione di installazione** selezionare **installare e configurare Oracle griglia infrastruttura per un Server autonomo**.

   ![Schermata della pagina Selezionare opzione di installazione del programma di installazione di hello](./media/oracle-asm/install01.png)

3. In hello **selezionare lingue prodotto** assicurarsi **inglese** o lingua hello desiderata è selezionata.  Fare clic su `next`.

4. In hello **Crea gruppo di dischi ASM** pagina:
   - Immettere un nome per il gruppo di dischi hello.
   - In **Redundancy** (Ridondanza) selezionare **External** (Esterna).
   - In **Allocation Unit Size** (Dimensioni dell'unità di allocazione) selezionare **4**.
   - In **Add Disks** (Aggiungi dischi) selezionare **ORCLASMSP**.
   - Fare clic su `next`.

5. In hello **specificare Password ASM** pagina, seleziona hello **utilizzare stessa password per questi account** opzione e immettere una password.

   ![Schermata della pagina specificare Password ASM del programma di installazione di hello](./media/oracle-asm/install04.png)

6. In hello **specificare opzioni di gestione** pagina, si dispone di hello opzione tooconfigure controllo Cloud EM. Questa opzione verrà ignorato: fare clic su `next` toocontinue. 

7. In hello **gruppi con privilegi di sistema operativo** pagina, utilizzare le impostazioni predefinite di hello. Fare clic su `next` toocontinue.

8. In hello **percorso di installazione specificare** pagina, utilizzare le impostazioni predefinite di hello. Fare clic su `next` toocontinue.

9. In hello **crea** pagina, modificare hello inventario Directory troppo`/u01/app/grid/oraInventory`. Fare clic su `next` toocontinue.

   ![Schermata della pagina di creare l'inventario del programma di installazione di hello](./media/oracle-asm/install08.png)

10. In hello **configurazione di esecuzione di script radice** pagina, seleziona hello **automaticamente di eseguire gli script di configurazione** casella di controllo. Selezionare quindi hello **vengono usate le credenziali utente "root"** opzione e immettere una password dell'utente root hello.

    ![Schermata radice script esecuzione del programma di installazione di hello pagina di configurazione](./media/oracle-asm/install09.png)

11. In hello **eseguire controlli dei prerequisiti** pagina installazione corrente di hello avrà esito negativo con errori. Si tratta di un comportamento previsto. Selezionare `Fix & Check Again`.

12. In hello **Script correzione** la finestra di dialogo, fare clic su `OK`.

13. In hello **riepilogo** pagina, rivedere le impostazioni selezionate e quindi fare clic su `Install`.

    ![Schermata della pagina di riepilogo dell'installazione guidata di hello](./media/oracle-asm/install12.png)

14. Una finestra di dialogo di avviso viene visualizzato per informare gli script di configurazione di è necessario toobe eseguito come utente con privilegi. Fare clic su `Yes` toocontinue.

15. In hello **fine** pagina, fare clic su `Close` installazione hello toofinish.

## <a name="set-up-your-oracle-asm-installation"></a>Configurare l'installazione di Oracle ASM

tooset installazione Oracle ASM, hello completo alla procedura seguente:

1. Verificare che si è ancora connessi come **grid** dalla sessione X11. Potrebbe essere necessario toohit `enter` toorevive hello terminal. Avviare quindi hello Oracle automatizzata Storage Management Configuration Assistant:

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   Verrà visualizzato ASM Configuration Assistant (Assistente alla configurazione di ASM).

2. In hello **configurare ASM: gruppi di dischi** finestra di dialogo fare clic su hello `Create` pulsante e quindi fare clic su `Show Advanced Options`.

3. In hello **Crea gruppo di dischi** la finestra di dialogo:

   - Immettere il nome del gruppo disco hello **dati**.
   - In **Select Member Disks** (Selezionare i dischi membri) selezionare **ORCL_DATA** e **ORCL_DATA1**.
   - In **Allocation Unit Size** (Dimensioni dell'unità di allocazione) selezionare **4**.
   - Fare clic su `ok` toocreate il gruppo di dischi hello.
   - Fare clic su `ok` tooclose finestra di conferma hello.

   ![Schermata della finestra di dialogo Crea gruppo di dischi hello](./media/oracle-asm/asm02.png)

4. In hello **configurare ASM: gruppi di dischi** finestra di dialogo fare clic su hello `Create` pulsante e quindi fare clic su `Show Advanced Options`.

5. In hello **Crea gruppo di dischi** la finestra di dialogo:

   - Immettere il nome del gruppo disco hello **francese**.
   - In **Redundancy** (Ridondanza) selezionare **External (none)** (Esterna (nessuna)).
   - In **Select Member Disks** (Selezionare i dischi membri) selezionare **ORCL_DATA**.
   - In **Allocation Unit Size** (Dimensioni dell'unità di allocazione) selezionare **4**.
   - Fare clic su `ok` toocreate il gruppo di dischi hello.
   - Fare clic su `ok` tooclose finestra di conferma hello.

   ![Schermata della finestra di dialogo Crea gruppo di dischi hello](./media/oracle-asm/asm04.png)

6. Selezionare **uscita** tooclose ASM Configuration Assistant.

   ![Schermata di hello configurare ASM: la finestra di dialogo di gruppi di dischi con il pulsante di uscita](./media/oracle-asm/asm05.png)

## <a name="create-hello-database"></a>Creare database hello

Hello software per database Oracle è già installato nell'immagine di Azure Marketplace hello. toocreate un database, hello completo alla procedura seguente:

1. Passare come superuser Oracle toohello di utenti e quindi inizializzare listener di hello per la registrazione:

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   Si apre Configuration Assistant (Assistente alla configurazione).

2. In hello **operazione sul Database** pagina, fare clic su `Create Database`.

3. In hello **la modalità di creazione** pagina:

   - Immettere un nome per il database di hello.
   - Per **Storage Type** (tipo di archiviazione) assicurarsi che **Automatic Storage Management (ASM)** (Gestione archiviazione automatica, ASM) sia selezionato.
   - Per **percorso file di Database**, utilizzare hello predefinito ASM suggerito percorso.
   - Per **rapida Area ripristino**, utilizzare hello predefinito ASM suggerito percorso.
   - Digitare una **Password amministratore** e **confermare la password**.
   - Verificare che `create as container database` sia selezionato.
   - Digitare un valore `pluggable database name`.

4. In hello **riepilogo** pagina, rivedere le impostazioni selezionate e quindi fare clic su `Finish` database hello toocreate.

   ![Schermata della pagina di riepilogo hello](./media/oracle-asm/createdb03.png)

5. Hello Database è stato creato. In hello **fine** sono disponibili hello opzione toounlock altri account toouse questo database e modificare le password hello. Se si desidera toodo scopo, selezionare **la gestione delle Password** -in caso contrario, fare clic su `close`.

## <a name="delete-hello-vm"></a>Eliminare hello VM

È stata configurata correttamente Gestione archiviazione automatica Oracle sull'immagine di Oracle DB hello da hello Azure Marketplace.  Quando non è più necessario questa macchina virtuale, è possibile utilizzare hello seguente gruppo di risorse di comando tooremove hello, macchina virtuale e tutte le relative risorse:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Passaggi successivi

[Esercitazione: Configurare Oracle DataGuard](configure-oracle-dataguard.md)

[Esercitazione: Configurare Oracle GoldenGate](Configure-oracle-golden-gate.md)

Revisione: [Definire l'architettura di un database Oracle](oracle-design.md)
