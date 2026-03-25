## Task 8: Bonus — Quick Reference Table
Topic          	Key Syntax	            Example
Variable	      VAR="value"           	NAME="DevOps"
Argument	        $1, $2	            ./script.sh arg1
If	           if [ cond ]; then	    if [ -f file ]; then
For loop	      for i in list; do	    for i in 1 2 3; do
Function	          name() {}	        greet() { echo "Hi"; }
Grep	           grep pattern file	   grep -i "error" log.txt
Awk	             awk '{print $1}'	     awk -F: '{print $1}' file
Sed              sed 's/old/new/g'	   sed -i 's/foo/bar/g' file

## Task 1: Basics
1. Shebang (#!/bin/bash) - Tells system which interpreter to use.
2. Running a script -chmod +x script.sh 
                     ./script.sh
3. Comments - echo "Hello" # Inline comment
4. Variables - NAME="Manjunath" 
               echo $NAME
               echo "$NAME"
               echo '$NAME'
5. User Input - read -p "Enter name: " NAME 
                 echo $NAME
6. Command-line Arguments
    echo $0  # script name
    echo $1  # first arg
    echo $#  # number of args
    echo $@  # all args
    echo $?  # last command status

## Task 2: Operators and Conditionals
1. String comparisons -
      [ "$a" = "$b" ]
      [ "$a" != "$b" ]
      [ -z "$a" ]
      [ -n "$a" ]
2. Integer Comparisons -
          [ $a -eq $b ]
          [ $a -ne $b ]
          [ $a -lt $b ]
          [  $a -gt $b ]
3. File test operators -
    [ -f file ] # file exists
    [ -d dir ] # directory
    [ -r file ] # readable
4. if-Else
      if [ condition ]; then
        echo "Yes"
      elif [ condition ]; then
        echo "Maybe"
      else
        echo "No"
      fi
5. Logical operators -
   [ condition ] && echo "True"
   [ condition ] || echo "False"
   ! [ condition ]

6. Case statements -
         case $var in
           start) echo "Start";;
           stop) echo "Stop";;
           *) echo "Unknown";;
         esac
## Task 3: Loops
 1. For Loop
      for i in 1 2 3; do
      echo $i
      done
2. C-style For
     for ((i=0;i<5;i++)); do
      echo $i
    done
3. While Loop
      while read line; do
        echo $line
      done < file.txt
4. Until Loop
      until [ $a -gt 5 ]; do
        ((a++))
      done
5. Loop Control
      break
      continue
6. Loop Files
      for file in *.log; do
        echo $file
      done
## Task 4: Functions
  1&2. Define & Call
            greet() {
              echo "Hello"
            }
            greet
  3. Arguments
            func() {
              echo $1
            }
            func "Hi"
  4. Return vs Echo
          return 1   # exit code
          echo "data" # output
  5. Local Variables
          func() {
            local var="test"
          }
## Task 5: Text Processing Commands
  1. grep
        grep -i "error" file
        grep -r "text" .
        grep -n "line" file
  2.awk
        awk '{print $1}' file
        awk -F: '{print $1}' /etc/passwd
  3.sed
        sed 's/old/new/g' file
        sed -i 's/foo/bar/g' file
  4.cut
        cut -d: -f1 file
  5.sort
        sort file
        sort -n file
        sort -r file
        sort -u file
  6.uniq
        uniq file
        uniq -c file
  7.tr
        tr 'a-z' 'A-Z'
        tr -d 'a'
  8.wc
        wc -l file 
        wc -w file
  9.head / tail
        head -n 5 file
        tail -f file
## Task 6: Useful Patterns and One-Liners
  1. Delete files older than 7 days
        find . -type f -mtime +7 -delete
  2. Count lines in .log files
        wc -l *.log
  3. Replace text in multiple files
        sed -i 's/old/new/g' *.txt
  4.Check if service is running
        ps aux | grep nginx
  5. Disk usage alert
        df -h | awk '$5 > 80 {print "High usage:", $0}'
  6. Tail logs with error filter
        tail -f app.log | grep --line-buffered "ERROR"
## ask 7: Error Handling & Debugging
1. Exit Codes
    exit 0
    exit 1
    echo $?
2. set -e  # exit on error
3. set -u  # undefined vars error
4. set -o pipefail
3. Debug Mode
4. set -x
5. Trap
trap 'echo "Cleaning up"; rm temp.txt' EXIT
             
