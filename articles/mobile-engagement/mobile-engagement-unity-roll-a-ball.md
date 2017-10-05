---
title: esercitazione su Roll a Ball di Unity
description: Procedura per creare il classico gioco Roll a Ball di Unity, un prerequisito per tutte le esercitazioni di Unity per Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0afd0eca-f74a-43aa-bba8-436a0265c312
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 6392d1f780b1bc2348fee5947550b05e86ea4de2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="f81b7-103"><a id="unity-roll-a-ball"></a>Creare il gioco Roll a Ball di Unity</span><span class="sxs-lookup"><span data-stu-id="f81b7-103"><a id="unity-roll-a-ball"></a>Create Unity Roll a Ball game</span></span>
<span data-ttu-id="f81b7-104">Questa esercitazione illustra i passaggi principali di un' [esercitazione su Roll a Ball di Unity](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial)leggermente modificata.</span><span class="sxs-lookup"><span data-stu-id="f81b7-104">This tutorial walks through the main steps for a slightly modified [Unity Roll a Ball tutorial](http://unity3d.com/learn/tutorials/projects/roll-ball-tutorial).</span></span> <span data-ttu-id="f81b7-105">Questo gioco di esempio è costituito da un oggetto "player" sferico controllato dall'utente dell'app e lo scopo del gioco è di raccogliere oggetti da collezione facendo scontrare l'oggetto player con questi oggetti da collezione.</span><span class="sxs-lookup"><span data-stu-id="f81b7-105">This sample game consists of a spherical 'player' object which is controlled by the app user and the objective of the game is to 'collect' collectible objects by colliding the player object with these collectible objects.</span></span> <span data-ttu-id="f81b7-106">Ciò presuppone una certa conoscenza di base dell'ambiente dell'editor di Unity.</span><span class="sxs-lookup"><span data-stu-id="f81b7-106">This assumes basic familiarity with Unity editor environment.</span></span> <span data-ttu-id="f81b7-107">In caso di problemi, vedere l'esercitazione completa.</span><span class="sxs-lookup"><span data-stu-id="f81b7-107">If you run into any issues then you should refer to the full tutorial.</span></span> 

### <a name="setting-up-the-game"></a><span data-ttu-id="f81b7-108">Configurazione del gioco</span><span class="sxs-lookup"><span data-stu-id="f81b7-108">Setting up the game</span></span>
<span data-ttu-id="f81b7-109">I passaggi seguenti sono tratti dall' [esercitazione di Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="f81b7-109">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/set-up?playlist=17141)</span></span>

1. <span data-ttu-id="f81b7-110">Aprire l'**editor Unity** e fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="f81b7-110">Open **Unity Editor** and click **New**.</span></span> 
   
    ![][51] 
2. <span data-ttu-id="f81b7-111">Fornire **nome del progetto** & **percorso**, selezionare **3D** e fare clic su **Create project**.</span><span class="sxs-lookup"><span data-stu-id="f81b7-111">Provide a **Project name** & **Location**, select **3D** and click **Create project**.</span></span>
   
    ![][52]
3. <span data-ttu-id="f81b7-112">Salvare la scena predefinita appena creata come parte del nuovo progetto con il nome **MiniGame** all'interno di una nuova cartella **\_Scenes** nella cartella **Assets**:</span><span class="sxs-lookup"><span data-stu-id="f81b7-112">Save the default scene just created as part of the new project as with the name **MiniGame** within a new **\_Scenes** folder under **Assets** folder:</span></span>
   
    ![][53]
4. <span data-ttu-id="f81b7-113">Creare il campo di gioco selezionando **3D Object -> Plane** e assegnare all'oggetto il nome **Ground**</span><span class="sxs-lookup"><span data-stu-id="f81b7-113">Create a **3D Object -> Plane** as the playing field and rename this plane object as **Ground**</span></span>
   
    ![][1]
5. <span data-ttu-id="f81b7-114">Reimpostare il componente di trasformazione per questo oggetto **Ground** in modo che si trovi in corrispondenza dell'origine.</span><span class="sxs-lookup"><span data-stu-id="f81b7-114">Reset the transform component for this **Ground** object so that it is at the Origin.</span></span> 
   
    ![][3]
