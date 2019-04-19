	# Debian

## monitoring

	sudo tail -f /var/log/apache2/access.log

## scp

	#copying from remote to local
	scp -vr user@remote:/path/to/file destination/folder

	# inverse for local to remote
	scp -vr /local/file user@remote:/path/to/destination

	# scp may not work while using zsh, so you may need to switch to bash.

# docker

## build image

	docker build -t __placeholder__ .

## create background container

	docker run -dp 9200:9200 --name ES elasticsearch

	# the "d" from -dp actually makes it run in the backfound

## remove all images

	docker rmi -f $(docker images -q)

## run commands inside container

	docker run -it --rm __placeholder__ bash

## stop containers all

	docker stop $(docker ps -q)

# Git

## branching

	git branch iss53
	git checkout iss53
	//or
	git checkout -b iss53
	git commit -m "test"
	// once done
	git checkout master
	git merge iss53

	You can have multiple local branches

## changing credentials

	git config --global user.name "Marc Harriss"

	git config --global user.email [my@email.com]

## checkout changes

	grep -lr '<<<<<<<' . | xargs git checkout --theirs

## copy ssh key

	cat ~/.ssh/id_rsa.pub | pbcopy .

## fix host verify

	ssh-keyscan -H __website.com__ >> ~/.ssh/known_hosts

## get config

	git config -l

## where to find git conf

	sublime ~/.gitconfig

## rm folder once uploaded

	git rm -r --cached node_modules && touch .gitignore && echo "node_modules/" >> .gitignore

## reverse comm

	git reset --soft HEAD^

	// reset to last commit
	git reset --hard HEAD^

# js 

## listen to all event

	Object.keys(window).forEach(key => {
	    if (/^on/.test(key)) {
	        window.addEventListener(key.slice(2), event => {
	            console.log(event);
	        });
	    }
	});

## psuedo elem

	var color = window.getComputedStyle(
		document.querySelector('.element'), ':before'
	).getPropertyValue('color')

# mac

## add app bar space

	$ defaults write com.apple.dock persistent-apps -array-add '{"tile-type"="spacer-tile";}’

	$Killall Dock

	repeat for each spacer

## check npm path

	cd ~/npm-global/bin

	// check if command your are trying to run exists

	// add alias in ~/.zshrc | ~/.bashrc whichever terminal you use

	alias ng="~/.npm-global/bin/__placeholder__

## fix npm links

	add source /Users/YOUUSERNAME/.bash_profile

	to top of ~/.zshrc

## flush dns

	sudo killall -HUP mDNSResponder;say DNS cache has been flushed

	if doesnt work then 

	sudo killall -HUP mDNSResponder;sudo killall mDNSResponderHelper;sudo dscacheutil -flushcache;say MacOS DNS cache has been cleared

## rm mysql Open the Terminal

	Use mysqldump to backup your databases

	Check for MySQL processes with: ps -ax | grep mysql

	Stop and kill any MySQL processes

	Analyze MySQL on HomeBrew:

	brew remove mysql
	brew cleanup
	Remove files:

	sudo rm /usr/local/mysql
	sudo rm -rf /usr/local/var/mysql
	sudo rm -rf /usr/local/mysql*
	sudo rm ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
	sudo rm -rf /Library/StartupItems/MySQLCOM
	sudo rm -rf /Library/PreferencePanes/My*
	Unload previous MySQL Auto-Login:

	launchctl unload -w ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
	Remove previous MySQL Configuration:

	sublime /etc/hostconfig` 
	# Remove the line MYSQLCOM=-YES-
	Remove previous MySQL Preferences:

	rm -rf ~/Library/PreferencePanes/My*
	sudo rm -rf /Library/Receipts/mysql*
	sudo rm -rf /Library/Receipts/MySQL*
	sudo rm -rf /private/var/db/receipts/*mysql*
	sudo rm -rf /etc/my.cnf
	sudo rm -rf /etc/mysql/

	Restart your computer just to ensure any MySQL processes are killed

	Try to run mysql, it shouldn't work

## chrome from term

	chrome () {
	    open -a /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome "$1"
	}

	code () {
		open -a /Applications/Visual\ Studio\ Code.app/Contents/MacOS/Electron "$1"
	}

## watch fs

	sudo fs_usage | grep my.cnf

# mongo

## check apache2 activ

	sudo netstat -plunt | grep apache2

## instal and fix

	brew update

	brew install mongodb

	mkdir -p /data/db

	sudo chown -R `id -un` /data/db

# npm

## shell autocomplete

	npm completion >> ~/.bashrc

	or #

	npm completion >> ~/.zshrc

## view all packages global

	npm ls -g --depth 0

# webiste

## add script to head

	var script = document.createElement('script');
	script.src = "https://code.jquery.com/ui/1.12.1/jquery-ui.js";
	script.integrity = "sha256-T0Vest3yCU7pafRw9r+settMBX6JkKN06dqBnpQ8d30=";
	script.crossOrigin = "anonymous";
	document.head.append(script);

## change icon release note style

	(function() {
	var b = document.querySelectorAll('i.fa-bug');
	var s = document.querySelectorAll('i.fa-star');
	var r = document.querySelectorAll('i.fa-rocket');

	b.forEach(function(item) {
		item.className = 'far fa-bug';
	})

	s.forEach(function(item) {
		item.className = 'far fa-star';
	})

	r.forEach(function(item) {
		item.className = 'far fa-rocket';
	})

	})()

	// easier way

	(function (newS, selector) {
	    var fonts = document.querySelectorAll(selector)
	    fonts.forEach(function(item) {
		item.classList.remove(selector);
		item.classList.add(newS);
	})   
	})('far', 'fa')

## migrating repositories

	git clone --mirror <url_of_old_repo>
	cd <name_of_old_repo>
	git remote add new-origin <url_of_new_repo>
	git push new-origin --mirror