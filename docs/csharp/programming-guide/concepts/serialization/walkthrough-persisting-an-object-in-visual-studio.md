---
title: "Procédure pas à pas : persistance d’un objet dans Visual Studio (C#)"
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-csharp
ms.topic: get-started-article
ms.assetid: a544ce46-ee25-49da-afd4-457a3d59bf63
caps.latest.revision: "3"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 7b1a3fc377875ee25baa0718a25b5ac509822154
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="walkthrough-persisting-an-object-in-visual-studio-c"></a>Procédure pas à pas : persistance d’un objet dans Visual Studio (C#)
Bien qu’il soit possible de définir des valeur par défaut pour les propriétés d’un objet au moment du design, les valeurs entrées lors de l’exécution sont perdues en cas de destruction de l’objet. Vous pouvez utiliser la sérialisation pour rendre les données d’un objet persistantes entre les instances, ce qui vous permet de stocker des valeurs et de les récupérer lors de la prochaine instanciation de l’objet.  
  
 Dans cette procédure pas à pas, vous allez créer un objet `Loan` simple et rendre ses données persistantes dans un fichier. Vous récupérerez ensuite les données du fichier lors de la recréation de l’objet.  
  
> [!IMPORTANT]
>  Cet exemple crée un fichier s’il n’existe pas déjà. Si une application doit créer un fichier, elle doit disposer de l’autorisation `Create` pour accéder au dossier. Les autorisations sont définies à l’aide de listes de contrôle d’accès. Si le fichier existe déjà, l’application a uniquement besoin de l’autorisation `Write`, ce qui représente une autorisation inférieure. Quand cela est possible, il est plus sûr de créer le fichier au cours du déploiement et de n’accorder l’autorisation `Read` que sur un seul fichier (plutôt que l’autorisation Créer sur un dossier). En outre, il est plus sûr d’écrire les données dans des dossiers utilisateur que dans le dossier racine ou le dossier Program Files.  
  
> [!IMPORTANT]
>  Cet exemple stocke les données dans un fichier au format binaire. Ces formats ne doivent pas être utilisés pour des données sensibles, telles que les mots de passe ou les informations relatives à la carte de crédit.  
  
> [!NOTE]
>  Les boîtes de dialogue et les commandes de menu qui s'affichent peuvent être différentes de celles qui sont décrites dans l'aide, en fonction de vos paramètres actifs ou de l'édition utilisée. Pour modifier ces paramètres, cliquez sur **Importation et exportation de paramètres** dans le menu **Outils** . Pour plus d’informations, consultez [Personnalisation des paramètres de développement dans Visual Studio](http://msdn.microsoft.com/library/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## <a name="creating-the-loan-object"></a>Création de l’objet Loan  
 La première étape consiste à créer une classe `Loan` et une application de test qui utilise cette classe.  
  
### <a name="to-create-the-loan-class"></a>Pour créer la classe Loan  
  
1.  Créez un projet Bibliothèque de classes et nommez-le « LoanClass ». Pour plus d’informations, consultez [Création de solutions et de projets](/visualstudio/ide/creating-solutions-and-projects).  
  
2.  Dans l’**Explorateur de solutions**, ouvrez le menu contextuel pour le fichier Class1, puis choisissez **Renommer**. Renommez le fichier `Loan` et appuyez sur Entrée. Quand vous renommez le fichier, la classe est également renommée `Loan`.  
  
3.  Ajoutez les membres publics suivants à la classe :  
  
    ```csharp  
    public class Loan : System.ComponentModel.INotifyPropertyChanged  
    {  
        public double LoanAmount {get; set;}  
        public double InterestRate {get; set;}  
        public int Term {get; set;}  
  
        private string p_Customer;  
        public string Customer  
        {  
            get { return p_Customer; }  
            set   
            {  
                p_Customer = value;  
                PropertyChanged(this,  
                  new System.ComponentModel.PropertyChangedEventArgs("Customer"));  
            }  
        }  
  
        public event System.ComponentModel.PropertyChangedEventHandler PropertyChanged;  
  
        public Loan(double loanAmount,  
                    double interestRate,  
                    int term,  
                    string customer)  
        {  
            this.LoanAmount = loanAmount;  
            this.InterestRate = interestRate;  
            this.Term = term;  
            p_Customer = customer;  
        }  
    }  
    ```  
  
 Vous devrez également créer une application simple qui utilise la classe `Loan`.  
  
### <a name="to-create-a-test-application"></a>Pour créer une application de test  
  
1.  Pour ajouter un projet d’application Windows Forms à votre solution, dans le menu **Fichier**, choisissez **Ajouter**, **Nouveau projet**.  
  
2.  Dans la boîte de dialogue **Ajouter un nouveau projet**, choisissez **Application Windows Forms** et entrez `LoanApp` comme nom du projet, puis cliquez sur **OK** pour fermer la boîte de dialogue.  
  
3.  Dans l’**Explorateur de solutions**, choisissez le projet LoanApp.  
  
4.  Dans le menu **Projet**, choisissez **Définir comme projet de démarrage**.  
  
5.  Dans le menu **Projet** , choisissez **Ajouter une référence**.  
  
6.  Dans la boîte de dialogue **Ajouter une référence**, choisissez l’onglet **Projets**, puis le projet LoanClass.  
  
7.  Cliquez sur **OK** pour fermer la boîte de dialogue.  
  
8.  Dans le concepteur, ajoutez quatre contrôles <xref:System.Windows.Forms.TextBox> au formulaire.  
  
9. Dans l'éditeur de code, ajoutez le code suivant :  
  
    ```csharp  
    private LoanClass.Loan TestLoan = new LoanClass.Loan(10000.0, 0.075, 36, "Neil Black");  
  
    private void Form1_Load(object sender, EventArgs e)  
    {  
        textBox1.Text = TestLoan.LoanAmount.ToString();  
        textBox2.Text = TestLoan.InterestRate.ToString();  
        textBox3.Text = TestLoan.Term.ToString();  
        textBox4.Text = TestLoan.Customer;  
    }  
    ```  
  
10. Ajoutez un gestionnaire d’événements pour l’événement `PropertyChanged` au formulaire en utilisant le code suivant :  
  
    ```csharp  
    private void CustomerPropertyChanged(object sender,   
        System.ComponentModel.PropertyChangedEventArgs e)  
    {  
        MessageBox.Show(e.PropertyName + " has been changed.");  
    }  
    ```  
  
 À ce stade, vous pouvez générer et exécuter l’application. Notez que les valeurs par défaut de la classe `Loan` apparaissent dans les zones de texte. Essayez de remplacer le taux d’intérêt 7,5 par 7,1, puis fermez l’application et exécutez-la de nouveau : le taux reprend sa valeur par défaut de 7,5.  
  
 Dans la réalité, les taux d’intérêt changent régulièrement, mais pas nécessairement chaque fois que l’application est exécutée. Plutôt que d’imposer à l’utilisateur de mettre à jour le taux d’intérêt chaque fois qu’il exécute l’application, il peut être plus judicieux de conserver le taux d’intérêt le plus récent entre les instances de l’application. C’est ce que vous ferez à l’étape suivante, en ajoutant la sérialisation à la classe Loan.  
  
## <a name="using-serialization-to-persist-the-object"></a>Utilisation de la sérialisation pour rendre l’objet persistant  
 Pour rendre les valeurs de la classe Loan persistantes, vous devez d’abord marquer la classe avec l’attribut `Serializable`.  
  
### <a name="to-mark-a-class-as-serializable"></a>Pour marquer une classe comme étant sérialisable  
  
-   Modifiez la déclaration de la classe Loan de la façon suivante :  
  
    ```csharp  
    [Serializable()]  
    public class Loan : System.ComponentModel.INotifyPropertyChanged  
    {  
    ```  
  
 L’attribut `Serializable` indique au compilateur que tout ce que contient la classe peut être persistant dans un fichier. Étant donné que l’événement `PropertyChanged` est géré par un objet Windows Form, il ne peut pas être sérialisé. L’attribut `NonSerialized` peut être utilisé pour marquer les membres de la classe qui ne doivent pas être persistants.  
  
### <a name="to-prevent-a-member-from-being-serialized"></a>Pour empêcher la sérialisation d’un membre  
  
-   Modifiez la déclaration de l’événement `PropertyChanged` comme suit :  
  
    ```csharp  
    [field: NonSerialized()]  
    public event System.ComponentModel.PropertyChangedEventHandler PropertyChanged;  
    ```  
  
 L’étape suivante consiste à ajouter le code de sérialisation à l’application LoanApp. Pour sérialiser la classe et l’écrire dans un fichier, vous utiliserez les espaces de noms <xref:System.IO> et <xref:System.Xml.Serialization>. Pour éviter de taper les noms qualifiés complets, vous pouvez ajouter des références aux bibliothèques de classes requises.  
  
### <a name="to-add-references-to-namespaces"></a>Pour ajouter des références aux espaces de noms  
  
-   Ajoutez les instructions suivantes au début de la classe `Form1` :  
  
    ```csharp  
    using System.IO;  
    using System.Runtime.Serialization.Formatters.Binary;  
    ```  
  
     Dans ce cas, vous utilisez un formateur binaire pour enregistrer l’objet sous un format binaire.  
  
 L’étape suivante consiste à ajouter le code permettant de désérialiser l’objet à partir du fichier lors de la création de l’objet.  
  
### <a name="to-deserialize-an-object"></a>Pour désérialiser un objet  
  
1.  Ajoutez une constante à la classe pour le nom de fichier des données sérialisées.  
  
    ```csharp  
    const string FileName = @"..\..\SavedLoan.bin";  
    ```  
  
2.  Modifiez le code de la procédure événementielle `Form1_Load` de la façon suivante :  
  
    ```csharp  
    private LoanClass.Loan TestLoan = new LoanClass.Loan(10000.0, 0.075, 36, "Neil Black");  
  
    private void Form1_Load(object sender, EventArgs e)  
    {  
        if (File.Exists(FileName))  
        {  
            Stream TestFileStream = File.OpenRead(FileName);  
            BinaryFormatter deserializer = new BinaryFormatter();  
            TestLoan = (LoanClass.Loan)deserializer.Deserialize(TestFileStream);  
            TestFileStream.Close();  
        }  
  
        TestLoan.PropertyChanged += this.CustomerPropertyChanged;  
  
        textBox1.Text = TestLoan.LoanAmount.ToString();  
        textBox2.Text = TestLoan.InterestRate.ToString();  
        textBox3.Text = TestLoan.Term.ToString();  
        textBox4.Text = TestLoan.Customer;  
    }  
    ```  
  
     Notez que vous devez d’abord vérifier que le fichier existe. S’il existe, créez une classe <xref:System.IO.Stream> pour lire le fichier binaire et une classe <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> pour convertir le fichier. Vous devez également convertir le type de flux en type d’objet Loan.  
  
 Vous devez ensuite ajouter le code permettant d’enregistrer les données saisies dans les zones de texte dans la classe `Loan`, puis sérialiser la classe dans un fichier.  
  
### <a name="to-save-the-data-and-serialize-the-class"></a>Pour enregistrer les données et sérialiser la classe  
  
-   Ajoutez le code suivant à la procédure événementielle `Form1_FormClosing` :  
  
    ```csharp  
    private void Form1_FormClosing(object sender, FormClosingEventArgs e)  
    {  
        TestLoan.LoanAmount = Convert.ToDouble(textBox1.Text);  
        TestLoan.InterestRate = Convert.ToDouble(textBox2.Text);  
        TestLoan.Term = Convert.ToInt32(textBox3.Text);  
        TestLoan.Customer = textBox4.Text;  
  
        Stream TestFileStream = File.Create(FileName);  
        BinaryFormatter serializer = new BinaryFormatter();  
        serializer.Serialize(TestFileStream, TestLoan);  
        TestFileStream.Close();  
    }  
    ```  
  
 À ce stade, vous pouvez de nouveau générer et exécuter l’application. À l’origine, les valeurs par défaut s’affichent dans les zones de texte. Essayez de modifier les valeurs et d’entrer un nom dans la quatrième zone de texte. Fermez l’application et exécutez-la de nouveau. Notez que les nouvelles valeurs s’affichent maintenant dans les zones de texte.  
  
## <a name="see-also"></a>Voir aussi  
 [Sérialisation (C# )](../../../../csharp/programming-guide/concepts/serialization/index.md)  
 [Guide de programmation C#](../../../../csharp/programming-guide/index.md)