6. <span data-ttu-id="f81b7-115">Deselezionare **Show Grid** dal **menu Gizmos** per l'oggetto **Ground**.</span><span class="sxs-lookup"><span data-stu-id="f81b7-115">Uncheck **Show Grid** from **Gizmos menu** for the **Ground** object.</span></span>
   
    ![][4]
7. <span data-ttu-id="f81b7-116">Aggiornare il componente **Scale** per l'oggetto **Ground** con le dimensioni [X = 2, Y = 1, Z = 2].</span><span class="sxs-lookup"><span data-stu-id="f81b7-116">Update the **Scale** component for the **Ground** object to be [X = 2,Y = 1, Z = 2].</span></span> 
   
    ![][5]
8. <span data-ttu-id="f81b7-117">Aggiungere un nuovo elemento al progetto andando su **3D Object -> Sphere** e assegnare all'oggetto sferico il nome **Player**.</span><span class="sxs-lookup"><span data-stu-id="f81b7-117">Add a new **3D Object -> Sphere** to the project and rename this sphere object as **Player**.</span></span> 
   
    ![][6]
9. <span data-ttu-id="f81b7-118">Selezionare l'oggetto **Player** e fare clic su **Reset Transform** in modo analogo all'oggetto Plane.</span><span class="sxs-lookup"><span data-stu-id="f81b7-118">Select the **Player** object and click **Reset Transform** similar to the Plane object.</span></span> 
10. <span data-ttu-id="f81b7-119">Aggiornare il componente **Transform -> Position -> Y Coordinate** per Player Y assegnando il valore 0,5.</span><span class="sxs-lookup"><span data-stu-id="f81b7-119">Update **Transform -> Position -> Y Coordinate** component for the Player Y as 0.5.</span></span>  
    
    ![][7]
11. <span data-ttu-id="f81b7-120">Creare nel progetto una nuova cartella denominata **Materials** dove verrà creato il materiale per colorare il giocatore.</span><span class="sxs-lookup"><span data-stu-id="f81b7-120">Create a new folder called **Materials** in the project where we will create the material to color the player.</span></span> 
12. <span data-ttu-id="f81b7-121">Creare un nuovo **materiale** chiamato **Background** in questa cartella.</span><span class="sxs-lookup"><span data-stu-id="f81b7-121">Create a new **Material** called **Background** in this folder.</span></span> 
    
    ![][8]
13. <span data-ttu-id="f81b7-122">Aggiornare il colore del materiale aggiornando la proprietà **Albedo** .</span><span class="sxs-lookup"><span data-stu-id="f81b7-122">Update the color of the material by updating the **Albedo** property of it.</span></span> <span data-ttu-id="f81b7-123">È possibile selezionare i valori RGB [0,32,64].</span><span class="sxs-lookup"><span data-stu-id="f81b7-123">You can select the RGB values of [0,32,64].</span></span> 
    
    ![][9]
14. <span data-ttu-id="f81b7-124">Trascinare questo materiale nella visualizzazione scena per applicare il colore all'oggetto **Ground** .</span><span class="sxs-lookup"><span data-stu-id="f81b7-124">Drag this material into the scene view to apply color to the **Ground** object.</span></span> 
    
    ![][10]
15. <span data-ttu-id="f81b7-125">Aggiornare infine il **Transform -> Rotation -> Y** assegnando il valore 60 nell'oggetto Directional Light per maggiore chiarezza.</span><span class="sxs-lookup"><span data-stu-id="f81b7-125">Finally update the **Transform -> Rotation -> Y** to 60 on the Directional Light object for clarity.</span></span> 
    
    ![][12]

### <a name="moving-the-player"></a><span data-ttu-id="f81b7-126">Spostamento del player</span><span class="sxs-lookup"><span data-stu-id="f81b7-126">Moving the player</span></span>
<span data-ttu-id="f81b7-127">I passaggi seguenti sono tratti dall' [esercitazione di Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span><span class="sxs-lookup"><span data-stu-id="f81b7-127">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-player?playlist=17141)</span></span>

