# AlexaProductSearchBaseline: Results & Dataloader

This package introduces how to evaluate the baseline model of Amazon Alexa language-assisted product search challenge at 2022 ECCV ILR workshop, along with the dataloader and relevant code of the evaluation.


### VAL: the baseline model

The baseline model for our Amazon Alexa language-assisted product search challenge is VAL by Chen et al. 

[Chen et al. Image Search with Text Feedback by Visiolinguistic Attention Learning. CVPR2020](http://openaccess.thecvf.com/content_CVPR_2020/papers/Chen_Image_Search_With_Text_Feedback_by_Visiolinguistic_Attention_Learning_CVPR_2020_paper.pdf). For original repo, [check here](https://github.com/yanbeic/VAL).

We have linked the original repo to our package, under the VAL directory (via submodule). 

To clone the submodule, please run:

```
git clone --recurse-submodules https://github.com/alexa/amazon-alexa-language-assisted-product-search
```

#### Evaluation Preparation

* Prepare the environment as follows:
	
	- To create a conda environment with the necessary tensorflow version, follow these steps

		```
		conda create -n tensorflow1.15 python=3.6
		conda activate tensorflow1.15
		pip install tensorflow==1.15 nltk numpy==1.18.1
		```
	
	- Open up a python console and run the following lines to download NLTK punkt:

		```
		import nltk
		nltk.download('punkt')
		```
	
	- (Optional) GPU can be used for acceleration. 


* Download the annotation dataset and gallery images according to the instructions in the challenge [website](https://eval.ai/web/challenges/challenge-page/1845/overview). To download the query images, download the gallery csv file (query\_file\_released.jsonl to ./src/VAL\_product\_search/datasets/data) and run following code in ./src

	```
	python download_tool/data_download.py -o ./VAL_product_search/datasets/data/product_search -i ./VAL_product_search/datasets/data/query_file_released.jsonl -t qe_jsonl
	```

* Download the trained VAL checkpoints from [Amazon Drive](https://www.amazon.com/clouddrive/share/TssaYesoP9ux2NpdEkorB0P7ikI7HyB1iLYcG3S8S6l), and put them under VAL\_product\_search/save\_model/product\_search/val\_resnet\_v2\_50\_ml/checkpoints/ directory.

* Download the data annotation files from [Amazon Drive](https://www.amazon.com/clouddrive/share/KceftgFr8Ii07ONZHHCAc7qGNTyRsS20rP3oLE2ASkN), and put them under VAL\_product\_search/datasets/product\_search/captions\_pairs directory.

* Copy all the files under VAL submodule to src/VAL\_product\_search directory.

	```
	cp -r ./VAL/* ./VAL_product_search/
	```

#### Evaluation offline

- Go to VAL\_product\_search directory, use the following bash command for evaluation:
```
bash scripts/run_product_search_eval.sh
```

The above script mainly includes the following three steps:

1. extracting query and gallery features;
2. calculating the Euclidean distance based similary scores between each query and product search image candidates;
3. dumping the evaluation result to a jsonl file for final submission to the challenge website.



### Submission for final online evaluation

- Go to challenge [website](https://eval.ai/web/challenges/challenge-page/1845/overview), direct to Submit page and submit the generated offline evaluation result file. 


> :warning: For any issue and question, please contact Skyler Zheng (nzhengji@amazon.com).