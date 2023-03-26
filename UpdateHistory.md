# Update History

## March 26 2026 UPDATE: Background execution and Hands Free control
This update is focused on making the assistant more viable in everyday life. 
 - You can now follow some instructions you can find at <span style="color:green"> BootJARVIS.pdf </span>. to run the main script automaitcally when the system boots;
 - There no more need to press Ctrl+C to deliver mic recordings to Wisper. Here hows *Hands Free* and *Summoning* work like:
    1. By default the assistant is at sleep. A python script will however run passively to listen for a special keyword to summon JARVIS. The function is hence ```PassiveListen```, you'll find it inside get_audio.py. It leverage the SpeechRecognition python package that is faster and more versatile than whisper but less accurate. 
    2. When the keyword (by default ```'elephant'```* ) is spoken, the assistant wakes up and the following audio is fed to Whisper. You'll need to summon the assistance only once, every time you begin a conversation.
    3. When a conversation begins, the assistant will listen, after you deliver a prompt some time will pass, **3 seconds** (```RESPONSE_TIME``` inside the ```record()``` function in get_audio.py ) before the audio is listened and transcribed by whisper. A conversation is closed when the user say a Closing Keyword (for now 'thanks'). This will trigger the chat saving and will put the assistant back to sleep, waiting for a awakening keyword. 
    4. In alternative, the system will go back to sleep automatically if **30 seconds** (variable ```SLEEP_DELAY``` inside the ```record()``` function in get_audio.py ) pass after the response is repoduced.
 - minor improvements:
    1. Adding the package pytts3x for text to speech when IBM is un-available (monthly usage expired);
    2. improved CLI outputs;
    3. improved descriptions;
<br>

(*) ```'elephant'``` was chosen as default keyword becaus it' uncommon and understandable. You can change it to 'Hey Jarvis' o 'Hey Siri' but you need to be sure the system catch what you are saying (SpeechRecognition is not that good with fancy names) maybe in future better ways to summon will be thought.



## March 13 2023 UPDATE: JARVIS VOICE IS HERE!
**How i did it**: I spent a huge amount of time on @CorentinJ github https://github.com/CorentinJ/Real-Time-Voice-Cloning which provides an interface to generate audio from text using a pretrained text-to-speech model. The GUI is pretty clever and I admire his work, however, using the model in a python script is not straight foward! I first edited the toolbox to save **embeddings**, which are the beginning of  the generation process,. They are the "voice ID" of the targeted people, expressed in terms of matrix. With this edit, I used the toolbox to generate Paul Bettany's voice embedding. <br>
Then, I wrote down a trimmed version of CorentinJ's toolbox, `JARVIS.py`. This version can load the embedding learned from Jarvis voice and do basic oprations like Synth and vocode upon request from any script. 

![toolbox](https://user-images.githubusercontent.com/49094051/224836993-ee7b4964-e518-46f4-85b1-b25f48f1a78c.PNG)
<p align="center"> Original Toolbox interface: you can see the embedding </p>