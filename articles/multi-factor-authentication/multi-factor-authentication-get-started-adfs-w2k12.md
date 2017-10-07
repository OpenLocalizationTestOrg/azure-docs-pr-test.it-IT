---
title: Server con AD FS in Windows Server aaaMFA | Documenti Microsoft
description: "Questo articolo descrive la modalità di avvio tooget con Azure multi-Factor Authentication e ADFS in Windows Server 2012 R2 e 2016."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 57208068-1e55-45b6-840f-fdcd13723074
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/29/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 656785abcc63a020add765a86670b488a3b84b51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-toowork-with-ad-fs-in-windows-server"></a>Configurare il Server Azure multi-Factor Authentication toowork con AD FS in Windows Server
Se si utilizza Active Directory Federation Services (ADFS) e si desidera che le risorse cloud o locale toosecure, è possibile configurare il Server Azure multi-Factor Authentication toowork con AD FS. Questa configurazione attiva la verifica in due passaggi per gli endpoint di alto valore.

Questo articolo illustra l'uso del server Azure Multi-Factor Authentication con AD FS in Windows Server 2012 R2 o Windows Server 2016. Per ulteriori informazioni, consultare le informazioni su troppo[proteggere le risorse cloud e locali tramite il Server Azure multi-Factor Authentication con AD FS 2.0](multi-factor-authentication-get-started-adfs-adfs2.md).

## <a name="secure-windows-server-ad-fs-with-azure-multi-factor-authentication-server"></a>Proteggere AD FS per Windows Server con il server Azure Multi-Factor Authentication
Quando si installa il Server Azure multi-Factor Authentication, è necessario hello le opzioni seguenti:

* Installare il Server Azure multi-Factor Authentication in hello locale nello stesso server AD FS
* Installare adapter Azure multi-Factor Authentication hello in hello server ADFS locale e quindi installare Server multi-Factor Authentication in un computer diverso

Prima di iniziare, tenere hello le seguenti informazioni:

* Non è necessario tooinstall Server Azure multi-Factor Authentication nel server ADFS. Tuttavia, è necessario installare l'adapter multi-Factor Authentication hello per ADFS in un Windows Server 2012 R2 o Windows Server 2016 che esegue AD FS. Se si tratta di una versione supportata e si installa scheda ADFS hello separatamente nel server federativo ADFS, è possibile installare server hello in un computer diverso. Vedere hello seguendo procedure toolearn come tooinstall hello scheda separatamente.
* Se l'organizzazione utilizza messaggio di testo o i metodi di verifica app per dispositivi mobili, le stringhe di hello definite nelle impostazioni società contengono un segnaposto, <$*application_name*$>. Nel server MFA 7.1 è possibile specificare il nome di un'applicazione per sostituire questo segnaposto. Nella versione 7.0 o precedenti, il segnaposto non viene sostituito automaticamente quando si utilizza l'adapter di hello AD FS. Rimuovere segnaposto hello da stringhe appropriate hello per le versioni precedenti, quando si protegge ADFS.
* Hello che l'account utilizzato toosign in deve avere gruppi di sicurezza toocreate diritti utente nel servizio Active Directory.
* installazione guidata di ADFS di multi-Factor Authentication Hello adapter crea un gruppo di sicurezza denominato PhoneFactor Admins nella propria istanza di Active Directory. Viene quindi aggiunto l'account del servizio ADFS hello del gruppo toothis servizio federativo. Verificare nel controller di dominio che hello effettiva creazione del gruppo PhoneFactor Admins e che l'account del servizio hello AD FS è un membro di questo gruppo. Se necessario, aggiungere manualmente toohello account di servizio AD FS hello gruppo PhoneFactor Admins nel controller di dominio.
* Per informazioni sull'installazione hello Web Service SDK con il portale utenti hello, conoscenza [distribuzione portale per gli utenti hello per il Server Azure multi-Factor Authentication.](multi-factor-authentication-get-started-portal.md)

