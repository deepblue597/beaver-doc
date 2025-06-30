# Features

Features are the elements (fields) of the data. Four categories of features are defined:

- **keep_features:** The features you want to retain from the data.
- **drop_features:** The features you want to discard from the data.
- **generated_features:** Features created by composing existing features. These are defined as functions, e.g.  
  `generated_feature = keep_feature1 * keep_feature2 - keep_feature3`
- **target_feature:** The target feature of your data.

All of the above categories are optional. If the user does not specify either `keep_features` or `generated_features`, Beaver will retain all features from the
