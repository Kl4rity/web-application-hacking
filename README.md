# web-application-hacking
This respository contains everything necessary to run a web-application-hacking workshop based on the juice-shop. 

# For the User

## Prerequisites
In order to participate in this Workshop you will need the following installed on your system:
1. [Docker](https://www.docker.com/products/docker-desktop/)
2. [Burpsuite](https://portswigger.net/burp/releases/professional-community-2022-3-9?requestededition=community&requestedplatform=)

## Setup
1. Start Dependencies
   Use `docker compose up -d` to start the target application (the juice shop) and your hacking environment
   
2. Download hacking tools in Kali container
   Exec into the Kali Linux container by fetching the container id with `docker ps` and then `docker exec -it <container-id>`.
   Once you're in, you run `apt update && apt -y install kali-linux-large` -> this will take about 20-30 minutes!
   
3. (Optional) Create and join your team
   If your Workshop is held in Team-Mode, sign up via the provided CTFd link and create & join / just join a team!
   
4. Start hacking!

# For the Host
There are two ways in which you can use this setup to run a Workshop - with individual hacking or team-based hacking later on.

## Individual
For participants working independently in your workshop, it is sufficient for them to run the vulnerable application locally on their machine.
You can use the docker-compose.yml file in this repository to do so.

## Team-based / CTF mode
To run a workshop with participants working in teams you will have to deploy the application and run it in CTF-Mode deployed on some container runtime. 
This repository uses CTFd since it is the best-maintained alternative out there. To use CTFd you will have to teach it about the juice-shop first.

You could, technically, set up CTFd manually with all the challenges, associated points for each, how many hints you want to provide etc. but it is advisable
to use a combination of tools to do so automatically.

1. Generate CTFd import 
   Create the necessary files using the [juice-shop-ctf](https://github.com/juice-shop/juice-shop-ctf) tool to generate the files. Remember the CTF-Key
   you provide in the prompt.
   
2. Apply Backup to CTFd
   In the admin panel of CTFd, there is a Backup feature. Use the *.zip generated in Step 1. to add the challenges, flags and hints.
   Beware: It is NOT possible to restore from Backup if you're using SQLite. You need to provide a fully-fledged DB to CTFd for this to work.
   
3. Local Juice-Shops 
   Participants can run the juice-shop locally - they just need to provide the correct CTF-key to be able to enter their results in CTFd and be rewarded.
   See the docker-compose provided in this repository. 
   ```yml
   juice-shop:
    image: bkimminich/juice-shop
    environment:
      - NODE_ENV=ctf
      - CTF_KEY=squercon
   ```

## Participant Tooling Setup
To build the container necessary for the Workshop you need to have Docker installed and to run the build.sh script. 
Additionally, you will have to download the [BurpSuite](https://portswigger.net/burp/releases/professional-community-2022-3-9).

