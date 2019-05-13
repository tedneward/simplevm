# StackVM-based simplevm

## Build/run

This is a Gradle project. use `gradle run` to run the simple tests in the `App.main` method. The rest of the Gradle tasks are likely to be pretty easy to infer.

## Future directions

There's a number of ways this code could be extended:

* **TESTS!!** Just because I didn't put any in here for my talk doesn't mean they're not a good idea. Add them! Lots of them! Go wild! (In fact, I'll happily accept some PRs that add tests and don't change any of the other code--I want to keep the code here pretty simple in order to support the talk better, but tests don't need to be part of the talk and so are quite welcome additions.) If you do any of the enhancements below, think about how the tests would need to reflect those changes.

* **Add debugging.** If the svm is run with a command-line parameter ("--debug", perhaps), have it break before each instruction and await a command. Add support to single-step (execute one opcode), run (resume the loop), dump (stack, frame, memory, and so on), and anything else that you think might be helpful.

* **Add strings.** The fact that the svm doesn't support strings natively is pretty limiting; add string support by setting up strings in the consant pool, using LDC to push them on the stack, and so on. This will, however, begin the first steps towards having some kind of type system (or deliberately choosing not to), because now you will need to start thinking about what happens when somebody writes `LDC 0 LDC 0 ADD` with the constant pool index 0 being `"Hello!"`. If you support the mathematical operations on strings, you are headed towards dynamically-typed (ECMAScript, Ruby, Python) territory; if you disallow it, you are headed towards statically-typed (JVM, CLR) territory. Neither place is bad, just different, and you'll find the exercise intriguing.

* **Add composite data structures.** Right now, svm only supports single, atomic data elements (integers). Add support for arrays, lists, etc, as fundamental items that are understood by the vm. Structures--arbitrary "blocks" of code--could easily be managed as little tiny "heaps" (a la the memory array) so long as there's opcodes for moving values to/from structure fields to the stack (FieldLOAD, FieldSTORE, for example). Note that the difference between the various structures--arrays, lists, fields, etc--are really invisible at this level, assuming you don't care too much about performance; a three-element tuple, a three-element array, and a three-element structure are all basically the same thing in memory, when you think about it.

* **Add objects.** Once you have composite data structures, add functions to the data structure, and you have a pretty decent basis for objects.

* **Add threads.** Kidding! Kidding.