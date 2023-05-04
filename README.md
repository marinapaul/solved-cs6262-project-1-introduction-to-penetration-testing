Download Link: https://assignmentchef.com/product/solved-cs6262-project-1-introduction-to-penetration-testing
<br>






<strong>The goal of this project : </strong>




Penetration testing is an important part of ensuring the security of a system. This project provides an introduction to some of the common tools used in penetration testing, while also exploring common vulnerabilities (such as Shellshock and setUID bit exploits).




On September 24, 2014, a severe vulnerability in Bash, nicknamed Shellshock, was identified. This vulnerability can exploit many systems and be launched either remotely or from a local machine. In this project, you will gain a better understanding of the Shellshock vulnerability by exploiting it to attack a machine. The learning objective of this project is to get first-hand experience on this interesting attack, understand how it works, and think about the lessons that we can get out of this attack.




<strong>Environment Setup : </strong>




<table width="680">

 <tbody>

  <tr>

   <td width="340">Files Provided</td>

   <td width="340">Description</td>

  </tr>

  <tr>

   <td width="340">shellshock_server.ova</td>

   <td width="340">The VM image (see setup Step 2).</td>

  </tr>

  <tr>

   <td width="340">assignment_questionnaire.txt</td>

   <td width="340">Template for final submission.</td>

  </tr>

 </tbody>

</table>




This project requires the use of virtual box and multiple VMs.




<strong>Installing Virtual Box: </strong>




<ol>

 <li>Install VirtualBox if it is not already installed. This project requires the latest version of VirtualBox 6.1.x. Using an earlier version of Virtual Box has been known to cause errors where the project VM freezes, so if you run into this, ensure you’re running on at least Virtual Box 6.1.0 or later.</li>

</ol>




<ol start="2">

 <li>Download the Oracle Virtual Box Extension Pack (available for download at the same location as</li>

</ol>

Virtual Box is).




<ol start="3">

 <li>Import the Extension Pack under File-&gt; Preferences-&gt; Extensions</li>

</ol>




<ol start="4">

 <li>In Virtual Box go to Tools -&gt; Preferences -&gt; Network.</li>

</ol>




<ol start="5">

 <li>Select the small plus sign in the upper right corner of the network preferences box to create a new NAT network. Select the NAT network and select the small gear below the add button to edit it. In the box that appears, change the name to something related to the project. Then save it, and close the preferences.</li>

</ol>




<strong>Installing the Kali Linux VM: </strong>




<ol start="6">

 <li>Visit <u>​</u><a href="https://www.offensive-security.com/kali-linux-vm-vmware-virtualbox-image-download">https://www.offensive-security.com/kali-linux-vm-vmware-virtualbox-image-download</a></li>

</ol>




<ol start="7">

 <li>Scroll down to “​<strong>Kali Linux Virtual Box Images​</strong>“, expand the tab, and select “​<strong>Kali Linux VirtualBox </strong></li>

</ol>

<strong>64-Bit​</strong>“. You should be prompted to save the virtual machine, and then a download should begin.




<ol start="8">

 <li>Import the Kali Linux VM to Virtual Box. Once you’ve imported the VM, you’ll likely need to go into the VM Settings and increase the number of CPUs if possible, as well as the RAM. Also enable 3-d acceleration, and set the zoom level to 300 (it makes it easier to read).</li>

</ol>




<ol start="9">

 <li>Go to the new Kali VM’s settings. In the network tab change “Attached to:” from NAT to NAT Network in the Adapter 1 tab. The name of the network should autofill to your newly created network if you only have one, but if you have multiple NAT networks, you’ll need to select the correct one.</li>

</ol>




<ol start="10">

 <li>Repeat the process with the other VMs you want to communicate with the Kali VM.</li>

</ol>




<ol start="11">

 <li>Start the Kali VM. The default username/password is: ​<strong>kali​</strong>/​<strong>kali​</strong>.</li>

</ol>




<ol start="12">

 <li>Ensure the guest additions are installed. If they’re not, go to devices-&gt;insert guest additions CD). Then follow the instructions in the popup window to install the guest additions..</li>

</ol>




<ol start="13">

 <li>In the top Virtual box menu bar of the Kali VM, go to Devices -&gt; Shared Folders -&gt; Shared Folders</li>

</ol>

Settings.




<ol start="14">

 <li>Click Machine Folders to ensure it’s highlighted. Click the small add folder icon on the right of the screen.</li>

</ol>




