# Does calibration matter?

**yechenzhi1** *Tue Jul 02 2024 19:06:56 GMT+0900 (日本標準時)* (3 votes)

Hello everyone,

As VALENTIN WERNER mentioned in a [previous discussion](https://www.kaggle.com/code/valentinwerner/log-loss-what-are-good-scores/notebook), good calibration can greatly enhance log loss scores. Despite experimenting with various calibration techniques, such as temperature adjustments and training a binary classifier for hard examples, I haven't achieved satisfactory results. I've been pondering this issue for a while. Should I perhaps shift my focus to other strategies, like ensemble methods or exploring newer models? Thanks in advance!



---

 # Comments from other users

> ## James Day
> 
> I haven't had any success trying to make my predictions better calibrated as a post-processing step either. Platt scaling, isotonic regression, and model stacking all seem to do more harm than good.
> 
> A while ago ChatGPT suggested I investigate how well calibrated my predictions are by calculating "Expected Calibration Error" as an additional cross-validation metric and generating "reliability diagrams". My code for doing that and sample results for my best ensemble (0.899 LB) are included below. It seems the confidence values are really well correlated with the probability of the top guess being correct, so there's not much that post-processing logic can do to help. Perhaps my models are slightly biased towards being a little under confident, but my best attempts at correcting for that at inference time score within 0.001 (CV) of just using the raw predictions. Perhaps if the underlying models were weaker the post-processing would be more beneficial.
> 
> ```
> def compute_ece(predictions, labels, num_bins=25):
>     bin_boundaries = np.linspace(0, 1, num_bins + 1)
>     ece = 0.0
>     total_samples = len(labels)
> 
>     confidences = []
>     accuracies = []
> 
>     for bin_lower, bin_upper in zip(bin_boundaries[:-1], bin_boundaries[1:]):
>         bin_indices = np.where((predictions >= bin_lower) & (predictions < bin_upper))[0]
>         if len(bin_indices) == 0:
>             continue
> 
>         bin_confidence = predictions[bin_indices].max(axis=1).mean()
>         bin_accuracy = (labels[bin_indices] == predictions[bin_indices].argmax(axis=1)).mean()
> 
>         bin_size = len(bin_indices)
>         ece += (bin_size / total_samples) * np.abs(bin_confidence - bin_accuracy)
> 
>         confidences.append(bin_confidence)
>         accuracies.append(bin_accuracy)
> 
>     return ece, confidences, accuracies
> 
> ece, confidences, accuracies = compute_ece(all_predictions, np.array(labels))
> print(f'Expected Calibration Error (ECE): {ece:.4f}')
> 
> from matplotlib import pyplot as plt
> 
> plt.plot([0, 1], [0, 1], linestyle='--')
> plt.scatter(confidences, accuracies, marker='o')
> plt.xlabel('Confidence')
> plt.ylabel('Accuracy')
> plt.title('Reliability Diagram')
> plt.show()
> 
> ```
> 
> 
> 
> > ## Yu Chengzhi
> > 
> > Thank you for sharing! How can I ensemble different methods? Is it just the mean of probabilities from various models?
> > 
> > 
> > 
> > > ## yechenzhi1Topic Author
> > > 
> > > You can adjust the weight of each model's probability, for example, preds = 0.8 * model_a_preds + 0.2 * model_b_preds.
> > > 
> > > 
> > > 
> > ## yechenzhi1Topic Author
> > 
> > Thanks for your reply! I guess I will focus on the training process or try some new ideas.
> > 
> > 
> > 


---

> ## Valentin Werner
> 
> Your models are already minimizing their loss, so post processing predictions will give no good results from my experience. However, when trainings transformers, parameters such as label smoothing may help to achieve better calibration (as the model is basically asked to predict 0.9 instead of 1.0 with an alpha of 0.1 etc.) - However, in general the data is confusing that this is one of the few challenges where my models basically never predict > 0.85 because it is so hard to be that confident.
> 
> When I wrote the discussion and linked notebook, I assumed that models would heavily overfit and strongly favour some classes, which does not seem to be the case.
> 
> Calibration definetly does matter, but it should probably be something you do during the training, rather than afterwards.
> 
> 
> 


---