1. <span data-ttu-id="f81b7-128">Aggiungere un componente **RigidBody** all'oggetto **Player**.</span><span class="sxs-lookup"><span data-stu-id="f81b7-128">Add a **RigidBody** component to the **Player** object.</span></span> 
   
    ![][13]
2. <span data-ttu-id="f81b7-129">Creare una nuova cartella denominata **Scripts** nel progetto.</span><span class="sxs-lookup"><span data-stu-id="f81b7-129">Create a new folder called **Scripts** in the Project.</span></span> 
3. <span data-ttu-id="f81b7-130">Fare clic su **Add Component-> New Script -> C# Script**.</span><span class="sxs-lookup"><span data-stu-id="f81b7-130">Click **Add Component-> New Script -> C# Script**.</span></span> <span data-ttu-id="f81b7-131">Assegnargli il nome **PlayerController** e fare clic su **Create and Add**.</span><span class="sxs-lookup"><span data-stu-id="f81b7-131">Name it **PlayerController**, and click **Create and Add**.</span></span> <span data-ttu-id="f81b7-132">Verrà creato uno script che verrà associato all'oggetto Player.</span><span class="sxs-lookup"><span data-stu-id="f81b7-132">This will create and attach a script to the Player object.</span></span>  
   
    ![][14]
4. <span data-ttu-id="f81b7-133">Spostare lo script nella cartella **Scripts** nel progetto.</span><span class="sxs-lookup"><span data-stu-id="f81b7-133">Move this script under the **Scripts** folder in the project.</span></span> 
5. <span data-ttu-id="f81b7-134">Aprire lo script per modificarlo nell'editor di script preferito, aggiornare il codice dello script con il codice seguente e salvarlo.</span><span class="sxs-lookup"><span data-stu-id="f81b7-134">Open the script for editing in your favorite script editor, update the script code with the following code and save it.</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour 
        {
            public float speed;
            private Rigidbody rb;
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
                rb.AddForce (movement * speed);
            }
        }
6. <span data-ttu-id="f81b7-135">Si noti che lo script precedente usa una proprietà **Speed** .</span><span class="sxs-lookup"><span data-stu-id="f81b7-135">Note that the script above uses a **Speed** property.</span></span> <span data-ttu-id="f81b7-136">Nell'editor di Unity impostare la proprietà Speed su 10.</span><span class="sxs-lookup"><span data-stu-id="f81b7-136">In the Unity editor, update the speed property to 10.</span></span>  
   
    ![][15]
7. <span data-ttu-id="f81b7-137">Selezionare **Play** nell'editor di Unity.</span><span class="sxs-lookup"><span data-stu-id="f81b7-137">Hit **Play** in the Unity Editor.</span></span> <span data-ttu-id="f81b7-138">Ora sarà possibile controllare con la tastiera la pallina che dovrebbe ruotare e muoversi.</span><span class="sxs-lookup"><span data-stu-id="f81b7-138">Now you should be able to control the ball using the keyboard and it should rotate and move around.</span></span> 

### <a name="moving-the-camera"></a><span data-ttu-id="f81b7-139">Spostamento della videocamera</span><span class="sxs-lookup"><span data-stu-id="f81b7-139">Moving the camera</span></span>
<span data-ttu-id="f81b7-140">I passaggi di seguito sono presi dall'[esercitazione su Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) e limiteranno **Main Camera** all'oggetto **Player**.</span><span class="sxs-lookup"><span data-stu-id="f81b7-140">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/moving-the-camera?playlist=17141) and will tie the **Main Camera** to the **Player** object.</span></span> 

1. <span data-ttu-id="f81b7-141">Aggiornare **Transform.Position** con i valori X = 0, Y = 10,5, Z = -10.</span><span class="sxs-lookup"><span data-stu-id="f81b7-141">Update the **Transform.Position** to be X = 0,  Y = 10.5, Z=-10.</span></span>  
2. <span data-ttu-id="f81b7-142">Impostare **Transform.Rotation** su X = 45, Y = 0, Z= 0.</span><span class="sxs-lookup"><span data-stu-id="f81b7-142">Update the **Transform.Rotation** to be X = 45, Y = 0, Z = 0.</span></span>  
   
    ![][16]
