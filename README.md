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


4. 小红书sql题：选出5月分和6月份总gmv最高的前50个商家，输出要求两列：一列月份（2019M5表示5月），一列seller_name
select p1.月份,p1.seller_name from ( select '2019M5' as 月份, seller_name,sum(gmv) as sum       
from purchase       
where month(dt)=5           
group by seller_name          
order by sum          
limit 50) p1          
union               
select p2.月份,p2.eller_name from             
( select '2019M6' as 月份, seller_name,sum(gmv) as sum                
from purchase             
where month(dt)=6               
group by seller_name              
order by sum              
limit 50) p2;            

#DP问题
#题目：最大奇数约数之合          
#例如f(44) = 11           
#输入：n  输出：f(n)+f(n-1)+....+f(1)               

def f(x):                   
    if x%2 == 1:                    
        return x                        
    else:                           
        x /= 2                            
        return f(x)                         
                
def dp(n):                          
    if n == 1:                      
        return 1                        
    else:                             
        mem = [0 for x in range(n)]                           
        mem[0] = 1                            
        for i in range(1,n):                          
            mem[i] = f(i+1) + mem[i-1]                            
    return int(mem[-1])                             
        



