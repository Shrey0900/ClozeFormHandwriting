# ClozeFormHandwriting

## 📖 Overview  
**ClozeFormHandwriting** is a dataset of **handwritten cloze-form answers**, collected for research on handwriting recognition, OCR robustness, and automatic grading.  

The dataset contains both **image samples** (train/test) and their corresponding **log files** that map image filenames to ground-truth text.

---

## 📂 Dataset Structure  


- **Images**: stored as `.png` files  
  - Filenames are in the format `<ID>_<Word>.png`  
  - Example: `6_Control.png` → ground-truth word = `Control`  
- **Logs**: CSV-formatted text files that map filenames to text  
  - Example rows from `log_test.txt`:  
    ```
    file_name,text
    test/6_Control.png,Control
    test/6_Scientist.png,Scientist
    test/2_Synchronicity.png,Synchronicity
    ```

---

## 🧑‍🏫 Use Cases  
This dataset can be used for:  
- Training handwriting recognition models  
- Benchmarking OCR methods on cloze-form handwriting  
- Evaluating legibility and robustness of automated grading systems  
- Research in low-resource handwriting recognition  

---

## ⚙️ Usage  

### Clone the repository
```bash
git clone https://github.com/Shrey0900/ClozeFormHandwriting.git
cd ClozeFormHandwriting/data
```

## Load images with labels in Python
```python
import pandas as pd
from PIL import Image
from pathlib import Path

root = Path("data")
log = pd.read_csv(root / "log_test.txt")   # or "log_train.txt"

for _, row in log.iterrows():
    img_path = root / row["file_name"]     # e.g., data/test/6_Control.png
    label = row["text"]
    img = Image.open(img_path)
    print(img_path, "->", label)

    img = Image.open(os.path.join("..", img_path))
    print(img_path, "->", label)
```


