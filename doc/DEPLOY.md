# Procédure de Déploiement

Décrivez ci-dessous votre procédure de déploiement en détaillant chacune des étapes. De la préparation du VPS à la méthodologie de déploiement continu.

## Préparation du VPS

Tout d'abord je me suis connectée à la VM en SSH avec les identifiants fournis. J'ai cloné et ouvert le dossier de projet sur VSCode. J'ai lancé un git init et un git add . suivis d'un premier commit via git commit-m. J'ai généré le cliff.toml grâce à la commande git-cliff --init et généré le CHANGELOG.md avec la commande git-cliff -o CHANGELOG.md. J'ai ensuite commit les fichiers de configuration (avec git add et git commit -m), j'ai ensuite lancé un composer install pour installer les dépendances du projet.

## Méthode de déploiement

J'ai installé aaPanel Free edition sur la VM en root. A la fin de l'installation j'ai noté les identifiants donnés par aaPanel : 
aaPanel Internet Address: https://90.80.241.65:34481/ba5d02ad
aaPanel Internal Address: https://172.16.1.240:34481/ba5d02ad
username: fybrbva4
password: ba8306df
J'ai utilisé ensuite le lien aaPanel Internal Address ainsi que le username et le password fournis. J'ai choisis un installation LNMP avec Nginx en One Click. A la fin de l'installation, j'ai ajouté le site sur aaPanel (Website -> Add site), en database j'ai sélectionné MySQL et j'ai noté les identifiants fournis.
Ensuite, sur la VM, j'ai créé le dépôt Git avec un mkdir dans le dossier var. Dans ce nouveau dossier, j'ai initialisé un dépôt Git vide avec git init --bare.
Dans le dossier projet sur VSCode, j'ai ajouté le remote au projet et vérifié avec un git remote qu'il était bien présent. J'ai ensuite push sur main. J'ai créé ensuite un tag que j'ai poussé.
Dans AaPanel, je suis allée dans Website, j'ai sélectionné mon site, je suis allée dans Site Directory, mis le running directory à /public (Save), désactivé le Anti-XSS attack et laissé le Write access log. Toujours dans les paramètres du site, sur l’onglet plus bas Composer, j'ai exécuté le composer. J'ai enfin créée le .env à partir des informations notées auparavant délivrées par Aapanel dans Files.

Tout allait bien jusqu'au moment où j'ai à nouveau voulu push sur le repo GitHub, plus rien ne passait et tout allait sur la VM... J'ai pu résoudre quelques failles de sécurité et je mettais à jour le CHANGELOG.md à chaque commit mais malheureusement celà n'apparait pas ici...
