# TallerGit
En el paso 0 me la salte ya que tenia la cuenta del GitHub creada 

Paso 1: 
creamos el nuevo reporsitorio local ejecudando. 
seguido Configuramos el nombre de usuario y correo electrónico de GitHub
entramos al reporsitorio que acabamos de crear con un cd tallergit 


Paso 2: 
Crea una nueva rama llamada feature con el comando: git checkout -b feature
Se crea un archivo archivo.txt y agregamos contenido a ese archivo con los siguientes comandos: 
DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (feature)
$ echo "Texto inicial" > archivo.txt

DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (feature)
$ git add archivo.txt
warning: in the working copy of 'archivo.txt', LF will be replaced by CRLF the next time Git touches it

DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (feature)
$ git commit -m "Commit inicial"
[feature (root-commit) 1de60f4] Commit inicial
 1 file changed, 1 insertion(+)
 create mode 100644 archivo.txt

Hazmos más cambios en archivo.txt para generar más commints:
DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (feature)
$ echo "Texto agregado en feature" >> archivo.txt

DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (feature)
$ git commit -am "Segundo commit en feature"
warning: in the working copy of 'archivo.txt', LF will be replaced by CRLF the next time Git touches it
[feature 197b0be] Segundo commit en feature
 1 file changed, 1 insertion(+)

DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (feature)
$ echo "Texto agregado en feature" >> archivo.txt

DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (feature)
$ git commit -am "Tercer commit en feature"
warning: in the working copy of 'archivo.txt', LF will be replaced by CRLF the next time Git touches it
[feature da49f89] Tercer commit en feature
 1 file changed, 1 insertion(+)


Paso 3: 
nos cambiamos de vuelta a la rama master
Fusionamos la rama feature con un merge tradicional con el comando git merge feature
nos revertimos de nuevo al merge con: git reset --hard HEAD~1
Hacemos un rebase de la rama feature sobre master con: git rebase feature


Paso 4: 
Creamos una nueva rama hotfix y agregamos un cambio urgente como lo vemos a continuación: 
DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (master)
$ git checkout -b hotfix
Switched to a new branch 'hotfix'

DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (hotfix)
$ echo "Corrección urgente" >> archivo.txt

DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (hotfix)
$ git commit -am "Hotfix"
warning: in the working copy of 'archivo.txt', LF will be replaced by CRLF the next time Git touches it
[hotfix e28a76e] Hotfix
 1 file changed, 1 insertion(+)

Aplicamos ese commit en la rama master usando cherry-pick con los siguientes comnados: git checkout master, git cherry-pick hotfix
Usamos un git reflog para explorar en el historial y restaurar un commit perdido mediante como lo vemos a continuación: 
DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (master)
$  git reflog
9b4186a (HEAD -> master) HEAD@{0}: cherry-pick: Hotfix
da49f89 (feature) HEAD@{1}: checkout: moving from hotfix to master
e28a76e (hotfix) HEAD@{2}: commit: Hotfix
da49f89 (feature) HEAD@{3}: checkout: moving from master to hotfix
da49f89 (feature) HEAD@{4}: rebase (finish): returning to refs/heads/master
da49f89 (feature) HEAD@{5}: rebase (start): checkout feature
197b0be HEAD@{6}: reset: moving to HEAD~1
da49f89 (feature) HEAD@{7}: checkout: moving from feature to master
da49f89 (feature) HEAD@{8}: commit: Tercer commit en feature
197b0be HEAD@{9}: commit: Segundo commit en feature
1de60f4 HEAD@{10}: commit (initial): Commit inicial


Paso 5: 
Aqui creamos un conflicto modificando las mismas líneas en ambas ramas para luego resolverlos durante un merge:
primero los hacemos el cambio en la rama feature de la siguiente manera: 
DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (master)
$ git checkout feature
Switched to branch 'feature'

DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (feature)
$ echo "Cambio en feature" > conflicto.txt

DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (feature)
$ git commit -am "Cambio en feature"
On branch feature
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        conflicto.txt

nothing added to commit but untracked files present (use "git add" to track)

DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (feature)
$ git add conflicto.txt
warning: in the working copy of 'conflicto.txt', LF will be replaced by CRLF the next time Git touches it

DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (feature)
$ git commit -am "Cambio en feature"
[feature 887df08] Cambio en feature
 1 file changed, 1 insertion(+)
 create mode 100644 conflicto.txt

Luego en la rama master de la siguiente forma: 
DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (feature)
$ git checkout master
Switched to branch 'master'

DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (master)
$ echo "Cambio en master" > conflicto.txt

DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (master)
$ git commit -am "Cambio en master"
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        conflicto.txt

nothing added to commit but untracked files present (use "git add" to track)

DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (master)
$ git add conflicto.txt
warning: in the working copy of 'conflicto.txt', LF will be replaced by CRLF the next time Git touches it

DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (master)
$ git commit -am "Cambio en master"
[master 4af4a12] Cambio en master
 1 file changed, 1 insertion(+)
 create mode 100644 conflicto.txt

Por ultimo intentamos hacer un merge para provocar el conflicto y resuélvelo manualmente con un git add conflicto.txt, luego hacemos un commit para decir que terminamos con el conflicto como lo vemos a continuación: 
DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (master)
$ git merge feature
Auto-merging conflicto.txt
CONFLICT (add/add): Merge conflict in conflicto.txt
Automatic merge failed; fix conflicts and then commit the result.

DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (master|MERGING)
$ git add conflicto.txt

DELL@DESKTOP-I3JT7HG MINGW64 ~/tallergit (master|MERGING)
$ git commit -am "terminado conflicto"
[master 81af16f] terminado conflicto
