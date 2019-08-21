# brew_install_mongodb

1.Install brew (if you do not have homebrew)                       
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"            
2.Update and verify you are good with               
brew update             
brew doctor              
3.Install mongodb with               
brew install mongodb                   
4.Create folder for mongo data files:              
mkdir -p /data/db                
5.Set permissions                      
sudo chown -R `id -un` /data/db                  
6.Open another terminal window & run and keep running a mongo server/daemon     
mongod      
7.Return to previous terminal and run a mongodb shell to access data:       
mongo   


##################################################
## how to drop database in Mongodb
use dbname
db.dropDatabase()