<ol start="15">

 <li>Select a path (in “Folder Path”) to a folder on your host machine that will act as the shared folder on the host. Give the folder a name, if it doesn’t autofill already. Check the “Auto-mount” box. Check the “Make Permanent” box. Click okay, and you should now see the folder under “Machine Folders”.</li>

</ol>




<ol start="16">

 <li>In a terminal on the Kali VM, run:</li>

</ol>




sudo usermod -a -G vboxsf $(whoami)




<ol start="17">

 <li>Now logout of the Kali VM and log back in (or just restart the Kali VM). The shared folder should be under: /media/sf_{shared folder name}</li>

</ol>







<strong>Vulnerable machine: </strong>

<ol start="18">

 <li>Download the project appliance via any of the following methods:

  <ol>

   <li>https://drive.google.com/file/d/1X7utm2Ygxpxy6gdCSKs9frA9fdsRHI4P/view?usp=sharing sha256sum: 699e5e1a02782df7c39c6638c8a520cf01ef146ab1653a0df2a422145f18201f</li>

  </ol></li>

</ol>




<ol start="19">

 <li>Import the downloaded OVA into VirtualBox (File -&gt; Import Appliance). Check the VM’s Network setting. Ensure Adapter 1 is set to NAT Network and the name of the NAT Network is the name you specified when creating the NAT Network in step 5.</li>

</ol>




<ol start="20">

 <li>Try to connect to the VM server from the Kali. Start the VM in VirtualBox (as no login is needed, you can use headless start, accessible by selecting the “Headless Start” option under the “Start” drop down menu in Virtualbox). Once you find the IP of the VM in Task 1 below, navigate to the following URL: http://&lt;IP address of the shellshock_server VM&gt;:&lt;http port found in part</li>

</ol>

1&gt;/cgi-bin/shellshock.cgi

Then you should be able to see the content:










<ol start="21">

 <li>Notice that you don’t need the password to access the web content hosted on the VM server. Instead of using a real server, it’s safer to perform the attack on an emulated Apache HTTP Server VM. ​<u>To be clear, you will not be logging into the shellshock VM during this project.</u> Once you​ configure the shellshock VM (by following steps 17-20 above), you’ll be exploiting it externally, from the Kali VM, by exploiting the Shellshock vulnerability.</li>

</ol>










<strong>Project Tasks (​</strong><strong>100​</strong><strong> points):  </strong>

<strong>Task 1: Network Scanning – (20 points) </strong>




The first step in any penetration test is to gather information about the network and servers you’ll be exploiting. In this task, you will perform network scanning and answer a few questions based on your finding. On startup, the shellshock VM listens to several ports for incoming messages.




<ol>

 <li>Find the IP address of the vulnerable VM on the NAT network.</li>

 <li>Find the port number of http traffic to the Apache web server on the VM.</li>

 <li>Find the list of open ports in the VM whose service name is shown as “unknown”. ​<strong>Hint: nmap can be used to scan open ports. Make sure to scan all ports! ​</strong>If you’re finding only one open port with the name “unknown”, you may not be using the right nmap command.</li>

 <li>Establish connection with each of the open ports with service name “unknown” that you found in question 2. Once connection is established, the server receives a unique integer answer message. <strong>Hint: netcat can be used to listen to a particular port. </strong></li>

</ol>







<strong>Task 2: Attack CGI Program– (20 points) </strong>




In this task, you will launch the Shellshock attack on a remote web server. Many web servers enable CGI, which is a standard method used to generate dynamic content on Web pages and Web applications. Many CGI programs are written using a shell script. Therefore, before a CGI program is executed, the shell program will be invoked first, and such an invocation can be triggered by a user from a remote computer.  To access this CGI program from the Web, you need to first check the server VM is running. Then, you can either use a browser by typing the following URL:




http://&lt;IP address found in part 1&gt;:&lt;http port found in part 1&gt;/cgi-bin/shellshock.cgi




or use the following command line program curl to do the same thing:




$ curl  http:// &lt;IP address found in part 1&gt;:&lt;http port found in part 1&gt;/cgi-bin/shellshock.cgi




For this task, your goal is to launch the attack through this URL, such that you can achieve something that you cannot do as a remote user. For example, you can execute some file on the server, or look up some file located on the server. When you successfully launch an attack, please execute the /bin/task2 program (which needs your GT username as the input) inside the VM. It will generate the submission hash for you.




For students that want to verify their work, here’s an example correct input/output for /bin/task2:




$ /bin/task2 g3

