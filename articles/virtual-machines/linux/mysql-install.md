---
title: aaaSet di MySQL in una VM Linux di Azure | Documenti Microsoft
description: Informazioni su come tooinstall hello MySQL stack di chiamate su una macchina virtuale Linux (RedHat o Ubuntu famiglia del sistema operativo) in Azure
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 153bae7c-897b-46b3-bd86-192a6efb94fa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: e47d0de7f0eb5bb873ad20e4bc35f1b5f8d33bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-mysql-on-azure"></a>Come tooinstall MySQL in Azure
In questo articolo si apprenderà come tooinstall e configurare MySQL in una macchina virtuale di Azure che eseguono Linux.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a>Installare MySQL nella macchina virtuale.
> [!NOTE]
> È necessario disporre già una macchina virtuale di Microsoft Azure che eseguono Linux in ordine toocomplete questa esercitazione. Vedere il [esercitazione VM Linux di Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate e impostare una VM Linux con `mysqlnode` come nome della macchina virtuale hello e `azureuser` come utente prima di procedere.
> 
> 

In questo caso, è possibile utilizzare 3306 porta come porta MySQL hello.  

Connettersi toohello VM Linux è stato creato tramite putty. Se si tratta hello prima volta che si usa una macchina virtuale Linux di Azure, vedere la modalità di connessione tooa VM Linux toouse putty [qui](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

In questo articolo, ad esempio, si utilizzerà repository pacchetto tooinstall MySQL5.6. In realtà, MySQL5.6 presenta maggiori miglioramenti in termini di prestazioni rispetto a MySQL5.5.  Ulteriori informazioni sono disponibili [qui](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).

### <a name="how-tooinstall-mysql56-on-ubuntu"></a>Come tooinstall MySQL5.6 in Ubuntu
Di seguito si utilizzerà una VM Linux con Ubuntu da Azure.

* Passaggio 1: Installare il Server di MySQL 5.6 passare troppo`root` utente:
  
            #[azureuser@mysqlnode:~]sudo su -
  
    Installare mysql-server 5.6:
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    Durante l'installazione, verrà visualizzato un poping finestra di dialogo backup tooask si tooset MySQL radice la password ed è necessario impostare password hello qui.
  
    ![immagine](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    Password hello input tooconfirm nuovamente.

    ![immagine](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* Passaggio 2: Accedere al server MySQL
  
    Al termine dell'installazione del server MySQL, il servizio MySQL verrà avviato automaticamente. È possibile accedere al server MySQL con l’utente `root` .
    Utilizzare hello seguito password toologin e input di comando.
  
             #[root@mysqlnode ~]# mysql -uroot -p
* Passaggio 3: Gestire hello in esecuzione il servizio MySQL
  
    (a) Ottenere lo stato del servizio MySQL
  
             #[root@mysqlnode ~]# service mysql status
  
    (b) Avviare il servizio MySQL
  
             #[root@mysqlnode ~]# service mysql start
  
    (c) Interrompere il servizio MySQL
  
             #[root@mysqlnode ~]# service mysql stop
  
    (d) riavviare il servizio di MySQL hello
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-tooinstall-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a>Aspetto tooinstall MySQL nella famiglia di sistemi operativi di Red Hat per CentOS, Oracle Linux
In questo caso si utilizzerà la VM Linux con CentOS oppure Oracle Linux.

* Passaggio 1: Aggiungere hello MySQL Yum repository commutatore troppo`root` utente:
  
            #[azureuser@mysqlnode:~]sudo su -
  
    Scaricare e installare hello MySQL versione pacchetto:
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* Passaggio 2: Modificare sotto i repository di MySQL hello tooenable file per il download del pacchetto MySQL5.6 hello.
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    Aggiornare ogni valore di questa toobelow file:
  
        \# *Enable toouse MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* Passaggio 3: Installare MySQL dal repository MySQL:
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    Il pacchetto RPM MySQL e tutti i pacchetti correlati verranno installati.
* Passaggio 4: Gestire hello in esecuzione il servizio MySQL
  
    (a) controllare lo stato del servizio di hello del server MySQL hello:
  
           #[root@mysqlnode ~]#service mysqld status
  
    (b) verificare se la porta di MySQL server di hello predefinita è in esecuzione:
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    (c) avviare hello MySQL server:

           #[root@mysqlnode ~]#service mysqld start

    (d) Arresta server MySQL hello:

           #[root@mysqlnode ~]#service mysqld stop

    (e) impostare MySQL toostart durante l'avvio del sistema hello:

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-tooinstall-mysql-on-suse-linux"></a>Come tooinstall MySQL in SUSE Linux
In questa circostanza si utilizzerà una VM Linux con OpenSUSE.

* Passaggio 1: Scaricare e installare MySQL Server
  
    Opzione troppo`root` utente tramite comando seguente:  
  
           #sudo su -
  
    Scaricare e installare il pacchetto MySQL:
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* Passaggio 2: Gestire hello in esecuzione il servizio MySQL
  
    (a) controllare lo stato di hello del server MySQL hello:
  
           #[root@mysqlnode ~]# rcmysql status
  
    (b) controllo hello se la porta predefinita del server MySQL hello:
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    (c) avviare hello MySQL server:

           #[root@mysqlnode ~]# rcmysql start

    (d) Arresta server MySQL hello:

           #[root@mysqlnode ~]# rcmysql stop

    (e) impostare MySQL toostart durante l'avvio del sistema hello:

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a>Passaggio successivo
Ulteriori utilizzi e informazioni su MySQL sono disponibili [qui](https://www.mysql.com/).

