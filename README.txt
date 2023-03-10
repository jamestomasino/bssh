BSSH(1)                     General Commands Manual                    BSSH(1)

NAME
       BSSH - a wrapper for Bitwarden CLI and ssh-agent

SYNOPSIS
       BSSH [ -hvpt ] [ssh key name]

DESRIPTION
       BSSH  quickly activates ssh keys by name, filling passwords via Bitwar‐
       den CLI, and adding them to ssh-agent. Keys are activated for 1-hour at
       a time.

       The  ssh key name provided to BSSH will be used to look up both the key
       itself and the password for the key. If that key has a  password,  BSSH
       will search Bitwarden for an entry named `SSH: [ssh key name]' and aut‐
       ofill the password with the results. If that entry is not found,  `[ssh
       key  name]'  will  also  be  attempted  before  giving up on a password
       search. The key will be passed to the ssh-agent regardless.

OPTIONS
       -h     Shows simple help.

       -v     Shows current version number.

       -p [pattern prefix]
              Set Bitwarden prefix pattern for the title search.  The  default
              pattern  is `SSH:'. If your key is named `testkey', then the de‐
              fault pattern will search `SSH: testkey' in  Bitwarden  for  the
              key password.

              This  is  the same as setting `pattern_prefix' in the configura‐
              tion file.

       -t [type]
              Set the SSH key type to test for. By default  BSSH  will  search
              for `id_ed25519', `id_dsa`, and `id_rsa` in that order.

              This  is  the  same  as setting `key_types' in the configuration
              file.

CONFIGURATION FILE
       $XDG_CONFIG_HOME/bssh/config
              Configuration settings in this file will override  default  set‐
              tings.  Each  setting  is  a  string  that  should be written as
              `NAME="VALUE"'. Valid settings are `pattern_prefix',  `key_loca‐
              tions', and `key_types'

ENVIRONMENT VARIABLES
       Environment  variables  will override the default settings and any con‐
       figuration file settings.

       SSH_KEY_LOCATIONS
              List of folders containing ssh keys.

              This environment variable  can  contain  any  number  of  folder
              paths, space separated, which will be used to search for the ssh
              keys. The folders are searched in order and the search stops  at
              the first successful match.

              Unless otherwise defined, this variable defaults to ~/.ssh/

              This is the same as setting `key_locations' in the configuration
              file.

       BW_PASSWORD
              Bitwarden master password (optional). If set,  this  environment
              variable will be used to automatically authenticate your bitwar‐
              den session. Alternatively, a file at $XDG_CONFIG_HOME/Bitwarden
              CLI/bw.pass  containing the password will provide the same func‐
              tionality. If neither exist the user will be  prompted  for  the
              password.

EXAMPLES
       If  you have an ssh key located at ~/.ssh/work/id_rsa, it can be loaded
       by entering:

       $ BSSH work

DEPENDENCIES
       bw     The Bitwarden CLI client

       expect programmed dialogue with interactive programs

AUTHOR
       James Tomasino

version 2023.03.10                10 Mar 2023                          BSSH(1)
