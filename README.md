Download Link: https://assignmentchef.com/product/solved-csci2500-final-project-pipelined-mips-simulator
<br>



For this team-based project, you will implement a pipelined MIPS simulator, building on the pipelining concepts covered in Homework 5. As a reminder, there are five stages to the pipeline, i.e., IF, ID, EX, MEM, and WB.

For your simulation, you are required to support the add, addi, and, andi, or, ori, slt, slti, beq, and bne instructions; note that pseudo-instructions are not supported and that the $zero register may be used. More specifically, you must simulate the execution of a given set of instructions, showing the register contents as each instruction executes.

You must also show how the given sequence of instructions would be pipelined in a five-stage MIPS implementation. For this project, you must be able to support data hazards, forwarding, and control hazards.

You can assume that each given instruction will be syntactically correct. You can also assume that there is a single space character between the instruction and its parameters. Further, each parameter is delimited by a comma or parentheses. And you must support the usual set of $t and

$s registers.

Since we are supporting branch instructions, labels must also be supported; you can assume that a label is all lowercase and is on a line by itself.

Below are a few example instructions and labels that you must support:

loop:

add $t0,$s2,$s3 addi $t1,$t3,73 or $s0,$zero,$t3 ori $s1,$zero,123 xyz:

slt $t3,$s1,$s2 beq $t2,$t4,loop

<h2>Required Command-Line Arguments</h2>

Your program must accept two command-line arguments as input. The first argument (i.e., argv[1]) is a single character, either ‘F’ or ‘N’, that corresponds to supporting “Forwarding” mode or “Nonforwarding” mode.

The second argument (i.e., argv[2]) specifies the input file containing MIPS code to simulate. You may assume that no more than ten instructions are given in the input file. And note that each instruction will end with a newline character (i.e., ‘
’).

<h2>Required Output</h2>

For your output, you must show <em>each cycle </em>of program execution, including the contents of the registers. To show the registers, use four columns, each with a fixed width of 20 characters. Display the $s registers first, then the $t registers. Be sure there are no trailing spaces on the end of each line of output.

And as with Homework 5, for the pipeline, each cycle will correspond to a column of output. Initially, each column is empty, indicated by a period (i.e., ‘.’). And note that all registers are assumed to be initialized to zero.

Unlike Homework 5, use fixed-width formatting (e.g., printf()) to delimit each column. More specifically, the first column must have a width of exactly 20 characters, while each subsequent column (corresponding to each clock cycle) must have a width of exactly four characters. Include a space between each column and left-justify each column. Further, be sure there are no trailing spaces on the end of each line of output.

Finally, show no more than 16 cycles in your simulation, meaning that if you reach cycle 16, display that last cycle and end your simulation.

<h2>Handling Data and Control Hazards</h2>

Recall that a <em>data hazard </em>describes a situation in which the next instruction cannot be executed in the next cycle until a previous instruction is complete. Your code should be able to detect when it is necessary to insert one or more “bubbles” (see Section 4.7 of the textbook and corresponding lecture notes for more details).

As you did on Homework 5, you will need to properly handle data hazards by adding nop instructions as necessary. Show these cases by indicating an asterisk (i.e., ‘*’) in the appropriate columns and adding the required number of nop instructions.

Data hazards are obstacles to pipelined execution, but in some instances, we can use <em>forwarding </em>to forward intermediate data as soon as it becomes available (i.e., after the EX stage) on to those components that need it. If the forwarding argument is set, then you should simulate forwarding (as illustrated in Figures 4.29 and 4.53 of our textbook).

Finally, for control hazards, you should use a prediction model that assumes the branch will <em>not </em>be taken. Recall that the decision to branch is decided at the MEM stage of the branch instruction. Therefore, if the branch is taken (i.e., we predicted incorrectly), the instructions (at most, three) that have been fetched and decoded must be discarded, with execution continuing at the branch target. Show this by indicating an asterisk (i.e., ‘*’) in the appropriate columns.

On the next few pages, we present a few example runs of your program that you should use to better understand how your program should work, how you can test your code, and what output formatting to use for Submitty. More examples will be made available as we get closer to the project deadline.

The first example (i.e., ex01.s) includes no data hazards (or forwarding).

bash$ cat ex01.s ori $s1,$zero,451 addi $t2,$s0,73 add $t4,$s3,$s7 bash$ ./a.out N ex01.s

