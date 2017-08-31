<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1. Corewar Champion</a>
<ul>
<li><a href="#sec-1-1">1.1. goal of the project</a></li>
<li><a href="#sec-1-2">1.2. opcode set</a></li>
<li><a href="#sec-1-3">1.3. grade</a></li>
</ul>
</li>
</ul>
</div>
</div>

# Corewar Champion<a id="sec-1" name="sec-1"></a>

## goal of the project<a id="sec-1-1" name="sec-1-1"></a>

make a corewar assembly program that will beat other programs

## opcode set<a id="sec-1-2" name="sec-1-2"></a>

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="left" />

<col  class="right" />

<col  class="left" />
</colgroup>
<tbody>
<tr>
<td class="left">mnemonic</td>
<td class="right">hex</td>
<td class="left">effects</td>
</tr>


<tr>
<td class="left">-</td>
<td class="right">-</td>
<td class="left">-</td>
</tr>


<tr>
<td class="left">live</td>
<td class="right">0x01</td>
<td class="left">Followed by 4 bytes representing the player name. This instruction indicates that the player is alive. (No parameter encoding byte).</td>
</tr>


<tr>
<td class="left">ld</td>
<td class="right">0x02</td>
<td class="left">This instruction takes 2 parameters, the 2nd of which has to be a register (not the PC) It loads the value of the first parameter in the register. This operation modifies the carry. ld 34,r3 loads the REG&#95;SIZE bytes from address (PC + (34 % IDX&#95;MOD)) in register r3</td>
</tr>


<tr>
<td class="left">st</td>
<td class="right">0x03</td>
<td class="left">This instruction takes 2 parameters. It stores (REG&#95;SIZE bytes) the value of the first argument (always a register) in the second. st r4,34 stores the value of r4 at the address (PC + (34 % IDX&#95;MOD)) st r3,r8 copies r3 in r8</td>
</tr>


<tr>
<td class="left">add</td>
<td class="right">0x04</td>
<td class="left">This instruction takes 3 registers as parameter, adds the contents of the 2 first and stores the result in the third. This operation modifies the carry. add r2,r3,r5 adds r2 and r3 and stores the result in r5</td>
</tr>


<tr>
<td class="left">sub</td>
<td class="right">0x05</td>
<td class="left">Same effect as add, but with a substraction</td>
</tr>


<tr>
<td class="left">and</td>
<td class="right">0x06</td>
<td class="left">p1 & p2 -> p3, the parameter 3 is always a register This operation modifies the carry. and r2, %0,r3 stores r2 & 0 in r3.</td>
</tr>


<tr>
<td class="left">or</td>
<td class="right">0x07</td>
<td class="left">Same as and but with an or (&vert; in C)</td>
</tr>


<tr>
<td class="left">xor</td>
<td class="right">0x08</td>
<td class="left">Same as and but with an xor (&#94; in C)</td>
</tr>


<tr>
<td class="left">zjmp</td>
<td class="right">0x09</td>
<td class="left">This instruction is not followed by any parameter encoding byte. It always takes an index (IND&#95;SIZE) and makes a jump at this index if the carry is set to 1. If the carry is null, zjmp does nothing but consumes the same amount of time. zjmp %23 does : If carry == 1, store (PC + (23 % IDX&#95;MOD)) in the PC.</td>
</tr>


<tr>
<td class="left">ldi</td>
<td class="right">0x0a</td>
<td class="left">This operation modifies the carry. ldi 3,%4,r1 reads IND&#95;SIZE bytes at address: (PC + (3 % IDX&#95;MOD)), adds 4 to this value. We will name this sum S. Read REG&#95;SIZE bytes at address (PC + (S % IDX&#95;MOD)), which are copied to r1. Parameters 1 and 2 are indexes.</td>
</tr>


<tr>
<td class="left">sti</td>
<td class="right">0x0b</td>
<td class="left">sti r2,%4,%5 sti copies REG&#95;SIZE bytes of r2 at address (4 + 5) Parameters 2 and 3 are indexes. If they are, in fact, registers, we’ll use their contents as indexes.</td>
</tr>


<tr>
<td class="left">fork</td>
<td class="right">0x0c</td>
<td class="left">This instruction is not followed by a parameter encoding byte. It always takes an index and creates a new program, which is executed from address : (PC + (first parameter % IDX&#95;MOD)). Fork %34 creates a new program. The new program inherits all of its father’s states.</td>
</tr>


<tr>
<td class="left">lld</td>
<td class="right">0x0d</td>
<td class="left">Same as ld, but without the % IDX&#95;MOD This operation modifies the carry.</td>
</tr>


<tr>
<td class="left">lldi</td>
<td class="right">0x0d</td>
<td class="left">Same as ldi, without the % IDX&#95;MOD This operation modifies the carry.</td>
</tr>


<tr>
<td class="left">lfork</td>
<td class="right">0x0f</td>
<td class="left">Same as fork, without the % IDX&#95;MOD This operation modifies the carry</td>
</tr>


<tr>
<td class="left">aff</td>
<td class="right">0x10</td>
<td class="left">This instruction is followed by a parameter encoding byte. It takes a register and displays the character the ASCII code of which is contained in the register. (a modulo 256 is applied to this ascii code, the character is displayed on the standard output) Ex: ld %52,r3 aff r3 Displays ’\*’ on the standard output.</td>
</tr>
</tbody>
</table>

## grade<a id="sec-1-3" name="sec-1-3"></a>

125/100
