# Starter desk

## Installation

### Packages

#### cURL
```bash
sudo apt-get update \
sudo apt-get install curl
```

#### vim
```bash
sudo apt-get update \
sudo apt-get install vim
```

#### git
```bash
sudo apt-get update \
sudo apt-get install git-core
```

#### subversion
```bash
sudo apt-get update \
sudo apt-get install subversion
```

### Applications

#### Filezilla
```bash
sudo apt-get update \
sudo apt-get install filezilla
```

#### Atom
```bash
wget -qO- https://atom.io/download/deb atom.deb \
sudo dpkg -i atom.deb
```

#### GitKraken
```bash
wget -qO- https://www.gitkraken.com/download/linux-deb gitkraken.deb \
sudo dpkg -i gitkraken.deb
```

#### Spotify
```bash
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0DF731E45CE24F27EEEB1450EFDC8610341D9410 \
echo deb http://repository.spotify.com stable non-free | sudo tee /etc/apt/sources.list.d/spotify.list \
sudo apt-get update \
sudo apt-get install spotify-client
```

#### Google Chrome
```bash
echo deb https://dl.google.com/linux/chrome/deb/ stable main | sudo tee /etc/apt/sources.list.d/google-chrome.list \
sudo apt-get update \
sudo apt-get install google-chrome-stable
```

#### Firefox
```bash
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C1289A29 \
echo deb http://downloads.sourceforge.net/project/ubuntuzilla/mozilla/apt all main | sudo tee /etc/apt/sources.list.d/firefox.list \
sudo apt-get update \
sudo apt-get install firefox-mozilla-build
```

### Outils (facultatif, voir Docker plus bas)

#### Drush
```bash
sudo sh -c "curl -L https://s3.amazonaws.com/files.drush.org/drush.phar > /usr/local/bin/drush" \
sudo chmod +x /usr/local/bin/drush \
drush init -y
```

#### WP-cli
```bash
sudo sh -c "curl -L https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar > /usr/local/bin/wp" \
sudo chmod +x /usr/local/bin/wp
```

```bash
sudo sh -c "curl -L https://raw.githubusercontent.com/wp-cli/wp-cli/master/utils/wp-completion.bash > /etc/bash_completion.d/wp-completion"
```

### Docker

#### Docker
```bash
DOCKER_VERSION=`svn ls https://github.com/rancher/install-docker.git/branches/master | grep -Po "(\d+\.)+" | tail -n 1`
wget -qO- https://releases.rancher.com/install-docker/${DOCKER_VERSION}.sh | sh
```

#### Docker-compose
```bash
COMPOSE_VERSION=`git ls-remote --tags https://github.com/docker/compose | grep -oP "[0-9]+\.[0-9][0-9]+\.[0-9]+$" | tail -n 1`
sudo sh -c "curl -L https://github.com/docker/compose/releases/download/${COMPOSE_VERSION}/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose"
sudo chmod +x /usr/local/bin/docker-compose
sudo sh -c "curl -L https://raw.githubusercontent.com/docker/compose/${COMPOSE_VERSION}/contrib/completion/bash/docker-compose > /etc/bash_completion.d/docker-compose"
```

#### Composer
```bash
docker pull composer
```

```bash
# ~/.bashrc or ~/.zshrc
composer () {
    tty=
    tty -s && tty=--tty
    docker run \
        $tty \
        --interactive \
        --rm \
        --user $(id -u):$(id -g) \
        --volume /etc/passwd:/etc/passwd:ro \
        --volume /etc/group:/etc/group:ro \
        --volume $(pwd):/app \
        composer "$@"
}
```

#### Drush
```bash
docker pull drush/drush
```

```bash
# ~/.bashrc or ~/.zshrc
drush () {
    tty=
    tty -s && tty=--tty
    docker run \
        $tty \
        --interactive \
        --rm \
        --user $(id -u):$(id -g) \
        --volume /etc/passwd:/etc/passwd:ro \
        --volume /etc/group:/etc/group:ro \
        --volume $(pwd):/app \
        drush/drush "$@"
}
```

#### Wp-cli
```bash
docker pull wordpress:cli
```

```bash
# ~/.bashrc or ~/.zshrc
wp () {
    tty=
    tty -s && tty=--tty
    docker run \
        $tty \
        --interactive \
        --rm \
        --user $(id -u):$(id -g) \
        --volume /etc/passwd:/etc/passwd:ro \
        --volume /etc/group:/etc/group:ro \
        --volume $(pwd):/app \
        wordpress:cli "$@"
}
```
