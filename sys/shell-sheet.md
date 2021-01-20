---
title: Shell Memo
published: true
date: 2021-01-20T00:50:04.789Z
tags: 
editor: markdown
dateCreated: 2021-01-20T00:49:57.718Z
---

# Disk usage with hidden files 

````bash
$ du -sh .* *
````
or

````bash
$ GLOBIGNORE=.:.. du -sh *
82M     .git
4,0K    .gitmodules
1,3M    reactbnb-final
733K    tp0
2,2M    tp1
...
````

# Gzip copy files over hosts using cpio
````bash
SOURCE_COMMAND="set -ex; cd ${SOURCE_DIR}; find ${FIND_PARAMETERS} | cpio ${CPIO_SOURCE_PARAMETERS} | gzip"
DESTINATION_COMMAND="set -ex; cd ${DESTINATION_DIR}; gunzip | cpio ${CPIO_DESTINATION_PARAMETERS}"

ssh "${SOURCE_SERVER}" "${SOURCE_COMMAND}"     | \
    ssh "${DESTINATION_SERVER}" "${DESTINATION_COMMAND}"
````


# log current script to file, as at screen 
````bash
exec 2> >(tee -a ${STDERR_FILE})  1>  >(tee -a ${STDOUT_FILE})
echo "running ${SCRIPT_NAME} with arguments : '$@', output files : ${STDERR_FILE}, ${STDOUT_FILE}"
````

# References
- https://askubuntu.com/questions/468901/how-to-show-only-hidden-files-in-terminal
- https://stackoverflow.com/questions/692000/how-do-i-write-stderr-to-a-file-while-using-tee-with-a-pipe
