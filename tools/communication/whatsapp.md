

## backup


[github | whatsapp database extractor](https://github.com/YuvrajRaghuvanshiS/WhatsApp-Key-Database-Extractor)

[whatsapp viewer](https://github.com/andreas-mausch/whatsapp-viewer/tree/v1.15)

[reddit thread copy - post](https://www.reddit.com/r/DataHoarder/comments/a7c0yq/comment/j6egul6/?utm_source=share&utm_medium=web2x&context=3)

Hi everyone, I managed to pull this off (for reference, it's January 29th 2023) and so I wanted to give someone as desperate as I was a guide. **No root required!**

What I had:

- WhatsApp Version **2.23.1.76**
    
- Samsung Galaxy **S22 Ultra**
    
- Windows PC
    
- A **fuckton** of messages
    

Let's begin.

- First, grab the **WhatsApp Key/Database Extractor** from [here](https://github.com/YuvrajRaghuvanshiS/WhatsApp-Key-Database-Extractor). Just click on the green **Code** button on the top right and hit **Download zip**.
    
    - Sidenote: you can also download it from the **Releases** section on the right column, but the contents are slightly different and for some reason I could not manage to get the **setup.py** to work.
        
- Install [Python](https://www.python.org/). I personally installed it from the [Microsoft Store](https://apps.microsoft.com/store/detail/python-310/9PJPW5LDXLZ5).
    
- Install [Java](https://www.java.com/en/).
    
- Enable **USB Debugging** on your phone. Look up how to do it for your phone (it usually requires you to enable **Developer Options** and toggle it from there, pretty straightforward).
    
- Small copypasta from the GitHub instructions (always check the page to see if new information was added):
    
    - _1) Before doing anything take a backup of your chats and turn off your phone's internet so you don't lose any new messages. For that go to "WhatsApp Settings → Chat Settings → Chat Backup" here take a local backup._
        
    - _2) If you see a folder "Android/media/com.whatsapp" copy it somewhere safe before running the script, new versions of WhatsApp are saving data here (including images and videos), I try to keep it intact during the process but you never know when code messes up._
        
        - I didn't follow this particular step because you probably need a rooted phone to find that folder, which I didn't have.
            
- **Extract** the Whatsapp Key/Database Extractor and get into the folder.
    
- If on **Windows 11**, **Right click inside the folder** --> **Open in terminal**. If on **Windows 10**, **SHIFT + Right click inside the folder** --> **Open in terminal**. If on other systems, good luck pal, you're on your own.
    
- In **Windows Terminal/PowerShell**, type: `python3 .\wa_kdbe.py` or simply `python3 wa` and then hit **TAB**, it should automatically complete the command with **wa_kdbe.py**.
    
- Read the instructions on screen. They are just gonna be repetitions of what you just read here and on the GitHub page.
    
- The executable will, in essence, replace your current WhatsApp version with an older one in order to be able to extract your messages.
    
- At some point, you will be prompted to look at your phone. There, you will be signalled that your phone installed an old version of WhatsApp and will ask you to either check for updates or to continue. Tell it to fuck off.
    
- You will now have to confirm the backup process. **DON'T FORGET TO PUT A SECURITY CODE!** I tried twice to complete the extraction without one, but it always ended in an error, for some reason. Put a stupid code, like **0000** and hit begin.
    
- After a few moments, your backup will have been extracted and you will be prompted (on your PC) to insert a username (optional) and to insert a password for the archive (optional).
    
- If god was on your side, you should have your archive under **WhatsAppExtractorDirectory/extracted/usernameYouInputted**, and the most important files are **key**, **msgstore.db** (containing your messages), and **wa.db**.
    
    - If god was not on your side (he was probably drinking tea while you were extracting), then simply open WhatsApp again, insert your phone number and stuff, wait for it to load the messages (you don't need to wait for it to restore all the media), and then try again. My first few tries **did not work** for some reason, first because I didn't put a password before beginning the backup and then for some obscure reasons, even when I correctly put the password. **Don't give up**, my brother in christ!
        
- Now, download [whatsapp-viewer](https://github.com/andreas-mausch/whatsapp-viewer/releases?page=1). In my specific case, version **1.15** was used. Just click on **WhatsApp.Viewer.zip** under **Assets** and extract it.
    
    - Don't get overly excited. As of now, reading your archive won't work because the archive itself (as of today) comes in a format that makes the extractor whine (_no such table: chat_list_), but don't worry, we have plot armor.
        
    - Luckily for us, user [ReMiOS](https://github.com/andreas-mausch/whatsapp-viewer/issues/151#issuecomment-1229244368) (**god bless your divine soul**) made an amazing little program that you can grab from [here](https://github.com/andreas-mausch/whatsapp-viewer/files/9438508/wav_create_table.zip) that allows you to fix the archive. Download it and put it in the same folder as the archive, then run it.
        
- Finally, open **WhatsApp Viewer**. Click on **File**, select the **msgstore.db** under _File_, input your account email under _Account name_ (just put the email you use for your **Play Store** account), and select the **wa.db** file under _wa.db (optional)_.
    
- Hit OK and cry of joy.
    

WhatsApp sucks ass, kids. Use Telegram.


## Tweaks

[Images downloader](https://www.wstoolsender.com/how-to-download-all-photos-images-video-from-a-whatsapp-chat/)