### <a name="install-azure-multi-factor-authentication-server-locally-on-hello-ad-fs-server"></a>Installare il Server Azure multi-Factor Authentication in locale nel server AD FS hello
1. Scaricare e installare il server Azure Multi-Factor Authentication nel server ADFS. Per informazioni sull'installazione, vedere [Introduzione al server Azure Multi-Factor Authentication](multi-factor-authentication-get-started-server.md).
2. Nella console di gestione di hello del Server Azure multi-Factor Authentication, fare clic su hello **ADFS** icona. Selezionare le opzioni di hello **Consenti registrazione utente** e **consentire agli utenti il metodo tooselect**.
3. Selezionare eventuali opzioni aggiuntive che si desidera toospecify per l'organizzazione.
4. Fare clic su **Installa scheda ADFS**.
   
   <center>![Cloud](./media/multi-factor-authentication-get-started-adfs-w2k12/server.png)</center>

5. Se viene visualizzata la finestra di Active Directory hello, significa che due elementi. Il computer è tooa aggiunti a un dominio e configurazione di Active Directory hello per proteggere la comunicazione tra l'adattatore ADFS hello Active Directory e il servizio multi-Factor Authentication hello è incompleta. Fare clic su **Avanti** tooautomatically completare la configurazione o selezionare hello **Ignora configurazione automatica di Active Directory e configurare le impostazioni manualmente** casella di controllo. Fare clic su **Avanti**.
6. Se windows Local Group hello è visualizzato, significa che due elementi. Il computer non è unita in join tooa dominio e configurazione gruppo locale di hello per proteggere la comunicazione tra l'adattatore ADFS hello Active Directory e il servizio multi-Factor Authentication hello è incompleta. Fare clic su **Avanti** tooautomatically completare la configurazione o selezionare hello **Ignora configurazione automatica di gruppo locale e configurare le impostazioni manualmente** casella di controllo. Fare clic su **Avanti**.
7. Hello installazione guidata fare clic su **Avanti**. Azure multi-Factor Authentication Server Crea gruppo PhoneFactor Admins hello e aggiunge toohello account di servizio AD FS hello gruppo PhoneFactor Admins.
   <center>![Cloud](./media/multi-factor-authentication-get-started-adfs-w2k12/adapter.png)</center>
8. In hello **Avvia programma di installazione** pagina, fare clic su **Avanti**.
9. Nel programma di installazione scheda ADFS di multi-Factor Authentication hello, fare clic su **Avanti**.
10. Fare clic su **Chiudi** termine installazione hello.
11. Quando l'adapter hello è stato installato, è necessario registrarlo con AD FS. Aprire Windows PowerShell ed eseguire hello comando seguente:<br>
    `C:\Program Files\Multi-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1`
    <center>![Cloud](./media/multi-factor-authentication-get-started-adfs-w2k12/pshell.png)</center>
12. toouse la scheda appena registrata, modifica i criteri di autenticazione globali hello in ADFS. Nella console di gestione di hello AD ADFS, passare toohello **criteri di autenticazione** nodo. In hello **multi-factor Authentication** fare clic su hello **modifica** collegamento successivo toohello **impostazioni globali** sezione. In hello **Modifica criteri di autenticazione globali** selezionare **multi-Factor Authentication** come metodo di autenticazione aggiuntivo e quindi fare clic su **OK**. Hello scheda viene registrata come WindowsAzureMultiFactorAuthentication. Riavviare il servizio ADFS hello Active Directory per effetto di tootake registrazione hello.

<center>![Cloud](./media/multi-factor-authentication-get-started-adfs-w2k12/global.png)</center>

A questo punto, multi-Factor Authentication Server è configurato toobe un toouse di provider di autenticazione aggiuntivi con AD FS.

