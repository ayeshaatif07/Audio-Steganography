# Audio Steganography

Two Jupyter notebooks that explore hiding messages in audio: one **detects and decodes** a message hidden in the ultrasonic range of a sound file, and the other **embeds and extracts** a text message using the least significant bits (LSB) of the audio samples.

## Notebooks

### Exercise 3.1: Detecting a Hidden Ultrasonic Message

`Exercise 3.1.ipynb` analyses every WAV file in `audio_files/` to find the one that carries a hidden message.

1. Loads each file, converts it to mono and normalises it.
2. Computes the frequency spectrum with the FFT.
3. Measures how much of the signal's energy lies above 18 kHz (the ultrasonic ratio).
4. Plots the spectra and picks the file with the highest ultrasonic ratio as the most suspicious.
5. Demodulates the hidden message from a 19 kHz carrier with a 4 kHz low-pass filter.
6. Saves the recovered audio as `decoded_message.wav`.

In the saved run, `Ex3_sound4.wav` was identified as the suspicious file, with an ultrasonic ratio of about 0.159.

### Exercise 3.2: Enhanced LSB Audio Steganography

`Exercise 3.2.ipynb` hides a text message in `Ex3_sound5.wav` and then recovers it.

- Uses **2 bits per sample** for more capacity.
- Spreads the bits over **non-consecutive samples** (every 3rd sample) to make the change harder to detect.
- Stores the **message length** in a 32-bit header so the message can be extracted correctly.
- Writes the result to `Ex3_sound5_embedded.wav` and checks that the extracted message matches the original.

In the saved run, the 42-character message "It always seems impossible until it's done" was embedded by modifying about 0.045% of the samples and extracted back exactly.

## Project Structure

| File / folder | Purpose |
|---------------|---------|
| `Exercise 3.1.ipynb` | Ultrasonic analysis and message demodulation |
| `Exercise 3.2.ipynb` | LSB embedding and extraction |
| `audio_files/` | The input sounds (`Ex3_sound1.wav` to `Ex3_sound5.wav`) and the embedded output `Ex3_sound5_embedded.wav` |
| `decoded_message.wav` | The message recovered by Exercise 3.1 |

## Run Locally

You need Python 3 and Jupyter.

```bash
git clone https://github.com/ayeshaatif07/Audio-Steganography.git
cd Audio-Steganography
pip install numpy scipy matplotlib librosa jupyter
jupyter notebook
```

Then open a notebook and run the cells from top to bottom. Start Jupyter from the project folder, because the notebooks read the sounds from the relative path `audio_files/`.

## Author and Credits

- **Author:** Ayesha Atif
- **Coursework:** Intelligent Signal Processing (CM3065) – Midterm (Exercise 3)
- Built with Python, [NumPy](https://numpy.org/), [SciPy](https://scipy.org/), [librosa](https://librosa.org/) and [Matplotlib](https://matplotlib.org/).
