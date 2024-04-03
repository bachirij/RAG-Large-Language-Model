# Personnalisation d'un chatbot par la méthode RAG (Retrieval Augmented Generation).

Ce projet a été réalisé en parallèle du projet KiloWhat. Lors du développement de mon site web de vulgarisation scientifique, j'ai voulu intégrer un chatbot personnalisé qui puisse répondre de manière précise et pertinente à des questions sur le génie électrique.

Pour cela, j'ai fait le choix d’utiliser la méthode de Génération Augmentée de Récupération (RAG – Retrieval Augmented Generation). Cette méthode offre un moyen d’améliorer les résultats d’un grand modèle de langage (LLM) en utilisant des informations précises, sans altérer le modèle lui-même. Ces informations peuvent être plus récentes que celles de la version du LLM et spécifiques à une entreprise ou à un secteur donné. Etant donné que la mise à jour constante d’un LLM nécessite d’importantes ressources de calcul, maintenir le modèle constamment à jour n’est pas réalisable. Ainsi, le système d’IA générative peut produire des réponses adaptées aux requêtes d’un utilisateur en se basant sur des données actualisées.

Le RAG offre à l’IA générative la capacité d'incorporer des informations provenant de sources externes, permettant ainsi au chat de fournir des informations plus récentes, mieux adaptées au contexte et plus précises. Cette méthode, relativement récente dans le domaine de l'intelligence artificielle, améliore la qualité des grands modèles de langage (LLM) en leur permettant d'utiliser des ressources de données supplémentaires sans nécessiter de réentraînement. Les modèles de RAG créent des référentiels de connaissances basés sur les données à fournir, et ces référentiels peuvent être continuellement mis à jour pour aider l'IA générative à produire des réponses optimales. La mise en œuvre de la RAG nécessite l'utilisation de technologies telles que les bases de données vectorielles, qui permettent un encodage rapide des nouvelles données, ainsi que des recherches sur ces données pour enrichir le LLM.

Lors de la mise en œuvre d’un RAG, toutes les informations disponibles, qu’elles proviennent de bases de données structurées, de documents PDF non structurés, de blog, etc, sont agrégées et converties dans un format standardisé. Ces données dynamiques sont ensuite stockées dans une bibliothèque de connaissances (ie. une base de donnée) accessible au système d’IA générative, afin de faciliter l’accès et l’utilisation de ces informations par le chatbot. Les données de cette bibliothèque de connaissances sont ensuite traitées en représentations numériques (ie. des vecteurs) à l’aide d’un type d’algorithme appelé modèle de langage intégré ou “embedding”. Ces vecteurs sont ensuite stockés dans une base de données vectorielle qui peut être facilement accessible et utilisée par le LLM pour récupérer des informations contextuelles correctes. 

Lors de l’utilisation du chatbot, la requête de l’utilisateur est transformée en vecteur et est ensuite utilisée pour interroger la base de données de vecteurs, qui extrait des informations pertinentes pour le contexte de cette requête. Ces informations contextuelles récupérées de la base de données sont ensuite introduites dans le LLM, qui génère une réponse textuelle basée à la fois sur ses connaissances généralisées (parfois obsolètes) et sur les informations contextuelles (fournie en amont du LLM à l’aide la méthode RAG).

Le processus de formation du LLM généralisé est long et coûteux, cependant ce n’est pas le RAG pour l’utilisation de la méthode RAG. De nouvelles données peuvent être chargées dans le modèle de langage intégré et traduites en vecteurs numériques de manière continue et incrémentielle. Les réponses de l’ensemble du système d’IA générative peuvent être renvoyées dans le modèle RAG, améliorant ainsi ses performances et sa précision, car il a gardé en mémoire la façon dont il a répondu à des questions similaires dans le passé. C’est pour ces raisons qu’il m’a semblé pertinent d'utiliser cette méthode pour personnaliser mon chatbot.

Pour cela, j’ai mis en œuvre la méthode sur le modèle de langage open source de Mistral, connu sous le nom de Mistral-7B-Instruct-v0.2. et j’ai codé ceci en Python dans un fichier JupyterNotebook à l’aide de JupyterLab. Je me suis aidée de la documentation du framework LangChain, couramment utilisé pour des applications basées sur des modèles de langages.

La première étape de cette méthode consiste à changer nos données dans le système. Dans notre cas, j’ai fourni au système un fichier texte “DonnesElec.txt” contenant toutes les informations des leçons proposées sur notre site web ainsi que des informations complémentaires de pages Wikipedia. 

Chaque bloc obtenu précédemment est transformé en vecteurs à l’aide d’un algorithme d’incorporation via la méthode HuggingFaceEmbedding (importée d’une librairie issue du site open-source HuggingFace), puis ces vecteurs sont stockés dans une base de données vectorielle. Cette base de donnée contient les données de notre fichier “DonneesElec.txt” sous forme de vecteurs, que nous pouvons interroger à l’aide d’un retriever qui permet au LLM d’accéder à ces données. Ainsi, ce chatbot personnalisé est capable de répondre aux questions des utilisateurs entre s’appuyant sur les données que je lui ai fournies.

Par exemple, j’ai demandé à mon chatbot : “Qu’est-ce que le flux conventionnel ?”. Et il a été capable de me répondre : “Le flux conventionnel est une convention historique pour analyser les circuits électriques en considérant le courant électrique comme des charges positives, du pôle positif au pôle négatif. Cela simplifie la compréhension des circuits électriques. Les électrons, qui sont en réalité négatifs et se déplacent du pôle négatif au pôle positif, sont imaginaires dans cette convention.”

Cependant, bien que je n'ai pas réussi à implémenter ce chatbot dans mon site web, ce dernier est bien fonctionnel.
