# Cours Avance de Common Lisp

## 1. Syntaxe Detaillee

### 1.1 Elements syntaxiques de base

- `;` : Commentaire sur une ligne
- `#|` et `|#` : Commentaires multi-lignes
- `'` : Quote (citation) - empeche l'evaluation
- ``` ` ``` : Backquote - permet la quasi-citation
- `,` : Unquote - evalue l'expression dans une quasi-citation
- `,@` : Unquote-splicing - evalue et insere le contenu d'une liste
- `#'` : Function quote - reference a une fonction
- `()` : Liste vide ou nil
- `*variable*` : Convention de nommage pour les variables speciales (globales)

### 1.2 Exemples detailles

```lisp
; Quote
'(1 2 3)  ; Resultat : (1 2 3)
(quote (1 2 3))  ; Equivalent a '(1 2 3)

; Backquote et Unquote
(let ((x 10))
  `(1 2 ,x))  ; Resultat : (1 2 10)

; Unquote-splicing
(let ((lst '(2 3)))
  `(1 ,@lst 4))  ; Resultat : (1 2 3 4)

; Function quote
(mapcar #'1+ '(1 2 3))  ; Resultat : (2 3 4)

; Variables speciales
(defvar *db* '())  ; Definit une variable globale *db*
```

## 2. Fonctions Utilitaires

### 2.1 Affichage et Debug

```lisp
; Affichage simple
(print "Hello, World!")

; Affichage formate
(format t "La valeur est ~a~%" 42)

; Debug avec trace
(trace fonction-a-debugger)
(untrace fonction-a-debugger)

; Macro pour le logging
(defmacro log-debug (format-string &rest args)
  `(when *debug-mode*
     (format *error-output* ,format-string ,@args)))

(defvar *debug-mode* t)
(log-debug "Valeur de x: ~a~%" x)
```

## 3. Exercice : Pseudo DB avec CRUD

Implementons une simple base de donnees en memoire avec des operations CRUD.

```lisp
(defvar *db* '())

(defun create-record (id name age)
  (push (list :id id :name name :age age) *db*))

(defun read-record (id)
  (find id *db* :key #'(lambda (record) (getf record :id))))

(defun update-record (id &key name age)
  (let ((record (read-record id)))
    (when record
      (when name (setf (getf record :name) name))
      (when age (setf (getf record :age) age)))))

(defun delete-record (id)
  (setf *db* (remove id *db* :key #'(lambda (record) (getf record :id)))))

; Exemple d'utilisation
(create-record 1 "Alice" 30)
(create-record 2 "Bob" 25)
(print (read-record 1))
(update-record 1 :age 31)
(delete-record 2)
(print *db*)
```

## 4. Exercice : ETL avec CSV

Cet exemple montre comment traiter un grand fichier CSV et effectuer des agregations.

```lisp
(ql:quickload '(:cl-csv :alexandria))

(defun process-csv (file-path)
  (let ((data (make-hash-table :test 'equal))
        (total-rows 0))
    (cl-csv:do-csv-rows (row file-path)
      (incf total-rows)
      (let ((category (nth 0 row))
            (value (parse-integer (nth 1 row))))
        (incf (gethash category data 0) value)))
    (format t "Total rows processed: ~a~%" total-rows)
    (maphash #'(lambda (k v)
                 (format t "Category: ~a, Total: ~a~%" k v))
             data)))

; Utilisation
; (process-csv "/path/to/large/csv/file.csv")
```

Pour tester avec un grand dataset, vous pouvez utiliser le "New York City TLC Trip Record Data" disponible sur :
https://www1.nyc.gov/site/tlc/about/tlc-trip-record-data.page

Notez que vous devrez ajuster les indices (nth) en fonction de la structure reelle du CSV.

## 5. Capacites de Common Lisp mises en evidence

- Manipulation flexible des donnees avec les listes et les hash-tables
- Macros puissantes pour l'extension du langage
- Traitement efficace de grandes quantites de donnees
- Programmation fonctionnelle avec mapcar, reduce, etc.
- REPL interactif pour le developpement rapide

Ce cours couvre les elements syntaxiques de base, fournit des exemples pratiques de manipulation de donnees, et demontre la capacite de Common Lisp a traiter efficacement de grands volumes de donnees.