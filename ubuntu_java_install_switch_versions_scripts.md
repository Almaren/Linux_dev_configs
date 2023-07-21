### Preparing environments file:
Create environments file for all users which loaded after log in:
```bash
touch /etc/profile.d/env.sh
sudo chmod a+x /etc/profile.d/env.sh

nano /etc/profile.d/env.sh
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export PATH=$PATH:$JAVA_HOME/bin
```
___
### Check version:
```bash
java --version #for java 11
java -version
whereis java
update-alternatives --list java # or:
update-java-alternatives --list
```
### Install:
Isntall location in case of manual installL /usr/lib/jvm  
https://jdk.java.net/19/  

```bash
sudo apt install openjdk-11-jdk
sudo apt install openjdk-8-jdk #(used for accepting android studio licenses: $flutter doctor --android-licenses)
sudo apt install openjdk-17-jdk

# or using the following with adding priority:
sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk-20/bin/java 1000
sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk-20/bin/javac 1000
sudo update-alternatives --install /usr/bin/javaws javaws /usr/lib/jvm/jdk-20/bin/javaws 1000
```
### Choose current version:
```bash
sudo update-alternatives --config java # and then select numerically or:

sudo update-alternatives --set java /usr/lib/jvm/java-17-openjdk-amd64/bin/java
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export PATH=$JAVA_HOME/bin:$PATH
source /etc/profile.d/env.sh
source /etc/profile
```
____
### Use scripts to switch between versions:
In my case add scripts to: /home/username/.local/bin/
java8.sh:
```bash
#!/bin/bash
sudo update-alternatives --set java /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
export PATH=$JAVA_HOME/bin:$PATH
source /etc/profile.d/env.sh
source /etc/profile
```
java11.sh:
```bash
#!/bin/bash
sudo update-alternatives --set java /usr/lib/jvm/java-11-openjdk-amd64/bin/java
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
export PATH=$JAVA_HOME/bin:$PATH
source /etc/profile.d/env.sh
source /etc/profile
```
java17.sh:
```bash
#!/bin/bash
sudo update-alternatives --set java /usr/lib/jvm/java-17-openjdk-amd64/bin/java
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export PATH=$JAVA_HOME/bin:$PATH
source /etc/profile.d/env.sh
source /etc/profile
```

Add to ~/.bashrc:
```bash
# Alias definitions.
# You may want to put all your additions into a separate file like
# ~/.bash_aliases, instead of adding them here directly.
# See /usr/share/doc/bash-doc/examples in the bash-doc package.

if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi
```
~/.bashaliases:
```bash
alias bat="/home/username/.local/bin/bat"
alias java8="source /home/username/.local/bin/java8.sh"
alias java11="source /home/username/.local/bin/java11.sh"
alias java17="source /home/username/.local/bin/java17.sh"
```
Recompile for changes:
`source ~/.bashrc`
Use script:
`java17`
