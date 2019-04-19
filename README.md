# Introduction 	

Just a curation of commands I keep find myself having to google.
If your often scouring through documentation or saving snippets, I would recommend using (Dash)[https://kapeli.com/dash].

## Linux

### Monitoring

Monitor the end of a file

`sudo tail -f /var/log/apache2/access.log`

### Scp

Copying from remote to local

`scp -vr user@remote:/path/to/file destination/folder`

Inverse for local to remote

`scp -vr /local/file user@remote:/path/to/destination`

_scp may not work while using zsh, so you may need to switch to bash._

## Docker

Build image (from directory where there is a dockerfile)

`docker build -t __placeholder__ .`

Create background container

`docker run -dp 9200:9200 --name ES elasticsearch`

_the "d" from -dp actually makes it run in the backfound_

Remove all images

`docker rmi -f $(docker images -q)`

Run commands inside container

`docker run -it --rm __placeholder__ bash`

Stop containers all

`docker stop $(docker ps -q)`

## Git

### Branching

Create Branch

`git branch _branch_name_`
`git checkout _branch_name_`

Shorthand for the above

`git checkout -b _branch_name_`

When happy with changes, merge

`git checkout master`
`git merge _branch_name_`

### changing config

Set global username and email

`git config --global user.name "Marc Harriss"`
`git config --global user.email my@email.com`

Get config

`git config -l`

Where to find git conf

`sublime ~/.gitconfig`

### General
`grep -lr '<<<<<<<' . | xargs git checkout --theirs`

copy ssh key

`cat ~/.ssh/id_rsa.pub | pbcopy .` _(mac)_

fix host verification issue

`ssh-keyscan -H __website.com__ >> ~/.ssh/known_hosts`

### Time-machine

Remove folder once uploaded

`git rm -r --cached node_modules && touch .gitignore && echo "node_modules/" >> .gitignore`

Undo commits

`git reset --soft HEAD^`

reset to last commit

`git reset --hard HEAD^`

## JavaScript

Listen to all events

```JavaScript 
Object.keys(window).forEach(key => {
	if (/^on/.test(key)) {
		window.addEventListener(key.slice(2), event => {
			console.log(event);
		});
	}
});
```

Psuedo elements

```JavaScript
var color = window.getComputedStyle(
	document.querySelector('.element'), ':before'
).getPropertyValue('color')
```

## NPM

### fix paths

`cd ~/npm-global/bin`

_check if command your are trying to run exists_
_add alias in ~/.zshrc | ~/.bashrc whichever terminal you use_

`alias ng="~/.npm-global/bin/__placeholder__`

### fix npm links


Add to top of ~/.zshrc | ~/.bash_profile

`source /Users/YOUUSERNAME/.bash_profile`

View all global packages

`npm ls -g --depth 0`

Shell autocomplete

`npm completion >> ~/.bashrc`
or

`npm completion >> ~/.zshrc`


## MacOS

Add app bar space

`defaults write com.apple.dock persistent-apps -array-add '{"tile-type"="spacer-tile";}’`
`$Killall Dock`
_repeat for each spacer_

Flush dns

`sudo killall -HUP mDNSResponder;say DNS cache has been flushed`

if doesnt work then 

`sudo killall -HUP mDNSResponder;sudo killall mDNSResponderHelper;sudo dscacheutil -flushcache;say MacOS DNS cache has been cleared`

Launching programs from the terminal.

```shell
chrome () {
	open -a /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome "$1"
}
```

```shell
code () {
	open -a /Applications/Visual\ Studio\ Code.app/Contents/MacOS/Electron "$1"
}
```

Watching files

`sudo fs_usage | grep my.cnf`

### rm mysql Open the Terminal

Use mysqldump to backup your databases

Check for MySQL processes

`ps -ax | grep mysql`

Stop and kill any MySQL processes

Analyze MySQL on HomeBrew:

`brew remove mysql`
`brew cleanup`

Remove files:

`sudo rm /usr/local/mysql`
`sudo rm -rf /usr/local/var/mysql`
`sudo rm -rf /usr/local/mysql*`
`sudo rm ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist`
`sudo rm -rf /Library/StartupItems/MySQLCOM`
`sudo rm -rf /Library/PreferencePanes/My*`

Unload previous MySQL Auto-Login:

`launchctl unload -w ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist`

Remove previous MySQL Configuration:

`sublime /etc/hostconfig`

_Remove the line MYSQLCOM=-YES-_
Remove previous MySQL Preferences:

`rm -rf ~/Library/PreferencePanes/My*`
`sudo rm -rf /Library/Receipts/mysql*`
`sudo rm -rf /Library/Receipts/MySQL*`
`sudo rm -rf /private/var/db/receipts/*mysql*`
`sudo rm -rf /etc/my.cnf`
`sudo rm -rf /etc/mysql/`

Reboot just to ensure any MySQL processes are killed
Try to run mysql, it shouldn't work

## MongoDB

Check if apache2 active

`sudo netstat -plunt | grep apache2`

### install and fix

`brew update`

`brew install mongodb`

`mkdir -p /data/db`

It's likely to encounter perm issues.

`sudo chown -R "id -un" /data/db`

## Browser JS

```JavaScript
Add script to head
var script = document.createElement('script');
script.src = "https://code.jquery.com/ui/1.12.1/jquery-ui.js";
script.integrity = "sha256-T0Vest3yCU7pafRw9r+settMBX6JkKN06dqBnpQ8d30=";
script.crossOrigin = "anonymous";
document.head.append(script);
```

Change icons Across Page
```JavaScript
(function (newS, selector) {
	var fonts = document.querySelectorAll(selector)
	fonts.forEach(function(item) {
	item.classList.remove(selector);
	item.classList.add(newS);
})   
})('far', 'fa')
```