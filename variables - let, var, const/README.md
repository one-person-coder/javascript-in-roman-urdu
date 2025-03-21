# JavaScript mein var, let, aur const

Agar tum JavaScript seekh rahe ho ya advance level pe ho, toh `var`, `let`, aur `const` ka sahi tareeke se istemal bohot zaroori hai. Yeh teenon keywords variables declare karne ke liye use hote hain, magar har ek ka apna scope, behavior, aur use case hai. Chalain, inko deeply samajhne ki koshish karte hain.

## 🔹 var – Purana tareeqa, global aur function scope

### 🟢 Kaam kaise karta hai?

1. **Function Scope hota hai**: var sirf function ke andar hi apni limit rakhta hai. Agar function ke andar declare kiya hai, toh sirf ussi function ke andar access ho sakta hai. Lekin agar kisi block `{}` ke andar declare karein, toh woh us block tak limited nahi hota.

2. **Re-declaration allowed hai**: Aik hi variable ko dubara declare kar sakte ho bina kisi error ke.

3. **Hoisting hoti hai**: JavaScript isko upar le jati hai execution se pehle, magar agar use karne se pehle initialize na ho toh undefined milega.

4. **Global object ka hissa banta hai**: Agar kisi function ke bahar declare karo, toh yeh window object ka part ban jata hai.

#### 📌 Example:

```javascript
function testVar() {
    if (true) {
        var x = 10; // Yeh block scope ka hissa nahi hai
    }
    console.log(x); // ✅ Output: 10
}
testVar();
```


```javascript
var name = "Ali";
var name = "Ahmed"; // ✅ Koi error nahi, overwrite ho gaya
console.log(name); // Output: Ahmed
```


```javascript
console.log(a); // Output: undefined (kyunki hoisting ho chuki)
var a = 5;
```

#### ✅ Kab istemal karein?

* Agar tum function-scoped variables declare karna chahte ho.
* Agar purani JavaScript ya ES5 compatible code likhna ho.
* Magar general practice mein `var` avoid karna chahiye.


## 🔹 let – Modern tareeqa, block scope

### 🟢 Kaam kaise karta hai?

1. **Block Scope hota hai**: `{}` ke andar declare kiya gaya variable sirf ussi block ke andar available hota hai.

2. **Re-declaration allowed nahi hai**: Aik hi variable ko ek hi scope mein dobara declare nahi kar sakte.

3. **Hoisting hoti hai magar Temporal Dead Zone (TDZ) ke wajah se initialize nahi hota**: Agar `let` ko declare karne se pehle use karne ki koshish karo toh error milega.

4. **Not attached to the window object**: Global scope pe declare karne ke bawajood `window` object ka hissa nahi banta.


#### 📌 Example:

```javascript
function testLet() {
    if (true) {
        let y = 20; // Yeh sirf is block tak limited hai
        console.log(y); // ✅ Output: 20
    }
    console.log(y); // ❌ ReferenceError: y is not defined
}
testLet();
```

```javascript
let name = "Ali";
let name = "Ahmed"; // ❌ Error: Identifier 'name' has already been declared
```

```javascript
console.log(b); // ❌ ReferenceError: Cannot access 'b' before initialization
let b = 10;
```

#### ✅ Kab istemal karein?

* Jab tum block-scope wali values store karna chaho.
* Agar tum mutable (change hone wale) values store kar rahe ho.
* Jab tum chaho ke accidental re-declaration na ho.


## 🔹 const – Immutable, block scope

### 🟢 Kaam kaise karta hai?

1. **Block Scope hota hai**: `{}` ke andar declare kiya gaya variable sirf ussi block ke andar available hota hai.

2. **Re-declaration aur re-assignment dono allowed nahi hai**: Aik baar value assign kar di, toh dobara change nahi kar sakte.

3. Hoisting hoti hai magar Temporal Dead Zone (TDZ) apply hoti hai: Declaration se pehle access nahi kar sakte.


4. **Not attached to the window object**: `const` ka koi link global window object se nahi hota.

5. **Reference types ke liye mutable hai**: Agar array ya object `const` se declare kiya, toh uske andar values change kar sakte ho, magar naya object ya array assign nahi kar sakte.

#### 📌 Example:

```javascript
const pi = 3.1416;
pi = 3.14; // ❌ TypeError: Assignment to constant variable.
```

```javascript
const obj = { name: "Ali" };
obj.name = "Ahmed"; // ✅ Allowed
console.log(obj.name); // Output: Ahmed

obj = { age: 25 }; // ❌ Error: Assignment to constant variable.
```

#### ✅ Kab istemal karein?

* Jab tumhe sure ho ke variable ki value change nahi hogi.
* Jab tum objects ya arrays ko mutate (modify) karna chahte ho magar naya reference assign nahi karna chahte.
* Jab tum read-only values store kar rahe ho.

## 🎯 Summary Table:

| Feature | var | let | const|
|---------|-----|-----|------|
|**Scope**|Function-scoped|Block-scoped|Block-scoped|
|**Re-declaration allowed?**|✅ Yes|❌ No|❌ No|
|**Re-assignment allowed?**|✅ Yes|✅ Yes|❌ No|
|**Hoisting?**|✅ Yes (`undefined`)|✅ Yes (TDZ error)|✅ Yes (TDZ error)|
|**Attached to window?**|✅ Yes|❌ No|❌ No|

### 🎯 Kis ko kahan use karna chahiye?
1. **Agar tum function-scope wali variable chahte ho**: `var` (magar avoid karna chahiye).
2. **Agar tum block-scope chahte ho aur mutable value ho**: `let`.
3. **Agar tum immutable (constant) value store karna chahte ho**: `const`.

#### 🛑 Best Practice:
* 80% time `const` use karo (taake accidental re-assignment na ho).
* Jab zaroorat ho tabhi `let` use karo (agar mutable variable chahiye).
* `var` ko avoid karo kyunki unpredictable behavior de sakta hai.
