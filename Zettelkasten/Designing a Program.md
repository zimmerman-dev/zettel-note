 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚7:55 am  📆 Mon Sep 1
 🔗 **Related Concepts**: #note #cpp
___
## 📝 Note: Designing a Program
### Design step 1: Define your goal
In order to write a successful program, you first need to define what your goal is. Ideally, you should be able to state this in a sentence or two. It is often useful to express this as a user-facing outcome.
### Design step 2: Define requirements
While defining your problem helps you determine _what_ outcome you want, it’s still vague. The next step is to think about requirements. A single problem may yield many requirements, and the solution isn’t “done” until it satisfies all of them.
### Design step 3: Define your tools, targets, and backup plan
When you are an experienced programmer, there are many other steps that typically would take place at this point, including:

- Defining what target architecture and/or OS your program will run on.
- Determining what set of tools you will be using.
- Determining whether you will write your program alone or as part of a team.
- Defining your testing/feedback/release strategy.
- Determining how you will back up your code.
### Design step 4: Break hard problems down into easy problems
instead of solving a single complex task, we break that task into multiple subtasks, each of which is individually easier to solve. If those subtasks are still too difficult to solve, they can be broken down further. By continuously splitting complex tasks into simpler ones, you can eventually get to a point where each individual task is manageable, if not trivial.
### Design step 5: Figure out the sequence of events
Now that your program has a structure, it’s time to determine how to link all the tasks together. The first step is to determine the sequence of events that will be performed.

At this point, we’re ready for implementation.
### Implementation step 1: Outlining your main function
Now we’re ready to start implementation. The above sequences can be used to outline your main program. Don’t worry about inputs and outputs for the time being.
```cpp
int main()
{
//    doBedroomThings();
//    doBathroomThings();
//    doBreakfastThings();
//    doTransportationThings();

    return 0;
}
```
### Implementation step 2: Implement each function
In this step, for each function, you’ll do three things:
1. Define the function prototype (inputs and outputs)
2. Write the function
3. Test the function
### Implementation step 3: Final testing
Once your program is “finished”, the last step is to test the whole program and ensure it works as intended. If it doesn’t work, fix it.