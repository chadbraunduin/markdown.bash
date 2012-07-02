
## What is it?
markdown.bash is a Markdown interpreter using only traditional Unix tools. Specifically, it only uses Bash, Sed, Grep, and Cut (in one small instance).

## Why did I write markdown.bash?
Good question. There already exist Markdown implementations in [a variety of languages][1]. Plus, the [original Markdown][2] was written in Perl which exists on virtually all Unix machines. So I didn't write it for any practical reason. Really I just wanted to see how much of it I could re-engineer in a single Bash script using mostly Sed for the transformations.

## How to use it?
You use it just like any other Unix program - by either passing files to it or piping input into it.

	sh markdown.sh file1 file2 file3 > output.html
	echo "# heading1\n\nparagraph" | sh markdown.sh
	sh markdown.sh samples/test.md
	
## What is missing / different?
By my own rough estimate, markdown.bash implements about 95% of the Markdown language. Still there are some areas where it doesn't.

* It doesn't convert E-mail addresses to a mix of decimal and hex entity-encoding. I really did not know a good, canonical way to do this in Unix/Linux. Suggestions are welcome.
* It processes Markdown inside block-level HTML. According to the original spec:
> Note that Markdown formatting syntax is not processed within block-level HTML tags. E.g., you can’t use Markdown-style *emphasis* inside an HTML block.

markdown.bash does, in fact, process Markdown syntax within block-level HTML. I couldn't think of a good way to implement this exactly like the spec.

* Due to the line-by-line processing nature of Sed, I recommend always putting hard breaks (\\n\\n) between block-level elements (lists, paragraphs, etc). markdown.bash does a lot less implicit processing of elements separated by only one break (\\n) than the Perl version does.

## Kudos
Before starting this project I had only a cursory understanding of Sed. I'm still not an expert, but I do know a lot more now. A couple of web resources were especially helpful.

* [Sed - An Introduction and Tutorial][3]
* [Unix Sed Tutorial][4]


[1]: http://stackoverflow.com/questions/2798123/markdown-why-are-there-numerous-implementations-of-the-markdown-markup-langua
[2]: http://daringfireball.net/projects/markdown/
[3]: http://www.grymoire.com/Unix/Sed.html#uh-55
[4]: http://www.thegeekstuff.com/2009/11/unix-sed-tutorial-multi-line-file-operation-with-6-practical-examples/
