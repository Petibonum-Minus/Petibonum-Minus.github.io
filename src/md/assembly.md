# Assembleur

## Introduction

[Source TryhackMe](https://tryhackme.com/room/introtox8664)

## Format

    movq source, destination

This involves:
* Transferring constants(which are prefixed using the $ operator) e.g. movq $3 rax would move the constant 3 to the register
* Transferring values from a register e.g. movq %rax %rbx which involves moving value from rax to rbx
* Transferring values from memory which is shown by putting registers inside brackets e.g. movq %rax (%rbx) which means move value stored in %rax to memory location represented by %rbx.

Intel Data      Type Suffix  Size(bytes)
Byte                b           1
Word                w           2
Double Word         l           4
Quad Word           q           8
Single Precision    s           4
Double Precision    l           8

Some other important instructions are:

* ```leaq source, destination```: this instruction sets destination to the address denoted by the expression in source
* ```addq source, destination```: destination = destination + source
* ```subq source, destination```: destination = destination - source
* ```imulq source, destination```: destination = destination * source
* ```salq source, destination```: destination = destination << source where << is the left bit shifting operator
* ```sarq source, destination```: destination = destination >> source where >> is the right bit shifting operator
* ```xorq source, destination```: destination = destination XOR source
* ```andq source, destination```: destination = destination & source
* ```orq source, destination```: destination = destination | source

## Register

The architecture is x86-64, the registers are 64 bit and Intel has a list of 16 registers:

64 bit  32 bit
%rax    %eax
%rbx    %ebx
%rcx    %ecx
%rdx    %edx
%rsi    %esi
%rdi    %edi
%rsp    %esp
%rbp    %ebp
%r8     %r8d
%r9     %r9d
%r10    %r10d
%r11    %r11d
%r12    %r12d
%r13    %r13d
%r14    %r14d
%r15    %r15d

## Syntax

### AT&T
    (fcn) main 78
    |   int main (int argc, char **argv, char **envp);
    |           ; DATA XREF from entry0 (0x5619ecb9557d)
    |           0x5619ecb9566a      4883ec08       sub rsp, 8
    |           0x5619ecb9566e      b902000000     mov ecx, 2
    |           0x5619ecb95673      ba01000000     mov edx, 1
    |           0x5619ecb95678      488d35c90000.  lea rsi, str.value_for_a_is__d_and_b_is__d ; 0x5619ecb95748 ; "value for a is %d and b is %d\n"
    |           0x5619ecb9567f      bf01000000     mov edi, 1
    |           0x5619ecb95684      b800000000     mov eax, 0
    |           0x5619ecb95689      e8b2feffff     call sym.imp.__printf_chk
    |           0x5619ecb9568e      b901000000     mov ecx, 1
    |           0x5619ecb95693      ba02000000     mov edx, 2
    |           0x5619ecb95698      488d35c90000.  lea rsi, str.value_of_a_is__d_and_b_is__d ; 0x5619ecb95768 ; "value of a is %d and b is %d\n"
    |           0x5619ecb9569f      bf01000000     mov edi, 1
    |           0x5619ecb956a4      b800000000     mov eax, 0
    |           0x5619ecb956a9      e892feffff     call sym.imp.__printf_chk
    |           0x5619ecb956ae      b800000000     mov eax, 0
    |           0x5619ecb956b3      4883c408       add rsp, 8
    \           0x5619ecb956b7      c3             ret

### Intel
    (fcn) main 78
    |   int main (int argc, char **argv, char **envp);
    |           ; DATA XREF from entry0 (0x5619ecb9557d)
    |           0x5619ecb9566a      4883ec08       subq $8, %rsp
    |           0x5619ecb9566e      b902000000     movl $2, %ecx
    |           0x5619ecb95673      ba01000000     movl $1, %edx
    |           0x5619ecb95678      488d35c90000.  leaq str.value_for_a_is__d_and_b_is__d, %rsi ; 0x5619ecb95748 ; "value for a is %d and b is %d\n"
    |           0x5619ecb9567f      bf01000000     movl $1, %edi
    |           0x5619ecb95684      b800000000     movl $0, %eax
    |           0x5619ecb95689      e8b2feffff     callq sym.imp.__printf_chk
    |           0x5619ecb9568e      b901000000     movl $1, %ecx
    |           0x5619ecb95693      ba02000000     movl $2, %edx
    |           0x5619ecb95698      488d35c90000.  leaq str.value_of_a_is__d_and_b_is__d, %rsi ; 0x5619ecb95768 ; "value of a is %d and b is %d\n"
    |           0x5619ecb9569f      bf01000000     movl $1, %edi
    |           0x5619ecb956a4      b800000000     movl $0, %eax
    |           0x5619ecb956a9      e892feffff     callq sym.imp.__printf_chk
    |           0x5619ecb956ae      b800000000     movl $0, %eax
    |           0x5619ecb956b3      4883c408       addq $8, %rsp
    \           0x5619ecb956b7      c3             retq

