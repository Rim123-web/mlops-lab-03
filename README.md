Lab3 : Versionnement des données et pipelines ML avec DVC



<div class="lab-section">

<h2>Lab 3 — Versionnement des données et pipelines ML avec DVC</h2>

<h3>Étape 1 : Initialisation de DVC</h3>

<p>
Cette étape consiste à initialiser <strong>DVC (Data Version Control)</strong> dans le projet afin
de gérer efficacement les fichiers volumineux et les datasets tout en gardant un dépôt Git léger.
</p>

<h3> Instructions</h3>

<ul>
    <li>Ouvrir un terminal à la racine du projet :</li>
</ul>

<pre><code>cd mlops-lab-01</code></pre>

<ul>
    <li>Initialiser DVC :</li>
</ul>

<pre><code>dvc init</code></pre>
<img width="349" height="304" alt="img1_dvc" src="https://github.com/user-attachments/assets/a16596a1-ef75-4171-ac8e-ac55a70136f1" />

<ul>
    <li>Vérifier les fichiers et dossiers créés :</li>
</ul>

<pre><code>.dvc/
.dvc/config</code></pre>
<img width="231" height="115" alt="img2_dvc" src="https://github.com/user-attachments/assets/1efe8cd9-7e6e-454b-ab5b-bcee89c59e24" />



</div>
<!-- ================== END LAB 3 - STEP 1 ================== -->



<!-- ================== LAB 3 - STEP 2 ================== -->


<div class="lab-section">


<h3>Étape 2 : Versionnement des données brutes avec DVC</h3>

<p>
Cette étape vise à versionner le dataset brut généré lors du lab précédent en utilisant
<strong>DVC</strong>, tout en retirant le dossier <code>data/</code> du suivi direct de Git.
Cela permet de conserver un dépôt Git léger et propre.
</p>

<h3> Instructions</h3>

<ul>
    <li>Supprimer toute référence au dossier <code>data/</code> dans le fichier <code>.gitignore</code>.</li>
</ul>
<img width="204" height="200" alt="img3_dvc" src="https://github.com/user-attachments/assets/29dd113d-79d3-4eae-a020-2b63362ecbda" />

<ul>
    <li>Ajouter le dataset brut au suivi DVC :</li>
</ul>

<pre><code>dvc add data/raw.csv</code></pre>
<img width="348" height="167" alt="img4_dvc" src="https://github.com/user-attachments/assets/b682d3b1-0a9b-4911-bfd5-44324d848160" />

<p>
Cette commande génère automatiquement les fichiers suivants :
</p>

<pre><code>data/raw.csv.dvc
data/.gitignore</code></pre>

<ul>
    <li>Ajouter les fichiers DVC et Git nécessaires au versionnement :</li>
</ul>

<pre><code>git add data/raw.csv.dvc data/.gitignore .gitignore
git commit -m "data: suivi du dataset brut via DVC"</code></pre>

<img width="349" height="108" alt="img5_dvc" src="https://github.com/user-attachments/assets/fcf91c02-ea8e-48ac-9994-1b601cb1d962" />


</div>
<!-- ================== END LAB 3 - STEP 2 ================== -->

<!-- ================== LAB 3 - STEP 3 ================== -->


<div class="lab-section">


<h3>Étape 3 : Configuration d’un remote DVC</h3>

<p>
Cette étape consiste à configurer un <strong>remote DVC</strong>, c’est-à-dire un espace de stockage
dédié aux fichiers volumineux versionnés par DVC. Le remote peut être local ou basé sur un service cloud.
</p>

<h3> Instructions</h3>

<ul>
    <li>Créer un dossier qui servira de stockage distant local pour DVC :</li>
</ul>

<pre><code>mkdir dvc_storage</code></pre>
<img width="332" height="177" alt="img6_dvc" src="https://github.com/user-attachments/assets/8dd2e607-2875-41c2-bcac-c813d04ae8fc" />

<ul>
    <li>Déclarer ce dossier comme remote DVC principal :</li>
</ul>

<pre><code>dvc remote add -d localremote dvc_storage</code></pre>
<img width="349" height="75" alt="img7_dvc" src="https://github.com/user-attachments/assets/4d1b9e76-b2c3-4dcb-a727-aaafa6dd0122" />

<p>
<strong>Remarque :</strong> dans un contexte cloud, un remote distant peut également être configuré, par exemple :
</p>

<pre><code># dvc remote add -d storage s3://mybucket/dvcstore</code></pre>

<ul>
    <li>Versionner la configuration du remote avec Git :</li>
</ul>

<pre><code>git add .dvc/config
git commit -m "dvc: configuration du remote local"</code></pre>
<img width="346" height="91" alt="img8_dvc" src="https://github.com/user-attachments/assets/7bb4d47e-a9ed-4767-bbed-862046c36649" />



</div>
<!-- ================== END LAB 3 - STEP 3 ================== -->

<!-- ================== LAB 3 - STEP 4 ================== -->


<div class="lab-section">


<h3>Étape 4 : Push des données dans le remote DVC</h3>

<p>
Cette étape consiste à envoyer les données versionnées par <strong>DVC</strong> vers le remote configuré
précédemment. Cela permet de partager les datasets et de les rendre récupérables par tous les collaborateurs.
</p>

<h3> Instructions</h3>

<ul>
    <li>Envoyer les données vers le remote DVC :</li>
</ul>

<pre><code>dvc push</code></pre>
<img width="340" height="79" alt="img9_dvc" src="https://github.com/user-attachments/assets/a658a5ef-d20e-4133-a018-b33284a4090a" />

