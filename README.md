# selpg-in-Go
An assignment for course : service computing.

# Selpg

Selpg represents SELect PaGes.

It allows the user to extract the range of a text specifically. The input text can be from a file or a process.

## Development Environment

* Ubuntu : 16.04-desktop-amd64

* Golang : go1.6.2 linux/amd64

* Atom : 1.21.0

## Build Setup

    go get github.com/renleimlj/selpg-in-Go

## Usage

    selpg -s=Number -e=Number [options] [filename]
1. -l ---------- Determine the number of lines per page and default is 72.

1. -f ---------- Determine the type and the way to be seprated.

1. [filename] ---------- Read input from this file.

1. If filename is not given, it will read input from stdin. Ctrl+D to cutout.

## Test

Create a txt file named test.txt to test if this selpg code can run and get correct response.

    FROM fairest creatures we desire increase,
    That thereby beauty's rose might never die,
    But as the riper should by time decease,
    His tender heir might bear his memory;
    But thou, contracted to thine own bright eyes,
    Feed'st thy light's flame with self-substantial fuel,
    Making a famine where abundance lies,
    Thyself thy foe, to thy sweet self too cruel.
    Thout that are now the world's fresh ornament
    And only herald to the gaudy spring,
    Within thine own bud buriest thy content
    And, tender churl, mak'st waste in niggarding.
    Pity the world, or else this glutton be,
    To eat the world's due, by the grave and thee.
    WHEN forty winters shall besiege thy brow
    And dig deep trenches in thy beauty's field,
    Thy youth's proud livery, so gazed on now,
    Will be a tottered weed of small worth held:
    Then being asked where all thy beauty lies,
    Where all the treasure of thy lusty days,
    To say within thine own deep-sunken eyes
    Were an all-eating shame and thriftless praise.
    How much more prasie deserved thy beauty's use
    If thou couldst answer, 'This fair child of mine
    Shall sum my count and make my old excuse,'
    Proving his beauty by succession thine.
    This were to be new made when thou art old
    And see thy blood warm when thou feel'st cold.

* Test `selpg -s 1 -e 1  -l 20 test`

        To say within thine own deep-sunken eyes
        Were an all-eating shame and thriftless praise.
        How much more prasie deserved thy beauty's use
        If thou couldst answer, 'This fair child of mine
        Shall sum my count and make my old excuse,'
        Proving his beauty by succession thine.
        This were to be new made when thou art old
        And see thy blood warm when thou feel'st cold.

* Test `cat test | selpg -s 2 -e 3 -l 5`

        Within thine own bud buriest thy content
        And, tender churl, mak'st waste in niggarding.
        Pity the world, or else this glutton be, 
        To eat the world's due, by the grave and thee.
        WHEN forty winters shall besiege thy brow
        And dig deep trenches in thy beauty's field,
        Thy youth's proud livery, so gazed on now,
        Will be a tottered weed of small worth held:
        Then being asked where all thy beauty lies,
        Where all the treasure of thy lusty days,

* Test `selpg -s=1 -e=1 -l 6 < test`

        Making a famine where abundance lies,
        Thyself thy foe, to thy sweet self too cruel.
        Thout that are now the world's fresh ornament
        And only herald to the gaudy spring,
        Within thine own bud buriest thy content
        And, tender churl, mak'st waste in niggarding.
        Pity the world, or else this glutton be, 
        To eat the world's due, by the grave and thee.
        WHEN forty winters shall besiege thy brow
        And dig deep trenches in thy beauty's field,
        Thy youth's proud livery, so gazed on now,
        Will be a tottered weed of small worth held:

* Test `selpg -s 2 -e 2 -l 5 test >output`

        Within thine own bud buriest thy content
        And, tender churl, mak'st waste in niggarding.
        Pity the world, or else this glutton be, 
        To eat the world's due, by the grave and thee.
        WHEN forty winters shall besiege thy brow
    以上是output文件中的内容，可以通过 `more output` 来查看。

* Test `selpg -s -2 -e 1 -l 5 test >output 2 > error`

    输入 `more output`，查看得到usage讲解：

        The following is usage of selpg.
                selpg -s=Number -e=Number [options] [filename]
                        -l ---------- Determine the number of lines per page and default is 72.
                        -f ---------- Determine the type and the way to be seprated.
                        [filename] ---------- Read input from this file.
                        If filename is not given, it will read input from stdin. Ctrl+D to cutout.
    输入 `more error`，得到错误日志：

        The range of the page is invalid

* Test `selpg -s 2 -l 5 test>output 2>error`

    输入 `more output`，查看得到usage讲解：

        The following is usage of selpg.
                selpg -s=Number -e=Number [options] [filename]
                        -l ---------- Determine the number of lines per page and default is 72.
                        -f ---------- Determine the type and the way to be seprated.
                        [filename] ---------- Read input from this file.
                        If filename is not given, it will read input from stdin. Ctrl+D to cutout.
    输入 `more error`，得到错误日志：

        selpg: not enough arguments
        selpg: 2nd arg should be -eend_page
