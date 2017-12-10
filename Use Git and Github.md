never use 

	pull

	
git branch feature1

	le serveur doit avoir une branche par feature
	mon rep local a la même branche et je bosse dessus
		
git rebase -i ou git rebase --interactif 

	affiche tous les commits crée depuis le commit qu'on a pris sur le serveur
	git rebase -i 98sdf56 tous les commits crée depuis le commit 98sdf56
	permet de :
		reordonner les commits
		fusionner les commits
		supprimer des commits
	
	
git rebase

	met a jour son rep local (plus particulierement sa branche courante) avec celui du serveur (branche correspondante du serveur)
	prend la branche du serveur qui a le même nom que celle où on est en local
	ajoute mes commits 1 a 1 par dessus et demande à resoudre les conflits si confits il y a.
	le faire regulierement (surtout si les autres ne travaillent pas sur la même feature et donc qu'il n'y aura pas de merge conflict)
	permet aussi de sauvegarder les autres branches (features) du serveur localement (utile en cas de perte)
	
git rebase feature2

	pour mettre à jour une autre branche que celle sur laquelle on se trouve 
	
git rebase ??????

	pour mettre à jour toutes les branches du serveur avec les notres
	
git fetch -p

	le -p permet d'eviter de pusher les branches qui on étée supprimées du serveur mais qu'on a toujours en local
	avec la branche (feature) correspondante
	
git push force

	quand on veut push beaucoup de nouveau commits
	on recoit un warning
	pour pusher malgre tout use push force
	
git merge --no-ff au lieu de git merge origin

	quand on veut merger la branche feature du serveur avec la branche master du serveur aussi
	
others stuff

	$ git push
	warning: push.default is unset; its implicit value has changed in
	Git 2.0 from 'matching' to 'simple'. To squelch this message
	and maintain the traditional behavior, use:

	  git config --global push.default matching

	To squelch this message and adopt the new behavior now, use:

	  git config --global push.default simple

	When push.default is set to 'matching', git will push local branches
	to the remote branches that already exist with the same name.

	Since Git 2.0, Git defaults to the more conservative 'simple'
	behavior, which only pushes the current branch to the corresponding
	remote branch that 'git pull' uses to update the current branch.

	See 'git help config' and search for 'push.default' for further information.
	(the 'simple' mode was introduced in Git 1.7.11. Use the similar mode
	'current' instead of 'simple' if you sometimes use older versions of Git)


	Defines the action git push should take if no refspec is explicitly given. Different values are well-suited for specific workflows; for instance, in a purely central workflow (i.e. the fetch source is equal to the push destination), upstream is probably what you want. Possible values are:
	•nothing - do not push anything (error out) unless a refspec is explicitly given. This is primarily meant for people who want to avoid mistakes by always being explicit.
	•current - push the current branch to update a branch with the same name on the receiving end. Works in both central and non-central workflows.
	•upstream - push the current branch back to the branch whose changes are usually integrated into the current branch (which is called @{upstream}). This mode only makes sense if you are pushing to the same repository you would normally pull from (i.e. central workflow).
	•simple - in centralized workflow, work like upstream with an added safety to refuse to push if the upstream branch’s name is different from the local one.
	When pushing to a remote that is different from the remote you normally pull from, work as current. This is the safest option and is suited for beginners.
	This mode has become the default in Git 2.0.
	•matching - push all branches having the same name on both ends. This makes the repository you are pushing to remember the set of branches that will be pushed out (e.g. if you always push maint and master there and no other branches, the repository you push to will have these two branches, and your local maint and master will be pushed there).
	To use this mode effectively, you have to make sure all the branches you would push out are ready to be pushed out before running git push, as the whole point of this mode is to allow you to push all of the branches in one go. If you usually finish work on only one branch and push out the result, while other branches are unfinished, this mode is not for you. Also this mode is not suitable for pushing into a shared central repository, as other people may add new branches there, or update the tip of existing branches outside your control.
	This used to be the default, but not since Git 2.0 (simple is the new default).


	
git init

	[We should have those branches
	Local (git branch ou git branch -vv): 
		master (untracked)
	Upstream (git branch -r ou git branch --remotes -v ou git branch -vv):
		0
	Remote (git remote show origin ou  git ls-remote origin):
		0
		
	We should have those commits (git log --oneline --graph)
		
		* b820def Initial commit

	]