3. <span data-ttu-id="f81b7-143">Aggiungere un nuovo script denominato **CameraController** a **MainCamera** e spostarlo nella cartella Scripts.</span><span class="sxs-lookup"><span data-stu-id="f81b7-143">Add a new script called **CameraController** to the **MainCamera** and move it under the Scripts folder.</span></span> 
   
    ![][17]
4. <span data-ttu-id="f81b7-144">Aprire lo script per la modifica e aggiungervi il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="f81b7-144">Open up the script for editing and add the following code in it:</span></span>
   
        using UnityEngine;
        using System.Collections;
   
        public class CameraController : MonoBehaviour {
   
            public GameObject player;
   
            private Vector3 offset;
   
            void Start ()
            {
                offset = transform.position - player.transform.position;
            }
   
            void LateUpdate ()
            {
                transform.position = player.transform.position + offset;
            }
        }
5. <span data-ttu-id="f81b7-145">Nell'ambiente di Unity trascinare la variabile Player nello slot Player per l'oggetto Main Camera per poter creare un'associazione tra di essi.</span><span class="sxs-lookup"><span data-stu-id="f81b7-145">In Unity environment - drag the Player variable into the Player slot for the Main Camera object so that the two are associated with one another.</span></span> 
   
    ![][18]
6. <span data-ttu-id="f81b7-146">Se ora si preme Play nell'editor di Unity e si ruota l'oggetto Player Ball, si potrà osservare che la videocamera lo segue nel movimento.</span><span class="sxs-lookup"><span data-stu-id="f81b7-146">Now if you hit Play in the Unity editor and rotate the Player Ball object then you will see the Camera following it in the movement.</span></span>  

### <a name="setting-up-the-play-area"></a><span data-ttu-id="f81b7-147">Configurazione dell'area di gioco</span><span class="sxs-lookup"><span data-stu-id="f81b7-147">Setting up the Play area</span></span>
<span data-ttu-id="f81b7-148">I passaggi seguenti sono tratti dall' [esercitazione di Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="f81b7-148">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/setting-up-the-play-area?playlist=17141).</span></span> <span data-ttu-id="f81b7-149">Verranno creati i muri che circondano il campo in modo che l'oggetto Player Ball non esca dall'area di gioco mentre è in movimento.</span><span class="sxs-lookup"><span data-stu-id="f81b7-149">We will create the Walls surrounding the Ground so that the Player Ball object doesn't drop off the play area in its movement.</span></span> 

1. <span data-ttu-id="f81b7-150">Fare clic su **Create -> Create Empty -> Game Object** e assegnare il nome **Walls**</span><span class="sxs-lookup"><span data-stu-id="f81b7-150">Click **Create -> Create Empty -> Game Object** and name it **Walls**</span></span>
   
    ![][19]
2. <span data-ttu-id="f81b7-151">In questo oggetto Walls creare un nuovo oggetto andando su **3D Object -> Cube** e assegnare il nome "West wall".</span><span class="sxs-lookup"><span data-stu-id="f81b7-151">Under this Walls object - create a new **3D Object -> Cube** and name it "West wall".</span></span> 
   
    ![][20]
3. <span data-ttu-id="f81b7-152">Aggiornare **Transform -> Position** e **Transform -> Scale** per l'oggetto West Wall.</span><span class="sxs-lookup"><span data-stu-id="f81b7-152">Update the **Transform -> Position** and **Transform -> Scale** for this West Wall object.</span></span> 
   
    ![][21]
4. <span data-ttu-id="f81b7-153">Duplicare West wall per creare un elemento **East wall** con la posizione e la scala di trasformazione aggiornate.</span><span class="sxs-lookup"><span data-stu-id="f81b7-153">Duplicate the West wall to create an **East wall** with the updated transform position and scale.</span></span> 
   
    ![][22]
