# Help 'for all the things'

Here is a help file 'for all the things'. Good luck!

By the way, here is a [markdown cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

# Bash Alias

```
export EDITOR=nano
export KOPS_STATE_STORE=s3://kops-state-rt7665
export NAMESPACE=staging
eval "$(rbenv init -)"

alias fl="networksetup -setairportpower en0 off; sudo route flush; networksetup -setairportpower en0 on;"
alias rs="bundle exec rails s"
alias rc="bundle exec rails c"
alias gs='git status '
alias ga='git add '
alias gb='git branch '
alias gc='git commit'
alias gd='git diff'
alias go='git checkout '
alias eh='subl ~/workspace/help/README.md'
# alias ch='cd ~/workspace/help/;git add .;git commit -m \'Update help\';git push origin master'
alias ks='kubectl'
alias dc='docker-compose'
alias dp='docker ps'
alias di='docker images'
alias wk='cd ~/workspace/'
alias wkp='cd ~/workspace/rotati/pyful/py-api'
alias wkv='cd ~/workspace/rotati/pyful/vue-crypto'
alias wkl='cd ~/workspace/learning/machine-learning-with-python'
alias wkh='cd ~/workspace/help/'
dexec() { docker exec -it "$1" bash; }
drun() { docker run -it --entrypoint bash -v "$PWD":"$1" "$2"; }
dclean() { docker stop $(docker ps -a -q); docker rm -f $(docker ps -a -q); docker rmi -f $(docker images | grep "<none>" | awk "{print \$3}"); docker system prune -f; docker system prune --volumes -f; }
ch() { cd ~/workspace/help/; git add .; git commit -m 'Update help'; git push origin master; }
tf() { docker run -i -t --rm -v $(pwd):/tf -v ~/.aws/:/root/.aws/ -w /tf hashicorp/terraform:light "$1"; } 
```

# Terminal Tips!

`sudo su` elevate to sudo user permanently (without password)

`du -skh *` check the size of files and folders in the current directory

`sed -i -e 's/"Amazon"/"Postgres"/g' appsettings.json` * find and replace a value in a file

`dpkg -l libgdiplus` * check if the libgdiplus is installed on the server

`host myip.opendns.com resolver1.opendns.com` *displays your public ip address*

`sed -i 's/ugly/beautiful/g' /home/bruno/old-friends/sue.txt`

`find . -name *.orig -exec rm {} \; -o -name *DS_Store* -exec rm {} \;`

`rename 's/\.png$/.jpg/' *.png`	*rename all .png to .jpg*

`rename 's/^/avatar_/' *.png`	*append 'avatar_' to all .png files*

`ls ~someuser/`	*Shortcut to the home directory of someuser*

`ls /etc/*a.*` 	*Finds all files in /etc/ with a follwoed by*

`find . -name '*.xml'` *Will find all xml files recursive under the cd*

`find ~ -name development.log` 	*Find all files with name development.log under the home(~)*

`find ~ -name '*.txt' -perm 644` *Finds all .txt files with permission 644*

`find ~ -mtime 0`	*Finds all files modified in the last 24 hours (0 = 24hrs, 1 = 48hrs, 2 = 72hrs)*

`find ~ -atime 0`	*Finds all files accessed in the last 24 hours (0 = 24hrs, 1 = 48hrs, 2 = 72hrs)*

`find workspace -amin 1` *Finds all files accessed in the last 1 minute (can also use: amin, cmin, mmin)*

`find workspace -name dadou -exec rm '{}' \;`	*Finds and deletes all found (test the find on it's own first!)*

`find workspace -name CVS -type d -exec rm -r '{}' \;` *Finds and recursive deletes all CVS folders under workspace*

`find / -user darren`	*Finds all files by darren*

`find / -user darren –exec grep root {} \;` *Finds all files by darren that contain the word "root" (note the use of -exec and "\;" at the end)*

`find ~/workspace -type f -empty` *Find all empty files*

`find ~/workspace -type d -empty` *Find all empty folders*

`tac` *'cat' command in reverse! It dumps content of file in reverse*

`tail` 	*shows the last 10 lines of a file*

`tail -40 /etc/sometime.txt` *Dumps last 40 lines of sometime.txt*

`tail –f`	*shows the last lines of a file and adds to the output as the file grows*

`grep -r dadou ./workspace/*` *Find everything in the workspace that contains the word dadou in the file*

`ls -l > list_of_files.txt` *Redirects the output to a file*

`ls -l >> list_of_files.txt` *Redirects the output to a file (and appends the contents >>)*

`cp -r /var/lib/ejabberd/ workspace/backup/` *Copy a folder from one location to another (note -r)*

`ln -s jruby-1.4.0/ jruby` *creates a simlink to the install folder for JRuby*

`chmod a+wr /some/file` * enables /some/file to be read(r) and write(w) by all(a)

`chmod u+rw /some/file` * enables /some/file to be read(r) and write(w) by the owner(u)

## SSH 

`ssh-keygen` *Generates a new public keypair*

`pbcopy < ~/.ssh/id_rsa.pub` *Securly copy your SSH key to your clipboard*

`ssh-keygen -p -f some-keypair.pem` *Encrypt a private key file*

`ssh-add -K ~/.ssh/id_rsa_somenewkey` *Add the new key to the ssh agent so its used when attempting to authenticate*

## Docker & Docker Compose tips

A good image to use for playing around with Docker and Docker Compose is `tutum/hello-world`

NOTE 1 : If there is a `.env` file in the project directory then it's values will be picked up by compose.

NOTE 2: If there is a `docker-compose.override.yml` file in the same directory then running `docker-compose up` will merge the two files together to create a single config. The override file could be put into a .gitignore file thus allowing developers to make speciif local only changes there without causing issues with others.

`docker-compose exec <service-name> bash`

`docker network ls`

`docker network inspect <name>`

`docker inspect <container-name>`

`docker inspect --format '{{.LogPath}}' <container-name>`

`docker-compose logs -f`

`docker volume ls`

`docker-compose config` #verifies the config is valid

`docker system prune` 

`docker-compose up --build clik.apps.crm`

* Stop and remove all Docker containers

`docker stop $(docker ps -a -q)
docker rm -f $(docker ps -a -q)`

* Remove all untagged images

`docker rmi -f $(docker images | grep "<none>" | awk "{print \$3}")`

## Run a command in a running *container* overriding the default entrypoint
`docker run -it --entrypoint bash ff095591b4d6`

## Run a command from starting up a new container *from an image* and overriding the default entrypoint
`docker run -it --entrypoint bash clik/crm:77ad795`

Another example (without using the --entrypoint flag):

`docker run -di rails6-demo_web bash`

## Run a commmand from a Docker image that requires mounting the local file structure (example below is using terraform)

`docker run -it --rm -v $(pwd):/tf -w /tf hashicorp/terraform:light init`

## Attach a debugger to a running Docker Container

Follow these steps:

1. Put the breakpoint in the code
1. Attach to the running docker container like so `docker attach CONTAINER_ID`
1. Execute the action which will cause the breakpoint to hit

### ... via Docker Compose

Esentially you need to add the following to the docker compose service that you want to debug:

```
stdin_open: true
tty: true
```

Then you simply run `docker attach CONTAINER_ID` and run the code / hit the end point that will cause the debugger to start.

NOTE: To DETACH from the running container WITHOUT stopping it follow the CTRL-p + CTRL-q key sequence

See [this example](https://blog.lucasferreira.org/howto/2017/06/03/running-pdb-with-docker-and-gunicorn.html) for more details.

## Running Postgres in a Docker Container

Run a postgres instance in Docker like so:

`docker run --name postgres_server -e POSTGRES_PASSWORD=mysecretpassword -v postgres_data:/var/lib/postgresql/data -d -p 5432:5432 postgres:10.6`

Now connect to the running server instance `docker exec -it postgres_server_container_id bash;`

...and create the database like so:

```
su - postgres
psql
create database "mycooldb";
```

Test connecting to the database server via the host (i.e. from outside the running db container):

`psql -h localhost -p 5432 -U postgres`

You will be asked for the Postgres server password which is set in the `docker run` command as an environment variable above.

Given the psql CLI connects to the database, the following general psql connection string should also work:

`postgresql://postgres:mysecretpassword@localhost:5432/pyapi-development`

## Let's say you want to test some sql file or data dump someone sent you
## Fire up Postgres instance mounting the folder where the sql files are (e.g. Downloads)

`docker run -v ~/Downloads:/var/data -d postgres:10.6`

### Connect to the running instance using your shortcut

`dexec CONTAINER_ID`

### In postgres you may need to create the database first and then run the folling

`psql -U postgres -d some_database -a -f some_dump_file.sql`

## AWS Linux Bastion Host 

Connect to RDS Postgres

```
sudo yum install postgresql

# Connect to template1 database (enter the pw set during setup)
psql -h RDS_DB_ENDPOINT -p 5432 -U MASTER_USERNAME template1

# Install Git
sudo yum install git

# Install Docker
sudo yum install docker

# Build Docker Image
sudo docker build -t "MY_IMAGE_TAG"

# Set the DATABASE_URL environment var on the host machine `export DATABASE_URL=postgresql+psycopg2://MASTER_USERNAME:MASTER_DB_PASSWORD@DOMAIN:5432/DATABASE_NAME`

# Or run the migrations in the Container and exit
# Note you need to set the DATABASE_URL environment var on the host machine
sudo docker run -it --rm -e DATABASE_URL=$DATABASE_URL py-api:latest flask db upgrade

# Connect to the the Container
sudo docker run -it --entrypoint bash REPOSITORY:TAG

# Test your database by connecting to it directly (see psql above)

```

## VPN (Tunnelblik)

1st turn off wifi manually then run:
`sudo route flush`

OR us the fl alias as setup above! :)

## Python HTTP Server

`python -m SimpleHTTPServer`

## Python Environments

```
# Create a new venv called venv
python -m venv venv

# Activate the venv environment
source venv/bin/activate

# Deactivate the environment
deactivate
```

## Git

Change the username of the commit, run:

```
git config --global user.name "Darren Jensen"
git config --global user.email "darren.jensen@gmail.com"
git config credential.username 'jensendarren'
```

Get the diff between two commits

```
# Between 4ac0a673 and 5688b75
git diff 5688b75..4ac0a673

# Between working copy and 5688b75
git diff 5688b75
```

Show a specific file at a particular commit

```
git show 000a7a9a:path/to/the/file.txt
```

Replace that version of the file in your wd

```
git checkout 000a7a9a path/to/the/file.txt
```

### Pushing to multiple git repos

Taken from [this gist](https://gist.github.com/rvl/c3f156e117e22a25f242)

Start by cloning the test repo!!

`git clone git@bitbucket.org:darren_jensen/hurdey-gurdey.git`

Setup remotes (the **origin** remote probably points to one of these URLs):

```
# Just set one additional remote since we can assume the remote origin is already set to git@bitbucket.org:darren_jensen/hurdey-gurdey.git since that is where we cloned from
git remote add rotati git@github.com:rotati/hurdey-gurdey.git
```

Setup remote push URLs

```
git remote set-url --add --push origin git@bitbucket.org:darren_jensen/hurdey-gurdey.git
git remote set-url --add --push origin git@github.com:rotati/hurdey-gurdey.git
```

Set the default checkout default remote to origin: 

```
git config --add checkout.defaultRemote origin
```

Check the config

```
git remote show origin
cat .git/config
```

So now all pushes will push to both remote repositories (no changes to the workflow here):

```
git push origin master
```

For pulling in work is slightly different in order to fetch changes from both remote repos. In order to do that:

```
git fetch --all
git merge --squash github/next_release bb/next_release
```

Process is:

```
git checkout develop
git pull origin develop
git checkout -b some_new_branch
git fetch --all
git branch -a 
git checkout rotati/167337886_blah <-- now in detached HEAD
git merge some_new_branch <-- effectivly merging in develop HEAD 
git checkout some_new_branch
git merge --squash rotati/167337886_blah
# Do work then commit....
```

### Deleting a local and remote commit

```
# Find the commit SHA you wish to remove from the current branch logs
git log --pretty=oneline --abbrev-commit

# Open the rebase tool to show the last N commits (here 2)
git rebase -i HEAD~2

# In the text editor that opens, remove the commit line from the file
# In my case the file opens in nano so I just remove the like using CTRL+K and then exit from nano

# Check the log again and you should see the commit is gone!
git log --pretty=oneline --abbrev-commit

# Finally, you must to a forced push to update the changes to the remove branch (note the + before the branch name means to force the changes)
git push origin +branch_name
```

### Deleting local and remote branches

```
# To delete a local branch
git branch -d branch_name

# To delete a remote branch
git push <remote_name> --delete <branch_name>
```

## Postgres

`psql -U postgres`

Display current database

`SELECT current_database();`

List databases

`\l`

Connect to a database called mydb

`\c mydb;`

List tables in database

`\d`

List schemas in database

`\dn`

List all tables in a schema (e.g. 'demo')

`\dt demo.`


### Zip

To compress

```
zip -r archive_name.zip folder_to_compress
```

To extract 


```
unzip archive_name.zip
```

### PIP

Install a Python pip package directly from Github:

```
# For example, install the master branch HEAD fof vcrpy package:
pip uninstall vcrpy
pip install https://github.com/kevin1024/vcrpy/archive/master.zip
```

### Tmux

You can attach to another session on a server by using Tmux as follows:

```
tmux attach
```

To detach simply:

```
tmux detach
```

### Curl

Below is a basic bash script example to load test an endpoint:

while true; do sleep 0.01; curl -H "Content-Type: application/json" -X GET www.example.com/someendpoint; echo -e '\n\n\n\n'$(date);done

