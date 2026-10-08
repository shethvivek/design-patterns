SOLID is basically 5 principles, which will help to create a good software architecture.</br></br>
You can see that all design patterns are based on these principles. SOLID is basically an acronym of the following:

* **S** is single responsibility principle (SRP)
* **O** stands for open closed principle (OCP)
* **L** Liskov substitution principle (LSP)
* **I** interface segregation principle (ISP)
* **D** Dependency injection principle (DIP)

<h2>1.1 Single responsibility principle (SRP)</h2>

<p style="text-indent: 2px;">A class should take one responsibility and there should be one reason to change that class. Now what does that mean? I want to share one picture to give a clear idea about this.</p>


Now see this tool is a combination of so many different tools like knife, nail cutter, screw driver, etc. So will you want to buy this tool?</br></br>
I don’t think so. Because there is a problem with this tool, if you want to add any other tool to it, then you need to change the base and that is not good.</br></br>
This is a bad architecture to introduce into any system. It will be better if nail cutter can only be used to cut the nail or knife can only be used to cut vegetables.

![Image1](./images/SRP1.png)

<p style="text-indent: 2px;"><b>'Employee'</b> class is taking 2 responsibilities, one is to take responsibility of employee database operation and another one is to generate employee report. </br></br> <b>Employee</b> class should not take the report generation responsibility because suppose some days after your customer asked you to give a facility to generate the report in Excel or any other reporting format, then this class will need to be changed and that is not good.

So according to SRP, <b><ins>one class should take one responsibility</ins></b> so we should write one <ins>different class</ins> for report generation, so that any change in report generation should not affect the ‘Employee’ class.</p>

![Image1](./images/SRP2.png)

<h2>2.2 Open closed principle (OCP)</h2>

Now take the same <b>‘ReportGeneration’</b> class as an example of this principle. Can you guess what is the problem with the below class!!

![Image1](./images/OCP1.png)

Brilliant!! Yes you are right, <b>too much ‘If’ clauses</b> are there and if we want to introduce another new report type like ‘Excel’, then you need to write another ‘if’. </br></br><b> This class should be open for extension but closed for modification.</b> But how to do that!!

![Image1](./images/OCP2.png)

So if you want to introduce a new report type, then just <b>__inherit__</b> from <b>IReportGeneration.</b></br></br> So <b>IReportGeneration</b> is <b><ins>open for extension</ins></b> but <b><ins>closed for modification.</ins></b>

<h2>2.3 Liskov substitution principle (LSP)</h2>

<p style="text-indent: 20px;">This principle is simple but very important to understand. <b><ins>Child class should not break parent class’s type definition and behavior.</ins></b>
</br></br>Now what is the meaning of this!! Ok let me take the same <b>employee</b> example to make you understand this principle.</br></br>Check the below picture. <ins>Employee is a parent class</ins> and <b>Casual</b> and <b>Contractual</b> employee are the <ins>child classes</ins>, inhering from <b>employee</b> class.</p>

<img src="./images/LSP0.png" alt="Description" width="300" height="200">
</br>
Now see the below code :
</br></br>
<img src="./images/LSP1.png">
Up to this is fine right?
</br></br>Now, check the below code and it will <b>violate the LSP principle.</b>

<img src="./images/LSP2.png">
Now I guess you got the problem.</br></br>Yes right, for <b>contractual employee,</b> you will get not implemented exception and that is violating LSP.</br></br>Then what is the solution?</br></br><b>Break the whole thing in 2 different interfaces,</b></br> 1. IProject</br> 2. IEmployee </br> and implement according to employee type.
</br></br>
<img src="./images/LSP3.png">

<h2>2.4 Interface segregation principle (ISP)</h2>

<p style="text-indent: 2px;">This principle states that <b>any client should not be forced to use an interface which is irrelevant to it.</b></br></br>Now what does this mean, suppose there is one database for storing data of all types of employees (i.e. Permanent, non-permanent), </br></br> what will be the best approach for our interface?</p>
<img src="./images/ISP1.png">
And all types of employee class will inherit this interface for saving data. This is fine right? Now suppose that company one day told to you that they want to read only data of permanent employees. What you will do, just add one method to this interface?</br></br>
<img src="./images/ISP2.png">
But now we are breaking something. We are forcing <b><ins>non-permanent employee</b></ins> class to show their details from database.</br></br> So, the solution is to <b><ins>give this responsibility to another interface.</b></ins>
</br>
<img src="./images/ISP3.png">
And <b>non-permanent</b> employee will implement <b>only IAddOperation</b> and <b>permanent employee</b> will implement <b>both the interface.</b>

<h2>2.5 Dependency inversion principle (DIP)</h2>
<p style="text-indent: 2px;">This principle tells <b><ins>you not to write any tightly coupled code because that is a nightmare to maintain when the application is growing bigger and bigger.</ins></b> If a class depends on another class, then we need to change one class if something changes in that dependent class. </br></br><b><ins>We should always try to write loosely coupled class.</ins></b></p>

<p style="text-indent: 2px;">Suppose there is one notification system after saving some details into database.</p>

<img src="./images/DI1.png">

Now <b>Notification class</b> totally depends on <b>Email class,</b> because it only sends one type of notification.</br></br> If we want to introduce any other like SMS then? We need to <b>change</b> the notification system also. And this is called <b>tightly coupled.</b>
</br></br>What can we do to make it loosely coupled?
</br>Ok, check the following implementation.</br></br>
<img src="./images/DI2.png">


Still Notification class depends on Email class. Now, we can use <b><ins>dependency injection</ins></b> so that we can make it loosely coupled. </br></br>There are 3 types to DI, Constructor injection, Property injection and method injection.

<b>Constructor Injection</b></br>
<img src="./images/DI3.png">

<b>Property Injection</b></br>
<img src="./images/DI4.png">

<b>Method Injection</b></br>
<img src="./images/DI5.png">

</br></br>SOLID principle will help us to write <b>loosely coupled code</b> which is <b>highly maintainable</b> and less error prone.
