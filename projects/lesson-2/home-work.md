gas随着员工数的变化如下：

1：transaction cost 	 23050
   execution cost 	   1778
   
2：transaction cost 	 23831
   execution cost 	   2559
   
3：transaction cost 	 24612
   execution cost 	   3340
   
4：transaction cost 	 25393
   execution cost 	   4121
   
5：transaction cost 	 26174
   execution cost 	   4902
   
6：transaction cost 	 26955
   execution cost 	   5683
   
7：transaction cost 	 27736
   execution cost 	   6464
   
8：transaction cost 	 28517
   execution cost 	   7245
   
9：transaction cost 	 29298
   execution cost 	   8026
   
10：transaction cost  30079
   execution cost 	   8807
 
从上面的数据可以看出随着员工数的增加，calculateRunWay函数消耗的gas越多，其原因是使用了for循环，员工越多，循环的次数越多，自然消耗的gas要随之增加。

解决方案：考虑到gas增加的原因是每次调用calculateRunWay函数时，for循环员工数执行累加工资导致的，因此我们要做的是考虑将计算累积工资的功能放到updateEmployee、removeEmployee以及addEmployee中进行，具体过程为：
1、定义一个全局的ntotalSalary，并初始化为0；
2、在添加员工时，ntotalSalary加上该员工的工资；
3、在更新员工工资时，根据差额修改ntotalSalary；
4、删除员工时，ntotalSalary减去该员工的工资；
5、最后在calculateRunWay中用this.balance/ntotalSalary即可。

通过上述方案不用每次都在calculateRunWay中计算工资累积金额，在有工资变化时才需计算一次，这样可以大大减少合约需要消耗的gas。