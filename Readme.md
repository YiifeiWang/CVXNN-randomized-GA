# Numerical experiments

## Download datasets
- Download IMDB dataset from [here](https://www.kaggle.com/datasets/lakshmi25npathi/imdb-dataset-of-50k-movie-reviews/) and Amazon dataset from [here](https://huggingface.co/datasets/amazon_polarity) and store them under the folder `./data/`.
- Download GLUE-QQ, GLUE-COLA, MNIST and CIFAR10 datasets based on the notebook `dl_dataset_huggingface.ipynb`.

## Install packages

```
pip install -r requirements.txt
```

## Preprocess data
Run the following lines to obtain OpenAI embedding data.

```
python3 preprocess-dataset.py --data_path ./data --export_num full --embedding OpenAI --data_name IMDB

python3 preprocess-dataset.py --data_path ./data --export_num 30K --embedding OpenAI --data_name Amazon

python3 preprocess-dataset.py --data_path ./data --export_num 50K --embedding OpenAI --data_name glue-qqp

python3 preprocess-dataset.py --data_path ./data --export_num full --embedding OpenAI --data_name glue-cola
```

## Reproduce results

For the result on 2D spiral dataset, simply open the notebook `Illustration_spiral.ipynb`.

For the results on Feature-based transfer learning, run the following lines:

```
for data in IMDB Amazon cola qqp ECG-signal ECG-report mnist cifar10
do
    for tm in cvx noncvx
    do
            python3 main_FT_input_num.py --data_path ./data/ --data_name $data --seed 1 --train_method $tm --Epochs 20 --train_choice f1 --embed OpenAI  --Hidden 50 --train_num f1 --shuffle --add_eps --aug_sym        
    done
done

```

## Plot figures

Open the notebook `FT_plot_input_num.ipynb`