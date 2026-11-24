# My-blog

Blog personnel créé avec Jekyll et publié sur GitHub Pages.

## Prérequis

- Git
- Ruby **3.4.13**
- Bundler **2.6.9**

Ruby et Bundler sont gérés avec [rbenv](https://github.com/rbenv/rbenv). Si rbenv et ruby-build sont installés :

```bash
rbenv install 3.4.13
rbenv shell 3.4.13
gem install bundler -v 2.6.9
```

Sous Ubuntu, la compilation de Ruby peut nécessiter ces paquets système :

```bash
sudo apt update
sudo apt install -y build-essential autoconf bison pkg-config \
  libssl-dev libyaml-dev libreadline-dev zlib1g-dev libffi-dev \
  libgdbm-dev libgdbm6 libncurses5-dev libsqlite3-dev liblzma-dev \
  uuid-dev curl git
```

## Installation du projet

Cloner le dépôt et installer les gems verrouillées par Bundler :

```bash
git clone https://github.com/Mooncode29/My-blog.git
cd My-blog
rbenv shell 3.4.13
bundle _2.6.9_ install
```

## Lancer le site en local

```bash
bundle _2.6.9_ exec jekyll serve
```

Ouvrir ensuite <http://localhost:4000> dans le navigateur. Pour arrêter le serveur, faire `Ctrl+C` dans le terminal.

## Générer le site

```bash
bundle _2.6.9_ exec jekyll build --trace
```

Les fichiers générés sont placés dans `_site/`.

## Dépendances

Les versions des gems sont définies dans `Gemfile` et verrouillées dans `Gemfile.lock`. Pour installer l’environnement existant, utiliser `bundle install` ; ne pas lancer `bundle update` sans intention de mettre à niveau les dépendances.
