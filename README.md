# SNAP
SNAP – Speech Navigation and Autonomous Pathfinding. Language Model for Human Machine Interface on an AV 

Below are the high-level goals to meet:

- [ ] Receive audio input (speech) and Convert it to text.
 - Look into following ASR: (Will have to quantize the larger models) 
    - [ ]  Whisper-base
    - [ ]  Whisper-large 
    - [ ]  Vosk
    - [ ]  DeepSpeech

- [ ] Interpret the user’s text command to figure out:
  - [ ] The type of task (e.g. “drive”)
  - [ ] Which destinations (out of possible n total) should be activated (e.g. 10001011 for n = 8).
  - Try the following: (Will have to quantize the models) 
    - [ ] T5-base
    - [ ] T5-small
    - [ ] GPT-Neo 1.3B
    - [ ] GPT-Neo 2.7
    - [ ] Llama 2 7B
    - [ ] Falcon 7B
  - Prompt Engineering for binary string output of a fixed length with test examples
  - Look into LoRA or QLoRA for specefic output finetuning

Potential pipeline:

- Capture whole speech command 
- Detect End of Speech using VAD or time thresholds
- Transcribe using ASR loaded into the mem (~~streaming~~ or chunk-based input)
- Once you have the text, unload ASR from memory and load in the NLP model
- Run inference on transcription. Task type and Locations.
- Have a structured output in the form of a predefined string, instructed using prompt engineering
- Send to the AV stack over CAN

#### Note To Self: 
- Does the NPU have specialized runtime like ONNX or TensorRT equivalent?
- Look into hardware acceleration on 2019 ARM Processors.
- Look into processors support for support dynamic sequence lengths.
