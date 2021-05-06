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
The flag has been deleted from the file "flag.txt" and needs to be found. 

## How to test:
```
docker build  -t beginners-git-challenge .  
docker run -d --name=beginners-git-challenge \
--hostname=beginners-git-challenge-server \
-e PASSWORD_ACCESS=true \
-e USER_PASSWORD=password  \
-e USER_NAME=tux -p 2222:2222 \
-e SUDO_ACCESS=false \
-v ~/.beginners-git-challenge-config:/config \
--rm beginners-git-challenge
git clone ssh://tux@localhost:2222/repo/challenge1 
git clone ssh://tux@localhost:2222/repo/challenge2
git clone ssh://tux@localhost:2222/repo/challenge3
git clone ssh://tux@localhost:2222/repo/challenge4
git clone ssh://tux@localhost:2222/repo/challenge5
```

## How to add further challenges:
Add your git repo to challenges.tar.gz. The git repo hast to contain 
an executable .git/hooks/pre-receive hook that exits with code 1, making the 
repository read-only. This script is also the place to check the content
of the pushed data and display the flag.

## Useful docker commands:  
docker exec -it beginners-git-challenge bash  

## Sample Docker compose file:  
Todo  

