---
title: aaaConfigure MPIO nell'host StorSimple Linux | Documenti Microsoft
description: Configurare MPIO nell'host di Linux tooa StorSimple connessi che eseguono 6.6 CentOS
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: tysonn
ms.assetid: ca289eed-12b7-4e2e-9117-adf7e2034f2f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: alkohli
ms.openlocfilehash: d9f7e02903243494c909313fb2c33ac690764274
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a>Configurare MPIO in un host di StorSimple che esegue CentOS
Questo articolo spiega hello passaggi necessari tooconfigure Multipath i/o (MPIO) sul server host Centos 6.6. server host Hello è dispositivo Microsoft Azure StorSimple tooyour connessi per la disponibilità elevata tramite gli iniziatori iSCSI. Vengono descritti in dettaglio hello l'individuazione automatica dei dispositivi a percorsi multipli e installazione specifiche di hello solo per i volumi StorSimple.

Questa procedura è applicabile tooall i modelli di hello di dispositivi della serie StorSimple 8000.

> [!NOTE]
> Questa procedura non può essere usata per un dispositivo virtuale StorSimple. Per ulteriori informazioni, vedere come tooconfigure ospitano server per il dispositivo virtuale.
> 
> 

## <a name="about-multipathing"></a>Informazioni sui percorsi multipli
Hello percorsi multipli consente tooconfigure più percorsi i/o tra un server host e un dispositivo di archiviazione. I percorsi I/O sono connessioni SAN fisiche che possono includere cavi, switch, interfacce di rete e controller separati. Percorsi multipli aggrega i percorsi i/o di hello, tooconfigure un nuovo dispositivo associato a tutti i percorsi di hello aggregato.

scopo di Hello di percorsi multipli è duplice:

