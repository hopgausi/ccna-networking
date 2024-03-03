# Basic Router Security configuration 
- User exec mode is identified by the greater sign prompt
- Privelege mode is identified by the hash sign prompt
- Global configuration is identified by the ```config``` parameter in the name prompt
- Line configuration mode is identified by the ```config-line``` parameter in the name prompt
- Interface configuration mode is identified by the ```config-if``` parameter in the name prompt
### 1. Connect R1 and R2  	
 - Use the straight through copper cable to connect the routers
### 2. Set hostnames
- Go to the global configuration mode to set the hostnames
```shell
enable # or en for shorthand - goes to priveledge exec mode
configure terminal # or conf t - enables the glob al configuration mode
hostname R1 # set the hostname of the router to R1
```
### 3. enable password on the routers
- Done in the global configuration mode - protects the priveledge exec mode. This sets the password on the router required when going from user exec mode to priveledge exec mode using the enable keyword and the password is by default encrypted(using type 5 encryption). The enable secret renders the enable password useless whether enable password is done last or not.
```shell
enable secret cisco # this sets the cisco password on the router required when going from user exec mode to priveledge exec mode using the enable keyword
```
- OR :  Done in the global configuration mode - protects the priveledge exec mode. This sets the password on the router required when going from user exec mode to priveledge exec mode using the enable keyword and the password is by default not encrypted
```shell
enable password cisco # this sets the cisco password on the router required when going from  exec mode to priveledge exec mode using the enable keyword
```
### 4. View password in the running config
- Done in the global configuration mode
```shell
do show running-config # or do sh run 
```
- Done in priveledge exec mode
```shell
show running-config # or do sh run
```
- Use space bar to move page by page or enter key to move line by line
### 5. enable password encryption
- For password set without password encryption, enable password encryption via below command in the global configuration mode. Encrypt password using type 7 password encryption.
```shell
service password-encryption
```
### 6. View password in running config to see if encrypted
- Step encrypts unencrypted password such that view it is no longer plain text - run in the priveledge exec mode
```shell
show running-config # view runnning configuration.
```
### 7. Disable password encryption and see if its still encrypted
- To disable password encryption: run in the global configuration mode
```shell
no service password-encryption
```
- This only disables password encryption on the next passwords set whereas previous password remains encrypted
### 8. Exiting the configuration modes
- Exit any configuration mode to privilege exec mode
```shell
end
```
- Exit any of the configuration modes to the previous mode except when the previous mode is user exec mode
```shel
exit
```
### 9. Save current configuration to start up configuration
- Done in the priveledge exec mode
```shell
copy running-config startup-config # or copy run start
```
OR
```shell
write # or w
```
- Any command to be run in the configuration mode that is supposed to be run in the priveledge exec mode needs to be prefixed with ```do```
### 10. Reloading the router
- Done in the priveledge exec mode - This reboots the router
```shell
reload
```
### 11. Console port connection security
- Done in the line configuration mode
```shell
line console 0  # Run in the global configuration mode
password YOUR_PASS
login # to enable password when using console connection
service password-encryption # Run in the global configuration mode
do w
```

#### -- Example basic router security configuration
- Set hostname, enable password, console password, save the configuration
```shell
enable
configure terminal
hostname R1
enable secret cisco
line console 0
password ccna
login
exit
service password-encryption
do w
```