5. <span data-ttu-id="f81b7-154">Duplicare East wall in modo da creare un oggetto **North wall** con la posizione di trasformazione e le proporzioni aggiornate.</span><span class="sxs-lookup"><span data-stu-id="f81b7-154">Duplicate the East wall to create a **North wall** with the updated transform position & scale.</span></span> 
   
    ![][23]
6. <span data-ttu-id="f81b7-155">Duplicare North wall in modo da creare un oggetto **South wall** con la posizione di trasformazione e le proporzioni aggiornate.</span><span class="sxs-lookup"><span data-stu-id="f81b7-155">Duplicate the North wall and create a **South wall** with the updated transform position & scale.</span></span> 
   
    ![][24]

### <a name="creating-collectible-objects"></a><span data-ttu-id="f81b7-156">Creazione di oggetti da collezione</span><span class="sxs-lookup"><span data-stu-id="f81b7-156">Creating Collectible objects</span></span>
<span data-ttu-id="f81b7-157">I passaggi seguenti sono tratti dall' [esercitazione di Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="f81b7-157">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/creating-collectables?playlist=17141).</span></span> <span data-ttu-id="f81b7-158">Verranno creati alcuni oggetti dall'aspetto interessante che costituiranno il set di oggetti da collezione che l'oggetto Player Ball deve raccogliere scontrandosi con essi.</span><span class="sxs-lookup"><span data-stu-id="f81b7-158">We will create some attractive looking objects which will form the set of collectible objects which the Player Ball object needs to 'collect' by colliding with them.</span></span> 

1. <span data-ttu-id="f81b7-159">Creare un nuovo **oggetto 3D Cube** e denominarlo Pickup.</span><span class="sxs-lookup"><span data-stu-id="f81b7-159">Create a new **3D Cube object** and name it Pickup.</span></span> 
2. <span data-ttu-id="f81b7-160">Regolare **Transform -> Rotation** & **Transform -> Scale** dell'oggetto Pickup.</span><span class="sxs-lookup"><span data-stu-id="f81b7-160">Adjust the **Transform -> Rotation** & **Transform -> Scale** of the Pickup object.</span></span> 
   
    ![][25]
3. <span data-ttu-id="f81b7-161">Creare e collegare un **nuovo script C#** chiamato **Rotator** all'oggetto Pickup.</span><span class="sxs-lookup"><span data-stu-id="f81b7-161">Create and attach a **new C# Script** called **Rotator** to the Pickup object.</span></span> <span data-ttu-id="f81b7-162">Verificare di inserire lo script nella cartella Scripts.</span><span class="sxs-lookup"><span data-stu-id="f81b7-162">Make sure to put the script under the Scripts folder.</span></span> 
   
    ![][26]
4. <span data-ttu-id="f81b7-163">Aprire lo script per la modifica e aggiornarlo come segue:</span><span class="sxs-lookup"><span data-stu-id="f81b7-163">Open this script for editing and update it to be the following:</span></span> 
   
        using UnityEngine;
        using System.Collections;
   
        public class Rotator : MonoBehaviour {
   
            void Update () 
            {
                transform.Rotate (new Vector3 (15, 30, 45) * Time.deltaTime);
            }
        }
5. <span data-ttu-id="f81b7-164">Selezionare ora la modalità Play nell'editor di Unity per far ruotare l'oggetto Pickup sul proprio asse.</span><span class="sxs-lookup"><span data-stu-id="f81b7-164">Now hit the Play mode in the Unity Editor and your Pickup object show be rotating on its axis.</span></span>
6. <span data-ttu-id="f81b7-165">Creare una nuova cartella denominata **Prefabs**</span><span class="sxs-lookup"><span data-stu-id="f81b7-165">Create a new folder called **Prefabs**</span></span> 
   
    ![][27]
7. <span data-ttu-id="f81b7-166">Trascinare l'oggetto **Pickup** e inserirlo nella cartella Prefabs.</span><span class="sxs-lookup"><span data-stu-id="f81b7-166">Drag the **Pickup** object and put it in the Prefabs folder.</span></span>
   
    ![][28]
