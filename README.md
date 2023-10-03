<h1 id="machinelearning_rug">MachineLearning_RUG</h1>
Authors:  

  
Christodoulos Hadjichristodoulou  
Chrysoula Maria Nampouri  
Marios Souroulla  
Filippos Andreadis  

You can find the scientific report [here](https://github.com/philip-andreadis/Machine-Learning-Rug/blob/main/Group23_Semester_project_report.pdf)

<h2 id="environment-setup">Environment setup</h2>
<hr>
<p>The python version this code was tested on is python 3.10, although it should work for earlier versions as well. To create the environment execute the following commands in succession:</p>
<p><code>python -m venv .venv</code></p>
<p><code>source .venv/Scripts/activate</code> or <code>source .venv/bin/activate</code> depending on your platform</p>
<p><code>python -m pip install --upgrade pip</code></p>
<p><code>pip install wheel</code></p>
<p><code>pip install -r requirements.txt</code></p>
<p>In case your system has CUDA support and you would like to activate it:</p>
<p><code>pip uninstall torch</code></p>
<p><code>pip install torch --extra-index-url https://download.pytorch.org/whl/cu117</code></p>
<p>In case the dataset is not provided, download it from <a href="https://www.kaggle.com/datasets/mondejar/mitbih-database">https://www.kaggle.com/datasets/mondejar/mitbih-database</a> and copy the contents to the parent folder of this directory under a directory named &#39;dataset\mitbih_database&#39;.</p>
<h2 id="execution-instructions">Execution instructions</h2>
<hr>
<h3 id="pre-training">Pre-training</h3>
<hr>
<p><code>python main.py --state pre-training</code></p>
<p>This command will start the experiment for the pre-training phase, with the parameters we used in our runs (visible in opts.py). This will create a folder named &#39;output&#39; in the parent of the current directory, which will contain the checkpoints for the model state for each epoch and three log files containing the loss, accuracy and other metrics for training, validation and test. The output folder can be specified with the flag --output_path. Other parameters defined in opts.py can tuned as well.</p>
<h3 id="baseline-individual-classifiers">Baseline individual classifiers</h3>
<hr>
<p><code>python main.py --state individuals</code></p>
<p>This command will start the experiments in which we train the CNN for each patient of our curated subset of patients individually using the best parameter set we found with grid search. This will create the folder &#39;../output/individuals&#39;, which will contain one folder for each patient, each one containing the same files as the ones described in the pre-training section.The output folder can be specified with the flag --output_path.</p>
<h3 id="fine-tuning">Fine-tuning</h3>
<hr>
<p><code>python main.py --state fine_tuning</code></p>
<p>This command will start the experiments in which we fine tune the best performing CNN generated by the pre-training phase to each patient in our curated subset. This will create the folder &#39;../output/fine_tuning&#39;, which will contain one folder for each patient, each one containing the same files as the ones described in the pre-training section.The output folder can be specified with the flag --output_path.</p>
<h2 id="parameter-tuning">Parameter tuning</h2>
<hr>
<p>It is possible to tune the parameters of the experiments from the command line. However, not all parameters defined in opts.py can be changed without unpredictable results. The list of tunable parameters is:</p>
<ul>
<li>data_path: Specify the directory under which the dataset lies. Needs to be specified if the dataset is not copied to the directory named above.</li>
<li>output_path: The folder where the checkpoints and log files will be created.</li>
<li>selected_patients_fine_tuning: The list of patients that will be used for the experiment. Only applies to the baseline individual phase and the fine-tuning phase.</li>
<li>weight_decay: The value of the weight decay parameter of the optimizer.</li>
<li>n_epochs: The maximum number of epochs for which the experiment will run.</li>
<li>batch_size: The batch size used for training</li>
<li>learning_rate: The initial learning rate</li>
<li>weighted_sampling: Whether weighed sampling is enabled or not</li>
</ul>
<p>Note that for the <em>individuals</em> and <em>fine-tuning</em> phases, setting the parameters _batch_size_, _learning_rate_ and _weighted_sampling_ will have no effect, since they will be overriden by the optimal paramer set for each patient.</p>
