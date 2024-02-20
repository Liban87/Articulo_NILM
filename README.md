# Non Intrusive Load Monitoring Models Training for Individual Household Energy consumption Dataset

[Download the dataset here](https://archive.ics.uci.edu/dataset/235/individual+household+electric+power+consumption)

## Dataset loading and preprocessing
1. During data loading the dates and times are parsed on an unique column using parse_dates parameter on read_csv function, the ? data is replaced with nan.

2. nan values are replaced by the corresponding column median.

3. 2 new features are created from the previous ones, the global apparent power and power factor.

4. Asign cathegorical tag tothe samples of the dataset. this is necessary beacuse subsequent steps involve the training of clasification models that identifies the kind of energy consumption corresponding to a global electrical measurements sample. Namely:
    * no consumption on any zone (___tag 0___)
    * zone 2 has the main consumption (___tag 1___)
    * zone 3 has the main consumption (___tag 2___)
    * the two zones has the same consumption (___tag 3___)
    
    zone 2 Corresponds to the Laundry room, containing washing machine, tumble dryer a refrigerator and a light.
    
    zone 3 corresponds to an electric water heater and an air conditioner.

Notes:
* ___could be interesting to retag the dataset having a value range for the zones to be considered equal___
* ___Could be necessary to create more classes in order to add relevance to the classification task___

## Split and Balance the Dataset
Due to the considerable high diferences in the quantity of samples for the various categories, it is necessary to make the training subset more balanced by means of undersampling the mayority classes. This is achieved using two undersampling steps first with EditedNearestNeighbours and then with TomekLinks.

Notes:
* ___Is needed to check performance using another undersampling or oversampling methods such as ADASYN or random___