8. <span data-ttu-id="f81b7-167">Creare un nuovo **oggetto Empty Game** chiamato **Pickups**.</span><span class="sxs-lookup"><span data-stu-id="f81b7-167">Create a new **Empty Game object** called **Pickups**.</span></span> <span data-ttu-id="f81b7-168">Reimpostarne la posizione sull'origine e quindi trascinare l'oggetto Pickup sotto l'oggetto gioco.</span><span class="sxs-lookup"><span data-stu-id="f81b7-168">Reset its position to origin and then drag the Pickup object under this game object.</span></span>  
   
    ![][29]
9. <span data-ttu-id="f81b7-169">Duplicare l'oggetto **Pickup** e distribuirlo nell'oggetto **Ground** attorno all'oggetto **Player** aggiornando in modo appropriato i valori **X e Z di Transform.Position**.</span><span class="sxs-lookup"><span data-stu-id="f81b7-169">Duplicate the **Pickup** object and spread it on the **Ground** object around the **Player** object by updating the **Transform.Position's X & Z** values appropriately.</span></span> 
   
    ![][30]
10. <span data-ttu-id="f81b7-170">Creare un **nuovo materiale** chiamato **Pickup** e impostarlo sul colore rosso aggiornando la **proprietà Albedo** tramite una procedura simile a quella seguita per l'aggiornamento dell'oggetto Ground.</span><span class="sxs-lookup"><span data-stu-id="f81b7-170">Create a **new material** called **Pickup** and update it to be Red in color by updating the **Albedo property** similar to what we did for updating the Ground object.</span></span> 
    
    ![][31]
11. <span data-ttu-id="f81b7-171">Applicare il materiale a tutti e 4 gli oggetti Pickup.</span><span class="sxs-lookup"><span data-stu-id="f81b7-171">Apply the material to all the 4 pickup objects.</span></span>
    
    ![][32]

### <a name="collecting-the-pickup-objects"></a><span data-ttu-id="f81b7-172">Raccolta degli oggetti Pickup</span><span class="sxs-lookup"><span data-stu-id="f81b7-172">Collecting the Pickup objects</span></span>
<span data-ttu-id="f81b7-173">I passaggi seguenti sono tratti dall' [esercitazione di Unity](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span><span class="sxs-lookup"><span data-stu-id="f81b7-173">The steps below are from the [Unity tutorial](https://unity3d.com/learn/tutorials/projects/roll-a-ball/collecting-pick-up-objects?playlist=17141).</span></span> <span data-ttu-id="f81b7-174">Verrà aggiornato il Player in modo che possa raccogliere gli oggetti Pickup scontrandosi con essi.</span><span class="sxs-lookup"><span data-stu-id="f81b7-174">We will update the Player so that it is able to 'collect' the pickup objects by colliding with them.</span></span> 

1. <span data-ttu-id="f81b7-175">Aprire lo script **PlayerController** collegato all'oggetto Player per la modifica e aggiornarlo come segue:</span><span class="sxs-lookup"><span data-stu-id="f81b7-175">Open up the **PlayerController** script attached to the Player object for editing and update it to the following:</span></span>  
   
        using UnityEngine;
        using System.Collections;
   
        public class PlayerController : MonoBehaviour {
   
            public float speed;
   
            private Rigidbody rb;
   
            void Start ()
            {
                rb = GetComponent<Rigidbody>();
            }
   
            void FixedUpdate ()
            {
                float moveHorizontal = Input.GetAxis ("Horizontal");
                float moveVertical = Input.GetAxis ("Vertical");
   
                Vector3 movement = new Vector3 (moveHorizontal, 0.0f, moveVertical);
   
                rb.AddForce (movement * speed);
            }
   
            void OnTriggerEnter(Collider other) 
            {
                if (other.gameObject.CompareTag ("Pick Up"))
                {
                    other.gameObject.SetActive (false);
                }
            }
        }
