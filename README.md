Download Link: https://assignmentchef.com/product/solved-cda41025155-project-1-simple-mips-simulator
<br>
In this project you will create a simple MIPS simulator which will perform the following two tasks. <strong>Please develop your project in ONLY one </strong>(C, C++, Java or Python) <strong>source file</strong> to avoid the stress of combining multiple files before submission and making sure it still works correctly.

<ul>

 <li>Load a specified MIPS text file<sup>1</sup> and generate the assembly code equivalent to the input file (<strong>disassembler</strong>). Please see the sample input file and disassembly output in the project assignment.</li>

 <li>Generate the instruction-by-instruction simulation of the MIPS code (<strong>simulator</strong>). It should also produce/print the contents of <em>registers</em> and <em>data memories</em> after execution of each instruction. Please see the sample simulation output file in the project assignment.</li>

</ul>

Since this is a functional simulation project, you do not have to worry about MIPS pipeline. Moreover,<strong> you do not have to implement any exception or interrupt handling for this project. </strong>We will use only valid testcases that will not create any exceptions. Please go through this document first, and then view the sample input/output files in the project assignment, before you start implementing the project.




<h1>Instructions</h1>




For reference, please use the MIPS Instruction Set Architecture PDF (available from the project1 assignment) to see the format for each instruction <strong>and pay attention to the following changes.</strong><strong>  </strong>

Your disassembler &amp; simulator need to support the three categories of instructions shown in <strong>Figure 1.</strong>

<table width="658">

 <tbody>

  <tr>

   <td width="244"><strong>Category-1 </strong></td>

   <td width="246"><strong>Category-2 </strong></td>

   <td width="168"><strong>Category-3 </strong></td>

  </tr>

  <tr>

   <td width="244">J, BEQ, BNE, BGTZ, SW, LW, BREAK</td>

   <td width="246">ADD, SUB, AND, OR, SRL, SRA,MUL</td>

   <td width="168">ADDI, ANDI, ORI</td>

  </tr>

 </tbody>

</table>

<h2>Figure 1: Three categories of instructions</h2>

The format of <strong>Category-1</strong> instructions is described in <strong>Figure 2</strong>. If the instruction belongs to <strong>Category-1</strong>, the first three bits (leftmost bits) are always “<strong>000</strong>” followed by <strong>3 bits </strong>Opcode. Please note that instead of using 6 bits opcode in MIPS, we use 3 bits opcode as described in<strong> Figure 3</strong>. The remaining part of the instruction binary is exactly the same as the original MIPS instruction set for that specific instruction.

<table width="624">

 <tbody>

  <tr>

   <td width="60">000</td>

   <td width="132">Opcode (3 bits)</td>

   <td width="432">Same as MIPS instruction</td>

  </tr>

 </tbody>

</table>

<h2>Figure 2: Format of Instructions in Category-1</h2>

Please pay attention to the exact description of instruction formats and its interpretation in MIPS instruction set manual. <em>For example, in case of <strong>J </strong>instruction, the 26 bit instruction_index is shifted left </em>




<sup>1</sup> This is a text file consisting of 0/1’s (not a binary file). See the sample input file sample.txt in the project1 assignment.

<em>by two bits (padded with 00 at LSB side) and then the leftmost (MSB side) four bits of the delay slot instruction are used to form the four bits (MSB side) of the target address. Since we do not use delay slot in this project, treat the address of the next instruction as the address of the delay slot instruction. Similarly, for <strong>BEQ</strong>, <strong>BNE</strong> and <strong>BGTZ</strong> instructions, the 16 bit offset is shifted left by two bits to form 18 bit signed offset that is added with the address of the next instruction to form the target address. </em><strong>Please note that we do not consider </strong><em>delay slot</em><strong> for this project</strong><em>. In other words, an instruction following the branch instruction should be treated as a regular instruction (see sample_simulation.txt). </em>

<strong> </strong>

