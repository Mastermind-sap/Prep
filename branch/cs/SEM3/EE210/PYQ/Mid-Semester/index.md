<div align="center">
  <h1>🏫 National Institute of Technology Silchar</h1>
</div>

<CodeTabs :languages="[
  { name: '2023-Oct', slot: '2023-Oct' },
  { name: '2019-SEP', slot: '2019-SEP' },
]">

<template #2019-SEP>

<details style="margin-bottom: 5px; margin-top : 10px; border: 1px solid #ccc; border-radius: 5px; padding: 8px;">
  <summary style="font-weight: bold; cursor: pointer; font-size: 1rem;">Click to view the Question Paper</summary>
  <div align="center" style="margin-top: 10px;">
    <img src="https://res.cloudinary.com/dywrfit3t/image/upload/v1763919328/Screenshot_23-Nov_23-05-09_16834_hmpzp3.png" 
         alt="Question Paper" 
         style="max-width: 90%; height: auto; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.2);" />
    <img src="https://res.cloudinary.com/dywrfit3t/image/upload/v1763919326/Screenshot_23-Nov_23-05-16_27483_mttgqa.png" 
         alt="Question Paper" 
         style="max-width: 90%; height: auto; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.2);" />

</div>
</details>

</template>

<template #2023-Oct>

<details style="margin-bottom: 5px; margin-top : 10px; border: 1px solid #ccc; border-radius: 5px; padding: 8px;">
  <summary style="font-weight: bold; cursor: pointer; font-size: 1rem;">Click to view the Question Paper</summary>
  <div align="center" style="margin-top: 10px;">
    <img src="https://res.cloudinary.com/dzgoq3ikq/image/upload/v1760768769/Screenshot_18-Oct_11-55-46_6112_lyplui.png" 
         alt="Question Paper" 
         style="max-width: 90%; height: auto; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.2);" />
    <img src="https://res.cloudinary.com/dzgoq3ikq/image/upload/v1760768794/Screenshot_18-Oct_11-56-14_4406_eapwzw.png" 
         alt="Question Paper" 
         style="max-width: 90%; height: auto; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.2);" />

</div>
</details>

<table style="width: 100%; border-collapse: collapse; border-color:none">
    <caption> Answer all Questions </caption>
  <thead>
    <tr>
      <th>Q. No.</th>
      <th>Questions</th>
      <th>Marks</th>
      <th>CO</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1.(a)</td>
      <td>The number of address pins in <strong>Intel 8085</strong> is <strong>16</strong> and in <strong>Intel 8086</strong> it is <strong>20</strong>. How many memory locations are they capable of <code>addressing?</code></td>
      <td>2</td>
      <td>CO3</td>
    </tr>
    <tr>
      <td>1.(b)</td>
      <td>Distinguish between the following pairs of instruction:<br>
      i. <code>LDA F900 H</code> and <code>LXI H, 1234H</code><br>
      ii. <code>ADD M</code> and <code>ADC M</code></td>
      <td>2</td>
      <td>CO3</td>
    </tr>
    <tr>
      <td>1.(c)</td>
      <td>Explain different types of <code>addressing modes</code> available in <strong>8085</strong> with an example for each.</td>
      <td>2</td>
      <td>CO3</td>
    </tr>
    <tr>
      <td>2.(a)</td>
      <td>Identify the value of '<strong>x</strong>', '<strong>y</strong>', '<strong>p</strong>', and '<strong>q</strong>', for absolute decoding of the memory chip of <strong>8 KB</strong> as shown in Fig. (i). <br> <strong>A<sub>x</sub></strong> to <strong>A<sub>y</sub></strong> represents range for address used as an input to decoder. <strong>A<sub>p</sub></strong> to <strong>A<sub>q</sub></strong> represents range for address line used for chip select for absolute decoding. Chip select (<strong>CS</strong>) is an active low signal.<br><br> <div align = "center"> <img src = "https://res.cloudinary.com/dzgoq3ikq/image/upload/v1760769203/Screenshot_18-Oct_12-03-04_8216_b7ejuc.png"> </img> </div><br>Address line <strong>A<sub>q</sub></strong> has only bubble at the input of NAND gate.</td>
      <td>6</td>
      <td>CO3</td>
    </tr>
    <tr>
      <td>2.(b)</td>
      <td>Suppose the machine codes <strong>(3EH)</strong> and <strong>(42H)</strong> for the instruction <code>MVI A, 42H</code> are stored in <em>memory</em> locations <strong>4000H</strong> and <strong>4001H</strong> respectively. <br> Draw the <code>timing diagram</code> for executing the instruction. If the processor is having <strong>5 MHz</strong> clock frequency, how much time will be needed to execute the instruction?</td>
      <td>6</td>
      <td>CO3</td>
    </tr>
    <tr>
      <td>3.(a)</td>
      <td>The contents of memory locations <strong>2400H</strong>, <strong>2401H</strong>, <strong>2402H</strong> and <strong>2403H</strong> are <strong>00</strong>, <strong>FFH</strong>, <strong>0FH</strong> and <strong>1AH</strong> respectively. What will be the memory contents after the following instructions are executed?<br>
      <code>LHLD 2402H</code><br>
      <code>LDA 2400H</code><br>
      <code>MOV B, L</code><br>
      <code>MOV C, H</code><br>
      <code>MVI D, 03</code><br>
      <code>MOV E, A</code><br>
      <code>SHLD 2400H</code><br>
      <code>STA 2402H</code></td>
      <td>4</td>
      <td>CO1</td>
    </tr>
    <tr>
      <td>3.(b)</td>
      <td>A set of <strong>16</strong> current readings is stored in memory locations starting at <strong>2000H</strong>. The readings are expected to be negative. <br> Write a program to<br>
      (i) <strong>Check each reading to determine whether the number is positive or negative.</strong><br>
      (ii) <strong>Reject all the positive readings.</strong><br>
      (iii) <strong>Add all the negative readings.</strong><br>
      (iv) Output <strong>01H</strong> to <strong>PORT1</strong> when there is an overload/sum exceeds <strong>FFH</strong>; otherwise display the sum at <strong>PORT1</strong>.</td>
      <td>5</td>
      <td>CO1</td>
    </tr>
    <tr>
      <td>3.(c)</td>
      <td>A set of eight readings is stored in memory starting at location <strong>2050H</strong>. <br> Write a program to check whether a byte <strong>40H</strong> exists in the set. If it does, stop checking and display <strong>01H</strong>; otherwise display <strong>FFH</strong>.<br>
      <code>Data (H) <strong>48, 32, F2, 38, 37, 40, 82, 8A</strong></code>.</td>
      <td>3</td>
      <td>CO1</td>
    </tr>
  </tbody>
</table>

</template>

</CodeTabs>
