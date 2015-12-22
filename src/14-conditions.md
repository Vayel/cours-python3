# Branchements conditionnels

> -- Quarante-deux ! cria Loonquawl. Et c'est tout ce que t'as à nous montrer au
> bout de sept millions et demi d'années de boulot ?
>
> -- J'ai vérifié très soigneusement, dit l'ordinateur, et c'est
> incontestablement la réponse exacte. Je crois que le problème, pour être tout
> à fait franc avec vous, est que vous n'avez jamais vraiment bien saisi la
> question.

> *Douglas Adams -- Le Guide du Voyageur Galactique*

Vous ne vous en doutez sûrement pas, mais dans la totalité des programmes qu'il
exécute, l'ordinateur passe son temps à **se poser des questions**. Oh, bien
sûr, il ne se demande pas ce qu'il va manger ce soir ni quel est le sens de sa
vie, mais il se pose des questions d'ordinateur, qui lui permettent de décider
*ce qu'il va faire ensuite*.

Par exemple, imaginons un programme qui demande à l'utilisateur d'entrer un mot
de passe. À un moment donné de ce programme, l'ordinateur va devoir décider si
le mot de passe entré par l'utilisateur est le bon, et il exécutera une action
différente suivant que ce soit le cas ou non. Ce genre de carrefour dans
l'exécution d'un programme s'appelle un **branchement conditionnel**, et c'est
ce que nous allons étudier tout au long de ce chapitre.

Dans ce chapitre, nous allons apprendre :

* ce qu'est une valeur **booléenne**,
* la notion de **prédicat**,
* à effectuer différentes actions dans différentes conditions.

## Notre programme d'exemple

Voici un programme qui illustre ce que nous allons apprendre dans ce chapitre :

```python
saisie = input("Saisissez votre mot de passe : ")

if saisie == 'abracadabra':
    print("Accès autorisé")
else:
    print("Accès refusé")
```

Nous allons découvrir dans la suite comment celui-ci fonctionne en détail.
Contentons nous de jouer avec dans un premier temps.

### Écrire un programme dans un fichier

À partir de ce chapitre, nous allons travailler sur des programmes d'exemple.
Il existe bien des façons d'exécuter un programme en Python suivant votre
système d'exploitation. Pour ne pas surcharger le propos, je me contenterai de
vous montrer ici la méthode qui marchera chez tout le monde.

Ouvrez le programme IDLE livré avec Python. Vous devriez voir apparaître une
fenêtre dans le style de la figure 1.

![La console IDLE](src/img/idle.png)

Puis cliquez sur `File -> New File` ou bien appuyez simultanément sur les
touches `<Ctrl>` et `<N>`.


Ceci devrait faire apparaître une fenêtre vide dans laquelle vous pouvez écrire
un programme en Python. Recopiez dedans notre programme d'exemple, comme sur
la figure 2.

