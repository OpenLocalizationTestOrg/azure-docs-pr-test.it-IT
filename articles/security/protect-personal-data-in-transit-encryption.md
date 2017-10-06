---
title: dati personali aaaProtect in transito con la crittografia in Azure | Documenti Microsoft
description: Usare la crittografia dei dati personali tooprotect Azure
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 218ad3f49326e8dec299a6d92b18116da65eae71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a>Tecnologie di crittografia di Azure: proteggere i dati personali in transito con la crittografia

In questo articolo consentono di comprendere e utilizzare dati toosecure di tecnologie Azure crittografia in transito. 

Durante il trasferimento in rete hello privacy hello protezione dei dati personali è una parte essenziale di una strategia di sicurezza a più livelli di difesa in profondità. La crittografia in transito è tooprevent progettato un utente malintenzionato intercetta le trasmissioni di dati in grado di hello tooview oppure utilizzare il.

## <a name="scenario"></a>Scenario

Una società crociera di grandi dimensioni, la sede centrale negli Stati Uniti hello espansione relativo itinerari toooffer operazioni Mediterraneo hello, Adriatico e mare Baltico, nonché hello isole britannico. toosupport tali attività, che è stato acquisito più righe crociera inferiori basate in Italia, Germania, Danimarca e hello Regno Unito 

la società Hello utilizza i dati aziendali di Microsoft Azure toostore nel cloud hello. Questi includono informazioni personali come nomi, indirizzi, numeri di telefono e dati delle carte di credito della base clienti globale, Include inoltre informazioni reparto risorse umane tradizionali, ad esempio indirizzi, i numeri di telefono, codici fiscali e informazioni mediche relativi ai dipendenti della società in tutte le posizioni. riga crociera Hello gestisce anche un database di grandi dimensioni di benefici e la fedeltà dei membri del programma che include informazioni personali tootrack relazioni con i clienti correnti e precedenti.

Dati personali di clienti viene inseriti nel database hello da sedi remote della società hello e dagli agenti di viaggio presenti in ogni HelloWorld. Documenti che contengono informazioni sul cliente vengono trasferiti attraverso l'archiviazione di tooAzure rete hello.

## <a name="problem-statement"></a>Presentazione del problema

società Hello necessario proteggere la privacy hello di clienti e dati personali dei dipendenti mentre sono in transito tooand dai servizi di Azure.

## <a name="company-goal"></a>Obiettivo dell'azienda

Hello tooensure obiettivo aziendale che i dati personali vengono crittografati quando dal disco. Se gli utenti non autorizzati intercettano i dati personali di hello off disco, deve essere in un formato che verrà eseguito il rendering illeggibile. L'applicazione della crittografia deve essere facile o completamente trasparente per utenti e amministratori.

## <a name="solutions"></a>Soluzioni

Servizi di Azure forniscono più toohelp strumenti e tecnologie proteggere i dati personali in transito.

### <a name="azure-storage"></a>Archiviazione di Azure

I dati archiviati nel cloud hello devono essere spostata dal client hello, che possono essere collocati fisicamente ovunque nel mondo hello, toohello data center di Azure. Quando i dati vengono recuperati dagli utenti, viene trasferito di nuovo, in hello opposto direzione. Dati in transito su hello rete Internet pubblica vengono sempre al rischio di intercettazione da utenti malintenzionati. È importante tooprotect sulla privacy di hello dei dati personali utilizzando la crittografia a livello di trasporto toosecure come si sposta tra i percorsi.

il protocollo HTTPS Hello fornisce un canale di comunicazione protetto e crittografato su hello Internet. HTTPS deve essere utilizzato tooaccess oggetti nell'archiviazione di Azure e quando si chiama l'API REST. Imporre l'uso del protocollo HTTPS hello quando si utilizza [firme di accesso condiviso](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) oggetti di archiviazione tooAzure accesso toodelegate (SAS). Esistono due tipi di firma di accesso condiviso: del servizio e dell'account.

#### <a name="how-do-i-construct-a-service-sas"></a>Come creare una firma di accesso condiviso del servizio

Servizio SAS delegati accesso tooa risorsa in uno dei servizi di archiviazione hello (servizio blob, coda, tabella o file). un servizio di firma di accesso condiviso, tooconstruct hello seguenti:

