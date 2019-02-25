Pendant les vacances
===

**Profitez des vacances pour vous reposer et faire autre chose avant la suite de votre formation. Penser tout de même à dégager qq heures chaque jour pour continuer dans votre lancée, je vous propose ci dessous une liste non exhaustive de tache quotidienne**

- Recherche stage et alternance :
-> profitez de vos vacances pour contacter un maximum d'entreprises, en candidature spontanée ou pas, puis envoi de CV+LM suivi d'appels tel et entretiens toute la semaine... Ce sera une bonne occasion pour vous entraîner à l'écrit comme à l'oral !
-> je vous invites à vous fixer une deadline s'agissant du stage comme de l'alternance, il faut avoir trouver d'ici fin mars
-> Il y a de nombreux évènements en Mars aussi préparez vous au maximum d'ici là !
-> Vous pouvez parler du STAGE DATING SIMPLON TOULOUSE du 21 mars de 9h30 à 12h ou nous accueillons les entreprises qui viendront vous rencontrer, n'oubliez pas de prendre leurs coordonnées pour les recontacter...

- Finir tous les exercices + envoi sur votre github + envoi de votre lien

- Prévoir une heure par jour sur opquast, nous vous le confirmerons mais à priori, l'examen serait début avril

- Proposition de lecture pour améliorer l'expression orale et écrite, l'orthographe et l'anglais (livre bilingue)

- S'agissant des veilles, j'enverrai dans la semaine, le programme sur discord

- Je vais mettre cette semaine une proposition de correction sur github

- Petit projet bonus qui nécessite de bien comprendre la notion d'interface avant de commencer


	Programme ma petite banque 1.0


On souhaite créer une première version d’une appli qui permet de gérer des comptes bancaires, tel que :
° chaque compte est défini par un code, un solde et une date de création
° un compte courant est un compte avec la particularité d’avoir un découvert
° un compte épargne est un compte avec la particularité d’avoir un taux d’intérêt
° chaque compte appartient à un client 
° chaque client est défini par son code et son nom
° chaque compte peut subir plusieurs opérations
° il existe 2 types d’opérations : versement + retrait
° une opération est définie par un numéro, une date et un montant

1/ Créer le diagramme de classes.

2/ Écrire les classes correspondantes en java et organiser votre programme à l’aide de packages.

3/ Écrire un programme de test en évitant les redondances de données pour permettre d’instancier des clients et des comptes comme ici :

Client c1 = new Client("dupont","dupont@gmail.com");
Client c2 = new Client("durand","durand@gmail.com");	
		
Compte cp1 = new CompteCourant("c1",new Date(), 900 , c1 , 60);  // code compte + date de creation + solde + client + découvert autorisé
Compte cp2 = new CompteEpargne("c2",new Date(), 600 , c2 , 5.5); // code compte + date de creation + solde + client + taux

System.out.println(cp1) ;
System.out.println(cp2) ;	

NB : l’objet Date est fourni  par le package « java.util »


4/ Utiliser l'interface IbanqueMetier (fourni plus bas) que vous devrez implémenter avec les méthodes suivantes :
consulterCompte, verser, retirer, virement et tester comme ce qui suit :

banqueMetier.ajouterCompte(cp1);
banqueMetier.ajouterCompte(cp2);
		
banqueMetier.verser("c1", 90);
banqueMetier.verser(cp1.getCodeCompte(), 60);
banqueMetier.retirer("c1", 50);
		
banqueMetier.verser("c2", 100);
banqueMetier.verser(cp2.getCodeCompte(), 600);
banqueMetier.retirer("c2", 300);
		
banqueMetier.virement("c2", "c1", 100);
		
System.out.println("\nsolde de " + cp1.getClient().getNom()   + " : "   + banqueMetier.consulterCompte("c1").getSolde());
System.out.println("solde de "   + cp2.getClient().getNom()   + " : "   + banqueMetier.consulterCompte("c2").getSolde());


5/ On souhaite à présent afficher l’historique des opérations pour un compte donné. Ajouter la dernière méthode listOperation à notre interface, elle servira à renvoyer l’historique des opérations pour un compte :

System.out.println("----------------Historique des opérations--------------------");
for(Operation op : banqueMetier.listOperation("c1")) 	System.out.println(op);
System.out.println("-----------------------------------------");
for(Operation op : banqueMetier.listOperation("c2"))	System.out.println(op);


6/ A l’aide enfin du mécanisme des Exceptions, lever puis capturer les exceptions provoquées lorsqu’un retrait n’est pas possible « solde insuffisant »

Le résultat final sur la console devra ressembler à :

------bienvenue dans la 1ère version de ma petite banque------

CompteCourant [ CodeCompte=c1 nomClient=Dupont Solde=900.0 Decouvert=60.0 DateCreation=Tue Sep 25 11:44:38 CEST 2018 ] 
CompteEpargne [ CodeCompte=c2 nomClient=Durand Solde=600.0 Taux=5.5 DateCreation=Tue Sep 25 11:44:38 CEST 2018 ] 

solde de Dupont : 1100.0
solde de Durand : 900.0

----------------Historique des opérations--------------------
Dupont
Versement [ Tue Sep 25 10:59:15 CEST 2018, Montant = 90.0, Compte = c1 ]
Versement [ Tue Sep 25 10:59:15 CEST 2018, Montant = 60.0, Compte = c1 ]
Retrait [ Tue Sep 25 10:59:15 CEST 2018, Montant = 50.0, Compte = c1 ]
Versement [ Tue Sep 25 10:59:15 CEST 2018, Montant = 100.0, Compte = c1 ]
-----------------------------------------
Durand
Versement [ Tue Sep 25 10:59:15 CEST 2018, Montant = 100.0, Compte = c2 ]
Versement [ Tue Sep 25 10:59:15 CEST 2018, Montant = 600.0, Compte = c2 ]
Retrait [ Tue Sep 25 10:59:15 CEST 2018, Montant = 300.0, Compte = c2 ]
Retrait [ Tue Sep 25 10:59:15 CEST 2018, Montant = 100.0, Compte = c2 ]


M.Dupont vous ne pouvez pas retirer 2000euros sur votre compte


(*) 
public interface IBanqueMetier {
	public Compte consulterCompte(String codeCpte);
	public void verser(String codeCpte,double montant);
	public void retirer(String codeCpte, double montant);
	public void virement(String codeCpte1,String codeCpte2, double montant);
	public ArrayList<Operation> listOperation(String codeCpte);
}
