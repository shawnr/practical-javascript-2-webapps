# Tips for Refactoring
In the previous section we discussed techniques for refactoring that are specific to enhancing the separation of concerns in our applications. Those are big concepts and worthy of the thought and effort it takes to implement them. But these are not the only ways to improve our code through refactoring. 

Keep in mind that refactoring is not about achieving performance enhancements or new features. It is about leaving the code more understandable to developers. Refactoring is all about improving the structures of our code so it is easier to maintain and enhance. This is a process of revision, and there are many ways to improve code that do not require as much conceptual thought as untangling logic and data to achieve a good separation of concerns.

## Improve Naming
Probably the most impactful improvement we can make on our code is to improve names where we have opportunities. We can improve the names of data objects, properties, functions, methods, classes, and anything else we have created and defined in our code. High quality names are beneficial to everyone who comes in contact with the work. They make it easier to understand what does what and how pieces go together.

A good metaphor can help guide understanding and even enhancement of a system, providing a shorthand for bigger concepts like relationships and hierarchies. But over time our software metaphors tend to change. Be sure to update naming when metaphors no longer apply. Allowing legacy naming patterns to stick around when they are no longer used creates confusion and leads to mistakes.

Balancing specific, clear names and all of the textual labels required to make software can be challenging. Updating names when concepts or business requirements change is important, and choosing high quality names is essential. Here are some tips for improving naming in our applications:

* Keep names short, but avoid shorthand names (better to be verbose than confused about which abbreviation is preferred)
* Name collections (arrays) with plural names to indicate the set of items
* Name data objects with nouns relevant to the properties they contain
* Avoid repeating parts of a name (e.g. `postTitle`, `postSummary`, `postBody`, `postAuthor`, etc.)
* Avoid overly specific names incorporating brand names, developer initials, etc.
* Use specific names that correspond to concepts/labels used elsewhere in the business
* Handle capitalization and formatting of names according to whatever style guide rules the codebase and do not deviate from those stylistic directives
* Single-letter variable names should never be referenced over more than two or three lines (preferably only in single-line statements) and should be well-scoped

There are many more considerations when naming things in our systems, but leaning on the advice above should at least help us move in the right direction with our renaming efforts.

## Clean Up Files
Do not leave extra files in the repository. If we need to use things like scripts or generate data output files, they should either be kept in a specific, well-defined location in the project, or they should be removed after they have been used. No developers on the project should leave test data or scripts in unexpected locations. 

Every file in the system demands attention from developers. If we work on projects with unused files strewn about, we lose focus on which files actually matter. We may find ourselves wasting time improving something that is not used, be distracted by outdated content, or otherwise be negatively impacted by vestigial files. These files often confuse new developers on the project because they increase the "noise" level in the repository.

## Remove Commented Code and Failed Experiments
Along the same lines as the advice to clean up extraneous files, it's important to let go of commented-out code and failed experiments. Developers often cling to versions that were almost working, or previous attempts they made to make something work. Sometimes we refactor a component, but then we leave the old code commented-out in the file like some monument to the work that came before. Unfortunately, nobody will ever come to see these monuments, and they can only do harm to the project.

Just like with extra files in our repository, having old code lingering in files is dangerous in several ways. First, it creates the potential for confusion on the part of developers. They may become distracted by the contents of the old code, or they may misunderstand and interpret the old code as guidance for something they should be doing. It's even possible to simply goof on a text edit and un-comment lines of old code, thereby causing an error in the software.

If we have trouble letting go of old code in our projects, remember that we can always go back in the history of the project and review what used to be in those files. As long as we're using a version control system, we can easily see the old code whenever we need. This should make us feel fine about deleting all that commented-out code.

## Improve Documentation
An improvement that many people overlook when refactoring is improving documentation. This is, technically, not altering the "structure" of the code, but it can definitely improve the efficiency of developers working on the project. Documentation applies to both longer instructional documents (e.g. "How to get the build deployed" or "How to work with our major feature") and to line comments in the code itself. 

Keep line comments relevant to the current state of the code. When changing functionality, be sure to update the comments, too. Do not leave any erroneous or irrelevant comments in the codebase because bad comments create the same kinds of issues that are created by extra files and legacy code: They cause confusion and increase the chance of developers making mistakes.

It is possible to go overboard on comments. We do not want to write so many comments in our code that it becomes difficult to read and follow the logic. We also do not need to comment on details that are totally evident to a regular developer: We can assume any developer coming into a project understands the basics of the language and platform. We should focus our comments on the elements that make our software unique and which will aid the understanding of the "new" developer. (Don't forget that in six months when we return to this code we, ourselves, will be the "new" developer!)

Here are some tips for writing comments in our code:

* Do not leave old `TODO` comments laying around after completing the task (use the "find in files" or similar tool in an editor to help find comments across all files)
* Do not leave outdated comments that describe functionality that has changed or in some other way become erroneous
* Focus on describing "why" something is happening in the code; don't just describe "what" is happening
* Be consistent in style and formatting of comments
* Describe Classes and major functions/methods with a descriptive block comment at the beginning of the definition
* Use inline comments to describe variables or values without taking up too much space
* If very long documentation is required, move it to another location and reference that location in a shorter comment
* Comment on any unique functionality
* Comment on any implementation that is required due to the use of another tool (e.g. "This configuration is used by XYZ module to accomplish ABC goal.")
* Avoid putting personal information in comments (nobody needs to see your name, rank, serial number, or anything else in the comments)
* Comments are not an art project; consider other developers and the ease of reading comments while working on code

Spending a little extra time to improve comments in our code is something we should do each time we make an edit. If we pay attention to the tips above, we can provide a better experience for everyone working on the project.









