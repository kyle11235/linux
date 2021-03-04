# vi

- shell go to beginning/end

        ctrl + a/e

- cat multiple lines into file

        cat <<EOF > hi.txt
        hello
        EOF

        cat <<EOF > hello.go
        package main

        import (
            "fmt"
            "rsc.io/quote"
        )

        func main() {
            fmt.Println(quote.Hello())
        }
        EOF

- vi

        - go to line
        1G -> line1
        2G -> line2
        G  -> last line
        
        - go to column
        shift + 4($) -> end
        shift + 6(^) -> begin
        
        - edit
        dd = delete line
        x = delete current character

        - find next
        /hello (hit enter)
        click enter, use 'n' to find next

        - find previous
        ?hello (hit enter)
        click enter, use 'n' to find previous

- sed

        - find （better to print into new file & compare）
        
                sed -n '/old/p' ./hello.txt

        - print, not replace 

                sed 's/old/new/g' ./hello.txt

        - replace

                oldold -> newnew
                sed -i 's/old/new/g' ./hello.txt

        - only replace 1st of each row (no g)

                oldold -> newold
                sed -i 's/old/new/' ./hello.txt

        - mac (gengrate hello.txt_bak)
                
                sed -i "_bak" 's/old/new/g' ./hello.txt

        
        - prepend
        - append

- awk

