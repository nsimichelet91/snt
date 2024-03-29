# L'image numérique

## 1. Vidéo introductive
<iframe width="790" height="444" src="https://www.youtube.com/embed/UnNPNc-F9ks" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## 2. Le pixel

### 2.1 Une image est composée de pixels
Le **pixel** (contraction de «Picture Element») est l'élément de base d'une image numérique.

Une image numérique se présente sous la forme d’un quadrillage - ou d'un tableau - dont chaque case est un pixel d’une couleur donnée. On peut donc repérer chaque pixel par sa ligne et sa colonne dans ce quadrillage, à l'aide de coordonnées en partant du coin en haut à gauche
![image](data/tabpixels.png){: .center }

### 2.2 Comment un écran affiche-t-il des pixels ?

L'observation à la loupe de différents écrans de téléphone donne ceci :
![image](data/apn.png){: .center}

Pour afficher une image sur un écran de téléphone, seules trois couleurs sont donc disponibles : le rouge, le vert et le bleu.
Comment ces 3 couleurs peuvent-elles générer toutes les autres couleurs ?


## 3. Le codage RGB


!!! info "Le codage RGB"
    Chaque pixel correspond à un triplet de trois nombres entiers, soit les valeurs de rouge (Red), de vert (Green) et de bleu (Blue) afin de reconstituer la couleur. Chaque valeur est codée entre 0 et 255. On parle de code RGB (RVB in français).

    ![](data/chromato.jpg){: .center} 
    
    Plus de renseignements sur la méthode additive peuvent être retrouvés [ici](http://physique.ostralo.net/syntheses_couleurs/){. target="_blank"}.

    À noter qu'une couleur dont les 3 composantes sont identiques correspond à un niveau de gris.


[Ce site](https://www.w3schools.com/colors/colors_rgb.asp){. target="_blank"} (parmi beaucoup d'autres !) permet de retrouver le codage RGB d'une couleur. Il permet aussi de trouver le codage html d'une couleur, qui est basé sur le système hexadécimal.


!!! abstract "Activité sur Capytale : modification en Python des couleurs d'une image"
    - [Activité 1 : modification d'une image en Python](../modification_image){. target="_blank"}.


??? info "la base 16 : l'hexadécimal"
    L'inconvénient essentiel du système binaire est la longueur de l'écriture des nombres qu'il génère. Pour cette raison, le **système hexadécimal**, ou système de **base 16** est très souvent employé.

    - Pour écrire en base 2, il faut 2 chiffres différents : le 0 et le 1.  

    - Pour écrire en base 10, il faut 10 chiffres différents: 0,1,2,3,4,5,6,7,8,9.  

    - Pour écrire en base 16, il faut donc 16 chiffres différents : **0,1,2,3,4,5,6,7,8,9,A,B,C,D,E,F**.    


    On a donc la correspondance :

    - A représente 10  
    - B représente 11  
    - C représente 12  
    - D représente 13  
    - E représente 14  
    - F représente 15 

    |256|16|1|
    |:---:|:---:|:---:|
    |$16^2$|$16^1$|$16^0$|
    | 1| D|2|



    $\rm{1D2}_{16}=1 \times 16^2+ 13 \times 16^1+2 \times 16^0=256+208+2=466_{10}$
    
    Le nombre hexadécimal `1D2` correspond donc au nombre décimal 466.
    
    
    En pratique, l'hexadécimal est surtout utilisé pour sa capacité à représenter la valeur de n'importe quel octet sur 2 chiffres ("chiffres" étant à prendre au sens large = chiffres ou lettres !).
 
    !!! example "Exercice"
        === "Énoncé"
            1. Donner la valeur des octets `FF`, `3A`, `B2`.
            2. Expliquer pourquoi la couleur RGB (138,255,51) a pour code html `#8AFF33`.
            3. Quelle est la couleur html du blanc ?



!!! example "Exercice 1"
    === "Énoncé"
        Si je possède une image de 600 pixels sur 400 pixels, quel est le poids (en octets, puis en Ko, puis en Mo) de cette image ? On considèrera que le fichier ne contient que les informations relatives à chaque pixel, et qu'aucun algorithme de compression n'a été utilisé.


!!! example "Exercice 2"
    === "Énoncé"
        Un ami m'envoie une photo de ses vacances. Le fichier de son image (en admettant qu'il ne contienne que le codage des pixels et rien d'autre, ce qui est faux...) commence par ceci :

        ```000011000001000111100110000011010001000111100100000010100000111111101000...```
        
        Est-ce que mon ami a beau temps pour ses vacances ?



!!! abstract "Conclusion :heart: :heart: :heart:"
    - Les écrans (téléphones, ordinateurs, télévisions) sont constitués de pixels eux-mêmes constitués de sous-pixels rouge, vert ou bleus, posés sur une dalle noire.
    - En allumant ces sous-pixels avec différentes intensités, on peut générer toutes les couleurs.
    - Pour pouvoir donner ces instructions d'allumage à différentes intensités, le processeur qui gère ces pixels reçoit pour chacun d'entre eux trois nombres, pour chacun des sous-pixels.
    - Ces nombres sont écrits en binaire et sont codés sur un octet : ces nombres sont donc compris entre 0 et 255.
    - ```(0,0,0)```  est le code RGB du noir, ```(255,255,255)```  est le code RGB du blanc. Il y a plus de 16 millions de combinaisons possibles ($256^3=16777216$). Vous pouvez les tester [ici](https://www.w3schools.com/colors/colors_rgb.asp){. target="_blank"}.



Nous allons maintenant essayer de répondre à la question suivante : comment la lumière extérieure est transformée en une multitude d'informations de rouge, de vert et de bleu ?


## 4. De la lumière aux pixels : le fonctionnement de l'appareil photo numérique

### 4.1 Un peu d'histoire

![image](data/frise_photo.png){: .center }

L'ancêtre de la photographie numérique, appelé *photographie argentique*, fonctionnait grâce à des réactions chimiques successives, permettant de fixer sur du papier la lumière capturée par l’objectif de l’appareil photo.

La photographie numérique consiste à convertir en signaux **numériques** cette lumière capturée par l’objectif.


### 4.2 Le capteur de l'appareil photo numérique

Comme évoqué précédememnt, le principe physique de fonctionnement d’un écran impose qu’il reçoive une information décomposée en niveaux de rouge, de vert et de bleu. Le procédé technique fondamental de la photographie numérique est donc la décomposition de la lumière visible suivant ces trois composantes : c’est le rôle de la **matrice de Bayer**.

![image](data/bayer.png){: .center}

Pour résumer, la matrice de Bayer va convertir la lumière visible en courant électrique (plus ou moins fort) selon la quantité de lumière verte, rouge ou bleue qui aura été reçue dans les photosites: 

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/Rs5ab3X9Oxo?si=2ZKMJxjoyVavMSAr" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/fW9bXLCooAE?si=AN0bp1ey5-ynSB1F" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Les photosites jouent un rôle dans la captation de la lumière,  à l’intérieur du capteur de l’appareil photo numérique, alors que les pixels de l’écran servent à reproduire cette lumière.
Lorsque les fabricants d’appareil photo ou de smartphones communiquent sur le nombre de mégapixels, ils font référence à la définition maximale (en nombre de pixels ) que pourra avoir l’image une fois affichée.
Ce nombre de mégapixels n’est pas égal au nombre de photosites. En effet, des procédés algorithmiques permettent maintenant de deviner de nouveaux pixels (on parle d’interpolation) non captés par les photosites.

## 5. Exemples d'algorithmes de traitement d'image : peut-on encore croire une photo ?

La qualité des photographies prises par les appareils photo numériques ou les smartphones augmente d’année en année.  
Il devient de plus en plus facile de réaliser une photographie qui satisfait nos attentes. Si des progrès ont eu lieu dans le domaine de l’optique, c’est essentiellement aux progrès fulgurants des algorithmes de traitement d’images que l’on doit la satisfaction d’une photographie réussie.  
Les algorithmes présentés ci-dessous peuvent être utilisés en post-traitement de photographie (sur un ordinateur avec un logiciel dédié), par le biais d’un filtre appliqué sur un réseau social, ou même de manière automatique lors de la prise de vue, lorsque ces algorithmes sont implémentés dans l’appareil photo numérique.

### 5.1 Algorithme n°1 : Fusion automatique 

Cet algorithme fusionne plusieurs photographies pour ne garder que des visages souriants.

![image](data/a1.png){: .center}

### 5.2 Algorithme n°2 : Effet Bokeh 

L'effet Bokeh rajoute une modification artificielle de la profondeur de champ. Appelé « mode Portrait » sur iOS
![image](data/a2.jpg){: .center}

### 5.3 Algorithme n°3 : Focus stacking 

Focus stacking : plusieurs photos de profondeurs de champs différentes sont fusionnées pour que le premier plan et l’arrière-plan soient nets en même temps.

![image](data/a3.jpg){: .center}


### 5.4 Algorithme n°4 : Correction de la distorsion

Cet algorithme compense les déformations optiques dues aux lentilles de l'objectif de l'appareil, et redresse artificiellement les photos.

![image](data/a4.png){: .center}

### 5.5 Exercice

1. Lequel de ces algorithmes est utilisé par Google Street View ?
2. Citez et décrivez les algorithmes (filtres) que vous utilisez le plus souvent.
3. Dans quelle mesure peut-on encore considérer qu’une photographie est une preuve ?


!!! abstract "Conclusion :heart: :heart: :heart:"
    - Pour stocker numériquement les informations nécessaires à l'affichage d'une photographie, il faut pour chaque pixel de l'image 3 informations sur la quantité de Rouge, de Vert et de Bleu.
    - Dans un capteur d'appareil photo numérique a lieu une transformation de la lumière en énergie électrique.
    - La lumière est concentrée par des lentilles, puis décomposée en passant dans des filtres rouge, vert et bleu. 
    - La lumière vient alors frapper des photosites (sorte de minuscules panneaux photovoltaïques) qui vont donc produire une quantité d'électricité proportionnelle à la quantité de lumière reçue. 
    - Ce courant électrique est ensuite converti en un nombre binaire sur 1 octet (donc entre 0 et 255), puis stocké dans un fichier.
    - Avant restitution de l'image numérique à l'écran, de multiples algorithmes de correction et d'amélioration de la photographie ont lieu.
    - Ces algorithmes, toujours plus évolués à mesure que la puissance des processeurs augmente, permettent de compenser les faiblesses du matériel optique (objectifs minuscules...), mais aussi les faiblesses du photographe (tremblements...)
    - On peut aussi appliquer ensuite à l'image d'autres transformations (filtres, modification des pixels), qui amènent naturellement à se poser des questions sur la confiance qu'on peut avoir dans une photographie (en matière judiciaire notamment).
