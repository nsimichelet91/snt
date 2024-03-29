# Activité 2 : Incrustation d'une image en Python

_Comment changer l'arrière-plan d'une image ?_


Vous avez déjà vu des extraits vidéos où un acteur tourne devant un fond vert, fond vert qui sera ensuite remplacé par une autre incrusatation vidéo au montage final. 

Nous sommes maintenant capables de faire (à peu près...) la même chose avec quelques lignes de Python.

## 1. Les images de travail

Nous travaillerons avec une image de John Travolta (image [john.bmp](data/john.bmp)).

![](data/john.bmp){: .center}

Nous disposons aussi d'une image de même taille, [lycee.jpg](data/lycee.jpg):

![](data/lycee.jpg){: .center}

L'objectif est bien sûr d'intégrer John Travolta devant le lycée.

Le reste de l'activité se passe sur [Capytale](https://capytale2.ac-paris.fr/web/c/5357-2180284).

<!--
## 2. Fusion des deux images

Nous savons :
- parcourir tous les pixels d'une image (avec une double boucle)
- récupérer la valeur d'un pixel (avec ```getpixel()``` )
- modifier la valeur d'un pixel (avec ```putpixel()``` )
- faire des tests avec ```if```...

Nous avons donc tous les outils nécessaires pour accueillir John Travolta ou Grumpy Cat au lycée : à vos claviers !

**Correction**

```python
from PIL import Image

img_john = Image.open("john.bmp")
img_lycee = Image.open("lycee.jpg")


for x in range(400):
    for y in range(400):
        pixel = img_john.getpixel((x,y))
        if pixel != (0, 255, 0):
            img_lycee.putpixel((x,y), pixel)

img_lycee.show()

```

![](data/sol.png)

-->
