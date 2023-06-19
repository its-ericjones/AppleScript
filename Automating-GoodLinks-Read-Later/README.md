# Automating GoodLinks and My Read Later Workflow

I often find articles while I’m at work that I’d like to save for reading later. On my personal devices that’s a pretty simple task - I just use the share extension within Safari to quickly send a URL to my [GoodLinks](https://goodlinks.app/) account.

Understandably, I don’t really want to add any of my personal accounts to a company owned computer (let alone we can’t even install non approved apps), so I’ve resorted to emailing myself articles and then manually adding them into GoodLinks from within the Mail app.

  
![iOS-Share-Sheet-GoodLinks](./Screenshots/iOS-Sharing-GoodLinks.png)  

After a few months of using this workflow I thought to myself, “Hey - I wonder if I can use AppleScript to parse through my email to extract the URLs and then add those links into GoodLinks”. While I found that AppleScript could handle the parsing of my email and gather the links, I noticed that there wasn’t a straightforward way to also add them into GoodLinks. I did discover however, that GoodLinks has built in Apple Shortcuts support to add a new link by reading the contents of the system clipboard.

I sat down and started to list out all the steps that I would need to complete in order for my script to work (this script uses a combination of AppleScript and Apple Shortcuts - all inside an Automator workflow).

1.  I set up a rule in Mail.app that took any incoming emails that were sent from my work email address and automatically moves them from my inbox into a dedicated folder called “Read Later”.
    
2.  Using AppleScript, I told macOS to open Mail.app, navigate to the “Read Later” folder that had been added to my favorites, and select all the messages in that folder.
    
3.  Using an included action within Automator.app called “Get Selected Mail Messages”, I gathered the selected items and passed them to the proceeding step.
    
  
![](./Screenshots/AutomatingGoodLinks-Steps-1-2.png) 

4.  These next few steps loops through the selected items, extracts the URLs, opens a new text file in TextEdit.app, and pastes the URLs into the file.
    
  
![](./Screenshots/AutomatingGoodLinks-Steps-3-5.png)  

5.  The script then uses AppleScript to save the newly created text file as “links.txt” into a predetermined location.
    
  
![](./Screenshots/AutomatingGoodLinks-Text-File.png)  

6.  Now it’s time to trigger the Apple Shortcut to take care of getting these links from the text file into GoodLinks. One of the ways to trigger a Shortcut is to use a system app called “Shortcuts Events” which lets you run shortcuts from any AppleScript script, without launching the Shortcuts app.
    
![](./Screenshots/AutomatingGoodLinks-Steps-6-7.png) 

7.  Add URLs From Text File to GoodLinks Shortcut
    
    1.  The input file path is defined (this directory and file name never changes).
        
    2.  The text file is split into separate lines so that each URL can be processed on its own.
        
    3.  A loop is created to parse through each URL and copy each one to the clipboard.
        
    4.  After a URL is in the clipboard, GoodLinks can then add a new link to its inbox from the system clipboard.
        
    5.  This loop continues until all the URLs in the text file are added to GoodLinks.
        
  
![](./Screenshots/AutomatingGoodLinks-Shortcuts.png) 

8.  A shell script is ran that navigates to the “read-later” directory on my local machine and deletes the previously generated text file.
    
9.  AppleScript is used to close any open TextEdit windows.
    
10.  Finally AppleScript is used to switch to Mail and delete all messages from “Read Later” folder.
    
  
![](./Screenshots/AutomatingGoodLinks-Steps-8-10.png)  

Now all I have to do at the end of the day is simply run this Automator workflow and within seconds have all my desired links in GoodLinks ready to go.