<ul>
    <li>Vérifier que le dossier du remote contient les fichiers de hash :</li>
</ul>

<pre><code>dvc_storage/</code></pre>
<img width="377" height="41" alt="img10_dvc" src="https://github.com/user-attachments/assets/c9e1c76b-5fff-41c2-b3fc-7b0466e54fe4" />



</div>
<!-- ================== END LAB 3 - STEP 4 ================== -->


<!-- ================== LAB 3 - STEP 5 ================== -->


<div class="lab-section">


<h3>Étape 5 : Simulation d’une collaboration avec DVC</h3>

<p>
Cette étape simule un scénario collaboratif dans lequel un utilisateur supprime localement
le dataset, puis le récupère depuis le <strong>remote DVC</strong>, démontrant ainsi la fiabilité
et l’efficacité de DVC pour le partage des données.
</p>

<h3> Instructions</h3>

<ul>
    <li>Supprimer le dataset localement :</li>
</ul>

<pre><code>del data\raw.csv   # Windows
# ou
rm data/raw.csv    # Linux / Mac</code></pre>

<ul>
    <li>Vérifier que le dossier <code>data/</code> ne contient plus le fichier :</li>
</ul>

<pre><code>ls data/</code></pre>
<img width="349" height="252" alt="img11_dvc" src="https://github.com/user-attachments/assets/df118151-d24d-4889-a42b-5295b0ab4588" />

<ul>
    <li>Récupérer le dataset depuis le remote DVC :</li>
</ul>

<pre><code>dvc pull</code></pre>

<img width="361" height="142" alt="img12_dvc" src="https://github.com/user-attachments/assets/24f6e460-094c-4403-8252-50ef0b80aec6" />

<img width="145" height="86" alt="img13_dvc" src="https://github.com/user-attachments/assets/901a6d1d-5f90-4505-b7c7-46e738bfc33d" />


</div>
<!-- ================== END LAB 3 - STEP 5 ================== -->


<!-- ================== LAB 3 - STEP 6 ================== -->


<div class="lab-section">


<h3>Étape 6 : Création d’un pipeline reproductible avec <code>dvc.yaml</code></h3>

<p>
Cette étape consiste à créer un pipeline DVC permettant d’automatiser et de rendre reproductibles
toutes les étapes du workflow ML : préparation des données, entraînement du modèle, et évaluation.
</p>

<h3> Instructions</h3>

<h4>1️ Étape de préparation des données :</h4>
<pre><code>dvc stage add -n prepare \
  -d src/prepare_data.py \
  -d data/raw.csv \
  -o data/processed.csv \
  -o registry/train_stats.json \
  python src/prepare_data.py</code></pre>

<img width="325" height="233" alt="img14_dvc" src="https://github.com/user-attachments/assets/dd09043b-676c-49b4-ad5f-5b8968c3cbe9" />

<h4>2️ Étape d’entraînement du modèle :</h4>
<pre><code>dvc stage add -n train \
  -d src/train.py -d data/processed.csv \
  -o models/model.joblib \
  python src/train.py</code></pre>

<img width="329" height="214" alt="img15_dvc" src="https://github.com/user-attachments/assets/a013f351-f528-4adb-a863-02ddd1a62ce9" />


<h4>3️ Étape d’évaluation :</h4>
<pre><code>dvc stage add -n evaluate \
  -d src/evaluate.py \
  -d models/model.joblib \
  -d data/processed.csv \
  -o reports/metrics.json \
  python src/evaluate.py</code></pre>

<img width="329" height="229" alt="img16_dvc" src="https://github.com/user-attachments/assets/8b8905a6-44f4-4f6e-a069-98956df9fc4b" />


<h4>4️ Versionner le pipeline :</h4>
<pre><code>git add dvc.yaml registry/.gitignore reports/.gitignore
git commit -m "pipeline: ajout des étapes prepare/train/evaluate"</code></pre>

<img width="350" height="118" alt="img17_dvc" src="https://github.com/user-attachments/assets/d3055534-b5e2-4a88-a555-091a949d3a5f" />



</div>
<!-- ================== END LAB 3 - STEP 6 ================== -->

<!-- ================== LAB 3 - STEP 7 ================== -->


<div class="lab-section">


<h3>Étape 7 : Reproduction et verrouillage du pipeline</h3>

<p>
Cette étape illustre la **reproductibilité totale** d’un pipeline DVC : si une source change (code ou données),
seules les étapes impactées sont réexécutées automatiquement.
</p>

<h3> Instructions</h3>

<ul>
    <li>Modifier un fichier source, par exemple <code>src/prepare_data.py</code> (ajout d’un <code>print</code>, changement d’un seuil…)</li>
</ul>
<img width="328" height="81" alt="img18_dvc" src="https://github.com/user-attachments/assets/ebbd2ca5-7b18-445b-826f-2f0cdbfabfbf" />

<ul>
    <li>Vérifier l’impact sur le pipeline :</li>
</ul>

<pre><code>dvc repro</code></pre>
<img width="328" height="379" alt="img19_dvc" src="https://github.com/user-attachments/assets/aa4a61ce-e0a4-47bc-ab81-8b33eaeef686" />

<ul>
    <li>Versionner le fichier <code>dvc.lock</code> généré :</li>
</ul>

<pre><code>git add dvc.lock
git commit -m "pipeline: lock after repro"</code></pre>

<img width="356" height="113" alt="img20_dvc" src="https://github.com/user-attachments/assets/9d6846f7-ac95-492f-9645-5c242e7f6d5f" />


</div>
<!-- ================== END LAB 3 - STEP 7 ================== -->