## <a name="install-a-standalone-instance-of-hello-ad-fs-adapter-by-using-hello-web-service-sdk"></a>Installare un'istanza autonoma di adapter hello ADFS utilizzando hello Web Service SDK
1. Installare hello SDK servizio Web nel server di hello che esegue Server multi-Factor Authentication.
2. Esempio hello copia i file dalla \programmi\multi-factor hello-server di toohello directory Server Factor Authentication su cui si prevede di adapter di tooinstall hello AD FS:
   * MultiFactorAuthenticationAdfsAdapterSetup64.msi
   * Register-MultiFactorAuthenticationAdfsAdapter.ps1
   * Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
   * MultiFactorAuthenticationAdfsAdapter.config
3. Eseguire i file di installazione di hello i file MultiFactorAuthenticationAdfsAdapterSetup64.msi.
4. Nel programma di installazione scheda ADFS di multi-Factor Authentication hello, fare clic su **Avanti** installazione hello toostart.
5. Fare clic su **Chiudi** termine installazione hello.

## <a name="edit-hello-multifactorauthenticationadfsadapterconfig-file"></a>Modifica file Multifactorauthenticationadfsadapter config hello
Seguire questi file multifactorauthenticationadfsadapter. config di passaggi tooedit hello:

1. Set hello **UseWebServiceSdk** nodo troppo**true**.  
2. Impostare il valore di hello per **WebServiceSdkUrl** toohello URL di hello multi-Factor Authentication Web Service SDK. Ad esempio: *https://contoso.com/&lt;certificatename&gt;/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx*, dove *certificatename* hello nome del certificato.  
3. Modifica di script hello Register-multifactorauthenticationadfsadapter.ps1 aggiungendo *- ConfigurationFilePath &lt;percorso&gt;*  toohello fine hello `Register-AdfsAuthenticationProvider` comando, in cui  *&lt;percorso&gt;*  hello percorso completo toohello multifactorauthenticationadfsadapter. config file.

### <a name="configure-hello-web-service-sdk-with-a-username-and-password"></a>Configurare hello Web Service SDK con un nome utente e password
Sono disponibili due opzioni per la configurazione di hello SDK servizio Web. con un nome utente e una password per primo è Hello, hello in secondo luogo è con un certificato client. Seguire questi passaggi per la prima opzione hello o ignorare per hello secondo.  

1. Impostare il valore di hello per **WebServiceSdkUsername** tooan account che è un membro del gruppo di sicurezza PhoneFactor Admins hello. Hello utilizzare &lt;dominio&gt;&#92;&lt; nome utente&gt; formato.  
2. Impostare il valore di hello per **webservicesdkpassword sulla** toohello password dell'account appropriata.

### <a name="configure-hello-web-service-sdk-with-a-client-certificate"></a>Configurare hello Web Service SDK con un certificato client
Se non si desidera toouse un nome utente e una password, seguire questi hello di passaggi tooconfigure Web Service SDK con un certificato client.