START OF SIMULATION (no forwarding)

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="92">1        2        3</td>

   <td width="31">4</td>

   <td width="31">5</td>

   <td width="92">6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="92">IF .               .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="92">$s1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="92">$s5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="92">$t1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="92">$t5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="92">1        2        3</td>

   <td width="31">4</td>

   <td width="31">5</td>

   <td width="92">6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="92">IF ID .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$s0,73</td>

   <td width="92">.            IF .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="92">$s1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="92">$s5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="92">$t1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="92">$t5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="122">1        2        3        4</td>

   <td width="31">5</td>

   <td width="92">6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="122">IF ID EX .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$s0,73</td>

   <td width="122">.               IF ID .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">add $t4,$s3,$s7</td>

   <td width="122">.         .            IF .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="122">$s1 = 0</td>

   <td width="31"> </td>

   <td width="92">$s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="122">$s5 = 0</td>

   <td width="31"> </td>

   <td width="92">$s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="122">$t1 = 0</td>

   <td width="31"> </td>

   <td width="92">$t2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="122">$t5 = 0</td>

   <td width="31"> </td>

   <td width="92">$t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t8 = 0</td>

   <td width="122">$t9 = 0</td>

   <td width="31"> </td>

   <td width="92"> </td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92"> </td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="153">1        2        3        4        5</td>

   <td width="92">6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="153">IF ID EX MEM .</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$s0,73</td>

   <td width="153">.                 IF ID EX .</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">add $t4,$s3,$s7</td>

   <td width="153">.         .              IF ID .</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="153">$s1 = 0</td>

   <td width="92">$s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="153">$s5 = 0</td>

   <td width="92">$s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="153">$t1 = 0</td>

   <td width="92">$t2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="153">$t5 = 0</td>

   <td width="92">$t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t8 = 0</td>

   <td width="153">$t9 = 0</td>

   <td width="92"> </td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92"> </td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="244">1        2        3        4        5        6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="244">IF ID EX MEM WB .                        .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$s0,73</td>

   <td width="244">.                IF ID EX MEM .               .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">add $t4,$s3,$s7</td>

   <td width="244">.         .                IF ID EX .                .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="244">$s1 = 451                                   $s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="244">$s5 = 0                                       $s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="244">$t1 = 0                                        $t2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="244">$t5 = 0                                        $t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="244">1        2        3        4        5        6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="244">IF ID EX MEM WB .                        .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$s0,73</td>

   <td width="244">.                 IF ID EX MEM WB .                .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">add $t4,$s3,$s7</td>

   <td width="244">.         .               IF ID EX MEM .               .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="244">$s1 = 451                                   $s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="244">$s5 = 0                                       $s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="244">$t1 = 0                                        $t2 = 73</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="244">$t5 = 0                                        $t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="244">1        2        3        4        5        6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="244">IF ID EX MEM WB .                        .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$s0,73</td>

   <td width="244">.                 IF ID EX MEM WB .                .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">add $t4,$s3,$s7</td>

   <td width="244">.         .                IF ID EX MEM WB .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="244">$s1 = 451                                   $s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="244">$s5 = 0                                       $s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="244">$t1 = 0                                        $t2 = 73</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="244">$t5 = 0                                        $t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

END OF SIMULATION

The second example (i.e., ex02.s) includes a dependency on register $s1, but no forwarding.

bash$ cat ex02.s ori $s1,$zero,451 addi $t2,$s0,73 add $t4,$s1,$s7 bash$ ./a.out N ex02.s

