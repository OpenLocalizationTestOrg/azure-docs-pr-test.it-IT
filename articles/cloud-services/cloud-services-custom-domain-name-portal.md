---
title: Configurare un nome di dominio personalizzato nei servizi cloud | Microsoft Docs
description: Informazioni su come esporre i dati su internet o l'applicazione Azure in un dominio personalizzato configurando le impostazioni DNS.  Questi esempi utilizzano il portale di Azure.
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 5783a246-a151-4fb1-b488-441bfb29ee44
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 139ec6578dc9e76039c5fb13e7a7741aa8ba4e0d
ms.sourcegitcommit: f847fcbf7f89405c1e2d327702cbd3f2399c4bc2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a>Configurazione di un nome di dominio personalizzato per un servizio cloud di Azure
Quando si crea un servizo cloud, Azure lo assegna a un sottodominio di **cloudapp.net**. Ad esempio, se il servizio cloud è denominato "contoso", gli utenti saranno in grado di accedere all'applicazione da un URL come http://contoso.cloudapp.net. Azure assegna anche un indirizzo IP virtuale.

È tuttavia possibile esporre l'applicazione in un nome di dominio personalizzato, ad esempio **contoso.com**. In questo articolo viene illustrato come riservare o configurare un nome di dominio personalizzato per i ruoli Web del servizio cloud.

