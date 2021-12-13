# (A) Usage of const keyword

The const keyword prevents a specific object/method/variable/pointer/object of class to modify its data items value.

### Below we will discuss some of its uses:
- **Constant variables:**
  constant variables have to be assigned value at the time of declaration (can't be left uninitialized at the time of 
  assignment or be assigned value elsewhere in the program).
  ```
  const int var; //error
  
  const int var;
  var = 5; //error
  
  const int var = 5; //correct
  ```
- **Const keyword with pointer variables:**
  There are 3 possible ways to use const keyword with a pointer:

  1. When pointer variable point to a const value.
     ```
     int x=10;
     const int* i=&x;
     x=8;
     //value of x can be changed, however the pointer is pointing to a const-int type value
     ```
  2. When the const pointer variable point to the value.
     ```
     int x=10;
     int* const i=&x;
     *i= 5;
     //the values stored in the memory location can be modified
     //however the address pointed by the pointer variable can't be changed
     //i.e. *i=&y;
     ```
  3. When const pointer pointing to a const variable.
     ```
     int x=10;
     const int* const i=&x;
     //neither the value of the variable nor the place pointed by the pointer can be changed
     ```
- **Passing const-argument value to a non-const parameter of a function cause error:**
  ```
  int fn(int x){}
  
  int main(){
  const int y=10;
  cout<<fn(y);
  //gives CTE error  
  ```
- **Constant Methods:**
  The objects of a class can also be declared as const, where they cannot be modified and hence, can invoke only const 
  member functions as these functions ensure not to modify the object.
  - When a function is declared as const, it can be called on any type of object, const object as well as non-const 
   objects.
  - Whenever an object is declared as const, it needs to be initialized at the time of declaration. However, the object initialization while declaring is possible only with the help of constructors.
  There are two ways to declare a constant function:
  1. ordinary const-function declaration.
     ```
     const void foo()
     {
     //void foo() const Not valid
     }                  
     int main()
     {
     foo(x);
     }   
     ```
  2. A const member function of the class.
     ```
     class
     {
     void foo() const
     {
     //.....
     }
     }
     ```
- **Constant function parameters and return type:**
  1. constant parameter.
     ```
     void foo(const int y)
     {
     // y = 6; const value
     // can't be change
     cout << y;
     }
     ```
  2. const return type.
  
     There is no substantial issue to pass const or non-const variable to the function because the value that will be returned by the function will be constant automatically.
     ```
     const int foo(int y)
     {
     y--;
     return y;
     }
     ```
  3. constant return type and parameter.
     ```
     const int foo(const int y)
     {
     // y = 9; it'll give CTE error as
     // y is const var its value can't
     // be change
     return y;
     }
     ```
     
*The above text was written with the help of [GeeksforGeeks](https://www.geeksforgeeks.org/const-keyword-in-cpp/).*
     

# (B) Usage of & operator

### Below we will discuss some of its uses:

- **To declare a reference to a type:**
  
  If you use & in the left-hand side of a variable declaration, it means that you expect to have a reference to the declared type. It can be used in any type of declarations (local variables, class members, method parameters).
  ```
  std::string mrSamberg("Andy");
  std::string& theBoss = mrSamberg;
  ```
- **To get the address of a variable:**

  The meaning of & changes if you use it in the right-hand side of an expression. In fact, if you use it on the left-hand side, it must be used in a variable declaration, on the right-hand side, it can be used in assignments too.

  When using it on the right-hand side of a variable, it's also known as the "address-of operator". Not surprisingly if you put it in front of a variable, it'll return its address in the memory instead of the variable's value itself. It is useful for pointer declarations.
  ```
  std::string mrSamberg("Andy");
  std::string* theBoss;

  theBoss = &mrSamberg;
  ```
- **As a bitwise operator:**
  
  It is the bitwise AND. Its an infix operator taking two numbers as inputs and doing an AND on each of the bit pairs of the inputs.


- **In a logical expression:**
  
  && in a (logical) expression is just the C-style way to say and.


- **To declare rvalue references:**

  Let's clarify first what are lvalues and rvalues and what are the differences.

  >An lvalue (locator value) represents an object that occupies some identifiable location in memory (i.e. has an address).
  >Rvalues are defined by exclusion, by saying that every expression is either an lvalue or an rvalue. Therefore, from the above definition of lvalue, an rvalue is an expression that does not represent an object occupying some identifiable location in memory.

  ```
  auto mrSamberg = std::string{"Andy"};
  ```

  mrSamberg represents an lvalue. It points to a specific place in the memory which identifies an object. On the other hand, what you can find on the right side std::string{"Andy"} is actually an rvalue. It's an expression that can't have a value assigned to, that's already the value itself. It can be only on the right-hand side of an assignment operator.


- **To  declare universal references:**

  The bad news is that && after a type might or might not mean that you are declaring an rvalue reference. In certain circumstances, it only means something that (Scott Meyers) calls a universal reference
  
  ```
  Vehicle car;
  auto&& car2 = car; // type deduction! this is a universal reference!
  Vehicle&& car3 = car; // no type deduction, so it's an rvalue reference
  ```
  
- **For funtion overloading:**

  Since C++11 you can use both the single and double ampersands as part of the function signature, but not part of the parameter list.
  
  ```
  void doSomething() &;
  void doSomething() &&;
  auto doSomethingElse() & -> int;
  auto doSomethingElse() && -> int;
  ```

  What this means is that you can limit the use of a member function based on whether *this is a lvalue or an rvalue. So you can only use this feature within classes, of course.
  
  ```
  class Tool {
  public:
  // ...
  void doSomething() &; // used when *this is a lvalue
  void doSomething() &&; // used when *this is a rvalue
  };

  Tool makeTool(); //a factory function returning an rvalue

  Tool t; // t is an lvalue

  t.doSomething(); // Tool::doSomething & is called

  makeTool().doSomething(); // Tool::doSomething && is called
  ```
  
*The above text was written with the help of [dev](https://dev.to/sandordargo/how-to-use-ampersands-in-c-3kga).*