[Published on the peer-reviewed journal Computational Brain & Behavior.](https://link.springer.com/article/10.1007/s42113-019-00071-w?shared-article-renderer)

[Pre-print available for free on bioRxiv.](https://www.biorxiv.org/content/10.1101/862516v1)

This page summarizes the two computational models used in the project: 
- The **machine learning SVM model** that predicts trial-by-trial subject behavior based on neural data;
- The **neural network model** that simulates temporal integration in vision and predicts average subject behavior and neural activity.

For better understanding of the models, a basic explanation of the experimental task performed by the subjects is included below. For further details, please refer to the section "Experimental design and behavioral data analysis" within "Material and Methods" in the paper.

## Experimental task

In the present research, subjects performed a word identification task, illustrated in the below figure:

<img src="https://raw.githubusercontent.com/lpljacob/word_priming/master/1_paradigm.png" width="300">

Each trial began with the presentation of a doubled-up "prime" word. The goal of this word was to change the way subsequent words in the stream are processed by the visual system. The prime word could be presented for a "short" duration of 50ms, or for a "long" duration of 400ms.

Immediately after the presentation of the prime, a "target" word was presented. It was flashed briefly for around 75ms. Subjects were instructed to pay attention and identify this target word.

After target word presentation, a "perceptual mask" consisting of randomly-generated lines was shown. The goal of the mask was to reduce visibility of the target word, making the task more difficult.

Finally, a test display consisting of a single "response" word was presented. Subjects had to decide whether this word was the "same" or "different" from the target word. In the figure above, the correct answer would be "different". Subjects indicated their choice by pressing a button once a response cue was displayed.

There were 8 experimental conditions total. These conditions were a product of three factors, each with two levels: prime duration (long or short), whether the response word matched the prime word (primed or unprimed), and what was the correct answer for the trial (same or different). 

## Machine learning SVM model

The goal of the SVM (support vector machine) model was to predict subject choice (whether they pressed the button that corresponded to "same" or "different"). 

The model was trained on the neural EEG (electroencephalogram) data collected during the 700ms following response word presentation, during which subjects deliberated which button to press (they were told to delay any button presses to the moment the response cue was shown). These 700ms of neural data were split into 14 windows of 50ms each; then, each of these 50ms of data were averaged into a single value. This was done independently for each of the 64 EEG sensors, resulting in a 64 (sensors) by 14 (time windows) data matrix for each experimental trial. The data from each trial was then normalized via z-scoring.

Prior to model training, data was set aside for validation. To parse out variability from random sampling, training and validation was conducted 1000 times. Each time, 40 trials for each subject were set aside for validation (5 randomly selected trials from each of the 8 conditions), and the model was trained on all remaining trials (aggregated from all subjects and conditions). Then, the model was validated on the held-out trials. Validation was done three ways: all subjects and conditions to obtain global performance, then on each subject at a time, then on each condition at a time. Model performance was saved, then everything was wiped clean and a new model was trained and validated. Finally, performance from the 1000 models were averaged.

The model predicted subject choice with 66.34% accuracy, a strikingly high value given the large amount of noise present in individual EEG trials. The classifier was above chance for all subjects; the lowest classification performance when validating on an individual subject was 56.38%, showing that the classifier succeeded in finding the neural signals shared between each individual's unique brain anatomy. Therefore, the next step was to identify the temporal profile of the shared neural signals driving the model's predictions.

To that end, the model was trained and validated on each time window separately. The validation accuracy of each time window is shown below.

(figure)

As seen in the figure, for the time windows immediately following response word presentation, accuracy is low and close to chance. This would be expected, considering the brain has not had enough time to process the word. Starting at the 200-250ms window, accuracy quickly rises, peaking at the 350-400ms window. The high predictive power of this individual window coincides with a well-known neural signal called the N400: a negative brain potential that typically peaks around 400ms following display of a word considered to be unexpected by readers. However, the N400 potential can happen in several different contexts, and the scientific literature has struggled to formulate a comprehensive theory of its neural basis. The results of this SVM model, showing that the 350-400ms time window is predictive of behavior in a novelty detection task (i.e. is this new/different or old/same), sheds new light in the neural basis of the N400 potential, and has important implications for the understanding of visual and linguistic processing.

## Neural network model

The goal of the neural network model was to test the validity of a theory known as neural habituation; according to this theory, neurons that respond to a particular visual stimulus (such as a specific word) become low on communication resources (neurotransmitters) if they are presented with their preferred stimulus for a significant period of time. When they are low on resources, their output becomes weaker; while this may appear to be a setback, this weaker output to a continued stimulus allows the brain to respond more strongly to new, different stimuli. In other word, the theory states that resource depletion leads to increased novelty detection.

To test this theory, an artificial neural network model that simulates temporal integration in vision was created, and resource depletion was implemented in the model through a series of mathematical equations. The model, therefore, simulates what is believed to be happening in the brain, and outputs behavior predictions (accuracy across different conditions in the experimental task) and neural activity predictions (the average shape of EEG waveforms elicited by the display of the response word). If the theory underlying the model actually represents what is happening within the brain, the model's predictions will be very similar to the observed data collected from participants.

The model structured is displayed in a schematic below. It is organized in four layers, equivalent to four functional areas of the brain that represent progressively more complex stimuli.

<img src="https://raw.githubusercontent.com/lpljacob/word_priming/master/2_nrouse.png" width="800">

The first (bottom) layer is the retinotipic layer; it represents simple line segments within each position of the visual field. The second layer represents simple visual objects (in the case of the present task, individual letters). The third layer represents more complex objects; lexical entries (words). These three layers together form the perceptual basis of the model (i.e. what is being seen right now). In order for the model to make same/different decisions, it needs a fourth layer; named maintained semantics, it acts as the model's working memory, allowing it to retain the identity of previously seen words for short periods of time.

Each layer contains nodes, and each node represents large group of neurons that respond to the same stimulus. As shown in the figure above, these nodes connect to each other via excitatory or inhibitory connections.
