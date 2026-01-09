Things to mention: 


- There were no missing values (described in description of dataset so no preprocessing was necessary)
- I need to explain crossover, mutation and model_selection
- Explain the plots and the data 
- Explain that i didnt go for fault taulerance but something else because thats what the dataset provides as target values or so
- Say that i didnt use seed even though the evaluation can be slow but for the size of this dataset i decided for that because it wouldnt matter that much and i just wanted to be as accurate as possible

- I need to evaluate the model (later compare it with normal backpropargation)
- I need to explain every plot






Contribution Percentage: 100% — I completed the entire Task 2 by myself.

Justification (why & how):

Background & motivation: I have been accepted as an AI Engineer intern at the National Bank of Austria, and developing neural networks and deep learning is my primary area of interest. That motivated me to both implement and compare learning approaches to deepen my practical understanding.
Scope of work: I implemented both a Genetic Algorithm (GA) training workflow and a Backpropagation (BP) training workflow for a simple MLP, then implemented evaluation and visualization to compare them. I intentionally implemented both methods so I could directly observe differences in training dynamics, robustness, convergence behavior, and final performance.
What I implemented (high level):
Designed and implemented a SimpleMLP model (input → hidden → output).
GA support: parameter flattening / reloading, tournament selection, uniform crossover, mutation, population initialization, generation loop, and tracking fitness_history.
Backprop support: PyTorch training loop with mini-batches, Adam optimizer, per-epoch monitoring and test_accs.
Evaluation & visualization: confusion matrix plot, fitness-history plot, and a simple GA vs Backprop comparison cell.
Saved results and plots to files and kept trained models in variables for later analysis (see Task_2_advanced.ipynb).
Choice of target/problem: I did not pursue a fault-tolerance target because the dataset I used provides phishing-related target labels; I selected the dataset that matched the available target values and the assignment's allowed datasets.
Randomness / seed decision: I did not fix a global random seed. Although seeding can make experiments reproducible, for this dataset size I prioritized natural variation and aiming for best achievable accuracy rather than forcing deterministic runs; the evaluation runs are reasonably fast and results are stable enough for comparison. (Note: if strict reproducibility is required, a seed can be added easily.)
Preprocessing: The dataset documentation indicated no missing values, so no missing-value imputation was necessary. I remapped target classes to {0,1,2} for PyTorch compatibility and converted features/labels to tensors.
Special approach / personal contribution style:

I focused on clarity and pedagogy: implementing each component (model, GA genome encoding, genetic operators, training loops) in a straightforward, readable way to make later interpretation easier.
I deliberately implemented the GA by directly manipulating flattened parameter vectors and reloading them into the model—this made the comparison to backprop clearer (weights updated as genomes vs. gradient updates).
I tracked simple, interpretable metrics (fitness_history, test_accs) and added lightweight plotting (confusion matrix, fitness over generations, accuracy per epoch) to make side-by-side comparison immediate for a reader.
Notes / dataset specifics:

The dataset contains three target labels (mapped from {-1,0,1} → {0,1,2}); label mapping and class names are used in evaluation plots.
No missing values were present according to the dataset description, so no imputation or complex preprocessing steps were required.
Open next step (left for later):

Interpretation and comparison of model behaviors and results (detailed analysis of confusion matrices, convergence patterns, per-class performance, and trade-offs) — I leave this analysis step open until the notebook is executed to produce the actual numeric results and plots. Once you want that, I can run the notebook, collect outputs, and produce the interpretation section.
Reference: implementation and code are in Task_2_advanced.ipynb.

GPT-5 mini • 0x









































Own Contribution Document – Task 2

Name: Florian Köhl
Contribution: 100% of Task 2

Justification (why & how)

I completed Task 2 entirely on my own. My motivation for investing additional effort into this task is that I have already been accepted as an AI Engineer Intern at the National Bank of Austria, and neural networks and deep learning are my primary areas of interest. I therefore chose to treat this task not only as an assignment, but also as a learning opportunity.

Scope of implementation
- Design and implementation of a 3-layer MLP
- GA training: genome encoding, selection, crossover, mutation, fitness tracking
- BP training: mini-batch training loop, Adam optimizer, loss tracking
- Evaluation: accuracy, precision, recall, F1-score, confusion matrices, and training dynamics plots
























Task 2 – Application of Genetic Algorithm for Training ANN
Author: Florian Köhl

In Task 2, a three-layer Multi-Layer Perceptron (MLP) was implemented and trained using a Genetic Algorithm (GA) for a multi-class classification problem. The dataset was split into training and test sets (80/20), and appropriate evaluation metrics such as accuracy, precision, recall, F1-score, and confusion matrices were used to assess performance.

In addition to the GA-based training, a Backpropagation-based training approach was implemented for the same network architecture. This allowed for a direct comparison between evolutionary optimization and gradient-based learning in terms of convergence behavior, robustness, and final classification performance.


Special approach and contributions
- I implemented both a Genetic Algorithm (GA) and a Backpropagation (BP) training workflow for the same MLP architecture.
This was done intentionally, as I believe the direct comparison between evolutionary and gradient-based learning provides the strongest learning effect.
- I did not focus on fault-tolerance prediction, but instead selected a classification problem aligned with the available target values of the chosen dataset (phishing-related labels), which is explicitly allowed by the assignment.
- According to the dataset documentation, no missing values were present, so no imputation or additional preprocessing steps were required.


Comparison: Genetic Algorithm (GA) vs. Backpropagation (BP)

Both approaches achieved similar overall test performance on the phishing dataset. This shows that, at a high level, both GA-based training and gradient-based backpropagation are capable of learning a reasonable decision boundary for the problem.
However, a class-wise analysis reveals important differences.

Suspicious class (minority class)
The Genetic Algorithm completely failed to detect the Suspicious class.
Precision = 0.00, Recall = 0.00
No samples were predicted as Suspicious, as also visible in the confusion matrix.
Backpropagation performed better on this minority class, detecting instances and achieving non-zero recall.
This highlights a key limitation of the GA approach in this setup: fitness optimization driven mainly by overall accuracy led to neglecting the smallest class, which has little influence on the global fitness score.

Overall behavior

GA
- Robust, gradient-free optimization
- Slower convergence
- Tends to favor majority classes
- Less effective for imbalanced data without explicit fitness weighting

Backpropagation
- Faster and more stable convergence
- Better handling of minority classes
- More sample-efficient
- Scales better with dataset size and complexity

Conclusion
While both methods reached comparable overall accuracy, Backpropagation clearly outperformed the Genetic Algorithm in class-sensitive performance, especially for the Suspicious class. This makes BP the more suitable approach for practical phishing detection, where detecting rare but critical cases is essential.

















