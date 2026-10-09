[简体中文](README.md) | [English](README.en.md) | [Русский](README.ru.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Čeština](README.cs.md) | [Dansk](README.da.md) | [Deutsch](README.de.md) | [Esperanto](README.eo.md) | [فارسی](README.fa.md) | [Suomi](README.fi.md) | [Français](README.fr.md) | [Ελληνικά](README.gr.md) | [Magyar](README.hu.md) | [Bahasa Indonesia](README.id.md) | [Italiano](README.it.md) | [മലയാളം](README.ml.md) | [Nederlands](README.nl.md) | [Norsk](README.no.md) | [Polski](README.pl.md) | [Português](README.ptbr.md) | [Română](README.ro.md) | [Türkçe](README.tr.md) | [Українська](README.ua.md) | [Tiếng Việt](README.vn.md)

# ☁️ Cloud-Windows — Bureau Windows cloud gratuit

Transformez une machine virtuelle Windows gratuite de GitHub Actions en un bureau cloud accessible depuis votre navigateur. Ouvrez une page web et vous avez un PC Windows — éteignez-le quand vous avez fini. Entièrement gratuit.

## ✨ Fonctionnalités

- 🖥️ Un bureau Windows complet, directement dans votre navigateur (client web noVNC)
- 📐 **Résolution automatique** : après avoir ouvert la page, la résolution du bureau s'ajuste automatiquement à la taille de votre fenêtre de navigateur — téléphones et PC obtiennent chacun le bon format ; le redimensionnement de la fenêtre est aussi suivi
- 🌐 Accès via le tunnel Cloudflare — pas d'IP publique, pas de traversée de NAT nécessaire
- ⌨️ Méthode de saisie Sogou Pinyin intégrée, la saisie du chinois fonctionne immédiatement (appuyez sur `Win + Space` pour basculer entre le chinois et l'anglais)
- 🖱️ Connectez-vous depuis votre téléphone, tablette ou ordinateur
- ⏱️ Chaque session dure jusqu'à ~6 heures, et vous pouvez l'annuler à tout moment
- 📦 **Édition RustDesk** : il existe aussi un workflow RustDesk qui télécharge automatiquement le dernier installateur RustDesk sur le bureau

## 🚀 Utilisation (fonctionne juste après le fork)

### Étape 1 : Forkez ce projet

Cliquez sur le bouton **Fork** en haut à droite de cette page pour copier le projet dans votre propre compte GitHub. Une fois forké, vous arriverez dans le dépôt `your-username/Cloud-Windows`.

> 💡 Pourquoi forker ? GitHub Actions ne peut s'exécuter que dans les dépôts de votre propre compte — le fork vous donne la permission de l'exécuter.

### Étape 2 : Lancez le bureau cloud

1. Allez sur la page de votre dépôt forké et cliquez sur l'onglet **Actions** en haut
2. Choisissez un workflow à gauche (choisissez-en un) :
   - **Windows Cloud Desktop** : le bureau cloud standard
   - **Windows Cloud Desktop + RustDesk** : l'édition standard plus le téléchargement automatique du dernier installateur RustDesk sur le bureau (version non figée — récupère toujours la dernière version officielle) ; double-cliquez pour l'installer quand vous avez besoin de contrôle à distance
3. Cliquez sur le bouton **Run workflow** à droite — une boîte de dialogue avec trois champs de saisie apparaît :

| Paramètre | Description |
|------|------|
| Mot de passe VNC | Le mot de passe que vous saisirez pour vous connecter au bureau — lettres et chiffres uniquement, 8 caractères maximum (ex. `abc12345`). **Notez-le** |
| Durée d'exécution | Combien de minutes cette session de bureau cloud reste active. Par défaut 300 (5 heures), maximum 350 |
| Résolution | La résolution initiale du bureau, par défaut 1920x1080 ; une fois la page ouverte dans votre navigateur, elle s'ajuste automatiquement à la taille de votre fenêtre |

4. Cliquez sur le bouton vert **Run workflow** pour confirmer — le bureau cloud commence à démarrer

### Étape 3 : Obtenez l'URL d'accès

1. Sur la page Actions, cliquez sur la session que vous venez de lancer (celle du haut — un point jaune signifie qu'elle est en cours)
2. Attendez environ 3 à 5 minutes que la VM installe les logiciels et établisse le tunnel
3. Cliquez sur l'étape **启动服务并建立隧道**, développez les journaux et faites défiler pour trouver une URL comme celle-ci :

```
https://xxx-xxx-xxx.trycloudflare.com/vnc.html
```

4. Copiez l'URL et ouvrez-la dans votre navigateur (le navigateur intégré de votre téléphone fonctionne très bien)

### Étape 4 : Connectez-vous au bureau

1. Sur la page noVNC qui s'ouvre, cliquez sur **Connect**
2. Saisissez le mot de passe VNC défini à l'étape 2
3. Vous y êtes — profitez de votre bureau Windows 🎉
4. La résolution du bureau s'ajustera automatiquement à votre fenêtre de navigateur environ 10 secondes après l'ouverture de la page ; redimensionner la fenêtre déclenche un réajustement automatique (choisi parmi les résolutions prises en charge par votre GPU)

> ⌨️ Appuyez sur **Win + Space** pour basculer la méthode de saisie entre Sogou Pinyin et le clavier anglais.

### Étape 5 : Éteignez-le quand vous avez fini

- Retournez sur la page Actions, ouvrez la session et cliquez sur **Cancel run** en haut à droite — la VM est détruite et le tunnel est coupé
- Elle se termine aussi automatiquement une fois la durée définie écoulée, donc pas de souci à avoir

## ⚠️ Remarques

- **L'URL change à chaque session** : l'ancienne URL cesse de fonctionner dès que la session précédente se termine, utilisez donc toujours l'URL des journaux de la dernière session
- **Rien n'est enregistré** : une fois la VM détruite, les fichiers, téléchargements et états de connexion sur le bureau sont tous effacés — déplacez les fichiers importants à temps
- **Règles du mot de passe** : lettres et chiffres uniquement, 8 caractères maximum — les mots de passe plus longs ou contenant des caractères spéciaux peuvent échouer à la connexion (avec `Authentication failed`)
- **Ne cliquez pas sur Re-run** : pour démarrer un nouveau bureau, cliquez sur **Run workflow** — Re-run rejoue l'ancien code
- **Connexion lente/laggy** : le tunnel passe par Cloudflare ; les vitesses depuis la Chine continentale dépendent de votre réseau, mais c'est utilisable
- **La page ne s'ouvre pas** : vérifiez d'abord que la session est toujours en cours (point jaune) — si elle a été annulée ou terminée, l'URL est morte

## ❓ FAQ

| Symptôme | Cause / Solution |
|------|-----------|
| `loopback connections are not enabled` | Bug d'ancienne version — démarrez une nouvelle session avec le dernier code via Run workflow |
| `Server is not configured properly` | Bug d'ancienne version — démarrez une nouvelle session avec le dernier code via Run workflow |
| `Authentication failed` | Mauvais mot de passe VNC, ou mot de passe de plus de 8 caractères / contenant des caractères spéciaux |
| 502 / 1033 dans la page | Le tunnel n'est pas encore établi ou a été coupé — attendez quelques minutes ou relancez |
| La résolution n'a pas changé automatiquement | Attendez ~10 secondes ; assurez-vous que la taille de la fenêtre du navigateur a réellement changé ; certaines résolutions non standard ne sont pas prises en charge par le GPU et la plus proche est choisie à la place |

## 🛠️ Vous voulez le personnaliser vous-même ?

Les fichiers de workflow se trouvent sous `.github/workflows/` (`windows-vnc.yml` pour l'édition standard, `windows-vnc-rustdesk.yml` pour l'édition RustDesk) — vous pouvez les modifier directement sur le site GitHub ; les changements prennent effet après commit.
