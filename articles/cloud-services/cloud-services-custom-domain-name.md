---
title: Configurare un nome di dominio personalizzato nei servizi cloud | Documentazione Microsoft
description: Informazioni su come esporre i dati o l'applicazione Azure in un dominio personalizzato configurando le impostazioni DNS.
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 6a62c2b7-ea47-4cce-9d6a-0cca38357f42
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: b61f6aad7cf974ce25baf944e342284b02ea0048
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a>Configurazione di un nome di dominio personalizzato per un servizio cloud di Azure
> [!div class="op_single_selector"]
> * [Portale di Azure](cloud-services-custom-domain-name-portal.md)
> * [Portale di Azure classico](cloud-services-custom-domain-name.md)
> 
> 

Quando si crea un servizo cloud, Azure lo assegna a un sottodominio di cloudapp.net. Ad esempio, se il servizio cloud è denominato "contoso", gli utenti saranno in grado di accedere all'applicazione da un URL come http://contoso.cloudapp.net. Azure assegna anche un indirizzo IP virtuale.

È tuttavia possibile esporre l'applicazione in un nome di dominio personalizzato, ad esempio contoso.com. In questo articolo viene illustrato come riservare o configurare un nome di dominio personalizzato per i ruoli Web del servizio cloud.

Se si conoscono già i record CNAME e A, [saltare la spiegazione](#add-a-cname-record-for-your-custom-domain).

> [!NOTE]
> Per velocizzare le operazioni, usare la [procedura guidata dettagliata](http://support.microsoft.com/kb/2990804). Grazie alla procedura guidata, è facile associare un nome di dominio personalizzato e proteggere le comunicazioni (SSL) con i Servizi cloud di Azure o Siti Web di Azure.
> 
> 

<p/>

> [!NOTE]
> Le procedure in questa attività si applicano ai servizi cloud di Azure. Per Servizi app, vedere [questo articolo](../app-service/app-service-web-tutorial-custom-domain.md). Per gli account di archiviazione, vedere [questo articolo](../storage/blobs/storage-custom-domain-name.md).
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
Un record A consente di eseguire il mapping di un dominio, ad esempio **contoso.com** o **www.contoso.com**, *o di un dominio con caratteri jolly* ad esempio **\*.contoso.com**, a un indirizzo IP. Nel caso di un servizio cloud di Azure, si tratta dell'IP virtuale del servizio. Il principale vantaggio di un record A rispetto a un record CNAME consiste quindi nel fatto che un'unica voce con un carattere jolly, ad esempio \***.contoso.com**, gestirà le richieste per più sottodomini, ad esempio **mail.contoso.com**, **login.contoso.com** o **www.contso.com**.

> [!NOTE]
> Poiché il mapping di un record A viene eseguito a un indirizzo IP statico, il record non è in grado di risolvere automaticamente le modifiche all'indirizzo IP del servizio cloud. L'indirizzo IP usato dal servizio cloud viene allocato la prima volta che si effettua una distribuzione in uno slot vuoto di produzione o di gestione temporanea. Se si elimina la distribuzione per lo slot, l'indirizzo IP viene rilasciato da Azure e le distribuzioni future in quello slot potrebbero ricevere un nuovo indirizzo IP.
> 
> L'indirizzo IP di un determinato slot di distribuzione (di produzione o di gestione temporanea) viene reso permanente durante i passaggi tra distribuzioni di produzione e di gestione temporanea o durante l'esecuzione di aggiornamenti sul posto di distribuzioni esistenti. Per ulteriori informazioni sull'esecuzione di queste azioni, vedere [Come gestire i servizi cloud](cloud-services-how-to-manage.md).
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a>Aggiunta di un record CNAME per il dominio personalizzato
Per creare un record CNAME è necessario aggiungere una nuova voce nella tabella DNS del dominio personalizzato utilizzando gli strumenti forniti dal registrar. Sebbene i registrar utilizzino metodi simili per specificare un record CNAME, vi sono alcune differenze nel modo in cui ognuno consente di effettuare questa operazione. Il concetto di base è tuttavia identico per tutti.

1. Utilizzare uno dei metodi seguenti per trovare il nome di dominio **.cloudapp.net** assegnato al servizio cloud in questione.
   
   * Accedere al [portale di Azure classico], selezionare il servizio cloud, scegliere **Dashboard**, quindi individuare la voce **URL sito** nella sezione **riepilogo rapido**.
     
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

A un visitatore di **www.contoso.com** non verrà mai visualizzato il nome dell'host reale (contoso.cloudapp.net), pertanto il processo di inoltro risulta totalmente invisibile all'utente finale.

> [!NOTE]
> L'esempio precedente si applica solo al sottodominio **www** . Poiché non è possibile usare caratteri jolly con i record CNAME, è necessario crearne uno per ogni dominio/sottodominio. Se si vuole indirizzare traffico da sottodomini, ad esempio \*.contoso.com, all'indirizzo cloudapp.net in uso, è possibile configurare una voce di **reindirizzamento URL** o **inoltro URL** nelle impostazioni DNS oppure creare un record A.
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a>Aggiungere un record A per il dominio personalizzato
Per creare un record A, è necessario innanzitutto trovare l'indirizzo IP virtuale del servizio cloud. Si aggiunge quindi una voce nella tabella DNS del dominio personalizzato utilizzando gli strumenti forniti dal registrar. Sebbene i registrar utilizzino metodi simili per specificare un record A, vi sono alcune differenze nel modo in cui ognuno consente di effettuare questa operazione. Il concetto di base è tuttavia identico per tutti.

1. Utilizzare uno dei metodi seguenti per ottenere l'indirizzo IP del servizio cloud.
   
   * Accedere al [portale di Azure classico], selezionare il servizio cloud, scegliere **Dashboard**, quindi individuare la voce **Indirizzo IP virtuale pubblico (VIP)** nella sezione **riepilogo rapido**.
     
       ![Sezione quick glance in cui è visualizzato l'indirizzo VIP][vip]
     
       **OR**  
   * Installare e configurare [Azure Powershell](/powershell/azure/overview), quindi eseguire il comando seguente:
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     Nel caso in cui vi siano più endpoint associati al servizio cloud, si riceveranno più righe contenenti l'indirizzo IP, tuttavia tali righe dovrebbero visualizzare tutte lo stesso indirizzo.
     
     Salvare l'indirizzo IP, poiché sarà necessario per la creazione di un record A.
2. Accedere al sito Web del registrar DNS e passare alla pagina di gestione dei DNS. Individuare collegamenti o aree del sito denominate **Domain Name**, **DNS** o **Name Server Management**.
3. Trovare la sezione in cui è possibile selezionare o immettere i record A. Può essere necessario selezionare un tipo di record in un elenco a discesa oppure passare a una pagina di impostazioni avanzate.
4. Selezionare o immettere il dominio o sottodominio che utilizzerà il record A. Selezionare ad esempio **www** se si vuole creare un alias per **www.customdomain.com**. Se si vuole creare una voce con caratteri jolly per tutti i sottodomini, immettere '__*__'. In questo modo verranno inclusi tutti i sottodomini, ad esempio **mail.customdomain.com**, **login.customdomain.com** e **www.customdomain.com**.
   
    Se si desidera creare un record A per il dominio radice, è possibile che sia elencato con il simbolo '**@**' negli strumenti DNS del registrar.
5. Immettere l'indirizzo IP del servizio cloud nell'apposito campo. La voce del dominio usata nel record A verrà associata all'indirizzo IP della distribuzione del servizio cloud.

Il record A seguente, ad esempio, inoltra tutto il traffico da **contoso.com** a **137.135.70.239**, che è l'indirizzo IP dell'applicazione distribuita:

| Nome host/Sottodominio | Indirizzo IP |
| --- | --- |
| @ |137.135.70.239 |

In questo esempio viene illustrata la creazione di un record A per il dominio radice. Se si desidera creare una voce con caratteri jolly per tutti i sottodomini, immettere '__*__' come sottodominio.

> [!WARNING]
> Gli indirizzi IP in Azure sono dinamici per impostazione predefinita. È possibile utilizzare un [indirizzo IP riservato](../virtual-network/virtual-networks-reserved-public-ip.md) per garantire che l'indirizzo IP non venga modificato.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* [Come gestire i servizi cloud](cloud-services-how-to-manage.md)
* [Come eseguire il mapping del contenuto della rete CDN a un dominio personalizzato](../cdn/cdn-map-content-to-custom-domain.md)
* [Configurazione generale del servizio cloud](cloud-services-how-to-configure.md).
* Procedura [distribuire un servizio cloud](cloud-services-how-to-create-deploy.md).
* Configurare i [certificati ssl](cloud-services-configure-ssl-certificate.md).

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: http://msdn.microsoft.com/library/ee517253.aspx
[Create a CNAME record that associates the subdomain with the storage account]: #create-cname
[portale di Azure classico]: https://manage.windowsazure.com
[Validate Custom Domain dialog box]: http://i.msdn.microsoft.com/dynimg/IC544437.jpg
[vip]: ./media/cloud-services-custom-domain-name/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name/csurl.png
