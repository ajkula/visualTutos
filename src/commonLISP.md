# Cours Detaille et Pedagogique de Common Lisp

## 1. Introduction a la Syntaxe de Common Lisp

Common Lisp est un langage unique en son genre, avec une syntaxe qui peut sembler etrange au premier abord, mais qui est en realite tres coherente et puissante. Commencons par explorer les elements de base de cette syntaxe.

### 1.1 Les S-expressions : La Base de Tout

En Common Lisp, tout est construit autour du concept de S-expression (expression symbolique). Une S-expression peut etre :

1. Un atome : un nombre, un symbole, une chaine de caracteres, etc.
2. Une liste : une collection d'atomes ou d'autres listes, entouree de parentheses.

Exemples :

```lisp
; Atomes
42        ; Un nombre
symbole   ; Un symbole
"texte"   ; Une chaine de caracteres

; Listes
(1 2 3)   ; Une liste de nombres
(a b c)   ; Une liste de symboles
(+ 2 3)   ; Une liste qui represente une operation
```

Pourquoi c'est important ? Cette structure uniforme permet a Common Lisp d'etre homoiconique, ce qui signifie que le code et les donnees ont la meme structure. Cela rend le langage extremement flexible et puissant pour la metaprogrammation.

### 1.2 Evaluation des S-expressions

Lorsque Common Lisp rencontre une S-expression, il l'evalue selon ces regles :

1. Les atomes s'evaluent a eux-memes, sauf les symboles qui s'evaluent a leur valeur.
2. Les listes sont interpretees comme des appels de fonction, ou le premier element est la fonction et les elements suivants sont les arguments.

Exemples :

```lisp
42        ; S'evalue a 42
(+ 2 3)   ; S'evalue a 5 (appel de la fonction + avec les arguments 2 et 3)
```

### 1.3 Quotation : Empecher l'Evaluation

Parfois, nous voulons empecher l'evaluation d'une expression. C'est la que la quotation entre en jeu.

```lisp
'(1 2 3)   ; La quote ' empeche l'evaluation, resultat : (1 2 3)
(quote (1 2 3))  ; Equivalent a '(1 2 3)
```

Pourquoi c'est utile ? La quotation nous permet de traiter le code comme des donnees, ce qui est crucial pour la metaprogrammation et la creation de macros.

### 1.4 Fonction Quote et Lambda

En Common Lisp, les fonctions sont des objets de premiere classe. Nous pouvons les passer comme arguments ou les retourner depuis d'autres fonctions.

```lisp
#'+        ; Reference a la fonction +
(function +)  ; Equivalent a #'+

; Creation d'une fonction anonyme (lambda)
(lambda (x) (* x x))  ; Fonction qui carre son argument
```

L'operateur #' (function quote) est utilise pour faire reference a une fonction sans l'appeler. C'est particulierement utile lors du passage de fonctions comme arguments.

### 1.5 Backquote, Unquote et Unquote-splicing

Ces operateurs sont essentiels pour la creation de macros et la manipulation de code.

```lisp
`(1 2 3)     ; Backquote, similaire a quote
`(1 2 ,(+ 1 2))  ; Unquote avec ,
`(1 2 ,@(list 3 4))  ; Unquote-splicing avec ,@
```

- Backquote (`) : Similaire a quote, mais permet l'insertion selective d'expressions evaluees.
- Unquote (,) : A l'interieur d'un backquote, evalue l'expression qui suit.
- Unquote-splicing (,@) : Comme unquote, mais "eclate" le resultat dans la liste environnante.

Ces operateurs sont cruciaux pour la creation de macros, permettant de generer du code de maniere flexible.

## 2. Structures de Controle et Fonctions

### 2.1 Conditionnels

Les structures conditionnelles en Common Lisp sont puissantes et flexibles.

```lisp
(if (> x 0)
    "positif"
    "non positif")

(when (> x 0)
  (print "x est positif")
  (print "on peut faire plusieurs actions"))

(cond ((< x 0) "negatif")
      ((> x 0) "positif")
      (t "zero"))
```

