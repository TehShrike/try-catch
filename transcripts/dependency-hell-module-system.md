# Every module import system sucks

- dependency hell is real
- most languages reference libraries by namespace
	- import a file directly, everything it contains is now visible to you
	- import an identifier like a package or class, and the compiler expects to find a single file providing that identifier when it goes to build
- What happens if you depend on SuperCoolTool and UsefulBusinessThing, and UsefulBusinessThing depends on a really old version of SuperCoolTool?
