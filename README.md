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

#################################################
## SQL practice
1. 查找奇数行姓名        
select e.first_name     
from employees e        
join        
(select first_name,row_number() over(order by first_name asc) as row_no           
from employees) as t          
on e.first_name = t.first_name and t.row_no % 2 = 1;          

