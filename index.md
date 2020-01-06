[Published on the peer-reviewed journal Computational Brain & Behavior.](https://link.springer.com/article/10.1007/s42113-019-00071-w?shared-article-renderer)

[Pre-print available for free on bioRxiv.](https://www.biorxiv.org/content/10.1101/862516v1)

This page summarizes the two computational models used in the project: 
- The **machine learning SVM model** that predicts trial-by-trial subject choice based on neural data;
- The **neural network model** that simulates temporal integration in vision and predicts average subject behavior and neural activity.

In order for the models to be understood, a basic explanation of the experimental task performed by the subjects is included below. For further details, please refer to the section "Experimental design and behavioral data analysis" within "Material and Methods" in the paper.

# Experimental task

In the present research, subjects performed a word identification task, illustrated in the below figure:

<img src="https://raw.githubusercontent.com/lpljacob/word_priming/master/1_paradigm.png" width="300">

Each trial began with the presentation of a doubled-up "prime" word. The goal of this word was to change the way subsequent words in the stream are processed by the visual system. The prime word could be presented for a "short" duration of 50ms, or for a "long" duration of 400ms.

Immediately after the presentation of the prime, a "target" word was presented. It was flashed briefly for around 75ms. Subjects were instructed to pay attention and identify this target word.

After target word presentation, a "perceptual mask" consisting of randomly-generated lines was shown.

Finally, a test display consisting of a single "response" word was presented. Subjects had to decide whether this word was the "same" or "different" from the target word.

# Machine learning SVM model

The goal of the SVM (support vector machine) model was to predict subject choice (whether they pressed the button that corresponded to "same" or "different").