2. <span data-ttu-id="f81b7-176">Creare un nuovo **tag** chiamato **Pick Up** (deve corrispondere ai contenuti dello script)</span><span class="sxs-lookup"><span data-stu-id="f81b7-176">Create a new **Tag** called **Pick Up** (it must match what is in the script)</span></span>  
   
    ![][33]
   
    ![][34]
3. <span data-ttu-id="f81b7-177">Applicare questo **Tag** all'oggetto Pickup di Prefab.</span><span class="sxs-lookup"><span data-stu-id="f81b7-177">Apply this **Tag** to the Prefab Pickup object.</span></span> 
   
    ![][35]
4. <span data-ttu-id="f81b7-178">Abilitare la casella di controllo **IsTrigger** per l'oggetto Prefab.</span><span class="sxs-lookup"><span data-stu-id="f81b7-178">Enable **IsTrigger** checkbox for the Prefab object.</span></span>
   
    ![][36]
5. <span data-ttu-id="f81b7-179">Aggiungere un Rigid body all'oggetto Pickup di Prefab.</span><span class="sxs-lookup"><span data-stu-id="f81b7-179">Add a Rigid body to Pickup Prefab object.</span></span> <span data-ttu-id="f81b7-180">Per ottimizzare le prestazioni, il collider statico usato verrà sostituito con un collider dinamico.</span><span class="sxs-lookup"><span data-stu-id="f81b7-180">For performance optimization we will update the static collider that we used to a Dynamic collider.</span></span> 
   
    ![][37]
6. <span data-ttu-id="f81b7-181">Selezionare infine la proprietà **IsKinematic** dell'oggetto Prefab.</span><span class="sxs-lookup"><span data-stu-id="f81b7-181">Finally check the **IsKinematic** property for the prefab object.</span></span> 
   
    ![][38]
7. <span data-ttu-id="f81b7-182">Premere **Play** nell'editor Unity e sarà possibile giocare a **Roll a Ball** spostando l'oggetto Player tramite i tasti della tastiera per indicare la direzione.</span><span class="sxs-lookup"><span data-stu-id="f81b7-182">Hit **Play** in the Unity editor and you will be able to play this **Roll a Ball** game by moving the Player object using your keyboard keys for direction input.</span></span> 

### <a name="updating-the-game-for-mobile-play"></a><span data-ttu-id="f81b7-183">Aggiornamento del gioco per la riproduzione su dispositivo mobile</span><span class="sxs-lookup"><span data-stu-id="f81b7-183">Updating the game for mobile play</span></span>
<span data-ttu-id="f81b7-184">Con le sezioni precedenti si è conclusa l'esercitazione di base di Unity.</span><span class="sxs-lookup"><span data-stu-id="f81b7-184">The sections above concluded the basic tutorial from Unity.</span></span> <span data-ttu-id="f81b7-185">Ora il gioco verrà modificato in modo che sia semplice da usare sui dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="f81b7-185">Now we will modify the game to make it mobile device friendly.</span></span> <span data-ttu-id="f81b7-186">Si noti che finora per il test è stato usato l'input da tastiera.</span><span class="sxs-lookup"><span data-stu-id="f81b7-186">Note that we used keyboard input for the game so far for testing.</span></span> <span data-ttu-id="f81b7-187">Ora verrà modificato per garantire il controllo del giocatore tramite movimenti del telefono, ad esempio</span><span class="sxs-lookup"><span data-stu-id="f81b7-187">Now we will modify it so that we can control the player by using the motion of the phone i.e.</span></span> <span data-ttu-id="f81b7-188">usando l'accelerometro come input.</span><span class="sxs-lookup"><span data-stu-id="f81b7-188">using Accelerometer as the input.</span></span> 

<span data-ttu-id="f81b7-189">Aprire lo script **PlayerController** per modificare e aggiornare il metodo **FixedUpdate** in modo da usare il movimento dell'accelerometro per spostare l'oggetto Player.</span><span class="sxs-lookup"><span data-stu-id="f81b7-189">Open up the **PlayerController** script for editing and update the **FixedUpdate** method to use the motion from the accelerometer to move the Player object.</span></span> 

        void FixedUpdate()
        {
            //float moveHorizontal = Input.GetAxis("Horizontal");
            //float moveVertical = Input.GetAxis("Vertical");
            //Vector3 movement = new Vector3(moveHorizontal, 0.0f, moveVertical);
            rb.AddForce(Input.acceleration.x * Speed, 0, -Input.acceleration.z * Speed);
        }

