# Entity Comparator

You are refactoring to a [Microservices Architecture](../Microservices/Microservices-Architecture.md) by using the [CQRS]() pattern and are applying [Playback Testing](Playback-Testing.md).  Your situation is complex in that simply checking for the final state of the system after running a number of transactions through the playback would not be sufficient.  This may be because you don't truly understand the way in which the current system functions, or because you do not have a full test suite for the existing system.  

**How do you determine if the new refactored system is working correctly when you aren't sure what transaction results should be a-priori?**

In many refactoring and replacement situations, particularly with older systems, not only are the developers that built the system long gone, but the code may not even be able to be fully analyzed for all possible functional outcomes.  In many older systems, including COTS systems, the source code may be unavailable, or may be written in a language (such as ASM) that is not easily understood.

However, even if the code cannot be easily understood or analyzed to build a functional test suite, what can usually be understood is the data (particuarly data in flat files or a database) that the code produces.  What's more, the data has the advantage of being persistent - you can often write new programs that run asynchronously that the team can use to read the values of the persistent data and report on it to other programs.  

Therefore,

**Build an Entity Comparator that plays back each transaction one at a time and then compares the state of the corresponding affected entities in both the existing and new systems then logs a report of the comparison values discovered throughout the entire playback sequence. **

Applying this pattern will help your team gain confidence in the functional test coverage of the new application even when it is impossible to determine all of the functional requirements of the existing application.  

This pattern is only implemented when you are also implementing the Playback Testing pattern. 
