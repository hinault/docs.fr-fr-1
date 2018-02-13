---
title: services de chiffrement
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cryptography [.NET Framework]
- pattern of derived class inheritance
- digital signatures
- asymmetric cryptographic algorithms
- digital signatures, public-key systems
- public keys
- decryptioin [.NET Framework]
- private keys
- MAC algorithms
- cryptographic algorithms
- private keys, overview
- encryption [.NET Framework]
- security [.NET Framework], encryption
- cryptographic services
- symmetric cryptographic algorithms
- hash
- message authentication codes
- derived class inheritance
- cryptography [.NET Framework], about
- random number generation
ms.assetid: f96284bc-7b73-44b5-ac59-fac613ad09f8
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 941dd9d130a31c997b634bce8059afef04c178d3
ms.sourcegitcommit: cf22b29db780e532e1090c6e755aa52d28273fa6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="cryptographic-services"></a>services de chiffrement
<a name="top"></a> Les réseaux publics, tels qu'Internet, n'offrent aucun moyen de sécuriser les communications entre les entités. Les communications qui transitent par ces réseaux sont susceptibles d'être lues voire modifiées par des tiers non autorisés. Le chiffrement permet de prévenir la consultation des données, offre des moyens de détecter si les données ont été modifiées et fournit un mode de communication sécurisé via des canaux qui autrement ne sont pas sécurisés. Par exemple, les données peuvent être chiffrées à l'aide d'un algorithme de chiffrement, transmises dans un état chiffré et par la suite déchiffrées par le destinataire prévu. Si un tiers intercepte les données chiffrées, il lui sera difficile de les déchiffrer.  
  
 Dans le .NET Framework, les classes de l'espace de noms <xref:System.Security.Cryptography?displayProperty=nameWithType> gèrent automatiquement divers détails liés au chiffrement. Certaines d'entre elles sont des wrappers pour l'API de chiffrement Microsoft non managée (CryptoAPI), tandis que d'autres sont de pures implémentations managées. Vous n'avez pas besoin d'être un expert en chiffrement pour utiliser ces classes. Quand vous créez une instance de l'une des classes d'algorithme de chiffrement, les clés sont générées automatiquement pour une plus grande facilité d'utilisation, et les propriétés par défaut sont aussi sûres et sécurisées que possible.  
  
 Cette vue d'ensemble offre un résumé des différentes méthodes et pratiques de chiffrement prises en charge par le .NET Framework, notamment les manifestes ClickOnce et la prise en charge de Suite B et de Cryptography Next Generation (CNG) introduite dans le [!INCLUDE[net_v35_long](../../../includes/net-v35-long-md.md)].  
  
 Cette vue d'ensemble contient les sections suivantes :  
  
