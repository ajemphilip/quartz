Date : 2024-12-01

# Tasks : Raspberry Pi Zero 2 W

# Goals
-Create more convenient speech-to-text and text-to-speech systems
-Test Raspberry Pi Zero 2 W

# Description
Raspberry PI Zero 2 W offers significantly greater computational power then ESP32. Because of that the proposal will test how well Raspberry PI Zero 2 W will perform with ChatGPT and Whispers voice and prompt service tasks. The proposal will take on the code created by ChatGPT to understand more about its rapid prototyping assistance and understanding of the device. 

# Prototyping
Two prototypes were created to understand how well Raspberry PI performs the tasks related to ChatGPT connection 
## Text-to-Speech
Speech to text was formed in the manner to vocalize the prompts to the ChatGPT prompts. The setup allows the user to type on the keyboard to ask ChatGPT any question and the answer will be via sound.
```
import openai
import os
from pydub import AudioSegment
from pydub.playback import play

# Set OpenAI API Key
api_key = "APIKEY"

# Initialize OpenAI client
client = openai.OpenAI(api_key=api_key)

# Store chat history
chat_history = [
    {"role": "system", "content": "You are a helpful assistant. Keep responses short."}
]

# Function to get a fast GPT-4 response (with memory)
def chat_with_gpt(prompt):
    # Add user message to chat history
    chat_history.append({"role": "user", "content": prompt})

    # Get GPT response
    response = client.chat.completions.create(
        model="gpt-4-turbo",
        messages=chat_history,  # Send full chat history
        max_tokens=60,
        temperature=0.3,
        stream=True
    )

    final_response = ""
    print("🤖 GPT-4: ", end="", flush=True)

    for chunk in response:
        if chunk.choices[0].delta.content:
            text_chunk = chunk.choices[0].delta.content
            print(text_chunk, end="", flush=True)  # Print response in real-time
            final_response += text_chunk

    print("\n")  # New line after response

    # Save GPT response to chat history
    chat_history.append({"role": "assistant", "content": final_response})

    return final_response.strip()

# Function to generate speech from GPT response
def text_to_speech(text, filename="output.mp3"):
    response = client.audio.speech.create(
        model="tts-1",
        voice="nova",  # "nova" is the fastest voice
        input=text
    )

    # Save the generated speech
    with open(filename, "wb") as f:
        f.write(response.content)

    # Play the audio (normal speed)
    audio = AudioSegment.from_mp3(filename)
    play(audio)

# Main Loop (GPT-4 remembers conversation + TTS speaks response)
def main():
    while True:
        user_input = input("📝 Enter your message (or type 'exit' to quit): ")
        if user_input.lower() == "exit":
            break

        print("⚡ Generating GPT-4 response...")
        gpt_response = chat_with_gpt(user_input)

        print("🔊 Generating speech...")
        text_to_speech(gpt_response)

if __name__ == "__main__":
    main()
```
## Speech-to-Text
Speech to text uses microphone to record audio and transfer it to Whispers API to decode the voice recorded in the file.
```
import openai
import sounddevice as sd
import numpy as np
import wave

# OpenAI API Key
api_key = "APIKEY"
client = openai.OpenAI(api_key=api_key)

# Audio settings
SAMPLE_RATE = 44100
CHANNELS = 1
DURATION = 5  # Seconds of audio to record

# Function to record audio from Blue Yeti
def record_audio(filename="input.wav"):
    print("🎤 Listening... Speak now!")
    recording = sd.rec(int(SAMPLE_RATE * DURATION), samplerate=SAMPLE_RATE, channels=CHANNELS, dtype=np.int16)
    sd.wait()  # Wait until recording is done

    wavefile = wave.open(filename, "wb")
    wavefile.setnchannels(CHANNELS)
    wavefile.setsampwidth(2)
    wavefile.setframerate(SAMPLE_RATE)
    wavefile.writeframes(recording.tobytes())
    wavefile.close()

    print("✅ Recording saved!")

# Function to transcribe audio using Whisper
def transcribe_audio(filename="input.wav"):
    with open(filename, "rb") as audio_file:
        transcript = client.audio.transcriptions.create(
            model="whisper-1",
            file=audio_file
        )
    return transcript.text.strip()

# Main loop
def main():
    while True:
        input("🔴 Press Enter to start recording... (or type 'exit' to quit): ")
        record_audio()
        transcribed_text = transcribe_audio()
        print(f"📝 You said: {transcribed_text}")

if __name__ == "__main__":
    main()
```
# Creating
To operate Raspberry PI microcomputer the SD card needs to be formatted and Linux operation system has to be flashed to the SD card. After insertion the device is usable. Because of one USB port it was necessary to purchase USB extender and external sound card with microphone and speakers. The parts were connected together and prototypes were run on the device.

# Cost
| Item                   | Quantity | Unit Price (CAD) | Total (CAD) |
|------------------------|----------|------------------|-------------|
| Raspberry Pi Zero 2 W  | 1        | 22.72            | 22.72       |
# Critical Reflection
## Raspberry PI Zero 2 W
Rasberry PI Zero 2 W definitely offers exceptionally better experience when it comes to computational power. ChatGPT and Whispers API connection were robust and fast. MP3 files exchange and processing did not post any difficulty for the microcontroller. The API connection on the other hand, despite it was significantly better then on ESP32, still had some latency. The longer recordings took around 2 minutes to process, especially during speech to text however the text-to-speech was taking maximum one minute per 2-3 medium length sentences. Despite device affordability it also adds additional cost while ESP32 wasn't replaced but simple connected to Raspberry PI. In this way the connection testing between two computers can be tested.
## ChatGPT
ChatGPT definitely helped a lot with the coding tasks making it robust tool to form assistive devices according to user needs. With Rasberry PI, ChatGPT understood the task quite well offering only couple iteration of errors related to indents in python and some obsolete coding methods that were fixed after pointing the error out. Despite those errors, when ChatGPT receives the error messages it modifies the code accordingly, making it working and usable. 