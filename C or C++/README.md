# C and C++
## Basic syntax
```
import cpp

from /* ... variable declarations ... */
where /* ... logical formulas ... */
select /* ... expressions ... */
```
## Basic class
 - Function: just function
 - FunctionCall: where function is called
 - Variable: just variables
 - Expr: expression
    - AssignExpr
    - AddExpr
    - ...
 - Stmt: statement
    - WhileStmt
    - ForStmt
    - IfStmt
    - ...
## Simple query
```
// This query will get all malloc call with size > 1000
import cpp

from Function f, FunctionCall fc
where f = fc.getTarget()
and f.hasQualifiedName("malloc")
and fc.getArgument('1').getValue().toInt() > 1000
select fc, fc.getFile()
```
## Create your own class
 - You can create ur own class to define and reuse some popular target, make ur query nice and clear
```
// create malloc class
import cpp

class mallocCall extends FunctionCall
{
  // consider as a constructor
  mallocCall()
  {
    this.getTarget().hasQualifiedName("malloc")
  }
  
  // get malloc size
  Expr getSize()
  {
    result = this.getArgument(0)
  }
}

// then u can use it in like above example
from mallocCall malloc
where malloc.getSize().getValue().toInt() > 1000
select malloc
```
## Create predicate
 - Predicates are used to describe the logical relations
 - When u need to write complex and long query, u can combine both class and predicate to make it ez to read and reuse
```
//check if malloc call
import cpp
predicate isMalloc(FunctionCall fc)
{
  fc.getTarget().hasQualifiedName("malloc")
}

from FunctionCall fc
where isMalloc(fc)
select fc, "malloc call"
```
## Data flow
 - Analyze data flow in your project
 - Below example will find which paramter in functions will be used in fopen
```
// import library
import cpp
import semmle.code.cpp.dataflow.DataFlow


from Function fopen, FunctionCall fc, Parameter src
where fopen.hasQualifiedName("fopen") // find fopen
  and fc.getTarget() = fopen
  and DataFlow::localFlow(DataFlow::parameterNode(src), DataFlow::exprNode(fc.getArgument(0))) 
  // find parameter which will be used in fopen
select src
```
 
## And so on
 - There are so many classes and libraries in QL that can't list all here
 - QL is usually used to find known type vulnerabilities that we know it's pattern
 - Finding new type may be hard 
