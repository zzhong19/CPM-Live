# CPM-Live Training Plan
## Table of Contents

- I. General overview of the program
- II. CPM-Live model
- III. Open Source Co-Building
- IV. Use Agreement
- V. Risk Warning
- VI. Support Program
- VII. CPM-Ant training program
- VIII. CPM-Bee training program

## I. General overview of the plan
CPM-Live live training is an open-source large model live training based on CPM series models, and the training process will adopt continuous learning and real-time live training progress. Compared with the existing open-source large models and related live training, CPM-Live has the following features.

- **Continuous learning**: CPM-Live is based on the continuous learning method and will continue to train and improve for a long time in the future. Specifically, the training of CPM-Live will be divided into several stages, and we will start with the training of the 10B large models, providing Chinese and English support and structured input and output capabilities. In the subsequent training, the scale of the CPM-Live model will continue to expand, the data will continue to increase, the capability will continue to improve, and the language will continue to enrich.

- **Open and democratic**: CPM-Live advocates open-source construction and the training process of CPM-Live hopes to actively solicit the opinions and suggestions of the open-source community. In the CPM-Live training process, community users can put forward initiatives on the CPM-Live model including but not limited to model features, training methods, use of data, etc., of which mature initiatives will likely be integrated into the final model. In addition, CPM-Live advocates openness and will provide downloads of relevant model parameters after training, and adopts an open model usage protocol that includes permission for commercialization.

- **Efficient Computing**: The CPM-Live training, compression, and inference process will be based on the OpenBMB open-source community toolkit. With the large model training "engine" BMTrain, we can train very large models of tens of billions or more in small clusters, which significantly reduces the cost of model training and makes our training more low-carbon and efficient. With the large model "thinning" tool library BMCook and efficient inference toolkit BMInf, ordinary users can run large models on consumer-grade graphics cards, so as to experience the charm of large models more conveniently.

## II. CPM-Live Model
### (i) Parameter scale
In the training of CPM-Live, we will achieve continuous parameter growth through multi-stage continuous learning. In order to take into account the computational efficiency in the actual use process, we will provide a variety of commonly used sizes of large model compression version, the specific training scale parameters and open source parameters scale is shown in the following table.

<table align="center">
<tr>
	<th></th>
	<th>Number of layers</th>
	<th>24</th>
	<th>36</th>
	<th>48</th>
	<th>60</th>
	<th>72</th>
	<th>96</th>
</tr>
<tr>
	<td rowspan="7"><strong>Hidden state dimension</strong></td>
	<td>12288</td>
	<td></td>
	<td></td>
	<td></td>
	<td></td>
	<td></td>
	<td>175B (GPT3)</td>
</tr>
<tr>
	<td>8192</td>
	<td></td>
	<td></td>
	<td></td>
	<td></td>
	<td>60B</td>
	<td></td>
</tr>
<tr>
	<td>5120</td>
	<td></td>
	<td></td>
	<td></td>
	<td>20B</td>
	<td>25B</td>
	<td></td>
</tr>
<tr>
	<td>4096</td>
	<td></td>
	<td>:bug: 7B</td>
	<td>:ant: 10B CPM-Ant/Bee</td>
	<td></td>
	<td></td>
	<td></td>
</tr>
<tr>
	<td>2560</td>
	<td></td>
	<td>:bug: 3B</td>
	<td></td>
	<td></td>
	<td></td>
	<td></td>
</tr>
<tr>
	<td>2048</td>
	<td>:bug: 1B</td>
	<td></td>
	<td></td>
	<td></td>
	<td></td>
	<td></td>
</tr>
<tr>
	<td>1024</td>
	<td>:bug: 0.3B</td>
	<td></td>
	<td></td>
	<td></td>
	<td></td>
	<td></td>
</tr>
</table>

				
- :bug: : Published model size
- :ant: : Target model size


