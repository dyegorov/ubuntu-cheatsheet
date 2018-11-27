# ubuntu-cheatsheet

# PS with git branch and new line
```
$ cat ~/.bash_profile
parse_git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export PS1="\[\033[32m\]\w\[\033[33m\]\$(parse_git_branch)\[\033[00m\]\n$ "
```
* Better move it to .bashrc to auto enable on terminal run from gui
* [look here why](https://askubuntu.com/questions/121073/why-bash-profile-is-not-getting-sourced-when-opening-a-terminal)
# Update VS Code
```
$ cat ~/update-code 
wget https://vscode-update.azurewebsites.net/latest/linux-deb-x64/stable -O /tmp/code_latest_amd64.deb
sudo dpkg -i /tmp/code_latest_amd64.deb
```
# Install local deb pkg with failed deps
```
$ sudo dpkg -i mysql-workbench-community-6.2.5-1ubu1404-amd64.deb 
error! (some deps missing)
ok
$ sudo apt-get update
$ sudo apt-get install -f
$ sudo dpkg -i mysql-workbench-community-6.2.5-1ubu1404-amd64.deb 
```
# view free ram
```
watch -n 5 free -m
```
Note that Linux likes to use any extra memory to cache hard drive blocks. So you don't want to look at just the free Mem. You want to look at the free column of the -/+ buffers/cache: row. 

# view who listens ports
```
sudo netstat -ntlp | grep LISTEN
```

# mysql
## connect
```
mysql -uroot -proot -D db_name -h 192.168.1.1
```

## backup db
```
$ mysqldump -uroot -proot db_name > db_name.sql
```

## restore db
```
mysql -uroot -proot db_name < db_name.sql
```

# mongodb
[https://docs.mongodb.com/](https://docs.mongodb.com/)
***
[mongo Shell Quick Reference](https://docs.mongodb.com/manual/reference/mongo-shell/)
***
* document model (db -> collection -> document/object). document = JSON object
* no joins
* no complex trns
* schemas are flexible
* documents stored as BSON (binary JSON)
* memory-mapped files
* B-tree indexes

## start manually
```
$ mongod
```
## connect
```
$ mongo
```
## view available dbs
```
> show dbs
admin         0.000GB
config        0.000GB
```
## choose current db
```
> use config
```
## drop db
```
> use parsuna
switched to db parsuna
> db.dropDatabase()
{ "dropped" : "parsuna", "ok" : 1 }
```
## view collections
```
> show collections
abouts
albums
```
## drop collection
```
> db.students.drop()
```
## select *  
```
> db.albums.find();
> db.albums.find({});
```
## select by id  
```
> db.inventory.find( { status: "D" } )
> db.albums.find({"_id": ObjectId("5b36317727a1947c49fbac4e")})
> db.albums.find({_id: ObjectId("5b36317727a1947c49fbac4e")})
```
better formatted:
```
> db.albums.findOne({_id: ObjectId("5b36317727a1947c49fbac4e")})
```
## select where equal
```
> db.posts.find({ author.name: “mike” })
```
## select greater than
```
> db.posts.find({ rating: { $gt: 2 }})
```
## select with sort and limit
```
db.posts.find().sort({date: -1}).limit(10)
```