<span data-ttu-id="f81b7-190">Con questa esercitazione termina la creazione di un gioco di base con Unity, che può essere distribuito e usato sul dispositivo preferito.</span><span class="sxs-lookup"><span data-stu-id="f81b7-190">This tutorial concludes a basic game creation with Unity and you can deploy this on a device of your choice to play the game.</span></span> 

<!-- Images -->
[1]: ./media/mobile-engagement-unity-roll-a-ball/1.png    
[2]: ./media/mobile-engagement-unity-roll-a-ball/2.png
[3]: ./media/mobile-engagement-unity-roll-a-ball/3.png
[4]: ./media/mobile-engagement-unity-roll-a-ball/4.png
[5]: ./media/mobile-engagement-unity-roll-a-ball/5.png
[6]: ./media/mobile-engagement-unity-roll-a-ball/6.png
[7]: ./media/mobile-engagement-unity-roll-a-ball/7.png
[8]: ./media/mobile-engagement-unity-roll-a-ball/8.png
[9]: ./media/mobile-engagement-unity-roll-a-ball/9.png    
[10]: ./media/mobile-engagement-unity-roll-a-ball/10.png    
[11]: ./media/mobile-engagement-unity-roll-a-ball/11.png    
[12]: ./media/mobile-engagement-unity-roll-a-ball/12.png
[13]: ./media/mobile-engagement-unity-roll-a-ball/13.png
[14]: ./media/mobile-engagement-unity-roll-a-ball/14.png
[15]: ./media/mobile-engagement-unity-roll-a-ball/15.png
[16]: ./media/mobile-engagement-unity-roll-a-ball/16.png
[17]: ./media/mobile-engagement-unity-roll-a-ball/17.png
[18]: ./media/mobile-engagement-unity-roll-a-ball/18.png
[19]: ./media/mobile-engagement-unity-roll-a-ball/19.png    
[20]: ./media/mobile-engagement-unity-roll-a-ball/20.png    
[21]: ./media/mobile-engagement-unity-roll-a-ball/21.png    
[22]: ./media/mobile-engagement-unity-roll-a-ball/22.png    
[23]: ./media/mobile-engagement-unity-roll-a-ball/23.png    
[24]: ./media/mobile-engagement-unity-roll-a-ball/24.png    
[25]: ./media/mobile-engagement-unity-roll-a-ball/25.png    
[26]: ./media/mobile-engagement-unity-roll-a-ball/26.png    
[27]: ./media/mobile-engagement-unity-roll-a-ball/27.png    
[28]: ./media/mobile-engagement-unity-roll-a-ball/28.png    
[29]: ./media/mobile-engagement-unity-roll-a-ball/29.png    
[30]: ./media/mobile-engagement-unity-roll-a-ball/30.png    
[31]: ./media/mobile-engagement-unity-roll-a-ball/31.png    
[32]: ./media/mobile-engagement-unity-roll-a-ball/32.png    
[33]: ./media/mobile-engagement-unity-roll-a-ball/33.png    
[34]: ./media/mobile-engagement-unity-roll-a-ball/34.png    
[35]: ./media/mobile-engagement-unity-roll-a-ball/35.png    
[36]: ./media/mobile-engagement-unity-roll-a-ball/36.png    
[37]: ./media/mobile-engagement-unity-roll-a-ball/37.png    
[38]: ./media/mobile-engagement-unity-roll-a-ball/38.png    
[51]: ./media/mobile-engagement-unity-roll-a-ball/new-project.png
[52]: ./media/mobile-engagement-unity-roll-a-ball/new-project-properties.png
[53]: ./media/mobile-engagement-unity-roll-a-ball/save-scene.png