git remote add origin https://github.com/Elorri/MyN.git

	[We should have those branches
	Local (git branch ou git branch -vv): 
		master (untracked)
	Upstream (git branch -r ou git branch --remotes -v ou git branch -vv):
		0
	Remote (git remote show origin ou  git ls-remote origin):
		Fetch URL: https://github.com/Elorri/MyN.git
		Push  URL: https://github.com/Elorri/MyN.git
		HEAD branch: (unknown)
		
	We should have those commits (git log --oneline --graph)
		
		* b820def Initial commit
	]
	
git push -u origin master

	[We should have those branches
	Local (git branch ou git branch -vv): 
		master (tracked)
	Upstream (git branch -r ou git branch --remotes -v ou git branch -vv):
		origin/master
	Remote (git remote show origin ou  git ls-remote origin):
		Fetch URL: https://github.com/Elorri/MyN.git
		Push  URL: https://github.com/Elorri/MyN.git
		HEAD branch: (unknown)
		
	We should have those commits (git log --oneline --graph ou it log --oneline --graph master ou it log --oneline --graph master origin/master give same result)
		
		* b820def Initial commit
	]
	
	
git checkout -b wip-features-desc

	[We should have those branches
	Local (git branch ou git branch -vv): 
	  master            b820def [origin/master] Initial commit
	* wip-features-desc b820def Initial commit

	Upstream (git branch -r ou git branch --remotes -v ou git branch -vv):
		origin/master
	Remote (git remote show origin ou  git ls-remote origin):
		master
		
	We should have those commits (git log --oneline --graph ou it log --oneline --graph master ou it log --oneline --graph master origin/master give same result)
		
		* b820def Initial commit		
	]


