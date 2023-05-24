# projet_Reco_films
Ce script est utilisé pour recommander des films en utilisant une méthode de filtrage collaboratif basée sur le calcul de similarité entre les films. Voici comment il fonctionne :

    La fonction preprocess_data(df) prend un DataFrame df contenant des informations sur les films et effectue les étapes de prétraitement suivantes :
        Concatène les colonnes "rated", "genre_1", "actor_1" et "plot" en une seule chaîne de caractères, stockée dans une nouvelle colonne appelée "concatenated".
        Retourne le DataFrame modifié.

    La fonction calculate_similarity_matrix(df) prend en entrée le DataFrame prétraité df et effectue les étapes suivantes :
        Utilise la classe TfidfVectorizer de la bibliothèque scikit-learn pour transformer les données textuelles de la colonne "concatenated" en une matrice de vecteurs TF-IDF.
        Applique le noyau sigmoïde (sigmoid_kernel) sur la matrice TF-IDF pour calculer une matrice de similarité entre les films.
        Retourne la matrice de similarité.

    La fonction give_rec(title, sig, indices, df) prend en entrée le titre d'un film, la matrice de similarité, un index des titres des films et le DataFrame df. Elle effectue les étapes suivantes :
        Exclut le film avec le titre donné du DataFrame df.
        Vérifie si le titre du film est présent dans l'index indices.
        Si le titre n'est pas présent, retourne une pd.Series() vide.
        Si le titre est présent, récupère l'indice correspondant et calcule les scores de similarité entre ce film et tous les autres films à l'aide de la matrice de similarité sig.
        Trie les scores de similarité en ordre décroissant.
        Sélectionne les 5 films les plus similaires (à l'exception du film lui-même).
        Retourne les titres de ces films.

    La fonction main() est la fonction principale du script. Elle effectue les étapes suivantes :
        Charge les données des films à partir d'une source non spécifiée en utilisant la fonction load_data().
        Prétraite les données en utilisant la fonction preprocess_data(df).
        Calcule la matrice de similarité en utilisant la fonction calculate_similarity_matrix(df).
        Crée un index des titres des films à l'aide de la colonne "title" du DataFrame df.
        Affiche un sous-titre dans l'interface utilisateur (probablement une interface graphique) demandant à l'utilisateur de sélectionner les films qu'il aime.
        Récupère le premier film sélectionné (ou None s'il n'y en a aucun).
        Utilise la fonction give_rec() pour obtenir les films recommandés en fonction du film sélectionné, de la matrice de similarité, de l'index et du DataFrame df.
        Si des films recommandés sont trouvés, les affiche sous forme de grille d'images avec leurs titres, classements et affiches.

Cela résume le fonctionnement général du script de recommandation de films basé sur une matrice de similarité sigmoïde.
