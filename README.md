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

2. table中有studentId, studentName, courseId, Score, 找出每个课程最高分的前两位同学。
select a.studentId, a.studentName, a.courseId, a.Score
from (select *, row_number() over (order by courseId, Score desc limit 2) as row_num from table) as a;

3. 对一个表新增一列，为每一行之前（包括自己）所有员工的工资之合               
select s1.emp_no, s1.salary,            
(select sum(s2.salary) from salaries s2           
where s2.emp_no <= s1.emp_no and s2.to_date = '9999-01-01') as running_total        
from salaries s1 where s1.to_date = '9999-01-01';         
###思想：子表用两个一样的表做和，如果s1.row>=s2.row则在s2求和as running_total，再select running_total###






