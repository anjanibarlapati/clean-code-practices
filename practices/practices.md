# Clean Code - Building a MindSet

- **"Clean Code is not a checklist, it's a mindset." – Naveen Gaddi**
- Clean code isn't just about following principles; it's about building a mindset that naturally leads us to write cleaner, more maintainable code.

- We should always write the code in the clients perspective and that should convey its intention to others.
- "Any fool can write code that a computer can understand. Good programmers write code that humans can understand." – *Martin Fowler*
- Always make code human readability. Machines execute code, but humans maintain it.

# Clean Code Practices:

Writing clean code is crucial because it makes our codebase easier to understand, maintain, and debug. If our code is unclear, it can lead to confusion and more bugs down the road. One way to identify problems in our code is through code smells—these are signs that something might be wrong, even if the code runs correctly.

In this post, we'll explore common code smells and how to clean them up.

## Avoiding Common Code Smells in TypeScript

We’ll cover naming functions and variables, magic numbers and strings, excessive comments, and letter case inconsistencies—all using TypeScript examples.

1.  ### Naming Functions and Variables Clearly

    Choosing good names for the functions and variables is one of the most important aspects of writing clean code. If the names are unclear or confusing, our code will be hard to understand.

    **The Problem:**

    Using unclear or generic names like temp, foo, bar, or data.
    Using function names that don’t clearly explain what the function does.

    **The Solution:**

    Use descriptive, meaningful names that convey the purpose of the function or variable.

    **Bad example:**

    ```TypeScript
    function cost(x: number): number {
        return x * 3 + 2;
    }
    ```

    **Good example:**

    ```TypeScript
    function calculateTotalPrice(price: number): number {
        return price * 3 + 2;
    }
    ```

    In the first example, cost doesn’t convey us what the function is doing. In the second example, calculateTotalPrice makes it clear that the function is calculating the total price.

2.  ### Avoid Magic Numbers

    Magic numbers are numbers hard-coded directly in the code, with no explanation of what they mean. These can confuse anyone reading the code, as the number's meaning is not clear.

    **The Problem:**

    Using raw numbers in the code, like 42, 100, or 3.14159, without explaining their purpose.

    **The Solution:**

    Replace magic numbers with named constants that explain what the number represents.

    **Bad example:**

    ```TypeScript
    function calculateArea(radius: number): number {
        return 3.14159 * radius * radius;
    }
    ```

    **Good example:**

    ```TypeScript
    const PI = 3.14159;

    function calculateArea(radius: number): number {
        return PI * radius * radius;
    }
    ```

    In the first example, 3.14159 is unclear unless if we are familiar with the value of Pi. In the second example, using the constant PI makes the meaning clear and makes the code easier to maintain.

3.  ### Avoid Magic Strings

    Similar to magic numbers, magic strings are hard-coded string values used throughout the code, which can make it harder to understand and maintain.

    **The Problem:**

    Using strings like "ERROR" or "SUCCESS" without explaining their usgae and importance.

    **The Solution:**

    Replace magic strings with named constants or enums to give them meaning.

    **Bad example**

    ```TypeScript
    function logStatus(status: string): void {
        if (status === "ERROR") {
            console.log("Something went wrong!");
        } else if (status === "SUCCESS") {
            console.log("Operation successful.");
        } else {
            console.log("Unknown status");
        }
    }
    ```

    **Good example**

    ```TypeScript
    const STATUS_ERROR = "ERROR";
    const STATUS_SUCCESS = "SUCCESS";

    function logStatus(status: string): void {
        if (status === STATUS_ERROR) {
            console.log("Something went wrong!");
        } else if (status === STATUS_SUCCESS) {
            console.log("Operation successful.");
        } else {
            console.log("Unknown status");
        }
    }
    ```

    In the first example, the magic strings "ERROR" and "SUCCESS" don’t have any context. By using constants like STATUS_ERROR and STATUS_SUCCESS, the code becomes clearer and easier to maintain.

4.  ### Too Many Comments? Refactor Instead!

    Comments are useful, but if we need to add a lot of comments to explain what our code is doing, it might mean that the code itself isn’t clear enough. Instead of relying on comments, focus on making the code more readable.

    **The Problem:**

    Overusing comments to explain what the code does instead of making the code self-explanatory.

    **The Solution:**

    Refactor your code to make it clear, and only add comments when absolutely necessary (e.g., to explain why something is done, not how).

    **Bad example**

    ```TypeScript
    // apply 2% discount for total cost cost is more than 1000
    if(totalCoast > 1000){
        totalCost = totalCost - totalCost * 0.02;
    }
    ```

    **Good example**
    ```TypeScript
    const TOTAL_DISCOUNT_PERCENTAGE: number = 0.02;
    const TOTAL_DISCOUNT_THRESHOLD: number = 1000;

    if (totalCost > TOTAL_DISCOUNT_THRESHOLD) {
       totalCost -= totalCost * TOTAL_DISCOUNT_PERCENTAGE;
    }
    ```

