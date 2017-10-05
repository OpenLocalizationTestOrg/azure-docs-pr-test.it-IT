---
title: Procedura dettagliata per la creazione del connettore Generic SQL | Documentazione Microsoft
description: Questo articolo presenta la procedura dettagliata per la creazione di un semplice sistema HR mediante il connettore Generic SQL.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 28c1cc60-24fd-4d0d-a36d-b4aba6de86e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 3fdc1b405b95180d031aa4ad45b406f7fc149d8f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="generic-sql-connector-step-by-step"></a><span data-ttu-id="cba2c-103">Procedura dettagliata per la creazione del connettore Generic SQL</span><span class="sxs-lookup"><span data-stu-id="cba2c-103">Generic SQL Connector step-by-step</span></span>
<span data-ttu-id="cba2c-104">Questo argomento è una guida dettagliata.</span><span class="sxs-lookup"><span data-stu-id="cba2c-104">This topic is a step-by-step guide.</span></span> <span data-ttu-id="cba2c-105">Verrà creato un semplice database delle risorse umane di esempio che sarà usato per importare alcuni utenti con la relativa appartenenza ai gruppi.</span><span class="sxs-lookup"><span data-stu-id="cba2c-105">It creates a simple sample HR database and use it for importing some users and their group membership.</span></span>