START OF SIMULATION (no forwarding)

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="92">1        2        3</td>

   <td width="31">4</td>

   <td width="31">5</td>

   <td width="92">6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="92">IF .               .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="92">$s1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="92">$s5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="92">$t1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="92">$t5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="92">1        2        3</td>

   <td width="31">4</td>

   <td width="31">5</td>

   <td width="92">6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="92">IF ID .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$s0,73</td>

   <td width="92">.            IF .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="92">$s1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="92">$s5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="92">$t1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="92">$t5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="122">1        2        3        4</td>

   <td width="31">5</td>

   <td width="92">6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="122">IF ID EX .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$s0,73</td>

   <td width="122">.               IF ID .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">add $t4,$s1,$s7</td>

   <td width="122">.         .            IF .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="122">$s1 = 0</td>

   <td width="31"> </td>

   <td width="92">$s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="122">$s5 = 0</td>

   <td width="31"> </td>

   <td width="92">$s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="122">$t1 = 0</td>

   <td width="31"> </td>

   <td width="92">$t2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="122">$t5 = 0</td>

   <td width="31"> </td>

   <td width="92">$t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t8 = 0</td>

   <td width="122">$t9 = 0</td>

   <td width="31"> </td>

   <td width="92"> </td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92"> </td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="153">1        2        3        4        5</td>

   <td width="92">6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="153">IF ID EX MEM .</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$s0,73</td>

   <td width="153">.                 IF ID EX .</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">add $t4,$s1,$s7</td>

   <td width="153">.         .              IF ID .</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="153">$s1 = 0</td>

   <td width="92">$s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="153">$s5 = 0</td>

   <td width="92">$s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="153">$t1 = 0</td>

   <td width="92">$t2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="153">$t5 = 0</td>

   <td width="92">$t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t8 = 0</td>

   <td width="153">$t9 = 0</td>

   <td width="92"> </td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92"> </td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="244">1        2        3        4        5        6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="244">IF ID EX MEM WB .                        .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$s0,73</td>

   <td width="244">.                IF ID EX MEM .               .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">nop</td>

   <td width="244">.         .             IF ID *              .         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">add $t4,$s1,$s7</td>

   <td width="244">.         .                 IF ID ID .                .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="244">$s1 = 451                                   $s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="244">$s5 = 0                                       $s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="244">$t1 = 0                                        $t2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="244">$t5 = 0                                        $t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="244">1        2        3        4        5        6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="244">IF ID EX MEM WB .                        .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$s0,73</td>

   <td width="244">.                 IF ID EX MEM WB .                .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">nop</td>

   <td width="244">.         .             IF ID *             *        .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">add $t4,$s1,$s7</td>

   <td width="244">.         .                   IF ID ID EX .                   .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="244">$s1 = 451                                   $s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="244">$s5 = 0                                       $s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="244">$t1 = 0                                        $t2 = 73</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="244">$t5 = 0                                        $t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="244">1        2        3        4        5        6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="244">IF ID EX MEM WB .                        .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$s0,73</td>

   <td width="244">.                 IF ID EX MEM WB .                .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">nop</td>

   <td width="244">.         .             IF ID *             *       *        .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">add $t4,$s1,$s7</td>

   <td width="244">.         .                  IF ID ID EX MEM .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="244">$s1 = 451                                   $s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="244">$s5 = 0                                       $s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="244">$t1 = 0                                        $t2 = 73</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="244">$t5 = 0                                        $t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t8 = 0</td>

   <td width="244">$t9 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92"> </td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="275">1        2        3        4        5        6        7        8        9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="275">IF ID EX MEM WB .                        .         .         .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$s0,73</td>

   <td width="275">.                 IF ID EX MEM WB .                .         .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">nop</td>

   <td width="275">.         .             IF ID *             *       *        .         .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">add $t4,$s1,$s7</td>

   <td width="275">.         .                   IF ID ID EX MEM WB .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="275">$s1 = 451                                   $s2 = 0</td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="275">$s5 = 0                                       $s6 = 0</td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="275">$t1 = 0                                        $t2 = 73</td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 451</td>

   <td width="275">$t5 = 0                                        $t6 = 0</td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

END OF SIMULATION

The third example (i.e., again ex02.s) includes a dependency on register $s1, this time with forwarding.

bash$ cat ex02.s ori $s1,$zero,451 addi $t2,$s0,73 add $t4,$s1,$s7 bash$ ./a.out F ex02.s

START OF SIMULATION (forwarding)

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="92">1        2        3</td>

   <td width="31">4</td>

   <td width="31">5</td>

   <td width="92">6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="92">IF .               .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="92">$s1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="92">$s5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="92">$t1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="92">$t5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t8 = 0</td>

   <td width="92">$t9 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92"> </td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92"> </td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="92">1        2        3</td>

   <td width="31">4</td>

   <td width="31">5</td>

   <td width="92">6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="92">IF ID .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$s0,73</td>

   <td width="92">.            IF .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="92">$s1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="92">$s5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="92">$t1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="92">$t5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t8 = 0</td>

   <td width="92">$t9 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92"> </td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92"> </td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="122">1        2        3        4</td>

   <td width="31">5</td>

   <td width="92">6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="122">IF ID EX .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$s0,73</td>

   <td width="122">.               IF ID .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">add $t4,$s1,$s7</td>

   <td width="122">.         .            IF .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="122">$s1 = 0</td>

   <td width="31"> </td>

   <td width="92">$s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="122">$s5 = 0</td>

   <td width="31"> </td>

   <td width="92">$s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="122">$t1 = 0</td>

   <td width="31"> </td>

   <td width="92">$t2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="122">$t5 = 0</td>

   <td width="31"> </td>

   <td width="92">$t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="153">1        2        3        4        5</td>

   <td width="92">6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="153">IF ID EX MEM .</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$s0,73</td>

   <td width="153">.                 IF ID EX .</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">add $t4,$s1,$s7</td>

   <td width="153">.         .              IF ID .</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="153">$s1 = 0</td>

   <td width="92">$s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="153">$s5 = 0</td>

   <td width="92">$s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="153">$t1 = 0</td>

   <td width="92">$t2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="153">$t5 = 0</td>

   <td width="92">$t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t8 = 0</td>

   <td width="153">$t9 = 0</td>

   <td width="92"> </td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92"> </td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="244">1        2        3        4        5        6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="244">IF ID EX MEM WB .                        .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$s0,73</td>

   <td width="244">.                IF ID EX MEM .               .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">add $t4,$s1,$s7</td>

   <td width="244">.         .                IF ID EX .                .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="244">$s1 = 451                                   $s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="244">$s5 = 0                                       $s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="244">$t1 = 0                                        $t2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="244">$t5 = 0                                        $t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="244">1        2        3        4        5        6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="244">IF ID EX MEM WB .                        .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$s0,73</td>

   <td width="244">.                 IF ID EX MEM WB .                .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">add $t4,$s1,$s7</td>

   <td width="244">.         .               IF ID EX MEM .               .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="244">$s1 = 451                                   $s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="244">$s5 = 0                                       $s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="244">$t1 = 0                                        $t2 = 73</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="244">$t5 = 0                                        $t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="244">1        2        3        4        5        6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="244">IF ID EX MEM WB .                        .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$s0,73</td>

   <td width="244">.                 IF ID EX MEM WB .                .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">add $t4,$s1,$s7</td>

   <td width="244">.         .                IF ID EX MEM WB .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="244">$s1 = 451                                   $s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="244">$s5 = 0                                       $s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="244">$t1 = 0                                        $t2 = 73</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 451</td>

   <td width="244">$t5 = 0                                        $t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