1. Specificare hello firmato il campo della versione

2. Specificare hello risorse firmato (Blob e File solo servizio)

3. Specificare i parametri di Query le intestazioni di risposta tooOverride (servizio Blob e File solo servizio)

4. Specificare il nome di tabella (solo servizio tabella) hello

5. Specificare i criteri di accesso hello

6. Specificare l'intervallo di validità della firma hello

8. Specificare le autorizzazioni

9. Specificare l'indirizzo IP o l'intervallo IP

10. Specificare il protocollo HTTP hello

11. Specificare gli intervalli di accesso delle tabelle

12. Specificare l'identificatore firmato hello

13. Specificare hello firma

Per istruzioni più dettagliate, vedere [Constructing a Service SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN) (Creazione di una firma di accesso condiviso del servizio).

#### <a name="how-do-i-construct-an-account-sas"></a>Come creare una firma di accesso condiviso dell'account

Una firma di accesso condiviso delega accesso tooresources in uno o più dei servizi di archiviazione hello. È inoltre possibile delegare accesso tooread, scrittura e le operazioni di eliminazione in contenitori blob, tabelle, code e le condivisioni di file che non sono consentite con un firma di accesso condiviso del servizio. Costruzione di una firma di accesso condiviso è simile toothat una firma di accesso condiviso del servizio. Per istruzioni dettagliate, vedere [Constructing an Account SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN) (Creazione di una firma di accesso condiviso dell'account).

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a>Come imporre HTTPS nella chiamata di API REST

tooenforce hello l'uso di HTTPS durante la chiamata di oggetti di API REST tooaccess negli account di archiviazione è possibile abilitare Secure trasferimento necessari per l'account di archiviazione hello. 

1. Nel portale di Azure hello, selezionare **crea Account di archiviazione**, o per un account di archiviazione esistente, selezionare **impostazioni** e quindi **configurazione**.

2. In **Trasferimento sicuro obbligatorio** selezionare **Abilitato**.

![Creazione di un account di archiviazione](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

Per istruzioni più dettagliate, incluso come tooenable Secure trasferimento necessarie a livello di codice, vedere [richiedono Secure trasferimento](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a>Come crittografare i dati in Archiviazione file di Azure

tooencrypt dati in transito con [archiviazione File di Azure](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), è possibile utilizzare SMB 3. x con Windows 8, 8.1 e 10 e Windows Server 2012 R2 e Windows Server 2016. Quando si utilizza il servizio di Azure file hello, qualsiasi connessione senza crittografia ha esito negativo quando la "Protezione di trasferimento richiesto" è abilitate. Sono inclusi scenari con alcune varianti di hello client Linux SMB, SMB 2.1 e SMB 3.0 senza crittografia.

#### <a name="azure-client-side-encryption"></a>Crittografia lato client di Azure

Un'altra opzione per proteggere i dati personali durante il trasferimento tra un'applicazione client e Archiviazione di Azure è la [crittografia lato client](https://docs.microsoft.com/azure/storage/storage-client-side-encryption). Hello dati vengono crittografati prima di essere trasferiti nell'archiviazione di Azure e quando si recuperano dati hello da archiviazione di Azure, dati hello viene decrittografati dopo la ricezione sul lato client hello.

### <a name="azure-site-to-site-vpn"></a>VPN da sito a sito di Azure

Un modo efficace tooprotect personali di dati in transito tra una rete aziendale o utente e hello rete virtuale di Azure sono toouse un [site-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) o [point-to-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) rete privata virtuale (VPN, Virtual Private Network). Una connessione VPN crea un canale crittografato protetto tra hello Internet.

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a>Come creare una connessione VPN da sito a sito

Una VPN da sito a sito si connette a più utenti su hello tooAzure di rete aziendale. una connessione site-to-site nel portale di Azure hello toocreate hello seguenti:

1. Creare una rete virtuale.

2. Specificare un server DNS

3. Creare subnet del gateway hello.

4. Creare il gateway VPN hello. 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. Creare il gateway di rete locale hello.

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. Configurare il dispositivo VPN.

7. Creare la connessione VPN hello.

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. Verificare una connessione VPN hello.

Per istruzioni dettagliate su come connessione toocreate una site-to-site in hello Azure portale, vedere [connessione di creare un sito a sito nel portale di Azure hello]. (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a>Come creare una connessione VPN da punto a sito

Una VPN Point-to-Site consente di creare una connessione sicura da una rete virtuale di computer tooa singoli client. Ciò è utile quando si desidera tooAzure tooconnect da una posizione remota, ad esempio dall'area home o un hotel conferenza. una connessione point-to-site nel portale di Azure hello toocreate

1. Creare una rete virtuale.

2. Aggiungere una subnet del gateway.

3. Specificare un server DNS (facoltativo).

4. Creare un gateway di rete virtuale.

5. Generare i certificati.

6. Aggiungere pool di indirizzi hello client.

7. Caricare dati certificato pubblica del certificato radice hello.

8. Generare e installare il pacchetto di configurazione client VPN di hello.

9. Installare un certificato client esportato.

10. Connettersi tooAzure.

11. Verificare la connessione.

Per istruzioni dettagliate, vedere [configurare un tooa connessione Point-to-Site rete virtuale utilizzando l'autenticazione del certificato: portale di Azure.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)

### <a name="ssltls"></a>SSL/TLS

Si consiglia di utilizzare sempre dati tooexchange di protocolli SSL/TLS in posizioni diverse. Le organizzazioni che scelgono toouse [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove grandi set di dati in un collegamento WAN ad alta velocità dedicato inoltre possibile crittografare i dati hello hello utilizzando SSL/TLS o altri protocolli per una maggiore protezione a livello di applicazione.

### <a name="encryption-by-default"></a>Crittografia predefinita

Microsoft utilizza i dati di tooprotect crittografia in transito tra clienti e i servizi cloud di Azure. Se si interagisce con l'archiviazione di Azure tramite il portale di Azure hello, tutte le transazioni si verificano tramite HTTPS.

[Livello di sicurezza del trasporto](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) è protocollo hello che data center Microsoft tenterà toonegotiate con i sistemi client che si connettono a servizi cloud tooMicrosoft. TLS offre autenticazione avanzata, privacy e integrità dei messaggi (supportando il rilevamento di manomissioni, intercettazioni e falsificazioni di messaggi), interoperabilità, flessibilità degli algoritmi e facilità di distribuzione e uso.

Viene anche usata la funzionalità [Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) affinché ogni connessione tra i sistemi client dei clienti e i servizi cloud Microsoft usi chiavi univoche. Servizi cloud di connessioni tooMicrosoft inoltre sfruttare basato su RSA 2048 bit crittografia lunghezze di chiave. combinazione di TLS, lunghezze delle chiavi RSA 2048 bit, Hello e PFS rende molto più difficile a qualcuno toointercept e accedere ai dati in transito tra clienti e i servizi cloud Microsoft.

I dati in transito sono sempre crittografati in [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview). Inoltre supporto toopersistent toostoring precedenti dati tooencrypting hello dati vengono sempre anche protetti in transito tramite HTTPS. HTTPS è l'unico protocollo hello è supportato per hello che interfacce REST di archivio Data Lake.

## <a name="summary"></a>Riepilogo

Per eseguire l'obiettivo di protezione sulla privacy di hello e dati personale di tali dati dall'applicazione tooAzure connessioni HTTPS archiviazione, tramite firme di accesso condiviso e l'abilitazione di Secure trasferimento necessarie sugli account di archiviazione hello società Hello. Può anche proteggere i dati personali usando connessioni SMB 3.0 e implementando la crittografia lato client. Le connessioni VPN da sito a sito da hello rete aziendale toohello rete virtuale di Azure e le connessioni VPN point-to-site da singoli utenti creerà un tunnel sicuro tramite cui possono essere trasmessi in modo sicuro i dati personali. Procedure consigliate di crittografia predefinita di Microsoft verranno proteggere ulteriormente privacy hello dei dati personali.

## <a name="next-steps"></a>Passaggi successivi

- [Procedure consigliate per la sicurezza dei dati e la crittografia in Azure](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [Pianificazione e progettazione per il gateway VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [Domande frequenti sul gateway VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [Acquistare e configurare un certificato SSL per il servizio app di Azure](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
