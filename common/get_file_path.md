
# file path

- full file path

        SHELL_DIR=$(dirname "$BASH_SOURCE")
        APP_DIR=$(cd $SHELL_DIR; pwd)

- full file path, support softlink

        DIR=`S=\`readlink "$0"\`; [ -z "$S" ] && S=$0; dirname $S`
        echo $DIR
