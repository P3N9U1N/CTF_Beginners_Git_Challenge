# Beginner's Git CTF Challenge
This is a CTF challenge that will teach the basics of git. The CTF challenge is
containerized with Docker for easy deployment.  

* Challenge 1   
Clone the repository, get the flag.  
* Challenge 2  
The flag has been changed in flag.txt. Look at the log to get it.  
* Further Challenges  
Todo.  

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
```

## Useful docker commands:  
docker exec -it beginners-git-challenge bash  

## Sample Docker compose file:  
Todo  

