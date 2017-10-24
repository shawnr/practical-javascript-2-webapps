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

## Improve Documentation