* **Disponibilità elevata**: fornisce un percorso alternativo se qualsiasi elemento del percorso dei / o hello (ad esempio un cavo, switch, l'interfaccia di rete o controller) ha esito negativo.
* **Il bilanciamento del carico**: a seconda della configurazione di hello del dispositivo di archiviazione, è possibile migliorare le prestazioni di hello rilevando carichi nei percorsi di hello i/o e tali carichi il ribilanciamento in modo dinamico.

### <a name="about-multipathing-components"></a>Informazioni sui componenti dei percorsi multipli
I percorsi multipli in Linux sono costituiti da componenti kernel e spazio utente come elencato di seguito.

* **Kernel**: il componente principale di hello è hello *dispositivo mapper* che reindirizza i/o e supporta il failover per i percorsi e i gruppi di percorso.

* **Spazio utente**: si tratta di *multipath strumenti* che gestiscono i dispositivi con percorsi multipli, indicando modulo a percorsi multipli di hello dispositivo mapper quali toodo. strumenti di Hello è costituito da:
   
   * **Multipath**: elenca e configura i dispositivi a percorsi multipli.
   * **Multipathd**: daemon che esegue i percorsi di hello multipath e monitoraggi.
   * **Nome di Devmap**: offre un significativo tooudev nome del dispositivo per devmaps.
   * **Kpartx**: devmaps lineare toodevice partizioni toomake multipath mappe partizionabile viene eseguito il mapping.
   * **Multipath.conf**: file di configurazione per percorsi multipli daemon che è usato toooverwrite hello configurazione incorporati tabella.

### <a name="about-hello-multipathconf-configuration-file"></a>Sul file di configurazione multipath.conf hello
file di configurazione Hello `/etc/multipath.conf` vengono apportate diverse hello Multipath funzionalità configurabile dall'utente. Hello `multipath` comando e hello daemon kernel `multipathd` utilizzare informazioni contenute in questo file. file Hello viene consultato solo durante la configurazione di hello di dispositivi a percorsi multipli hello. Assicurarsi che tutte le modifiche vengono apportate prima di eseguire hello `multipath` comando. Se si modifica il file hello in seguito, sarà anche necessario toostop e avviare multipathd nuovamente per effetto di tootake modifiche hello.

Hello multipath.conf include cinque sezioni:

- **System level defaults***(defaults)*: è possibile ignorare i valori predefiniti a livello di sistema.
- **Disattivato dispositivi** *(nera)*: È possibile specificare hello elenco di dispositivi che non devono essere controllati da BizTalk mapper di dispositivo.
- **Disattivare le eccezioni** *(blacklist_exceptions)*: È possibile identificare considerati i dispositivi a percorsi multipli, anche se è elencato nella blacklist hello toobe di dispositivi specifici.
- **Impostazioni specifiche di controller di archiviazione** *(dispositivi)*: È possibile specificare le impostazioni di configurazione che verrà applicato toodevices che le informazioni di prodotto e fornitore.
- **Impostazioni specifiche di dispositivo** *(multipaths)*: È possibile utilizzare le impostazioni di configurazione hello toofine ottimizzare questa sezione per singoli LUN.

## <a name="configure-multipathing-on-storsimple-connected-toolinux-host"></a>Configurare percorsi multipli sull'host connesso tooLinux StorSimple
Un host di Linux tooa dispositivo connesso StorSimple può essere configurato per la disponibilità elevata e bilanciamento del carico. Ad esempio, se host Linux hello ha due interfacce toohello connesso SAN e hello dispositivo ha due interfacce connessi toohello SAN ad presenti queste interfacce hello stessa subnet, quindi esisterà 4 percorsi disponibili. Tuttavia, se ogni interfaccia di dati nell'interfaccia di dispositivi e host hello in un'altra subnet IP (e non instradabili), quindi solo 2 i percorsi saranno disponibili. È possibile configurare percorsi multipli tooautomatically individuare tutti i percorsi disponibili hello, scegliere un algoritmo di bilanciamento del carico per tali percorsi, applicare impostazioni di configurazione specifiche per i volumi StorSimple-only, abilitare e verificare i percorsi multipli.

Hello procedura riportata di seguito viene descritto come percorsi multipli tooconfigure quando un dispositivo StorSimple con due interfacce di rete viene connessa tooa host con due interfacce di rete.

## <a name="prerequisites"></a>Prerequisiti
Questa sezione descrive i prerequisiti di configurazione hello per server CentOS e il dispositivo StorSimple.

### <a name="on-centos-host"></a>Sull'host CentOS
1. Assicurarsi che l'host CentOS abbia due interfacce di rete abilitate. Digitare:
   
    `ifconfig`
   
    Hello riportato di seguito output di hello quando due interfacce di rete (`eth0` e `eth1`) sono presenti nell'host di hello.
   
        [root@centosSS ~]# ifconfig
        eth0  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:41  
          inet addr:10.126.162.65  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3341/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3341/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
         RX packets:36536 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6312 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:13994127 (13.3 MiB)  TX bytes:645654 (630.5 KiB)
   
        eth1  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:42  
          inet addr:10.126.162.66  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3342/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3342/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25962 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:2597350 (2.4 MiB)  TX bytes:754 (754.0 b)
   
        loLink encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:12 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:720 (720.0 b)  TX bytes:720 (720.0 b)
2. Installare *iSCSI-initiator-utils* sul server CentOS. Eseguire i seguenti passaggi tooinstall hello *utilità di iniziatore iSCSI*.
   
   1. Accedere come `root` all'host CentOS.
   2. Installare hello *utilità di iniziatore iSCSI*. Digitare:
      
       `yum install iscsi-initiator-utils`
   3. Dopo aver hello *utilità di iniziatore iSCSI* è stato installato, avviare il servizio iSCSI hello. Digitare:
      
       `service iscsid start`
      
       In alcuni casi, `iscsid` possono avviare e non è effettivamente hello `--force` opzione potrebbe essere necessaria.
   4. che l'iniziatore iSCSI è abilitato durante la fase di avvio, utilizzare hello tooensure `chkconfig` servizio hello tooenable di comando.
      
       `chkconfig iscsi on`
   5. tooverify che è stato corretto del programma di installazione, eseguire il comando di hello:
      
       `chkconfig --list | grep iscsi`
      
       Di seguito è riportato un output di esempio.
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       Da hello esempio precedente, si noterà che l'ambiente iSCSI verrà eseguito in fase di avvio su livelli fase 2, 3, 4 e 5.
3. Installare *device-mapper-multipath*. Digitare:
   
    `yum install device-mapper-multipath`
   
    verrà avviata l'installazione di Hello. Tipo **Y** toocontinue alla richiesta di conferma.

### <a name="on-storsimple-device"></a>Sul dispositivo StorSimple
Il dispositivo StorSimple deve avere:

* Almeno due interfacce abilitate per iSCSI. tooverify che due interfacce siano abilitate per iSCSI sul dispositivo StorSimple, eseguire hello nel portale di Azure classico per il dispositivo StorSimple hello come segue:
  
  1. Accedere al portale classico di hello per il dispositivo StorSimple.
  2. Selezionare il servizio StorSimple Manager, fare clic su **dispositivi** e scegliere il dispositivo StorSimple specifico di hello. Fare clic su **configura** e verificare le impostazioni dell'interfaccia di rete hello. Di seguito è riportata una schermata con due interfacce di rete abilitate per iSCSI. Entrambe le interfacce di rete da 10 GbE, DATA 2 e DATA 3, sono abilitate per iSCSI.
     
      ![Configurazione DATA 2 StorSimple MPIO](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![Configurazione DATA 3 StorSimple MPIO](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      In hello **configura** pagina
     
     1. Assicurarsi che entrambe le interfacce di rete siano abilitate per iSCSI. Hello **abilitato per iSCSI** campo deve essere impostato troppo**Sì**.
     2. Verificare che le interfacce di rete hello abbiano hello stessa velocità, entrambi devono essere da 1 GbE o 10 GbE.
     3. Si noti indirizzi IPv4 hello delle interfacce abilitate per iSCSI hello e salvare per un utilizzo successivo nell'host di hello.
* interfacce iSCSI Hello nel dispositivo StorSimple devono essere raggiungibile dal server CentOS hello.
      tooverify, gli indirizzi IP di hello tooprovide le interfacce di rete abilitate per iSCSI StorSimple è necessario nel server host. i comandi usati Hello e hello output corrispondente con DATA2 (10.126.162.25) e DATA3 (10.126.162.26) è illustrato di seguito:
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a>Configurazione hardware
È consigliabile connettersi hello due iSCSI interfacce di rete su percorsi diversi per la ridondanza. Hello seguente figura configurazione hardware consigliata hello per la disponibilità elevata e bilanciamento del carico percorsi multipli per il server di CentOS e un dispositivo StorSimple.

![Configurazione hardware di MPIO per StorSimple tooLinux host](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

Come illustrato nella figura precedente hello:

* Il dispositivo StorSimple ha una configurazione attiva-passiva con due controller.
* Due commutatori di rete SAN sono connessi tooyour controller del dispositivo.
* Due iniziatori iSCSI sono abilitati nel dispositivo StorSimple.
* Due interfacce di rete sono abilitate sull'host CentOS.

Se le interfacce di hello host e i dati siano instradabili, Hello sopra configurazione genererà 4 percorsi separati tra l'host del dispositivo e hello.

> [!IMPORTANT]
> * È consigliabile non combinare interfacce di rete da 1 GbE e da 10 GbE per i percorsi multipli. Quando si usano due interfacce di rete, entrambe le interfacce hello devono essere hello stesso tipo.
> * Sul dispositivo StorSimple, DATA0, DATA1, DATA4 e DATA5 sono interfacce da 1 GbE mentre DATA2 e DATA3 sono interfacce di rete da 10 GbE.|
> 
> 

## <a name="configuration-steps"></a>Procedura di configurazione
passaggi di configurazione Hello per percorsi multipli implicano i percorsi disponibili per l'individuazione automatica, specificare hello bilanciamento del carico algoritmo toouse, consentendo a percorsi multipli e infine verifica configurazione hello hello di configurazione. Ognuno di questi passaggi è illustrato in dettaglio nelle sezioni che seguono hello.

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a>Passaggio 1: Configurare percorsi multipli per il rilevamento automatico
i dispositivi supportati multipath Hello possono essere individuati automaticamente e configurati.

1. Inizializzare il file `/etc/multipath.conf` . Digitare:
   
     `mpathconf --enable`
   
    Hello sopra comando creerà un `sample/etc/multipath.conf` file.
2. Avviare il servizio a percorsi multipli. Digitare:
   
    `service multipathd start`
   
    Verrà visualizzato hello seguente output:
   
    `Starting multipathd daemon:`
3. Abilitare il rilevamento automatico dei percorsi multipli. Digitare:
   
    `mpathconf --find_multipaths y`
   
    Verrà modificato hello sezione Impostazioni predefinite del `multipath.conf` come illustrato di seguito:
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a>Passaggio 2: Configurare i percorsi multipli per volumi StorSimple
Per impostazione predefinita, tutti i dispositivi sono elencati nel file multipath.conf hello neri e verranno ignorati. È necessario toocreate blacklist eccezioni tooallow Multipath per volumi da dispositivi StorSimple.

1. Modifica hello `/etc/mulitpath.conf` file. Digitare:
   
    `vi /etc/multipath.conf`
2. Nella sezione hello blacklist_exceptions nel file multipath.conf hello. Il dispositivo StorSimple deve toobe elencato come eccezione blacklist in questa sezione. È possibile rimuovere il commento rilevanti righe toomodify questo file, come illustrato di seguito (utilizzare solo hello modello specifico di dispositivo hello in uso):
   
        blacklist_exceptions {
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8100*"
            }
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8600*"
            }
           }

### <a name="step-3-configure-round-robin-multipathing"></a>Passaggio 3: Configurare percorsi multipli round robin
Questo algoritmo di bilanciamento del carico utilizza tutti i controller attivo di hello toohello multipaths disponibile in modo bilanciato e round robin.

1. Modifica hello `/etc/multipath.conf` file. Digitare:
   
    `vi /etc/multipath.conf`
2. In hello `defaults` sezione, hello set `path_grouping_policy` troppo`multibus`. Hello `path_grouping_policy` multipaths toounspecified hello predefinito percorso raggruppamento criteri tooapply specifica. sezione Impostazioni predefinite di Hello apparirà come illustrato di seguito.
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> valori più comuni di Hello `path_grouping_policy` includono:
> 
> * failover = 1 percorso per ogni gruppo prioritario
> * multibus = tutti i percorsi validi in 1 gruppo prioritario
> 
> 

### <a name="step-4-enable-multipathing"></a>Passaggio 4: Abilitare i percorsi multipli
1. Riavviare hello `multipathd` daemon. Digitare:
   
    `service multipathd restart`
2. output di Hello saranno come indicato di seguito:
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a>Passaggio 5: Verificare i percorsi multipli
1. Assicurarsi innanzitutto che viene stabilita la connessione iSCSI con dispositivo StorSimple hello come indicato di seguito:
   
   a. Trovare il dispositivo StorSimple. Digitare:
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on hello device>:<iSCSI port on StorSimple device>
    ```
    
    output di Hello quando l'indirizzo IP DATA0 è 10.126.162.25 e porta 3260 viene aperta nel dispositivo StorSimple hello per il traffico in uscita iSCSI è come illustrato di seguito:
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    Hello Copia nome IQN del dispositivo StorSimple `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, da hello output precedente.

   b. Collegare il dispositivo di toohello tramite iSCSI di destinazione. dispositivo StorSimple Hello è una destinazione iSCSI di hello qui. Digitare:

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    Hello esempio seguente viene illustrato l'output con una nome qualificato iSCSI di destinazione di `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`. output di Hello indica che sono stati connessi toohello due interfacce di rete abilitate per iSCSI sul dispositivo.

    ```
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    Se viene visualizzato un solo host interfaccia e i due percorsi, è necessario tooenable entrambe le interfacce hello nell'host per iSCSI. È possibile seguire hello [dettagliate nella documentazione di Linux](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).

2. Server CentOS toohello esposto dal dispositivo StorSimple hello è un volume. Per ulteriori informazioni, vedere [passaggio 6: creare un volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) tramite hello portale di Azure classico nel dispositivo StorSimple.

3. Verificare i percorsi disponibili hello. Digitare:

      ```
      multipath –l
      ```

      Hello di esempio seguente viene illustrato l'output di hello per le due interfacce di rete su un'interfaccia di rete StorSimple dispositivo connesso tooa singolo host con due percorsi disponibili.

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        hello following example shows hello output for two network interfaces on a StorSimple device connected tootwo host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After hello paths are configured, refer toohello specific instructions on your host operating system (Centos 6.6) toomount and format this volume.

## <a name="troubleshoot-multipathing"></a>Risoluzione dei problemi relativi ai percorsi multipli
Questa sezione contiene alcuni suggerimenti utili in caso di problemi durante la configurazione dei percorsi multipli.

D: Non vengono visualizzati le modifiche di hello in `multipath.conf` file diventino effettive.

R. Se sono state apportate toohello eventuali modifiche `multipath.conf` file, sarà necessario del servizio di toorestart hello percorsi multipli. Digitare hello comando seguente:

    service multipathd restart

D: È stata attivata due interfacce di rete nel dispositivo StorSimple hello e due interfacce di rete sull'host hello. Quando elencano i percorsi disponibili hello, viene visualizzato solo due percorsi. Previsto toosee quattro percorsi disponibili.

R. Assicurarsi che siano percorsi hello due su hello stessa subnet e instradabile. Se sono interfacce di rete hello su VLAN diversi e non è instradabile, verrà visualizzato solo due percorsi. Unidirezionale tooverify equivale toomake assicurarsi che entrambe le interfacce host hello da un'interfaccia di rete nel dispositivo StorSimple hello può raggiungere. È necessario troppo[contattare il supporto Microsoft](storsimple-contact-microsoft-support.md) come questa verifica può essere eseguita solo tramite una sessione di supporto.

D: Nell'elenco dei percorsi disponibili non è visualizzato alcun output.

R. In genere, non possono visualizzare tutti i percorsi con percorsi multipli suggerisce un problema con il daemon di percorsi multipli hello ed è probabile che qualsiasi problema risiede nella hello `multipath.conf` file.

Sarebbe inoltre controllare che è possibile visualizzare alcuni dischi dopo la connessione di destinazione, toohello come alcuna risposta da elenchi di percorsi multipli hello non potrebbe inoltre risultare che non includa alcun disco.

* Utilizzare hello bus SCSI hello toorescan di comando seguente:
  
    `$ rescan-scsi-bus.sh `(parte del pacchetto sg3_utils)
* Digitare hello seguenti comandi:
  
    `$ dmesg | grep sd*`
     
     Or
  
    `$ fdisk –l`
  
    Verranno restituite informazioni dettagliate sui dischi aggiunti di recente.
* Se si tratta di un disco di StorSimple, toodetermine utilizzare hello seguenti comandi:
  
    `cat /sys/block/<DISK>/device/model`
  
    Verrà restituita una stringa, che determinerà se si tratta di un disco StorSimple.

Una causa meno probabile, ma possibile, potrebbe anche essere un PID iSCSI non aggiornato. Utilizzare hello successivo comando toolog off da sessioni iSCSI hello:

    iscsiadm -m node --logout -p <Target_IP>

Ripetere questo comando per tutte le interfacce di rete connessa hello in destinazione iSCSI hello, che è il dispositivo StorSimple. Dopo aver eseguito l'accesso da tutte le sessioni iSCSI di hello, utilizzare una sessione iSCSI hello iSCSI destinazione IQN tooreestablish hello. Digitare hello comando seguente:

    iscsiadm -m node --login -T <TARGET_IQN>


D: Come è possibile verificare che il dispositivo sia incluso nell'elenco dei dispositivi consentiti?

R. Se il dispositivo è abilitata, tooverify utilizzare hello comando interattivo sulla risoluzione dei problemi seguente:

    multipathd –k
    multipathd> show devices
    available block devices:
    ram0 devnode blacklisted, unmonitored
    ram1 devnode blacklisted, unmonitored
    ram2 devnode blacklisted, unmonitored
    ram3 devnode blacklisted, unmonitored
    ram4 devnode blacklisted, unmonitored
    ram5 devnode blacklisted, unmonitored
    ram6 devnode blacklisted, unmonitored
    ram7 devnode blacklisted, unmonitored
    ram8 devnode blacklisted, unmonitored
    ram9 devnode blacklisted, unmonitored
    ram10 devnode blacklisted, unmonitored
    ram11 devnode blacklisted, unmonitored
    ram12 devnode blacklisted, unmonitored
    ram13 devnode blacklisted, unmonitored
    ram14 devnode blacklisted, unmonitored
    ram15 devnode blacklisted, unmonitored
    loop0 devnode blacklisted, unmonitored
    loop1 devnode blacklisted, unmonitored
    loop2 devnode blacklisted, unmonitored
    loop3 devnode blacklisted, unmonitored
    loop4 devnode blacklisted, unmonitored
    loop5 devnode blacklisted, unmonitored
    loop6 devnode blacklisted, unmonitored
    loop7 devnode blacklisted, unmonitored
    sr0 devnode blacklisted, unmonitored
    sda devnode whitelisted, monitored
    dm-0 devnode blacklisted, unmonitored
    dm-1 devnode blacklisted, unmonitored
    dm-2 devnode blacklisted, unmonitored
    sdb devnode whitelisted, monitored
    sdc devnode whitelisted, monitored
    dm-3 devnode blacklisted, unmonitored


Per ulteriori informazioni, visitare troppo[utilizzare risoluzione dei problemi di un comando interattivo per percorsi multipli](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).

## <a name="list-of-useful-commands"></a>Elenco di comandi utili
| Digitare  | Comando | Descrizione |
| --- | --- | --- |
| **iSCSI** |`service iscsid start` |Avviare il servizio iSCSI |
| &nbsp; |`service iscsid stop` |Arrestare il servizio iSCSI |
| &nbsp; |`service iscsid restart` |Riavviare il servizio iSCSI |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |Individuare le destinazioni disponibili in hello specificato indirizzo |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |Accedere alla destinazione iSCSI toohello |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |Disconnettersi dalla destinazione iSCSI hello |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |Stampare il nome dell'iniziatore iSCSI |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |Controllare lo stato di hello di sessione iSCSI hello e volume individuato nell'host di hello |
| &nbsp; |`iscsi –m session` |Mostra tutte le sessioni iSCSI hello stabilite tra host hello e il dispositivo StorSimple hello |
|  | | |
| **Percorsi multipli** |`service multipathd start` |Avviare il daemon a percorsi multipli |
| &nbsp; |`service multipathd stop` |Arrestare il daemon a percorsi multipli |
| &nbsp; |`service multipathd restart` |Riavviare il daemon a percorsi multipli |
| &nbsp; |`chkconfig multipathd on` </br> OPPURE </br> `mpathconf –with_chkconfig y` |Abilitare toostart daemon a percorsi multipli in fase di avvio |
| &nbsp; |`multipathd –k` |Avviare la console interattiva di hello per la risoluzione dei problemi |
| &nbsp; |`multipath –l` |Elencare le connessioni e i dispositivi a percorsi multipli |
| &nbsp; |`mpathconf --enable` |Creare un file mulitpath.conf di esempio in `/etc/mulitpath.conf` |
|  | | |

## <a name="next-steps"></a>Passaggi successivi
Come si configura MPIO nell'host di Linux, è necessario anche toohello toorefer CentoS 6.6 documenti seguenti:

* [Configurazione di MPIO su CentOS](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [Guida alla formazione Linux](http://linux-training.be/files/books/LinuxAdm.pdf)

