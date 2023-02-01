# Unix Shell

```ps ax```

```ls –al```

```ps ax > myfile.out```
saves the list of all running processes to a file named "myfile.out"

```head myfile.out```  - displays the first 10 lines of the file "myfile.out"

```grep “eclipse” myfile.out``` performs a search for the string "eclipse" in the file "myfile.out"

```ps ax | grep eclipse``` list all of the processes running on the system and then filter the output to only show the lines that contain the string "eclipse"

```ps ax | more``` list all of the processes running on the system and then display the output one screenful at a time

*```more``` - allows to view the output one screenful at a time and navigate through the output by pressing the "space" bar to go to the next page, or the "q" key to exit.*

*```wc``` - word count*