END OF SIMULATION

The fourth example (i.e., ex03.s) illustrates a control hazard, with forwarding.

bash$ cat ex03.s ori $s1,$zero,451 loop:

addi $t2,$t2,73 slti $t4,$s1,453 addi $s1,$s1,1 bne $t4,$zero,loop ori $s6,$t6,77 add $s7,$s0,$s0 andi $s2,$t5,255 bash$ ./a.out F ex03.s

START OF SIMULATION (forwarding)

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="92">1        2        3</td>

   <td width="31">4</td>

   <td width="31">5</td>

   <td width="92">6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="92">IF .               .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="92">$s1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="92">$s5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="92">$t1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="92">$t5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="92">1        2        3</td>

   <td width="31">4</td>

   <td width="31">5</td>

   <td width="92">6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="92">IF ID .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$t2,73</td>

   <td width="92">.            IF .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="92">$s1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="92">$s5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="92">$t1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="92">$t5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153">CPU Cycles ===&gt;</td>

   <td width="122">1        2        3        4</td>

   <td width="31">5</td>

   <td width="92">6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="153">ori $s1,$zero,451</td>

   <td width="122">IF ID EX .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$t2,73</td>

   <td width="122">.               IF ID .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">slti $t4,$s1,453</td>

   <td width="122">.         .            IF .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="122">$s1 = 0</td>

   <td width="31"> </td>

   <td width="92">$s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="122">$s5 = 0</td>

   <td width="31"> </td>

   <td width="92">$s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="122">$t1 = 0</td>

   <td width="31"> </td>

   <td width="92">$t2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 0</td>

   <td width="122">$t5 = 0</td>

   <td width="31"> </td>

   <td width="92">$t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="153">$t8 = 0</td>

   <td width="122">$t9 = 0</td>

   <td width="31"> </td>

   <td width="92"> </td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92"> </td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

———————————————————————————-




$s4 = 0                                        $s5 = 0                                     $s6 = 0                                     $s7 = 0

$t0 = 0                                        $t1 = 0                                      $t2 = 0                                      $t3 = 0

$t4 = 0                                        $t5 = 0                                      $t6 = 0                                      $t7 = 0

$t8 = 0                                        $t9 = 0

<table width="0">

 <tbody>

  <tr>

   <td width="153"> </td>

   <td width="153">IF ID EX MEM .</td>

   <td width="92">.</td>

   <td width="115"> </td>

  </tr>

  <tr>

   <td width="153"> </td>

   <td width="153">.                 IF ID EX .</td>

   <td width="92">.         .</td>

   <td width="115"> </td>

  </tr>

  <tr>

   <td width="153"> </td>

   <td width="153">.         .              IF ID .</td>

   <td width="92">.         .         .</td>

   <td width="115"> </td>

  </tr>

  <tr>

   <td width="153"> </td>

   <td width="153">.         .         .            IF .</td>

   <td width="92">.         .         .</td>

   <td width="115">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="153">$s1 = 0</td>

   <td width="92">$s2 = 0</td>

   <td width="115">$s3 = 0</td>

  </tr>

 </tbody>

