- [Wine Review API](#wine-review-api)
    - [A propos du dataset](#a-propos-du-dataset)
    - [La stack technique](#la-stack-technique)
        - [Pourquoi MongoDB ?](#pourquoi-mongodb-)
    - [Analyse du fichier `winemag-data-130k-v2.json`](#analyse-du-fichier-winemag-data-130k-v2json)
        - [Champs ayant la valeur nulle](#champs-ayant-la-valeur-nulle)


# Wine Review API

**Wine Review API** fournit des données et des scores qualifiés sur les vins du monde entier.

Les données proviennent de [Kaggle](https://www.notion.so/Data-56d270708947430ea54b929b8f2dc01b) et sont issues d’un `webscraping` du site **WineEnthusiast** en juin 2017. L'API permet les faire des opérations standards telles que la création, la lecture, la mise à jour et la suppression. Elle permet également de faire des recherches par titre et par score.

## A propos du dataset

Le dataset obtenu contient trois fichiers :

- `winemag-data-130k-v2.csv` contient 10 colonnes et 130k lignes de critiques de vins.
- `winemag-data_first150k.csv` contient 10 colonnes et 150k lignes d'évaluations de vins.
- `winemag-data-130k-v2.json` contient 6919 noeuds de critiques de vin.

La version 2 des données est la plus récente . Elle est proposée aux formats `JSON` et `CSV`.

Pour le projet, nous avons choisi le format `JSON`

## La stack technique

- FastAPI
- MongoDB
- Docker et Docker Compose

### Pourquoi MongoDB ?

Comme il a été précisé précédemment, les données sont issues d’un `webscraping`  du site **WineEnthusiast**. ****Nous n’avons donc aucune garantie d’un schéma strict pour ces données. En effet, le site web va évoluer, avoir de nouvelles pages, de nouvelles fonctionnalités. Si nous voulons suivre l'utilisation de ces nouvelles fonctionnalités, vous devons peut-être mettre à jour le schéma de notre base de données.

Pour ce cas d’usage, une base de données de type document comme `MongoDB` parait appropriée. Les documents d'une collection Mongo sont sans schéma et n'ont aucune relation entre eux. Cela signifie que vous pouvez introduire de nouveaux champs à tout moment sans avoir besoin de réviser votre schéma de table au préalable, ce qui vous permet d'itérer plus rapidement.

## Analyse du fichier `winemag-data-130k-v2.json`

### Champs ayant la valeur nulle

Une analyse avec `jq` permet

```json
$>jq . winemag-data-130k-v2.json | grep -E -i null,$ | sort | uniq -c

63     "country": null,
37465     "designation": null,
8996     "price": null,
63     "province": null,
21247     "region_1": null,
79460     "region_2": null,
26244     "taster_name": null,
31213     "taster_twitter_handle": null,
1     "variety": null,

```
