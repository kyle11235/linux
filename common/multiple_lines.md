
# multiple lines

- use EOF

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
