<div align="center">
  <h1>🏫 National Institute of Technology Silchar</h1>
</div>

<CodeTabs :languages="[
    { name: '2023-Nov-Dec', slot: '2023-Nov-Dec' },
    {name : '2022-Dec', slot : '2022-Dec'},
    {name : '2019-NOV', slot : '2019-NOV'},
]">

<template #2019-NOV>

<details style="margin-bottom: 5px; margin-top : 10px; border: 1px solid #ccc; border-radius: 5px; padding: 8px;">
  <summary style="font-weight: bold; cursor: pointer; font-size: 1rem;">Click to view the Question Paper</summary>
  <div align="center" style="margin-top: 10px;">
    <img src="https://res.cloudinary.com/dywrfit3t/image/upload/v1763919208/Screenshot_23-Nov_23-03-08_19715_du9u02.png" 
         alt="Question Paper" 
         style="max-width: 90%; height: auto; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.2);" />
    <img src="https://res.cloudinary.com/dywrfit3t/image/upload/v1763919207/Screenshot_23-Nov_23-03-16_29751_rxd1hu.png" 
         alt="Question Paper" 
         style="max-width: 90%; height: auto; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.2);" />
</div>
</details>

</template>

<template #2023-Nov-Dec>

<details style="margin-bottom: 5px; margin-top : 10px; border: 1px solid #ccc; border-radius: 5px; padding: 8px;">
  <summary style="font-weight: bold; cursor: pointer; font-size: 1rem;">Click to view the Question Paper</summary>
  <div align="center" style="margin-top: 10px;">
    <img src="https://res.cloudinary.com/dzgoq3ikq/image/upload/v1760772080/Screenshot_18-Oct_12-50-59_24278_bb67sf.png" 
         alt="Question Paper" 
         style="max-width: 90%; height: auto; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.2);" />
</div>
</details>

<table>
<caption>Answer any 5 Questions</caption>
  <thead>
    <tr>
      <th>Q.N.</th>
      <th>Questions</th>
      <th>Marks</th>
      <th>CO</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1. (a)</td>
      <td>What are the advantages of instruction queue in <strong>8086</strong> as compared to <strong>8085</strong>?<br>
      What is the usage of <code>source index (SI)</code> and <code>destination index (DI)</code> in <strong>8086</strong>?</td>
      <td>3</td>
      <td>CO-3</td>
    </tr>
    <tr>
      <td>(b)</td>
      <td>How are the physical addresses are calculated in <strong>8086</strong>? Illustrate through example?</td>
      <td>2</td>
      <td>CO-3</td>
    </tr>
    <tr>
      <td>(c)</td>
      <td>List down <strong>8</strong> general purpose register, each of which is <strong>16 bits</strong> wide in <strong>8086</strong>. Which specific register is used for count application?</td>
      <td>3</td>
      <td>CO-3</td>
    </tr>
    <tr>
      <td>2. (a)</td>
      <td>Explain <code>DMA Master</code> and <code>Slave mode</code>.</td>
      <td>2</td>
      <td>CO-3</td>
    </tr>
    <tr>
      <td>(b)</td>
      <td>What is a interrupt in <strong>8085</strong>? List all the interrupts. Explain <code>SIM</code> and <code>RIM</code> instructions.</td>
      <td>1+1+3</td>
      <td>CO-3</td>
    </tr>
    <tr>
      <td>(c)</td>
      <td>Write a program assuming the microprocessor is completing an <code>RST 5.5</code> interrupt request, check to see if <code>RST 7.5</code> is pending. If it is pending, enable <code>RST 7.5</code> without affecting any other interrupts, otherwise, return to the main program.</td>
      <td>5</td>
      <td>CO-2</td>
    </tr>
    <tr>
      <td>3. (a)</td>
      <td>Calculate the total delay for the given set of instructions.<br>
      <code>LXI B,2384H</code> - 10 T-States<br>
      <code>LOOP: DCX B</code> - 6 T-States<br>
      <code>MOV A, C</code> - 4 T-States<br>
      <code>ORA B</code> - 4 T-States<br>
      <code>JNZ LOOP</code> - 10/7 T-States</td>
      <td>5</td>
      <td>CO-1</td>
    </tr>
    <tr>
      <td>(b)</td>
      <td>Calculate the total delay for the given set of instructions<br>
      <code>MVI B, 38H</code> - 7 T-States<br>
      <code>LOOP2: MVI C, FFH</code> - 7 T-States<br>
      <code>LOOP 1: DCR C</code> - 4 T-States<br>
      <code>JNZ LOOP 1</code> - 10/7 T-States<br>
      <code>DCR B</code> - 4 T-States<br>
      <code>JNZ LOOP 2</code> - 10/7 T-States</td>
      <td>5</td>
      <td>CO-1</td>
    </tr>
    <tr>
      <td>4.</td>
      <td>Write a program to count continuously the hexadecimal numbers from <code>FFH</code> to <code>00H</code> in a system with a <code>0.5μs</code> clock period. Use register <code>C</code> to set up one millisecond (ms) delay between each count and display the numbers at one of the output ports.</td>
      <td>10</td>
      <td>CO-1</td>
    </tr>
    <tr>
      <td>5.</td>
      <td>Write a <code>20ms</code> time delay subroutine using register pair <code>BC</code> Clear the <code>Z flag</code> without affecting any other flag register and return to the main program.</td>
      <td>10</td>
      <td>CO-1</td>
    </tr>
    <tr>
      <td colspan="4" style="text-align: center;"><strong>OR</strong></td>
    </tr>
    <tr>
      <td>6.</td>
      <td>A railway crossing signal has two flashing lights run by a microcomputer. One light is connected to data bit <code>D₇</code> and the second light is connected to data bit <code>D₆</code>. Write a program to turn each signal light alternatively on and off at an interval of <strong>1 second</strong>.<br><br>
      <code>Note: Flowchart and description of the instructions in programming questions is a must.</code></td>
      <td>10</td>
      <td>CO-1</td>
    </tr>
  </tbody>
</table>

</template>

<template #2022-Dec>

<details style="margin-bottom: 5px; margin-top : 10px; border: 1px solid #ccc; border-radius: 5px; padding: 8px;">
  <summary style="font-weight: bold; cursor: pointer; font-size: 1rem;">Click to view the Question Paper</summary>
  <div align="center" style="margin-top: 10px;">
    <img src="https://res.cloudinary.com/dzgoq3ikq/image/upload/v1760781145/Screenshot_18-Oct_15-22-06_116_kiwhzf.png" 
         alt="Question Paper" 
         style="max-width: 90%; height: auto; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.2);" />
    <img src="https://res.cloudinary.com/dzgoq3ikq/image/upload/v1760781170/Screenshot_18-Oct_15-22-33_31534_ve4wqe.png" 
         alt="Question Paper" 
         style="max-width: 90%; height: auto; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.2);" />

</div>
</details>

</template>

</CodeTabs>
