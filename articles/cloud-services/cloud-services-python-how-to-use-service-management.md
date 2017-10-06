---
title: "aaaHow toouse hello API gestione dei servizi (Python) - Guida alle funzionalità"
description: "Informazioni su come eseguire attività comuni di gestione del servizio di tooprogrammatically da Python."
services: cloud-services
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: 61538ec0-1536-4a7e-ae89-95967fe35d73
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/30/2017
ms.author: lmazuel
ms.openlocfilehash: b59622203470e1586484cec4033515edb39ca4d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-management-from-python"></a>La gestione dei servizi da Python toouse
Questa guida viene illustrato come eseguire attività comuni di gestione del servizio di tooprogrammatically da Python. Hello **ServiceManagementService** classe hello [Azure SDK per Python](https://github.com/Azure/azure-sdk-for-python) supporta l'accesso programmatico toomuch di hello-relative alla gestione delle funzionalità del servizio che è disponibile in hello [Portale di azure classico] [ management-portal] (ad esempio **creazione, aggiornamento ed eliminazione di servizi cloud, le distribuzioni, servizi di gestione dati e le macchine virtuali**). Questa funzionalità può essere utile per la creazione di applicazioni che richiedono la gestione di accesso a livello di codice tooservice.

## <a name="WhatIs"></a>Informazioni sulla gestione dei servizi
Hello API del servizio di gestione fornisce l'accesso programmatico toomuch di funzionalità di Gestione servizio hello disponibili tramite hello [portale di Azure classico][management-portal]. Hello Azure SDK per Python consente toomanage i servizi cloud e account di archiviazione.

API di gestione del servizio hello toouse, è necessario troppo[creare un account Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="Concepts"></a>Concetti
esegue il wrapping di Hello Azure SDK per Python hello [API di gestione del servizio di Azure][svc-mgmt-rest-api], che è un'API REST. Tutte le operazioni dell'API vengono eseguite tramite SSL e autenticate reciprocamente con certificati X.509 v3. il servizio di gestione di Hello sono accessibili da un servizio in esecuzione in Azure o direttamente su hello Internet da qualsiasi applicazione in grado di inviare una richiesta HTTPS e ricevere una risposta HTTPS.

## <a name="Installation"> </a>Installazione
Tutte le funzionalità di hello descritte in questo articolo sono disponibili in hello `azure-servicemanagement-legacy` pacchetto, è possibile installare l'uso di pip. Per ulteriori informazioni sull'installazione (ad esempio, se si è tooPython nuova), vedere questo articolo: [l'installazione di Python e hello Azure SDK](../python-how-to-install.md)

## <a name="Connect"></a>Procedura: connettersi a gestione tooservice
endpoint di gestione dei servizi toohello tooconnect, è necessario l'ID sottoscrizione Azure e un certificato di gestione valido. È possibile ottenere l'ID sottoscrizione tramite hello [portale di Azure classico][management-portal].

> [!NOTE]
> È ora possibile toouse certificati creati con OpenSSL durante l'esecuzione in Windows.  È necessario Python 2.7.4 o versioni successive. Gli utenti toouse OpenSSL anziché con estensione pfx, è consigliabile poiché il supporto per certificati verranno probabilmente rimossa in futuro hello pfx.
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a>Certificati di gestione in Windows/Mac/Linux (OpenSSL)
È possibile utilizzare [OpenSSL](http://www.openssl.org/) toocreate il certificato di gestione.  È necessario effettivamente toocreate due certificati, uno per il server di hello (un `.cer` file) e uno per i client hello (un `.pem` file). hello toocreate `.pem` file, eseguire:

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

hello toocreate `.cer` certificati, eseguire:

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

Per altre informazioni sui certificati di Azure, vedere [Panoramica sui certificati per i servizi cloud di Azure](cloud-services-certs-create.md). Per una descrizione completa di OpenSSL parametri, vedere la documentazione di hello in [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).

Dopo aver creato questi file, è necessario hello tooupload `.cer` file tooAzure tramite l'azione "Carica" hello della scheda "Impostazioni" hello di hello [portale di Azure classico][management-portal], ed è necessario annotare toomake in cui è stato salvato hello `.pem` file.

Dopo aver ottenuto l'ID sottoscrizione, un certificato creato e caricato hello `.cer` tooAzure file, è possibile connettere l'endpoint di gestione di Azure di toohello passando l'id sottoscrizione hello e hello percorso toohello `.pem` file troppo**ServiceManagementService**:

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

Nell'esempio sopra riportato, hello `sms` è un **ServiceManagementService** oggetto. Hello **ServiceManagementService** classe è hello classe primaria utilizzata toomanage servizi di Azure.

### <a name="management-certificates-on-windows-makecert"></a>Certificati di gestione in Windows (MakeCert)
È possibile creare nel computer un certificato di gestione autofirmato usando `makecert.exe`.  Aprire un **prompt dei comandi di Visual Studio** come un **amministratore** e utilizzare hello comando seguente, sostituendo *AzureCertificate* con nome certificato hello desiderato toouse.

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

comando Hello crea hello `.cer` file e lo installa nell'hello **personale** archivio certificati. Per altre informazioni, vedere [Panoramica sui certificati per i servizi cloud di Azure](cloud-services-certs-create.md).

Dopo aver creato il certificato di hello, è necessario hello tooupload `.cer` file tooAzure tramite l'azione "Carica" hello della scheda "Impostazioni" hello di hello [portale di Azure classico][management-portal].

Dopo aver ottenuto l'ID sottoscrizione, un certificato creato e caricato hello `.cer` tooAzure file, è possibile connettere endpoint di gestione di Azure toohello passando il idsottoscrizionehelloeilpercorsodihellodelcertificatohello**Personale** archivio certificati troppo**ServiceManagementService** (nuovamente, sostituire *AzureCertificate* con nome hello del certificato):

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

Nell'esempio sopra riportato, hello `sms` è un **ServiceManagementService** oggetto. Hello **ServiceManagementService** classe è hello classe primaria utilizzata toomanage servizi di Azure.

## <a name="ListAvailableLocations"></a>Procedura: Creare un elenco delle località disponibili
percorsi di hello toolist disponibili per l'hosting dei servizi, utilizzare hello **elenco\_percorsi** metodo:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

Quando si crea un servizio cloud o un servizio di archiviazione è necessario tooprovide un percorso valido. Hello **elenco\_percorsi** metodo restituisce sempre un elenco aggiornato dei percorsi di hello attualmente disponibile. In questo modo, le posizioni disponibili hello sono:

* Europa occidentale
* Europa settentrionale
* Asia sudorientale
* Asia orientale
* Stati Uniti centrali
* Stati Uniti centro-settentrionali
* Stati Uniti centro-meridionali
* Stati Uniti occidentali
* Stati Uniti orientali
* Giappone orientale
* Giappone occidentale
* Brasile meridionale
* Australia orientale
* Australia sudorientale

## <a name="CreateCloudService"></a>Procedura: Creare un servizio cloud
Quando si crea un'applicazione ed eseguirla in Azure, il codice hello e la configurazione vengono chiamati di Azure [servizio cloud] [ cloud service] (noto come un *servizio ospitato* in precedenza Versioni di Azure). Hello **creare\_ospitato\_servizio** metodo consente toocreate un nuovo servizio ospitato, fornendo un nome di servizio ospitato (che deve essere univoco in Azure), un'etichetta (toobase64 codificato automaticamente), un descrizione e un percorso.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

È possibile elencare tutti i servizi ospitato hello per la sottoscrizione con hello **elenco\_ospitato\_servizi** metodo:

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

Se si desiderano tooget informazioni relative a un servizio ospitato particolare, è possibile farlo passando hello ospitato servizio nome toohello **ottenere\_ospitato\_servizio\_proprietà** metodo:

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

Dopo aver creato un servizio cloud, è possibile distribuire il servizio toohello codice con hello **creare\_distribuzione** metodo.

## <a name="DeleteCloudService"></a>Procedura: Eliminare un servizio cloud
È possibile eliminare un servizio cloud passando hello servizio nome toohello **eliminare\_ospitato\_servizio** metodo:

    sms.delete_hosted_service('myhostedservice')

Prima di poter eliminare un servizio, è necessario eliminare innanzitutto tutte le distribuzioni per il servizio di hello. Per informazioni dettagliate, vedere [Procedura: Eliminare una distribuzione](#DeleteDeployment) .

## <a name="DeleteDeployment"></a>Procedura: Eliminare una distribuzione
toodelete una distribuzione, utilizzare hello **eliminare\_distribuzione** metodo. Hello esempio seguente viene illustrato come toodelete una distribuzione denominata `v1`.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <a name="CreateStorageService"> </a>Procedura: Creare un servizio di archiviazione
Oggetto [servizio di archiviazione](../storage/common/storage-create-storage-account.md) fornisce l'accesso tooAzure [BLOB](../storage/blobs/storage-python-how-to-use-blob-storage.md), [tabelle](../cosmos-db/table-storage-how-to-use-python.md), e [code](../storage/queues/storage-python-how-to-use-queue-storage.md). toocreate un servizio di archiviazione, è necessario un nome per il servizio di hello (compreso tra 3 e 24 caratteri minuscoli e univoco all'interno di Azure), una descrizione, un'etichetta (i caratteri too100, toobase64 automaticamente con codifica) e un percorso. Hello di esempio seguente viene illustrato come toocreate uno spazio di archiviazione del servizio, specificando un percorso.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mystorageaccount'
    label = 'mystorageaccount'
    location = 'West US'
    desc = 'My storage account description.'

    result = sms.create_storage_account(name, desc, label, location=location)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

Si noti in hello sopra riportato lo stato di hello hello **creare\_archiviazione\_account** operazione può essere recuperata passando hello risultato **creare\_archiviazione \_account** toohello **ottenere\_operazione\_stato** metodo.  

È possibile elencare gli account di archiviazione e le relative proprietà con hello **elenco\_archiviazione\_account** metodo:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <a name="DeleteStorageService"></a>Procedura: Eliminare un servizio di archiviazione
È possibile eliminare un servizio di archiviazione passando hello archiviazione servizio nome toohello **eliminare\_archiviazione\_account** metodo. Se si elimina un servizio di archiviazione, tutti i dati archiviati nel servizio hello (BLOB, tabelle e code).

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <a name="ListOperatingSystems"></a>Procedura: Elencare i sistemi operativi disponibili
sistemi operativi toolist hello disponibili per l'hosting dei servizi, utilizzare hello **elenco\_operativo\_sistemi** metodo:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

In alternativa, è possibile utilizzare hello **elenco\_operativo\_sistema\_famiglie** metodo, che raggruppa i sistemi operativi hello dalla famiglia di:

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <a name="CreateVMImage"></a>Procedura: Creare un'immagine del sistema operativo
un archivio di immagini del sistema operativo immagine toohello, tooadd utilizzare hello **aggiungere\_os\_immagine** metodo:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mycentos'
    label = 'mycentos'
    os = 'Linux' # Linux or Windows
    media_link = 'url_to_storage_blob_for_source_image_vhd'

    result = sms.add_os_image(label, media_link, name, os)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

immagini del sistema operativo hello toolist disponibili, utilizzare hello **elenco\_os\_immagini** metodo. Sono incluse tutte le immagini di piattaforma e utente:

    result = sms.list_os_images()

    for image in result:
        print('Name: ' + image.name)
        print('Label: ' + image.label)
        print('OS: ' + image.os)
        print('Category: ' + image.category)
        print('Description: ' + image.description)
        print('Location: ' + image.location)
        print('Media link: ' + image.media_link)
        print('')

## <a name="DeleteVMImage"></a>Procedura: Eliminare un'immagine del sistema operativo
toodelete un'immagine utente, utilizzare hello **eliminare\_os\_immagine** metodo:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <a name="CreateVM"> </a>Procedura: Creare una macchina virtuale
toocreate una macchina virtuale, è innanzitutto necessario toocreate un [servizio cloud](#CreateCloudService).  Creare quindi distribuzione della macchina virtuale hello utilizzando hello **creare\_virtuale\_macchina\_distribuzione** metodo:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where hello VM disk
    # will be created
    media_link = 'url_to_target_storage_blob_for_vm_hd'

    # Linux VM configuration, you can use WindowsConfigurationSet
    # for a Windows VM instead
    linux_config = LinuxConfigurationSet('myhostname', 'myuser', 'mypassword', True)

    os_hd = OSVirtualHardDisk(image_name, media_link)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=os_hd,
        role_size='Small')

## <a name="DeleteVM"></a>Procedura: Eliminare una macchina virtuale
toodelete una macchina virtuale, prima di tutto eliminare hello distribuzione mediante hello **eliminare\_distribuzione** metodo:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

è quindi possibile eliminare il servizio di cloud Hello utilizzando hello **eliminare\_ospitato\_servizio** metodo:

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a>Procedura: Creare una macchina virtuale da un'immagine di macchina virtuale acquisita
toocapture un'immagine di macchina virtuale, chiamare prima hello **acquisire\_vm\_immagine** metodo:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace hello below three parameters with actual values
    hosted_service_name = 'hs1'
    deployment_name = 'dep1'
    vm_name = 'vm1'

    image_name = vm_name + 'image'
    image = CaptureRoleAsVMImage    ('Specialized',
        image_name,
        image_name + 'label',
        image_name + 'description',
        'english',
        'mygroup')

    result = sms.capture_vm_image(
            hosted_service_name,
            deployment_name,
            vm_name,
            image
        )

Successivamente, toomake certi che è stato acquisizione immagine hello, utilizzare hello **elenco\_vm\_immagini** api e assicurarsi che l'immagine viene visualizzata nei risultati di hello:

    images = sms.list_vm_images()

toofinally creare una macchina virtuale hello utilizzando l'immagine acquisita hello, utilizzare hello **creare\_virtuale\_macchina\_distribuzione** come prima, ma questa volta passare vm_image_name hello invece

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=None,
        role_size='Small',
        vm_image_name = image_name)

altre informazioni sulle toolearn toocapture una macchina virtuale Linux, vedere [come tooCapture una macchina virtuale di Linux.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

altre informazioni sulle toolearn toocapture una macchina virtuale di Windows, vedere [come tooCapture una macchina virtuale di Windows.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="What's Next"></a>Passaggi successivi
Dopo aver appreso hello passaggi di base di gestione dei servizi, è possibile accedere hello [documentazione di riferimento API completa per hello Azure SDK Python](http://azure-sdk-for-python.readthedocs.org/) ed eseguire complesso è attività facilmente toomanage applicazione python.

Per ulteriori informazioni, vedere hello [Centro per sviluppatori Python](/develop/python/).

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect tooservice management]: #Connect
[How to: List available locations]: #ListAvailableLocations
[How to: Create a cloud service]: #CreateCloudService
[How to: Delete a cloud service]: #DeleteCloudService
[How to: Create a deployment]: #CreateDeployment
[How to: Update a deployment]: #UpdateDeployment
[How to: Move deployments between staging and production]: #MoveDeployments
[How to: Delete a deployment]: #DeleteDeployment
[How to: Create a storage service]: #CreateStorageService
[How to: Delete a storage service]: #DeleteStorageService
[How to: List available operating systems]: #ListOperatingSystems
[How to: Create an operating system image]: #CreateVMImage
[How to: Delete an operating system image]: #DeleteVMImage
[How to: Create a virtual machine]: #CreateVM
[How to: Delete a virtual machine]: #DeleteVM
[Next Steps]: #NextSteps
[management-portal]: https://manage.windowsazure.com/
[svc-mgmt-rest-api]: http://msdn.microsoft.com/library/windowsazure/ee460799.aspx


[cloud service]:/services/cloud-services/
