All code can be found on [github](https://github.com/AlexisWu-01/EMG-rock-paper-scissor)
# Result
## KNN
### Train (Cross Validation)
- Accuracy: 0.42
- F1 Score: [0.46 0.52 0.26]
- Confusion Matrix: ![knn train](https://github.com/AlexisWu-01/EMG-rock-paper-scissor/blob/main/result_plots/mav%7Cwl%7Cvar%7Czc_KNN_train.png?raw=True)

### Test
- Accuracy: 0.58
- F1 Score: [0.58 0.69 0.5]
- Confusion Matrix: ![knn test](https://github.com/AlexisWu-01/EMG-rock-paper-scissor/blob/main/result_plots/mav%7Cwl%7Cvar%7Czc_KNN_test.png?raw=True)

## SVM
### Train (Cross Validation)
- Accuracy: 0.44
- F1 Score: [0.43 0.54 0.31]
- Confusion Matrix: ![svm train](https://github.com/AlexisWu-01/EMG-rock-paper-scissor/blob/main/result_plots/mav%7Cwl%7Cvar%7Czc_SVM_train.png?raw=True)

### Test
- Accuracy: 0.63
- F1 Score: [0.67 0.67 0.53]
- Confusion Matrix: ![svm test](https://github.com/AlexisWu-01/EMG-rock-paper-scissor/blob/main/result_plots/mav%7Cwl%7Cvar%7Czc_SVM_test.png?raw=True)


# Improvement Efforts
## Adding New Features
I introduced frequency domain features which is the median frequency.Median Frequency is the frequency below which 50% of the total power is contained.  
## Multiple Models
I used KNN (clustering) and SVM (classification) to see if there is any difference in performance.
Spectrogram processing failed dramatically this time.
## Parameter Sweep on Models 
I used GridSearchCV to find the best parameters for each model.

# Future Work
1. Better data processing: From the plot I saw even with the same gesture, the data is not consistent in peak time and amplitude. I think onset detection should be really helpful here but I have not had time to find a general threshold that works well. 
2. More features: I think there are still a lot of features that can be extracted from the data. For example, the number of peaks, the time between peaks, the amplitude of the peaks, etc.

All current feature plots: ![feature plots](https://github.com/AlexisWu-01/EMG-rock-paper-scissor/blob/main/feature_plots/all.png?raw=True)

| Feature Name | Mathematical Expression | Definition |
| --- | --- | --- | --- |
|Root Mean Square|$$RMS = \sqrt{\frac{1}{N}\sum_{i=1}^Nx_i^2}$$ |Calculates the signal's amplitude, reflecting muscle strength.|
|Median Frequency| N/A, Welch method applied with scipy. | It computes the power spectral density and then find the frequency at which the cumulative power reaches half of the total power.|
|Peak Frequency| N/A, Welch method applied with scipy.| It is the frequency that corresponds to the maximum value in the power spectral density.|
|Hjorth Parameters| $$Activity = VAR = \frac{1}{N}\sum_{i=1}^{N}(x_i-\mu)^2$$ $$Mobility = \sqrt{\frac{VAR(dx)}{VAR(x)}}$$ $$Complexity=\frac{Mobility(dx)}{Mobility(x)}$$|**Mobility** is measure of the mean frequency or the rate of change iof the signal. It reflects the average frequency or the proportion of standard deviation of a signal's power spectrum. **Complexity** compares the mobility of the signal with the mobility of its first derivative. In essence, it indicates the similarity of the waveform of the signal to a pure sine wave, with lower values suggesting a more sine-like (less complex) signal. It is a measure of the change in frequency. A more complex signal, such as one with frequent shifts in frequency, will have a higher complexity value. |
|Band Power |$$BP = \int_{f_{low}}^{f_high}PSD(f)df$$ where PSD is power spectral density calculated with Welch method.| It integrates the power within the selected frequency band ($f_{low}$ and $f_{high})$|
