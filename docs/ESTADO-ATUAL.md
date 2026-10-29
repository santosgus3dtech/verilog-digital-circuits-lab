# Estado atual — Verilog Digital Circuits Lab

Revisão documental: 13/10/2026. Somente leitura de HDL e testbench.

## Arquitetura e regras observadas

`simple_adder.v` implementa somador de um bit por XOR e expressão de carry. `adder.v` encadeia quatro instâncias com carries intermediários para entradas A/B de quatro bits e Cin, saídas Sum/Cout. `adder_tb.v` aplica estímulos, usa `$monitor` e finaliza por `$finish`.

## Cobertura e lacunas

No testbench há duas atribuições consecutivas sem atraso entre os casos 1+2 e 6+5+carry; por leitura estática, não constituem duas janelas separadas de observação. Não foi identificada suíte exaustiva/autoverificação com assertions. O [README](../README.md) traz capturas e exemplos, sem registrar toolchain/comando de simulação reproduzível.

## Operação

Não há manifest ou comando explícito de simulador/síntese identificado no README. Não inventar um fluxo de FPGA a partir dos módulos. Testbench, simulação, testes e serviços não executados nesta tarefa; screenshots não foram usados como aprovação atual.

## Retomada

Sugestões: registrar simulador e comando realmente usados em tarefa futura; separar os estímulos temporalmente se houver pedido de melhoria; definir cobertura esperada para o laboratório. Nenhuma implementação HDL ou decisão de hardware foi alterada/aprovada aqui.

[Índice](INDEX.md)
