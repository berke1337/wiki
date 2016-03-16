# Setup a git Server
This guide has been tested on Debian. On CentOS I have had some problems I couldn't resolve...

### On the Server:
* `sudo useradd -m -d /var/git -s /bin/bash -c 'Git' git`
* `sudo su - git`
* `mkdir .ssh`
* `vim .ssh/authorized_keys`
* `chmod 700 .ssh`
* `git --bare init test.git`
* `logout`
* `sudo chsh -s /usr/bin/git-shell git`

### On the Client:
* `git remote add origin git@server.com:test.git`
* if not done already, `git add bla.txt`, `git commit`
* `git push origin master`
