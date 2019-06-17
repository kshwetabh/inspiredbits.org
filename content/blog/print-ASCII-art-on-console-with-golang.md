---
title: "Golang: Print ASCII Art on Console"
date: 2018-11-27T13:05:38+05:30
draft: false
description: TL;DR There's a simple way to output Ascii Art in your command line program if you don't need all the bells and whisles that comes with the external specialized go packages.
tags: [go, automation]
---
Ascii Arts are always fun. Few days back I finished writing a small utility that automates the code generation for the Frontend in my project. It is a command line tool and is meant to be executed on the console (command prompt as its called on Windows). I wanted to print a nice Ascii art whenever it runs. I did some research online and found two options.

- Either use one of the open source libraries that provides many more option for generating dynamic Ascii art
- Or write something by my own (quick and dirty)

I came up with a simple solution that should be obvious for most developers. Guess what ? Simply print the ascii art as string on console using `fmt.Println()` :wink:
This meets my simple requirement. The only con is that I can't generate dynamic Ascii Arts.

### Here are the steps involved:

- To generate and grab ascii art for your text, visit the below link and generate your ascii art. You have around 314 styles (at the time of this writing) to choose from. Link [<a href="http://patorjk.com/software/taag/#p=testall&f=Graffiti&t=Code%20Generator" target="_blank"> patorjk.com</a>]
- Paste the ascii text in your code and define it as a string. Refer the snippet below. Note that the ascii text might contain "**`**" character that interfares with go code so just replace those occurances with something like **'**. Won't make much of a difference in the output.
- You are good to go. Print it on console :smile:

<div class="code">
{{< highlight go "linenos=table,hl_lines=7 17 21 28" >}}
package main

import "fmt"

func main() {
	asciiArt :=
`
=============================================================================
 _____           _        _____                           _             
/  __ \         | |      |  __ \                         | |            
| /  \/ ___   __| | ___  | |  \/ ___ _ __   ___ _ __ __ _| |_ ___  _ __ 
| |    / _ \ / _' |/ _ \ | | __ / _ \ '_ \ / _ \ '__/ _' | __/ _ \| '__|
| \__/\ (_) | (_| |  __/ | |_\ \  __/ | | |  __/ | | (_| | || (_) | |   
 \____/\___/ \__,_|\___|  \____/\___|_| |_|\___|_|  \__,_|\__\___/|_|   
																		  
=============================================================================
`
	fmt.Println(asciiArt)

	asciiArt =
`
=============================================================================
 __   __   __   ___     __   ___       ___  __       ___  __   __  
/  ' /  \ |  \ |__     / _' |__  |\ | |__  |__)  /\   |  /  \ |__) 
\__, \__/ |__/ |___    \__> |___ | \| |___ |  \ /~~\  |  \__/ |  \ 

=============================================================================
`
	fmt.Println(asciiArt)
}
{{< / highlight >}}  
</div>

<br />
**And here's the short and sweet output:**

<a href="/images/asciiart.jpg"><img src="/images/asciiart.jpg" alt="Eslint AstExplorer Image" class="responsive-post-image"/></a>