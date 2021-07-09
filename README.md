# Beginner's Git CTF Challenge
This is a CTF challenge that will teach the basics of git. The CTF challenge is
containerized with Docker for easy deployment.  

* Challenge 1   
Clone the repository, get the flag.  
* Challenge 2  
The flag has been changed in flag.txt. Look at the log to get it.  
* Challenge 3:  
There is a bug in a source file. Remove the bug and push the changes to origin.
* Challenge 4:  
The flag is in working progress. A feature and a bug branch has been added and needs to be merged.
* Challenge 5:  
Someone implemented a bug, find out who. 
* Challenge 6:  
The flag has been deleted from the file "flag.txt" and needs to be found. 
* Challenge 7:  
Another flag is in working progress. A change from a branch needs to be cherry-picked.


## How to test:
```
docker build  -t beginners-git-challenge .  
docker run -d --name=beginners-git-challenge \
--hostname=beginners-git-challenge-server \
-e PASSWORD_ACCESS=true \
-e USER_PASSWORD=password  \
-e USER_NAME=tux \
-p 2222:2222 \
-e SUDO_ACCESS=false \
-v ~/.beginners-git-challenge-config:/config \
--rm beginners-git-challenge
git clone ssh://tux@localhost:2222/repo/challenge1 
git clone ssh://tux@localhost:2222/repo/challenge2
git clone ssh://tux@localhost:2222/repo/challenge3
git clone ssh://tux@localhost:2222/repo/challenge4
git clone ssh://tux@localhost:2222/repo/challenge5
git clone ssh://tux@localhost:2222/repo/challenge6
git clone ssh://tux@localhost:2222/repo/challenge7
```

## How to add further challenges:
Add your git repo to challenges.tar.gz. The git repo hast to contain 
an executable .git/hooks/pre-receive hook that exits with code 1, making the 
repository read-only. This script is also the place to check the content
of the pushed data and display the flag.

## Useful docker commands:  
docker exec -it beginners-git-challenge bash  

## Sample Docker compose file:  
```
version: "2.1"
services:
  beginners-git-challenge:
    image: beginners-git-challenge
    container_name: beginners-git-challenge
    hostname: beginners-git-challenge-server
    environment:
      - SUDO_ACCESS=false 
      - PASSWORD_ACCESS=true
      - USER_PASSWORD=password 
      - USER_NAME=tux
    volumes:
      - ~/.beginners-git-challenge-config:/config
    ports:
      - 9000:2222 #map port 9000 to container ssh port 2222 
    restart: unless-stopped
```
## Solutions

<details>
<summary>Challenge 1</summary>
cat flag.txt  
</details>
<details>
<summary>Challenge 2</summary>
git log -p  
</details>
<details>
<summary>Challenge 3</summary>
Remove the line with the BUG using a text editor of your choice.<br>  
commit -am "Fix bug"<br>  
git push
</details>
<details>
<summary>Challenge 4</summary>
git log --all --graph -p<br>  
The 2 changes that are shown with the above command must be combined for retrieving the proper flag.<br>  
This is achieved by merging both branches into main:<br>  
git merge origin/bug-flag-typo<br>  
git merge origin/feature-flag-entropy<br>
</details>
<details>
<summary>Challenge 5</summary>
Find out commit id where bug was implemented:<br>  
git blame flag.txt<br>  
Show commit details:<br>  
git log c50d4edd --max-count 1
</details>
<details>
<summary>Challenge 6</summary>
git log -p -S flag<br>
</details>
<details>
<summary>Challenge 7</summary>
Look at the log:<br>  
git log --all --graph<br>  
Change 3  with commit id d8b45514f5af9528c3ea75e1fb9134917920a0b9 needs to be cherry picked:<br>  
git cherry-pick d8b45514f5af9528c3ea75e1fb9134917920a0b9<br>  
cat flag.txt<br>  
</details>

