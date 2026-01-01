
# plain-sight

Can you help find my flag? I tried asking around but all I found was this poem


- Extraer imagen del pdf



```
mutool extract hiding_in_plain_sight.pdf

warning: ICC support is not available
extracting image-0004.png
extracting font-0035.ttf
extracting font-0039.ttf
extracting font-0043.ttf
extracting font-0047.ttf
extracting font-0051.ttf

```

- otra forma de extraer
```
pdfimages -all hiding_in_plain_sight.pdf flag.png

```

- abriendo la imagen esta la flag
```

bcactf{Now_yOU_s3e_mE}


bcactf{Now_y0U_s3e_mE}  ok
```


- con script

```bash
pip install --upgrade pymupdf

```


```python
import fitz  # PyMuPDF
import os

pdf_path = "hiding_in_plain_sight.pdf"  # Change to your PDF file
output_dir = "extracted_images"
os.makedirs(output_dir, exist_ok=True)

doc = fitz.open(pdf_path)

for page_index in range(len(doc)):
    page = doc[page_index]
    images = page.get_images(full=True)

    for img_index, img in enumerate(images):
        xref = img[0]
        base_image = doc.extract_image(xref)
        image_bytes = base_image["image"]
        image_ext = base_image["ext"]
        image_name = f"image_{page_index+1}_{img_index+1}.{image_ext}"
        image_path = os.path.join(output_dir, image_name)

        with open(image_path, "wb") as f:
            f.write(image_bytes)
        print(f"Saved: {image_path}")

```