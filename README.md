# Travail Pratique 1

# Partie 1 - GéoPiscines2026 (30 points)
Bienvenue chez GéoPiscines! Vous avez été mandaté pour modéliser des piscines originales.


## Objectifs
- Création de classes abstraites et méthodes abstraites
- Héritage et implémentation de classes héritant d'une classe abstraite
- Utilisation de matplotlib

## Instructions
- Le code doit être implémenter dans le fichier ``piscines2026.py``
- Vous devez installer ``matplotlib``
- Vous pouvez utiliser la bibliothèque ``numpy`` 

## Classes à implémenter

### Piscine (5 points)
Implémenter la classe abstraite ``Piscine``
- La classe doit contenir les attributs protégés suivants :
  - nom_modele: str
    - Le nom du modèle de la piscine
  - code: str
    - Le code du modèle de la piscine
  - profondeur: float
    - La profondeur de la piscine

- La classe doit implémenter les getters/setters en utilisant la notation ``@property``
- La classe doit contenir les méthodes abstraites suivantes :
  - volume(self) -> float
    - Retourne le volume de la piscine
  - dessiner(self) -> None
    - Affiche un dessin de la piscine à l'aide d'un graphique matplotlib
    - Un exemple de projection 3D avec des faces colorées est disponibles dans la section extras du dépôt du cours
    - Ne pas ajouter de face sur le dessus de la piscine
    - Les faces des côtés de la piscine devront être en gris
    - Le face du fond de la piscines devra être en bleu

### PiscineRectangulaire (8 points)
Implémenter la classe PiscineRectangulaire dérivant de Piscine
- C'est la piscine classique rectangulaire
- La classe doit contenir les attributs privés suivants :
     - longueur: float
       - La longueur de la piscine
     - largeur: float
       - La largeur de la piscine
- La classe doit implémenter le constructeur
- La classe doit implémenter les getters/setters en utilisant la notation ``@property``
- La classe doit implémenter les méthodes abstraites de Piscine
 
### PiscineCylindrique (8 points)  
Implémenter la classe PiscineCylindrique dérivant de Piscine
- C'est la piscine classique cylindrique
- La classe doit contenir l'attribut privé suivant :
     - rayon: float
       - Le rayon de la piscine
- La classe doit implémenter le constructeur
- La classe doit implémenter les getters/setters en utilisant la notation ``@property``
- La classe doit implémenter les méthodes abstraites de Piscine

### PiscineHexagonale (9 points)
Implémenter la classe PiscineHexagonale dérivant de Piscine
- C'est la piscine classique ayant la forme d'un hexagone régulier
- La classe doit contenir l'attribut privé suivant :
     - longueur_cote: float
       - La longueur d'un côté de la piscine
         - Attention, c'est le côté et non le rayon ou l'apothème
- La classe doit implémenter le constructeur
- La classe doit implémenter les getters/setters en utilisant la notation ``@property``
- La classe doit implémenter les méthodes abstraites de Piscine



# Partie 2 - Gestion d'une liste de lecture (70 points)

## Objectifs
- Utilisation de bibliothèques externes
- Implémentation d'une liste double chaînée

## Instructions
- Le code doit être implémenté dans le fichier ``liste_lecture.py``
- Vous devez installer les packages externes suivant:
  - ``tinytag``
    - permet d'obtenir les méta-informations des fichiers mpo3
  - ``playsound3``
    - permet de jouer un fichier au format mp3

## Classes à implémenter

### Chanson (10 points)
Cette classe représente une chanson de la liste de lecture

- Doit contenir les variables d'instance privées suivantes :
  - ``titre``
    - le titre de la chanson
  - ``artiste``
    - l'artiste de la chanson
  - ``annee``
    - L'année de distribution de la chanson
  - ``chemin_fichier``
    - Le chemin du fichier au format mp3

- Doit implémenter les méthodes suivantes :
  - le constructeur ``__init__(self, titre:str, artiste: str, annee: int, chemin_fichier: str)``
  - la **méthode de classe** ``charger_chanson(cls, chemin_fichier: str)``
    - doit utiliser TinyTag pour obtenir les informations de la chanson
    - doit appeler le constructeur de la classe et retourner l'objet créé
  - la méthode ``__repr__(self)``
    - retourne les informations de la chanson sous forme :
      - ```
        "Titre: {titre} Artiste: {artiste} Année: {année}
        ```


### ListeLecture (50 points)
Cette classe représente une liste de lecture de pour les chansons. C'est une liste double chaînée contenant des objets
de type ``Noeud``

- Doit contenir les variables d'instance privées suivantes :
  - tete
    - référence vers la tête de la liste (sera de type Noeud)
      - ``None`` lorsque la liste est vide
  - queue
    - référence vers la queue de la liste (sera de type Noeud)
    - ``None`` lorsque la liste est vide
  - taille
    - La taille de la liste de lecture
      - i.e. Le nombre de ``Noeud`` dans la liste

