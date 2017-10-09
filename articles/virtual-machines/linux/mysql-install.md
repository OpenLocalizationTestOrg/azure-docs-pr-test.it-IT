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
# <a name="how-tooinstall-mysql-on-azure"></a><span data-ttu-id="b1939-103">Come tooinstall MySQL in Azure</span><span class="sxs-lookup"><span data-stu-id="b1939-103">How tooinstall MySQL on Azure</span></span>
<span data-ttu-id="b1939-104">In questo articolo si apprenderà come tooinstall e configurare MySQL in una macchina virtuale di Azure che eseguono Linux.</span><span class="sxs-lookup"><span data-stu-id="b1939-104">In this article, you will learn how tooinstall and configure MySQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a><span data-ttu-id="b1939-105">Installare MySQL nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b1939-105">Install MySQL on your virtual machine</span></span>
> [!NOTE]
> <span data-ttu-id="b1939-106">È necessario disporre già una macchina virtuale di Microsoft Azure che eseguono Linux in ordine toocomplete questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b1939-106">You must already have a Microsoft Azure virtual machine running Linux in order toocomplete this tutorial.</span></span> <span data-ttu-id="b1939-107">Vedere il [esercitazione VM Linux di Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate e impostare una VM Linux con `mysqlnode` come nome della macchina virtuale hello e `azureuser` come utente prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="b1939-107">Please see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate and set up a Linux VM with `mysqlnode` as hello VM name and `azureuser` as user before proceeding.</span></span>
> 
> 

<span data-ttu-id="b1939-108">In questo caso, è possibile utilizzare 3306 porta come porta MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="b1939-108">In this case, use 3306 port as hello MySQL port.</span></span>  

