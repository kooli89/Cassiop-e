Langages utilisés : keras 2.6.1 theano backend / notebooks Jupyter anaconda distribution 
Packages : conda install viennarna / conda install -c anaconda biopython 

Les notebooks ipynb sont documentés/commentés, voici l'organisation générale de ce dépôt : 

Ce github contient :

- Un dossier 'benchmark_result' contenant les résultats des algorithmes RNA Subopt RNA duplex et Deep_rna_rna sur le benchmark de notre base de données construite à partir de RISE. Ces données benchmark ont été tirées de la base avant l'apprentissage du réseau de neurones. Le MCC des deux méthodes subopt et duplex sont comparés aux MCC de Deep_rna_rna sur les 2433 paires de séquences du benchmark, de longueur environ 200nt et dont les milieux sont sensés interagir. Nous évaluons la capacité de ces algorithmes à détecter ces sites d'interaction. 

- Un dossier 'genomes' dans lequel ajouter les différentes bases de données nécessaires selon les besoins. Chaque notebook précise les moyens de télécharger les génomes/bases de données. Nos bases d'apprentissage sont disponibles à cette adresse : 
https://drive.google.com/drive/folders/1ecz_YGceAhehFO2kdkJ8B0z_tGLLv5K7?usp=sharing

Si vous souhaitez reconstruire les bases d'apprentissage par vous-mêmes, les génomes humains et de la souris sont disponibles à ces adresses (You can download the reference genome, then use bedtools getfasta / BioPython SeqIO command to retrieve the interacting regions sequence of the duplexes):  
mouse : ftp://ftp.sanger.ac.uk/pub/gencode/Gencode_mouse/release_M9/GRCm38.primary_assembly.genome.fa.gz
human : ftp://ftp.sanger.ac.uk/pub/gencode/Gencode_human/release_24/GRCh38.primary_assembly.genome.fa.gz

RISE est disponible à cette adresse : 
http://rise.life.tsinghua.edu.cn/downloads.html
Human and Mouse Transcriptome-wide studies téléchargées depuis ce site, format .txt à renommer en .csv afin de procéder à la construction des bases de données.



- 6 notebooks Jupyter Anaconda Python dont : 

Building_database_from_RISE.ipynb : construction des bases d'apprentissage depuis RISE, que vous n'avez pas besoin d'exécuter si vous les téléchargez depuis l'adresse mentionnée plus haut.

Deep-rna-rna-data_loading-model_training-testing.ipynb : Chargement des données d'apprentissage et du modèle de réseau de neurones, en keras 2.6.1 theano backend, apprentissage, et test de deep_rna_rna sur des paires de séquences de 36nt interagissant ou non. Acc = 77% et MCC = 0.51 sur un test de 25 000 paires de 36nt. L'apprentissage est effectué sur 140 000 paires. 
Ce réseau de neurones a été sauvegardé et peut être simplement recréé et chargé sans phase d'apprentissage.

Predict_explain.ipynb : notebook dans lequel on peut prédire les interactions entre deux séquences, de façon modulaire, par fenêtrage des deux séquences et évaluation de chaque couple de sites par deep_rna_rna. Le réseau de neurones est chargé et les poids viennent du fichier 'model_rna-rna_deep_livrable.h5'. 
Après prédiction, il est possible de procédder à la phase d'explication par la méthode de Gradient Class Activation Maps, qui extrait les motifs des deux séquences les plus repsonsables de l'interaction sur les deux sites donnés en arguments.

benchmarkRISE-RNASubopt-RNADuplex.ipynb : le notebook évalue les algorithmes RNA subopt et RNA duplex sur le benchmark de nos données issues de RISE. Ces données benchmark ont été tirées de la base avant l'apprentissage du réseau de neurones. Le MCC des deux méthodes subopt et duplex sont comparés aux MCC de Deep_rna_rna sur les 2433 paires de séquences du benchmark, de longueur environ 200nt et dont les milieux sont sensés interagir. Nous évaluons la capacité de ces algorithmes à détecter ces sites d'interaction. 

deep-rna-rna-performances-benchmark.ipynb : Ce notebook calcule cette fois les performances de deep_rna_rna sur ce même benchmark. Le réseau de neurones est chargé à partir des poids 'model_rna-rna_deep_livrable.h5'. Voir dossier benchmark_result. Les MCC sont sauvegardés dans 'MCC_benchmark_deep_rna_rna_.npy'

deep-rna-rna-identify_binding_motifs.ipynb : La méthode Gradient Class Activation Maps est exécutée sur une partie de la base d'apprentissage. Cela permet à grande échell d'identifier des couples de motifs fréquents dans les interactions et d'indentifier des fonctions biologiques traduites par des séquences primaires de nucléotides particulières qui s'apparient au travers des interactions ARN-ARN. Il y a besoin pour cela des bases d'apprentissage. Les motifs trouvés sont enregistrés dans 'motifs.npy'. Le réseau de neurones utilise les poids 'model_finaldeep.h5'. 






