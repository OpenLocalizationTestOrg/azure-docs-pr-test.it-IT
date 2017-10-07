---
title: autenticazione non interattivo aaaCreate HDInsight .NET OLAF - Azure | Documenti Microsoft
description: Informazioni su come applicazioni di HDInsight .NET toocreate autenticazione non interattivo.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 8e32430f-6404-498a-9fcd-f20338d964af
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 5367c160b0146e6b855486b95f363e8fe7f1c98f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a>Creare applicazioni .NET HDInsight di autenticazione non interattive
È possibile eseguire l'applicazione .NET Azure HDInsight con identità dell'applicazione (non interattivo) o con identità hello di hello utente connesso di un'applicazione hello (interattiva). Per un esempio di un'applicazione hello interattivo, vedere [connettersi tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight). In questo articolo illustra come toocreate interattivo autenticazione .NET applicazione tooconnect tooAzure e gestire HDInsight.

Dall'applicazione .NET non interattiva, è necessario disporre degli elementi seguenti:

* ID tenant della sottoscrizione di Azure, ovvero l'ID di directory. Vedere [Ottenere l'ID tenant](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).
* ID client dell'applicazione di Hello Azure Active Directory. Vedere [Creare un'applicazione Azure Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application) e [Ottenere un ID applicazione](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)
* Hello Azure Active Directory dell'applicazione la chiave privata. Vedere [Ottenere la chiave di autenticazione dell'applicazione](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)

## <a name="prerequisites"></a>Prerequisiti
* Cluster HDInsight. Vedere [Esercitazione introduttiva](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).



## <a name="assign-azure-ad-application-toorole"></a>Assegnare toorole applicazione Azure AD
È necessario assegnare tooa applicazione hello [ruolo](../active-directory/role-based-access-built-in-roles.md) toogrant le autorizzazioni per l'esecuzione di azioni. È possibile impostare l'ambito hello a livello di hello di sottoscrizione hello, gruppo di risorse o la risorsa. le autorizzazioni di Hello sono ereditati toolower livelli di ambito (ad esempio, l'aggiunta di un ruolo di lettore toohello applicazione per un gruppo di risorse significa che è possibile leggere il gruppo di risorse hello e le risorse contenute). In questa esercitazione si imposteranno ambito hello a livello di gruppo di risorse hello. Per ulteriori informazioni, vedere [utilizzare le risorse di sottoscrizione di Azure tooyour accesso toomanage assegnazioni ruolo](../active-directory/role-based-access-control-configure.md)

**hello tooadd applicazione Azure AD toohello del ruolo proprietario**

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **gruppo di risorse** hello nel riquadro di sinistra.
3. Fare clic su gruppo di risorse hello che contiene il cluster di HDInsight hello in cui si eseguirà la query Hive più avanti in questa esercitazione. Se sono presenti troppi gruppi di risorse, è possibile utilizzare il filtro di hello.
4. Fare clic su **Access control (IAM)** dal menu del gruppo di risorse hello.
5. Fare clic su **Aggiungi** da hello **utenti** blade.
6. Seguire hello di hello istruzione tooadd **proprietario** toohello ruolo applicazione AD Azure creata nella procedura ultimo hello. Quando viene completata correttamente, verrà visualizzata un'applicazione hello elencata nel Pannello di hello gli utenti con ruolo di proprietario hello.

## <a name="develop-hdinsight-client-application"></a>Sviluppare l'applicazione client HDInsight

1. Creare un'applicazione console C#.
2. Aggiungere i seguenti pacchetti Nuget hello:

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. Utilizzare hello nell'esempio di codice seguente:

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Common.Authentication;
        using Microsoft.Azure.Common.Authentication.Factories;
        using Microsoft.Azure.Common.Authentication.Models;
        using Microsoft.Azure.Management.Resources;
        using Microsoft.Azure.Management.HDInsight;
        
        namespace CreateHDICluster
        {
            internal class Program
            {
                private static HDInsightManagementClient _hdiManagementClient;
        
                private static Guid SubscriptionId = new Guid("<Enter Your Azure Subscription ID>");
                private static string tenantID = "<Enter Your Tenant ID (A.K.A. Directory ID)>";
                private static string applicationID = "<Enter Your Application ID>";
                private static string secretKey = "<Enter hello Application Secret Key>";
        
                private static void Main(string[] args)
                {
                    var key = new SecureString();
                    foreach (char c in secretKey) { key.AppendChar(c); }

                    var tokenCreds = GetTokenCloudCredentials(tenantID, applicationID, key);
                    var subCloudCredentials = GetSubscriptionCloudCredentials(tokenCreds, SubscriptionId);
        
                    var resourceManagementClient = new ResourceManagementClient(subCloudCredentials);
                    resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        
                    _hdiManagementClient = new HDInsightManagementClient(subCloudCredentials);
        
                    var results = _hdiManagementClient.Clusters.List();
                    foreach (var name in results.Clusters)
                    {
                        Console.WriteLine("Cluster Name: " + name.Name);
                        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
                        Console.WriteLine("\t Cluster location: " + name.Location);
                        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
                    }
                    Console.WriteLine("Press Enter toocontinue");
                    Console.ReadLine();
                }

                /// Get hello access token for a service principal and provided key                
                public static TokenCloudCredentials GetTokenCloudCredentials(string tenantId, string clientId, SecureString secretKey)
                {
                    var authFactory = new AuthenticationFactory();
                    var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
                    var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
                    var accessToken =
                        authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
        
                    return new TokenCloudCredentials(accessToken);
                }
        
                public static SubscriptionCloudCredentials GetSubscriptionCloudCredentials(SubscriptionCloudCredentials creds, Guid subId)
                {
                    return new TokenCloudCredentials(subId.ToString(), ((TokenCloudCredentials)creds).Token);
                }
            }
        }

## <a name="next-steps"></a>Passaggi successivi
* [Creare un'applicazione e un'entità servizio di Azure Active Directory tramite il portale](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [Autenticazione di un'entità servizio con Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-control-configure.md)
