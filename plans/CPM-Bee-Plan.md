#CPM-Bee Training Plan

## I. Model Architecture
The overall structure of CPM-Bee is consistent with CPM-Ant, which can be referred to in the model details.

Compared with CPM-Ant, CPM-Bee has added the following features.

- **Structured Data Processing**: CPM-Bee will support the processing of structured data (e.g. JSON files) to better support downstream applications.
- **Pre-trained Hard Prompts**: In order for CPM-Bee to better grasp the form of structured data corresponding to different tasks, we organize structured data through hard prompts and fully learn these hard prompts in pre-training.
- **Vocabulary Expansion**: CPM-Bee is a multilingual model, so we add vocabulary expansion to support the continuous learning of more languages, and we also introduce word splitters for the simultaneous processing of different languages.
- **[UNK] and [MASK] labels**: traditional pre-training models use uniform [UNK] and [MASK] labels (or similar to T5 pre-training with a fixed number of [MASK] labels), which is difficult to fine-tune the [UNK] and [MASK] processing. Here we will introduce a quantity-adaptive [UNK] and [MASK] mechanism, i.e., the model can automatically recognize [UNK] and [MASK] in the input data, encode them as [MASK#1], [MASK#2]... and [UNK#1], [UNK#2]..., and process each [UNK] and [ MASK] are characterized separately. This mechanism is very useful for processing some web texts with complex contexts, such as texts with emoji.
For performance impact and ease of use, CPM-Bee also introduces some simplifications based on CPM-Ant.
- **Segment Embeddings**: Numerous experiments based on CPM-Ant have shown that in CPM-Ant's Multi-segment Mechanism & Relative Position Bias, the relative position encoding combined with segment information can already effectively distinguish The segmentation characteristics of the input sequence can be effectively distinguished without using segment vectors like those in BERT to guide the model. In addition, segment vectors often face the problem of generalizability, i.e., a large amount of pre-trained data only has 1~2 segments, and the trained model has difficulty in handling input data with more than 2 segments. Therefore, we remove the segment vector design in CPM-Bee.


## II. Model Characteristics
CPM-Bee has the following model characteristics.

### (i) Multilingual integration
In CPM-Ant, we focus on building a large model with Chinese as the core. In CPM-Bee, we will gradually add English and other language data (including independent data of each language and cross-language parallel data) to form a large-scale pre-trained language model with Chinese as the core and multiple languages as well.

### (ii) Complex structure processing
The existing pre-trained language models are mainly based on the use of unstructured text for training, and thus are weak in handling semi-structured and structured data. In CPM-Bee, we will add various types of semi-structured and structured data processing functions to better support the processing capability of structured and complex texts such as web pages and codes. The following shows structured training data.
```json
{
    "document": "Today the weather was really <mask_0>, we went to <mask_1> and played very <mask_2>." ,
    "<ans>": {
        "<mask_0>": "Good",
        "<mask_1>": "Summer Palace",
        "<mask_2>": "Happy"
    }
}
```
(iii) Task mode enhancement
In CPM-Bee, we will introduce data enhancements for various common task modes during pre-training, including generation, Q&A, summarization, translation, etc., to support CPM-Bee's out-of-the-box use on various text processing tasks and enhance the performance of efficient fine-tuning of parameters combined with a small number of samples.

## III. Training details
### (I) Training data
CPM-Ant uses 1TB of raw data and cleans it to get 200GB of high-quality Chinese data, which will continue to be used in CPM-Bee. In addition, CPM-Bee introduces 400GB of multilingual data for pre-training. Based on the above 600GB data, we designed diverse data augmentation algorithms to make CPM-Bee multilingual, which we will expand on in detail in the subsequent technical report.

### (ii) Training tools
In CPM-Ant, we have verified the reliability of OpenBMB's large-model full-flow computing framework, so CPM-Bee will also be trained, fine-tuned, compressed and inferred based on the following tools.

- Training tool [[BMTrain](https://github.com/OpenBMB/BMTrain)]
- Fine-tuning tool [[OpenDelta](https://github.com/thunlp/OpenDelta)]
- Compression tool [[BMCook](https://github.com/OpenBMB/BMCook)]
- Inference tool [[BMInf](https://github.com/OpenBMB/BMInf)]

### (iii) Training Program
CPM-Bee 10B large model training will be launched on October 13, 2022, and will release one version of the model per month.

The model training process focuses on performance monitoring and problem handling, collecting functional initiatives and community discussions and making model modifications and feedback. The main planned related work is as follows.

- Real-time: display model training metrics curves
- Daily: Publish single-day model training logs
- Weekly: centralize the feedback from community discussions and comments
- Periodically: Publish intermediate checkpoint of model training and provide users with downloads
After the model training is completed, CPM-Bee will organize and integrate the community model proposals, compress the models to the appropriate scale, prepare a summary report and publish the relevant models one after another. In addition, for some of the community proposals that are not adopted, we will consider introducing them into the next-generation model training and start the preparation of the next-generation model training.
