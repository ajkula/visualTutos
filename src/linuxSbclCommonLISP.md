# Guide d'Installation et d'Utilisation de Steel Bank Common Lisp (SBCL)

## 1. Introduction

Steel Bank Common Lisp (SBCL) est une implementation haute performance de Common Lisp. Contrairement a Node.js qui est specifique a JavaScript, SBCL est un environnement complet pour executer du code Common Lisp. Ce guide vous montrera comment installer SBCL, creer des scripts, et les executer de maniere similaire a ce que vous feriez avec Node.js.

## 2. Installation de SBCL

L'installation de SBCL varie selon votre systeme d'exploitation. Voici les etapes pour les systemes les plus courants :

### 2.1 Sur Windows

1. Allez sur le site officiel de SBCL : http://www.sbcl.org/platform-table.html
2. Telechargez la derniere version pour Windows.
3. Executez l'installateur et suivez les instructions.
4. Ajoutez le chemin d'installation de SBCL a votre variable d'environnement PATH.

### 2.2 Sur macOS

Si vous utilisez Homebrew :

```bash
brew install sbcl
```

Sinon, telechargez le package depuis le site officiel et installez-le manuellement.

### 2.3 Sur Linux (Ubuntu/Debian)

```bash
sudo apt-get update
sudo apt-get install sbcl
```

Pour d'autres distributions Linux, utilisez le gestionnaire de paquets approprie.

### 2.4 Verification de l'installation

Ouvrez un terminal et tapez :

```bash
sbcl --version
```

Vous devriez voir la version de SBCL s'afficher.

## 3. Creation et Execution de Scripts

Contrairement a Node.js ou vous creez simplement un fichier .js et l'executez, SBCL necessite quelques etapes supplementaires pour creer des scripts executables. Voici comment proceder :

### 3.1 Creation d'un Script Simple

Creez un fichier nomme `hello-world.lisp` avec le contenu suivant :

```lisp
(defun main ()
  (format t "Hello, World!~%"))

(main)
```

### 3.2 Execution Directe du Script

Vous pouvez executer ce script directement avec SBCL comme ceci :

```bash
sbcl --script hello-world.lisp
```

Cela est similaire a `node hello-world.js` en Node.js.

### 3.3 Creation d'un Script Executable

Pour creer un script executable plus proche de l'experience Node.js, vous pouvez utiliser un "shebang" et rendre le fichier executable. Voici comment :

1. Modifiez `hello-world.lisp` comme suit :

```lisp
#!/usr/bin/env sbcl --script

(defun main ()
  (format t "Hello, World!~%"))

(main)
```

2. Rendez le fichier executable (sur Unix/Linux/macOS) :

```bash
chmod +x hello-world.lisp
```

3. Vous pouvez maintenant executer le script directement :

```bash
./hello-world.lisp
```

C'est similaire a l'execution d'un script Node.js avec le shebang `#!/usr/bin/env node`.

### 3.4 Utilisation d'Arguments en Ligne de Commande

Pour traiter des arguments en ligne de commande (comme `process.argv` en Node.js), utilisez `*posix-argv*` :

```lisp
#!/usr/bin/env sbcl --script

(defun main ()
  (format t "Arguments: ~{~A~^, ~}~%" (cdr sb-ext:*posix-argv*)))

(main)
```

Executez-le comme ceci :

```bash
./hello-world.lisp arg1 arg2 arg3
```

## 4. Gestion des Dependances

En Node.js, vous utilisez npm pour gerer les dependances. En Common Lisp, l'equivalent le plus proche est Quicklisp. Voici comment l'installer et l'utiliser :

### 4.1 Installation de Quicklisp

1. Telechargez Quicklisp :

```bash
curl -O https://beta.quicklisp.org/quicklisp.lisp
```

2. Chargez-le dans SBCL :

```bash
sbcl --load quicklisp.lisp
```

3. Dans le REPL SBCL, executez :

```lisp
(quicklisp-quickstart:install)
(ql:add-to-init-file)
(quit)
```

### 4.2 Utilisation de Quicklisp dans un Script

Pour utiliser une bibliotheque dans votre script, ajoutez ceci au debut :

```lisp
#!/usr/bin/env sbcl --script

(load "~/quicklisp/setup.lisp")
(ql:quickload :nom-de-la-bibliotheque)

;; Reste de votre code
```

C'est similaire a `require()` en Node.js.

## 5. Developpement Interactif

Une des forces de Common Lisp est son environnement de developpement interactif (REPL). Contrairement a Node.js ou vous devez generalement redemarrer l'application pour tester des changements, en Common Lisp, vous pouvez charger et tester du code en temps reel.

Pour entrer dans le REPL de SBCL :

```bash
sbcl
```

Vous pouvez alors taper du code Lisp directement et voir les resultats immediatement.

## 6. Bonnes Pratiques

1. Utilisez des systemes de construction comme ASDF (Another System Definition Facility) pour organiser des projets plus grands.
2. Exploitez le REPL pour le developpement interactif et le debogage.
3. Utilisez des outils comme Slime ou Sly avec Emacs pour une experience de developpement plus riche.
4. Documentez vos fonctions avec des docstrings.

## Conclusion

Bien que l'approche soit differente de Node.js, SBCL offre un environnement puissant et flexible pour le developpement en Common Lisp. La combinaison de scripts executables, du REPL interactif, et d'un systeme de gestion de packages comme Quicklisp permet un flux de travail efficace et productif.