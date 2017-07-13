# Titre
__Sous-titre__



## Enchaînements


* Avec 2 lignes d'espacement, les diapo défilent __vers le bas__


* Avec 3 lignes d'espacement, les diapo défilent __vers la droite__



## Formatage


### Styles

\_\_gras\_\_ : __gras__  
\_emphase\_ : _emphase_  
\`code\` : `code`


### Code

```javascript
function toggle(elemID){
    var elem = document.getElementById(elemID);   
    if (elem.style.display === 'block') {
        elem.style.display = 'none';  
    }
    else {
        elem.style.display = 'block';
    }
}
```


### Puces

* rouge
* vert
* bleu
    * bleu marine
    * bleu ciel
* noir



## Images


* On peut préciser la _taille des images_ avec  
`<!-- .element: height="200px" -->`

![Logo SII](images/logo-sii.png)  <!-- .element: height="200px" -->
![Logo SII](images/logo-sii.png)  <!-- .element: height="100px" -->



## Liens

\[Nom de la ressource\](Url de la ressource)

\[GitHub SII\](https://github.com/groupe-sii)



## Tableaux


Taille normale

| Colonne 1 | Colonne 2 | Colonne 3 |
| -         | -         | -         |
| A1        | B1        | C1        |
| A2        | B2        | C2        |


Taille moyenne

`<!-- .slide: data-state="medium-table" -->`

<!-- .slide: data-state="medium-table" -->
| Colonne 1 | Colonne 2 | Colonne 3 |
| -         | -         | -         |
| A1        | B1        | C1        |
| A2        | B2        | C2        |


Petite taille

`<!-- .slide: data-state="small-table" -->`

<!-- .slide: data-state="small-table" -->
| Colonne 1 | Colonne 2 | Colonne 3 |
| -         | -         | -         |
| A1        | B1        | C1        |
| A2        | B2        | C2        |
