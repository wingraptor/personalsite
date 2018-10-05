+++
date = "2018-04-09"
title = "Switching It Up With Switch Statements"

+++
## What are Switch Statements?

This is another form of 'conditional logic' that can be used in a javascript program (think If/else statements). Switch statements are useful when many conditions are being evaluated because they can be easier to type or read compared with using if/else statements.

### Syntax

```js
switch (expression) {
case value1:
//Statements executed when the
//result of expression matches value1
break;
case value2:
//Statements executed when the
//result of expression matches value2
break;
...
case valueN:
//Statements executed when the
//result of expression matches valueN
break;
default:
//Statements executed when none of
//the values match the value of the expression
break;
}
// break and default statements are optional.
```

### Description

Switch statements evaluate an expression (found in parenthesis after the keyword 'switch') then looks for the first case clause whose expression (found after the keyword 'case') evaluates to the same value as the original input expression. A match occurs when the values are equal in value and type (strict comparison '==='). When this occurs the statement(s) in the matching clause are then executed.

If a 'break;' is present in that clause's statement then the program ceases execution of the switch statement and proceeds to the next statement after the switch statement. If there is no break present then the program continues to execute the next statement in the switch statement.

Note that default is an optional clause whose statements are executed if no matching case clause expressions are found. It is most commonly the last clause in the switch statement but this is not a requirement.

### Example 1:

<iframe src="https://repl.it/@akonobrathwaite/Blog-Switch-Statements-Eg-1?lite=true" width="100%" height="400px" frameborder="no" scrolling="no" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals" allowfullscreen="allowfullscreen"></iframe>

In **Example** **1:** the variable fruit has been assigned the value 'Bananas'. This is then used in the expression to be evaluated in the switch statement. The program goes through each case clause one by one until it finds the clause with the expression that evaluates to 'Bananas'. It then executes the nested statement, which in this case logs 'Bananas are $0.48 a pound.' to the console. The program encounters then encounters '**break**' which ceases execution of the switch statement .

Go ahead and click the "Play" button to see what happens.

### Example 2:

<iframe src="https://repl.it/@akonobrathwaite/Blog-Switch-Statements-Eg-2?lite=true" width="100%" height="400px" frameborder="no" scrolling="no" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals" allowfullscreen="allowfullscreen"></iframe>

In **Example 2** the variable <a href="https://www.youtube.com/watch?v=sV2t3tW_JTQ">MsInBankAccount</a> has been assigned the value '7Ms'. This is then used as the expression to be evaluated by the switch statement. As you can see, the case clause with the matching expression logs "You have one more M to go" to the console. Note that there is no **break** in this case clause and because of this the statement in the next clause is executed. This then logs 'Welcome 21 Savage' to the console as well. This statement does contain a **break** which then ceases execution of the switch statement.

Note that MsInBankAccount could be 1M, 2Ms, 3Ms, 4Ms, 5Ms, 6Ms and the output would be the same as for 7Ms. 21 Savage would be proud.

![21Savage](https://media.giphy.com/media/3o8dFsv6Pw69TZzmLK/giphy.gif)