</table>

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="397">CPU Cycles ===&gt;                 1        2        3        4        5        6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="397">ori $s1,$zero,451                         IF ID EX MEM WB .                .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="397">addi $t2,$t2,73                      .               IF ID EX MEM .               .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="397">slti $t4,$s1,453                      .         .                IF ID EX .                .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="397">addi $s1,$s1,1                        .         .         .              IF ID .              .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="397">bne $t4,$zero,loop .                     .         .         .            IF .            .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="397">$s0 = 0                                        $s1 = 451                                $s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="397">$s4 = 0                                       $s5 = 0                                     $s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="397">$t0 = 0                                        $t1 = 0                                      $t2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="397">$t4 = 0                                        $t5 = 0                                      $t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="397">CPU Cycles ===&gt;                 1        2        3        4        5        6        7        8</td>

   <td width="31">9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td width="397">ori $s1,$zero,451                         IF ID EX MEM WB .                .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="397">addi $t2,$t2,73                      .                IF ID EX MEM WB .                .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="397">slti $t4,$s1,453                      .         .               IF ID EX MEM .               .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="397">addi $s1,$s1,1                        .         .         .                IF ID EX .                .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="397">bne $t4,$zero,loop .                     .         .         .              IF ID .              .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="397">ori $s6,$t6,77                         .         .         .         .         .            IF .           .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="397">$s0 = 0                                        $s1 = 451                                $s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="397">$s4 = 0                                       $s5 = 0                                     $s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="397">$t0 = 0                                        $t1 = 0                                      $t2 = 73</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="397">$t4 = 0                                        $t5 = 0                                      $t6 = 0$t8 = 0                                        $t9 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153"> </td>

   <td colspan="2" width="244">IF ID EX MEM .</td>

   <td width="31">.</td>

   <td width="31"> </td>

   <td width="53"> </td>

  </tr>

  <tr>

   <td width="153"> </td>

   <td width="122">.</td>

   <td width="122">IF ID EX .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="53"> </td>

  </tr>

  <tr>

   <td width="153"> </td>

   <td width="122">.</td>

   <td width="122">.               IF ID .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="53"> </td>

  </tr>

  <tr>

   <td width="153"> </td>

   <td width="122">.</td>

   <td width="122">.         .            IF .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="53">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="122">$s1 = 451</td>

   <td width="122">$s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="53">$s3 = 0</td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="122">$s5 = 0</td>

   <td width="122">$s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="53">$s7 = 0</td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="122">$t1 = 0</td>

   <td width="122">$t2 = 73</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="53">$t3 = 0</td>

  </tr>

  <tr>

   <td width="153">$t4 = 1</td>

   <td width="122">$t5 = 0</td>

   <td width="122">$t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="53">$t7 = 0</td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td colspan="2" width="428">CPU Cycles ===&gt;                 1        2        3        4        5        6        7        8        9</td>

   <td colspan="5" width="199">10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td colspan="2" width="428">ori $s1,$zero,451                         IF ID EX MEM WB .                .         .         .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td colspan="2" width="428">addi $t2,$t2,73                      .                IF ID EX MEM WB .                .         .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td colspan="2" width="428">slti $t4,$s1,453                      .         .                IF ID EX MEM WB .                .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="244">addi $s1,$s1,1                        .         .         .</td>

   <td width="183">IF ID EX MEM WB .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="244">bne $t4,$zero,loop .                     .         .</td>

   <td width="183">.                IF ID EX MEM .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="244">ori $s6,$t6,77                         .         .         .</td>

   <td width="183">.         .                IF ID EX .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="244">add $s7,$s0,$s0                    .         .         .</td>

   <td width="183">.         .         .              IF ID .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="244">andi $s2,$t5,255                   .         .         .</td>

   <td width="183">.         .         .         .            IF .</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="244">$s0 = 0                                        $s1 = 452</td>

   <td width="183">$s2 = 0</td>

   <td width="31"> </td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="244">$s4 = 0                                       $s5 = 0</td>

   <td width="183">$s6 = 0</td>

   <td width="31"> </td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="244">$t0 = 0                                        $t1 = 0</td>

   <td width="183">$t2 = 73</td>

   <td width="31"> </td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="244">$t4 = 1                                        $t5 = 0</td>

   <td width="183">$t6 = 0</td>

   <td width="31"> </td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td colspan="6" width="626">CPU Cycles ===&gt;                 1        2        3        4        5        6        7        8        9                                   10 11 12 13 14 15 16</td>

  </tr>

  <tr>

   <td colspan="2" width="458">ori $s1,$zero,451                         IF ID EX MEM WB .                .         .         .         .</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td colspan="2" width="458">addi $t2,$t2,73                      .                IF ID EX MEM WB .                .         .         .</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td colspan="2" width="458">slti $t4,$s1,453                      .         .                IF ID EX MEM WB .                .         .</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="244">addi $s1,$s1,1                        .         .         .</td>

   <td width="214">IF ID EX MEM WB .                        .</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="244">bne $t4,$zero,loop .                     .         .</td>

   <td width="214">.                 IF ID EX MEM WB .</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="244">ori $s6,$t6,77                         .         .         .</td>

   <td width="214">.         .                IF ID EX *               .</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="244">add $s7,$s0,$s0                    .         .         .</td>

   <td width="214">.         .         .             IF ID *             .</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="244">andi $s2,$t5,255                   .         .         .</td>

   <td width="214">.         .         .         .           IF *           .</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="244">addi $t2,$t2,73                      .         .         .</td>

   <td width="214">.         .         .         .         .            IF .</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="15">.</td>

  </tr>

  <tr>

   <td width="244">$s0 = 0                                        $s1 = 452</td>

   <td width="214">$s2 = 0</td>

   <td width="92">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="244">$s4 = 0                                       $s5 = 0</td>

   <td width="214">$s6 = 0</td>

   <td width="92">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="244">$t0 = 0                                        $t1 = 0</td>

   <td width="214">$t2 = 73</td>

   <td width="92">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

  <tr>

   <td width="244">$t4 = 1                                        $t5 = 0</td>

   <td width="214">$t6 = 0</td>

   <td width="92">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="15"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="153"> </td>

   <td width="92"> </td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92"> </td>

   <td width="153">..         .</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="8"> </td>

  </tr>

  <tr>

   <td width="153">addi $t2,$t2,73</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="153">IF ID .                    .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="153">slti $t4,$s1,453</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="153">.            IF .           .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="92">$s1 = 452</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s2 = 0</td>

   <td width="153">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="8"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="92">$s5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s6 = 0</td>

   <td width="153">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="8"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="92">$t1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t2 = 73</td>

   <td width="153">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="8"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 1</td>

   <td width="92">$t5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t6 = 0</td>

   <td width="153">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="8"> </td>

  </tr>

  <tr>

   <td width="153">$t8 = 0</td>

   <td width="92">$t9 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92"> </td>

   <td width="153"> </td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="8"> </td>

  </tr>

 </tbody>