Here is your task2 hash: bed3f8d83f1b21fa8cc328b551069a0e59e62fc69b3ee6f68de766665f76beb7




<strong>Task 3: Reverse Shell with Metasploit – (20 points) </strong>




Now you’ve successfully launched the Shellshock attack, and you can execute commands on the server VM. However, during a penetration test, you likely won’t have time to craft a payload for every exploit you use. And, what if the server wasn’t in fact vulnerable to shellshock. How would you know if your exploit failed because it was wrong, or because there wasn’t a vulnerability?




That’s where Metasploit comes in. Metasploit is a standard in the penetration testing community. It allows pen testers to run precompiled exploits against a host, using predefined payloads. For this project, we’re going to use Metasploit to establish a reverse shell between your machine and the host machine.




Let’s first see how Metasploit works by using it to scan the open tcp ports of the shellshock_server VM. While this is a task better suited to tools like nmap (as seen in Task 1), it serves as a good demonstration of how to use a Metasploit module.​<strong> ​</strong>If you’ve used Metasploit before, you can skip this introduction and go directly to the Task 3 assignments section at the end.<strong>  </strong>




<table width="83">

 <tbody>

  <tr>

   <td width="83">msfconsole</td>

  </tr>

 </tbody>

</table>

<ol>

 <li>Begin by opening a new terminal on your Kali VM. In the new terminal type: ​​. ​After a moment, the Metasploit Framework console (msfconsole) will load. For this project, the msfconsole is the main way of accessing Metasploit. While there are other tools and command prompts associated with Metasploit, the msfconsole is suitable for the entirety of this project.</li>

</ol>




<ol start="2">

 <li>For this example, we’re going to scan the ports of a host. You can use the results from task 1 to ensure Metasploit is behaving properly. In practice using a Metasploit module solely for the purpose of scanning ports on a host is a little overcomplicated, since nmap can do much more and takes less setup, but this does offer a good introduction to using a Metasploit module.</li>

</ol>




<ol start="3">

 <li>A Metasploit module is the base of any task performed in Metasploit. It roughly consists of Ruby code that is written to perform a certain task (like exploit a certain vulnerability, or scan a certain kind of system). There are multiple different varieties of modules, but for our purposes we’ll focus on three of them:

  <ol>

   <li><strong>The Exploit modules: ​</strong>These are modules written to exploit a certain vulnerability.</li>

   <li><strong>The Auxiliary modules:​</strong> These are modules written to perform some task related to exploiting a system (like scanning). Within the auxiliary modules there are many different kinds of modules. We’ll be using the “scanner” modules for this example.</li>

   <li><strong>Payloads:​</strong> Calling these modules is a little misleading. They are the payloads (for example the shellcode) that are sent within the exploit.</li>

  </ol></li>

</ol>







The reason there are so many results is that “scanner” is a class of auxiliary modules (as seen by there being so many modules beginning with “auxiliary/scanner”). So searching for “scanner” (or “scan”) will give everything at all related to network or vulnerability scanning.







That seems a little better. Only 7 results. Since we’re scanning for open tcp ports, let’s use: “auxiliary/scanner/portscan/tcp”. In order to use a metasploit module, you should run the command: ​use module_name







You should now see “auxiliary(scanner/portscan/tcp)” after “msf5” indicating you are using the auxiliary(scanner/portscan/tcp) module.




<ol start="6">

 <li>Now that we’re using the correct module, we have to set the correct options. Try running the</li>

</ol>




While each of the options is marked as required, most of the pre-filled values work for our purposes. The only one we need to change is RHOSTS. RHOSTS should be the IP address of the host we want to scan. In this case, you should set it to the IP address of the shellshock_server VM, that you found in part 1. You can use the command: ​set rhosts IP_of_host. Now try running​       options again and ensure the RHOST option is set to the right IP address​          .




<ol start="7">

 <li>Now run ​run and you should see the same list of open ports that nmap showed. While “run” i​ s usually used to run auxiliary exploits, the command “check” and “exploit” are often used to check and run exploit modules.</li>

</ol>




Now you’ve seen an example of how to use Metasploit. You’ll follow a similar process when exploiting the shellshock vulnerability.




<strong>Task 3 Assignments: </strong>