5.  ### Inconsistent Letter Case

    Inconsistent letter casing in the code can lead to confusion, especially when it comes to variable and function names. Different coding styles can make the code harder to read and cause bugs.

    **The Problem:**

    Mixing different letter case styles in the same codebase (e.g., camelCase for variables and snake_case for others).

    **The Solution:**
    Stick to a consistent letter case convention throughout the code.

    In TypeScript, we typically use:

    camelCase for variables and functions.

    PascalCase for class names.

    UPPER_SNAKE_CASE for constants.

    **Bad example**

    ```TypeScript
    let TotalAmount = 100;
    const MAX_LIMIT = 500;
    let final_amount = TotalAmount + MAX_LIMIT;
    ```

    **Good example**
    ```TypeScript
    let totalAmount = 100;
    const MAX_LIMIT = 500;
    let finalAmount = totalAmount + MAX_LIMIT;
    ```

## GOD Line

- **God Line** refers to a single, very long and complex line of code that tries to do too much at once. These lines are difficult to read, understand, and debug because they combine multiple operations, making the logic unclear.
- **Refactoring Technique: Split into Smaller Steps**
  - Break the complex line into smaller and meaningful steps. Assign intermediate results to proper named variables. This improves readability and makes debugging easier since each step do its job independently.

- **Example**
    - Code with GOD line
        ```TypeScript
        let amount = quantity * price - Math.max(0, quantity - 10) * price * 0.2 + Math.min(40, quantity * price * 0.1);
        ```
    - Refactored code
        ```TypeScript
        function discountFor(quantity:number, price: number):number {
            const MAX_QUANTITY_FOR_DISCOUNT = 10;
            const DISCOUNT_RATE = 0.1;
            if(quantity < MAX_QUANTITY_FOR_DISCOUNT) {
                return 0;
            }

            return (quantity - MAX_QUANTITY_FOR_DISCOUNT) * price * DISCOUNT_RATE ;
        }

        function shippingAmountFor(quantity:number, price: number):number {
            const SHIPPING_RATE = 0.1;
            return Math.min(40, quantity * price * SHIPPING_RATE);
        }

        const discount: number = discountFor(quantity, price);
        const basePrice: number = quantity * price;
        const shippingAmount: number = shippingAmountFor(quantity, price);
        let amount = basePrice - discount + shippingAmount;
        ```
        
## Code Formatting

- If we use inconsistent formatting throughout a codebase, then the code is not readable and easier to understand.
- Formatting the code is an important aspect of writing clean code. It make the code more readable and easier to understand.

- When code is formatted properly, then developers can easily identify patterns and understand how the code works, which makes it easier to debug, maintain, and update the codebase over time. 

- **Example**
  - Code without formatting
    ```TypeScript
    const add=(number1,number2)=>{
    const result=number1+number2;
    return result;
    }
    ```
  - Code after formatting
    ```TypeScript
    const add = (number1, number2) => {
        const result = number1 + number2
        return result
    }
    ```
    
