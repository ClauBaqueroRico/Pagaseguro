
<center>

![AID logo](./logo_aid.png)

</center>



<center><h1>CLASSIFICATION MODELS</h1></center>



Models for "Classification" workflows, in this path you will find tools to develop, train, test and deploy classification models focused on classifying images or texts depending on their document type.

Here you will find three principal models :

- Beto model: Transfer learning fot text classification using as base model BETO[ bert-base-spanish-wwm-uncased](https://huggingface.co/dccuchile/bert-base-spanish-wwm-uncased) and/or DISTILBETO[ CenIA/distilbert-base-spanish-uncased](https://huggingface.co/CenIA/distilbert-base-spanish-uncased)

- Spacy model: Train spacy model for text classification using [spacy's textcat model](https://spacy.io/api/textcategorizer) 

- ResNet model: Train a Resnet model that is a convolutional neural network that can be utilized as a state of the art for image classification [End-to-End Multiclass Image Classification Example](https://sagemaker-examples.readthedocs.io/en/latest/introduction_to_amazon_algorithms/imageclassification_caltech/Image-classification-fulltraining.html)
----
## General files and folders tree:

```
📦 vsec-aid-modelos
 ┣ 📂 clasificacion
 ┃ ┣ 📂 beto_text_model        --> Beto model folder 
 ┃ ┣ 📂 spacy_text_model       --> Spacy model folder
 ┃ ┣ 📂 image_model            --> ResNet model folder
 ┃ ┣ 📂 utils                  --> Utils folder
 ┃ ┃ ┗ 📄 s3_sync_dataset.py   --> Script to download data from s3 to local
 ┃ ┣ 📂 wf_metrics             --> Wofklow metrics utilities 
 ┃ ┃ ┗ 📂 notebooks_or_scripts --> Notebooks or script to calculate wf metrics
 ┃ ┃ ┃ ┗ 📄 metrics_calc.py -->  Script to calculate wf metrics
 ┃ ┃ ┃ ┗ 📄 metrics_calculator.py -->  Notebook to calculate wf metrics
 ┃ ┃ ┗ 📂 wf_outputs           --> Workflow output folder
 ┃ ┃ ┃ ┗ 📄 results.csv        --> Workflow output downloaded from dynamodb
 ```

- wf_metrics: 
    - notebooks_or_scripts: Notebooks or scripts with predict and ground truth comparing to generate workflow metrics.
    - wf_outputs: Results csv's with the output of ground truth processing on workflow (downloaded from dynamodb).


----

## Common folders for models:

```
📦 vsec-aid-modelos
 ┣ 📂 clasificacion
 ┃ ┣ 📂 xxxx_model  --> Model folder 
 ┃ ┃ ┗ 📂 notebooks --> Notebooks for model training, exploring, evaluating, etc.
 ┃ ┃ ┃ ┗ 📂 explore --> Notebooks for explore.
 ┃ ┃ ┃ ┗ 📂 train   --> Notebooks for model train and eval.
 ┃ ┃ ┃ ┗ 📂 model_metrics --> Notebooks for evaluating if not configured on train.
 ┃ ┃ ┗ 📂 scripts   --> Scripts for model training, exploring, evaluating, etc.
 ┃ ┃ ┃ ┗ 📂 explore --> Scripts for explore.
 ┃ ┃ ┃ ┗ 📂 train   --> Scripts for model train and eval.
 ┃ ┃ ┃ ┗ 📂 model_metrics --> Scripts for evaluating if not configured on train.
 ```

- xxxx_model: Have all necesary files for train, test and deploy the final model ready for production.
- notebooks: 
    - explore: Have notebooks for discovering and testing models or other insights. (Optional)
    - train: Have notebooks to train and improve the model, the final model is trained, deployment tests, metrics, hyperparameter tuning and others are performed. 
    - model_metrics: If model not generate it's own metrics. (Optional)
- scripts: Have final scripts to train the model this usualy include files of preproccesing, inference, train, test and orchestor pipeline end to end
    - explore: Have scripts for discovering and testing models or other insights. (Optional)
    - train: Have scripts to train and improve the model, the final model is trained, deployment tests, metrics, hyperparameter tuning and others are performed. 
    - model_metrics: If model not generate it's own metrics. (Optional)

----

## Training notebooks and scripts versioning:

- For this models there's no difference on scripts or notebooks between trainings. The main difference are the datasets. That's why we don't have a version folder structure for classification models. The latest script or notebook is meant to be used with different dataset versions.

----  

## Dataset tree folders and datasets versioning:

- Model versioning is given by data versioning so you would see that there's a data version for each model that is used to train a model version (all with the same scripts or notebooks, the version is given by data).
- The ground truth is inside every model because it changes as long we change the text_model, BUT, if at sometime we decide to add the image model to the aid workflow, we would have to reconsider this premise.

Bucket data [Link to aws](https://s3.console.aws.amazon.com/s3/buckets/nu0087001-aid-data-bucket?region=us-east-1&prefix=id_cards/&showversions=false)
```
💾nu0087001-aid-data-bucket
📂clasificacion
 ┣ 📂raw_dataset -->  Raw data used to generate all the datasets for all classification models.
 ┣ 📂image_model 
 ┃ ┣ 📂data_v{version #} -->  Data used for traing, val, test and calculate metrics of X model version.
 ┃ ┃ ┣ 📂train ---> Train files separated on subfolders by document tipology. (png)
 ┃ ┃ ┣ 📂val ---> Validation files separated on subfolders by document tipology. (png)
 ┃ ┃ ┣ 📂test ---> Test files. (png)
 ┣ 📂text_model
 ┃ ┣ 📂data_v{version #} --> Data used for traing, val, test and calculate metrics of X model version.
 ┃ ┃ ┃ ┣ 📂dataset --> Png images used to extract text dataset separated on train and val.  (png)
 ┃ ┃ ┃ ┗ 📂text_dataset --> Train and val files separated on subfolders by document tipology. (txt)
 ┃ ┃ ┃ ┃ ┗ 📂train --> Train files separated on subfolders by document tipology. (txt)
 ┃ ┃ ┃ ┃ ┗ 📂val --> Val files separated on subfolders by document tipology. (txt)
 ┃ ┃ ┃ ┗ 📂ground_truth --> Ground truth files.
 ┃ ┃ ┃ ┃ ┗ 📂muestras --> All ground truth files grouped by typology folder (used to validate file typology).
 ┃ ┃ ┃ ┃ ┗ 📂todas --> All ground truth raw files in one folder (used to upload them to aid wf).
```

----
## Datasets synching before training:

For dataset synching we will use the script located in clasificacion/utils/s3_sync_dataset.py 
  1. First we would log in into our aws sandbox account and copy our aws environment variable credentials:
    ![Credentials](./credentials.png)
  2. Then we would open a cmd or terminal and paste the credentials in there.
  3. After that we would look up on the [Data Bucket](https://s3.console.aws.amazon.com/s3/buckets/nu0087001-aid-data-bucket?region=us-east-1&prefix=id_cards/&showversions=false) the dataset we would like to sync.
  4. Having the bucket, main prefix and the sub prefixes we would like to sync we would open a text editor and modify the following line script replacing the {bucket}, {main_prefix} and {list_of_subfolders} with the ones we desire to sync.
   ```
   python3 s3_sync_dataset.py s3://{bucket}/{main_prefix}/ {list_of_subfolders}
   ```
  5. For example if we would like to sync the data_v1 text dataset, with train and val files we could run the command:
   ```
   python3 s3_sync_dataset.py s3://nu0087001-aid-data-bucket/clasificacion/text_model/data_v1/text_dataset/ train,val
   ```
  6. Recommendation: list_of_subfolders are going to be executed in parallel. That's why we suggest to list all the typologies and sync train and val for separated, for example: 
   ```
    python3 s3_sync_dataset.py s3://nu0087001-aid-data-bucket/clasificacion/text_model/data_v1/text_dataset/train/ balance_general,...,cedula_ciudadania
   ```
  7. Run the command on the terminal or cmd while you are standing on the utils folder.
  8. Wait until the script ends executing.
  9. You would see inside the utils folder, a new folder called temp_data that contains the folders and files you asked to sync.

----
## How to calculate workflow metrics:

To calculate workflow metrics you should execute a ground truth on aid's classify workflow, retrieve their results and run a metrics calculator script or notebook as we are going to specify now:

1.  First we have to sync the ground truth from the aws sbx account to our local machine before uploading it to the raw bucket on the dev account. For that we would locate the ground truth we would like to test, for example let's suppose we would like to test the data_v2 ground truth. So first let's sync that grount truth to our local machine as follows:
   ```
    python3 s3_sync_dataset.py s3://nu0087001-aid-data-bucket/clasificacion/text_model/data_v2/ground_truth/ muestras_unificado,todas_unificado
   ```
2.  After that we would have this files on our local machine on the utils/temp_data folder.
3.  Then we would log in into our aws dev account and go to the raw bucket. 
4.  Inside the raw bucket, go to caso_uno/classify path and upload all the samples on utils/temp_data/todas_unificado.
5.  After all the samples are processed by aid's classify workflow you should go to dynamodb results table and download all the results to a csv.
6.  Then open the script or notebook (it doesn't matter) for metrics calculation located on: clasificacion/wf_metrics/notebooks_or_scripts/metrics_calc.pynb or metrics_calcualtor.py
7.  On load predictions section change the route of the results.csv to the one downloaded from dynamodb and run all the notebook or script. (For the scripts case, you should print the variables to see the result or use spyder IDE to inspect variables values).
8.  Accuracy unifying is the final metric of the wf metrics.
   
----
## How to train

### Beto model
Follow [Beto/Distilbeto train documentation](./beto_text_model/manual_ejecucion.md). 

### Spacy model
Follow [Spacy train documentation](./spacy_text_model/manual_ejecucion.md).

### ResNet model
Follow [ResNet train documentation](./image_model/manual_ejecucion.md). 

----

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

----
## License
Internal use of [Bancolombia](https://www.grupobancolombia.com/personas).