![Notre programme d'exemple](src/img/programme_motdepasse.png)

Enfin, exécutez ce programme en appuyant sur la touche `<F5>`. IDLE va vous
demander si vous souhaîtez sauvegarder ce fichier au passage, enregistrez-le en
lui donnant l'extension `.py`, par exemple sous le nom `motdepasse.py`. Une
fois ceci fait, le programme se lance dans la console interactive, comme sur la
figure 3.

![Exécution](src/img/execution.png)

Essayez d'exécuter plusieurs fois ce programme avec des mots de passe
différents, puis essayez avec le bon : abracadabra. Comme vous pouvez le
constater, le programme n'affiche "Accès autorisé" que si vous lui entrez le
bon mot de passe.

### Jouons !

Avant même de chercher à comprendre comment ce script marche, essayez de le
modifier pour changer son comportement. Par exemple:

* Faites en sorte que le mot de passe correct soit autre chose que « abracadabra ».

* Traitez l'utilisateur d'idiot lorsqu'il entre le mauvais mot de passe.

C'est une bonne habitude à prendre lorsque vous êtes confronté à un code de ce
cours : réussir à bidouiller un programme pour lui faire faire ce que l'on
veut, c'est beaucoup plus efficace qu'un long discours théorique !

## Vrai ou faux ?

### Les booléens

Je vous ai dit plus haut que même si l'ordinateur se pose des questions à
longueur de temps, il ne peut pas se poser n'importe lesquelles. En fait, les
questions qu'il se pose sont des questions *logiques*, c'est-à-dire qu'elles
n'acceptent que deux réponses possibles : oui ou non.

Par exemple, nous pouvons demander à Python si 2 est inférieur à 38.

Pour cela, nous allons formuler notre question d'une façon qui va peut-être
vous sembler bizarre : nous allons *affirmer* que 2 est inférieur à 38,
et Python nous répondra si c'est vrai ou faux.

```python
>>> 2 < 38
True
```

À l'inverse, si on lui dit que 7 est inférieur à 4, Python nous répondra que
c'est faux :

```python
>>> 7 < 4
False
```

En programmation, une expression qui peut être vraie (`True`) ou fausse
(`False`) s'appelle **un prédicat**, et les deux valeurs de vérité possibles
d'un prédicat sont un type d'objet à part entière, c'est le type **booléen**.
Python appelle ces valeurs des `bool` :

```python
>>> type(True)
<class 'bool'>
>>> type(False)
<class 'bool'>
```

### Opérateurs de comparaison

La plupart des prédicats que nous allons écrire au départ utiliseront des
opérateurs un peu spéciaux que nous appelons *opérateurs de comparaison*.

Ces opérateurs sont relativement simples à comprendre, ils fonctionnent comme
en maths :

--------------------------------------------------------
    Opérateur     Signification
----------------- --------------------------------------
     `x < y`      `x` est strictement inférieur à `y`

    `x <= y`      `x` est inférieur ou égal à `y`

    `x == y`      `x` est égal à `y`

    `x != y`      `x` est différent de `y`

    `x >= y`      `x` est supérieur ou égal à `y`

     `x > y`      `x` est strictement supérieur à `y`
---------------------------------------------------------

Table: Opérateurs de comparaison usuels

> **Remarquez que l'opérateur d'égalité se note `==`, contrairement à
> l'opérateur d'affectation (`=`) que nous utilisons depuis le début de ce
> cours.**

Ces opérateurs s'appliquent sur tous les types de données de base que nous
avons vus jusqu'à présent. Si, pour les nombres leur signification est
évidente, il y a de quoi être perplexe sur leur utilisation avec des chaînes de
caractères :

```python
>>> 'bacon' > 'oeufs'
False
>>> 'bacon' != 'oeufs'
True
>>> 'bacon' <= 'oeufs'
True
>>> 'spam' == 'spam'
True
```

En fait, il existe une manière d'ordonner les chaînes de caractères (on parle 
de relation d'ordre sur les chaînes de caractères), que l'on appelle 
pompeusement l'**ordre lexicographique**. Dans les faits, il s'agit plus ou 
moins de l'ordre alphabétique, à ceci près que l'on différencie les lettres 
majuscules et minuscules.

Ne nous attardons pas sur l'ordre lexicographique pour le moment. Vous
pouvez faire des tests dans la console pour comprendre comment celui-ci
fonctionne, mais en réalité, il y a peu de chances que vous ayez besoin de
comparer les chaînes de caractères autrement qu'avec `==` et `!=` avant un bon
moment. Nous reviendrons sur ce sujet lorsque nous étudierons la façon dont les
chaînes sont encodées par Python.

### Encadrements

Une particularité des opérateurs de comparaison, à laquelle on pense trop
rarement, est que ceux-ci peuvent être chaînés pour exprimer des
*encadrements*. Par exemple, on peut vérifier qu'un nombre est strictement
compris entre 0 et 10 :

```python
>>> n = 4
>>> 0 < n < 10
True
```

Ou bien qu'il est strictement positif mais inférieur ou égal à 10:

```python
>>> n = 10
>>> 0 < n <= 10
True
```

On peut même laisser libre cours à notre fantaisie, en écrivant des tests un
peu plus alambiqués :

```python
>>> a, b = 5, 3
>>> 0 < a < b < 10
False
>>> a, b = 3, 5
>>> 0 < a < b < 10
True
```

Gardez bien ces encadrements en tête : ils sont particulièrement efficaces pour
exprimer de façon très lisible des conditions parfois complexes.

## Exprimer une condition

Même si nous n'en avons pas encore fini avec les prédicats, ce que nous venons
de voir est largement suffisant pour comprendre notre programme d'exemple,
puisque celui-ci compare une entrée saisie par l'utilisateur au mot de passe
`"abracadabra"` :

```python
>>> saisie = "Sésame ouvre toi !"
>>> saisie == "abracadabra"
False
>>> saisie = "abracadabra"
>>> saisie == "abracadabra"
True
```

### Avec des "*si*"...

Il ne nous reste plus qu'à comprendre comment Python se débrouille pour
exécuter des actions différentes selon que le mot de passe entré est le bon ou
non. En fait, cela s'exprime de façon assez naturelle :

* **Si** la saisie est égale à `"abracadabra"` : j'affiche `"Accès autorisé"`.
* **Sinon** : j'affiche `"Accès refusé"`.

Les deux mots que j'ai mis en gras, (« *si* » et « *sinon* »), se traduisent en
anglais, respectivement, par « *if* » et « *else* ». Concentrons-nous sur la
première phrase :

```python
if saisie == 'abracadabra':     # Si la saisie est égale à 'abracadabra'
    print('Accès autorisé')     # J'affiche 'Accès autorisé'
```

Notez que tout ce qui se trouve derrière le symbole `#` désigne des *commentaires*.
Python ne tient pas compte de ce qui est écrit après ce symbole, donc il s'agit d'un
moyen très pratique d'expliquer ce que l'on est en train de faire.

La première ligne désigne une *condition*, introduite par la syntaxe `if
[predicat]:` (n'oubliez pas le `:`), elle sert à introduire un *bloc*
d'instructions qui seront exécutées uniquement si le prédicat est vérifié.

Ainsi :

```python
if True:
    print("Ce texte sera tout le temps affiché")

if False:
    print("Ce texte ne sera jamais affiché")
```

Notez que les instructions à l'intérieur de ce bloc sont *indentées*,
c'est-à-dire décalées de quatre espaces par rapport à la ligne du dessus. Cette
indentation est **obligatoire** en Python. C'est de cette façon qu'il
différencie les instructions à exécuter tout le temps, de celles qui
appartiennent au bloc conditionnel :

```python
if predicat:
    print('Ce texte ne sera affiché que si le prédicat est vrai')

print('Ce texte sera toujours affiché')
```


### Remarques à propos de l'indentation dans la console interactive

Essayons d'écrire la ligne `if` dans la console Python:

```python
>>> age = 25
>>> if age >= 18:
...     print('Vous êtes majeur.')
...
Vous êtes majeur
>>>
```

Remarquez que l'interpréteur nous montre ces fameux trois points pour nous
indiquer qu'il a besoin de plus de lignes avant d'évaluer notre code. Si on
omet d'indenter la seconde ligne, l'interpréteur nous crache au visage :

```python
>>> if age >= 18:
... print("Vous êtes majeur")
  File "<stdin>", line 2
    print("Vous êtes majeur")
        ^
IndentationError: expected an indented block
```

La ligne la plus importante est la dernière, qui signifie, littéralement :
« *Erreur d'indentation : j'attendais un bloc indenté* ». C'est plutôt sympa de
sa part, remarquez : Python nous explique exactement ce qui le gêne au lieu de
se contenter de râler.

## Aller plus loin

### Opérateurs logiques

Le nom du type `bool`, aussi cool soit-il, n'est pas dû au hasard. Il vient du
nom du célèbre mathématicien George Boole, à qui nous devons la logique moderne.
Pour la petite histoire, Boole a créé l'algèbre qui décrit les relations entre
plusieurs propositions logiques.

En ce qui nous concerne, en Python, cette algèbre va se traduire par les
opérateurs que l'on peut appliquer aux booléens, et qui permettent de créer des
expressions logiques complexes.

#### Le ET logique : `and`

Jusqu'à présent, nos conditions ne comportaient qu'un seul prédicat.
Heureusement, Python permet d'en combiner plusieurs, et notamment de s'assurer
que tous sont vérifiés, avec le mot-clé `and`. Son emploi est très naturel :
`if [predicat1] and [predicat2]:`. Par exemple :

```python
if nom == 'Merlin' and passe == 'abracadabra':     # Si le nom est 'Merlin' et le mot de passe 'abracadabra'
    print('Bienvenue à vous, noble magicien')
```

Python dispose de règles de priorité pour interpréter la condition. En
l'occurrence, l'opérateur d'égalité est prioritaire sur le `and`, tout comme
les autres opérateurs de compraison vus plus haut. On n'aurait effectivement
pas idée de lire la ligne précédente comme ça :

```python
if nom == ('Merlin' and passe) == 'abracadabra':     # Si le nom est 'Merlin' et le mot de passe 'abracadabra'
```

`and` est un opérateur dit *binaire*, puisqu'il s'applique à deux objets, en
l'occurrence à deux prédicats. Pour bien comprendre le fonctionnement de `and`,
examinons tous les cas possibles pour les valeurs des prédicats :

```python
>>> False and False
False
>>> False and True
False
>>> True and False
False
>>> True and True
True
```

Autrement dit, la **conjonction** de deux prédicats est vraie si et seulement
si les deux prédicats le sont. Cela peut se généraliser à $n$ prédicats :

```python
>>> True and False and True
False
>>> (True and False) and True
False
>>> True and (False and True)
False
```

On remarque que les parenthèses n'ont pas d'importance : quel que soit l'ordre
d'évaluation des prédicats, le résultat est le même. On dit que l'opérateur
`and` est **associatif**.

Par contre, cet opérateur n'est pas **commutatif** : `predicat1 and
predicat2` et `predicat2 and predicat1` n'ont pas les mêmes effets.
Effectivement, Python est paresseux, puisqu'il ne regarde pas la valeur du
second prédicat s'il n'en a pas besoin : à partir du moment où le premier est
faux, la conjonction le sera, donc inutile de perdre son temps à regarder ce
que vaut le deuxième prédicat.

#### Le OU logique : `or`

Le ET logique n'est pas la seule façon de combiner deux prédicats, et il est
aussi possible de se demander si au moins un est vrai. C'est ce que permet
l'opérateur `or` :

```python
>>> False or False
False
>>> False or True
True
>>> True or False
True
>>> True or True
True
```

Il s'utilise aussi simplement que `and` pour former une condition : `if
[predicat1] or [predicat2]:`. Voyez plutôt :

```python
if panneau == 'stop' or feu == 'rouge':
    print("S'arrêter")
```

On parle cette fois-ci de **disjonction** de deux prédicats. On constate
qu'elle n'est fausse que lorsque les deux prédicats le sont. `or` est associatif
mais pas commutatif : là encore, Python en fait le moins possible. Dès que le
premier prédicat est vrai, la disjonction le sera et on peut s'épargner de
calculer la valeur du second.

On retrouve aussi la règle de priorité entre `or` et les opérateurs de
comparaison. De plus, le `and` est prioritaire sur le `or`, on peut même le
distribuer : `A and (B or C)` a la même valeur logique que `A and B or A and C`
. D'ailleurs, on fait souvent l'analogie suivante :

Opérateur logique | Opérateur mathématique
------------------|-----------------------
`or` | $+$
`and` | $\times$

#### La négation : `not`

Python fournit également un opérateur unaire `not` pour obtenir la valeur
logique opposée à celle d'un prédicat : `if not predicat:`. Sans surprise, on
a :

```python
>>> not False
True
>>> not True
False
```

`not` est prioritaire sur `and` et `or` mais pas sur les opérateurs de
comparaison :

```python
>>> not True or True
True
>>> not (True or True)
False
>>> 3 > 5 or 3 < 4
True
```

Par contre, `not` n'est pas distributif par rapport à `and` ou `or` du fait des
[lois de De Morgan](https://fr.wikipedia.org/wiki/Lois_de_De_Morgan).

### Valeur logique des autres types de données
