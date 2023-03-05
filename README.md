# Cloud-Computing-Ubuntu-Assignment-2

### LunixStatus Script
* Create script file
```
$ touch LinuxStatus
```
* Change file mode to be executable
```
$ chmod +x LinuxStatus
```
* Set requirements in the file using `vim LinuxStatus`
```
#!/bin/bash

function display_option {
    case "$1" in
        1|p)
            echo "Running processes:"
            ps
            ;;
        2|r)
            echo "Memory status:"
            free -h
            ;;
        3|h)
            echo "Hard disk status:"
            df -h
            ;;
        4|a)
            if command -v apache2 >/dev/null 2>&1; then
                version=$(apache2 -v | grep "Server version:" | awk '{print $3}')
                echo "Apache version: $version"
            else
                echo "Apache is not installed"
            fi
            ;;
        5)
           exit 0
           ;;
        *)
            echo "Invalid input. Please enter input from 1 to 4 or one or more than one of p, r, h, and a."
            ;;
    esac
}

if [ $# -gt 0 ]; then
    for arg in "$@"; do
        display_option "$arg"
    done
    exit
fi

clear
echo "========= Welcome $(whoami) =============="
echo "------------------------------------------"
echo "Current user: $(whoami)"
echo "Current date: $(date '+%Y-%m-%d_%H:%M')"
echo "Linux version: $(lsb_release -d | awk '{print $2, $3}')"
echo "========================================="

echo ""
echo "Available Options:"
echo "1. List the running processes"
echo "2. Check the memory status and free memory in the RAM"
echo "3. Check the hard disk status and free memory in the HDD"
echo "4. Check if Apache is installed and if yes, return its version"
echo "5. Exit"

read -p "Enter your choice (1-5): " main_choice

declare -i out=0
while true; do

    if [ $out -eq 1 ]; then
         exit
    fi
    display_option "$main_choice"

    echo ""
    echo "1. Back to the main view"
    echo "2. Update the view"
    echo "3. Exit"
    read -p "Enter your choice (1-3): " choice

    case "$choice" in
        1)
            clear
            ./LinuxStatus;;
        2)
            clear;;
        3)
            out=1
            break;;
        *)
            clear
            echo "Invalid input";;
    esac
done

echo "Goodbye!"
exit
```
* Adding script to linux PATH, pwd command was `/home/yaseen` which is where the script exist
```
$ export PATH="$(pwd):$PATH"
```
* Way 1: Using command without args using `$ LinuxStatus` nad deal with minu
![image](https://user-images.githubusercontent.com/59315877/222989902-0c78dec6-b021-444d-9ed9-f645675f2190.png)
* Way 2: Using command with one or more arguments (p, r, a, and h)
![image](https://user-images.githubusercontent.com/59315877/222990078-d2f074ce-f551-45a1-a6f1-85fd1511f97d.png)