<span data-ttu-id="b1939-109">Connettersi toohello VM Linux è stato creato tramite putty.</span><span class="sxs-lookup"><span data-stu-id="b1939-109">Connect toohello Linux VM you created via putty.</span></span> <span data-ttu-id="b1939-110">Se si tratta hello prima volta che si usa una macchina virtuale Linux di Azure, vedere la modalità di connessione tooa VM Linux toouse putty [qui](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b1939-110">If this is hello first time you use Azure Linux VM, see how toouse putty connect tooa Linux VM [here](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b1939-111">In questo articolo, ad esempio, si utilizzerà repository pacchetto tooinstall MySQL5.6.</span><span class="sxs-lookup"><span data-stu-id="b1939-111">We will use repository package tooinstall MySQL5.6 as an example in this article.</span></span> <span data-ttu-id="b1939-112">In realtà, MySQL5.6 presenta maggiori miglioramenti in termini di prestazioni rispetto a MySQL5.5.</span><span class="sxs-lookup"><span data-stu-id="b1939-112">Actually, MySQL5.6 has more improvement in performance than MySQL5.5.</span></span>  <span data-ttu-id="b1939-113">Ulteriori informazioni sono disponibili [qui](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span><span class="sxs-lookup"><span data-stu-id="b1939-113">More information [here](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span></span>

### <a name="how-tooinstall-mysql56-on-ubuntu"></a><span data-ttu-id="b1939-114">Come tooinstall MySQL5.6 in Ubuntu</span><span class="sxs-lookup"><span data-stu-id="b1939-114">How tooinstall MySQL5.6 on Ubuntu</span></span>
<span data-ttu-id="b1939-115">Di seguito si utilizzerà una VM Linux con Ubuntu da Azure.</span><span class="sxs-lookup"><span data-stu-id="b1939-115">We will use Linux VM with Ubuntu from Azure here.</span></span>

* <span data-ttu-id="b1939-116">Passaggio 1: Installare il Server di MySQL 5.6 passare troppo`root` utente:</span><span class="sxs-lookup"><span data-stu-id="b1939-116">Step 1: Install MySQL Server 5.6   Switch too`root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="b1939-117">Installare mysql-server 5.6:</span><span class="sxs-lookup"><span data-stu-id="b1939-117">Install mysql-server 5.6:</span></span>
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    <span data-ttu-id="b1939-118">Durante l'installazione, verrà visualizzato un poping finestra di dialogo backup tooask si tooset MySQL radice la password ed è necessario impostare password hello qui.</span><span class="sxs-lookup"><span data-stu-id="b1939-118">During installation, you will see a dialog window poping up tooask you tooset MySQL root password below, and you need set hello password here.</span></span>
  
    ![immagine](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    <span data-ttu-id="b1939-120">Password hello input tooconfirm nuovamente.</span><span class="sxs-lookup"><span data-stu-id="b1939-120">Input hello password again tooconfirm.</span></span>

    ![immagine](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* <span data-ttu-id="b1939-122">Passaggio 2: Accedere al server MySQL</span><span class="sxs-lookup"><span data-stu-id="b1939-122">Step 2: Login MySQL Server</span></span>
  
    <span data-ttu-id="b1939-123">Al termine dell'installazione del server MySQL, il servizio MySQL verrà avviato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b1939-123">When MySQL server installation finished, MySQL service will be started automatically.</span></span> <span data-ttu-id="b1939-124">È possibile accedere al server MySQL con l’utente `root` .</span><span class="sxs-lookup"><span data-stu-id="b1939-124">You can login MySQL Server with `root` user.</span></span>
    <span data-ttu-id="b1939-125">Utilizzare hello seguito password toologin e input di comando.</span><span class="sxs-lookup"><span data-stu-id="b1939-125">Use hello below command toologin and input password.</span></span>
  
             #[root@mysqlnode ~]# mysql -uroot -p
* <span data-ttu-id="b1939-126">Passaggio 3: Gestire hello in esecuzione il servizio MySQL</span><span class="sxs-lookup"><span data-stu-id="b1939-126">Step 3: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="b1939-127">(a) Ottenere lo stato del servizio MySQL</span><span class="sxs-lookup"><span data-stu-id="b1939-127">(a) Get status of MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql status
  
    <span data-ttu-id="b1939-128">(b) Avviare il servizio MySQL</span><span class="sxs-lookup"><span data-stu-id="b1939-128">(b) Start MySQL Service</span></span>
  
             #[root@mysqlnode ~]# service mysql start
  
    <span data-ttu-id="b1939-129">(c) Interrompere il servizio MySQL</span><span class="sxs-lookup"><span data-stu-id="b1939-129">(c) Stop MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql stop
  
    <span data-ttu-id="b1939-130">(d) riavviare il servizio di MySQL hello</span><span class="sxs-lookup"><span data-stu-id="b1939-130">(d) Restart hello MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-tooinstall-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a><span data-ttu-id="b1939-131">Aspetto tooinstall MySQL nella famiglia di sistemi operativi di Red Hat per CentOS, Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="b1939-131">How tooinstall MySQL on Red Hat OS family like CentOS, Oracle Linux</span></span>
<span data-ttu-id="b1939-132">In questo caso si utilizzerà la VM Linux con CentOS oppure Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="b1939-132">We will use Linux VM with CentOS or Oracle Linux here.</span></span>

* <span data-ttu-id="b1939-133">Passaggio 1: Aggiungere hello MySQL Yum repository commutatore troppo`root` utente:</span><span class="sxs-lookup"><span data-stu-id="b1939-133">Step 1: Add hello MySQL Yum repository   Switch too`root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="b1939-134">Scaricare e installare hello MySQL versione pacchetto:</span><span class="sxs-lookup"><span data-stu-id="b1939-134">Download and install hello MySQL release package:</span></span>
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* <span data-ttu-id="b1939-135">Passaggio 2: Modificare sotto i repository di MySQL hello tooenable file per il download del pacchetto MySQL5.6 hello.</span><span class="sxs-lookup"><span data-stu-id="b1939-135">Step 2: Edit below file tooenable hello MySQL repository for downloading hello MySQL5.6 package.</span></span>
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    <span data-ttu-id="b1939-136">Aggiornare ogni valore di questa toobelow file:</span><span class="sxs-lookup"><span data-stu-id="b1939-136">Update each value of this file toobelow:</span></span>
  
        \# *Enable toouse MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* <span data-ttu-id="b1939-137">Passaggio 3: Installare MySQL dal repository MySQL:</span><span class="sxs-lookup"><span data-stu-id="b1939-137">Step 3: Install MySQL from MySQL repository   Install MySQL:</span></span>
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    <span data-ttu-id="b1939-138">Il pacchetto RPM MySQL e tutti i pacchetti correlati verranno installati.</span><span class="sxs-lookup"><span data-stu-id="b1939-138">MySQL RPM package and all related packages will be installed.</span></span>
* <span data-ttu-id="b1939-139">Passaggio 4: Gestire hello in esecuzione il servizio MySQL</span><span class="sxs-lookup"><span data-stu-id="b1939-139">Step 4: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="b1939-140">(a) controllare lo stato del servizio di hello del server MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="b1939-140">(a) Check hello service status of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]#service mysqld status
  
    <span data-ttu-id="b1939-141">(b) verificare se la porta di MySQL server di hello predefinita è in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="b1939-141">(b) Check whether hello default port of  MySQL server is running:</span></span>
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    <span data-ttu-id="b1939-142">(c) avviare hello MySQL server:</span><span class="sxs-lookup"><span data-stu-id="b1939-142">(c) Start hello MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld start

    <span data-ttu-id="b1939-143">(d) Arresta server MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="b1939-143">(d) Stop hello MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld stop

    <span data-ttu-id="b1939-144">(e) impostare MySQL toostart durante l'avvio del sistema hello:</span><span class="sxs-lookup"><span data-stu-id="b1939-144">(e) Set MySQL toostart when hello system boot-up:</span></span>

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-tooinstall-mysql-on-suse-linux"></a><span data-ttu-id="b1939-145">Come tooinstall MySQL in SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="b1939-145">How tooinstall MySQL on SUSE Linux</span></span>
<span data-ttu-id="b1939-146">In questa circostanza si utilizzerà una VM Linux con OpenSUSE.</span><span class="sxs-lookup"><span data-stu-id="b1939-146">We will use Linux VM with OpenSUSE here.</span></span>

* <span data-ttu-id="b1939-147">Passaggio 1: Scaricare e installare MySQL Server</span><span class="sxs-lookup"><span data-stu-id="b1939-147">Step 1: Download and install MySQL Server</span></span>
  
    <span data-ttu-id="b1939-148">Opzione troppo`root` utente tramite comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b1939-148">Switch too`root` user through below command:</span></span>  
  
           #sudo su -
  
    <span data-ttu-id="b1939-149">Scaricare e installare il pacchetto MySQL:</span><span class="sxs-lookup"><span data-stu-id="b1939-149">Download and install MySQL package:</span></span>
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* <span data-ttu-id="b1939-150">Passaggio 2: Gestire hello in esecuzione il servizio MySQL</span><span class="sxs-lookup"><span data-stu-id="b1939-150">Step 2: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="b1939-151">(a) controllare lo stato di hello del server MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="b1939-151">(a) Check hello status of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]# rcmysql status
  
    <span data-ttu-id="b1939-152">(b) controllo hello se la porta predefinita del server MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="b1939-152">(b) Check whether hello default port of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    <span data-ttu-id="b1939-153">(c) avviare hello MySQL server:</span><span class="sxs-lookup"><span data-stu-id="b1939-153">(c) Start hello MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql start

    <span data-ttu-id="b1939-154">(d) Arresta server MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="b1939-154">(d) Stop hello MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql stop

    <span data-ttu-id="b1939-155">(e) impostare MySQL toostart durante l'avvio del sistema hello:</span><span class="sxs-lookup"><span data-stu-id="b1939-155">(e) Set MySQL toostart when hello system boot-up:</span></span>

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a><span data-ttu-id="b1939-156">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="b1939-156">Next Step</span></span>
<span data-ttu-id="b1939-157">Ulteriori utilizzi e informazioni su MySQL sono disponibili [qui](https://www.mysql.com/).</span><span class="sxs-lookup"><span data-stu-id="b1939-157">Find more usage and information regarding MySQL [Here](https://www.mysql.com/).</span></span>

