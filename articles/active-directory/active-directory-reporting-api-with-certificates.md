---
title: utilizzando dati aaaGet hello API Azure AD Reporting con certificati | Documenti Microsoft
description: Viene illustrato come toouse hello API Azure AD Reporting con dati tooget le credenziali del certificato dalla directory senza intervento dell'utente.
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a>Acquisizione di dati utilizzando l'API di Reporting di hello Azure AD con certificati
Questo articolo illustra come toouse hello API Azure AD Reporting con dati tooget le credenziali del certificato dalla directory senza intervento dell'utente. 

## <a name="use-hello-azure-ad-reporting-api"></a>Utilizzare hello API Azure AD Reporting 
API Azure AD Reporting richiede di completare hello alla procedura seguente:
 *  Installare i componenti prerequisiti
 *  Impostare il certificato hello nell'app
 *  Ottenere un token di accesso
 *  Utilizzare hello toocall token di accesso hello API Graph

Per informazioni sul codice sorgente, vedere [Sfruttare il modulo dell'API di creazione report](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils). 

### <a name="install-prerequisites"></a>Installare i componenti prerequisiti
Sarà necessario toohave Azure AD PowerShell V2 e AzureADUtils modulo installato.

1. Scaricare e installare Azure AD Powershell V2, attenendosi alle istruzioni hello in [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).
2. Scaricare il modulo di Azure AD Utils hello da [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1). 
  Questo modulo offre diversi cmdlet di utilità, tra cui:
   * versione più recente di Hello della libreria ADAL tramite Nuget
   * Token di accesso dell'utente, chiavi dell'applicazione e certificati con ADAL
   * API Graph che gestisce i risultati di paging

**modulo di Azure AD Utils tooinstall hello:**

1. Creare un modulo di utilità hello toosave directory (ad esempio, c:\azureAD) e scaricare il modulo di hello da GitHub.
2. Aprire una sessione di PowerShell e passare toohello directory che appena creata. 
3. Importare il modulo hello e installarlo nel percorso di modulo di PowerShell hello utilizzando il cmdlet Install-AzureADUtilsModule hello. 

sessione Hello dovrebbe essere simile toothis schermo:

  ![Windows Powershell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a>Impostare il certificato hello nell'app
1. Se si dispone già di un'app, è possibile ottenere l'ID di oggetto da hello portale di Azure. 

  ![Portale di Azure](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. Aprire una sessione di PowerShell e connettersi AD tooAzure utilizzando il cmdlet Connect-AzureAD hello.

  ![Portale di Azure](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. Utilizzare il cmdlet New-AzureADApplicationCertificateCredential hello da AzureADUtils tooadd tooit di credenziali un certificato. 

>[!Note]
>È necessaria un'applicazione hello tooprovide ID di oggetto acquisita in precedenza, nonché hello oggetto certificato (ottenere questa operazione utilizzando hello Cert: unità).
>


  ![Portale di Azure](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a>Ottenere un token di accesso

tooget un token di accesso, utilizzare il cmdlet Get-AzureADGraphAPIAccessTokenFromCert hello da AzureADUtils. 

>[!NOTE]
>È necessario toouse hello ID applicazione anziché hello ID di oggetto utilizzati nell'ultima sezione hello.
>

 ![Portale di Azure](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a>Utilizzare hello toocall token di accesso hello API Graph

È ora possibile creare script hello. Di seguito è riportato un esempio, tramite il cmdlet Invoke-AzureADGraphAPIQuery hello da hello AzureADUtils. Questo cmdlet gestisce i risultati con più pagine e quindi invia tali pipeline di PowerShell toohello risultati. 

 ![Portale di Azure](./media/active-directory-report-api-with-certificates/script-completed.png)

Si sono ora pronti tooexport tooa CSV e Salva sistema SIEM tooa. È possibile anche includere lo script in un tooget attività pianificata, i dati di Azure AD dal tenant periodicamente senza chiavi applicazione toostore nel codice sorgente hello. 

## <a name="next-steps"></a>Passaggi successivi
[Nozioni fondamentali su Hello della gestione delle identità di Azure](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