## <a name="prepare-the-sample-database"></a><span data-ttu-id="cba2c-106">Preparare il database di esempio</span><span class="sxs-lookup"><span data-stu-id="cba2c-106">Prepare the sample database</span></span>
<span data-ttu-id="cba2c-107">In un server che esegue SQL Server avviare lo script SQL disponibile nell'[Appendice A](#appendix-a). Lo script crea un database di esempio con il nome GSQLDEMO.</span><span class="sxs-lookup"><span data-stu-id="cba2c-107">On a server running SQL Server, run the SQL script found in [Appendix A](#appendix-a). This script creates a sample database with the name GSQLDEMO.</span></span> <span data-ttu-id="cba2c-108">Il modello a oggetti per il database creato sarà simile a questa immagine: </span><span class="sxs-lookup"><span data-stu-id="cba2c-108">The object model for the created database looks like this picture:</span></span>  
<span data-ttu-id="cba2c-109">![Modello a oggetti](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span><span class="sxs-lookup"><span data-stu-id="cba2c-109">![Object Model](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)</span></span>

<span data-ttu-id="cba2c-110">Creare anche un utente da usare per connettersi al database.</span><span class="sxs-lookup"><span data-stu-id="cba2c-110">Also create a user you want to use to connect to the database.</span></span> <span data-ttu-id="cba2c-111">In questa procedura dettagliata l'utente si chiama FABRIKAM\SQLUser e si trova nel dominio.</span><span class="sxs-lookup"><span data-stu-id="cba2c-111">In this walkthrough, the user is called FABRIKAM\SQLUser and located in the domain.</span></span>

## <a name="create-the-odbc-connection-file"></a><span data-ttu-id="cba2c-112">Creare il file di connessione ODBC</span><span class="sxs-lookup"><span data-stu-id="cba2c-112">Create the ODBC connection file</span></span>
<span data-ttu-id="cba2c-113">Il connettore Generic SQL usa ODBC per connettersi al server remoto.</span><span class="sxs-lookup"><span data-stu-id="cba2c-113">The Generic SQL Connector is using ODBC to connect to the remote server.</span></span> <span data-ttu-id="cba2c-114">È necessario innanzitutto creare un file con le informazioni di connessione ODBC.</span><span class="sxs-lookup"><span data-stu-id="cba2c-114">First we need to create a file with the ODBC connection information.</span></span>

1. <span data-ttu-id="cba2c-115">Avviare l'utilità di gestione di ODBC sul server: </span><span class="sxs-lookup"><span data-stu-id="cba2c-115">Start the ODBC management utility on your server:</span></span>  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. <span data-ttu-id="cba2c-117">Selezionare la scheda **DSN su file**.</span><span class="sxs-lookup"><span data-stu-id="cba2c-117">Select the tab **File DSN**.</span></span> <span data-ttu-id="cba2c-118">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="cba2c-118">Click **Add...**.</span></span>  
   <span data-ttu-id="cba2c-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span><span class="sxs-lookup"><span data-stu-id="cba2c-119">![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)</span></span>
3. <span data-ttu-id="cba2c-120">Il driver predefinito è adeguato allo scopo, quindi selezionarlo e fare clic su **Avanti>**.</span><span class="sxs-lookup"><span data-stu-id="cba2c-120">The out-of-box driver works fine, so select it and click **Next>**.</span></span>  
   <span data-ttu-id="cba2c-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span><span class="sxs-lookup"><span data-stu-id="cba2c-121">![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)</span></span>
4. <span data-ttu-id="cba2c-122">Assegnare un nome al file, ad esempio **GenericSQL**.</span><span class="sxs-lookup"><span data-stu-id="cba2c-122">Give the file a name, such as **GenericSQL**.</span></span>  
   <span data-ttu-id="cba2c-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span><span class="sxs-lookup"><span data-stu-id="cba2c-123">![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)</span></span>
5. <span data-ttu-id="cba2c-124">Fare clic su **Finish**(Fine).</span><span class="sxs-lookup"><span data-stu-id="cba2c-124">Click **Finish**.</span></span>  
   <span data-ttu-id="cba2c-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span><span class="sxs-lookup"><span data-stu-id="cba2c-125">![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)</span></span>
6. <span data-ttu-id="cba2c-126">È ora necessario configurare la connessione.</span><span class="sxs-lookup"><span data-stu-id="cba2c-126">Time to configure the connection.</span></span> <span data-ttu-id="cba2c-127">Assegnare una descrizione appropriata all'origine dati e specificare il nome del server che esegue SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cba2c-127">Give the data source a good description and provide the name of the server running SQL Server.</span></span>  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. <span data-ttu-id="cba2c-129">Selezionare la modalità di autenticazione con SQL.</span><span class="sxs-lookup"><span data-stu-id="cba2c-129">Select how to authenticate with SQL.</span></span> <span data-ttu-id="cba2c-130">In questo caso si userà l'autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="cba2c-130">In this case, we use Windows Authentication.</span></span>  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. <span data-ttu-id="cba2c-132">Specificare il nome del database di esempio, **GSQLDEMO**.</span><span class="sxs-lookup"><span data-stu-id="cba2c-132">Provide the name of the sample database, **GSQLDEMO**.</span></span>  
   <span data-ttu-id="cba2c-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span><span class="sxs-lookup"><span data-stu-id="cba2c-133">![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)</span></span>
9. <span data-ttu-id="cba2c-134">In questa schermata mantenere tutte le selezioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="cba2c-134">Keep everything default on this screen.</span></span> <span data-ttu-id="cba2c-135">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="cba2c-135">Click **Finish**.</span></span>  
   <span data-ttu-id="cba2c-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span><span class="sxs-lookup"><span data-stu-id="cba2c-136">![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)</span></span>
10. <span data-ttu-id="cba2c-137">Per verificare che tutto funzioni come previsto, fare clic su **Verifica origine dati**.</span><span class="sxs-lookup"><span data-stu-id="cba2c-137">To verify everything is working as expected, click **Test Data Source**.</span></span>  
    <span data-ttu-id="cba2c-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span><span class="sxs-lookup"><span data-stu-id="cba2c-138">![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)</span></span>
11. <span data-ttu-id="cba2c-139">Assicurarsi che la verifica abbia esito positivo.</span><span class="sxs-lookup"><span data-stu-id="cba2c-139">Make sure the test is successful.</span></span>  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. <span data-ttu-id="cba2c-141">Il file di configurazione ODBC dovrebbe essere ora visibile in DSN su file.</span><span class="sxs-lookup"><span data-stu-id="cba2c-141">The ODBC configuration file should now be visible in File DSN.</span></span>  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

<span data-ttu-id="cba2c-143">Il file necessario è ora disponibile e si può iniziare a creare il connettore.</span><span class="sxs-lookup"><span data-stu-id="cba2c-143">We now have the file we need and can start creating the Connector.</span></span>

## <a name="create-the-generic-sql-connector"></a><span data-ttu-id="cba2c-144">Creare il connettore Generic SQL</span><span class="sxs-lookup"><span data-stu-id="cba2c-144">Create the Generic SQL Connector</span></span>
1. <span data-ttu-id="cba2c-145">Nell'interfaccia utente di Synchronization Service Manager selezionare **Connectors** (Connettori) e **Create** (Crea).</span><span class="sxs-lookup"><span data-stu-id="cba2c-145">In the Synchronization Service Manager UI, select **Connectors** and **Create**.</span></span> <span data-ttu-id="cba2c-146">Selezionare **Generic SQL (Microsoft)** e assegnargli un nome descrittivo.</span><span class="sxs-lookup"><span data-stu-id="cba2c-146">Select **Generic SQL (Microsoft)** and give it a descriptive name.</span></span>  
   <span data-ttu-id="cba2c-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span><span class="sxs-lookup"><span data-stu-id="cba2c-147">![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)</span></span>
2. <span data-ttu-id="cba2c-148">Trovare il file DSN creato nella sezione precedente e caricarlo nel server.</span><span class="sxs-lookup"><span data-stu-id="cba2c-148">Find the DSN file you created in the previous section and upload it to the server.</span></span> <span data-ttu-id="cba2c-149">Immettere le credenziali per connettersi al database.</span><span class="sxs-lookup"><span data-stu-id="cba2c-149">Provide the credentials to connect to the database.</span></span>  
   ![Connector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. <span data-ttu-id="cba2c-151">In questa procedura dettagliata si considera un caso semplificato in cui esistono due tipi di oggetti, **User** e **Group**.</span><span class="sxs-lookup"><span data-stu-id="cba2c-151">In this walkthrough, we are making it easy for us and say that there are two object types, **User** and **Group**.</span></span>
   <span data-ttu-id="cba2c-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span><span class="sxs-lookup"><span data-stu-id="cba2c-152">![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)</span></span>
4. <span data-ttu-id="cba2c-153">Il connettore dovrà trovare gli attributi esaminando la tabella.</span><span class="sxs-lookup"><span data-stu-id="cba2c-153">To find the attributes, we want the Connector to detect those attributes by looking at the table itself.</span></span> <span data-ttu-id="cba2c-154">Poiché **Users** è una parola riservata in SQL, occorre specificarla fra parentesi quadre [ ].</span><span class="sxs-lookup"><span data-stu-id="cba2c-154">Since **Users** is a reserved word in SQL, we need to provide it in square brackets [ ].</span></span>  
   <span data-ttu-id="cba2c-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span><span class="sxs-lookup"><span data-stu-id="cba2c-155">![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)</span></span>
5. <span data-ttu-id="cba2c-156">È ora necessario definire l'attributo di ancoraggio e l'attributo DN.</span><span class="sxs-lookup"><span data-stu-id="cba2c-156">Time to define the anchor attribute and the DN attribute.</span></span> <span data-ttu-id="cba2c-157">Per **Users**si usa la combinazione dei due attributi Username ed EmployeeID.</span><span class="sxs-lookup"><span data-stu-id="cba2c-157">For **Users**, we use the combination of the two attributes username and EmployeeID.</span></span> <span data-ttu-id="cba2c-158">Per **Group**si usa GroupName, non molto plausibile in un caso reale, ma adeguato per questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="cba2c-158">For **group**, we use GroupName (not realistic in real-life, but for this walkthrough it works).</span></span>
   <span data-ttu-id="cba2c-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span><span class="sxs-lookup"><span data-stu-id="cba2c-159">![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)</span></span>
6. <span data-ttu-id="cba2c-160">Non tutti i tipi di attributo possono essere rilevati in un database SQL.</span><span class="sxs-lookup"><span data-stu-id="cba2c-160">Not all attribute types can be detected in a SQL database.</span></span> <span data-ttu-id="cba2c-161">In particolare, non può essere rilevato il tipo di attributo di riferimento.</span><span class="sxs-lookup"><span data-stu-id="cba2c-161">The reference attribute type in particular cannot.</span></span> <span data-ttu-id="cba2c-162">Per il tipo di oggetto Group è necessario cambiare OwnerID e MemberID a cui fare riferimento.</span><span class="sxs-lookup"><span data-stu-id="cba2c-162">For the group object type, we need to change the OwnerID and MemberID to reference.</span></span>  
   ![Connector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. <span data-ttu-id="cba2c-164">Gli attributi selezionati come attributi di riferimento nel passaggio precedente richiedono il tipo di oggetto cui questi valori fanno riferimento.</span><span class="sxs-lookup"><span data-stu-id="cba2c-164">The attributes we selected as reference attributes in the previous step require the object type these values are a reference to.</span></span> <span data-ttu-id="cba2c-165">In questo caso si tratta del tipo di oggetto User.</span><span class="sxs-lookup"><span data-stu-id="cba2c-165">In our case, the User object type.</span></span>  
   ![Connector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. <span data-ttu-id="cba2c-167">Nella pagina Global Parameters (Parametri globali) selezionare **Watermark** (Limite) come strategia differenziale.</span><span class="sxs-lookup"><span data-stu-id="cba2c-167">On the Global Parameters page, select **Watermark** as the delta strategy.</span></span> <span data-ttu-id="cba2c-168">Digitare anche il formato di data/ora **yyyy-MM-dd HH:mm:ss**(aaaa-MM-gg HH:mm:ss).</span><span class="sxs-lookup"><span data-stu-id="cba2c-168">Also type in the date/time format **yyyy-MM-dd HH:mm:ss**.</span></span>
   <span data-ttu-id="cba2c-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span><span class="sxs-lookup"><span data-stu-id="cba2c-169">![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)</span></span>
9. <span data-ttu-id="cba2c-170">Nella pagina **Configure Partitions and Hierarchies** (Configura partizioni e gerarchie) selezionare entrambi i tipi di oggetto.</span><span class="sxs-lookup"><span data-stu-id="cba2c-170">On the **Configure Partitions and Hierarchies** page, select both object types.</span></span>
   <span data-ttu-id="cba2c-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span><span class="sxs-lookup"><span data-stu-id="cba2c-171">![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)</span></span>
10. <span data-ttu-id="cba2c-172">In **Select Object Types** (Seleziona tipi di oggetto) e **Select Attributes** (Seleziona attributi) selezionare entrambi i tipi di oggetto e tutti gli attributi.</span><span class="sxs-lookup"><span data-stu-id="cba2c-172">On the **Select Object Types** and **Select Attributes**, select both object types and all attributes.</span></span> <span data-ttu-id="cba2c-173">Nella pagina **Configure Anchors** (Configura ancoraggi) fare clic su **Finish** (Fine).</span><span class="sxs-lookup"><span data-stu-id="cba2c-173">On the **Configure Anchors** page, click **Finish**.</span></span>

## <a name="create-run-profiles"></a><span data-ttu-id="cba2c-174">Creare i profili di esecuzione</span><span class="sxs-lookup"><span data-stu-id="cba2c-174">Create Run Profiles</span></span>
1. <span data-ttu-id="cba2c-175">Nell'interfaccia utente di Synchronization Service Manager selezionare **Connectors** (Connettori) e **Configure Run Profiles** (Configura profili di esecuzione).</span><span class="sxs-lookup"><span data-stu-id="cba2c-175">In the Synchronization Service Manager UI, select **Connectors**, and **Configure Run Profiles**.</span></span> <span data-ttu-id="cba2c-176">Fare clic su **New Profile**(Nuovo profilo).</span><span class="sxs-lookup"><span data-stu-id="cba2c-176">Click **New Profile**.</span></span> <span data-ttu-id="cba2c-177">Si inizierà con **Full Import**(Importazione completa).</span><span class="sxs-lookup"><span data-stu-id="cba2c-177">We start with **Full Import**.</span></span>  
   <span data-ttu-id="cba2c-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span><span class="sxs-lookup"><span data-stu-id="cba2c-178">![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)</span></span>
2. <span data-ttu-id="cba2c-179">Selezionare il tipo **Full Import (Stage Only)**(Importazione completa - solo staging).</span><span class="sxs-lookup"><span data-stu-id="cba2c-179">Select the type **Full Import (Stage Only)**.</span></span>  
   <span data-ttu-id="cba2c-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span><span class="sxs-lookup"><span data-stu-id="cba2c-180">![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)</span></span>
3. <span data-ttu-id="cba2c-181">Selezionare la partizione **OBJECT=User**.</span><span class="sxs-lookup"><span data-stu-id="cba2c-181">Select the partition **OBJECT=User**.</span></span>  
   <span data-ttu-id="cba2c-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span><span class="sxs-lookup"><span data-stu-id="cba2c-182">![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)</span></span>
4. <span data-ttu-id="cba2c-183">Selezionare **Table** (Tabella) e digitare **[USERS]**.</span><span class="sxs-lookup"><span data-stu-id="cba2c-183">Select **Table** and type **[USERS]**.</span></span> <span data-ttu-id="cba2c-184">Scorrere fino alla sezione del tipo di oggetto multivalore e immettere i dati riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="cba2c-184">Scroll down to the multi-valued object type section and enter the data as in the following picture.</span></span> <span data-ttu-id="cba2c-185">Selezionare **Finish** (Fine) per salvare il passaggio.</span><span class="sxs-lookup"><span data-stu-id="cba2c-185">Select **Finish** to save the step.</span></span>  
   <span data-ttu-id="cba2c-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span><span class="sxs-lookup"><span data-stu-id="cba2c-186">![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)</span></span>  
   <span data-ttu-id="cba2c-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span><span class="sxs-lookup"><span data-stu-id="cba2c-187">![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)</span></span>  
5. <span data-ttu-id="cba2c-188">Selezionare **New Step**(Nuovo passaggio).</span><span class="sxs-lookup"><span data-stu-id="cba2c-188">Select **New Step**.</span></span> <span data-ttu-id="cba2c-189">Questa volta selezionare **OBJECT=Group**.</span><span class="sxs-lookup"><span data-stu-id="cba2c-189">This time, select **OBJECT=Group**.</span></span> <span data-ttu-id="cba2c-190">Nell'ultima pagina usare la configurazione illustrata nell'immagine.</span><span class="sxs-lookup"><span data-stu-id="cba2c-190">On the last page, use the configuration as in the following picture.</span></span> <span data-ttu-id="cba2c-191">Fare clic su **Finish**(Fine).</span><span class="sxs-lookup"><span data-stu-id="cba2c-191">Click **Finish**.</span></span>  
   <span data-ttu-id="cba2c-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span><span class="sxs-lookup"><span data-stu-id="cba2c-192">![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)</span></span>  
   <span data-ttu-id="cba2c-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span><span class="sxs-lookup"><span data-stu-id="cba2c-193">![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)</span></span>  
6. <span data-ttu-id="cba2c-194">Facoltativo: se si vuole, è possibile configurare altri profili di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="cba2c-194">Optional: If you want to, you can configure additional run profiles.</span></span> <span data-ttu-id="cba2c-195">In questa procedura dettagliata si usa solo l'importazione completa.</span><span class="sxs-lookup"><span data-stu-id="cba2c-195">For this walkthrough, only the Full Import is used.</span></span>
7. <span data-ttu-id="cba2c-196">Fare clic su **OK** per terminare la modifica dei profili di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="cba2c-196">Click **OK** to finish changing run profiles.</span></span>

## <a name="add-some-test-data-and-test-the-import"></a><span data-ttu-id="cba2c-197">Aggiungere alcuni dati di prova e testare l'importazione</span><span class="sxs-lookup"><span data-stu-id="cba2c-197">Add some test data and test the import</span></span>
<span data-ttu-id="cba2c-198">Immettere alcuni dati di prova nel database di esempio.</span><span class="sxs-lookup"><span data-stu-id="cba2c-198">Fill out some test data in your sample database.</span></span> <span data-ttu-id="cba2c-199">Quando si è pronti, selezionare **Run** (Esegui) e **Full import** (Importazione completa).</span><span class="sxs-lookup"><span data-stu-id="cba2c-199">When you are ready, select **Run** and **Full import**.</span></span>

<span data-ttu-id="cba2c-200">In questo esempio si ottiene un utente con due numeri di telefono e un gruppo con alcuni membri.</span><span class="sxs-lookup"><span data-stu-id="cba2c-200">Here is a user with two phone numbers and a group with some members.</span></span>  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![cs2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a><span data-ttu-id="cba2c-203">Appendice A</span><span class="sxs-lookup"><span data-stu-id="cba2c-203">Appendix A</span></span>
<span data-ttu-id="cba2c-204">**Script SQL per la creazione del database di esempio**</span><span class="sxs-lookup"><span data-stu-id="cba2c-204">**SQL script to create the sample database**</span></span>

```SQL
---Creating the Database---------
Create Database GSQLDEMO
Go
-------Using the Database-----------
Use [GSQLDEMO]
Go
-------------------------------------
USE [GSQLDEMO]
GO
/****** Object:  Table [dbo].[GroupMembers]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GroupMembers](
    [MemberID] [int] NOT NULL,
    [Group_ID] [int] NOT NULL
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[GROUPS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GROUPS](
    [GroupID] [int] NOT NULL,
    [GROUPNAME] [nvarchar](200) NOT NULL,
    [DESCRIPTION] [nvarchar](200) NULL,
    [WATERMARK] [datetime] NULL,
    [OwnerID] [int] NULL,
PRIMARY KEY CLUSTERED
(
    [GroupID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[USERPHONE]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[USERPHONE](
    [USER_ID] [int] NULL,
    [Phone] [varchar](20) NULL
) ON [PRIMARY]

GO
SET ANSI_PADDING OFF
GO
/****** Object:  Table [dbo].[USERS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[USERS](
    [USERID] [int] NOT NULL,
    [USERNAME] [nvarchar](200) NOT NULL,
    [FirstName] [nvarchar](100) NULL,
    [LastName] [nvarchar](100) NULL,
    [DisplayName] [nvarchar](100) NULL,
    [ACCOUNTDISABLED] [bit] NULL,
    [EMPLOYEEID] [int] NOT NULL,
    [WATERMARK] [datetime] NULL,
PRIMARY KEY CLUSTERED
(
    [USERID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_GROUPS] FOREIGN KEY([Group_ID])
REFERENCES [dbo].[GROUPS] ([GroupID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_GROUPS]
GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_USERS] FOREIGN KEY([MemberID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_USERS]
GO
ALTER TABLE [dbo].[GROUPS]  WITH CHECK ADD  CONSTRAINT [FK_GROUPS_USERS] FOREIGN KEY([OwnerID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GROUPS] CHECK CONSTRAINT [FK_GROUPS_USERS]
GO
ALTER TABLE [dbo].[USERPHONE]  WITH CHECK ADD  CONSTRAINT [FK_USERPHONE_USER] FOREIGN KEY([USER_ID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[USERPHONE] CHECK CONSTRAINT [FK_USERPHONE_USER]
GO
```
