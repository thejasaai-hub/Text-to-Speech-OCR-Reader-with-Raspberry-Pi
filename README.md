# Text-to-Speech OCR Reader with Raspberry Pi

This project implements a text-to-speech reader using a Raspberry Pi, camera module, and a physical button. The program captures an image through the Raspberry Pi's camera, extracts text from the image using Optical Character Recognition (OCR), and converts the extracted text into speech using Google Text-to-Speech (gTTS). The entire process is triggered by a physical button press, making it a simple yet effective assistive tool.

## Features
- **Capture Image:** Automatically captures a frame from the camera when the button is pressed.
- **Text Recognition:** Uses Tesseract OCR to identify and extract text from the captured image.
- **Text-to-Speech Conversion:** Converts the detected text into speech using Google Text-to-Speech (gTTS).
- **Audio Playback:** Plays the generated speech using VLC media player.
- **Physical Button Control:** The entire process is initiated with a button press.

## How It Works
1. **Pytesseract Configuration:**  
   The script configures the `pytesseract` library to use the Tesseract OCR engine installed on the Raspberry Pi:
   ```python
   pytesseract.pytesseract.tesseract_cmd = '/usr/bin/tesseract'

2. **Text-to-Speech Function (texttospeech)**:
   This is the main function that performs the following tasks:

   **Video Frame Capture**:
    - Captures a frame from the Raspberry Pi's camera using OpenCV.
      
    **OCR Processing**:
    - Tesseract processes the frame to identify words. Bounding boxes and labels are drawn around detected text in the image.
      
    **Text Storage**:
    - The extracted text is saved in a file named String.txt.
      
    **Speech Generation**:
    - If the file contains text, it is converted to speech using the gTTS library and saved as an audio file (test.mp3).
      
    **Audio Playback**:
    - The speech file is played using VLC media player, and the program waits for the playback to complete.

3. **Button Control**:
   
   - A physical button connected to GPIO 16 (BUTTON_PIN) is used to trigger the text-to-speech function. The pin is set up with an internal pull-up resistor to default to a HIGH state.
     
   - When the button is pressed (LOW state), the program calls the texttospeech function.

5. **Main Loop**:
   
    The program continuously monitors the button press. On pressing the button:
   
    - Captures an image.
    - Extracts text from the image.
    - Converts the text to speech and plays the audio.

## Hardware Requirements

- Raspberry Pi (any model with GPIO support)
- Camera module compatible with the Raspberry Pi
- Push-button
- Resistors (for the button, optional if internal pull-up is used)
- Speaker or headphones (for audio output)

## Software Requirements

- Python 3
- Libraries:
    - RPi.GPIO (for GPIO handling)
    - cv2 (OpenCV for video capture and image processing)
    - pytesseract (OCR using Tesseract)
    - gTTS (Google Text-to-Speech for audio generation)
    - vlc (for audio playback)
- Tesseract OCR installed on the Raspberry Pi
- VLC media player installed on the Raspberry Pi

## How to Run

1. **Install Required Libraries**:

     sudo apt-get update
   
     sudo apt-get install tesseract-ocr vlc python3-opencv
   
     pip3 install gTTS python-vlc

3. **Connect the Hardware:**

   - Attach the camera module to the Raspberry Pi.
   - Connect the button to GPIO 16 and GND (use a pull-up resistor if needed).

4. **Run the Program**:

  - Save the script as text_to_speech_ocr.py.
  - Run the script:
      python3 text_to_speech_ocr.py

4. **Trigger the Functionality**:

  - Press the button to capture an image, extract text, and hear the text converted to speech.

## Application Use Cases

**Assistive Tool for Visually Impaired**:
  Helps visually impaired individuals by reading out text from documents or signs.
  
**Educational Purposes**:
  Demonstrates how OCR and text-to-speech can be integrated into real-world projects.
  
**Portable Text Reader**:
  Can be used to build a portable OCR-based text reader for various environments.

## Key Functions

  texttospeech()
  
    1. Captures a frame using the Raspberry Pi's camera.
    
    2. Uses Tesseract OCR to extract text from the frame.
    
    3. Saves the text into String.txt.
    
    4. Converts the text to speech using gTTS.
    
    5. Plays the generated audio using VLC media player.

## GPIO Setup

  **Button Pin**: GPIO 16
  
  **Mode**: Internal pull-up resistor is used to ensure the pin defaults to HIGH (not pressed).
            When the button is pressed, the pin goes LOW, triggering the texttospeech() function.

## Handling Interruptions

  The program uses a try-except block:
  
  **Main loop**: Continuously monitors for button presses.
  
  **Keyboard Interrupt (Ctrl+C)**: Ensures GPIO pins are cleaned up properly using:
    GPIO.cleanup()

## Limitations

  - Requires good lighting for accurate text recognition.
    
  - May not work well with heavily styled or handwritten fonts.

## Future Enhancements

  - Add support for multiple languages in OCR and speech.
    
  - Implement real-time video stream OCR.
    
  - Improve text extraction accuracy with advanced preprocessing techniques.


