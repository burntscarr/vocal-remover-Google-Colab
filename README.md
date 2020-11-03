# vocal-remover
Burnt's version of vocal-remover for Google Colab

This is a tool to remove vocals from a song, and to also create a version that is the opposite of the created track with inversion.

The files you need to import to Google Colab will not be hosted on GitHub.
Find those at https://mega.nz/file/Mbx3TLIZ#o6yEif1etlOT7KkEpgoSX7JUalzztrXNO2OrQzjxh9M and upload the vocal-remover folder to your GDrive

Let's begin!

# SETUP:
First you'll want to go to https://github.com/burntscarr/vocal-remover/blob/main/vocal_remover_burnt.ipynb and click the button up top to open in Google Colab. (This links you to https://colab.research.google.com/github/burntscarr/vocal-remover/blob/main/vocal_remover_burnt.ipynb)

Next, you'll want to press the Copy To Drive button up top under the menu (File Edit View Insert Runtime Tools Help).

Now you have a copy in your drive that is open. You can close the other tab that came from GitHub.

Up at the top right under "Comment" should be either "Connect" or a menu with the RAM and CPU data. Click the arrow on the right of that. Now click Manage Sessions and terminate any running sessions.

# FILE SETUP
Okay to begin, I assume you've got a song you want to remove the vocals for. You need to get that song into your Google Drive in the main/default folder. Once it's in there you can continue.

Now rename the file to something simple. It can be very troubling to have to change lots of code to match a long filename. I suggest the first word of the song title in lowercase. For example, Queen - We Are The Champions.flac becomes we.flac

# INITIAL CODE EDITING
Now you get to code! Well, a little at least. In Steps 1-4 you don't need to edit anything. Step 5.1 5.2 and 5.3 all require you to change the [FILE] and [EXT] parts.

Let's go through that step by step with the same example song, we.flac

STEP 5.1 In the line containing !python multi-genre-secondgen.py --input "/content/drive/My Drive/[FILE].[EXT]" --gpu 0 Change [FILE] to we !python multi-genre-secondgen.py --input "/content/drive/My Drive/we.[EXT]" --gpu 0 and then change [EXT] to the extension for our song which is flac. !python multi-genre-secondgen.py --input "/content/drive/My Drive/we.flac" --gpu 0 and in the line containing !mv [FILE]_Vocals.wav [FILE]_Vocals_MG.wav again change [FILE] to your song name (we) !mv we_Vocals.wav we_Vocals_MG.wav Don't change the .wav part, the program automatically converts your audio to wav we'll talk about converting back later. and in the next line !mv [FILE]_Instruments.wav [FILE]_Instruments_MG.wav again change [FILE] to your song name (we) !mv we_Instruments.wav we_Instruments_MG.wav

The same applies for STEP 5.2 and STEP 5.3 except multi-genre-secondgen.py is a different file, which you don't need to edit. 5.2: !python multi-genre-np.py --input "/content/drive/My Drive/[FILE].[EXT]" --gpu 0 %cd "/content/drive/My Drive/vocal-remover/" !mv [FILE]_Vocals.wav [FILE]_Vocals_NP.wav !mv [FILE]_Instruments.wav [FILE]_Instruments_NP.wav

becomes

!python multi-genre-np.py --input "/content/drive/My Drive/we.flac" --gpu 0 %cd "/content/drive/My Drive/vocal-remover/" !mv we_Vocals.wav we_Vocals_NP.wav !mv we_Instruments.wav we_Instruments_NP.wav

and it's about the same for 5.3 so I'll skip that.

# Time To Start!
Alright finally! Press the play buttons in order, there's notes in the colab project but I'll explain here anyway:

STEP 1 Click Play, click the Link it gives you, sign in, Allow, copy code, paste in colab step 1, press enter, wait until it says done.

STEP 2 Click Play, wait until it says done.

STEP 3 Click Play, wait until all packages are installed and it says done.

STEP 4 Click Play, wait until it says done.

STEP 5.1 Since you edited the code earlier, you should be able to just press play and wait until it says done.

STEP 5.2 Since you edited the code earlier, you should be able to just press play and wait until it says done.

STEP 5.3 Since you edited the code earlier, you should be able to just press play and wait until it says done.

STEP 6 This is optional, you can run the stacked model on one of the Instrumentals generated. You'll need to change [FILE] to your filename (in our earlier example it was "we") and change [_XX] to _MG _NP or _HP before pressing play. I couldn't have you edit this code earlier because you need to choose which one you want to use, based on which model(s) you ran (Steps 5.1 5.2 & 5.3). 5.1 is MG, 5.2 is NP, and 5.3 is HP. The line of code you're editing should look like this at first: !python inferences.py --input "/content/drive/My Drive/vocal-remover/[FILE]_Instruments[_XX].wav" --gpu 0 and if you choose to use MG from step 5.1 it should look like this when you're done (using same example): !python inferences.py --input "/content/drive/My Drive/vocal-remover/we_Instruments_MG.wav" --gpu 0 then you can press play, it will generate files that have _Instruments_Instruments and _Instruments_Vocals on them.

STEP 7.1 This is also optional, you can save space by converting the WAV files that the project generates to FLAC which is still lossless. BASIC - If you're okay with converting ALL of the WAV files in your vocal-remover folder then you can press play with no code editing required. ADVANCED - If there's a specific file, you'll need to change the *.wav to the name of the wav you want to convert.

STEP 7.2 DO NOT run this command before running 7.1 - Optional also, removes the remaining WAV files that were converted to your Google Drive trash. BASIC - If you're okay with removing ALL of the WAV files in your vocal-remover folder, then you can press play with no code editing required. ADVANCED - If you chose the advanced method for 7.1, change the *.wav to the same file name to only delete that file.
