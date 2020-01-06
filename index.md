[Published on the peer-reviewed journal Computational Brain & Behavior.](https://link.springer.com/article/10.1007/s42113-019-00071-w?shared-article-renderer)

[Pre-print available for free on bioRxiv.](https://www.biorxiv.org/content/10.1101/862516v1)

This page summarizes two core aspects of the project: 
- The machine learning SVM model that predicts trial-by-trial subject choice based on neural data;
- The neural network model that simulates temporal integration in vision and predicts average subject behavior and neural activity.

# Experimental task

In the present research, subjects performed a word identification task, illustrated in the below figure. An explanation of the key aspects of the task follows; for further details, please refer to the section "Experimental design and behavioral data analysis" within "Material and Methods" in the [paper](https://www.biorxiv.org/content/10.1101/862516v1.full.pdf).

![experimental task](https://raw.githubusercontent.com/lpljacob/word_priming/master/1_paradigm.png)

Each trial began with the presentation of a doubled-up "prime" word. The goal of this word was to change the way subsequent words in the stream are processed by the visual system. The prime word could be presented for a "short" duration of 50ms (very brief and difficult to perceive), or for a "long" duration of 400ms (longer than the time it takes for an adult to read a single word). The prime is doubled-up so that it is not presented in the same screen position as the target

Immediately after the presentation of the prime, a "target" word was presented. It was flashed briefly for around 75ms (time adjusted according to subject performance; goal accuracy was 75%, so target duration was adjusted accordingly to make the task harder or easier). Subjects were instructed to pay attention and identify this target word.

After target word presentation, a "perceptual mask" consisting of randomly-generated lines was shown

# Machine learning SVM model

The goal of the SVM (support vector machine) model was to predict subject choice.
