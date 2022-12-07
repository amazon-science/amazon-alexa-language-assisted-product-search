## 2022 Amazon Alexa Language Assisted Product Search Challenge

The package defines a set of tool to access the annotated data we collected for 2022 Amazon Alexa language-assisted product search challenge. Please check the detail of the challenge and the dataset [here](https://eval.ai/web/challenges/challenge-page/1845/overview).

The dataset contains 2 types of files, the annotation csv file and the gallery csv file. 

#### The annotation file

The annotation file contains the source product, target product, non-target product and the language feedback provided by the annotator when they wanted to buy the target product but provided with the source product. For each product, we will provide with one ASIN (Product ID) and one image ID. Note, one product may have multiple product images. The image ID we shown in the csv file is the one we showed to the annotator. 

| Source ASIN | Source Image ID  | Target ASIN  | Target Image ID  | Non-Target ASIN  | Non-Target Image ID  | Utterance 1  | Utterance 2  | Utterance 3  |
| :---:   | :-: | :-: | :---:   | :-: | :-: | :---:   | :-: | :-: |
| B076XHGMDF | 51vqFfngUiL | B07ZL983C6 | 31kN-JQA-SL | B075WWCW2S | 415+CAE5ydL | with a candy pink color shirt | with French cuffs | with tan buttons |

To download the annotated images pairs, download the annotation csv file and run following code in ./src

```
python ./download_tool/data_download.py -o <output_path> -i <annotation_csv_path> -t annotation_csv
```

To visualize the annotation with a html file (randomly select n=100). Note that there is no need to download the image files to local disk before the visualization. The html file will directly load image files from Amazon's servers.

```
python ./download_tool/html_visualization_csv.py -o <output_html_path> -i <annotation_csv_path> -n 100
```

#### The gallery image file

The gallery file contains a list of gallery images with ASIN and Image ID. 

| ASIN | Image ID | 
| :---:   | :-: | 
| B076XHGMDF | 51vqFfngUiL |

To download the gallery images, download the gallery csv file and run following code in ./src

```
python ./download_tool/data_download.py -o <output_path> -i <gallery_csv_path> -t gallery_csv
```

#### The query file

The query file is a jsonl file. Each line contains one query (a product and all three feedbacks from the annotator), and a set of candidate products.

```
{
 "index": 1,
 "source_pid": "31DIXIgC5wL",
 "feedback1": "with a grey dress pant",
 "feedback2": "with side button placket waistband",
 "feedback3": "with a taper leg",
 "candidates": [
  {"candidate_pid": "71sq8PHKCeL"},
  {"candidate_pid": "41qOjyIs8YL"}
 ]
}
```

To download the query images, download the gallery csv file and run following code in ./src

```
python ./download_tool/data_download.py -o <output_path> -i <query_jsonl_path> -t qe_jsonl
```

> :warning: For any issue and question, please contact Xu Zhang(xzhnamz@amazon.com), Sanqiang Zhao(sanqiang@amazon.com) or Skyler Zheng(nzhengji@amazon.com). 
