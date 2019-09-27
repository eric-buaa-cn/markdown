[TOC]

#### Block Elements

##### Paragraph and line breaks

A paragraph is simply one or more consecutive lines of text. In markdown source code, paragraphs are seperated by tow or more blank lines. In Typora, you only need one blank line(press Return once) to create a new paragraph.

Press Shift + Return to create a new single line break. Most other markdown parsers will ignore single line breaks, so in order to make other markdown parsers to recognize your line breaks, you can leave to spaces at the end of the line, or insert <br/\>.

##### headers

Headers use 1-6 hash(#) characters at the start of the line, corresponding to header levels 1-6. For example:

\# This is an H1

\## This is an H2

\###### This is an H6

In Typora, input '#' followed by title content, and press Return key will create a header.

##### Blockquotes

Markdown uses email-style > characters for block quoting. They are presented as:

\> This is a blockquote.

It shows like this:

> This is a blockquote.

In Typora, inputting '>' followed by your quote contents will generate a quote block.  Nested block quotes (a block quote inside another block quote) by adding additional levels of '>'.

##### Lists

unordered list

* red
* green
* blue

ordered list

1. first
2. second
3. third

##### Task List

- [ ] a task list item
- [ ] list syntax required
- [x] completed

##### Code Blocks

```cpp
int main() {
    return 0;
}
```

##### Math Blocks

$$
\mathbf{V}1 \times \mathbf{V}2 =  \begin{vmatrix}
\mathbf{i} & \mathbf{j} & \mathbf{k} \\
\frac{\partial X}{\partial u} & \frac{\partial Y}{\partial u} & 0 \\
\frac{\partial X}{\partial v} & \frac{\partial Y}{\partial v} & 0 \\
\end{vmatrix}
$$

##### Table

| 姓名 | 学校 |
| ---- | ---- |
| 张三 | 北航 |

***

***

##### Emphasis

*italic*

**bold**

This is c code: `print()`

~~strikethrough~~

<u>underline</u>

:happy:

$\lim_{x \to \infty} \exp(-x) = 0 $

$H_2O$

$x^2$

==HIGHLIGHT==

$X_{long\ text}$

