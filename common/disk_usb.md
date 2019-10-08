
# disk / usb

- df

        df -h

- du
        du -sh file_path (du = disk usage, s = summary, h = human)
        du -sh *
        du -h --max-depth=1 | sort -hr

- ls

        ls -lh

- revert bootable usb to normal

        diskutil list
        diskutil zeroDisk /dev/disk2
        disk utility app -> erase

- usb disk format

        use mac disk utility app to erase format, MS-DOS(FAT), ExtFAT
