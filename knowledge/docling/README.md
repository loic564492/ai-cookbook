Construction d'un Pipeline d'Extraction de Connaissances avec Docling

Docling est une bibliothèque open-source puissante et flexible pour le traitement de documents. Elle permet de convertir divers formats de documents en un format unifié et intègre des modèles d'IA avancés pour l'analyse de mise en page et la reconnaissance des structures de tableaux.

L’ensemble du système fonctionne localement sur des ordinateurs standards et est conçu pour être extensible : les développeurs peuvent ajouter de nouveaux modèles ou modifier le pipeline selon leurs besoins. Il est particulièrement utile pour des tâches telles que la recherche documentaire en entreprise, la récupération de passages et l’extraction de connaissances. Grâce à ses capacités avancées de segmentation et de traitement, c'est l'outil idéal pour alimenter les applications d'IA générative avec des pipelines RAG (Retrieval-Augmented Generation).

Principales Fonctionnalités
✅ Support universel de formats : prise en charge des fichiers PDF, DOCX, XLSX, PPTX, Markdown, HTML, images, etc.
✅ Compréhension avancée : analyse de mise en page et reconnaissance des structures de tableaux grâce à l’IA
✅ Sortie flexible : exportation en HTML, Markdown, JSON ou texte brut
✅ Haute performance : traitement rapide sur du matériel local

Améliorations en cours
🛠 Extraction automatique des métadonnées (titre, auteurs, références, langue)
🛠 Intégration de modèles de langage visuel (SmolDocling)
🛠 Compréhension de graphiques (diagrammes en barres, camemberts, courbes, etc.)
🛠 Analyse avancée de structures chimiques (molécules, formules)

Démarrage avec l'exemple
Prérequis
1️⃣ Installez les dépendances :

bash
Copier
Modifier
pip install -r requirements.txt
2️⃣ Configurez votre environnement en créant un fichier .env :

bash
Copier
Modifier
OPENAI_API_KEY=your_api_key_here
Exécution du pipeline
Exécutez les scripts dans l'ordre suivant pour construire et interroger la base documentaire :

1️⃣ Extraction du contenu des documents :

bash
Copier
Modifier
python 1-extraction.py
2️⃣ Segmentation des documents en fragments :

bash
Copier
Modifier
python 2-chunking.py
3️⃣ Création des embeddings et stockage dans LanceDB :

bash
Copier
Modifier
python 3-embedding.py
4️⃣ Test de la recherche basique :

bash
Copier
Modifier
python 4-search.py
5️⃣ Lancement de l’interface Streamlit pour le chat :

bash
Copier
Modifier
streamlit run 5-chat.py
Puis, ouvrez votre navigateur et accédez à http://localhost:8501 pour interagir avec l’interface de questions-réponses.

Traitement des Documents
Formats Pris en Charge
Format	Description
PDF	Documents PDF natifs avec préservation de la mise en page
DOCX, XLSX, PPTX	Fichiers Microsoft Office (2007+)
Markdown	Texte brut avec balisage
HTML/XHTML	Documents Web
Images	PNG, JPEG, TIFF, BMP
USPTO XML	Brevets déposés auprès de l'USPTO
PMC XML	Articles scientifiques de PubMed Central
Pipeline de Traitement
Le pipeline standard inclut :
📌 Analyse du format avec des outils spécifiques
📌 Reconnaissance de mise en page via des modèles IA
📌 Détection des structures de tableaux
📌 Extraction des métadonnées
📌 Organisation et structuration du contenu
📌 Formatage pour l'exportation

Modèles Utilisés
Docling repose sur deux modèles spécialisés pour la compréhension des documents :

1️⃣ Modèle d’analyse de mise en page basé sur RT-DETR (Real-Time Detection Transformer). Il détecte et classe les éléments d'une page en moins d’une seconde sur un CPU standard. Il est entraîné sur DocLayNet, un dataset spécialisé.

2️⃣ TableFormer, un modèle de reconnaissance de structures de tableaux. Il gère des tableaux complexes avec cellules fusionnées, bordures partielles, en-têtes hiérarchiques… Il traite un tableau en 2 à 6 secondes sur CPU.

🔍 OCR en option : Pour l’extraction de texte à partir d’images, Docling peut intégrer EasyOCR. Ce module fonctionne à 216 dpi mais nécessite environ 30 secondes par page.

Les modèles sont disponibles sur Hugging Face sous ds4sd/docling-models.

Segmentation Intelligente des Documents (Chunking)
Lorsqu'on construit une application RAG, il faut découper les documents en morceaux pertinents et exploitables. Mais une découpe arbitraire (tous les 500 mots, par exemple) peut briser le contexte.

Méthodes de segmentation
🔹 Chunking hiérarchique : détecte automatiquement les structures naturelles du document (sections, paragraphes, listes…) pour éviter des coupures inappropriées.
🔹 Chunking hybride : améliore encore la segmentation en :

Fractionnant les morceaux trop longs pour s’adapter au modèle d’embedding
Fusionnant les morceaux trop courts
Optimisant la taille des segments pour le tokenizer utilisé
Pourquoi c'est essentiel pour le RAG ?
Contrairement à une découpe rigide, Docling garantit :
✅ Une cohérence contextuelle : les titres restent associés à leur contenu
✅ La préservation des structures : listes, tableaux et légendes ne sont pas éclatés
✅ Une meilleure pertinence des résultats : chaque segment est autonome et significatif

Cela permet d’améliorer la récupération d’information et la précision des réponses des modèles d’IA.

Documentation
📖 Documentation complète : consultez le site officiel.
📂 Exemples et guides détaillés : explorez le dépôt GitHub.
