---
layout: blog_post
title: "Test blog post"
categories: blog
tags: test
author: "Example Author"
type: blog
img_tag: <img src="/img/posts/overspecialization.png" class="blog-photo">
img: posts/overspecialization.png
---

<em>Author's Note:</em> This post is a test. Content is copied directly from the Crimson Vista website.

<hr />

&nbsp;

I love programming languages. I've been studying them for over a decade, and my <a href="http://sequoia.cs.byu.edu/lab/files/pubs/Nielson2004b.pdf">Master's thesis</a> was focused entirely on what I saw as "multi-paradigm" trends within the popular object-oriented languages of the 2002-2004 time frame. In short, I suggested that pure OO languages were becoming OO++; that they would incorporate more idioms and approaches from other paradigms over time.

In this one instance, my research was amazingly prescient. C++ has embraced an exceptional range of functional programming concepts. Consider this quote from "<a href="http://www.amazon.com/Modern-Design-Generic-Programming-Patterns/dp/0201704315">Modern C++ Design</a>" by Andrei Alexandrescu.

<blockquote>Therefore, although C++ is mostly an imperative language, any compile-time computation must rely on techniques that definitely are reminiscent of pure functional languages...

[p. 54]</blockquote>
Alexandrescu goes on to talk about a number of functional concepts, including functions as first-class data. It's really quite exciting.

With that said, I'm also surprised at the <em>complexity </em>for performing relatively basic operations in this modern, multi-paradigm C++. Alexandrescu talks about some of the most awkward mechanisms for what should be straight-forward tasks like error checking and sub-type checking. Here's an example:

<!--more-->
<blockquote>This way, the [code] yields either an allegedly correct [data] or an [error] at runtime.

Obviously, it would be more desirable to detect such an error during compilation...

There is hope; the expression being evaluated is a compile-time constant, which means that you can have the compiler, instead of runtime code, check it.

[p. 24]</blockquote>
So far, so good. I like where this is going. Detecting errors <em>before</em> the program is running sounds like a great idea. And having an automated compiler do the checking also seems like a great idea. But the very next sentence seems almost non-sequitur:

<blockquote>The idea is to pass the compiler a language construct that is legal for a nonzero expression and illegal for an expression that evaluates to zero.

[p. 24]</blockquote>
What?! What in the world does checking for an error have to do with a language evaluation? For those technically curious, the approach is to write a piece of code that causes a compile time error when there's a data size mismatch. But even if you can accept this, check out the code that Alexandrescu uses:

<blockquote>The <em>simplest solution</em> to compile-time assertions (Van Horn 1997), and one that works in C as well as C++, <em><span style="text-decoration: underline;">relies on the fact that a zero-length array is illegal</span>.</em>

[p.24 (Emphasis Added)]</blockquote>
Are you catching the image? For checking if there's enough space to copy from one data type to another, we're going to evaluate their sizes and, if it's big enough, it will create a one-element array. If they're not big enough, it will create a zero-element array in order to cause an error. Just so you know, this array is never used. It has no purpose other than to create an error.

It turns out that the compiler really wasn't intended to do the kind of programming it's doing, and certainly has no error checking capabilities for this insult to its object-oriented nature. Don't get me wrong, every programming language has weird oddities and unholy abominations of black magic that the arcane acolytes employ to create their bizarre monsters for the strange edge-cases of computer programming.

But this is chapter two of a book about C++ design. This is Standard Operating Procedure for compile-time error checking. This is not supposed to be arcane, but common.

I'm not even done yet. It gets much, much worse. It turns out that the error created by this monstrosity is very difficult to understand:

<blockquote>The problem with this approach is that the error message you receive is not terribly informative. "Cannot create array of size zero" does not suggest "Type char is too narrow to hold a pointer."

[p. 24]</blockquote>
Really? Understatement much?

<blockquote>A better solution is to rely on a template with an informative name; <em><span style="text-decoration: underline;">with luck, the compiler will mention the name of that template in the error message</span>. </em>

[p. 25 (Emphasis Added)]</blockquote>
Well I feel so much more confident after reading that. The author spends the next two pages walking the user through naming conventions and compiler quirks in order to get them to the point that they can produce a useful error message.

While I won't go through another example from the same chapter with the same detail, here is what the author has to say about another method for compile-time type checking:

<blockquote>(Passing a C++ object to a function with ellipses had undefined results, but this doesn't matter. Nothing actually calls the function. It's not even implemented. Recall that sizeof does not evaluate its argument.)

... (Remember, we're in the sizeof wonderland where no expression is actually evaluated.)...

(By the way, <em><span style="text-decoration: underline;">isn't it nifty just how much you can do with functions, like MakeT and Test, that not only don't do anything but don't even really exist at all?</span>)</em>

[pp. 35-36 (Emphasis Added)]</blockquote>
Oh, but how I laughed after reading these parenthetical statements from an author that definitely loves what he does.

At this point, I want to make it clear that I am not maligning C++ at all or the approaches suggested above. These features are, in fact, very powerful. From a security perspective, every error caught at compile time is absolutely significant. Errors are the lifeblood of hackers. Errors are the cracks in the walls, the blind spots in the sensors, and the turncoats in the software government. Every error eliminated is one less vector for the bad guy to exploit.

But on the flip side, this example illustrates how our advanced technology requires massive specialization of human knowledge and expertise. I have been writing programs for twenty plus years, including a fair number of C++ projects, and this basic error-checking is something I'm not very familiar with. Truthfully, I'm reading Alexandrescu's book in order to bring myself current with the ongoing evolution of the C++ language.

There are security issues with depending on such deep specialization.

I remember in my computer architecture class back in 1996 that the professor had just come from industry and was familiar with the development of the original Pentium. He said the chip was so complicated that most of the engineers had no idea how it worked altogether, and had to focus on their one small specialty. One can only imagine how much worse it is this many iterations of hardware later.

When computer security is fragmented into deep specialists, it can create new, or conceal existing, holes in the spaces between the specialties as I've visualized below:

<img class="alignnone wp-image-100 size-large" src="/images/overspecialization.png" alt="Specializations and Exploits" width="1024" height="576" />

The really frustrating thing is that the bad guys do <em>not</em> have to be specialists in order to find weaknesses and vulnerabilities. Any good analyst knows how much less knowledge you need to understand (and potentially exploit) a system than to create one of similar size, complexity, and functionality. I have performed dozens of source code reviews for many clients over the years, and I have sometimes had to learn a new programming language literally when I stepped into the code review room. But within hours I could already begin to piece together how the program worked. Within a day or two, I could trace down just about any major functional component.

Although in the graphic above, I've trivialized the illustration to visually depict a noticeable gap, in reality, most attacks involve a series of steps across a wide range of systems. The bad guys find a minor SQL injection attack on a low-priority database, but in cracking the database, they break a password that they can use on another system. A firewall is misconfigured that enables them to connect from their compromised system to a more trusted internal network. And once inside, a compromised Windows machine enables them to reach their final destination.

Defeating that kind of bad guy is incredibly difficult, especially for security professionals that get so focused on their specialty that they lose sight of the big picture. We need the specialists, of course. And we will need deeper and deeper specialties as technology grows more complex. But we cannot lose sight of the overall context, nor undervalue the generalists that work to keep the fragments connected.