`if` est la structure de base, `when` est utile quand on n'a pas besoin de branche "else", et `cond` permet de gerer plusieurs conditions.

### 2.2 Boucles

Common Lisp offre plusieurs facons de creer des boucles.

```lisp
; Boucle simple
(dotimes (i 5)
  (print i))

; Iteration sur une liste
(dolist (item '(a b c))
  (print item))

; Boucle generale
(loop for i from 1 to 10
      when (evenp i)
      collect i)
```

`dotimes` et `dolist` sont simples et efficaces pour des cas specifiques. `loop` est extremement puissant et flexible, permettant de creer des boucles complexes de maniere declarative.

### 2.3 Definition de Fonctions

Les fonctions sont definies avec `defun`.

```lisp
(defun carre (x)
  "Calcule le carre de x"
  (* x x))

(defun factorielle (n)
  (if (<= n 1)
      1
      (* n (factorielle (- n 1)))))
```

Notez la docstring optionnelle apres les arguments. C'est une bonne pratique pour documenter vos fonctions.

## 3. Manipulation de Donnees

### 3.1 Listes

Les listes sont fondamentales en Lisp. Voici quelques operations courantes :

```lisp
(car '(1 2 3))   ; Premier element : 1
(cdr '(1 2 3))   ; Reste de la liste : (2 3)
(cons 1 '(2 3))  ; Construit une nouvelle liste : (1 2 3)

(mapcar #'1+ '(1 2 3))  ; Applique 1+ a chaque element : (2 3 4)
```

`car` et `cdr` sont historiques mais toujours utilises. `mapcar` est un exemple de fonction d'ordre superieur, prenant une fonction comme argument.

### 3.2 Hash Tables

Les tables de hachage sont utiles pour les associations cle-valeur.

```lisp
(defvar *ht* (make-hash-table))
(setf (gethash 'cle *ht*) 'valeur)
(gethash 'cle *ht*)  ; Recupere la valeur
```

## 4. Exercice : Pseudo DB avec CRUD

Maintenant, implementons une base de donnees simple en memoire. Nous allons expliquer chaque partie en detail.

```lisp
; Definition de notre "base de donnees"
(defvar *db* '())

; Creation d'un enregistrement
(defun create-record (id name age)
  "Cree un nouvel enregistrement et l'ajoute a la base de donnees."
  (push (list :id id :name name :age age) *db*))

; Explication :
; - 'push' ajoute un element au debut d'une liste.
; - Nous creons une liste avec des paires cle-valeur (:cle valeur).
; - Cette structure est appelee "property list" ou plist en Common Lisp.

; Lecture d'un enregistrement
(defun read-record (id)
  "Recherche un enregistrement par son ID."
  (find id *db* :key #'(lambda (record) (getf record :id))))

; Explication :
; - 'find' cherche un element dans une liste.
; - ':key' specifie une fonction pour extraire la valeur a comparer.
; - 'lambda' cree une fonction anonyme qui extrait l'ID de chaque enregistrement.
; - 'getf' recupere la valeur associee a une cle dans une plist.

; Mise a jour d'un enregistrement
(defun update-record (id &key name age)
  "Met a jour un enregistrement existant."
  (let ((record (read-record id)))
    (when record
      (when name (setf (getf record :name) name))
      (when age (setf (getf record :age) age)))))

; Explication :
; - '&key' permet d'avoir des arguments nommes optionnels.
; - 'let' cree des variables locales.
; - 'when' execute le code seulement si la condition est vraie.
; - 'setf' est utilise pour modifier des valeurs.

; Suppression d'un enregistrement
(defun delete-record (id)
  "Supprime un enregistrement de la base de donnees."
  (setf *db* (remove id *db* :key #'(lambda (record) (getf record :id)))))

; Explication :
; - 'remove' cree une nouvelle liste sans les elements qui correspondent au predicat.
; - Nous remplacons *db* par cette nouvelle liste, effectuant ainsi la suppression.

; Exemple d'utilisation
(create-record 1 "Alice" 30)
(create-record 2 "Bob" 25)
(print (read-record 1))
(update-record 1 :age 31)
(delete-record 2)
(print *db*)
```

