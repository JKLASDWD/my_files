

https://github.com/skilion/onedrive/



在Ubuntu上同步文件至Onedrive



按页面上的教程在系统上安装好Onedrive后，在~/.config/onedrive/config对配置文件进行书写





```
# Directory where the files will be synced

sync_dir = "~/OneDrive"

\# Skip files and directories that match this pattern

skip_file = ".*|~*"
```



sync_dir 对应的是当前系统下的某个文件夹，在这个文件夹下的文件会与Onedrive的文件进行同步，进行上传和下载

skip_file 可以使用*和?对要匹配的文件进行筛选，过滤掉不想同步的文件



```
Selective sync
Selective sync allows you to sync only specific files and directories. To enable selective sync create a file named sync_list in ~/.config/onedrive. Each line of the file represents a relative path from your sync_dir. All files and directories not matching any line of the file will be skipped during all operations. Here is an example of sync_list:

Backup
Documents/latest_report.docx
Work/ProjectX
notes.txt
```

创建sync_list文件可以对要同步的文件/文件夹进行更严格的筛选，仅同步自己想要的文件/文件夹

(建议使用这个，好用)



在命令行输入onedrive后，会对sync_dir文件夹下的文件和onedrive对应的文件进行同步，第一次使用会弹出链接，进行授权，将返回链接输入到命令行即授权完成

接下来就可以开始文件的同步了