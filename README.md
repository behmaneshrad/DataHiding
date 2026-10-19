# DataHiding — LSB image steganography

Hide a UTF-8 text message inside an image, and read it back, using **least-significant-bit (LSB)** embedding. Two Jupyter notebooks, Python + OpenCV.

## How it works
- The message is encoded as UTF-8 and prefixed with a **32-bit big-endian length header**.
- Every bit is written into the least significant bit of one colour channel (B, G, R) of consecutive pixels — 3 bits per pixel, so capacity is `height × width × 3` bits (the code raises an error if the message does not fit).
- Extraction reads the 4-byte header first, checks that the length fits the image, then reads that many bytes and decodes them as UTF-8.
- Save the result as **PNG** (lossless). JPEG compression destroys LSB data.

## Files
```
LSB/Image-DataHiding/
  Embed.ipynb          encode_lsb(image_path, secret_text, output_path)
  Extract.ipynb        decode_lsb(image_path)
  input.png            sample cover image
  encoded_image.png    sample output
```

## Run
```bash
pip install opencv-python numpy jupyter
jupyter notebook LSB/Image-DataHiding/
```

## Limits (be honest about what this is)
LSB embedding is a teaching example. It is **not encryption** and is easy to detect with statistical steganalysis; encrypt the message first if it is sensitive.
