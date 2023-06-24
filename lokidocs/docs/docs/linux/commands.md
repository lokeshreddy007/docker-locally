## ls command

| commands | Description                                            |
| -------- | ------------------------------------------------------ |
| ls -a    | list all files including hidden file starting with '.' |
| ls -i    | list file's inode index number                         |
| ls -l    | list with long format - show permissions               |
| ls -la   | list long format including hidden files                |
| ls -lh   | list long format with readable file size               |
| ls -ls   | list with long format with file size                   |
| ls -r    | list in reverse order                                  |
| ls -R    | list recursively directory tree                        |
| ls -s    | list file size                                         |
| ls -S    | sort by file size                                      |
| ls -t    | sort by time & date                                    |
| ls -X    | sort by extension name                                 |

## Utility Commands

#### Current Working directory

```bash
pwd
```

#### Navigation

```bash
# Navigate to the last directory you were working in
cd -

# Navigate to the current user's home directory.
cd ~

# Go to the parent directory of current directory (mind the space between cd and ..)
cd ..
```

#### Copy

```bash
# Will copy the file from source to destination. -p stands for preservation. It preserves the original attributes of file while copying like file owner, timestamp, group, permissions etc
cp -p source destination

# Will copy source directory to specified destination recursively
cp -R source_dir destination_dir
```

#### Move

```bash

# In Linux there is no rename command as such. Hence mv moves/renames the file1 to file2.
mv file1 file2
```

#### Create file

```bash
touch filename
```

#### Make directory

```bash

# Create a directory dir-name
mkdir dir-name

# Create a directory hierarchy. Create parent directories as needed, if they don't exist. You can specify multiple directories.
mkdir -p dir-name/dir-name
```

#### Remove File

```bash
rm filename

# Will remove the directory dir-name recursively
rm -R dir-name

# Will remove the directory dir recursively, ignoring non-existent files and will never prompt for anything. BE CAREFUL USING THIS COMMAND! You can specify multiple directories.

rm -rf dir-name
```

#### View Content

```bash
cat myFirstFile

# View the content of a file with pager (one screenful at a time):
less myFirstFile

# View the first several lines of a file
head myFirstFile

# View the last several lines of a file
tail myFirstFile
tail -n 3 state.txt
tail -3 state.txt
tail -n 3 hello.txt fine.txt
# This option shows the last ten lines of a file and will update when new lines are added
tail -f error.log


```

| Commands                                       | Description                                                                                                                                                                                                                       |
| ---------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| man <name>                                     | Read the manual page of <name>.                                                                                                                                                                                                   |
| man <section>                                  | <name> Read the manual page of <name> related to the given section.                                                                                                                                                               |
| man -k <editor>                                | Output all the software whose man pages contain <editor> keyword.                                                                                                                                                                 |
| man -K <keyword>                               | Outputs all man pages containing <keyword> within them.                                                                                                                                                                           |
| apropos <editor>                               | Output all the applications whose one line description matches the word editor.When not able to recall the name of the application use this command.help In Bash shell this will display the list of all available bash commands. |
| help <name>                                    | In Bash shell this will display the info about the <name> bash command.                                                                                                                                                           |
| info <name>                                    | View all the information about <name>.                                                                                                                                                                                            |
| dpkg -l                                        | Output a list of all installed packages on a Debian-based system.                                                                                                                                                                 |
| dpkg -L                                        | packageName Will list out the files installed and path details for a given package on Debian.                                                                                                                                     |
| dpkg -l &#124; grep -i <edit>                  | Return all .deb installed packages with <edit> irrespective of cases.                                                                                                                                                             |
| less /var/lib/dpkg/available                   | Return descriptions of all available packages.                                                                                                                                                                                    |
| whatis vim List a one-line description of vim. |                                                                                                                                                                                                                                   |
| <command-name> --help                          | Display usage information about the <tool-name>. Sometimes command -h also works but not for all commands                                                                                                                         |

#### Tree representation of the file system

```bash

# install
sudo apt install tree

# use
tree folder_name
```
