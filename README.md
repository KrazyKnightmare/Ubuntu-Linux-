# Ubuntu-Linux-
Ubuntu Linux Script to help with automation in AWS 
Updates Ubuntu to the Latest Version: It checks for updates and upgrades the system to the latest available packages.

Checks All Files and Directories: It lists all files and directories within Ubuntu and logs their locations.

Identifies the EC2 Instance and AWS Cloud Console: The script will fetch the EC2 instance metadata and the AWS instance ID to log which EC2 instance the script is running on.

Tracks the Last Power User: It checks the system logs to determine the last active user who had elevated (sudo) privileges.

Script Breakdown:
Update the System:

The script starts by updating the system using sudo apt update && sudo apt upgrade -y to make sure the system is up to date.

List All Files and Directories:

It uses find / -type f to recursively list all files in the system and stores the result in /home/$(whoami)/file_list.txt.

EC2 Metadata:

If the script is running on an EC2 instance (it checks for /sys/hypervisor/uuid), it fetches EC2 instance details like the instance ID, public IP address, and region by querying the instance metadata service (http://169.254.169.254/latest/meta-data/).

Track the Last User with Sudo Privileges:

The script checks the authentication logs (/var/log/auth.log) to identify the last user who used sudo. It uses grep 'sudo:' to filter out sudo-related entries and grabs the most recent one.

Output Information:

It saves the information about files, EC2 metadata, and the last sudo user to text files in the current user's home directory (/home/$(whoami)).

User Interaction:

The script asks if it can proceed with the actions (updating, checking files, etc.), and it uses echo to communicate the actions.

Logs:

The information is logged to three text files:

/home/$(whoami)/file_list.txt: Contains the list of files and directories.

/home/$(whoami)/ec2_instance_info.txt: Contains EC2 instance metadata.

/home/$(whoami)/last_power_user.txt: Contains the last user who used sudo.

How to Use:
Save the Script: Copy the script to a file (e.g., ubuntu_update_and_check.sh).

Make the Script Executable:

chmod +x ubuntu_update_and_check.sh
Run the Script:

./ubuntu_update_and_check.sh
Notes:
Ensure you have root privileges to run this script, as it requires access to update the system, check EC2 metadata, and read authentication logs.

The script will save all logs to the current user's home directory (/home/$(whoami)), which can be modified as per your preference.

The EC2 instance metadata will only work if the script is executed on an actual EC2 instance.
