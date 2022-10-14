CPM-Ant Training Plan
Considering the scale of data and computing resources, CPM-Live will start with a 10B model training, which we named CPM-Ant. The CPM-Ant model training will be launched on May 29, 2022, and the whole training process is expected to be 5 months.

I. Model Architecture
The model architecture and main settings of CPM-Ant are as follows:


Prompt-based multi-segment framework: Prompts are used to enable the model to quickly switch between comprehension, generation, and summarization functions, and to easily add new functions (learning new prompts).

Segments provide the basic text encoding capability and influence the model encoding pattern through segment embedding. Complex text encoding patterns can be broken down into combinations of several basic segments, for example, the encoding-decoding framework can be broken down into a combination of an encoding segment and a decoding segment. For each base segment, relative position encoding is used within the segment.

Based on the combination of templates and segments, the structure is simple and easy to add and modify modules for continuous learning and functional updates.

Shared embedding: CPM-Ant input embedding and output embedding will share parameters, which is consistent with BERT, GPT and T5, but not with T5-1.1 and mT5. Our experiments show that sharing the input and output embedding parameters greatly enhances the training stability, while not sharing the embedding parameters can easily lead to NaN in the training process.

No bias: In our model, all types of linear transformations and layer norms are not set with bias; on the one hand, it is because the training stability of the model without bias is stronger, and on the other hand, the model without bias is more advantageous in terms of computational speed and memory consumption.

Dynamic word list: For the word list, we will provide a Chinese word list of size 30,000 at the initial stage, which will be dynamically changed in the subsequent training process with new data.


Model Training
During the model training process, we focus on performance monitoring and problem handling, collecting functional initiatives and community discussions, and making model modifications and feedback. The main planned related works are as follows.

Real-time: Display model training metrics
Every day: Release the model training log
Every week: Deal with discussions and feedback from the community
Irregularly: Release checkpoints during model training which everyone can download

After the model training is completed, CPM-Ant will organize and integrate the community model proposals, compress the models to the appropriate scale, prepare a summary report and publish the relevant models one after another. In addition, for some of the community proposals that are not adopted, we will consider introducing them into the next-generation model training.

III. Data Analysis
CPM-Ant uses 1TB of raw data, and 200GB of high-quality data are obtained after cleaning, and the data details are shown in the following table.