<ol>

 <li>Find an exploit module that exploits the shellshock vulnerability on an Apache web server. Once you’ve found the module, place the module name in assignment_questionnaire.txt.</li>

 <li>Use ​show payloads to show the possible payloads for the module. Find a payload that spawns​​ <strong> a reverse tcp shell​</strong>. Place the full name of the payload in assignment_questionnaire.txt.</li>

 <li>Run the exploit and spawn a reverse shell on the VM.</li>

 <li>Run /bin/task3 in the resulting shell, then type cs6262 then your user ID. Report the hash value for your user ID in assignment_questionnaire.txt.</li>

</ol>




You’ll submit all of your answers for this section in assignment_questionnaire.txt. You should keep the reverse shell running after finishing Task 3, as you will need it in Task 4.




<strong>Task 4: Privilege Escalation – (20 points) </strong>




<strong>Your goal: </strong>

You aim to upgrade the privilege for your command shell by exploiting the setUID vulnerability. You will run bintask4 as the higher privileged user “shellshock_server”, not the default user “www-data”.​

<strong> </strong>

<strong>Background: </strong>

In Unix based systems, setUID is access rights flags that determine what users can run a program. For instance, when users want to change their password, they may run the ​passwd that requires root privilege.​     The setUID can help the user run the ​passwd with temporarily elevated privileges. However, if setUID is​ misused or setUID flags are misconfigured, it can cause a variety of vulnerabilities such as information leakage, unwanted privilege escalation, etc.




<table width="176">

 <tbody>

  <tr>

   <td width="125">As a first step, type ​</td>

   <td width="51">whoami​</td>

  </tr>

  <tr>

   <td colspan="2" width="176">bintask4 your_userI</td>

  </tr>

 </tbody>

</table>

<strong>Assignments: </strong> in your shell. You should see “www-data” which is your user ID. Now, run D. You would see a permission denied error. That is  because ​​          bintask4 is​

configured to allow only the “shellshock_server” user to run it. So, you need to find a way to run the task4 as the “shellshock_server” user. A feasible approach is to spawn a shell running as a “shellshock_server” user, and run the task4 through it.




You goal is to find a program which:

<ol>

 <li>Hash a higher privilege than the default user.</li>

 <li>Can spawn a shell.</li>

</ol>

You may want to ransack ​usrbin for a program which has a higher privilege than the default user, and​      run ​bintask4 your_userID in the shell spawned. .​




What is the vulnerable program? What command do you use to search it? What command do you use to spawn a shell with the vulnerable program? And what is the hash value from ​bintask4 your_gtid (similar to /bin/task2)? Please leave your answers in assignment_questionnaire.txt.




<strong>Task 5: Password Cracking – (20 points) </strong>




An invaluable part of any penetration test is password cracking. While there may be no known vulnerabilities in a system, a weak password could be just as damaging in allowing an attacker to gain access to a system (or view sensitive information once they gain access). We’re going to look at two kinds of weak passwords in this task: passwords that are too short, and passwords that can easily be guessed via password scraping.




To begin, start a Meterpreter shell (using a meterpreter shell payload) through the Metasploit shellshock module in Task 3. A Meterpreter shell is different from the reverse TCP shell in Task 3, as it allows you to run metasploit specific commands on the vulnerable machine (like ​download)​ . Navigate to

homeshellshock_serversecret_files. There are two encrypted .pyc files here. ​​          task51.zip is​ encrypted with zip, while ​task52.pyc.gpg is encrypted with gpg (a common file encryption tool in Linux).​          Download these two files (​task51.zip and ​​        task52.pyc.gpg)​ to your Kali VM using the meterpreter.




We already know the developers of this web server aren’t very security savvy, since they let a shellshock vulnerability plus a setUID exploit give a high privilege shell on their machine. So, chances are they didn’t pick very secure passwords for these secret files. Your goal in this task is to crack the passwords of these two files using John the Ripper (a popular password cracker) and cewl (a password scraper).




The command line tools used in Task 5 are located in ​/usr/sbin on the Kali VM. In order to run them, you​   can either add /usr/sbin to the $PATH variable, or write ​/usr/sbin/ before each command.​




You should use ​zip2john and ​​     gpg2john to extract the password hashes from the encrypted files. For​      task51.zip, try running John the Ripper incrementally. Report your John the Ripper command in​       assignment_questionnaire.txt (whether you also report your the zip2john and gpg2john commands is up to you, but they won’t be graded).




For ​task52.pyc.gpg, try running John the Ripper incrementally again. Hmm… it seems to run forever.​          That’s because John the Ripper is trying every possible combination of characters. If the password is too long (among other things), John the Ripper could run for years before it finds it.




But, just because the password is too long to be found incrementally, doesn’t mean it can’t be cracked.