<table width="336">

 <tbody>

  <tr>

   <td width="178"><strong>Instruction </strong></td>

   <td width="158"><strong>Opcode </strong></td>

  </tr>

  <tr>

   <td width="178">J</td>

   <td width="158">000</td>

  </tr>

  <tr>

   <td width="178">BEQ</td>

   <td width="158">001</td>

  </tr>

  <tr>

   <td width="178">BNE</td>

   <td width="158">010</td>

  </tr>

  <tr>

   <td width="178">BGTZ</td>

   <td width="158">011</td>

  </tr>

  <tr>

   <td width="178">SW</td>

   <td width="158">100</td>

  </tr>

  <tr>

   <td width="178">LW</td>

   <td width="158">101</td>

  </tr>

  <tr>

   <td width="178">BREAK</td>

   <td width="158">110</td>

  </tr>

 </tbody>

</table>

<h2>Figure 3: Opcode for Category-1 instructions</h2>

If the instruction belongs to <strong>Category-2 </strong>which has the form “dest ← src1 op src2”, the first three bits

(leftmost three bits) are always “001” as shown in <strong>Figure 4</strong>, followed by 3 bits opcode as indicated in <strong>Figure 5</strong>. Then the following 5 bits serve as dest. The next 5 bits for src 1, followed by 5 bits for src2. The src1 is always register but src2 can be register (ADD, SUB, AND, OR, MUL) or immediate (SRL, SRA) depending on the opcode. The remaining bits are all 0’s.







<table width="637">

 <tbody>

  <tr>

   <td width="42">001</td>

   <td width="115">opcode (3 bits)</td>

   <td width="126">dest (5 bits)</td>

   <td width="120">src1 (5 bits)</td>

   <td width="108">src2 (5 bits)</td>

   <td width="126">00000000000</td>

  </tr>

 </tbody>

</table>

<h2>Figure 4: Format of  Category-2 instructions where both sources are registers</h2>




<table width="336">

 <tbody>

  <tr>

   <td width="178"><strong>Instruction </strong></td>

   <td width="158"><strong>Opcode </strong></td>

  </tr>

  <tr>

   <td width="178">ADD</td>

   <td width="158">000</td>

  </tr>

  <tr>

   <td width="178">SUB</td>

   <td width="158">001</td>

  </tr>

  <tr>

   <td width="178">AND</td>

   <td width="158">010</td>

  </tr>

  <tr>

   <td width="178">OR</td>

   <td width="158">011</td>

  </tr>

  <tr>

   <td width="178"> SRL</td>

   <td width="158">100</td>

  </tr>

  <tr>

   <td width="178">SRA</td>

   <td width="158">101</td>

  </tr>

  <tr>

   <td width="178">MUL</td>

   <td width="158">110</td>

  </tr>

 </tbody>

</table>

<h2>Figure 5: Opcode for Category-2 instructions</h2>

If the instruction belongs to <strong>Category-3 </strong>which has the form “dest ← src1 op immediate_value”, the first three bits (leftmost three bits) are always “010”. Then 3 bits for opcode as indicated in <strong>Figure 6</strong>. The subsequent 5 bits serve as dest followed by 5 bits for src1. The second source operand is immediate 16-bit value. The instruction format is shown in <strong>Figure 7</strong>.







<table width="336">

 <tbody>

  <tr>

   <td width="178"><strong>Instruction </strong></td>

   <td width="158"><strong>Opcode </strong></td>

  </tr>

  <tr>

   <td width="178">ADDI</td>

   <td width="158">000</td>

  </tr>

  <tr>

   <td width="178">ANDI</td>

   <td width="158">001</td>

  </tr>

  <tr>

   <td width="178">ORI</td>

   <td width="158">010</td>

  </tr>

 </tbody>

</table>

<h2>Figure 6: Opcode for Category-3 instructions</h2>




<table width="667">

 <tbody>

  <tr>

   <td width="42">010</td>

   <td width="139">opcode (3 bits)</td>

   <td width="150">dest (5 bits)</td>

   <td width="145">src1 (5 bits)</td>

   <td width="191">immediate_value (16 bits)</td>

  </tr>

 </tbody>

</table>

<h2>Figure 7: Format of  Category-3 instructions with source2 as immediate value</h2>




Once you look at the sample_disassembly.txt in the project assignment, it may be confusing for you to see that the last 16 bits of the following binary (offset) has the value of 9 but the assembly shows it as 36. This is a convention issue with MIPS. The binary always shows the actual offset (9 in this case) value. However, the assembly always shows the value shifted by 2 bits to the left (i.e., multiplied by 4).




