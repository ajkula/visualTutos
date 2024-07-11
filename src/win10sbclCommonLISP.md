# Guide d'Installation et d'Utilisation de Steel Bank Common Lisp (SBCL) sur Windows 10

## 1. Introduction

Ce guide vous aidera a installer et utiliser Steel Bank Common Lisp (SBCL) sur Windows 10. SBCL est une implementation robuste et performante de Common Lisp. Bien que l'environnement Windows differe de celui de Node.js, nous allons voir comment configurer SBCL pour une experience de developpement fluide.

## 2. Installation de SBCL sur Windows 10

### 2.1 Telechargement de SBCL

1. Visitez le site officiel de SBCL : http://www.sbcl.org/platform-table.html
2. Dans la section Windows, telechargez la derniere version stable (par exemple, "sbcl-2.x.x-x86-64-windows-binary.msi")

### 2.2 Installation

1. Double-cliquez sur le fichier .msi telecharge pour lancer l'installateur
2. Suivez les instructions de l'assistant d'installation
3. Choisissez un repertoire d'installation (par defaut : C:\Program Files\Steel Bank Common Lisp)
4. Completez l'installation

### 2.3 Configuration du Chemin (PATH)

Pour pouvoir utiliser SBCL depuis n'importe quel endroit dans l'invite de commande :

1. Ouvrez le menu Demarrer et recherchez "Variables d'environnement"
2. Cliquez sur "Modifier les variables d'environnement systeme"
3. Dans la fenetre qui s'ouvre, cliquez sur "Variables d'environnement"
4. Dans la section "Variables systeme", trouvez la variable "Path" et cliquez sur "Modifier"
5. Cliquez sur "Nouveau" et ajoutez le chemin d'installation de SBCL (par exemple, C:\Program Files\Steel Bank Common Lisp)
6. Cliquez sur "OK" pour fermer toutes les fenetres

### 2.4 Verification de l'Installation

1. Ouvrez une nouvelle invite de commande (cmd)
2. Tapez la commande suivante :

```
sbcl --version
```

Vous devriez voir s'afficher la version de SBCL installee.

## 3. Creation et Execution de Scripts

### 3.1 Creation d'un Script Simple

1. Ouvrez un editeur de texte (par exemple, Notepad++)
2. Creez un nouveau fichier nomme `hello-world.lisp`
3. Ajoutez le code suivant :

```lisp
(defun main ()
  (format t "Hello, World from Windows 10!~%"))

(main)
```

4. Sauvegardez le fichier

### 3.2 Execution du Script

Pour executer le script, ouvrez une invite de commande dans le repertoire contenant votre fichier et tapez :

```
sbcl --script hello-world.lisp
```

Cette commande est l'equivalent de `node hello-world.js` dans l'environnement Node.js.

### 3.3 Creation d'un Script Executable sur Windows

Contrairement a Unix, Windows n'a pas de support natif pour les shebangs. Cependant, nous pouvons creer un fichier batch (.bat) pour executer notre script Lisp :

1. Creez un fichier `hello-world.bat` dans le meme repertoire que votre script Lisp
2. Ajoutez le contenu suivant :

```batch
@echo off
sbcl --script hello-world.lisp %*
```

3. Sauvegardez le fichier

Maintenant, vous pouvez executer votre script Lisp en double-cliquant sur le fichier .bat ou en tapant `hello-world` dans l'invite de commande (si vous etes dans le bon repertoire).

### 3.4 Utilisation d'Arguments en Ligne de Commande

Modifiez votre script Lisp pour utiliser des arguments :

```lisp
(defun main ()
  (format t "Arguments: ~{~A~^, ~}~%" (cdr sb-ext:*posix-argv*)))

(main)
```

Vous pouvez maintenant passer des arguments a votre script via le fichier .bat :

```
hello-world arg1 arg2 arg3
```

## 4. Gestion des Dependances avec Quicklisp

### 4.1 Installation de Quicklisp

1. Telechargez Quicklisp :
   - Ouvrez votre navigateur et allez sur https://beta.quicklisp.org/quicklisp.lisp
   - Sauvegardez la page sous forme de fichier "quicklisp.lisp" dans un repertoire de votre choix

2. Ouvrez une invite de commande dans ce repertoire et lancez SBCL :

```
sbcl --load quicklisp.lisp
```

3. Dans le REPL SBCL, executez :

```lisp
(quicklisp-quickstart:install)
(ql:add-to-init-file)
(quit)
```

### 4.2 Utilisation de Quicklisp dans un Script

Pour utiliser une bibliotheque dans votre script, ajoutez ceci au debut de votre fichier .lisp :

```lisp
(load "C:/Users/VotreNomUtilisateur/quicklisp/setup.lisp")
(ql:quickload :nom-de-la-bibliotheque)

;; Reste de votre code
```

Remplacez "VotreNomUtilisateur" par votre nom d'utilisateur Windows.

## 5. Developpement Interactif avec le REPL

Le REPL (Read-Eval-Print Loop) est un outil puissant pour le developpement interactif en Common Lisp.

Pour lancer le REPL de SBCL :

1. Ouvrez une invite de commande
2. Tapez `sbcl`

Vous etes maintenant dans le REPL ou vous pouvez taper du code Lisp et voir les resultats immediatement.

Pour charger un fichier dans le REPL :

```lisp
(load "C:/chemin/vers/votre/fichier.lisp")
```

## 6. Environnement de Developpement Integre (IDE)

Pour une experience de developpement plus riche sur Windows, considerez l'utilisation d'un IDE :

1. Emacs avec Slime : 
   - Telechargez Emacs pour Windows
   - Installez Slime via Quicklisp
   - Configurez Emacs pour utiliser Slime avec SBCL

2. VSCode avec l'extension "Common Lisp":
   - Installez Visual Studio Code
   - Ajoutez l'extension "Common Lisp" depuis le marketplace
   - Configurez l'extension pour utiliser SBCL

Ces environnements offrent des fonctionnalites avancees comme la completion de code, la navigation dans le code, et l'integration du REPL.

## 7. Bonnes Pratiques pour le Developpement sous Windows

1. Utilisez des chemins absolus ou assurez-vous d'etre dans le bon repertoire lors de l'execution de scripts
2. Preferez l'utilisation de '/' plutot que '\' dans les chemins de fichiers, meme sous Windows
3. Utilisez des outils comme ASDF pour gerer la structure de vos projets
4. Familiarisez-vous avec l'invite de commande Windows ou considerez l'utilisation de PowerShell pour une experience plus riche

## Conclusion

Bien que l'environnement de developpement Common Lisp sur Windows differe de celui de Node.js, SBCL offre une plateforme puissante et flexible. Avec les bons outils et configurations, vous pouvez creer un environnement de developpement Common Lisp productif et efficace sous Windows 10.