Take a look at the shellshock.cgi page in the browser. It looks like it gives a link to a profile of the authors. If the authors aren’t great at picking secure passwords, maybe the password is something about them that we can guess from their profile page.




But, even if the password is on the profile page, it can still take a while to guess by hand. What if the password was kItt3n$ or deVEL0p3r. It would be hard to guess that, even if the word it was based on (like “kittens”, or “developer”) was on the profile page.




Instead, let’s use a password scraper to create a custom wordlist for John the Ripper. For this project, we suggest using cewl. cewl is a relatively simple command line program that comes preinstalled on Kali, and creates password wordlists off of webpages. Since we want to get every possible password (including if the authors based the password off something on shellshock.cgi, or one of the landing pages), you should run cewl on shellshock.cgi, with the proper settings to ensure it follows the links all the way to profile.cgi (you may need to tune the cewl parameters). Report your cewl command in assignment_questionnaire.txt. Then try running John the Ripper on ​task52.pyc.gpg with the wordlist (and the default wordlist rules for​       testing different permutations of the words). Report your John the Ripper command in assignment_questionnaire.txt.




Once you find the passwords, report them in assignment_questionnaire.txt. Then decrypt the two files

(using zip for ​task51.zip and gpg for​      ​task52.pyc.gpg)​ and run ​python task51.pyc your_user_ID and ​python task52.pyc your_user_ID. Report the resulting hash values for your user ID in​       assignment_questionnaire.txt.




<strong>Deliverables: </strong>




​Please use ​<strong>Gradescope ​</strong>to submit the assignment files. The link to Gradescope is found in Canvas under Courses tab -&gt; Gradescope.  In Gradescope under active assignments click project 1 to upload your files.  ● assignment_questionnaire.txt

<ul>

 <li>README.txt</li>

</ul>







The provided template “assignment_questionnaire.txt” marks where you should add your answers for each question. ​<strong>Please DO NOT edit anything other than the fields marked for your answers (or student ID) in assignment_questionnaire.txt. ​</strong>Doing so may result in the autograder failing to process your submission.




Please note that there is a <u>​5-point penalty​</u> for not following the format given in assignment_questionnaire.txt.




You should also include a “README” plain text file explaining how and why each piece of your solution works. Including it makes grading easier if we cannot reproduce your results. You may also include screenshots in your submission to show proof. If you use any outside sources not mentioned in this write-up, then the README would be a good place to mention them as well. Although there is no specific format for the README, since it is not officially graded, we do offer a sample format under sample-README.txt.




<strong>Reminders:</strong>




Please submit the files <u>​EXACTLY</u> as requested to Canvas. ​​      <u>DO NOT package them up (e.g., as a ZIP file).</u> Any deviations may result in a deduction of your grade.




There is a <u>​5-point penalty</u>​ for not following the submission format shown.




<strong>Useful Links and References:</strong>




<ul>

 <li>Shellshock Vulnerability</li>

</ul>

◦ <a href="https://github.com/carter-yagemann/ShellShock">https://github.com/carter-yagemann/ShellShock</a>

◦ <a href="https://en.wikipedia.org/wiki/Shellshock_(software_bug)">https://en.wikipedia.org/wiki/Shellshock_(software_bug</a>)​

◦ <a href="http://seclists.org/oss-sec/2014/q3/650">http://seclists.org/oss-sec/2014/q3/650</a> ● curl

◦ <a href="https://curl.haxx.se/docs/manpage.html">https://curl.haxx.se/docs/manpage.html</a>

◦ <a href="https://curl.haxx.se/download.html">https://curl.haxx.se/download.html</a><u>​</u> (curl.exe for Windows)

<ul>

 <li>netcat</li>

</ul>

◦ <a href="https://linux.die.net/man/1/nc">https://linux.die.net/man/1/nc</a>

◦ <a href="https://eternallybored.org/misc/netcat/">https://eternallybored.org/misc/netcat/</a><u>​</u> (nc.exe for Windows)

<ul>

 <li>nmap</li>

</ul>

◦ <a href="https://nmap.org/book/man.html">https://nmap.org/book/man.html</a>

<ul>

 <li>Metasploit</li>

</ul>

◦ <a href="https://www.offensive-security.com/metasploit-unleashed/metasploit-fundamentals/">https://www.offensive-security.com/metasploit-unleashed/metasploit-fundamentals/</a>

<ul>

 <li>John the Ripper</li>

</ul>

◦ <a href="https://www.openwall.com/john/doc/">https://www.openwall.com/john/doc/</a> ● cewl

