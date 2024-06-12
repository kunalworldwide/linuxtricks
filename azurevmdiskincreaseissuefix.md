## How to Fix Azure VM Not Showing Updated Disk Space

When you resize a disk on an Azure VM, sometimes the operating system does not automatically recognize the new disk size. This guide provides a step-by-step process to ensure your Azure VM uses the updated disk space.

### Prerequisites

- Access to the Azure portal.
- SSH or console access to the Azure VM.
- Administrative privileges on the VM.

### Steps to Fix Disk Space Issue

1. **Resize the Disk in Azure Portal:**

   1.1. Go to the Azure portal and navigate to your VM.

   1.2. In the left menu, click on `Disks`.

   1.3. Select the disk you want to resize.

   1.4. Click on `Size + performance`.

   1.5. Enter the new disk size and save the changes.

2. **Verify the Disk Size in the VM:**

   After resizing the disk in the Azure portal, log into your VM and verify the disk size:

   ```sh
   sudo fdisk -l
   ```

   Ensure that the disk reflects the new size.

3. **Resize the Partition:**

   3.1. Identify the disk and partition. For example, if your disk is `/dev/sda` and the partition is `/dev/sda1`, you should see it listed.

   3.2. Use `fdisk` or `parted` to resize the partition to use the full disk space:

   ```sh
   sudo fdisk /dev/sda
   ```

   - Delete the existing partition using the `d` command.
   - Create a new partition using the `n` command.
   - Set the same start sector as the old partition, and the end sector to the maximum size.
   - Write the changes using the `w` command.

4. **Resize the Filesystem:**

   Depending on your filesystem type (`ext4` or `xfs`), use the appropriate command to resize the filesystem.

   - For `ext4` Filesystem:

     ```sh
     sudo resize2fs /dev/sda1
     ```

   - For `xfs` Filesystem:

     ```sh
     sudo xfs_growfs /
     ```

5. **Verify the Filesystem Resize:**

   Use the `df -h` command to verify that the filesystem now reflects the updated disk size.

   ```sh
   df -h
   ```

6. **Check Disk Usage with `ncdu`:**

   Install and use `ncdu` to visualize disk usage before and after the changes.

   - Install `ncdu` (if not already installed):

     ```sh
     sudo apt-get install ncdu -y
     ```

   - Check disk usage:

     ```sh
     sudo ncdu /
     ```

### Example Commands

#### Step-by-Step for `ext4` Filesystem:

1. **Resize Partition with `fdisk`:**

   ```sh
   sudo fdisk /dev/sda
   ```

   - Press `d` to delete the existing partition.
   - Press `n` to create a new partition.
   - Select the same start sector as the old partition.
   - Select the end sector to use the entire disk.
   - Press `w` to write changes and exit.

2. **Resize Filesystem:**

   ```sh
   sudo resize2fs /dev/sda1
   ```

3. **Verify the New Size:**

   ```sh
   df -h
   ```

4. **Check Disk Usage with `ncdu`:**

   ```sh
   sudo apt-get install ncdu -y
   sudo ncdu /
   ```

#### Step-by-Step for `xfs` Filesystem:

1. **Resize Partition with `fdisk`:**

   ```sh
   sudo fdisk /dev/sda
   ```

   - Press `d` to delete the existing partition.
   - Press `n` to create a new partition.
   - Select the same start sector as the old partition.
   - Select the end sector to use the entire disk.
   - Press `w` to write changes and exit.

2. **Resize Filesystem:**

   ```sh
   sudo xfs_growfs /
   ```

3. **Verify the New Size:**

   ```sh
   df -h
   ```

4. **Check Disk Usage with `ncdu`:**

   ```sh
   sudo apt-get install ncdu -y
   sudo ncdu /
   ```