Se si conoscono già i record CNAME e A, [saltare la spiegazione](#add-a-cname-record-for-your-custom-domain).

> [!NOTE]
> Le procedure in questa attività si applicano ai servizi cloud di Azure. Per Servizi app, vedere [Esecuzione del mapping di un nome DNS personalizzato esistente con un app Web di Azure](../app-service/app-service-web-tutorial-custom-domain.md). Per gli account di archiviazione, vedere [Configurare un nome di dominio personalizzato per l'endpoint di archiviazione BLOB](../storage/blobs/storage-custom-domain-name.md).
> 
> 

<p/>

> [!TIP]
> Acquistare velocità: usare il NUOVO [percorso guidato](http://support.microsoft.com/kb/2990804) di Azure  Grazie al percorso guidato, è facilissimo associare un nome di dominio personalizzato E proteggere le comunicazioni (SSL) con i Servizi cloud di Azure o Siti Web di Azure.
> 
> 

## <a name="understand-cname-and-a-records"></a>Informazioni sui record CNAME e A
I record CNAME (o record Alias) e i record A consentono entrambi di associare un nome di dominio a un server specifico (o in questo caso a un servizio) tuttavia le modalità di funzionamento sono diverse. Vi sono inoltre alcune considerazioni specifiche sull'utilizzo di record A con i servizi cloud di Azure, di cui è necessario tenere conto prima di decidere il tipo di record da utilizzare.

### <a name="cname-or-alias-record"></a>Record CNAME o Alias
Un record CNAME consente di eseguire il mapping di un dominio *specifico* , ad esempio **contoso.com** or **www.contoso.com**, a un nome di dominio canonico. In questo caso, il nome di dominio canonico è il nome di dominio **[myapp].cloudapp.net** dell'applicazione ospitata in Azure. Dopo la creazione, il record CNAME crea a sua volta un alias per **[myapp].cloudapp.net**. La voce CNAME viene risolta nell'indirizzo IP del servizio **[myapp].cloudapp.net** in modo automatico, pertanto se l'indirizzo IP del servizio cloud cambia non sarà necessaria alcuna azione.

> [!NOTE]
> Alcuni registrar consentono di eseguire il mapping solo dei sottodomini se si usa un record CNAME, ad esempio www.contoso.com, e non dei nomi radice come contoso.com. Per altre informazioni sui record CNAME, vedere la documentazione fornita dal registrar, la [voce di Wikipedia sui record CNAME](http://en.wikipedia.org/wiki/CNAME_record) oppure il documento di IETF relativo a [implementazione e specifiche dei nomi di dominio](http://tools.ietf.org/html/rfc1035).
> 
> 

### <a name="a-record"></a>Record A
Un record *A* consente di eseguire il mapping di un dominio, ad esempio **contoso.com** o **www.contoso.com**, *o di un dominio con caratteri jolly*, ad esempio **\*.contoso.com**, a un indirizzo IP. Nel caso di un servizio cloud di Azure, si tratta dell'IP virtuale del servizio. Il principale vantaggio di un record A rispetto a un record CNAME consiste quindi nel fatto che un'unica voce con un carattere jolly, ad esempio \***.contoso.com**, gestirà le richieste per più sottodomini, ad esempio **mail.contoso.com**, **login.contoso.com** o **www.contso.com**.

> [!NOTE]
> Poiché il mapping di un record A viene eseguito a un indirizzo IP statico, il record non è in grado di risolvere automaticamente le modifiche all'indirizzo IP del servizio cloud. L'indirizzo IP usato dal servizio cloud viene allocato la prima volta che si effettua una distribuzione in uno slot vuoto di produzione o di gestione temporanea. Se si elimina la distribuzione per lo slot, l'indirizzo IP viene rilasciato da Azure e le distribuzioni future in quello slot potrebbero ricevere un nuovo indirizzo IP.
> 
> L'indirizzo IP di un determinato slot di distribuzione (di produzione o di gestione temporanea) viene reso permanente durante i passaggi tra distribuzioni di produzione e di gestione temporanea o durante l'esecuzione di aggiornamenti sul posto di distribuzioni esistenti. Per ulteriori informazioni sull'esecuzione di queste azioni, vedere [Come gestire i servizi cloud](cloud-services-how-to-manage-portal.md).
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a>Aggiunta di un record CNAME per il dominio personalizzato
Per creare un record CNAME è necessario aggiungere una nuova voce nella tabella DNS del dominio personalizzato utilizzando gli strumenti forniti dal registrar. Sebbene i registrar utilizzino metodi simili per specificare un record CNAME, vi sono alcune differenze nel modo in cui ognuno consente di effettuare questa operazione. Il concetto di base è tuttavia identico per tutti.

1. Utilizzare uno dei metodi seguenti per trovare il nome di dominio **.cloudapp.net** assegnato al servizio cloud in questione.
   
   * Accedere al [portale di Azure], selezionare il servizio cloud, esaminare la sezione **Informazioni di base** e quindi individuare la voce **URL sito**.
     
       ![Sezione quick glance in cui è visualizzato l'URL del sito][csurl]
     
       **OR**
   * Installare e configurare [Azure Powershell](/powershell/azure/overview), quindi eseguire il comando seguente:
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     Salvare il nome di dominio utilizzato nell'URL restituito da uno dei metodi, poiché sarà necessario per la creazione di un record CNAME.
2. Accedere al sito Web del registrar DNS e passare alla pagina di gestione dei DNS. Individuare collegamenti o aree del sito denominate **Domain Name**, **DNS** o **Name Server Management**.
3. Trovare la sezione in cui è possibile selezionare o immettere CNAME. Può essere necessario selezionare un tipo di record in un elenco a discesa oppure passare a una pagina di impostazioni avanzate. Individuare i termini **CNAME**, **Alias** o **Subdomains** (Sottodomini).
4. È necessario fornire anche l'alias di dominio o sottodominio per CNAME, ad esempio **www**, se si vuole creare un alias per **www.customdomain.com**. Se si desidera creare un alias per il dominio radice, è possibile che sia elencato con il simbolo '**@**' negli strumenti DNS del registrar.
5. A questo punto, occorre fornire un nome host canonico, che in questo caso corrisponde al dominio **cloudapp.net** .

Il record CNAME seguente, ad esempio, inoltra tutto il traffico da **www.contoso.com** a **contoso.cloudapp.net**, che è il nome di dominio personalizzato dell'applicazione distribuita:

| Alias/Nome host/Sottodominio | Dominio canonico |
| --- | --- |
| www |contoso.cloudapp.net |

> [!NOTE]
> A un visitatore di **www.contoso.com** non verrà mai visualizzato il nome dell'host reale (contoso.cloudapp.net), pertanto il processo di inoltro risulta totalmente invisibile all'utente finale.
> 
> L'esempio precedente si applica solo al sottodominio **www** . Poiché non è possibile usare caratteri jolly con i record CNAME, è necessario crearne uno per ogni dominio/sottodominio. Se si vuole indirizzare traffico da sottodomini, ad esempio *.contoso.com, all'indirizzo cloudapp.net in uso, è possibile configurare una voce di **reindirizzamento URL** o **inoltro URL** nelle impostazioni DNS oppure creare un record A.
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a>Aggiungere un record A per il dominio personalizzato
Per creare un record A, è necessario innanzitutto trovare l'indirizzo IP virtuale del servizio cloud. Si aggiunge quindi una voce nella tabella DNS del dominio personalizzato utilizzando gli strumenti forniti dal registrar. Sebbene i registrar utilizzino metodi simili per specificare un record A, vi sono alcune differenze nel modo in cui ognuno consente di effettuare questa operazione. Il concetto di base è tuttavia identico per tutti.

1. Utilizzare uno dei metodi seguenti per ottenere l'indirizzo IP del servizio cloud.
   
   * Accedere al [portale di Azure], selezionare il servizio cloud, esaminare la sezione **Informazioni di base** e quindi individuare la voce **Indirizzi IP pubblici**.
     
       ![Sezione quick glance in cui è visualizzato l'indirizzo VIP][vip]
     
       **OR**
   * Installare e configurare [Azure Powershell](/powershell/azure/overview), quindi eseguire il comando seguente:
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     Salvare l'indirizzo IP, poiché sarà necessario per la creazione di un record A.
2. Accedere al sito Web del registrar DNS e passare alla pagina di gestione dei DNS. Individuare collegamenti o aree del sito denominate **Domain Name**, **DNS** o **Name Server Management**.
3. Trovare la sezione in cui è possibile selezionare o immettere i record A. Può essere necessario selezionare un tipo di record in un elenco a discesa oppure passare a una pagina di impostazioni avanzate.
4. Selezionare o immettere il dominio o sottodominio che utilizzerà il record A. Selezionare ad esempio **www** se si vuole creare un alias per **www.customdomain.com**. Se si vuole creare una voce con caratteri jolly per tutti i sottodomini, immettere '*****'. In questo modo verranno inclusi tutti i sottodomini, ad esempio **mail.customdomain.com**, **login.customdomain.com** e **www.customdomain.com**.
   
    Se si desidera creare un record A per il dominio radice, è possibile che sia elencato con il simbolo '**@**' negli strumenti DNS del registrar.
5. Immettere l'indirizzo IP del servizio cloud nell'apposito campo. La voce del dominio usata nel record A verrà associata all'indirizzo IP della distribuzione del servizio cloud.

Il record A seguente, ad esempio, inoltra tutto il traffico da **contoso.com** a **137.135.70.239**, che è l'indirizzo IP dell'applicazione distribuita:

| Nome host/Sottodominio | Indirizzo IP |
| --- | --- |
| @ |137.135.70.239 |

In questo esempio viene illustrata la creazione di un record A per il dominio radice. Se si vuole creare una voce con caratteri jolly per tutti i sottodomini, immettere '*****' come sottodominio.

> [!WARNING]
> Gli indirizzi IP in Azure sono dinamici per impostazione predefinita. È possibile utilizzare un [indirizzo IP riservato](../virtual-network/virtual-networks-reserved-public-ip.md) per garantire che l'indirizzo IP non venga modificato.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* [Come gestire i servizi cloud](cloud-services-how-to-manage-portal.md)
* [Come eseguire il mapping del contenuto della rete CDN a un dominio personalizzato](../cdn/cdn-map-content-to-custom-domain.md)
* [Configurazione generale del servizio cloud](cloud-services-how-to-configure-portal.md).
* Procedura [distribuire un servizio cloud](cloud-services-how-to-create-deploy-portal.md).
* Configurare i [certificati ssl](cloud-services-configure-ssl-certificate-portal.md).

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: cloud-services-how-to-manage-portal.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
[Create a CNAME record that associates the subdomain with the storage account]: #create-cname
[portale di Azure]: https://portal.azure.com
[vip]: ./media/cloud-services-custom-domain-name-portal/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name-portal/csurl.png
