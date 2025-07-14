## Tesseract OCR

---

### What is Tesseract?

* **Tesseract** is an open-source **OCR (Optical Character Recognition)** engine developed by HP and currently maintained by **Google**.
* It converts **images of text** into **machine-encoded text**.
* Supports over **100 languages** and can be trained for other languages too.

---

### Architecture and Workflow

| Stage                          | Description                                                        |
| ------------------------------ | ------------------------------------------------------------------ |
| **1. Input**                   | Accepts images (TIFF, JPEG, PNG, etc.) or PDFs (via add-ons)       |
| **2. Image Preprocessing**     | Thresholding, noise removal, binarization (optional, user-managed) |
| **3. Page Layout Analysis**    | Detects orientation, columns, blocks, lines, and words             |
| **4. Line and Word Detection** | Performs segmentation to extract lines and words                   |
| **5. Character Recognition**   | Uses **LSTM-based deep learning** (since v4.0)                     |
| **6. Output**                  | Produces plain text, hOCR, ALTO XML, TSV, PDF, etc.                |

---

### Engine Modes (OEM)

| Mode | Description               |
| ---- | ------------------------- |
| 0    | Legacy only               |
| 1    | Neural nets LSTM only     |
| 2    | Legacy + LSTM (combined)  |
| 3    | Default: Use best of both |

---

### Output Formats

* `txt`: Plain text
* `tsv`: Tab-separated data with location info
* `pdf`: Image over text PDF
* `hocr`: HTML-based OCR output
* `alto`: XML format used in libraries and archives

---

### Input Image Types

* Supported: TIFF (preferred), PNG, JPG, BMP
* Preprocessing using OpenCV or PIL often required

---

### Key Features

* **Multi-language support**
* **Script and orientation detection**
* **Custom training**
* **Batch OCR using command-line**
* **Text detection coordinates**
* **PDF generation with text layer**

---

### Usage Options

#### CLI:

```bash
tesseract input.png output -l eng --oem 3 --psm 6
```

#### Python (with pytesseract):

```python
import pytesseract
from PIL import Image

text = pytesseract.image_to_string(Image.open('image.png'), lang='eng')
```

---

### Page Segmentation Modes (PSM)

| Mode | Description                           |
| ---- | ------------------------------------- |
| 0    | Orientation and script detection only |
| 3    | Fully automatic page segmentation     |
| 6    | Assume a single uniform block of text |
| 11   | Sparse text with OSD                  |
| 13   | Raw line (no layout analysis)         |

---

### Training Tesseract (Custom OCR)

* **Purpose**: Extend Tesseract to recognize new fonts, handwriting, or scripts
* **Steps**:

  * Prepare box/text files
  * Generate `.traineddata`
  * Use `text2image`, `lstmeval`, `combine_tessdata`, etc.

---

### Tesseract Versions

| Version        | Highlights                                                            |
| -------------- | --------------------------------------------------------------------- |
| 3.x            | Legacy engine (no deep learning)                                      |
| 4.x            | Added LSTM-based recognition                                          |
| 5.x            | Enhanced accuracy, support for newer formats and faster LSTM training |
| 6.x (Beta/Dev) | Improved layout analysis and model tuning                             |

---

### Limitations

* Struggles with:

  * Complex layouts (tables, multi-column)
  * Handwriting (unless trained)
  * Skewed or low-resolution images
* Requires manual preprocessing for best accuracy

---

### Integrations and Wrappers

| Tool                 | Use                        |
| -------------------- | -------------------------- |
| `pytesseract`        | Python wrapper             |
| `Tess4J`             | Java wrapper               |
| `tesserocr`          | Fast C++-Python binding    |
| `OCRopus` / `kraken` | Higher-level OCR pipelines |

---

### Best Practices

* **Preprocess images** (denoise, binarize, resize)
* Choose correct **PSM and OEM** settings
* Use **language packs** wisely
* Use **bounding boxes** for layout-specific OCR
* For multi-language text, specify multiple langs: `-l eng+hin`

---
