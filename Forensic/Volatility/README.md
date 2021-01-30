![Volatility](https://i.ibb.co/tmbBmC1/1.jpg "Volatility")

------------

# Volatility

###### Volatility is a free memory forensics tool developed and maintained by Volatility labs. Regarded as the gold standard for memory forensics in incident response, Volatility is wildly expandable via a plugins system and is an invaluable tool for any Blue Teamer.Volatility is a free memory forensics tool developed and maintained by Volatility labs. Regarded as the gold standard for memory forensics in incident response, Volatility is wildly expandable via a plugins system and is an invaluable tool for any Blue Teamer.


------------
#### Task 1
###### Intro
```No Answer Needed!```

------------

#### Task 2
###### Obtaining Memory SamplesObtaining Memory Samples
- What memory format is the most common?

Answer:

```.raw```

- The Window's system we're looking to perform memory forensics on was turned off by mistake. What file contains a compressed memory image?

Answer:

```hiberfil.sys```

- How about if we wanted to perform memory forensics on a VMware-based virtual machine?

Answer:

```.vmem```

------------

#### Task 3
###### Examining Our Patient
Now that we've collected our memory image let's dig into it! For those using their own workstation for this activity, I've provided a download link to our memory sample attached to this task.

- First, let's figure out what profile we need to use. Profiles determine how Volatility treats our memory image since every version of Windows is a little bit different. Let's see our options now with the command
```volatility -f MEMORY_FILE.raw imageinfo```

![ImageInfo](https://i.ibb.co/PtVdF1n/1.jpg "ImageInfo")

Answer:

```No Answer Needed!```

- Running the imageinfo command in Volatility will provide us with a number of profiles we can test with, however, only one will be correct. We can test these profiles using the pslist command, validating our profile selection by the sheer number of returned results. Do this now with the command 
`volatility -f MEMORY_FILE.raw --profile=PROFILE pslist`

![Plist](https://i.ibb.co/QYSbNjK/2.jpg "Plist")

What profile is correct for this memory image?

Answer:

```WinXPSP2x86```

- Take a look through the processes within our image. What is the process ID for the smss.exe process? If results are scrolling off-screen, try piping your output into less

![368](https://i.ibb.co/09SdCD7/3.jpg "368")

Answer:

```368```

- In addition to viewing active processes, we can also view active network connections at the time of image creation! Let's do this now with the command `volatility -f MEMORY_FILE.raw --profile=PROFILE netscan`. Unfortunately, something not great is going to happen here due to the sheer age of the target operating system as the command netscan doesn't support it.

![netscan](https://i.ibb.co/df9PtG5/4.jpg "netscan")

Answer:

```No Answer Needed!```

- It's fairly common for malware to attempt to hide itself and the process associated with it. That being said, we can view intentionally hidden processes via the command `psxview`. What process has only one 'False' listed?

![PsXview](https://i.ibb.co/ypJvxFr/5.jpg "PsXview")

Answer:

```csrss.exe```

- In addition to viewing hidden processes via psxview, we can also check this with a greater focus via the command 'ldrmodules'. Three columns will appear here in the middle, InLoad, InInit, InMem. If any of these are false, that module has likely been injected which is a really bad thing. On a normal system the grep statement above should return no output. Which process has all three columns listed as 'False' (other than System)?

![lsrmodules](https://i.ibb.co/9pz9J0g/6.jpg "lsrmodules")

Answer:

```csrss.exe```

- Processes aren't the only area we're concerned with when we're examining a machine. Using the 'apihooks' command we can view unexpected patches in the standard system DLLs. If we see an instance where Hooking module: <unknown> that's really bad. This command will take a while to run, however, it will show you all of the extraneous code introduced by the malware.

Answer:

```No Answer Needed!```


- Injected code can be a huge issue and is highly indicative of very very bad things. We can check for this with the command `malfind`. Using the full command `volatility -f MEMORY_FILE.raw --profile=PROFILE malfind -D <Destination Directory>` we can not only find this code, but also dump it to our specified directory. Let's do this now! We'll use this dump later for more analysis. How many files does this generate?

![malfind](https://i.ibb.co/vYMWgFM/7.jpg "malfind")
![dlllist](https://i.ibb.co/CMhSFCD/8.jpg "dlllist")
![](https://i.ibb.co/2cQFyJY/9.jpg)

Answer:

```12```

- Last but certainly not least we can view all of the DLLs loaded into memory. DLLs are shared system libraries utilized in system processes. These are commonly subjected to hijacking and other side-loading attacks, making them a key target for forensics. Let's list all of the DLLs in memory now with the command `dlllist`

Answer:

```No Answer Needed!```

- Now that we've seen all of the DLLs running in memory, let's go a step further and pull them out! Do this now with the command `volatility -f MEMORY_FILE.raw --profile=PROFILE --pid=PID dlldump -D <Destination Directory>` where the PID is the process ID of the infected process we identified earlier (questions five and six). How many DLLs does this end up pulling?

![](https://i.ibb.co/2cQFyJY/9.jpg)

![](https://i.ibb.co/qxrfnpx/10.jpg)

Answer:

```12```

------------
#### Task 4
###### Post Actions
Now that we've performed some basic forensics, let's go a step further and see what the community at large has to say about the items we've discovered. Check out the following two sites and upload the injected code we yanked out of our previous section. You can pull this code either via SCP with the box above, your local volatility workstation, or via a download link attached to this task.

[VirusTotal ](http://https://www.virustotal.com/gui/home/upload "VirusTotal ")

[Hybrid Analysis](https://www.hybrid-analysis.com/ "Hybrid Analysis")
![](https://i.imgur.com/q97tZIn.png)

- Upload the extracted files to VirusTotal for examination.

![](https://i.ibb.co/JHXcR0w/11.jpg)

Answer:

```No Answer Needed!```

- Upload the extracted files to Hybrid Analysis for examination - Note, this will also upload to VirusTotal but for the sake of demonstration we have done this separately.

![](https://i.ibb.co/JHXcR0w/11.jpg)

Answer:

```No Answer Needed!```

- What malware has our sample been infected with? You can find this in the results of VirusTotal and Hybrid Anaylsis.

![](https://i.ibb.co/PrxSTvd/12.jpg)

Answer:

```Cridex```


------------
#### Task 5
###### Extra Credit
Interested in going further? Here's a slew of awesome resources (both paid and free in no particular order) to check out and learn more!

[AlienVault Open Threat Exchange (OTX)](https://otx.alienvault.com/dashboard/new "AlienVault Open Threat Exchange (OTX)")

[windows-forensic-analysis](https://www.sans.org/cyber-security-courses/windows-forensic-analysis/ "windows-forensic-analysis")

[FOR526: Advanced Memory Forensics & Threat Detection](https://www.sans.org/brochure/course/advanced-memory-forensics-and-threat-detection/2690 "FOR526: Advanced Memory Forensics & Threat Detection")

https://www.youtube.com/watch?reload=9&v=dB5852eAgpc&feature=youtu.be

Answer:

```No Answer Needed!```

