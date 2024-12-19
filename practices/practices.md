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

# DRY principle(Don't repeat yourself)
### Dry principle is a concept in software development, which aims to reduce the repitition by introducing an abstraction. It avoids redundancy in our code.
## Why repetetion is a code smell ?
1. When you repeat code, any changes to that logic or functionality need to be made in multiple places.
2. When the same logic or code appears in multiple places, it becomes harder to ensure consistency. When bug is one place, you need to modify in multiple places.
3. Repetition increases the size of the codebase without adding new functionality.
4. Having repeated code makes the program harder to read because developers are likely to see the same thing multiple times in different parts of the system.
5. It creates redundancy. There is a more difficulty in finding errors.
6. There's always a risk that changes or fixes made in one instance of the code may not be propagated to all others, leading to inconsistencies and bugs. 

#### What is the value of refactoring it?
1. Main aim is to avoid the **duplication** of code(re-implementing the same logic in multiple places), by providing reusability.
2. When the DRY principle is applied successfully, a modification of any single element of a system does not require a change multiple places, we can implement the changes in all the related places/logics at once.  Centralized logic makes **maintenance** easier. When you need to change a piece of functionality, you only need to update it in one place instead of multiple locations.
3. It helps in **isolating logic** into functions or methods, making the code easier to test.
4. Debugging is more efficient because any error that arises due to the repeated code will only need to be fixed in one place.
5. By abstracting logic, we ensure that the same logic is applied uniformly across the entire codebase.

#### How we can refactor code by applying DRY principle?
1. We will centralize the logic by making it into reusable functions, methods, or components.
2. We have to split functions, and reuse it whenever necessary.

**Example**

Here we are repeating the code which calculates discount price. There is duplication.
```bash
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
```bash
export function calculateTotal(cart: { price: number; discount: number }[]) {
  let total = 0;
  for (const cartItem of cart) {
    const shippingCost = 5.0;
    const taxPercentageOnProduct = 0.08;
    const discountedPrice = cartItem.price - cartItem.price * cartItem.discount;
    const tax = discountedPrice * taxPercentageOnProduct;
    total +=discountedPrice + tax + shippingCost;
  }
  return total;
}
```
- Now the duplication has been eliminated. This is how we refactored it.