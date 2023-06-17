# Cloning remote repository with SSH

## What I want to do

I would like to clone remote repository via ssh in order to clone in more security

## What to do 

 1. check you local ssh key
  If you have ssh key already, you can use it to clone.<br>
  So firstly you should check your local key in the fllowing command.<br>
    1. open Git Bush
    2. excute following command
        ```text
        ls -al ~/.ssh
        ```
      ※ls -> show you about file and folder in current directory.(same as dir of windows command)<br>
      ※-al -> show extension of eah file showed(same as -all)<br>
      
      if you get like following message after excuted above command, your local ssh key is nothing.<br>
      So you should make it<br>
      ```text
      ls: cannot access '{your path}/.ssh': No such file or directory
      ```
      
      if you get like following message after excuted above command, your local ssh key exist.<br>
      So you don't have to make new local ssh key.<br>
      ```text
      ls: cannot access '{your path}/.ssh': No such file or directory
      ```
 2. add new ssh key and add it to ssh-agent
    1. open Git Bush
    2. excute following command(replace your github email)
        ```text
        ssh-keygen -t ed25519 -C "your_email@example.com"
        ```
      after axcuted above command, you can neww ssh key.<br>
      and you should get follwoing message, so you can type path that you want keep on.(if you want to use default path, don't type any path and press enter button)<br>
      ```text
      Generating public/private ed25519 key pair.
      Enter file in which to save the key (/your path/.ssh/id_ed25519):
      ```
      and then propably git bush will show you following message.<br>
      If that is, you should type passphrase to protect your ssh key against attacker that aim to you<br>
      ```text
      Enter passphrase (empty for no passphrase):[Type new passpohrase]
      Enter same passphrase again:[Repeat the new passphrase]
      ```
      Congratulations! you should get new ssh key!<br>
  
 3. set automatically ssh-agent wroking on Git for Windows
  If you want to automatically make ssh key work when starting git bush, you should do following step<br>
    1. make ~/.profile or ~/.bashrc<br>
     If you have alerady them, you can skip this step.
        ```text
        touch .profile
        ```
    2. write following code in that file
        ```text
        env=~/.ssh/agent.env

        agent_load_env () { test -f "$env" && . "$env" >| /dev/null ; }

        agent_start () {
            (umask 077; ssh-agent >| "$env")
            . "$env" >| /dev/null ; }

        agent_load_env

        # agent_run_state: 0=agent running w/ key; 1=agent w/o key; 2=agent not running
        agent_run_state=$(ssh-add -l >| /dev/null 2>&1; echo $?)

        if [ ! "$SSH_AUTH_SOCK" ] || [ $agent_run_state = 2 ]; then
            agent_start
            ssh-add
        elif [ "$SSH_AUTH_SOCK" ] && [ $agent_run_state = 1 ]; then
            ssh-add
        fi

        unset env
        ```
    3. restart git bush
      In the first time after you finished above step, let you type passphrase<br>
        ```text
        Enter passphrase for [your path]/.ssh/id_ed25519:[Type your passphrase]
        ```

 4. add ssh key to git account
    1. copy public key to clip boed
      ```text
      clip < ~/.ssh/id_ed25519.pub
      ```
    2. click profile image on github and click SSH adn GPS Keys
    3. click ADD SSH Key
    4. fill out you ssh key infomation
      Title -> description How you use this key. for exmple [personal laptop]<br>
      Key type -> chose authentication (you can chose both)<br>
      Key -> past public key <br>
    
    Congratulations! you compleate ssh setting!<br>
    if you would like to test connecting, you are able to get method of test on foolowing link.<br>
    https://docs.github.com/en/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection

## reference Document
add ssh key::https://docs.github.com/ja/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases<br>
Key phrease:https://docs.github.com/ja/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases
