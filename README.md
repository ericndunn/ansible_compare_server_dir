# ansible_compare_server_dir
Compare contents of folders on remote hosts

# Assumptions:
    - MacOS Instructions.
    - Ansible installed
        `brew install ansible`
    - SSH keys copied to hosts 
        `ssh-copy-id user@servername`

# Create Inventory Hosts file for Ansible Playbook:
`/Users/UserID/inventory`

`[AA-PROD-WAS]`

`Servername1 inv_folder=/usr/WebSphere/wlp/usr/servers/b1_443_api/apps`

`Servername2 inv_folder=/usr/WebSphere/wlp/usr/servers/b2_444_api/apps`

`Servername3 inv_folder=/usr/WebSphere/wlp/usr/servers/b3_445_api/apps`

`Servername4 inv_folder=/usr/WebSphere/wlp/usr/servers/b4_446_api/apps`


# Variables:
Hardcode the variables or override with --extra-vars on `ansible-playbook` command line:

    `my_userid: "{{ lookup('env','MY_USERID') }}"`
    `master: "{{ lookup('env','MASTER_SERVER') }}"`

In ansible There is no option to store passphrase-protected private key. For that we need to add the passphrase-protected private key in the ssh-agent. 

# Start the ssh-agent in the background.
`eval "$(ssh-agent -s)"`

# Add SSH private key to the ssh-agent
`ssh-add ~/.ssh/id_rsa`

# Run Ansible Playbook
`ansible-playbook -i /Users/UserID/inventory --extra-vars "my_userid=UserID master=Servername1"`

        