For details of the training tools, see.
- [BMTrain](https://github.com/OpenBMB/BMTrain)
- [Model Center](https://github.com/OpenBMB/ModelCenter)

For details on the compression tool, see.
- [BMCook](https://github.com/OpenBMB/BMCook)

### (II) Model Features
CPM-Live has the following model characteristics.

#### Continuously increasing scale
For CPM-Live, we do not seek to shape a model with a huge number of parameters at one time but start from the scale of ten billion parameters, based on model knowledge inheritance, the dynamic growth of parameters and other technologies, to continuously promote the pre-trained model capacity and parameter growth, while effectively avoiding the negative effects of catastrophic forgetting on the continuous learning process. The growth of model parameters depends on whether the model reaches the bottleneck of learning ability or not. The related content can be found in the paper Knowledge inheritance for pre-trained language models.

#### Continuous capacity scaling
We will introduce generic task cues in the pre-training process of CPM-Live and use a self-supervised approach to pre-train these task cues in parallel to facilitate the adaptation of the large model capabilities to downstream tasks. In the initial stage, we will pre-train basic generic cues such as text continuation, rewriting, summarization, and comprehension. New functional task cues will be added to the pretraining later, taking into account specific needs. For more information about the fine-tuning method of pre-trained prompts, please refer to the paper PPT: Pre-trained prompt tuning for few-shot learning.

#### Continuous increase in data
For the training data of CPM-Live, we will initially complete 1TB of training data, and the details of the training data can be found in the Data Analysis section. In the subsequent continuous learning process, we will continue to add more general domain data for training on the one hand; on the other hand, we will add domain data in combination with specific domains to continuously improve CPM-Live's ability to solve specific tasks in specific domains.

#### Version Backward Compatibility
As the model size continues to increase, the model capability continues to grow, and the training data gradually increases, it is easy to have the problem that the earlier version of the hint template does not work with the new version of the model, and we will introduce the necessary measures in the training process of CPM-Live to ensure that the new version has better backward compatibility with the old hint template.

#### Multilingual integration
In the initial model training, we focus on building a large model with Chinese as the core. In the subsequent continuous learning process, we will gradually add data from English and other languages to eventually form a large-scale pre-trained language model with Chinese as the core and multiple languages in mind to provide strong cross-language task support.

#### Complex Structure Processing
The existing pre-trained language models are mainly based on the use of unstructured text for training, so the processing ability of semi-structured and structured data is weak. CPM-Live will gradually add various semi-structured and structured data processing functions during the continuous learning process to better support the processing ability of structured and complex text such as web pages and codes.

### (III) Data processing
CPM-Live carries out a series of processing for raw data to improve data quality, reduce information redundancy and enhance model security, which mainly includes the following three stages.

- **Data filtering**: The data filtering stage uses various filtering schemes such as templates, rules, and PPL to screen out low-quality data and sensitive information in the original corpus, which is used to improve model security and stability in the training stage.
- **Data de-duplication**: The data de-duplication phase uses a hash value approach to de-duplicate the data. The de-duplication algorithm calculates a hash value for each paragraph in the document. When more than 70% of the hash values of the paragraphs in a document have already appeared in the database, it is considered a duplicate, otherwise, the hash values of all paragraphs are stored in the database.
- **Data augmentation**: The data augmentation phase constructs or generates additional supervised signals through some existing models or unsupervised methods, which are used to enhance the performance of the model in the downstream tasks in zero-shot and few-shot environments.
After completing the three phases of processing, the data is finally converted into a series of token ids by the tokenizer and cut into multiple training instances for model training according to the maximum training length of CPM-Live.

## III. open-source co-construction
CPM-Live actively creates a large model online training community and advocates open source sharing in the training process, encouraging community users to participate deeply and actively provide suggestions. The main ways of user participation are as follows.

### (i) Functional initiatives
In the training process of CPM-Live, community users can put forward initiatives on CPM-Live model including but not limited to model characteristics, training methods, use of data and so on. Community users can publish feature initiatives in the community. For initiatives with high feasibility and community support, OpenBMB will assign engineers or community volunteers to exchange and discuss the initiatives, and the initiatives will have the opportunity to be integrated into the current version of the model during the training process of CPM-Live after maturity. If new functions, features or data are added during the training process to stabilize the performance of the model, the initiative will have the opportunity to be integrated into the final version for release.

### (ii) Application Development
Based on the released CPM-Live series models, community users can propose any ideas and works of CPM-Live creative applications in the community, including but not limited to initial ideas, prototype designs, development codes or finished applications. The community will regularly collect the more popular creative applications and display them on the platform.

### (iii) Community Discussion
Users can exchange and discuss about large models in the user community, and the content can be related to academic discussion, engineering implementation, tool use, application design, etc. The community encourages positive and healthy technical exchanges and discussions. The community encourages positive and healthy technical exchanges and discussions, and jointly promotes the construction and development of the ecology related to large models.

### (iv) Model Download
Users can download all public versions of CPM-Live models for free and use them according to the agreement of this plan.

The user community will be based on GitHub-related functions at the beginning, and the subsequent community functions will be improved and integrated into the official website of CPM-Live one after another.

## IV. Use Agreement
The agreement applicable to the CPM-Live series release model is ["General Model License Agreement - Source Description - Publicity Restrictions"].(https://github.com/OpenBMB/General-Model-License/blob/main/%E9%80%9A%E7%94%A8%E6%A8%A1%E5%9E%8B%E8%AE%B8%E5%8F%AF%E5%8D%8F%E8%AE%AE-%E6%9D%A5%E6%BA%90%E8%AF%B4%E6%98%8E-%E5%AE%A3%E4%BC%A0%E9%99%90%E5%88%B6.md) According to the circumstances set under this agreement, the publisher grants users global, non-exclusive and free-use rights, including model inference, model modification, model sharing and distribution, but based on the following prerequisites.

- **Description of Source**: Users shall use the Generic Model and Generic Model results with a link to the source of this Generic Model and this License Agreement.
- **Permission to modify and distribute**: Users may distribute and disseminate derived models and derived model results after modifying the source model at their own discretion.
- **Publicity Restrictions**: Users may not promote the Generic Model on behalf of the publisher.
- **Commercialization**: The user may use the generic model for any commercial purpose.
- **No Additional Restrictions**: The user may not use any additional legal or technical measures to restrict others from doing anything permitted by this License.
For more details on this agreement, please refer to this [website].(https://github.com/OpenBMB/General-Model-License/blob/main/%E9%80%9A%E7%94%A8%E6%A8%A1%E5%9E%8B%E8%AE%B8%E5%8F%AF%E5%8D%8F%E8%AE%AE-%E6%9D%A5%E6%BA%90%E8%AF%B4%E6%98%8E-%E5%AE%A3%E4%BC%A0%E9%99%90%E5%88%B6.md) This Agreement is part of the Generic Model License family, and more information about the Generic Model License can be found on this [website](https://www.openbmb.org/models/license).

## V. Risk Warning
Given the "black box" nature of machine learning models, the models may output uncontrolled content including, but not limited to, disinformation, political misinformation, biased and discriminatory discourse, incitement and innuendo of undesirable behaviour, etc. Although CPM-Live has performed data cleansing on the relevant training data, there is still a risk that it may be used in ways that are not limited to the following. The risk of use is limited to the following. Before using the resources related to CPM-Live, users should be clear about the relevant risks involved in this section and bear all the risks and responsibilities in the process of use.

- **Invasion of personal privacy**: There is a risk that the model may generate personal privacy content, either directly or through guidance.
- **Infringement of Content Copyright**: The Model may directly or indirectly generate content that is identical or similar to other publications.
- **Generate false information**: Models may, directly or through guidance, generate false information that is not factual or objective. Users should not intentionally use and guide the Models to create false content.
- **Generate politically sensitive content**: Models may generate politically sensitive content related to policies, regulations, etc., either directly or through guidance.
- **Generating Biased and Discriminatory Discourse**: Models may be directed or guided to generate biased and discriminatory statements, including but not limited to gender, race, etc.
- **Generate incitement and implication of undesirable behaviour**: Models may incite and suggest, either directly or through guidance, undesirable behaviours such as delinquency.
- **Produce individually hurtful comments**: The model may directly or through guidance produce a discourse that is harmful to individuals, such as discrediting or discouraging individuals or encouraging them to engage in self-harming behaviour.
## VI. Support Programs
It is not easy to train, every time you share and forward will help to train the big model.

If you want to provide computing power, data, financial support or other cooperation, 请联系openbmb@gmail.com.

## VII. CPM-Ant Training Program
See [here] for details(CPM-Ant%E8%AE%AD%E7%BB%83%E8%AE%A1%E5%88%92%E4%B9%A6.md)

## VIII, CPM-Bee training program
See [here] for more details(./CPM-Bee%E8%AE%AD%E7%BB%83%E8%AE%A1%E5%88%92%E4%B9%A6.md)
