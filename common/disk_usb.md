
# disk / usb

- df

        df -h

- du
        
        du -sh file_path (du = disk usage, s = summary, h = human)
        
        - current folder
        du -sh *
        
        - child folder without current
        du -h --max-depth=1 | sort -hr

- ls

        ls -lh

- revert bootable usb to normal

        - mac/ubuntu?
        diskutil list
        diskutil zeroDisk /dev/disk2
        disk utility app -> erase
        
        - win
        find disk name in device manager e.g. disk 1
        cmd -> diskpart -> select disk 1 -> clean
        new volume in disk manager

- usb disk format

        use mac disk utility app to erase format, MS-DOS(FAT), ExtFAT
