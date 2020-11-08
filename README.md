Setup development environment for window 10



# [Cmder](https://cmder.net/)

Cmder is "terminal" in window instead of the bad console emulator "cmd" in window.

The installation is very simple because it's portable, so you just need to download, unzip and run *cmder.exe*.

## Create a shortcut (Ctrl + Alt + T) to open cmder immediately

1. Open the directory you have placed Cmder
2. Right click to *Cmder.exe* -> Send to -> Desktop (create shortcut)
3. Right click to cmder shortcut created -> Properties -> shortcut key : Ctrl + Alt+ T

![properties cmder](.\img\Properties_cmder.jpg)

## Shortcut to open Cmder in a chosen folder

1. Open a terminal as an Administrator
2. Navigate to the directory you have Administrator
3. Execute ```.\cmder.exe \REGISTER ALL```. *if you get message "**Access Denied**" ensure you are executing the command in an **Administrator** prompt* 

In a file explorer window right click in or on a directory to see "Cmder Here" in the context menu.

## My custom Cmder

### Theme

![dracula theme cmder](.\img\cmder.png)

I use [Dracula theme](https://draculatheme.com/cmder). To install:

1. Download and unzip
2. Open your cmder
3. Click Win+Alt+P
4. Click in Import
5. Select the Dracula.xml
6. Save Settings

### Change default path

1. Go to *'settings'* (Click Win+Alt+P)

2. In the settings group *'Startup'*, click on *'Tasks'*

3. Click the console you want to modify (e.g. *cmd::Cmder*, *cmd::Cmder as Admin*, *bash::bash* etc.)

4. Click the button that says *'Startup dir...'*

5. Select the directory you want the console to start up in by default

   ![cmder_startup](.\img\cmder_startup.jpg)

### Change symbol  lambda "λ"

1. Open the directory you have placed Cmder
2. Open file ```cmder/vendor/clink.lua``` 
3. In line ``` local lambda = "λ"``` replace  "λ" to your symbol
4. save file

### Use within Terminal of PHPStorm

1. Add a new environment variable into your Windows via the Control Panel.

   ![](.\img\cmder_add_path.jpg)

2.  Update your terminal setting inside PhpStorm. Change the shell path from cmd.exe as follows:

   ```shell
   "cmd" /k ""%CMDER_ROOT%\vendor\init.bat""
   ```

*Note: if not working, restart your computer to add new environment variable*

### ZSH

#### Install Subsystem Linux using powershell

1. Install Subsystem

   ```shell
   powershell -command Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
   ```

   *Window will be restarted after finish installation*

2. Install Ubuntu form Microsoft Store

#### Subsystem Linux install zsh, oh-my-zsh, theme and configurations

- Install zsh

  ```shell
  sudo apt install zsh
  ```

- Install [oh-my-zsh](https://github.com/ohmyzsh/ohmyzsh)

  ```shell
  sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
  ```

- install oh-my-zsh theme: [Powerlevel9k](https://github.com/Powerlevel9k/powerlevel9k)

  ```shell
  git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k
  ```

- oh-my-zsh configurations in ```~/.zshrc```

  ```shell
  # Path to your oh-my-zsh installation.
  export ZSH="/home/nhoxnho1212/.oh-my-zsh"
  
  ZSH_THEME="powerlevel9k/powerlevel9k"
  POWERLEVEL9K_LEFT_PROMPT_ELEMENTS=(dir rbenv vcs virtualenv)
  POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status root_indicator background_jobs history time)
  POWERLEVEL9K_PROMPT_ON_NEWLINE=true
  POWERLEVEL9K_VCS_MODIFIED_BACKGROUND=’red’
  POWERLEVEL9K_PROMPT_ADD_NEWLINE=true
  
  # Add a space in the first prompt
   POWERLEVEL9K_MULTILINE_FIRST_PROMPT_PREFIX="%f"
  # # Visual customisation of the second prompt line
  local user_symbol="$"
  if [[ $(print -P "%#") =~ "#" ]]; then
       user_symbol = "#"
       fi
  POWERLEVEL9K_MULTILINE_LAST_PROMPT_PREFIX="%{%B%F{black}%K{yellow}%} $user_symbol%{%b%f%k%F{yellow}%} %{%f%}"
  
  plugins=(
            git
    )
  
  source $ZSH/oh-my-zsh.sh
  ```

#### Running zsh on cmder