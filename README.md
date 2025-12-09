# Cloze-Form Handwriting Dataset (Bad-Handwriting Benchmark)

This dataset contains handwritten **single-word responses** collected from real classroom settings, where students answered cloze-form questions by writing one word per blank. Each image is a cropped handwritten response paired with its ground-truth transcription.

The handwriting exhibits substantial variation in **legibility**, **stroke quality**, **spacing**, and **letter formation**, making it a challenging benchmark for OCR systems and a realistic testbed for studying automated grading robustness.

---

## Dataset Contents (Current Release)

The full benchmark originally consists of **5,000 handwritten responses**, but these fall into two categories:

- **3,000 correct responses** — the student wrote the intended target word.  
- **2,000 incorrect responses** — the student wrote a wrong or unrelated word.

### Current Release

**This public release includes only the 3,000 correct responses.**

These samples are suitable for **word-level OCR training and evaluation** because each image aligns cleanly with a single target word. The remaining 2,000 responses correspond to incorrect answers and are *not* included in this release, as they require a different evaluation protocol (grading/semantic correctness) and are not directly compatible with standard OCR objectives.

A small number of visually duplicated or low-quality crops were removed during preprocessing to ensure data consistency.

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
## 📊 Citation
If you use this dataset in your research, please cite:

```bibtex
@inproceedings{chandola2025far,
  title={How far are we from Automatic Grading of Handwritten Cloze Form Questions?},
  author={Chandola, Shrey and Ravikiran, Manikandan and Saluja, Rohit},
  booktitle={International Conference on Artificial Intelligence in Education},
  pages={336--343},
  year={2025},
  organization={Springer}
}
```