</table>

———————————————————————————-

CPU Cycles ===&gt;                  1        2        3        4        5        6        7        8        9                                   10 11 12 13 14 15 16

<table width="0">

 <tbody>

  <tr>

   <td colspan="5" width="519">ori $s1,$zero,451                         IF ID EX MEM WB .                .         .         .         .         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td colspan="5" width="519">addi $t2,$t2,73                      .                IF ID EX MEM WB .                .         .         .         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td colspan="5" width="519">slti $t4,$s1,453                      .         .                IF ID EX MEM WB .                .         .         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td colspan="2" width="244">addi $s1,$s1,1                        .         .         .</td>

   <td colspan="3" width="275">IF ID EX MEM WB .                        .         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td colspan="2" width="244">bne $t4,$zero,loop .                     .         .</td>

   <td width="31">.</td>

   <td colspan="2" width="244">IF ID EX MEM WB .                        .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="153">ori $s6,$t6,77</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="214">IF ID EX *                      *        .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="153">add $s7,$s0,$s0</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="214">.              IF ID *             *        *        .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="153">andi $s2,$t5,255</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="214">.         .           IF *          *        *        .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="153">addi $t2,$t2,73</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="214">.         .         .                IF ID EX .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="153">slti $t4,$s1,453</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="214">.         .         .         .              IF ID .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="153">addi $s1,$s1,1</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="214">.         .         .         .         .            IF .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="153">$s0 = 0</td>

   <td width="92">$s1 = 452</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td colspan="2" width="244">$s2 = 0                                       $s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="8"> </td>

  </tr>

  <tr>

   <td width="153">$s4 = 0</td>

   <td width="92">$s5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td colspan="2" width="244">$s6 = 0                                       $s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="8"> </td>

  </tr>

  <tr>

   <td width="153">$t0 = 0</td>

   <td width="92">$t1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td colspan="2" width="244">$t2 = 73                                     $t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="8"> </td>

  </tr>

  <tr>

   <td width="153">$t4 = 1</td>

   <td width="92">$t5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td colspan="2" width="244">$t6 = 0                                        $t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="8"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-




$t8 = 0                                        $t9 = 0

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="244">addi $t2,$t2,73                      .         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td colspan="2" width="153">IF ID EX MEM .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="244">slti $t4,$s1,453                      .         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="122">IF ID EX .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="244">addi $s1,$s1,1                        .         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="122">.               IF ID .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="244">bne $t4,$zero,loop .                     .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="122">.         .            IF .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="244">$s0 = 0                                        $s1 = 452</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s2 = 0</td>

   <td width="31"> </td>

   <td width="122">$s3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="8"> </td>

  </tr>

  <tr>

   <td width="244">$s4 = 0                                       $s5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s6 = 0</td>

   <td width="31"> </td>

   <td width="122">$s7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="8"> </td>

  </tr>

  <tr>

   <td width="244">$t0 = 0                                        $t1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t2 = 73</td>

   <td width="31"> </td>

   <td width="122">$t3 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="8"> </td>

  </tr>

  <tr>

   <td width="244">$t4 = 1                                        $t5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t6 = 0</td>

   <td width="31"> </td>

   <td width="122">$t7 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="8"> </td>

  </tr>

 </tbody>

</table>

CPU Cycles ===&gt;                  1        2        3        4        5        6        7        8        9                                   10 11 12 13 14 15 16