0000010000100010   0000000000001001           276      BEQ R1, R2, #36




Please note there are also convention related confusion for other instructions. For example, in many binary format, the destination is the middle operand, whereas the destination always shows up as the leftmost operand in assembly instructions &lt;opcode, dest, src1, src2&gt;.







<h1>Sample Input/output Files</h1>




Your program will be given a text input file (see sample.txt). This file will contain a sequence of 32-bit instruction words starting at address <strong>“260”</strong>. The final instruction in the sequence of instructions is always BREAK. There will be only one BREAK instruction. Following the BREAK instruction (immediately after BREAK), there is a sequence of 32-bit 2’s complement signed integers for the program data up to the end of the file. The newline character can be either “
” (linux) or “r
” (windows). Your code should work for both cases. <strong><em>Please download the sample input/output files </em></strong>

<strong><em>using “Save As” instead of using copy/paste of the content.</em> </strong>




Your MIPS simulator (with executable name as <strong>MIPSsim</strong>) should accept an input file (<strong>inputfilename.txt</strong>) in the following command format and produce two output files in the same directory: <strong>disassembly.txt</strong> (contains disassembled output) and <strong>simulation.txt (</strong>contains the simulation trace). Please hardcode the names of the output files. <strong><em>Please do not hardcode the input filename</em></strong><em>. It will be specified when running your program. For example, it can be “sample.txt” or “test.txt”</em>.

MIPSsim inputfilename.txt




Correct handling of the sample input file (with possible different data values) will be used to determine 60% of the credit. The remaining 40% will be determined from other valid test cases that you will not have access prior to grading. It is recommended that you construct your own sample input files with which to further test your disassembler/simulator.

The disassembler output file should contain 3 columns of data with each column separated by one tab character (‘t’ or char(9)). See the sample disassembly file in the project1 assignment.

<ol>

 <li>The text (e.g., 0’s and 1’s) string representing the 32-bit data word at that location.</li>

 <li>The address (in decimal) of that location</li>

 <li>The disassembled instruction.</li>

</ol>

Note, if you are displaying an instruction, the third column should contain every part of the instruction, with each argument separated by a comma and then a space (“, ”).




The simulation output file should have the following format.

20 hyphens and a new line

Cycle  &lt; cycleNumber &gt;:&lt; tab &gt;&lt; instr_Address &gt;&lt; tab &gt;&lt; instr_string &gt;

&lt; blank_line &gt;

Registers

R00: &lt; tab &gt;&lt; int(R0) &gt;&lt; tab &gt;&lt; int(R1) &gt;…&lt; tab &gt;&lt; int(R7) &gt;

R08: &lt; tab &gt;&lt; int(R8) &gt;&lt; tab &gt;&lt; int(R9) &gt;…&lt; tab &gt;&lt; int(R15) &gt;

R16: &lt; tab &gt;&lt; int(R16) &gt;&lt; tab &gt;&lt; int(R17) &gt;…&lt; tab &gt;&lt; int(R23) &gt;

R24: &lt; tab &gt;&lt; int(R24) &gt;&lt; tab &gt;&lt; int(R25) &gt;…&lt; tab &gt;&lt; int(R31) &gt;

&lt; blank_line &gt;

Data

&lt; firstDataAddress &gt;: &lt; tab &gt;&lt; display 8 data words as integers with tabs in between &gt; ….. &lt; continue until the last data word &gt;




The instructions and instruction arguments should be in capital letters. Display all integer values in decimal. Immediate values should be preceded by a “#” symbol. <strong>Note that some instructions take signed immediate values while others take unsigned immediate values</strong>. You will have to make sure you properly display a signed or unsigned value depending on the context.

Because we will be using “<strong>diff –w -B</strong>” to check your output versus the expected outputs, please follow the output formatting. Mismatches will be treated as wrong output and will lead to score penalty.




The      project             assignment      contains           the       following         sample             programs/files to         test       your disassembler/simulator.

<ul>

 <li><u>txt</u> : This is the input to your program.</li>

 <li><u>txt</u> : This is what your program should produce as disassembled output.</li>

 <li><u>txt</u> : This is what your program should output as simulation trace.</li>

</ul>