Describe the steps of using the `clone()` method in a class.

<details><summary>Solution</summary>
1. Make the class implement Cloneable. <br>
2. Use super.clone(). <br>
3. Cast super.clone() to your class. <br>
4. In the cloned instance "Deep copy" and handle any inner field that is not a primitive.<br>
5. Return the cloned instance.
</details>