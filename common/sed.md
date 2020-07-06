
- print, not replace 

        sed  's/old/new/' ./hello.txt
        
- replace 1st of each row (-i)

        oldold -> newold

        - linux, 
        sed -i 's/old/new/' ./hello.txt

        - mac (gengrate hello.txt_bak)
        sed -i "_bak" 's/old/new/' ./hello.txt

- replace everyone (/g)

        oldold -> newnew

        sed 's/old/new/g' ./hello.txt

- prepend
- append
