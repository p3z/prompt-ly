# prompt-ly
Many AI interfaces take text prompts from a human user and output a response. From experimenting on the daily over the last 6 months, I've found that it's a pain in the proverbial to keep track of valuable prompts that ellicit certain responses.

For example, let's say we're using ChatGPT or Midjourney, we might discover a particular way of describing things returns predictable output. Thus, we may desire to keep track of such prompts or snippets of prompts for future riffing and further iteration. The problem is you end up with a word doc (if your inclination is anything like mine!) with a list of text with bits bolded, underlined and highlighted a hundred times over for different scenarios. That may be fine for you, if so woohoo! Have at it.

But I was finding it a pain hence in passing I've coined this simple syntax that I can use and amend on the regular so as to give me a semantic framework for keeping track of what I'm calling 'prompt scripts'. Atm, it's mainly for my own use, but you may find it helpful so go for it. Presently, it requires a human to make sense of, but I'll probs get around to building a UI for it at some point to save time.

Simply use the tags to keep track of it all and assign semantics to parts of your prompts. I imagine as these technologies become more prevalent, this kind of thing will become more common. But for now... well here we are.


## Prompt scripts
These are just files that contain prompts for a textbase AI using the 'prompt-ly' syntax (described below) to keep track of things.

## Promptly Syntax

Promptly uses tags in a similar way to HTML to keep things organised. 

### Block Tags
**Constant block**
```
<<<
	THIS BLOCK SHOULD NOT CHANGE
<<<
```
Prompts written inside these tags should never change. 

### Variable block
```
???
	THIS BLOCK IS VARIABLE
???
```
Prompts written inside these tags are subject to change and can be nested inside block tags

### Nested blocks
```
<<<
	THIS IS AN ???EXAMPLE??? THAT USES A VARIABLE
<<<
```
Variable blocks can be nested inside of Constants but not vice versa

### Block-Chaining
```
<<<1
	I SHOULD GO FIRST
<<<1

<<<2
	I SHOULD GO SECOND
<<<2
```
Not to be confused with blockchains (related to crypto, that's a completely different topic!)
Blockchaining, simply lists constant blocks alongside ints to establish and preserve order, handy if you're trying to splice prompts together from different sources and want to keep track of where one ends and one begins (you can of course just throw them all together but if you're experimenting, then you might want to keep track of these things as I've encountered)

### Alternates
You may wish to list variables next to each other to indicate that are interchangeable. Use this syntax so that you can list them all together and yet keep them separate from each other
```
???---
	I AM ONE POSSIBLE VARIABLE
???
	I AM ANOTHER POSSIBLE VARIANT
???
	I AM YET ANOTHER
???---
```
### Source blocks
```
***
	I AM SOURCE MATERIAL, YOU KNOW I HAVE NOT CHANGED
***
```
Use these tags to keep track of original prompts you want to iterate on, as distinct from the overall prompt you're building using the rest of the syntax

### Comments (Single line and encased
```
<<<
	I'm a random prompt
		+++ Im a single line comment, you can safely ignore me
	This prompt now continues
	
	Lorem ipsum dolor +++ Im an encased comment, I will be ignored too +++ sit amet, consectetur adipiscing elit. Etiam enim ante, ultricies eget orci vel, commodo viverra lacus. Nullam eros ligula, condimentum sed congue ut, pretium id velit. Morbi pharetra dictum mi, ac elementum tellus interdum eu. Maecenas luctus ullamcorper urna, ut porttitor tortor maximus eget.
<<<
```
Just like in other languages, handy to be able to annotate your scripts with comments that you can safely ignore from the main working body of your script

## To do
Promptly interpreter: a UI tool that can take a prompt script and trim it down based on passed-in parameters and directives, returning the output as a single text block to be pasted directly into the required tool.

For example, let's say we have a script that takes 4 main variables, if it were a CLI interpreter you might call it like so: 
```
// structure
promptly FILE_NAME ARG1 ARG2 ARG3 ARG4

// example
promptly my_awesome_prompt_script "Tim" SKIP2 "write in the style of an author who has experienced such things firsthand" USE2
```
This example starts the interpreter with the 'promptly' command, it runs the file 'my_awesome_prompt_script' against the interpreter and passes the provided arguments into the script as variables. These are then interpolated like mad libs (where relevant) or interpreted (in the case of directives).

The example invocation might result in something like the following:
1. "Tim": A simple variable that would be interpolated into the first relevant place
2. SKIP2: A directive (distinguished by the use uppercase and the int referring to the argument in question). These might trigger certain actions, for example to completely skip the place in the prompt script that expects a variable
3. "write in the style of an author who has experienced such things firsthand": A longer more complex string. This is just to illustrate that you're not limited to simple strings
4. USE2: A directive that might specify which variable to use in the case of a multiple choice variable being provided directly in the text.

Obviously this is crude and has taken me about 15 mins to come up with the context to the extent that it currently exists, but something to build on in coming days
