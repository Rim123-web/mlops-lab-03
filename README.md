Lab3 : Versionnement des données et pipelines ML avec DVC



<div class="lab-section">

<h2>Lab 3 — Versionnement des données et pipelines ML avec DVC</h2>

<h3>Étape 1 : Initialisation de DVC</h3>

<p>
Cette étape consiste à initialiser <strong>DVC (Data Version Control)</strong> dans le projet afin
de gérer efficacement les fichiers volumineux et les datasets tout en gardant un dépôt Git léger.
</p>

<h3>📌 Instructions</h3>

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

<h2>Lab 3 — Versionnement des données et pipelines ML avec DVC</h2>

<h3>Étape 2 : Versionnement des données brutes avec DVC</h3>

<p>
Cette étape vise à versionner le dataset brut généré lors du lab précédent en utilisant
<strong>DVC</strong>, tout en retirant le dossier <code>data/</code> du suivi direct de Git.
Cela permet de conserver un dépôt Git léger et propre.
</p>

<h3>📌 Instructions</h3>

<ul>
    <li>Supprimer toute référence au dossier <code>data/</code> dans le fichier <code>.gitignore</code>.</li>
</ul>
<img width="204" height="200" alt="img3_dvc" src="https://github.com/user-attachments/assets/29dd113d-79d3-4eae-a020-2b63362ecbda" />

<ul>
    <li>Ajouter le dataset brut au suivi DVC :</li>
</ul>

<pre><code>dvc add data/raw.csv</code></pre>

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



</div>
<!-- ================== END LAB 3 - STEP 2 ================== -->
