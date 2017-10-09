---
title: un nome di dominio personalizzato in servizi Cloud aaaConfigure | Documenti Microsoft
description: Informazioni su come tooexpose applicazione Azure o ai dati in un dominio personalizzato, configurare le impostazioni DNS.
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
ms.openlocfilehash: 71e553a73b40a8d0512b4d40173500561841772c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a>Configurazione di un nome di dominio personalizzato per un servizio cloud di Azure
> [!div class="op_single_selector"]
> * [Portale di Azure](cloud-services-custom-domain-name-portal.md)
> * [portale di Azure classico](cloud-services-custom-domain-name.md)
> 
> 

Quando si crea un servizio Cloud, Azure assegna tooa sottodominio di cloudapp.net. Ad esempio, se il servizio Cloud denominato "contoso", gli utenti verranno essere in grado di tooaccess l'applicazione in un URL come http://contoso.cloudapp.net. Azure assegna anche un indirizzo IP virtuale.

È tuttavia possibile esporre l'applicazione in un nome di dominio personalizzato, ad esempio contoso.com. Questo articolo viene illustrato come tooreserve o configurare un nome di dominio personalizzato per i ruoli web del servizio Cloud.

Se si conoscono già i record CNAME e A, [Jump oltre hello spiegazione](#add-a-cname-record-for-your-custom-domain).

> [!NOTE]
> Per velocizzare le operazioni, Hello utilizzare Azure [interattiva procedura dettagliata](http://support.microsoft.com/kb/2990804). Grazie alla procedura guidata, è facile associare un nome di dominio personalizzato e proteggere le comunicazioni (SSL) con i Servizi cloud di Azure o Siti Web di Azure.
> 
> 

<p/>

> [!NOTE]
> procedure Hello in questa attività si applicano i servizi Cloud tooAzure. Per Servizi app, vedere [questo articolo](../app-service-web/web-sites-custom-domain-name.md). Per gli account di archiviazione, vedere [questo articolo](../storage/blobs/storage-custom-domain-name.md).
> 
> 

## <a name="understand-cname-and-a-records"></a>Informazioni sui record CNAME e A
CNAME (o record di alias) e un record sia consentono tooassociate un nome di dominio con un server specifico (o del servizio in questo caso,) tuttavia funzionano in modo diverso. Esistono inoltre alcune considerazioni specifiche quando si utilizza un record con i servizi Cloud di Azure che è necessario considerare prima di decidere quale toouse.

### <a name="cname-or-alias-record"></a>Record CNAME o Alias
Esegue il mapping di un record CNAME un *specifico* dominio, ad esempio **contoso.com** o **www.contoso.com**, il nome di dominio canonico tooa. In questo caso, il nome di dominio canonico hello è hello **.cloudapp [myapp] .net** applicazione host del dominio di Azure. Una volta creato, hello CNAME crea un alias per hello **.cloudapp [myapp] .net**. Hello voce CNAME risolverà l'indirizzo IP del toohello il **.cloudapp [myapp] .net** service automaticamente, se l'indirizzo IP di hello del servizio cloud hello viene modificato, non è tootake alcuna azione.

> [!NOTE]
> Alcuni Registrar consentono solo i sottodomini toomap quando si utilizza un record CNAME, ad esempio www.contoso.com e non i nomi radice, ad esempio contoso.com. Per ulteriori informazioni sui record CNAME, vedere la documentazione di hello fornita dal registrar, [hello di Wikipedia sul record CNAME](http://en.wikipedia.org/wiki/CNAME_record), o hello [i nomi di dominio IETF - implementazione e specifiche](http://tools.ietf.org/html/rfc1035) documento.
> 
> 

### <a name="a-record"></a>Record A
Esegue il mapping, ad esempio un record A un dominio, **contoso.com** o **www.contoso.com**, *o in un dominio con caratteri jolly* , ad esempio  **\*. contoso.com**, indirizzo IP tooan. Nel caso di hello di un servizio Cloud di Azure, hello IP virtuale del servizio hello. Vantaggio principale di hello di un record in un record CNAME è che è possibile avere una voce che utilizza un carattere jolly, ad esempio \* **. contoso.com**, che si gestisce le richieste per più sottodomini, ad esempio  **Mail.contoso.com**, **login.contoso.com**, o **www.contso.com**.

> [!NOTE]
> Poiché viene eseguito il mapping di un record di indirizzo IP statico tooa, in grado di risolvere automaticamente le modifiche toohello IP indirizzo del servizio Cloud. indirizzo IP di Hello utilizzato dal servizio Cloud viene allocato hello prima volta che si distribuisce tooan slot vuoto (produzione o gestione temporanea.) Se si elimina la distribuzione di hello per slot hello, indirizzo IP di hello viene rilasciato da Azure e qualsiasi slot toohello distribuzioni future può essere assegnato un nuovo indirizzo IP.
> 
> Per praticità, indirizzo IP hello di uno slot di distribuzione specificata (produzione o gestione temporanea) viene mantenuto quando si passa tra l'esecuzione di un aggiornamento sul posto di una distribuzione esistente e le distribuzioni di produzione o gestione temporanea. Per ulteriori informazioni sull'esecuzione di queste azioni, vedere [come servizi cloud toomanage](cloud-services-how-to-manage.md).
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a>Aggiunta di un record CNAME per il dominio personalizzato
toocreate un record CNAME, è necessario aggiungere una nuova voce nella tabella di hello DNS per il dominio personalizzato tramite strumenti hello forniti dal registrar. Ogni autorità di registrazione è un metodo simile, ma leggermente diverso per specificare un record CNAME, ma hello concetti sono hello stesso.

1. Utilizzare uno di questi hello toofind metodi **. cloudapp.net** nome di dominio del servizio cloud tooyour assegnato.
   
   * Account di accesso toohello [portale di Azure classico], selezionare il servizio cloud, **Dashboard**e quindi individuare hello **URL del sito** voce hello **riepilogo rapido**  sezione.
     
       ![sezione di riepilogo rapido che mostra l'URL del sito hello][csurl]
     
       **OR**  
   * Installare e configurare [Azure Powershell](/powershell/azure/overview), e quindi utilizzare hello finestra di comando seguente:
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     Salvare il nome di dominio hello utilizzato nell'URL di hello restituito da dei metodi, perché sarà necessaria quando si crea un record CNAME.
2. Accedere al sito Web del registrar DNS tooyour e toohello pagina per la gestione DNS passare. Cercare i collegamenti o aree del sito hello etichettata come **nome di dominio**, **DNS**, o **denomina Gestione Server**.
3. Trovare la sezione in cui è possibile selezionare o immettere CNAME. Potrebbe essere record hello tooselect digitare un elenco a discesa oppure passare tooan pagina Impostazioni avanzate. È consigliabile cercare parole hello **CNAME**, **Alias**, o **sottodomini**.
4. È inoltre necessario specificare hello dominio o sottodominio di alias per hello CNAME, ad esempio **www** se si desidera toocreate un alias per **www.customdomain.com**. Se si desidera toocreate un alias per il dominio radice hello, potrebbe essere elencato come hello '**@**' simbolo negli strumenti DNS del registrar.
5. A questo punto, occorre fornire un nome host canonico, che in questo caso corrisponde al dominio **cloudapp.net** .

Ad esempio, hello seguente record CNAME inoltra tutto il traffico da **www.contoso.com** troppo**contoso.cloudapp.net**, il nome di dominio personalizzato hello dell'applicazione distribuita:

| Alias/Nome host/Sottodominio | Dominio canonico |
| --- | --- |
| www |contoso.cloudapp.net |

Un visitatore di **www.contoso.com** non vedranno mai host true hello (contoso.cloudapp.net), in modo hello processo di inoltro è l'utente finale toothe invisibile.

> [!NOTE]
> Hello esempio precedente si applica solo tootraffic in hello **www** sottodominio. Poiché non è possibile usare caratteri jolly con i record CNAME, è necessario crearne uno per ogni dominio/sottodominio. Se si desidera che il traffico toodirect da sottodomini, ad esempio \*. contoso.com, l'indirizzo di cloudapp.net tooyour, è possibile configurare un **Reindirizzamento URL** o **URL rollforward** voce nelle impostazioni DNS, o creare un record A.
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a>Aggiungere un record A per il dominio personalizzato
toocreate un record, è necessario trovare indirizzi IP virtuali hello del servizio cloud. Aggiungere quindi una nuova voce nella tabella di hello DNS per il dominio personalizzato tramite strumenti hello forniti dal registrar. Ogni autorità di registrazione è un metodo simile, ma leggermente diverso della specifica di un record A, ma hello concetti sono hello stesso.

1. Utilizzare uno dei seguenti metodi tooget hello indirizzo del servizio cloud hello.
   
   * account di accesso toohello [portale di Azure classico], selezionare il servizio cloud, **Dashboard**e quindi individuare hello **indirizzo IP virtuale pubblico (VIP)** voce hello **riepilogo rapido** sezione.
     
       ![sezione di riepilogo rapido che illustra hello VIP][vip]
     
       **OR**  
   * Installare e configurare [Azure Powershell](/powershell/azure/overview), e quindi utilizzare hello finestra di comando seguente:
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     Se si dispone di più endpoint associati al servizio cloud, si riceverà più le righe contenenti l'indirizzo IP di hello, ma tutti deve essere visualizzato hello stesso indirizzo.
     
     Salva l'indirizzo IP di hello, perché sarà necessaria quando si crea un record A.
2. Accedere al sito Web del registrar DNS tooyour e toohello pagina per la gestione DNS passare. Cercare i collegamenti o aree del sito hello etichettata come **nome di dominio**, **DNS**, o **denomina Gestione Server**.
3. Trovare la sezione in cui è possibile selezionare o immettere i record A. Potrebbe essere record hello tooselect digitare un elenco a discesa oppure passare tooan pagina Impostazioni avanzate.
4. Selezionare o immettere il dominio di hello o un sottodominio che verrà utilizzato il record A. Ad esempio, selezionare **www** se si desidera toocreate un alias per **www.customdomain.com**. Se si desidera toocreate una voce con caratteri jolly per tutti i sottodomini, immettere '__*__'. In questo modo verranno inclusi tutti i sottodomini, ad esempio **mail.customdomain.com**, **login.customdomain.com** e **www.customdomain.com**.
   
    Se si desidera toocreate un record per il dominio radice hello, potrebbe essere elencato come hello '**@**' simbolo negli strumenti DNS del registrar.
5. Immettere l'indirizzo IP di hello del servizio cloud nel campo fornito hello. In questo modo viene voce di dominio hello utilizzata nel record A hello con indirizzo IP hello la distribuzione del servizio cloud.

Ad esempio, dopo un record di hello inoltra tutto il traffico da **contoso.com** troppo**137.135.70.239**, hello indirizzo IP dell'applicazione distribuita:

| Nome host/Sottodominio | Indirizzo IP |
| --- | --- |
| @ |137.135.70.239 |

In questo esempio viene illustrata la creazione di un record A per il dominio radice hello. Se si desidera toocreate un toocover voce jolly tutti i sottodomini, immettere '__*__' come sottodominio hello.

> [!WARNING]
> Gli indirizzi IP in Azure sono dinamici per impostazione predefinita. Probabilmente si desidererà toouse un [degli indirizzi IP riservati](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure che l'indirizzo IP non cambia.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* [Come tooManage dei servizi Cloud](cloud-services-how-to-manage.md)
* [Come tooMap CDN contenuto tooa dominio personalizzato](../cdn/cdn-map-content-to-custom-domain.md)
* [Configurazione generale del servizio cloud](cloud-services-how-to-configure.md).
* Informazioni su come troppo[distribuire un servizio cloud](cloud-services-how-to-create-deploy.md).
* Configurare i [certificati ssl](cloud-services-configure-ssl-certificate.md).

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: http://msdn.microsoft.com/library/ee517253.aspx
[Create a CNAME record that associates hello subdomain with hello storage account]: #create-cname
[portale di Azure classico]: https://manage.windowsazure.com
[Validate Custom Domain dialog box]: http://i.msdn.microsoft.com/dynimg/IC544437.jpg
[vip]: ./media/cloud-services-custom-domain-name/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name/csurl.png
