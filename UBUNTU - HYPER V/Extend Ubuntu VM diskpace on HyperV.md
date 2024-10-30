# How to extend Ubuntu VM diskspace on Hyper V

## Step 1: Extend the disk in Hyper V
1. Shutdown the VM
2. Open Hyper V Manager
3. Right click on the VM and click on Settings
4. Click on the hard drive you want to extend
   If you have checkpoints, you will need to delete them first
5. Click on Edit
6. Increase the size of the disk
7. Click on Apply
8. Click on OK


## Step 2: Extend the partition in Ubuntu
1. Start the VM
2. Open a terminal
3. Run the following command to list the disks
   ```
   sudo cfisk    
   ```
Identify the disk you want to extend
4. Run the following command to extend the disk
   ```
   sudo cfdisk /dev/sda
   ```
5. Select the disk you want to extend
6. Select the partition you want to extend
7. Select Resize
8. Enter the new size
9. Select Write
10. Select Quit
11. Run the following command to extend the filesystem
    ```
    sudo resize2fs /dev/sda1
    ```
14. Reboot the VM
15. run cfdisk again to verify the disk size

## Alternative method using parted
1. Start the VM
2. Open a terminal
3. Run the following command to list the disks
   ```
   sudo parted
   ```
4. Type this command to list the disks and the available space
   ```
   print free
   ```
5. Identify the disk you want to extend
6. Run the following command to extend the disk
   ```
    resizepart 
   ```
7. Enter the partition number you want to extend
8. Complete the wizard
9. Now type the command `quit` to exit the parted tool
10. Run the following command to extend the filesystem
    ```
    sudo resize2fs /dev/sda1
    ```
11. Reboot the VM   