<table width="0">

 <tbody>

  <tr>

   <td colspan="5" width="580">ori $s1,$zero,451                         IF ID EX MEM WB .                .         .         .         .         .         .         .         .</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="183">addi $t2,$t2,73                      .</td>

   <td colspan="4" width="397">IF ID EX MEM WB .                        .         .         .         .         .         .         .</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="183">slti $t4,$s1,453                      .</td>

   <td colspan="4" width="397">.                 IF ID EX MEM WB .                .         .         .         .         .         .</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="183">addi $s1,$s1,1                        .</td>

   <td width="61">.         .</td>

   <td colspan="3" width="336">IF ID EX MEM WB .                        .         .         .         .         .</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="183">bne $t4,$zero,loop .</td>

   <td width="61">.         .</td>

   <td width="31">.</td>

   <td colspan="2" width="305">IF ID EX MEM WB .                        .         .         .         .</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="183">ori $s6,$t6,77                         .</td>

   <td width="61">.         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="275">IF ID EX *                      *        .         .         .         .</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="183">add $s7,$s0,$s0                    .</td>

   <td width="61">.         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="275">.              IF ID *             *        *        .         .         .</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="183">andi $s2,$t5,255                   .</td>

   <td width="61">.         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="275">.         .           IF *          *        *       *        .         .</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="183">addi $t2,$t2,73                      .</td>

   <td width="61">.         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="275">.         .         .                IF ID EX MEM WB .</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="183">slti $t4,$s1,453                      .</td>

   <td width="61">.         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="275">.         .         .         .               IF ID EX MEM .</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="183">addi $s1,$s1,1                        .</td>

   <td width="61">.         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="275">.         .         .         .         .                IF ID EX .</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="183">bne $t4,$zero,loop .</td>

   <td width="61">.         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="275">.         .         .         .         .         .              IF ID .</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="183">ori $s6,$t6,77                         .</td>

   <td width="61">.         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="275">.         .         .         .         .         .         .            IF .</td>

   <td width="31">.</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td colspan="2" width="244">$s0 = 0                                        $s1 = 452</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="275">$s2 = 0                                       $s3 = 0</td>

   <td width="31"> </td>

   <td width="8"> </td>

  </tr>

  <tr>

   <td colspan="2" width="244">$s4 = 0                                       $s5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="275">$s6 = 0                                       $s7 = 0</td>

   <td width="31"> </td>

   <td width="8"> </td>

  </tr>

  <tr>

   <td colspan="2" width="244">$t0 = 0                                        $t1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="275">$t2 = 146                                   $t3 = 0</td>

   <td width="31"> </td>

   <td width="8"> </td>

  </tr>

  <tr>

   <td colspan="2" width="244">$t4 = 1                                        $t5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="275">$t6 = 0                                        $t7 = 0</td>

   <td width="31"> </td>

   <td width="8"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="244">addi $t2,$t2,73                      .         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td colspan="3" width="214">IF ID EX MEM WB .                        .</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="244">slti $t4,$s1,453                      .         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td colspan="2" width="183">IF ID EX MEM WB .</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="244">addi $s1,$s1,1                        .         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="153">IF ID EX MEM .</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="244">bne $t4,$zero,loop .                     .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="153">.                 IF ID EX .</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="244">ori $s6,$t6,77                         .         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="153">.         .              IF ID .</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="244">add $s7,$s0,$s0                    .         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="153">.         .         .            IF .</td>

   <td width="8">.</td>

  </tr>

  <tr>

   <td width="244">$s0 = 0                                        $s1 = 452</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="153">$s3 = 0</td>

   <td width="8"> </td>

  </tr>

  <tr>

   <td width="244">$s4 = 0                                       $s5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="153">$s7 = 0</td>

   <td width="8"> </td>

  </tr>

  <tr>

   <td width="244">$t0 = 0                                        $t1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t2 = 146</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="153">$t3 = 0</td>

   <td width="8"> </td>

  </tr>

  <tr>

   <td width="244">$t4 = 1                                        $t5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="153">$t7 = 0</td>

   <td width="8"> </td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

CPU Cycles ===&gt;                  1        2        3        4        5        6        7        8        9                                   10 11 12 13 14 15 16

