<div align="center">
  <img src="https://i.imgur.com/Zr41qXZ.png" width="100%"></img>
</div>

WordPress Privilege Escalation Rapidly  
  
<b>About:</b>  
Automatically upload, execute, and delete PHP files on WordPress with a single command (and valid credentials).  
Speed++. Stealth++. Shell WordPress in mere seconds with wopper!  
wopper also makes a great skeleton for other web exploits. Feel free to modify the curl calls and use it as a template for other projects!  
  
Read the article [here](https://www.netspi.com/blog/technical-blog/web-application-pentesting/getting-shells-at-terminal-velocity-with-wopper).
  
<b>Installation:</b>  
pup is used for HTML processing.  
<code>sudo apt-get install pup</code>  
  
<b>Usage:</b> wopper -u [user] -p [pass] -f [file] (-x) (-s) (-t [time]) (-i) (-c) (-o) (-v) [URL]  
  
The URL must be specified as the final argument and should point to the target's WordPress root directory. The URL should include the protocol and supports non-standard ports.  
The -u, -p, and -f flags are required for most commands.  
  
Wopper has five modes of operation depending on whether the following flags are used:  
  
Default Mode:  
The chosen file will be automatically uploaded and its location will be returned, if successful.  
An optional execution flag, -x, can be set to execute the file after upload.  
This is useful when you want to automatically upload and execute, but not delete a file.  
Usage: wopper -u [user] -p [pass] -f [file] (-x) [URL]  
  
Scrub Mode (-s):  
The chosen file will be automatically uploaded, executed, and subsequently deleted via a second file.  
An optional timer flag, -t, can be set to add a timeout (in seconds) after execution and before deletion.  
This mode is useful if you'd like to kill and remove a script after a set time or automate deletion without modifying the original file.  
In Scrub, Inject, and Command Mode, the optional -v flag can be used to verify deletion.  
Usage: wopper -u [user] -p [pass] -f [file] -s (-t [timeout]) (-v) [URL]  
  
Inject Mode (-i):  
The chosen file will be injected into a wrapper script that will allow it to run in a background process while deleting itself.  
Furthermore, this option provides minor obfuscation via Base64 and randomly generated file names.  
Usage:  wopper -u [user] -p [pass] -f [file] -i (-v) [URL];  wopper -f [file] -i (file name)  
  
Command Mode (-c):  
The chosen command will be converted to Base64 and inserted into a self-destructing wrapper script, similar to Inject Mode.  
The difference is that instead of executing another PHP script, the command is executed directly.  
Usage:  wopper -u [user] -p [pass] -c [cmd] (-v) [URL];  wopper -c [cmd] (file name)  
  
Obfuscation Mode (-o):  
This mode simply performs additional obfuscation by randomizing variable names. More obfuscation to be added in the future.  
Usage: wopper -f [file] -o (file name)  
  
Local Use:  
If no URL is specified in Inject or Command Mode, the resulting file is saved locally and not uploaded.  
When saving locally, the resulting file name can be set as the final argument. Otherwise the file name is random. File names must end with ".php".  
If a second file name is given as the final argument in Obfuscation Mode, a copy with that name is obfuscated instead of the original.  
<br>
<br>
<b>Credits:</b>  
Thank you to Karl Fosaaen, Amanda Squire, and Emily Hinderaker for helping me get this tool and the blog post published!  
Thank you to Ben Lister for all the help with detection engineering!  