# Code smell in functions

  1. ### Incorrect function name:

     - **The code smell:**

       - Wrong function name does not conveys the original action of the function. It will create misconception to the one who is looking at it.

     - **Refactoring Techniques:**

       - Initially check the function name, the name of the function is conveying what job or action it is doing. The name of the function should related to the action the function is doing.
       - The function should be in the present tense not in the past tense.
  [For more information refer this ](#1-incorrect-function-name)

 2. ### Long function signature ( More than 2 parameters in the function signature)

    **The code smell:**

       - If function signature is too long it looks messy and every time we need to check the parameters. The function signature is too long i.e is it taking more than 2 parameters, then it is in the code smell.

    **Refactoring Techniques:**

      - If you want to give more than two parameters to a function then use a class and create instance for that class and give that instance to the function. This makes more sense, because the function taking properties and acting upon the properties, so they may belong to the one class.

    **Code smell**

    ```Typescript
    function costFor(productName:string,productQuantity:number,productPrice:number){
        return productQuantity*productPrice;
    }
    ```

    **Refactored code**

    ```Typescript
    function costFor(product:Product){
        return product.quantity*product*price;
    }
    ```

 3. ### Lengthy function.

    **The code smell:**    

     - A function should do only one task. And lengthy function is a code smell. We need to go through the whole function to understand what the function is doing. It effects the readability too. 

    **Refactoring Techniques:**

    - If your function doing more than one task then divide the function into multiple function. And make sure that the resultant function is doing only one task.
    - After diving call those functions inside this function. That will solve this problem and your code also looks clean. This will increases the readability.
    - It also helps you to use the extracted logic to use anywhere it is required, because you moved that into another function.

    **Code smell**
    ```TypeScript
    function processData(data: number[]): void {
        if (data.length === 0) {
            console.log("No data provided");
            return;
        }

        let total = 0;
        for (let index = 0; index<data.length; index++) {
            if (typeof data[index] !== "number") {
                console.log(`Invalid number: ${data[index]}`);
                return;
            }
            total += data[index];
        }

        const average = total / data.length;
        console.log(`Total: ${total}`);
        console.log(`Average: ${average}`);
    }
    ```
    **Refactored code**
    ```Typescript
    function checkEmptyData(data: number[]): boolean {
        if (data.length === 0) {
            console.log("No data provided");
            return true;
        }
        return false;
    }

    function validateNumbers(data: number[]): boolean {
        for (let index = 0; index < data.length; index++) {
            if (typeof data[index] !== "number") {
                console.log(`Invalid number: ${data[index]}`);
                return false;
            }
        }
        return true;
    }

    function calculateTotal(data: number[]): number {
        let total = 0;
        for (let index = 0; index < data.length; index++) {
            total += data[i];
        }
        return total;
    }

    function calculateAverage(total: number, count: number): number {
        return total / count;
    }

    function processData(data: number[]): void {
        if (checkEmptyData(data)) {
            return;
        }

        if (!validateNumbers(data)) {
            return;
        }

        const total = calculateTotal(data);
        const average = calculateAverage(total, data.length);

        console.log(`Total: ${total}`);
        console.log(`Average: ${average}`);
    }

    ```
## Organizing the private and public methods in the class.

  -  **The code smell:**
     - If the private and public methods are mixed so we need to search for the method. And it looks messy.

  -  **Refactoring Techniques:**

      - Keep all the private methods at one place and all public methods at one place. So the class looks clean. And we can also easily find a method in the class. If the function we are searching is the private then we can directly search in the private methods. And if the method we are searching is the public then we can search directly in the public methods.

  - **code smell**

    ```Typescript
        class Product{
            name:string,
            price:number,
            private barcode:string;
            quantity:number,
            constructor(name:string,price:number,quantity:number,barcode:string){
                this.name=name;
                this.price=price;
                this.quantity=quantity;
                this.barcode=barcode;
            }
            public calculateCost(){
            // some logic
            }
            private displayBarcode(){
                console.log(this.barcode);
            }
            public DisplayBill(){
                //some logic
            }
        }
    ```

 - **Refactored code**
 

    ```TypeScript
    class Product{
        name:string,
        price:number,
        quantity:number,
        private barcode:string;
        constructor(name:string,price:number,quantity:number,barcode:string){
            this.name=name;
            this.price=price;
            this.quantity=quantity;
            this.barcode=barcode;
        }
        private displayBarcode(){
            console.log(this.barcode);
        }
        public calculateCost(){
        // some logic
        }
            public DisplayBill(){
            //some logic
        }
        }

    ```

## Feature - Envy
**Feature envy** is a code smell which occurs when a class or methods need to access and manipulate the data from another class to complete its own task.
This method accesses properties or behaviour of other class excessively which indicates that it might belongs to the class.

In simple way, feature envy code smell occurs when a funciton frequently interacts with data or functions in other modules.

- ## Issues :
    - It violates the principle of encapsulation.
    - It also increases **coupling** between the classes.
    - It doesn't follow **`tell-don't-ask`** principle.

- ## Ways to handle feature-envy :
    - **`Extract`** the method that uses the data or functionality from another class and move it to that class.
    - Introducing a new **`class`** tht encapsulates the data and functionality that are used by another class.

- ## `Tell don't ask` 
    - Tell don't ask is a principle which helps people to remember that Object-Orientation is about bundling data with the functions that operate on that data.
    - In simple words, it means we should tell an object what to do instead of asking for its data and acting on that data.
    - It focuses on making objects more resposible for their own data and behaviour.

    ### Let's understand more with an example :
    ---
    ```typescript
    class Orders {
        products: Product[]

        constructor(products: Product[]) {
            this.products = products
        }

        public totalCost() {
            return this.products.reduce((totalCost, product) => {
                totalCost + product.getPrice() * product.getQuantity() 
            }, 0);
        }
    }

    class Product {
        private _name: string,
        private _price: number,
        private _quantity: number

        constructor(product: ProductAttributes) {
            this._name = product.name
            this._price = product.price
            this._quantity = product.quantity
        }

        public getPrice() {
            return this._price;
        }

        public getQuantity() {
            return this._quantity;
        }
    }
    ```

    In the above **code snippet**, the `totalCost` method in Orders class is purely dependent on the `Product` class for its internal data (**price** and **quantity**) to calculate the total cost.

    - Here it creates a tight coupling (dependency) between **`Product`** and **`Orders`** class.
    
    - The behaviour of calculating the cost of product might logically belong to the Product class since it involves its own data.

    ### Now, Let's refactor this code snippet !
    
    - Move the logic for calculating the cost of a product to the Product class.

    #### Refactored code snippet :
    ---

    ```typescript
    class Product {
        private _name: string,
        private _price: number,
        private _quantity: number

        constructor(product: ProductAttributes) {
            this._name = product.name
            this._price = product.price
            this._quantity = product.quantity
        }

        public cost() {
            return this._price * this._quantity;
        }
    }

    class Orders {
        products: Product[]

        constructor(products: Product[]) {
            this.products = products
        }

        public totalCost() {
            return this.products.reduce((totalCost, product) => {
                totalCost + product.cost();
            }, 0);
        }
    }
    ```


# Boy Scout Rule:

- The "**Boy Scout Rule**" is a principle in software development that encourages us to leave the codebase in a cleaner state than we have found it. 
- The idea is inspired by the scouting motto: "**Leave the  campground cleaner than you found it.**" 

    - In the context of coding, this means that every time we touch or work on a piece of code, we should aim to improve it, even if it’s in small ways. 


- ## Code Smells Related to Boy Scout Rule :

    1. **Duplicated Code:** 
    - Repeating the same code in multiple places instead of abstracting it into a function or class can lead to redundancy and maintenance headaches. When we see code repetition, it’s a good sign we should refactor it.

    Example:
    -  Duplicated code for calculating the tax in multiple places:
    ```sh
    const TAX_RATE = 0.05;

    function calculateTotalPrice(price: number): number {
        const tax = price * TAX_RATE;
        return price + tax;
    }

    function calculateDiscountedPrice(price: number, discount: number): number {
        const tax = price * TAX_RATE;
        return price - discount + tax;
    }
    ```

    - Instead of duplicating the tax calculation logic, we can refactor it into a helper function.

    **Refactored code:**

    ```sh
    const TAX_RATE = 0.05;

    function calculateTax(price: number, taxRate: number = TAX_RATE): number {
        return price * taxRate;
    }

    function calculateTotalPrice(price: number): number {
        const tax = calculateTax(price);
        return price + tax;
    }

    function calculateDiscountedPrice(price: number, discount: number): number {
        const tax = calculateTax(price);
        return price - discount + tax;
    }
    ```
   2. **Lengthy Methods:** Large, complex methods can be hard to read, test, and maintain. 
        If a function or method does too many things, it might be time to break it down into smaller methods.

    Example:
    ```sh
    const ERROR_MESSAGES = {
        INVALID_ORDER: "The order is invalid.",
        INSUFFICIENT_STOCK: "Not enough stock to fulfill the order.",
    };

    function processOrder(order: Order): void {
        if (!order.isValid()) {
            throw new Error(ERROR_MESSAGES.INVALID_ORDER);
        }
        if (!checkInventory(order)) {
            throw new Error(ERROR_MESSAGES.INSUFFICIENT_STOCK);
        }
        chargeCustomer(order);
        shipOrder(order);
        sendConfirmation(order);
    }
    ```
  - **Problem (Code Smell):** The ```process_order()``` method is doing too many things — `validating`, `checking inventory`, `charging`, `shipping`, etc.

   - **Solution (Boy Scout Rule):** Breaking the responsibilities into smaller methods. This makes the code easier to test, understand, and modify.
   
   **Refactored code:**
   ```sh

    const ERROR_MESSAGES = {
        INVALID_ORDER: "The order is invalid.",
        INSUFFICIENT_STOCK: "Not enough stock to fulfill the order.",
    };

    function processOrder(order: Order): void {
        validateOrder(order);
        checkInventory(order);
        chargeCustomer(order);
        shipOrder(order);
        sendConfirmation(order);
    }

    function validateOrder(order: Order): void {
        if (!order.isValid()) {
            throw new Error(ERROR_MESSAGES.INVALID_ORDER);
        }
    }

    function checkInventory(order: Order): void {
        if (!checkInventory(order)) {
            throw new Error(ERROR_MESSAGES.INSUFFICIENT_STOCK);
        }
    }
    ```
    3. **Long Parameter Lists:**
    -  A function or method that takes too many parameters is usually a sign that something is wrong. It can indicate that the function is doing too much or that there’s a missing abstraction.

    Example: 

    ```sh
    function createUser(username: string, email: string, password: string, phone: string, address: string, city: string, country: string): void { ... }
    ```

    - **Problem (Code Smell):** The method ``createUser`` takes a long list of parameters, which can be error-prone and difficult to maintain.

    - **Solution (Boy Scout Rule):** Can be refactored by encapsulating the parameters in a User class, reducing the number of parameters and improving clarity.

    **Refactored code:**
    ```sh
    class User {
        constructor(
            public username: string,
            public email: string,
            public password: string,
            public phone: string,
            public address: string,
            public city: string,
            public country: string
        ) {}
    }

    function createUser(user: User): void {

    }
    ```

    4. **Hard-Coded Values:**
    
    -  Hard-coding values (such as strings, numbers, file paths, etc.) in our code is a bad practice because it makes the code harder to maintain and less flexible.

    Example:
    ```sh
    function connectToDatabase(): void {
        const connection = mysql.createConnection({
            host: "localhost",
            user: "admin",
            password: "admin123",
            database: "app_db"
        });
        connection.connect();
    }
    ```

    - **Problem (Code Smell):** Hard-coded values like `localhost`, `admin123`, and `app_db` make the code less flexible and harder to maintain.

    - **Solution (Boy Scout Rule):** Using environment variables (via dotenv) to store sensitive or configurable data like database connection details, makes the code more flexible and environment-agnostic.

    **Refactored code:**

    ```sh
    import * as dotenv from 'dotenv';

    dotenv.config();

    function connectToDatabase(): void {
        const connection = mysql.createConnection({
            host: process.env.DB_HOST || 'localhost',
            user: process.env.DB_USER || 'admin',
            password: process.env.DB_PASSWORD || '',
            database: process.env.DB_DATABASE || 'app_db'
        });
        connection.connect();
    }
    ```


    5. **Too Much Commenting:** 
    
    - If code is heavily commented, it might be a sign that the code is unclear or difficult to understand. Instead of writing extensive comments, it’s often better to improve the code itself, making it more self-explanatory.

    Example:
    ```sh
    const TAX_RATE = 0.05;
    // This function calculates the total price with tax added
    function calculateTotal(price: number): number {

    // First, calculate the tax

        const tax = price * TAX_RATE;

    // Now, add tax to the original price

        const total = price + tax;

    // Return the final total price

        return total;
    }
    ```

    - **Problem (Code Smell):** Excessive comments clutter the code, and the code itself isn't clear.
    - **Solution (Boy Scout Rule):** Simplify the code and remove unnecessary comments. Using clear variable and function names so the code is self-explanatory.


    **Refactored code:**

    ```sh
    const TAX_RATE = 0.05;

    function calculateTotal(price: number): number {
        const tax = price * TAX_RATE;
        return price + tax;
    }

    ```

## Compile Time Safety.

- Compile-time safety means that the compiler can analyze our code and guarantee that certain kinds of errors are not present in our code.
  - For example, consider the below function:
    ```
    const max = (numberOne:number,numberTwo:number) : number => {
        if(numberOne>=numberTwo){
            return numberOne;
        }
        return numberTwo;
    }
    ```
  - Now the above function takes two numbers as parameters and gives a number as output.
  - But, while calling the function i.e., while using the above function, if we pass other than numbers to the function, an error pops up in the below manner:
    ```
    max(2,"u");
    ```
     Error: `Argument of type 'string' is not assignable to parameter of type 'number'`.

- But Sometimes, a logic which may validate few aspects in run time may be converted to get checked in compile time. This can be done using `generics` in Type Script.
- Consider the below class example:

    ```
    class Container<T>{
        value:T;
        constructor(value:T){
            this.value = value;
        }
        set(value:T){
            this.value=value
        }
    }
    ```

- If we look into the usage:
    ```
    const stringContainer = new Container<string>("Good");
    stringContainer.set("Good Morning") //No compile time error as string is passed.
    stringContainer.set(1) 
    ```
    Error: `Argument of type 'number' is not assignable to parameter of type 'string' `.
    
- This is how compile time safety works in TypeScript. 
- It checked whether the string type is being passed or not. 
- If not passed properly, throwing a compile time error makes us check for the mistake.

## Internal duplication:

- Internal duplication refers to the repetition of logic, code, or data with in single code base. 
- This type of duplication can make your codebase harder to maintain, increase the likelihood of introducing bugs, and reduce overall readability. 
- Addressing internal duplication is a crucial step toward writing clean and maintainable code.


1. Logic Duplication

When the same logic is duplicating multiple time which is not visible to us. Where duplication occurs internally
```Typescript
Example:
for(let index = 0 ; index < 5; index++){
    console.log("Hello all!")
}
```
In the above example, we have created the loop which console a string, but internally same logics duplicating. In above logics is same as like this.
```Typescript
console.log("Hello all!")
console.log("Hello all!")
console.log("Hello all!")
console.log("Hello all!")
console.log("Hello all!")

```
So, to avoid such duplication we need to wrap that logic in some function and then we need to call that function.

```Typescript
const printHello(){
    console.log("Hello all!")
}

for(let index = 0 ; index < 5 ;index++){
    printingHello()
}
```

### Why Avoid Internal Duplication?

1. Improves Maintainability
Fixing a bug or updating logic in one place automatically reflects across the entire codebase.


2. Enhances Readability
Centralized logic or data is easier to understand than scattered, repetitive pieces.


3. Prevents Bugs
Reducing duplication ensures consistency and avoids errors caused by outdated or mismatched changes.


4. Promotes DRY Principle
Following the "Don't Repeat Yourself" principle leads to cleaner, modular, and reusable code.



### Strategies to Eliminate Internal Duplication

1. Refactor Repeated Logic
Identify repeated patterns and extract them into helper functions, methods, or utilities.


2. Use Constants and Configuration Files
Centralize hardcoded values and repeated data into a dedicated file or module.


3. Leverage Design Patterns
Apply patterns like Singleton, Factory, or Strategy to handle repetitive instantiations or logic.


4. Adopt Modular Programming
Break down your codebase into small, reusable components or modules.


5. Write Tests to Detect Duplication
Automated tests can help highlight repeated patterns and ensure changes in one place do not break functionality elsewhere.

## Nested conditional statements in the code.

- The code with more nested conditional statements like multiple if statements inside each other is a code smell. It becomes hard to read, understand, and maintain. This makes the logic look messy, like an arrow pointing to the right, and hides the main purpose of the code.
- **Refactoring Technique: Early Returns**
   - Instead of nesting conditions, handle failure conditions at the start of the function and return immediately. Then, write the main logic without unnecessary nesting. This makes the code is easier to read and understand.

- **Example**
 
    - Code with nested conditions 
        ```TypeScript
        function handleLogin(username: string | null, password: string | null, user: User | null): string {
            if (username !== null && password !== null) {
                if (user !== null) {
                    if (user.isActive) {
                        if (user.password === password) {
                            return `Welcome back, ${user.name}!`;
                        } else {
                            return "Invalid password.";
                        }
                    } else {
                        return "Account is inactive.";
                    }
                } else {
                    return "User not found.";
                }
            } else {
                return "Username or password cannot be null.";
            }
        }
        ```
    - Refactored code using early returns
        ```TypeScript
        function handleLogin(username: string | null, password: string | null, user: User | null): string {
            if (!username || !password) {
                return "Username or password cannot be null.";
            }

            if (!user) {
                return "User not found.";
            }

            if (!user.isActive) {
                return "Account is inactive.";
            }

            if (user.password !== password) {
                return "Invalid password.";
            }

            return `Welcome back, ${user.name}!`;
        }
        ```
### Writing Extensible Code is a good practice

 1.   ### What is extensible code?

      The code is extensible when someone can easily add a new feature without editing any existing code other than configuration.

      It simply means writing a code that is easy to extend with new features, without making the system complex, hard to maintain, or prone to errors. The goal is to create a codebase that is not only adaptable to new requirements but also simple, readable, and testable.

    
  2. ### Example

     In this example, we have a Product class, and we want to calculate the discount for different types of products (e.g., Electronics, Clothing).
    
  ``` Typescript
  enum ProductType {
    ELECTRONICS,
    CLOTHING,
    FOOD,
  }

  class Product {
      constructor(
        public name: string,
        public type: ProductType,
        public price: number
      ) {}
    }

  class ShoppingCart {
      private products: Product[] = [];

      addProduct(product: Product) {
        this.products.push(product);
      }

      calculateTotalCost(): number {
        let total = 0;

        for (const product of this.products) {
          let discount = 0;
          if (product.type === ProductType.ELECTRONICS) {
            discount = 0.1;
          } else if (product.type === ProductType.CLOTHING) {
            discount = 0.2;
          }
          total += product.price * (1 - discount);
        }

        return total;
      }
    }

```

  3. ### Problems with this code

   - The logic for calculating the discount is hardcoded in the ShoppingCart class based on the product type. If we need to add new product types, we must modify the ShoppingCart class.
   - Adding a new product type (like FOOD) requires modifying the ShoppingCart class.
   - If the discount calculation rules change (e.g., changing the discount for ELECTRONICS), we must modify the ShoppingCart class.
   - If a new feature add, the code base increases which automatically increase the complexity of our code.
   - It Reduces the readability.
   - Increases the code duplication.

  4. ### Extensible code for this Example

  ``` Typescript
  enum ProductType {
    ELECTRONICS,
    CLOTHING,
    FOOD,
  }

  class Product {
    constructor(
      public name: string,
      public type: ProductType,
      public price: number
    ) {}
  }

  interface DiscountStrategy {
    calculateDiscount(price: number): number;
  }

  class ElectronicsDiscountStrategy implements DiscountStrategy {
    const tenPercentDiscount:number=0.1;
    calculateDiscount(price: number): number {
      return price * tenPercentDiscount;
    }
  }

  class ClothingDiscountStrategy implements DiscountStrategy {
    const twentyPercentDiscount:number=0.2;
    calculateDiscount(price: number): number {
      return price * twentyPercentDiscount;
    }
  }

  class FoodDiscountStrategy implements DiscountStrategy {
    const fivePercentDiscount:number=0.1;
    calculateDiscount(price: number): number {
      return price * fivePercentDiscount;
    }
  }

  class DiscountStrategyFactory {
    static getStrategy(productType: ProductType): DiscountStrategy {
      switch (productType) {
        case ProductType.ELECTRONICS:
          return new ElectronicsDiscountStrategy();
        case ProductType.CLOTHING:
          return new ClothingDiscountStrategy();
        case ProductType.FOOD:
          return new FoodDiscountStrategy();
        default:
          throw new Error('Unknown product type');
      }
    }
  }

  class ShoppingCart {
    private products: Product[] = [];

    addProduct(product: Product) {
      this.products.push(product);
    }

    calculateTotalCost(): number {
      let total = 0;

      for (const product of this.products) {
        const discountStrategy = DiscountStrategyFactory.getStrategy(product.type);
        total += product.price - discountStrategy.calculateDiscount(product.price);
      }

      return total;
    }
  }

  ```

  5. ### Benefits of Extensible code

   - The discount calculation logic is moved to individual strategy classes (ElectronicsDiscountStrategy, ClothingDiscountStrategy, etc.). This makes the ShoppingCart class cleaner and more focused on the main logic (managing products).
   - We can add new product types and discount strategies without modifying the existing ShoppingCart class. We simply create a new discount strategy class and update the DiscountStrategyFactory.
   - If we need to add a new product type (like FOOD), we just create a new strategy and update the factory without touching the ShoppingCart class.
   - If the discount rules change for a particular product type, we only need to modify the respective strategy class, not the core logic of the shopping cart.


##  DRY principle(Don't repeat yourself)
- Dry principle is a concept in software development, which aims to reduce the repitition by introducing an abstraction. It avoids redundancy in our code.

- #### Why repetition is a code smell ?
    - When you repeat code, any changes to that logic or functionality need to be made in multiple places.
    - It becomes harder to ensure consistency.
    - Repetition increases the size of the codebase without adding new functionality.
    - Repeated code makes the program harder to read.
    - There is a more difficulty in finding errors.
    - There's always a risk that changes or fixes made in one instance of the code may not be propagated to all others, leading to inconsistencies and bugs. 

- #### What is the value of refactoring it?
    - Main aim is to avoid the **duplication** of code(re-implementing the same logic in multiple places), by providing reusability.
    - We can implement the changes in all the related places/logics at once.
    - We can centralize the logic by making it into reusable functions, methods, or components, centralized logic makes **maintenance** easier. When you need to change a piece of functionality, you only need to update it in one place instead of multiple locations.
    - It helps in **isolating logic** into functions or methods, making the code easier to test.
    - Debugging is more **efficient** because any error that arises due to the repeated code will only need to be fixed in one place.
    - By abstracting logic, we ensure that the same **logic is applied uniformly** across the entire codebase.

    **Example**
  
    Here we are repeating the code which calculates discount price. There is duplication.
    ``` TypeScript
    export function calculateTotal(cart: { price: number; discount: number }[]) {
        let total = 0;

        const discountedPrice1 = cart[0].price - cart[0].price * cart[0].discount;
        const tax1 = discountedPrice1 * 0.08; 
        const shipping1 = 5.0; 
        total += discountedPrice1 + tax1 + shipping1;

        const discountedPrice2 = cart[1].price - cart[1].price * cart[1].discount;
        const tax2 = discountedPrice2 * 0.08; 
        const shipping2 = 5.0; 
        total += discountedPrice2 + tax2 + shipping2;

        const discountedPrice3 = cart[2].price - cart[2].price * cart[2].discount;
        const tax3 = discountedPrice3 * 0.08; 
        const shipping3 = 5.0;
        total += discountedPrice3 + tax3 + shipping3;

        return total;
    }
    ```
   So we are introducing abstraction, which makes the logic centralized at one place.
    ```TypeScript
    import { Product } from "./types";

    function costOf(product: Product) {
        const SHIPPING_PRICE = 5.0;
        const TAX = 0.08;

        const discountedPrice = product.price - product.price * product.discount;
        const taxOnProduct = discountedPrice * TAX;
        return discountedPrice + taxOnProduct + SHIPPING_PRICE;
    }
    export function totalCost(cart: Product[]) {
        let total = 0;
        for (const product of cart) {
            total += costOf(product);
        }
        return total;
    }
    ```
  Now the duplication has been eliminated. This is how we refactored it.

## Impure and Pure functions.

1. ### Impure functions:

   An impure function can have side effects, such as modifying global variables or interacting with external systems.

   An impure may rely on external state, causing unpredictable behavior.

   - In the below example, function is changing the `oldValue` which is declared outside the function i.e., external aspect.

     ```JavaScript
     let oldValue = 7;
     function add(newValue) {
         oldValue += newValue;
         return oldValue;
     }
     console.log(add(5));
     ```

     **Bad Example (impure function with side effects):**

     ```JavaScript
     numbers:number[]=[1,2,3,4]
     function removeFirstItem() {
         numbers.shift();
     }
     ```

     **Disadvantages of Impure Function:**

     1. Harder to Test: Since impure functions depend on external state or produce side effects, it's more difficult to isolate and test them.

     2. Unpredictable Behavior: Impure functions may behave differently depending on the state of the program or external factors, making them harder to reason about.

     3. Hidden Dependencies: Impure functions may rely on external state, which can introduce bugs and make the code harder to maintain.

2. ### Pure functions:

   - A pure function is a function that Always returns the same output for the same input.

   - A pure function is a function that Does not modify any external state or rely on it.

   - A pure function is a function that Given the same inputs, a pure function will always return the same output.

   - A pure function is a function that Has no side effects, meaning it does not change anything outside of the function (like global variables or external systems).

     **Example of a pure Function:**

     ```JavaScript
     function add(a, b) {
         return a + b;
     }
     console.log(add(2, 3));
     ```

- ### Refactor Impure function to Pure:

  - In the above bad example od impure function, removed the global dependency, `arr` is declared out side the function and external change is being taken place.
  - So, in order to avoid it: A pure function is written which takes the input and returns the respective output for that input.

  ```JavaScript
   function removeFirstItem(numbers) {
       return numbers.slice(1);
   }
   let numbers = [1, 2, 3];
   console.log(removeFirstItem(numbers));
   console.log(numbers);
  ```

- ### Few examples of impure and their respective pure functions.

    **Impure Fucntion**
    
    ```
    let total = 0;
    function add(newValue) {
        total += newValue;
        return total;
    }
    console.log(add(5));
    ```

  **Refactored to a Pure Function:**

  ```JavaScript
  function add(newValue, total) {
     return total + newValue;
  }

  let currentTotal = 0;
  console.log(add(5, currentTotal));
  ```

  **Impure Fucntion**

  ```JavaScript
  let counter = 0;
  function increment() {
    counter += 1;
    return counter;
  }
  ```

  **Refactored to a Pure Function:**

  ```JavaScript
  function increment(counter) {
      return counter + 1;
  }
  let currentCounter = 0;
  console.log(increment(currentCounter));
  ```

  **Adavantages of Pure Functions:**

  1.  Easier to Test: Since the output is predictable and based only on inputs, pure functions are easier to test.

  2.  Predictability: The same input always produces the same output, so there are no surprises.

  3.  Composability: Pure functions can be composed together to build more complex behaviors without side effects.

## Shotgun surgery

The shotgun surgery code smell is one of the code smells that often overlaps with other code smells, particularly duplicate code. Shotgun Surgery resembles Divergent Change. Divergent Change is when many changes are made to a single class. Shotgun Surgery refers to when a single change is made to multiple classes simultaneously.

In fact, the shotgun surgery code smell is at the root of that issue of “you change something here and it breaks something over there”.

**Why it should be avoided?**

- Changes in logic require updates in multiple locations, increasing the time and effort needed for updates.
- The logic is duplicated instead of being encapsulated in one place.

  **Example**

```TypeScript
class Library {

    borrowBook(bookId) {
       if (this.balanceDue > MAX_BALANCE_ALLOWED) {
         this.notifyMember("MEMBERSHIP_INACTIVE_BORROW");
         return;
       }
   }

   reserveBook(bookId) {
      if (this.balanceDue > MAX_BALANCE_ALLOWED) {
         this.notifyMember("MEMBERSHIP_INACTIVE_RESERVE");
         return;
       }
   }

   LateFees(amount) {
      this.balanceDue -= amount;
      if (this.balanceDue > MAX_BALANCE_ALLOWED) {
        this.notifyMember("MEMBERSHIP_INACTIVE_PAYMENT");
      }
   }

   notifyMember(message) {
      console.log(`Notification: ${message}`);
   }
}

const MAX_BALANCE_ALLOWED = 50;
const library = new LibrarySystem();
library.balanceDue = 60;

library.borrowBook(123);
library.reserveBook(456);
library.payLateFees(20);
```

In the above example, everytime when we are borrowing a book , or returning a book we are having check to find whether the member is active or not. BalanceDue is checked in multiple places (within the methods borrowBook, reserveBook, and LateFees). Each time a member attempts to borrow or reserve a book, the system checks whether the balanceDue exceeds the MAX_BALANCE_ALLOWED limit. If so, it sends a notification to the member.

If you need to change the behavior related to the balance check (e.g., change the limit or modify the way the notification is sent), you would need to modify it in all these methods (borrowBook, reserveBook, and LateFees). Here balance checking is duplicated across several methods, making the system more resist.

**Solution**

```TypeScript
class Library {

  borrowBook(bookId) {
    if (this.isMembershipInactive()) {
      this.notifyMember("MEMBERSHIP_INACTIVE_BORROW");
      return;
    }
  }

  reserveBook(bookId) {
    if (this.isMembershipInactive()) {
       this.notifyMember("MEMBERSHIP_INACTIVE_RESERVE");
       return;
    }
  }

  payLateFees(amount) {
    this.balanceDue -= amount;
    if (this.isMembershipInactive()) {
     this.notifyMember("MEMBERSHIP_INACTIVE_PAYMENT");
    }
  }

  isMemberInactive() {
    return this.balanceDue > MAX_BALANCE_ALLOWED;
  }

  notifyMember(message) {
    console.log(`Notification: ${message}`);
  }
}

const MAX_BALANCE_ALLOWED = 50;
const library = new LibrarySystem();
library.balanceDue = 60;

library.borrowBook(123);
library.reserveBook(456);
library.payLateFees(20);
```
## Explaining Variables and Explaining Functions in Clean Code
   In clean code, explaining variable and function names mean choosing names that clearly tell you what the variable or function represents, without needing extra explanation or comments. The goal is to make our code so clear that someone reading it can understand what it's doing just by looking at the names.

This will provide the following:
- **Clarity**: Clear variable names help anyone reading your code (including you) understand what the variable is for.
- **Less Confusion**: You don’t have toconfusewhat a variable means.

- **Easier to Maintain**: Clear names make it easy to go back and modify the code later, because you already know what the variables do.

   Here’s an example where the variable names

   **Unclear function & variable names**

    ```TypeScript
   function sqr(x: number): number {
          return x * x;
   }      
    let n=5;
    console.log(sqr(n));
    ```
  From the above example, the problems are:
  - Non-descriptive function name:
The function name sqr is an abbreviation, and while it's short, it's not immediately clear to someone unfamiliar with the code what it does. square would be a better name.
  - Non-descriptive variable name:
The variable n could be more descriptive, such as number or inputNumber.

   **Clear function & variable names**

    ```TypeScript
    function calculateSquare(number: number): number {
          return number * number;
    }      
    let inputNumber=5;
    console.log(calculateSquare(inputNumber));
    ```
   From the above example, when we observe this and it makes us to understand the below points. 
   - Descriptive function name: The function name calculateSquare clearly describes what the function does, it calculates the square of a number.
   - Descriptive variable name: The variable inputNumber clearly indicates that it holds a number input to the function.
   - The function and variable names are longer but far more readable and self-explanatory, which improves maintainability.

  
 The good example follows clean code principles by favoring clarity and descriptiveness over shortness. Even for simple tasks, naming things well goes a long way in making code understandable to others (and to our future self).


## Chatracterization Testing
A Characterization Testing is a type of automated test that is written to document the behavior of existing code. The primary goal of a characterization test is not to change the behavior of the code.

1. ### Why Are Characterization Tests Important
    * Sometimes, code is hard to understand. Characterization tests help show how the code works, even if it’s not fully clear.

    * Characterization tests help capture what the code currently does. Before making changes, we write these tests. If the tests pass after code changes, it means we are doing it correctly. They basically ensure the code still works as expected.
    
    * When changes are made to the code, these tests help find any new errors.

 **Problem statement:**
 ```
  Simple example of a function that calculates the area of a rectangle.
```

**Initial Code**
 ```TypeScript
    export function rectangleArea(length: number, width: number): number {
        return length * width;
    }
```

* Write a Test Case for the Current Behavior
```TypeScript
import { rectangleArea } from "./rectangle";
   test("should calculate the area of a rectangle correctly", () => 
   {
      const area = rectangleArea(5, 10);
      expect(area).toBe(50);
   });

   test("should throw an error if length or width is non-positive", () =>
    {
       expect(() => rectangleArea(-5, 10)).toThrow("Length and width must be positive numbers.");
       expect(() => rectangleArea(5, 0)).toThrow("Length and width must be positive numbers.");
    });
```

* Refactor the Code

```TypeScript
    export function rectangleArea(length: number, width: number): number 
    {
        if (length <= 0 || width <= 0) 
        {
           throw new Error("Length and width must be positive numbers.");
        }
       return length * width;
    }
```
