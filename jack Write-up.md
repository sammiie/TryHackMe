## Instruction

Connect to our network and deploy this machine.

Add jack.thm to /etc/hosts

![image](https://user-images.githubusercontent.com/16500435/98109056-3c949000-1e9d-11eb-99be-4f29ac14217c.png)

## Enumerating the machine and information Gathering

First I scanned the ip using **nmap** to discover open ports  

![image](https://user-images.githubusercontent.com/16500435/98109324-ac0a7f80-1e9d-11eb-83e4-521ddb863096.png)

port 80 is open so i tried to see what is on the webpage but nothing seems interesting and useful just yet.

I used **Gobuster** scan to find hidden directory


![image](https://user-images.githubusercontent.com/16500435/98110554-8bdbc000-1e9f-11eb-8baa-ff2f439966c1.png)

/robots.txt

![image](https://user-images.githubusercontent.com/16500435/98110790-eb39d000-1e9f-11eb-8bbb-23eec9cda1ad.png)


/wp-admin/ /admin /login all led to a wordpress login page

![image](https://user-images.githubusercontent.com/16500435/98111115-69967200-1ea0-11eb-8646-faf921c17477.png)

I went back to check the Hint on the room page 

![image](https://user-images.githubusercontent.com/16500435/98111266-9ba7d400-1ea0-11eb-8f8b-95f76b27d70c.png)

After doing some digging and searching online i stumbled on a page that with showed me how I can use wpscan (don't forget I'm also still learning)

[https://www.wpwhitesecurity.com/enumerate-wordpress-users-wpscan-security-scanner/](url)

[https://www.wpwhitesecurity.com/strong-wordpress-passwords-wpscan/](url)

First i did a user enumeration using **wpscan**


![image](https://user-images.githubusercontent.com/16500435/98114309-5b972000-1ea5-11eb-9ea1-16f19e7619ca.png)

First I got the WordPress version

![image](https://user-images.githubusercontent.com/16500435/98115614-63f05a80-1ea7-11eb-90d7-0b2a87bb5ada.png)

then some users 

![image](https://user-images.githubusercontent.com/16500435/98115089-89c92f80-1ea6-11eb-9338-6880cd27fe01.png)

## Getting Login Access to wp-admin page
Now that i have some users i decided to save them in a txt file as users.txt, then use wpscan to bruteforce login just as show below

![image](https://user-images.githubusercontent.com/16500435/98116259-55ef0980-1ea8-11eb-8a0a-85dcfaf5abfb.png)


Hurray!!! Got a user and matching password

![image](https://user-images.githubusercontent.com/16500435/98116459-9484c400-1ea8-11eb-9848-f980fc086e33.png)

Now i will login with this crendentials

![image](https://user-images.githubusercontent.com/16500435/98116713-f47b6a80-1ea8-11eb-8d49-dc35eb335d0f.png)


I started pressing and clicking evrything on the page. I tried to add new post then upload file but got a message like this

![image](https://user-images.githubusercontent.com/16500435/98117382-f4c83580-1ea9-11eb-89c1-0212090cb5ff.png)

decided to check exploitdb for any vulnerabilities for this version




