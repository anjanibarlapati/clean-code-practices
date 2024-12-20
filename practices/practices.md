# Clean Code - Building a MindSet

- "Clean Code is not a checklist, it's a mindset." – **Naveen Gaddi**
- Clean code isn't just about following principles; it's about building a mindset that naturally leads us to write cleaner, more maintainable code.

- We should always wrirt the code in the clients perspective and that should convey its intention to others.
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

    **Bad example**

    ```TypeScript
    function cost(x: number): number {
        return x * 3 + 2;
    }
    ```

    **Good example**

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

    **Bad example**

    ```TypeScript
    function calculateArea(radius: number): number {
        return 3.14159 * radius * radius;
    }
    ```

    **Good example**

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
  - Break the complex line into smaller, meaningful steps. Assign intermediate results to proper named variables. This improves readability and makes debugging easier since each step to its job independently.

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