- Doit implémenter les méthodes suivantes :
  - Le constructeur
  - les getters/setters (accesseurs) en utilisant la notation ``@property``
  - la **méthode statique** ``charger_chemins_fichiers()``
    - cette méthode retourne la liste des chemins de fichiers de format mp3 sous le répertoire ``musique``
    - voici l'implémentation
      - ```
        return glob.glob("./musique/*.mp3")
        ```
  - la méthode ``charger_liste_lecture(self)``
    - Cette méthode utilise le retour de ``charger_chemins_fichiers()`` pour ajouter les ``Noeud`` contenant
    les ``Chanson`` à la liste de lecture; elle construit la liste double chaînée.
  - La méthode ``menu()`` contenant le menu suivant:
    - ```
              print("Veuillez choisir une option:"
              "[0] Charger la liste de lecture à partir du répertoire 'musique'\n"
              "[1] Afficher la liste de lecture\n"
              "[2] Supprimer une chanson par titre\n"
              "[3] Insérer 'Horizons' à un index\n"
              "[4] Afficher la liste en ordre inverse\n"
              "[5] Joueur une chanson\n"
              "[6] Quitter")
              choix = input("Veuillez entrer une option")
      ```
    - vous devez compléter la logique pour faire les appels des options du menu
  - La méthode ``afficher_liste_lecture(self)``
    - retourne une str de la liste à partir du début sous le format suivant :
      - ```
        1 - {la str retournée par le __repr__() de la première chanson}
        2 - {la str retournée par le __repr__() de la deuxièmne chanson}
        3 - {la str retournée par le __repr__() de la troisième chanson}
        etc..
        ```
  - La méthode ``afficher_liste_inverse(self)``
    - retourne une str de la liste à partir de la fin sous le format suivant :
      - ```
        6 - {la str retournée par le __repr__() de la sixième chanson}
        5 - {la str retournée par le __repr__() de la cinquième chanson}
        4 - {la str retournée par le __repr__() de la quatrième chanson}
        etc..
        ```
  - La méthode ``supprimer_par_titre(self, titre:str)``
    - Lorsque l'option 2 du menu est sélectionnée
      - Demander à l'utilisateur de saisir un titre
      - Faire l'appel à cette méthode en passant le titre en paramètre
        - Si le titre est dans la liste, supprimer ce Noeud de la liste de lecture
        - Sinon, lever une exception de type ValueError avec le message ``titre introuvable``
        - Ne pas oublier d'ajuster vos références vers le suivant et le précédent et la taille de la liste.
  - La méthode ``inserer_horizons(self, index: int)``
    - insère le Noeud contenant la chanson "horizons" à l'index spécifié
      - Le chemin vers le fichier de la chanson est ``./horizons.mp3``
      - ex: si on spécifie 1 comme index, on l'insère entre la première et deuxième chanson de la liste
      - Ne pas oublier d'ajuster vos références vers le suivant et le précédent et la taille de la liste.
  - La méthode ``jouer_chanson(no_liste_lecture: int)``
    - Lorsque l'option 5 du menu est sélectionée
      - Afficher la liste de lecture dans l'ordre
      - Demander à l'utilisateur d'entrer le numéro de la chanson à jouer
      - Faire l'appel à cette méthode en passant le numéro en paramètre
      - faire jouer la chanson en utilisant playsound3 (voir plus bas)
        - L'appel ne doit pas être bloquant

- Si l'option 6 (Quitter) du menu est sélectionnée, on quitte l'application

### Classe Noeud (10 points)
Cette classe représente un Noeud de la liste de lecture 

- Doit contenir les variables d'instance privées suivantes :
  - ``chanson``
    - un objet de type ``Chanson``
  - precedent
    - Référence vers le ``Noeud`` précédent
  - suivant
    - Référence vers le ``Noeud`` suivant

- Doit implémenter les méthodes suivantes :
  - Le constructeur
  - les getters/setters (accesseurs) en utilisant la notation ``@property``


## Utilisation des bibliothèques externes
- TinyTag
  - TinyTag s'utilise de la façon suivante :
    ```
    tag: TinyTag = TinyTag.get(chemin_fichier)
    # On obtient un objet TinyTag que l'on peut utiliser pour aller chercher de l'information
    print(tag.title)
    ```

- playsound3
  - pour jouer une chanson, on doit passer le chemin de fichier (une des propriétés de l'objet Chanson) à la fonction ``playsound()``
  - ex: 
  ```
  playsound(chemin_de_fichier, block=False)
  ```

## Droits d'auteurs
Toutes les musiques incluses sont libres de droits et proviennent de https://freetouse.com/music 

# Correction
- Les barèmes sont entre parenthèses
- Des points seront enlevés pour les erreurs de PEP-008
- Inclure des commentaires explicatifs pour les sections plus complexes.

# Bugs
Si vous trouvez des erreurs dans l'énoncé, merci de les signaler à l'enseignant. La première équipe rapportant une erreur d'énoncé se verra attribuer jusqu'à 5 points bonis.