Cette implementation simple montre comment on peut utiliser les structures de donnees de base de Common Lisp (listes et plists) pour creer un systeme de gestion de donnees rudimentaire. Elle illustre egalement l'utilisation de fonctions d'ordre superieur et la manipulation de listes.

## 5. Exercice : ETL avec CSV

Cet exemple montre comment traiter un grand fichier CSV et effectuer des agregations. Nous allons l'expliquer en detail.

```lisp
; Chargement des bibliotheques necessaires
(ql:quickload '(:cl-csv :alexandria))

(defun process-csv (file-path)
  "Traite un fichier CSV et effectue des agregations."
  (let ((data (make-hash-table :test 'equal))
        (total-rows 0))
    ; 'let' cree des variables locales:
    ; - 'data' est une table de hachage pour stocker nos agregations
    ; - 'total-rows' compte le nombre total de lignes traitees

    (cl-csv:do-csv-rows (row file-path)
      ; 'do-csv-rows' est une macro qui itere sur chaque ligne du CSV
      (incf total-rows)
      ; 'incf' incremente la variable 'total-rows'

      (let ((category (nth 0 row))
            (value (parse-integer (nth 1 row))))
        ; 'nth' recupere un element d'une liste par son index
        ; 'parse-integer' convertit une chaine en entier

        (incf (gethash category data 0) value)))
        ; 'gethash' recupere la valeur associee a 'category' dans 'data'
        ; Le '0' est la valeur par defaut si la cle n'existe pas encore
        ; 'incf' incremente cette valeur de 'value'

    ; Affichage des resultats
    (format t "Total rows processed: ~a~%" total-rows)
    ; '~a' est un marqueur de place pour une valeur dans 'format'
    ; '~%' insere un saut de ligne

    (maphash #'(lambda (k v)
                 (format t "Category: ~a, Total: ~a~%" k v))
             data)))
    ; 'maphash' applique une fonction a chaque paire cle-valeur de la table de hachage
    ; Ici, nous utilisons une fonction lambda pour formater et afficher chaque resultat

; Utilisation
; (process-csv "/path/to/large/csv/file.csv")
```

Cette fonction fait plusieurs choses interessantes :

1. Elle utilise une bibliotheque externe (cl-csv) pour lire efficacement un fichier CSV.
2. Elle utilise une table de hachage pour accumuler des totaux par categorie.
3. Elle demontre l'utilisation de fonctions d'ordre superieur avec `maphash`.
4. Elle montre comment Common Lisp peut traiter de grandes quantites de donnees de maniere efficace.

Pour utiliser cette fonction avec un grand dataset, vous pouvez telecharger un fichier du "New York City TLC Trip Record Data" et ajuster les indices (nth) en fonction de la structure reelle du CSV.

## 6. Reflexions sur les Capacites de Common Lisp

Ces exercices mettent en evidence plusieurs points forts de Common Lisp :

1. Flexibilite : La capacite a manipuler facilement differentes structures de donnees (listes, tables de hachage).
2. Expressivite : Des constructions comme `mapcar`, `maphash`, et les fonctions anonymes permettent d'exprimer des operations complexes de maniere concise.
3. Extensibilite : L'utilisation de bibliotheques externes (comme cl-csv) montre comment Common Lisp peut etre etendu pour des taches specifiques.
4. Performance : Meme s'il n'est pas montre explicitement ici, Common Lisp est connu pour sa capacite a traiter efficacement de grandes quantites de donnees.
5. Interactivite : Tous ces exemples peuvent etre developpes et testes incrementalement dans un REPL, ce qui est un atout majeur pour le developpement et le debogage.

Common Lisp offre un equilibre unique entre la puissance d'expression, la flexibilite et la performance, ce qui en fait un excellent choix pour une variete de taches de programmation, du prototypage rapide au developpement de systemes complexes.