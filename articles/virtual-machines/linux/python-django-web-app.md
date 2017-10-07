---
title: app web aaaPython con Django in una macchina virtuale Linux di Azure | Documenti Microsoft
description: Informazioni su come toohost a Django basato su web app in Azure utilizzando una VM Linux.
services: virtual-machines-linux
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-resource-manager
ms.assetid: 00ad4c2c-4316-4f9a-913f-f7f49b158db7
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 520c47e19e8ffb4bb866f70772d506ddf76e242c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-linux-vm"></a>App Web Hello World Django in una macchina virtuale Linux
> [!div class="op_single_selector"]
> * [Windows](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [Mac/Linux](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

In questa esercitazione illustra come toohost un sito Web basato su Django in Linux in macchine virtuali di Azure. Nell'esercitazione di hello, non si presuppone alcuna esperienza precedente con Azure. Dopo aver esercitazione hello, è possibile avere un'applicazione basata su Django backup e in esecuzione nel cloud hello.

È possibile passare agli argomenti seguenti:

* Consente di impostare un Django di toohost macchina virtuale di Azure. Sebbene in questa esercitazione viene illustrato come toodo per **Linux**, è possibile eseguire hello uguali per una macchina virtuale di Windows Server ospitato in Azure. 
* Creare una nuova applicazione Django in Linux.

Hello esercitazione vengono illustrate le modalità di applicazione web toobuild una base di Hello World. un'applicazione Hello è ospitata in una macchina virtuale di Azure.

Hello seguente schermata mostra un'applicazione hello completata:

![Una finestra del browser visualizza una pagina di Hello World hello in Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>Creare e configurare un toohost macchina virtuale di Azure Django

1. vedere toocreate macchina virtuale di Azure con distribuzione Ubuntu Server 14.04 LTS, hello [creare una macchina virtuale Linux nel portale di Azure hello](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). È anche possibile scegliere l'autenticazione della password invece di usare una chiave pubblica SSH.
2. tooedit hello rete sicurezza gruppo tooallow in ingresso HTTP traffico tooport 80, vedere [creare gruppi di sicurezza di rete nel portale di Azure hello](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).
3. (Facoltativo) La nuova macchina virtuale non dispone di un nome di dominio completo (FQDN) per impostazione predefinita.  toocreate una macchina virtuale con un nome di dominio completo, vedere [creare un nome di dominio completo in hello portale di Azure per una macchina virtuale Windows](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Questo passaggio non è necessario per completare questa esercitazione.

## <a id="setup"></a>Configurare un ambiente di sviluppo hello
> [!NOTE]
> Se è necessario tooinstall Python o le librerie client di hello toouse, vedere hello [Guida all'installazione di Python](../../python-how-to-install.md).

Hello Ubuntu Linux VM include Python 2.7 preinstallati, ma non proviene con Apache o Django. Completare i seguenti passaggi tooconnect tooyour VM hello e installare il pacchetto Apache e Django:

1. Aprire una nuova finestra del terminale.
2. tooconnect toohello macchina virtuale di Azure, immettere hello comando seguente. Se non è stato creato un nome di dominio completo, è possibile connettersi utilizzando l'indirizzo IP pubblico hello che viene visualizzato nella macchina virtuale hello riepilogo in hello portale di Azure.
   
       $ ssh yourusername@yourVmUrl
3. tooinstall Django, immettere hello seguenti comandi:
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. tooinstall Apache con mod-wsgi, immettere hello comando seguente:
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a>Creare una nuova app Django
1. tooaccess SSH toouse la macchina virtuale, la finestra Terminal aprire hello usato nella precedente sezione hello.
2. un nuovo progetto, Django toocreate immettere hello seguenti comandi:
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   Hello `django-admin.py` script genera una struttura di base per i siti Web basati su Django:
   
   * `helloworld/manage.py` consente di avviare e arrestare l'hosting del sito Web basato su Django.
   * `helloworld/helloworld/settings.py` contiene le impostazioni di Django per l'applicazione.
   * `helloworld/helloworld/urls.py`dispone di codice di mapping hello tra ogni URL e la relativa visualizzazione.
3. Nella directory /var/www/helloworld/helloworld hello, creare un nuovo file denominato views.py. Questo file contiene una visualizzazione hello che esegue il rendering hello "hello world" pagina. Nell'editor di codice, immettere hello seguenti comandi:
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. Sostituire il contenuto di hello del file urls.py hello con hello seguenti comandi:
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a>Configurare Apache
1. Nella cartella /etc/apache2/sites-available/helloworld.conf hello, creare un file di configurazione host virtuale Apache. Impostare hello contenuto toohello i valori seguenti. Sostituire *Nomevm* con nome effettivo del hello della macchina hello in uso (ad esempio, *pyubuntu*).
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. sito di hello tooactivate, utilizzare hello comando seguente:
   
       $ sudo a2ensite helloworld
3. toorestart Apache, utilizzare hello comando seguente:
   
       $ sudo service apache2 reload
4. Caricare la pagina Web hello nel browser:
   
   ![Una finestra del browser visualizza una pagina di hello hello world in Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a>Arrestare la macchina virtuale di Azure
Una volta terminato con questa esercitazione, si consiglia di spegnere o rimuovere una macchina virtuale di Azure creata per l'esercitazione hello hello. Ciò consente di liberare risorse per altre esercitazioni ed evitare di incorrere in costi di utilizzo di Azure.

