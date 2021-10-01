# Activity-II-Closures
/* Q:what´s closure?
A: A closure is a feature in JavaScript that gives you access to an outer function’s scope (lexical environment) from an inner function.
Give me an example of closure:
*/
function outeerFunction(){
    var outerVariable = "Outer varible"
    function innerFunction(){
        console.log(outerVariable);
    }
    return innerFunction();
}
outeerFunction();

/* What is ()() in code? 
 In JS ther are use to call a function inside another which returns this first function */
function add(x){
    return function(y){
        return x+y;
    }
}
console.log(add(3)(5));

/* Move the variable after the closure (the function inside the function) and explain what happens. 
In this case the code still works because the second function is call after the compiler reads the variable count */
function counter(){
    function incrementCounterBy1(){
        console.log(count)
    }
    var count = 5;
    return incrementCounterBy1
}
counter()();

/* Change var for let and explain why the logic is not affected 
This still works as a result of the clouse which allows the use of any variable inside the parent function */
function counter(){
    function incrementCounterBy1(){
        console.log(count)
    }
    let count = 5;
    return incrementCounterBy1
}
counter()();

/* Scope chain, an example of it, how many closures can we nest 
You could increase tha chain as you would like and the code will work as long as either all the variables are kept inside the parent fuction or you use global scope */
function grandParent(){
    let grandVariable = 'grandVariable';
    function parent(){
        const parentVariable = 'parentVariable';
        const child = () =>{
            console.log(`${grandVariable} & ${parentVariable} inside children function` );
        }
        return child();
    }
    return parent();
}
grandParent();

/* They are conflicts between the closure and the global scope? 
Thanks to the closure, we are let to name to varibles equal, avoiding conflict */
let sameNameVar = 1;
(function(){
    let sameNameVar = 2;
    console.log(sameNameVar);
})();

/* Advantages of closures.
You dont have to worry for conflicts caused by repeated varible names 
You can make either public or private a variable
function fabric */
function counterBuilder(n){
    let counter = 0;
    function incrementCounter(){
        counter = counter + n
        console.log(counter)
    }
    return incrementCounter
}

/* ¿What is data hiding and encapsulation? 
Data hiding is the ability of objects to shield variables from external access. It is a useful consequence of the encapsulation principle which is the ability of an object to be a container (or capsule) for its member properties, including variables and methods. 
Give me an example of privacy with closures */
let myBankBalance = (function(){
    let myTrueMoney = 1000;
    return {
        get accessToMyMoney(){
            return myTrueMoney;
        }
    }
})();
console.log(myBankBalance.accessToMyMoney);// 1000 
console.log(myBankBalance.myTrueMoney);//undefiend
// myTrueMoney is closed off from outside of the function myBankBalance but accible to  accessToMyMoney

/* What happens if you create two counters with the same closure?
The function is run again and each of the counters will always throw a 1 since the counter variable is reset each call */
function incremental(){
    let counter = 0;
    function incrementCounter(){
        counter++;
        console.log(counter)
    }
    return incrementCounter()
}
const counter1 = incremental();
const counter2 = incremental();

/* How can we add more functions as a decrement counter? Give an example of it. 
With a function constructor, turning this into an object and ading internal functions (closures) */
function Counter(){
    let counter = 0;
    this.incrementCounter = () => {
        counter++
        console.log(counter)
    }
    this.decrementCounter = () => {
        counter--
        console.log(counter)
    }
}
const incrementCounter = new Counter;
incrementCounter.incrementCounter();

/* What are the disadvantages of closures?  
Variables used by closure will not be garbage collected. =>(monitor memory allocation and determine when a block of allocated memory is no longer needed and reclaim it) which leads to an increase of memory. */