git push origin wip-features-desc (si cette branche n'existe pas sur le serveur)

	[We should have those branches
	Local (git branch ou git branch -vv): 
	  master            b820def [origin/master] Initial commit
	* wip-features-desc b820def Initial commit
	Upstream (git branch -r ou git branch --remotes -v ou git branch -vv):
	  origin/master
	  origin/wip-features-desc
	Remote (git remote show origin ou  git ls-remote origin):
		master            tracked
		wip-features-desc tracked
	We should have those commits (git log --oneline --graph ou it log --oneline --graph master ou it log --oneline --graph master origin/master give same result)
		
		* b820def Initial commit	
	]


I add some comits on my local wip-features-desc branch

	git add -A
	git commit -m 'Add feature scenario1-Given'
	git add -A
	git commit -m 'Add feature scenario1-Given (1)'
	git add -A
	git commit -m 'Add feature scenario1-Given (2)'
	git add -A
	git commit -m 'Add feature scenario1-When'
	git add -A
	git commit -m 'Add feature scenario1-Given (3)'
	git add -A
	git commit -m 'Add feature scenario1-Then'	

Other have added new commits on the serveur wip-feature branch
	
	Add feature scenario2-Given
	Add feature scenario2-When
	Add feature scenario2-Then
	
Others have also added 2 new branches

	wip-feature2
	wip-feature3
	
I need to synchronise my local wip-feature branch with the one from the serveur. I do 

	git config --global fetch default (pour voir si le comportement pardéfaut a été changé)
	git fetch -p : (comportement par défaut) copie master du serveur into origin/master + copie wip-feature du serveur into origin/wip-feature + idem if other tracked branches

	[We should have those branches
	Local (git branch ou git branch -vv): 
		master (untracked)
	Upstream (git branch -r ou git branch --remotes -v ou git branch -vv):
		0
	Remote (git remote show origin ou  git ls-remote origin):
		0
	]
	
Others have remove 1 branch

	wip-feature3
	
I need to synchronise my local wip-feature branch with the one from the serveur. I do 

	git config --global fetch default (pour voir si le comportement pardéfaut a été changé)
	git fetch -p : (comportement par défaut) copie master du serveur into origin/master + copie wip-feature du serveur into origin/wip-feature + idem if other tracked branches

	[We should have those branches
	Local (git branch ou git branch -vv): 
		master (untracked)
	Upstream (git branch -r ou git branch --remotes -v ou git branch -vv):
		0
	Remote (git remote show origin ou  git ls-remote origin):
		0
	]
	
I want my list of commit to look like this

	Add feature scenario1-Given
	Add feature scenario1-When
	Add feature scenario1-Then
	
I do git rebase -i ou git rebase --interactive ou git rebase -i bcd5fe (<- is a sha1)

	Add feature scenario1-Given
	Add feature scenario1-When
	Add feature scenario1-Then
	etc

My list of commit is correct. I do git rebase (in the default config. it is equal to git rebase origin/wip-feature and it will mix your current local branch with it. Make sure you are on the correct branch)


	[We should have those branches
	
	Local (git branch ou git branch -vv): 
		master (untracked)
	Upstream (git branch -r ou git branch --remotes -v ou git branch -vv):
		0
	Remote (git remote show origin ou  git ls-remote origin):
		0
	And thoses commits : 
	
	Local (git checkout master + git log --graph --abbrev-commit): 
		master (untracked)
	Upstream (git checkout origin/master + git log --graph --abbrev-commit): 
		0
	Remote (check out github or bitbucket repo):
		0
	]
	
Push your work on the serveur to be able to ask for review. The rebase may have renamed your commits with other sha1, to achieve the proper history you want. If it is the case you will have you will have to force the push.
	
	git config --global push default (pour voir si le comportement par défaut a été changé)
	git push -p (might fail) : (comportement par défaut since git 2.0 (git --version)) push the current branch to its upstream branch but refuses to push if the upstream branch's name is different from the local one. if I'm on wip-feature, it will push on the serveur wip-feature if there is an upstream branch origin/wip-feature
	git push -p --force (or -f) :replace everything on remote with local state of the branch
	git push -p --force-with-lease : prevent there placement of commits not fetched locally (if any). More secure.If you did a fetch just before pushing there shouldn't be such commit like that.

	[We should have those branches
	Local (git branch ou git branch -vv): 
		master (untracked)
	Upstream (git branch -r ou git branch --remotes -v ou git branch -vv):
		0
	Remote (git remote show origin ou  git ls-remote origin):
		0
	And thoses commits : 
	
	Local (git checkout master + git log --graph --abbrev-commit): 
		master (untracked)
	Upstream (git checkout origin/master + git log --graph --abbrev-commit): 
		0
	Remote (check out github or bitbucket repo):
		0
	]
	
Ask someone for review va bitbucket

	git request-pull https://github.com/Elorri/HowTo/branches/wip-feature 
	add the people you want for review

The reviewers have added comments on the serveur branch. If noone has work on your feature don't fetch. Do your modifs. Commits and do, like before.

	git add -A
	git commit -m "fixed a few things"
	git fetch -p
	git rebase
	git push -p (or git push -p --force-with-lease)
	
The serveur wip-feature branch and the upstream origin/wip-feature branch are up to date and working, it is time to add this entiere branch feature to the master of the serveur.

	git checkout master
	git fetch -p (copy remote master into origin/master)
	git rebase origin/master (add all new serveur commits on top of my local master commit + add my new master commit on top of this(I shouldn't have any new master commits normally))
	git merge --no-ff origin/wip-myfeature (add all origin/wip-myfeature commits on top of my local master branch without allowing fast forward+ add a merge commit node)
	git push -p (will push master to the master of the serveur)
	
The feature has been merged on the master. Now you can delete the serveur feature branch and your local branch.

	git branch delete -D wip-my-feature (delete the local one)
	git push --delete origin wip-myfeature wip-my-feature (delete the serveur one)
	
	
	
# MyScript rules

browse the git history local and remote

	git log --graph --abbrev-commit --decorate --date=relative --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)'
	
create an alias for this

	git config --global alias.lg "log --color --graph --abbrev-commit --decorate --date=relative --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)'"
	
use the alias

	git lg # show only current branch
	git lg --all #all branches locales and remotes
	
create a local and remote branch from master to work on it

	git checkout master
	git checkout -b wip-myfeature
	git push origin wip-myfeature
	
work on your branch and regularly update it from the remote

	git fetch (--prune or -p removed deleted branches)
	git rebase (or git pull)
	
to tidy your commits

	git rebase --interactive (-i)
	git rebase -i bcd5fe #specify the commit from which starting the rebase

when your branch is ready

	git fetch -p (-p supprime les branches qui ont été supprimée, en plus de mettre à jour les commits locaux)
	git rebase master (rebase ma branche courante au dessus de master)
	lancer une pull request en utilisant bitbucket

merging and pushing your work on master

	git rebase origin/master
	add your new commits on the serveur branch one by one, asking you to resolve any conflits if needed.
	once finished the serveur branch is up to date
	
on peut aussi faire ceci mais c'est moins bien

	git merge master (ne va pas réécrire l'historique des commits)
	git merge --no-ff origin/wip-myfeature (fait le merge mais non fast forward)
	
pushing a commit that was updated on the serveur

	if the serveur commit is different from the one you want to push, the push or rebase will fail, use push force but be sure of what you do
	git fetch
	git push #might fail
	git push --force (of -f) #replaces everything on remote with the local state of a branch
	git push --force-with-lease # prevents the replacement of commits on remote no fetch locally if any
	
delete local and remote useless branch

	git branch -D wip-myfeature
	git push --delete origin wip-myfeature
	








	


	







	



