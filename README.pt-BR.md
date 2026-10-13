# Verilog Digital Circuits Lab

[English / README principal](README.md) · Português (Brasil)

Repositório de lógica digital no estilo de trabalhos acadêmicos, com módulos Verilog,
bancadas de teste e capturas de simulação. Ele permanece público como uma amostra
compacta de engenharia da computação, em vez de um sistema completo de produção.

## Captura de tela

<img align="center" height="480" src="Screenshot_3.png"/>

## Módulos

Somador completo de um bit (nível de portas)
```verilog
`timescale 1ns / 1ps
module simple_adder (
    input A, B, Cin,
    output Sum, Cout
);
    assign Sum = A ^ B ^ Cin;
    assign Cout = (A & B) | (Cin & (A ^ B));
endmodule

Four bit full adder (using one bit full adders)

`timescale 1ns / 1ps 
module adder (
    input [3:0] A, B,
    input Cin,
    output [3:0] Sum,
    output Cout
);
    wire carry1, carry2, carry3;

    simple_adder first (A[0], B[0], Cin, Sum[0], carry1);
    simple_adder second (A[1], B[1], carry1, Sum[1], carry2);
    simple_adder third (A[2], B[2], carry2, Sum[2], carry3);
    simple_adder fourth (A[3], B[3], carry3, Sum[3], Cout);
endmodule
```

### Bancadas de teste

Somador de quatro bits (`adder_tb.v`):

```verilog
`timescale 1ns / 1ps
module adder_tb;
    reg [3:0] A, B;
    reg Cin;
    wire [3:0] Sum;
    wire Cout;

    adder uut (
        .A(A),
        .B(B),
        .Cin(Cin),
        .Sum(Sum),
        .Cout(Cout)
    );

    initial begin
        A = 4'b0000; B = 4'b0000; Cin = 0;
        $monitor("Time = %0t | A = %b, B = %b, Cin = %b | Sum = %b, Cout = %b", $time, A, B, Cin, Sum, Cout);

        #10;
        A = 4'b0001; B = 4'b0010; Cin = 0;
        A = 4'b0110; B = 4'b0101; Cin = 1;

        #10;
        A = 4'b1111; B = 4'b1111; Cin = 1;
        #20;
        A = 4'b1111; B = 4'b1111; Cin = 1;
        #10;
        $finish;
    end
endmodule
```

## Captura da simulação

<img align="center" height="480" src="Screenshot_5.png"/>
