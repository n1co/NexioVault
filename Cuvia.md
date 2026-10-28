~~ajouter fausse latence dans la file d'attente client premium/pas premium~~

~~gestion archivage dans le mockup en db~~

~~modularite de switch ollama/openai~~

~~remove url import~~

~~loading de doc avant le load preview import doc~~

mise en cache par hash des PDF cv ET ~~formation/plan de cours~~

~~redirection vers match apres upload~~

~~commenter template de competence apres upload~~

~~Plan de formation validé > plan de formation analysé~~

~~verifier la modification du plan de foramtion analysé/validé~~

~~commenter generate report~~
~~commenter bouton noter sur les match~~

~~bouton coeur sur la page match~~

~~desactiver graphique radar~~

~~cacher <20%~~
~~recent activity: qui a import un cv~~
~~cacher les stats de progression~~
~~bouton telecharger le cv original back+front~~

## dashboard
~~cacher export data~~
~~cacher generate report de quicl links & system settings et manage settings~~

## i18n
- ~~Francais~~
- ~~Anglais~~
- ~~Portugais~~
- ~~Espagnol~~
- ~~Italien~~
- ~~Allemand~~
- ~~Portugais brésilien ??~~
- ~~Chinois ??~~
~~Choix par UserAgent + choix dans les parametres de compte~~



bouton télécharger cv sur un formateur, faire un "dropdown"  avec une petite flèche avec:
	Générer depuis modèle: Télécharger CV original
	 Fleche: telecharger original
Virer generer pdf

Liste formateur: 
~~drop down compétence avec recherche et multi select~~
~~mode compact de MUI du tableau~~
~~pouvoir cocher differents formateurs en vue liste (header sticky)~~
	~~- pouvoir en delete plusieurs~~
	- telecharger en pdf, si plusieurs select ca fait un zip avec le fake delay (12/35 sec), et le lien vers le zip dans les notif
~~clic sur le nom -> modale qui présente les infos importantes~~

~~Suite a import de profil, mettre un dialogue pour dire a l'utilisateur d'aller verifier les infos avec une modale (avec un bouton vers le profil)~~
~~cacher le temps du fake timer en notif~~
~~clic sur notif de fin d'import -> vers le profil importé~~
~~liste formateur: mémoriser les ifltres utilisés en localstorage~~
~~ouvrir la fiche dans un autre onglet quand on clic pour voir un profil~~
~~commenter le bouton export CSV sur la liste des formateurs~~

~~sur un profil importé, fais un systeme, est-ce que le profil a été review ou pas avec indicateur "en attente de review" avec la puce "active" si pas active pas exploitable~~
~~ajouter un switch pour afficher uniquement les profils en attente de review sur la liste des formateurs~~
~~prevenir que c'est une ia et que ça fait des erreurs et qu'il faut bien review, par exemple avec une modale quand on arrive sur un profil non review~~

~~vue profil formateur: bontouon pour regen le profil si changements manuels~~
~~empecher acces à la page users si pas admin, y'a que le lien de caché dans le menu~~

~~page settings de compte pouvoir ajouter une photo~~




le mec nous passer les CV, chaque CV est dans un dossier nomme par le trigramme du formateur genre: NNR/xxxxx versions des cv

DB:
trigramme,nom,prenom, list des codes formation annimes, note donnee au formateur 2chifgfre apres la virgule quui est la moyenne generale

table de lien entre l'existant et la future tables IB

table  pour les formation
code formation PK,intitule formation, champ texte avec le plan