1. Ottenere un certificato client da un'autorità di certificazione per il server hello hello Web Service SDK in esecuzione. Informazioni su come troppo[ottenere i certificati client](https://technet.microsoft.com/library/cc770328.aspx).  
2. Importazione hello archivio certificati client toohello computer locale dei certificati personali nel server di hello hello Web Service SDK in esecuzione. Verificare che certificato pubblico dell'autorità di certificazione che hello sia nell'archivio certificati di certificati radice attendibili.  
3. Esportare le chiavi pubbliche e private di hello hello client tooa pfx del file di certificato.  
4. Esportare la chiave pubblica di hello nel file con estensione cer tooa in formato Base64.  
5. In Server Manager, verificare che la funzionalità di autenticazione Mapping certificati Client hello \Web Server\Security\IIS Server Web (IIS) sia installato. Se non è installato, selezionare **Aggiungi ruoli e funzionalità** tooadd questa funzionalità.  
6. In Gestione IIS, fare doppio clic su **Editor di configurazione** nel sito Web di hello contenente le directory virtuali di hello SDK servizio Web. Sito Web di hello tooselect importanti, non una directory virtuale hello è.  
7. Passare toohello **system.webServer/security/authentication/iisClientCertificateMappingAuthentication** sezione.  
8. Impostare enabled troppo**true**.  
9. Impostare oneToOneCertificateMappingsEnabled troppo**true**.  
10. Fare clic su hello **...**  pulsante toooneToOneMappings avanti e quindi fare clic su hello **Aggiungi** collegamento.  
11. Aprire file con estensione cer Base64 hello esportato in precedenza. Rimuovere *-----BEGIN CERTIFICATE-----*, *-----END CERTIFICATE-----* e tutte le interruzioni di riga. Copiare la stringa risultante hello.  
12. Set certificato toohello stringa copiata nel passaggio precedente hello.  
13. Impostare enabled troppo**true**.  
14. Impostare userName tooan account è un membro del gruppo di sicurezza PhoneFactor Admins hello. Hello utilizzare &lt;dominio&gt;&#92;&lt; nome utente&gt; formato.  
15. Impostare la password di hello password toohello account appropriato e quindi chiudere l'Editor di configurazione.  
16. Fare clic su hello **applica** collegamento.  
17. Nella directory virtuale Web Service SDK hello, fare doppio clic su **autenticazione**.  
18. Verificare che la rappresentazione ASP.NET e l'autenticazione di base impostata troppo**abilitato**, e che tutti gli altri elementi siano impostate troppo**disabilitato**.  
19. Nella directory virtuale Web Service SDK hello, fare doppio clic su **impostazioni SSL**.  
20. Impostare certificati Client troppo**Accept**, quindi fare clic su **applica**.  
21. Copiare file con estensione pfx hello esportato precedenti toohello server che esegue hello scheda ADFS.  
22. Importare l'archivio certificati personali di hello. pfx file toohello computer locale.  
23. Mouse e scegliere **Gestisci chiavi Private**e quindi concedere l'accesso in lettura toohello account usato toosign nel servizio di toohello AD ADFS.  
24. Aprire hello certificato e copia hello identificazione personale del client da hello **dettagli** scheda.  
25. Nel file multifactorauthenticationadfsadapter. config hello impostare **WebServiceSdkCertificateThumbprint** toohello stringa copiata nel passaggio precedente hello.  

Infine, tooregister hello adapter, eseguire \programmi\multi-factor hello-Factor Authentication Server\register-multifactorauthenticationadfsadapter.ps1 script di PowerShell. Hello scheda viene registrata come WindowsAzureMultiFactorAuthentication. Riavviare il servizio ADFS hello Active Directory per effetto di tootake registrazione hello.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>Proteggere le risorse Azure AD con ADFS
toosecure la risorsa cloud, impostare una regola attestazioni, in modo che Active Directory Federation Services genera hello multipleauthn attestazione quando un utente esegue la verifica completata. Questa attestazione viene passata in tooAzure Active Directory. Seguire questa procedura toowalk passaggi hello:

1. Aprire il componente di gestione di ADFS.
2. A sinistra di hello, selezionare **Relying Party Trusts**.
3. Fare clic con il pulsante destro del mouse su **Piattaforma delle identità di Microsoft Office 365** e selezionare **Modifica regole attestazione...**

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. In Regole di trasformazione rilascio fare clic su **Aggiungi regola**.

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. In aggiunta guidata regole attestazione trasformare hello, selezionare **Pass Through or Filter an Incoming Claim** hello elenco a discesa e fare clic su **Avanti**.

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. Assegnare un nome alla regola.
7. Selezionare **riferimenti dei metodi di autenticazione** come hello in arrivo tipo di attestazione.
8. Selezionare **Pass-through di tutti i valori attestazione**.
    ![Aggiunta guidata regole attestazione di trasformazione](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. Fare clic su **Finish**. Chiudere la console di gestione di ADFS hello Active Directory.

## <a name="related-topics"></a>Argomenti correlati
Per la risoluzione dei problemi, vedere hello [domande frequenti di Azure multi-Factor Authentication](multi-factor-authentication-faq.md)