-   [Primitives de chiffrement](#primitives)  
  
-   [Chiffrement à clé secrète](#secret_key)  
  
-   [Chiffrement à clé publique](#public_key)  
  
-   [Digital Signatures](#digital_signatures)  
  
-   [Valeurs de hachage](#hash_values)  
  
-   [Random Number Generation](#random_numbers)  
  
-   [Manifestes ClickOnce](#clickonce)  
  
-   [Prise en charge de Suite B](#suite_b)  
  
-   [Rubriques connexes](#related_topics)  
  
 Pour plus d'informations sur le chiffrement et les services, composants et outils Microsoft qui permettent d'ajouter à vos applications une sécurité par chiffrement, consultez la section relative au développement et à la sécurité Win32 et COM de cette documentation.  
  
<a name="primitives"></a>   
## <a name="cryptographic-primitives"></a>Primitives de chiffrement  
 Dans un cas classique où le chiffrement est utilisé, la communication entre deux parties (Alice et Jean) se fait via un canal non sécurisé. Alice et Jean veulent s'assurer que leurs communications restent incompréhensibles pour quiconque les écouterait. De plus, comme Alice et Jean sont distants l'un de l'autre, Alice doit s'assurer que les informations qu'elle reçoit de Jean n'ont pas été modifiées par quiconque durant la transmission. Par ailleurs, elle doit s'assurer que les informations viennent bien de Jean et non d'une personne qui aurait emprunté son identité.  
  
 Le chiffrement vise à atteindre les objectifs suivants :  
  
-   Confidentialité : pour empêcher la lecture de l'identité ou des données d'un utilisateur.  
  
-   Intégrité des données : pour empêcher la modification des données.  
  
-   Authentification : pour s'assurer que les données viennent bien d'un tiers donné.  
  
-   Non-répudiation : pour empêcher un tiers donné de nier qu'il a envoyé un message.  
  
 Pour atteindre ces objectifs, vous pouvez utiliser une combinaison d'algorithmes et de pratiques appelés primitives de chiffrement pour créer un modèle de chiffrement. Le tableau suivant répertorie les primitives de chiffrement et leurs fonctions.  
  
|Primitive de chiffrement|Utilisez|  
|-----------------------------|---------|  
|Chiffrement à clé secrète (chiffrement symétrique)|Transforme les données pour empêcher des tiers de les lire. Ce type de chiffrement fait appel à une clé partagée, secrète et unique pour chiffrer et déchiffrer des données.|  
|Chiffrement à clé publique (chiffrement asymétrique)|Transforme les données pour empêcher des tiers de les lire. Ce type de chiffrement fait appel à une paire de clés publique/privée pour chiffrer et déchiffrer les données.|  
|Signature chiffrée|Permet de vérifier que les données viennent bien d'un tiers déterminé en créant une signature numérique qui lui est propre. Ce processus utilise aussi des fonctions de hachage.|  
|Hachages de chiffrement|Mappe les données de n'importe quelle longueur à une séquence d'octets de longueur fixe. Les hachages sont statistiquement uniques ; deux séquences de deux octets n'auront jamais la même valeur de hachage.|  
  
 [Retour au début](#top)  
  
<a name="secret_key"></a>   
## <a name="secret-key-encryption"></a>Chiffrement à clé secrète  
 Les algorithmes de chiffrement à clé secrète font appel à une clé secrète unique pour chiffrer et déchiffrer les données. Vous devez sécuriser la clé pour empêcher des agents non autorisés d'y accéder, car n'importe quel tiers qui aurait la clé en sa possession pourrait s'en servir pour déchiffrer vos données ou chiffrer les siennes en prétendant qu'elles viennent de vous.  
  
 Le chiffrement à clé secrète est aussi appelé chiffrement symétrique, car la même clé est utilisée pour le chiffrement et déchiffrement. Les algorithmes de chiffrement à clé secrète sont très rapides (par rapport aux algorithmes à clé publique) et se prêtent bien aux transformations de chiffrement sur les flux de données importants. Les algorithmes de chiffrement asymétrique tels que RSA sont limités mathématiquement quant à la quantité de données qu'ils peuvent chiffrer. En général, les algorithmes de chiffrement symétrique n'ont pas ces problèmes.  
  
 Un type d'algorithme à clé secrète appelé chiffrement par blocs est utilisé pour chiffrer un bloc de données à la fois. Les chiffrements par blocs tels que Data Encryption Standard (DES), TripleDES et Advanced Encryption Standard (AES) transforment par chiffrement un bloc d'entrée de *n* octets en un bloc d'octets chiffrés de sortie. Si vous voulez chiffrer ou déchiffrer une séquence d'octets, vous devez le faire bloc par bloc. Sachant que la valeur *n* est faible (8 octets pour DES et TripleDES ; 16 octets [par défaut], 24 octets ou 32 octets pour AES), les valeurs de données supérieures à *n* doivent être chiffrées un bloc à la fois. Les valeurs de données inférieures à *n* doivent être étendues à *n* afin d'être traitées.  
  
 Il existe une forme simple de chiffrement par blocs, qui est appelée « mode ECB » (Electronic Codebook, livre de codes électronique). Le mode ECB n'est pas considéré comme sécurisé, car il n'utilise pas de vecteur d'initialisation pour initialiser le premier bloc de texte en clair. Pour une clé secrète donnée *k*, un simple chiffrement par blocs qui n'utilise pas de vecteur d'initialisation chiffrera-t-il un même bloc d'entrée de texte en clair en bloc de sortie de texte chiffré équivalent. Par conséquent, si vous avez des blocs en double dans votre flux de texte en clair d'entrée, vous aurez des blocs en double dans votre flux de texte chiffré de sortie. La présence de ces blocs de sortie en double alerteront les utilisateurs non autorisés sur la faiblesse du chiffrement utilisé, sur les algorithmes qui ont pu être utilisés et sur les modes d'attaque possibles. Le mode de chiffrement ECB est donc assez vulnérable à l'analyse et, en fin de compte, à la découverte de clés.  
  
 Les classes de chiffrement par blocs fournies dans la bibliothèque de classes de base utilisent un mode de chaînage par défaut appelé CBC (Cipher-Block Chaining, chaînage de blocs de chiffrement), mais vous pouvez éventuellement modifier ce mode par défaut.  
  
 Le chiffrement CBC surpasse les problèmes liés au chiffrement ECB en utilisant un vecteur d'initialisation pour chiffrer le premier bloc de texte en clair. Avant d'être chiffré, chaque bloc de texte en clair suivant fait l'objet d'une opération OR exclusive au niveau du bit (`XOR`) avec le bloc de texte chiffré précédent. Chaque bloc de texte chiffré dépend donc de tous les blocs précédents. Avec ce système, les en-têtes de message courants qu'un utilisateur non autorisé pourrait connaître ne peuvent pas être utilisés pour reconstituer une clé.  
  
 Une façon de compromettre des données chiffrées avec un chiffrement CBC est d'effectuer une recherche exhaustive de chaque clé possible. Selon la taille de la clé utilisée pour effectuer le chiffrement, ce type de recherche peut être extrêmement fastidieux, sinon impossible, même en utilisant les ordinateurs les plus rapides. Les clés de grande taille sont plus difficiles à déchiffrer. Même si, en théorie, le chiffrement n'empêche pas un adversaire de récupérer les données chiffrées, il rend la tâche bien plus difficile. S'il faut trois mois pour effectuer une recherche exhaustive en vue de récupérer des données qui ne seront valables que quelques jours, cette méthode de recherche ne revêt aucun intérêt.  
  
 L'inconvénient du chiffrement à clé secrète est qu'il suppose que les deux parties se sont mises d'accord sur une clé et un vecteur d'initialisation et qu'elles se sont communiqué leurs valeurs. Le vecteur d'initialisation n'est pas considéré comme un secret et peut être transmis en texte en clair avec le message. Cependant, la clé doit être tenue secrète des utilisateurs non autorisés. Du fait de ces problèmes, le chiffrement à clé secrète est souvent employé conjointement avec le chiffrement à clé publique pour communiquer de manière confidentielle les valeurs de la clé et du vecteur d'initialisation.  
  
 Si l'on considère qu'Alice et Jean sont deux parties qui désirent communiquer sur un canal non sécurisé, ils peuvent utiliser le chiffrement à clé secrète comme suit : Alice et Jean conviennent ensemble d'utiliser un certain algorithme (AES, par exemple) avec une clé et un vecteur d'initialisation déterminés. Alice compose un message et crée un flux de réseau (par exemple un e-mail nommé canal ou de réseau) sur lequel envoyer le message. Ensuite, elle chiffre le texte à l'aide de la clé et du vecteur d'initialisation, puis envoie le message chiffré et le vecteur d'initialisation à Jean via l'intranet. Jean reçoit le texte chiffré et le déchiffre à l'aide du vecteur d'initialisation et de la clé convenue précédemment. Si la transmission est interceptée, l'intercepteur ne peut pas récupérer le message d'origine, car il ne connaît pas la clé. Dans ce scénario, seule la clé doit rester secrète. Dans un scénario réel, Alice ou Jean génère une clé secrète et utilise un chiffrement (asymétrique) à clé publique pour transférer la clé (symétrique) secrète à l'autre partie. Pour plus d'informations sur le chiffrement à clé publique, consultez la section suivante.  
  
 Le [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] fournit les classes suivantes, qui implémentent des algorithmes de chiffrement à clé secrète :  
  
-   <xref:System.Security.Cryptography.AesManaged> (introduit dans le [!INCLUDE[net_v35_long](../../../includes/net-v35-long-md.md)]).  
  
-   <xref:System.Security.Cryptography.DESCryptoServiceProvider>.  
  
-   <xref:System.Security.Cryptography.HMACSHA1> (Techniquement, il s'agit d'un algorithme de clé secrète dans la mesure où il représente un code d'authentification de message calculé à l'aide d'une fonction de hachage de chiffrement combinée à une une clé secrète. Consultez la section [Valeurs de hachage](#hash_values), plus loin dans cette rubrique.)  
  
-   <xref:System.Security.Cryptography.RC2CryptoServiceProvider>.  
  
-   <xref:System.Security.Cryptography.RijndaelManaged>.  
  
-   <xref:System.Security.Cryptography.TripleDESCryptoServiceProvider>.  
  
 [Retour au début](#top)  
  
<a name="public_key"></a>   
## <a name="public-key-encryption"></a>Chiffrement à clé publique  
 Le chiffrement à clé publique fait appel à une clé privée qui doit être tenue secrète des utilisateurs non autorisés et à une clé publique qui peut être divulguée à n'importe qui. La clé publique et la clé privée sont liées mathématiquement ; les données chiffrées avec la clé publique ne peuvent être déchiffrées qu'avec la clé privée, tandis que les données signées avec la clé privée ne peuvent être vérifiées qu'avec la clé publique. La clé publique peut être divulguée à n'importe qui ; elle sert à chiffrer les données à envoyer au détenteur de la clé privée. Les algorithmes de chiffrement à clé publique sont aussi appelés algorithmes asymétriques, car ils font appel à une clé pour chiffrer les données et à une autre clé pour les déchiffrer. Il existe une règle de base en matière de chiffrement qui interdit la réutilisation d'une clé. Par ailleurs, les deux clés doivent être uniques pour chaque session de communication. Or, dans la pratique, les clés asymétriques ont généralement une longue durée de vie.  
  
 Les deux parties (Alice et Jean) peuvent utiliser le chiffrement à clé publique comme suit : dans un premier temps, Alice génère une paire de clés publique/privée. Si Jean veut envoyer un message chiffré à Alice, il lui réclame sa clé publique. Alice envoie sa clé publique à Jean via un réseau non sécurisé et Jean utilise cette clé pour chiffrer un message. Jean envoie le message chiffré à Alice, qui le déchiffre à l'aide de sa clé privée. Si Jean a reçu la clé d'Alice via un canal non sécurisé, tel qu'un réseau public, il est exposé à une « attaque de l'intercepteur ». Par conséquent, Jean doit vérifier auprès d'Alice que la copie dont il dispose de sa clé publique est correcte.  
  
 Pendant la transmission de la clé publique d'Alice, le risque existe qu'un agent non autorisé intercepte la clé. De plus, ce même agent pourrait intercepter le message chiffré de Jean. En revanche, l'agent ne peut pas déchiffrer le message avec la clé publique. Le message ne peut être déchiffré qu'avec la clé privée d'Alice, qui n'a pas été transmise. Alice n'utilise pas sa clé privée pour chiffrer un message de réponse à Jean, car quiconque en possession de la clé publique pourrait déchiffrer le message. Si Alice souhaite envoyer une réponse à Bob, elle réclame à Jean sa clé publique et chiffre son message à l'aide de cette clé publique. Jean déchiffre ensuite le message à l'aide de sa clé privée associée.  
  
 Dans ce scénario, Alice et Jean utilisent le chiffrement à clé publique (asymétrique) pour transférer une clé secrète (symétrique) et utilisent le chiffrement à clé secrète pour le reste de leur session.  
  
 La liste suivante propose une comparaison entre les algorithmes de chiffrement à clé publique et à clé secrète :  
  
-   Les algorithmes de chiffrement à clé publique utilisent une taille de mémoire tampon fixe, tandis que les algorithmes de chiffrement à clé secrète utilisent une mémoire tampon de longueur variable.  
  
-   Les algorithmes à clé publique ne peuvent pas être utilisés pour chaîner ensemble des données sous forme de flux à la manière des algorithmes à clé secrète, car seules de petites quantités de données peuvent être chiffrées. Par conséquent, les opérations asymétriques n'utilisent pas le même modèle de diffusion en continu que les opérations symétriques.  
  
-   Le chiffrement à clé publique dispose d'un plus grand espace de clés (plage de valeurs possibles pour la clé) que le chiffrement à clé secrète. Par conséquent, le chiffrement à clé publique est moins vulnérable aux attaques exhaustives qui essaient toutes les clés possibles.  
  
-   Les clés publiques sont faciles à distribuer dans la mesure où elles n'ont pas besoin d'être sécurisées, à condition qu'il existe un moyen de vérifier l'identité de l'expéditeur.  
  
-   Certains algorithmes à clé publique (tels que RSA et DSA, mais pas Diffie-Hellman) permettent de créer des signatures numériques pour vérifier l'identité de l'expéditeur des données.  
  
-   Les algorithmes à clé publique sont très plus lents par rapport aux algorithmes à clé secrète et ne sont pas conçus pour chiffrer de grandes quantités de données. Les algorithmes à clé publique ne sont utiles que pour le transfert de très petites quantités de données. En règle générale, le chiffrement à clé publique est utilisé pour chiffrer la clé et le vecteur d'initialisation destiné à être utilisé par un algorithme à clé secrète. Une fois la clé et le vecteur d'initialisation transférés, le chiffrement à clé secrète est utilisé pour le reste de la session.  
  
 Le [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] fournit les classes suivantes, qui implémentent des algorithmes de chiffrement à clé publique :  
  
-   <xref:System.Security.Cryptography.DSACryptoServiceProvider>  
  
-   <xref:System.Security.Cryptography.RSACryptoServiceProvider>  
  
-   <xref:System.Security.Cryptography.ECDiffieHellman> (classe de base)  
  
-   <xref:System.Security.Cryptography.ECDiffieHellmanCng>  
  
-   <xref:System.Security.Cryptography.ECDiffieHellmanCngPublicKey> (classe de base)  
  
-   <xref:System.Security.Cryptography.ECDiffieHellmanKeyDerivationFunction> (classe de base)  
  
-   <xref:System.Security.Cryptography.ECDsaCng>  
  
 Si RSA autorise à la fois le chiffrement et la signature, DSA ne peut être utilisé que pour la signature et Diffie-Hellman seulement pour la génération de clés. En général, les algorithmes à clé publique sont plus limités dans leurs utilisations que les algorithmes à clé privée.  
  
 [Retour au début](#top)  
  
<a name="digital_signatures"></a>   
## <a name="digital-signatures"></a>signatures numériques  
 Les algorithmes à clé publique peuvent aussi être utilisés pour créer des signatures numériques. Les signatures numériques permettent d'authentifier l'identité d'un expéditeur (si vous jugez que sa clé publique est fiable) et d'assurer l'intégrité des données. En utilisant la clé publique générée par Alice, le destinataire des données d'Alice peut vérifier que c'est bien elle qui les a envoyées en comparant la signature numérique aux données et à la clé publique d'Alice.  
  
 Pour utiliser le chiffrement à clé publique pour signer numériquement un message, Alice applique d'abord un algorithme de hachage au message pour créer une synthèse du message. La synthèse du message est une représentation compacte et unique des données. Alice chiffre ensuite la synthèse du message à l'aide de sa clé privée pour créer sa signature personnelle. À réception du message et de la signature, Jean déchiffre la signature à l'aide de la clé publique d'Alice pour récupérer la synthèse du message et hache ce dernier en utilisant le même algorithme de hachage que celui utilisé par Alice. Si la synthèse du message calculé par Jean correspond exactement à la synthèse du message reçue d'Alice, Jean est assuré que le message provient de la détentrice de la clé privée et que les données n'ont pas été modifiées. Si Jean est convaincu qu'Alice est la détentrice de la clé privée, il sait que le message vient d'Alice.  
  
> [!NOTE]
>  Une signature peut être vérifiée par n'importe qui, car la clé publique de l'expéditeur est connue de tous et est généralement incluse dans le format de signature numérique. Cette méthode ne préserve pas le caractère confidentiel du message ; pour être secret, le message doit aussi être chiffré.  
  
 Le [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] fournit les classes suivantes, qui implémentent des algorithmes à signature numérique :  
  
-   <xref:System.Security.Cryptography.DSACryptoServiceProvider>  
  
-   <xref:System.Security.Cryptography.RSACryptoServiceProvider>  
  
-   <xref:System.Security.Cryptography.ECDsa> (classe de base)  
  
-   <xref:System.Security.Cryptography.ECDsaCng>  
  
 [Retour au début](#top)  
  
<a name="hash_values"></a>   
## <a name="hash-values"></a>Valeurs de hachage  
 Les algorithmes de hachage mappent les valeurs binaires de longueur arbitraire à des valeurs binaires de longueur fixe de plus petite taille appelées valeurs de hachage. Une valeur de hachage est une représentation numérique d'un élément de données. Si vous hachez un paragraphe de texte en clair et que vous modifiez ne serait-ce qu'une lettre du paragraphe, un hachage ultérieur générera une valeur différente. Si le hachage est renforcé sur le plan du chiffrement, sa valeur changera considérablement. Par exemple, si un seul bit est modifié dans un message, une fonction de hachage renforcé peut générer une sortie différente de 50 %. Diverses valeurs d'entrée peuvent être hachées dans une même valeur de sortie. En revanche, d'un point de vue informatique, il n'est pas possible que le hachage de deux entrées distinctes donne une même valeur.  
  
 Les deux parties que constituent Alice et Jean peuvent utiliser une fonction de hachage pour garantir l'intégrité des messages. Pour cela, ils doivent choisir un algorithme de hachage pour signer leurs messages. Alice écrit un message et crée ensuite un hachage de ce message à l'aide de l'algorithme sélectionné. Ils doivent ensuite appliquer l'une des méthodes suivantes :  
  
-   Alice envoie le message de texte en clair et le message haché (signature numérique) à Jean. Jean reçoit et hache le message et compare sa valeur de hachage à celle qu'il a reçue d'Alice. Si les valeurs de hachage sont identiques, cela signifie que le message n'a pas été modifié. Si les valeurs ne sont pas identiques, le message a été modifié après avoir été rédigé par Alice.  
  
     Malheureusement, cette méthode ne permet pas d'établir l'authenticité de l'expéditeur. N'importe qui peut emprunter l'identité d'Alice et envoyer un message à Jean. L'usurpateur peut utiliser le même algorithme de hachage pour signer son message et tout ce que Jean pourra constater, c'est que le message présente la même signature. Il s'agit d'une forme d'attaque de l'intercepteur. Consultez [NIB : exemple de Communication sécurisée Cryptography Next Generation (CNG)](http://msdn.microsoft.com/library/8048e94e-054a-417b-87c6-4f5e26710e6e) pour plus d’informations.  
  
-   Alice envoie le message de texte en clair à Jean via un canal public non sécurisé. Elle envoie le message haché à Jean via un canal privé sécurisé. Jean reçoit le message de texte en clair, le hache et compare le hachage à celui échangé en privé. Si les hachages correspondent, Jean peut en déduire deux choses :  
  
    -   le message n'a pas été modifié ;  
  
    -   l'expéditeur du message (Alice) est authentique.  
  
     Pour que ce système fonctionne, Alice doit cacher sa valeur de hachage d'origine à tous les tiers, à l'exception de Jean.  
  
-   Alice envoie le message de texte en clair à Jean via un canal public non sécurisé et place le message haché sur son site web accessible publiquement.  
  
     Cette méthode évite toute falsification du message en empêchant quiconque de modifier la valeur de hachage. Même si le message et son hachage peuvent être lus par n'importe qui, la valeur de hachage ne peut être modifiée que par Alice. Une personne malveillante qui chercherait à emprunter l'identité d'Alice doit avoir accès au site web d'Alice.  
  
 Aucune des méthodes précédentes n'empêchera quiconque de lire les messages d'Alice, car ils sont transmis sous forme de texte en clair. Pour bénéficier d'une sécurité complète, les signatures numériques (signature des messages) et le chiffrement s'avèrent nécessaires.  
  
 Le [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] fournit les classes suivantes, qui implémentent des algorithmes de hachage :  
  
-   <xref:System.Security.Cryptography.HMACSHA1>.  
  
-   <xref:System.Security.Cryptography.MACTripleDES>.  
  
-   <xref:System.Security.Cryptography.MD5CryptoServiceProvider>.  
  
-   <xref:System.Security.Cryptography.RIPEMD160>.  
  
-   <xref:System.Security.Cryptography.SHA1Managed>.  
  
-   <xref:System.Security.Cryptography.SHA256Managed>.  
  
-   <xref:System.Security.Cryptography.SHA384Managed>.  
  
-   <xref:System.Security.Cryptography.SHA512Managed>.  
  
-   Variantes HMAC de tous les algorithmes SHA (Secure Hash Algorithm), MD5 (Message Digest 5) et RIPEMD-160.  
  
-   Implémentations CryptoServiceProvider (wrappers de code managé) de tous les algorithmes SHA.  
  
-   Implémentations CNG (Cryptography Next Generation) de tous les algorithmes MD5 et SHA.  
  
> [!NOTE]
>  Suite à la découverte de défauts de conception de MD5 en 1996, il a été recommandé de le remplacer par SHA-1. En 2004, des défauts supplémentaires ont été découverts. Depuis, l'algorithme MD5 n'est plus considéré comme sécurisé. L'algorithme SHA-1 a aussi été pointé du doigt pour son manque de fiabilité et SHA-2 est désormais l'algorithme recommandé.  
  
 [Retour au début](#top)  
  
<a name="random_numbers"></a>   
## <a name="random-number-generation"></a>génération de nombres aléatoires  
 La génération de nombres aléatoires est un élément indispensable de nombreuses opérations de chiffrement. Par exemple, les clés de chiffrement doivent être aussi aléatoires que possible de sorte qu'il soit impossible de les reproduire. Les générateurs de nombres aléatoires de chiffrement doivent générer des sorties qu'il est impossible de prédire du point de vue informatique avec une probabilité de plus de 50 %. Par conséquent, toute méthode de prédiction du bit de sortie suivant ne doit pas pas se montrer plus performante que le hasard. Les classes du [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] utilisent des générateurs de nombres aléatoires pour générer des clés de chiffrement.  
  
 La classe <xref:System.Security.Cryptography.RNGCryptoServiceProvider> est une implémentation d'un algorithme de génération de nombres aléatoires.  
  
 [Retour au début](#top)  
  
<a name="clickonce"></a>   
## <a name="clickonce-manifests"></a>Manifestes ClickOnce  
 Dans le [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)], les classes de chiffrement suivantes vous permettent d'obtenir et de vérifier les informations sur les signatures de manifeste des applications déployées à l'aide de la [technologie ClickOnce](/visualstudio/deployment/clickonce-security-and-deployment):  
  
-   La classe <xref:System.Security.Cryptography.ManifestSignatureInformation> obtient des informations sur une signature de manifeste quand vous utilisez ses surcharges de méthode <xref:System.Security.Cryptography.ManifestSignatureInformation.VerifySignature%2A> .  
  
-   Vous pouvez utiliser l'énumération <xref:System.Security.ManifestKinds> pour spécifier les manifestes à vérifier. Le résultat de la vérification est l'une des valeurs d'énumération <xref:System.Security.Cryptography.SignatureVerificationResult> .  
  
-   La classe <xref:System.Security.Cryptography.ManifestSignatureInformationCollection> fournit une collection en lecture seule d'objets <xref:System.Security.Cryptography.ManifestSignatureInformation> des signatures vérifiées.  
  
 De plus, les classes suivantes fournissent des informations de signature spécifiques :  
  
-   <xref:System.Security.Cryptography.StrongNameSignatureInformation> contient les informations de signature de nom fort d'un manifeste.  
  
-   <xref:System.Security.Cryptography.X509Certificates.AuthenticodeSignatureInformation> représente les informations de signature Authenticode d'un manifeste.  
  
-   <xref:System.Security.Cryptography.X509Certificates.TimestampInformation> contient des informations sur l'horodatage d'une signature Authenticode.  
  
-   <xref:System.Security.Cryptography.X509Certificates.TrustStatus> offre un moyen simple de vérifier si une signature Authenticode est fiable.  
  
 [Retour au début](#top)  
  
<a name="suite_b"></a>   
## <a name="suite-b-support"></a>Prise en charge de Suite B  
 Le [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] prend en charge le jeu d'algorithmes de chiffrement Suite B publié par la NSA (National Security Agency). Pour plus d’informations sur Suite B, consultez le [NSA Suite B Cryptography Fact Sheet](https://www.nsa.gov/what-we-do/information-assurance/).  
  
 Les algorithmes inclus sont les suivants :  
  
-   Algorithme AES (Advanced Encryption Standard) avec des tailles de clé de 128, 192 et 256 bits pour le chiffrement.  
  
-   Algorithmes de hachage sécurisé SHA-1, SHA-256, SHA-384 et SHA-512 pour le hachage. (Les trois derniers sont généralement regroupés et appelés SHA-2.)  
  
-   Algorithme ECDSA (Elliptic Curve Digital Signature Algorithm), utilisant des courbes de moduli premiers de 256, 384 et 521 bits pour la signature. La documentation de la NSA définit précisément ces courbes et les appelle P-256, P-384 et P-521. Cet algorithme est fourni par la classe <xref:System.Security.Cryptography.ECDsaCng> . Il vous permet de signer à l'aide d'une clé privée et de vérifier la signature avec une clé publique.  
  
-   Algorithme Diffie-Hellman à courbe elliptique (ECDH, Elliptic Curve Diffie-Hellman), utilisant des courbes de moduli premiers de 256, 384 et 521 bits pour l'échange de clés et l'accord secret. Cet algorithme est fourni par la classe <xref:System.Security.Cryptography.ECDiffieHellmanCng> .  
  
 Des wrappers de code managé pour les implémentations certifiées FIPS (Federal Information Processing Standard) des implémentations AES, SHA-256, SHA-384 et SHA-512 sont disponibles dans les nouvelles classes <xref:System.Security.Cryptography.AesCryptoServiceProvider>, <xref:System.Security.Cryptography.SHA256CryptoServiceProvider>, <xref:System.Security.Cryptography.SHA384CryptoServiceProvider>et <xref:System.Security.Cryptography.SHA512CryptoServiceProvider> .  
  
 [Retour au début](#top)  
  
<a name="cng"></a>   
## <a name="cryptography-next-generation-cng-classes"></a>Classes CNG (Cryptography Next Generation)  
 Les classes CNG fournissent un wrapper managé autour des fonctions CNG natives. (CNG remplac CryptoAPI.) Le nom de ces classes comporte « Cng ». Au cœur des classes du wrapper CNG se trouve la classe de conteneur de clés <xref:System.Security.Cryptography.CngKey>, qui s'approprie le stockage et l'utilisation des clés CNG. Cette classe vous permet de stocker une paire de clés ou une clé publique en toute sécurité et d'y faire référence en utilisant un nom de chaîne simple. La classe de signature <xref:System.Security.Cryptography.ECDsaCng> à courbe elliptique et la classe de chiffrement <xref:System.Security.Cryptography.ECDiffieHellmanCng> peuvent utiliser des objets <xref:System.Security.Cryptography.CngKey> .  
  
 La classe <xref:System.Security.Cryptography.CngKey> sert à diverses autres opérations, notamment à ouvrir, créer, supprimer et exporter des clés. Elle permet aussi d'accéder au handle de clé sous-jacent à utiliser quand il s'agit d'appeler des fonctions natives directement.  
  
 Par ailleurs, le [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] inclut diverses classes CNG de prise en charge, notamment les suivantes :  
  
-   <xref:System.Security.Cryptography.CngProvider> dispose d'un fournisseur de stockage de clés.  
  
-   <xref:System.Security.Cryptography.CngAlgorithm> dispose d'un algorithme CNG.  
  
-   <xref:System.Security.Cryptography.CngProperty> dispose de propriétés de clé fréquemment utilisées.  
  
 [Retour au début](#top)  
  
<a name="related_topics"></a>   
## <a name="related-topics"></a>Rubriques connexes  
  
|Titre|Description|  
|-----------|-----------------|  
|[Modèle de chiffrement](../../../docs/standard/security/cryptography-model.md)|Explique comment le chiffrement est implémenté dans la bibliothèque de classes de base.|  
|[Procédure pas à pas : création d’une application de chiffrement](../../../docs/standard/security/walkthrough-creating-a-cryptographic-application.md)|Présente des tâches de chiffrement et de déchiffrement de base.|  
|[Configuration des classes de chiffrement](../../../docs/framework/configure-apps/configure-cryptography-classes.md)|Explique comment mapper des noms d'algorithmes à des classes de chiffrement et comment mapper des identificateurs d'objets à un algorithme de chiffrement.|
