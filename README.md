# SaraElwatany.github.io




# 1.Const:

### 1.1.The const keyword specifies that a variable's value is constant and tells the compiler to prevent the programmer from modifying it.

**int const x = 5;**

or

**const int x = 5;**



### 1.2.You can also use it to modify the size of the array.

**const int maxarray = 255;**

**char store_char[maxarray];**





### 1.3.In pointer declarations

*We cannot change the pointer.

**char *mybuf = 0, *yourbuf;**
   
  **char *const aptr = mybuf;**
   
   ***aptr = 'a';**   // OK
   
   **aptr = yourbuf;**   // C3892(Error)

*We cannot change the data and also constant data must be assigned to constant pointers.

**const char *mybuf = "test";**
   
   **char *yourbuf = "test2";**
   
   **printf_s("%s\n", mybuf);**

  **const char *bptr = mybuf;**   // Pointer to constant data
  
  **printf_s("%s\n", bptr);**

   // *bptr = 'a';  // Error





### 1.4.const member functions
Declaring a member function with the const keyword specifies that the function is a
"read-only" function. The const keyword is required in both the declaration and the
 definition. const objects can only access const functions, while const functions can be called
 by both const and not const objects.

**class Date {**

**public:**
   
   **Date( int mn, int dy, int yr );**
   
   **int getMonth() const;**     // A read-only function
   
   **void setMonth( int mn );**   // A write function; can't be const

**private:**
  
  **int month;  };**

**int Date::getMonth() const  {**
  
  **return month;**        // Doesn't modify anything   **}**

**void Date::setMonth( int mn ) {**
  
  **month = mn;**          // Modifies data member  **}**

**int main() {**
  
  **Date MyDate( 7, 4, 1998 );**
  
  **const Date BirthDate( 1, 18, 1953 );**
  
  **MyDate.setMonth( 4 );**    // Okay
  
  **BirthDate.getMonth();**    // Okay
   
   **BirthDate.setMonth( 4 );** // C2662 Error  **}**







### 1.5.For const return type and const parameter 


**const int foo(const int y){**
   
   // y = 9; it'll give CTE error as
    
   // y is const var its value can't
    
   // be changed
    
   **return y;  }**
 

   **int main() {**    // Driver code
   
   **int x = 9;**
    
   **const int z = 10;**
    
   **cout << foo(x) << '\n'**
       
   **<< foo(z);**
 
   **return 0;   }**



   

### 1.6.Const iterators
Since iterators can also be used to modify the underlying collection.
when an STL collection is declared const, then any iterators used over the collection 
must be const iterators. They're just like normal iterators, except that they cannot be
used to modify the underlying data. (Since iterators are a generalization of the idea of pointers).

  std::vector<int>vec;

   **vec.push_back( 3 );**

   **vec.push_back( 4 );**

   **vec.push_back( 8 );**
 
**for ( std::vector<int>::const_iterator itr = vec.begin(), end = vec.end(); itr != end;++itr )**  **{** // just print out the values...
        
   std::cout<< *itr <<std::endl;

   **}**





### 1.7.Const cast

Sometimes, you have a const variable and you want to pass it into a function that you are certain won't modify it. But that function doesn't declare its argument as const.
Fortunately, if you know that you are safe in passing a const variable into a function that doesn't explicitly indicate that it will not change the data, then you can use a **const_cast** in order to temporarily strip away the const-ness of the object.


// a bad version of strlen that doesn't declare its argument const

   int **bad_strlen** (char *x) {
        
	strlen( x ); }
 
// note that the extra const is actually implicit in this declaration since
// string literals are constant

	const char *x = "abc";
 
// cast away const-ness for our strlen function 

	bad_strlen( const_cast<char *>(x) );










# 2.&:

### 2.1.Bitwise AND
The bitwise AND operator (&) compares each bit of the first operand to that bit of the second operand. If both bits are 1, the bit is set to 1. Otherwise, the bit is set to 0. Both operands to the bitwise **AND** operator must be of integral types. 
 
**int main() {**  
  
   **unsigned short a = 0x5555;**      // pattern 0101 ...  
   
   **unsigned short b = 0xAAAA;**      // pattern 1010 ...  

   **cout << hex << ( a & b ) << endl;  }**


### 2.2.&& OPERATOR (and)

   **( (5 == 5) && (3 > 6) )**  // evaluates to false ( true && false )


### 2.3.&&to declare a universal reference 

   -If the expression initializing a universal reference is an lvalue, the universal reference becomes an lvalue reference.

   -If the expression initializing the universal reference is an rvalue, the universal reference becomes an rvalue reference.



   >*If you can take the address of an expression, the expression is an lvalue.*

   >*If the type of an expression is an lvalue reference (e.g., T& or const T&, etc.), that expression is an lvalue. Otherwise, the expression is an rvalue.  Conceptually (and >typically also in fact), rvalues correspond to temporary objects, such as those returned from functions or created through implicit type conversions. Most literal values (e.g., >10 and 5.3) are also rvalues.*


	1.template<typename T>
	
   2.void f(T&& param);               // “&&” might mean rvalue reference

1.	f(10);                           // 10 is an rvalue

   OR

   1.	int x = 10;

   2.	f(x);                            // x is an lvalue

   OR

   1.	template<typename T2>

   2.	    Gadget(T2&& rhs);            // deduced parameter type ⇒ type deduction;

   3.	    ...                          // && ≡ universal reference

   4.	};

   5.	 

   6.	void f(Widget&& param);          // fully specified parameter type ⇒ no type deduction;

   7.	                                 // && ≡ rvalue reference


### 2.4.Function Call by reference

   **void swap(int &x, int &y) {**
   
   **int temp;**
   
   **temp = x;**  /* save the value at address x */
   
   **x = y;**    /* put y into x */
   
   **y = temp;** /* put x into y */
  
   **return;  }**



### 2.5.Address Of operator

   C++ provides two-pointer operators, which are Address of Operator (&) and Indirection Operator (*).

**int main () {**
  
   **int  var , *ptr , val;**

   **var = 3000;**
   
   **ptr = &var;**  // take the address of var 

   **val = *ptr;**   // take the value available at ptr
   
   **cout << "Value of var :" << var << endl;**
   
   **cout << "Value of ptr :" << ptr << endl;**
   
   **cout << "Value of val :" << val << endl;**
 
   **return 0;   }**



 



