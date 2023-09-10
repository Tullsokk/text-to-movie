# text-to-movie
A google colab notebook for generating short films from a single prompt 

This is an open project I started to see how hard it would be to cobble together some code that can generate a full movie from a single prompt. Not that hard, as it turns out, when GPT can help with the coding. You are welcome to contribute to the project. A lot of the code is written with the help of GPT, and has just been thrown together to get the basics working. Is is quite messy, not very efficient, but in time and with some help, I hope to get it in good shape. 

In this notebook, you can give a movie title and a description. You need api tokens for openAI and elevenlabs. A paid google colab will also help with more and faster GPU compute. 

In short, the code does the following:
- GTP is then used to write a movie script. The system prompt is primed to give a structured response in a defined json format that inculdes a scene description, music description and dialogue. If the response is not valid json, GPT is asked to try again.
- All characters are extracted. A list of all availavle voices from elevenlabs, including age, gender and description of the voice is sent to GPT along with the list of characters, with instruction to return a suitable casting. It tends to cast Han Solo as a middle aged war veteran, Princess Leia is a calm young lady, C3PO gets a british accents, etc.
- The program then loops throug every scene description and creates a 5 second video clip for each line of text. E.g. "The millenium falcon is flying through space"
- For each line of dialouge, the elevenlabs api is used to create the sound. A video of corresponding length is created with the promt "midshot of [character] talking".
- I have had problems with some prompts just returning a noisy pattern, e.g. zebra stripes. To get around this, the code uses openCV to check the average laplacian value of the clip. If there is too much noise, it tries again, to the set max number of retries.
- A text to music model is used to generate the soundtrack
- Subtitles are added as well as captions for the scene description/prompt. It can sometimes be hard to recognize what the video model tried to create, this text helps interpret what is going on.
- All the clips are automatically edited together
- Final video can be downloaded locally or saved to your google drive

The results are, unsurprisingly, quite janky, but entertaining notetheless. Much like the early days of text to imgage with dalle mini/craiyon. 

Some of the improvements I hope to see are:
- More consistent videos
- Fix multi line captions and subtitles
- Add movie poster
- Get rid of issues with some clips only consisting of noise
- Improved video model
- Upscaling and increasing frame rate by interpolating frames
- Better music
- 16:9 video format
- Fix issues with stuttering last dialouge in final scene
