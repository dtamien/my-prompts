Tu dois produire une représentation textuelle d’une image contenue dans une page de document afin de rendre cette image récupérable par un retriever exclusivement textuel.

Tu reçois trois éléments :

* **PAGE_OCR** : le texte OCR extrait de la page courante ;
* **PAGE_IMAGE** : l’image complète de la page, avec sa mise en page et son contexte visuel ;
* **TARGET_IMAGE** : l’image précise que tu dois décrire.

La description produite sera insérée dans le contenu textuel du document à l’emplacement de TARGET_IMAGE. Elle fera ensuite partie du contenu utilisé pour construire les chunks et effectuer la recherche documentaire.

L’image originale **sera montrée ultérieurement** au modèle chargé de répondre à l’utilisateur. La description n’a donc pas besoin de reproduire exhaustivement tout ce qui est directement visible dans l’image.

## Objectif

Produis une description sémantique de **TARGET_IMAGE uniquement**, suffisamment informative pour qu’un chunk contenant cette description puisse être retrouvé lorsqu’une future requête porte sur une information que TARGET_IMAGE représente, illustre, relie ou permet de déterminer.

La description doit favoriser la récupération de TARGET_IMAGE aussi bien pour des requêtes qui nomment directement son sujet que pour des requêtes qui interrogent une information, une relation, un fonctionnement ou une conclusion que TARGET_IMAGE permet d’établir dans le contexte de la page.

Concentre ton analyse sur TARGET_IMAGE.

Utilise PAGE_IMAGE et PAGE_OCR comme contexte pour comprendre correctement TARGET_IMAGE : sa fonction dans la page, sa légende éventuelle, les termes employés dans le document et les relations qui peuvent exister entre l’image et les autres éléments de la page.

PAGE_IMAGE et PAGE_OCR servent à **interpréter TARGET_IMAGE**, et non à décrire le reste de la page.

## Contenu attendu

Décris en priorité :

* ce que TARGET_IMAGE représente réellement dans le contexte du document ;
* ce qu’elle permet de comprendre, comparer, identifier, déterminer, mesurer, suivre ou déduire ;
* les principales entités, concepts, variables, catégories ou objets concernés ;
* les relations importantes entre ces éléments ;
* les comparaisons, évolutions, tendances, étapes, flux, dépendances, hiérarchies ou correspondances qu’elle représente lorsqu’ils sont pertinents ;
* les éléments suffisamment distinctifs pour qu’une requête portant sur cette image puisse retrouver le chunk.

Ne te limite pas au titre apparent, au type de figure ou à une formulation générique si TARGET_IMAGE contient des informations plus spécifiques utiles au retrieval.

Par exemple, si l’image est simplement intitulée « Architecture de traitement » mais qu’elle montre que la validation d’un token intervient avant l’accès à une base de données, la description doit faire apparaître cette relation si elle peut être établie avec confiance à partir de TARGET_IMAGE et de son contexte. Une future requête peut porter sur « l’endroit où le token est validé avant l’accès à la base » sans jamais employer l’expression « architecture de traitement ».

Lorsque le sens de TARGET_IMAGE dépend de son contexte dans la page, explicite ce lien.

Cela inclut notamment les cas où la signification dépend :

* d’une légende ;
* d’un titre ou sous-titre ;
* d’un paragraphe associé ;
* de couleurs utilisées pour établir une correspondance ;
* de symboles, styles graphiques ou typographiques ;
* de différences de taille, forme, position ou organisation ;
* de renvois entre TARGET_IMAGE et un autre élément visible ou mentionné sur la page.

Dans ces situations, exprime **la signification de la relation**, et pas seulement son apparence visuelle.

Par exemple, si une couleur permet d’associer un élément de TARGET_IMAGE à une catégorie définie ailleurs dans la page, indique cette association lorsqu’elle est pertinente pour comprendre ou retrouver l’image.

## Ce qu’il faut éviter

Évite les détails purement visuels qui n’apportent aucune information utile au retrieval.

Par exemple, ne décris pas simplement :

« une flèche rouge relie deux rectangles »

si le contexte permet plutôt de dire :

« le service d’authentification transmet la requête au service utilisateur ».

N’énumère pas inutilement toutes les valeurs, tous les textes ou tous les détails que le modèle pourra directement voir dans TARGET_IMAGE après retrieval.

En revanche, conserve les informations précises lorsqu’elles sont nécessaires pour caractériser le sujet, distinguer l’image ou comprendre ce qu’elle permet de déterminer.

Ne complète jamais les informations manquantes par supposition.

N’attribue pas à TARGET_IMAGE une information uniquement parce qu’elle apparaît dans PAGE_OCR ou ailleurs dans PAGE_IMAGE. Un lien doit être raisonnablement établi avec TARGET_IMAGE.

En cas d’ambiguïté, formule uniquement ce qui peut être affirmé avec confiance.

## Longueur

La longueur doit être proportionnelle à la richesse informationnelle de TARGET_IMAGE.

Une image simple peut être décrite en une ou deux phrases.

Une figure complexe peut nécessiter plusieurs phrases si plusieurs informations ou relations sont importantes pour permettre son retrieval.

Reste concis, mais ne supprime pas une information utile uniquement pour réduire la longueur.

La description doit être suffisamment complète pour représenter correctement TARGET_IMAGE dans l’index textuel, sans chercher à remplacer l’image elle-même.

## Format de sortie

Retourne uniquement la description destinée à être insérée dans le document.

N’ajoute aucun titre, préfixe, commentaire méthodologique, liste de mots-clés ou explication de ton raisonnement.

PAGE_OCR:
{{PAGE_OCR}}

PAGE_IMAGE:
{{PAGE_IMAGE}}

TARGET_IMAGE:
{{TARGET_IMAGE}}