◦ <a href="https://tools.kali.org/password-attacks/cewl">https://tools.kali.org/password-attacks/cewl</a>




<strong>Acknowledgment:</strong>




This Lab was modified from SEED Labs, Copyright 2014 Wenliang Du, under the terms of GNU Free

Documentation License, Version 1.2. The original document can be found at <a href="http://www.cis.syr.edu/~wedu/seed/">http://www.cis.syr.edu/~wedu/seed/</a>




<strong>Checklist/Rubric:</strong>




<table width="703">

 <tbody>

  <tr>

   <td colspan="2" width="594">Section</td>

   <td width="84">Points</td>

   <td width="25">✓</td>

  </tr>

  <tr>

   <td width="37"><strong>1 </strong></td>

   <td width="557"><strong>Network Exploration </strong></td>

   <td width="84"><strong>20 </strong></td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">1.1</td>

   <td width="557">Correct first digits of the IP Address of the vulnerable VM.</td>

   <td width="84">5</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">1.2</td>

   <td width="557">Correct HTTP port.</td>

   <td width="84">5</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">1.3</td>

   <td width="557">Correct Port/Message Pairs (points divided evenly over all pairs)</td>

   <td width="84">10</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37"><strong>2 </strong></td>

   <td width="557"><strong>Exploiting the System </strong></td>

   <td width="84"><strong>20 </strong></td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">2.2</td>

   <td width="557">Correct hash value from running /bin/task2.</td>

   <td width="84">20</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37"><strong>3 </strong></td>

   <td width="557"><strong>Spawning a Shell with Metasploit </strong></td>

   <td width="84"><strong>20 </strong></td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">3.1</td>

   <td width="557">Correct exploit module</td>

   <td width="84">5</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">3.2</td>

   <td width="557">Correct payload module (there are multiple correct answers here)</td>

   <td width="84">5</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">3.3</td>

   <td width="557">Correct hash value from running /bin/task3.</td>

   <td width="84">10</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37"><strong>4 </strong></td>

   <td width="557"><strong>Privilege Escalation </strong></td>

   <td width="84"><strong>20 </strong></td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">4.2</td>

   <td width="557">Correct vulnerable program name.</td>

   <td width="84">10</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">4.4</td>

   <td width="557">Correct hash value from running /bin/task4</td>

   <td width="84">10</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37"><strong>5 </strong></td>

   <td width="557"><strong>Password Cracking </strong></td>

   <td width="84"><strong>20 </strong></td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">5.2</td>

   <td width="557">Correct password for task51.zip.</td>

   <td width="84">5</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">5.3</td>

   <td width="557">Correct hash value from running python task51.pyc.</td>

   <td width="84">5</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">5.6</td>

   <td width="557">Correct password for task52.pyc.gpg.</td>

   <td width="84">5</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">5.7</td>

   <td width="557">Correct hash value from running python task52.pyc.</td>

   <td width="84">5</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37"><strong>– </strong></td>

   <td width="557"><strong>Possible Deductions </strong></td>

   <td width="84"><strong> </strong></td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">i.</td>

   <td width="557">Incorrect assignment_questionnaire.txt format.</td>

   <td width="84">-5</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">ii.</td>

   <td width="557">Incorrect upload to Gradescope/Canvas.</td>

   <td width="84">-5</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">2.1</td>

   <td width="557">No command given for exploiting the shellshock vulnerability.</td>

   <td width="84">-5</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">4.1</td>

   <td width="557">No command given for finding the vulnerable program.</td>

   <td width="84">-5</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">4.3</td>

   <td width="557">No command given for exploiting the setUID vulnerability.</td>

   <td width="84">-5</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">5.1</td>

   <td width="557">No command given for cracking task51.zip.</td>

   <td width="84">-5</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">5.4</td>

   <td width="557">No command given for scraping the shellshock server webpage.</td>

   <td width="84">-5</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">5.5</td>

   <td width="557">No command given for cracking task52.pyc.gpg.</td>

   <td width="84">-5</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37">+</td>

   <td width="557">Your Submission IncludesTotal:</td>

   <td width="84">100</td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37"></td>

   <td width="557">assignment_questionnaire.txt – Answers to questions</td>

   <td width="84"></td>

   <td width="25"></td>

  </tr>

  <tr>

   <td width="37"></td>

   <td width="557">README.txt</td>

   <td width="84"></td>

   <td width="25"></td>

  </tr>

 </tbody>

</table>


