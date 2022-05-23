# The Magic of Subler and Applescript

I've been in the process of digitizing all my DVDs of movies and tv shows. After I have the files, I like to embed all the relevant metadata into the file itself so I'm able to move it to any self hosted media service without having to rely on third party metadata indexers.

My application of choice for this task is called Subler which allows me to search various databases for metadata, embed that data, optimize for handheld devices, and export.

The process of a few movies or shows is fairly straightforward with a couple clicks and export, however when you're trying to work with an entire tv series you end up having to do the same clicks over and over.

This is where automation comes into play. I created a script with AppleScript on macOS that utilizes emulating keyboard shorcuts for the entire workflow.

Here's a look at the final AppleScript file:
![subler-script](/Screenshots/Script.png)

Here's a gif of the workflow in action:

![subler-gif-workflow](/Videos/Subler-Script.gif)

This is what the workflow looks like in Subler if you were to execute it manually:

1. Importing Files
![subler-importing-files](/Screenshots/Step-2-Import-File.png)
2. Search and Adding Metadata
![subler-adding-metadata](/Screenshots/Step-3-Add-Metadata.png)
3. Adding Artwork 
![subler-adding-artwork-1](/Screenshots/Step-4-Adding-Artwork-1.png)
4. Exporting
![subler-exporting](/Screenshots/Step-5-Exporting.png)

This script is available for anyone to download. 