<table width="0">

 <tbody>

  <tr>

   <td colspan="6" width="619">ori $s1,$zero,451                         IF ID EX MEM WB .                .         .         .         .         .         .         .         .         .          .</td>

  </tr>

  <tr>

   <td width="183">addi $t2,$t2,73                      .</td>

   <td colspan="5" width="435">IF ID EX MEM WB .                        .         .         .         .         .         .         .         .         .</td>

  </tr>

  <tr>

   <td width="183">slti $t4,$s1,453                      .</td>

   <td width="31">.</td>

   <td colspan="4" width="405">IF ID EX MEM WB .                        .         .         .         .         .         .         .          .</td>

  </tr>

  <tr>

   <td width="183">addi $s1,$s1,1                        .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td colspan="3" width="374">IF ID EX MEM WB .                        .         .         .         .         .         .         .</td>

  </tr>

  <tr>

   <td width="183">bne $t4,$zero,loop .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td colspan="2" width="344">IF ID EX MEM WB .                        .         .         .         .         .          .</td>

  </tr>

  <tr>

   <td width="183">ori $s6,$t6,77                         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="313">IF ID EX *                      *        .         .         .         .         .         .</td>

  </tr>

  <tr>

   <td width="183">add $s7,$s0,$s0                    .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="313">.              IF ID *             *        *        .         .         .         .         .</td>

  </tr>

  <tr>

   <td width="183">andi $s2,$t5,255                   .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="313">.         .           IF *          *        *       *        .         .         .         .</td>

  </tr>

  <tr>

   <td width="183">addi $t2,$t2,73                      .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="313">.         .         .                IF ID EX MEM WB .                .         .</td>

  </tr>

  <tr>

   <td width="183">slti $t4,$s1,453                      .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="313">.         .         .         .                IF ID EX MEM WB .                 .</td>

  </tr>

  <tr>

   <td width="183">addi $s1,$s1,1                        .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="313">.         .         .         .         .                        IF ID EX MEM WB .</td>

  </tr>

  <tr>

   <td width="183">bne $t4,$zero,loop .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="313">.         .         .         .         .         .                      IF ID EX MEM .</td>

  </tr>

  <tr>

   <td width="183">ori $s6,$t6,77                         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="313">.         .         .         .         .         .         .                        IF ID EX .</td>

  </tr>

  <tr>

   <td width="183">add $s7,$s0,$s0                    .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="313">.         .         .         .         .         .         .         .                    IF ID .</td>

  </tr>

  <tr>

   <td width="183">andi $s2,$t5,255                   .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="313">.         .         .         .         .         .         .         .         .               IF .</td>

  </tr>

  <tr>

   <td colspan="3" width="244">$s0 = 0                                        $s1 = 453</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="313">$s2 = 0                                       $s3 = 0</td>

  </tr>

  <tr>

   <td colspan="3" width="244">$s4 = 0                                       $s5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="313">$s6 = 0                                       $s7 = 0</td>

  </tr>

  <tr>

   <td colspan="3" width="244">$t0 = 0                                        $t1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="313">$t2 = 146                                   $t3 = 0</td>

  </tr>

  <tr>

   <td colspan="3" width="244">$t4 = 1                                        $t5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="313">$t6 = 0                                        $t7 = 0</td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

<table width="0">

 <tbody>

  <tr>

   <td width="244">addi $t2,$t2,73                      .         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td colspan="3" width="229">IF ID EX MEM WB .                        .            .</td>

  </tr>

  <tr>

   <td width="244">slti $t4,$s1,453                      .         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td colspan="2" width="199">IF ID EX MEM WB .                            .</td>

  </tr>

  <tr>

   <td width="244">addi $s1,$s1,1                        .         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="168">IF ID EX MEM WB .</td>

  </tr>

  <tr>

   <td width="244">bne $t4,$zero,loop .                     .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="168">.                    IF ID EX MEM WB</td>

  </tr>

  <tr>

   <td width="244">ori $s6,$t6,77                         .         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="168">.         .                         IF ID EX *</td>

  </tr>

  <tr>

   <td width="244">add $s7,$s0,$s0                    .         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="168">.         .         .                     IF ID *</td>

  </tr>

  <tr>

   <td width="244">andi $s2,$t5,255                   .         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="168">.         .         .         .                IF *</td>

  </tr>

  <tr>

   <td width="244">addi $t2,$t2,73                      .         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="92">.         .         .</td>

   <td width="31">.</td>

   <td width="31">.</td>

   <td width="168">.         .         .         .         .          IF</td>

  </tr>

  <tr>

   <td width="244">$s0 = 0                                        $s1 = 453</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s2 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="168">$s3 = 0</td>

  </tr>

  <tr>

   <td width="244">$s4 = 0                                       $s5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$s6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="168">$s7 = 0</td>

  </tr>

  <tr>

   <td width="244">$t0 = 0                                        $t1 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t2 = 146</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="168">$t3 = 0</td>

  </tr>

  <tr>

   <td width="244">$t4 = 1                                        $t5 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="92">$t6 = 0</td>

   <td width="31"> </td>

   <td width="31"> </td>

   <td width="168">$t7 = 0</td>

  </tr>

 </tbody>

</table>

$t8 = 0                                        $t9 = 0

———————————————————————————-

END OF SIMULATION




<h1>Assumptions</h1>

Given the complexity of this assignment, you can make the following assumptions:

<ul>

 <li>Assume all input files are valid.</li>

 <li>Assume the length of argv[1] is exactly 1 character, but do not assume that argv[1] is present.</li>

 <li>Assume the length of argv[2] is at most 128 characters, but do not assume that argv[2] is present.</li>

</ul>

<h1>Error Checking</h1>

Be sure to verify that you have the correct number of arguments by checking the argument count (i.e., argc); display an error message if argument(s) are missing.

In general, if an error occurs, display the error to stderr. And be sure to return either EXIT_SUCCESS or EXIT_FAILURE (or their equivalents) upon program termination.


