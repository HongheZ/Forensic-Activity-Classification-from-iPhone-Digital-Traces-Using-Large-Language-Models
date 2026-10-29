# Binary experiment (171 activity pairs)

This experiment has no training files of its own.

- **Model:** the binary experiment reuses the models fine-tuned for the 19-class experiment, one per fold. The training files are in `../19_classes/train/`.
- **Test prompts:** these are not stored as files. The scoring script builds them from the 19-class test files in `../19_classes/test/`. For each test sample and each of the 18 other activities, it makes one prompt that compares the sample's true activity with that activity. Over the 12 folds this gives 9,374 × 18 = 168,732 prompts.
- **How a binary prompt differs from the 19-class prompt:** the rest of the prompt stays word for word the same. Two parts change:
  1. The 19-line letter legend (`A = bus` ... `S = walking`) is cut down to the two lines of the pair, still in letter order.
  2. This sentence is added above the answer line:
     `The activity is one of the two listed below; you must choose one of them.`

  Example for the pair stair_up / walking:
  ```
  The activity is one of the two listed below; you must choose one of them.
  Answer with exactly one capital letter, the code of the activity:
  N = stair_up
  S = walking
  ```
- **Answer:** the letter with the higher next-token probability at the answer position.
