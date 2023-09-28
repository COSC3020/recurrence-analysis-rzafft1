[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-718a45dd9cf7e7f842a935f5ebbe5719a5e09af4491e668f4dbf3b35d5cca122.svg)](https://classroom.github.com/online_ide?assignment_repo_id=12041729&assignment_repo_type=AssignmentRepo)
# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```
Analysis ...

- Each recursive call returns a third of the input size => $T(\frac{n}{3})$
- I have three recursie calls => $3 * T(\frac{n}{3})$
- We return $n^5$ from each recursive call because we have three nested for loops, who of which that iterate n^2 instead of n. So we ahave => $3 * T(\frac{n}{3}) + n^5$ 

Recurrence Relation : 

$
T(n) =
\begin{cases} 
1 & \text{if } n \leq 1 \\
3 * T(\frac{n}{3}) + n^5 & \text{else} 
\end{cases}
$

Solve Recurrence Relation : 

- $T(n) = 3 * T(\frac{n}{3}) + n^5$
- $T(n) = 3 * (3 * T(\frac{(\frac{n}{3})}{3}) + (\frac{n}{3})^5) + n^5$
- $T(n) = 9 * T(\frac{n}{9}) + \frac{n^5}{81} + n^5$
- ...
- $T(n) = 3^i * T(\frac{n}{3^i}) + in^5$
- ...
- since we are using a divide and conquer by three approach, we can let $i = log_{3}n$
- ... 
- $T(n) = 3^{log_{3}n} * T(\frac{n}{3^{log_{3}n}}) + (log_{3}n)n^5$
- $T(n) = n * 1 + n^5log_{3}n$
- $T(n) = n + n^5log_{3}n$
- **NOTE** : $n^5log_{3}n$ grows faster than $n$, so we dont need to include $+n$
- $T(n) \in \Theta(n^5log_{3}n)$


Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.
