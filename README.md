# Hardware Projects

Three digital design projects with full testbenches and simulation.

---

## Projects

1. **Quantized-Stream NPU** - 4×4 INT8 matrix accelerator with quantization
2. **riscv32-harvard-pipeline** - 5-stage RV32I processor with forwarding
3. **VGA Image Stream with Ping-Pong FIFO buffers** - Video streaming to VGA

Each project has its own README with details.

---

## Prerequisites

```
choco install icarus-verilog  # Windows
brew install icarus-verilog   # macOS
sudo apt install iverilog     # Linux
```

GTKwave (for waveforms):
```
choco install gtkwave         # Windows
brew install gtkwave          # macOS
sudo apt install gtkwave      # Linux
```

---

## Quick Commands

### Quantized-Stream NPU

Full integration test (quantize FP32 → RTL → verify):
```powershell
cd "Quantized-Stream-NPU"; g++ -std=c++17 -O2 -o build/gen_test_vectors.exe sw/gen_test_vectors.cpp; .\build\gen_test_vectors.exe; iverilog -g2012 -o build/npu_integrated_tb rtl/pe.sv rtl/npu_core.sv tb/npu_integrated_tb.sv; vvp build/npu_integrated_tb
```

### RISC-V Pipeline

CPU test:
```powershell
cd "riscv32-harvard-pipeline"; iverilog -g2012 -s cpu_test -o sim_cpu Test\cpu_test.sv CPU\cpu.v CPU\D_memory\D_memory.v CPU\Instruction_Memory\instruction_mem.v CPU\Processor\RV32I_processor.v CPU\Processor\regfile.v CPU\Processor\controller.v CPU\Processor\mux.v CPU\Processor\imm_decode.v CPU\Processor\load_store_modifier.v CPU\Processor\Pipeline_Registers\if_id_reg.v CPU\Processor\Pipeline_Registers\id_exe_reg.v CPU\Processor\Pipeline_Registers\exe_mem_reg.v CPU\Processor\Pipeline_Registers\mem_wb_reg.v CPU\Processor\Pipeline_Registers\pc_reg.v CPU\Processor\ALU\ALU.v CPU\Processor\ALU\shifter.v CPU\Processor\AddORSub\add_sub.v CPU\Processor\AddORSub\CLA_32.v CPU\Processor\Comparator\comp_32.v; vvp sim_cpu; gtkwave cpu_test.vcd
```

### VGA Image Stream

Simulation:
```powershell
cd "VGA Image Stream with Ping-Pong FIFO buffers"; iverilog -g2012 -o stream_tb top_stream_tb.v top_stream.v video_stream_fifo.v vga.v; vvp stream_tb
```

Waveforms:
```powershell
cd "VGA Image Stream with Ping-Pong FIFO buffers"; powershell -ExecutionPolicy Bypass -File tools\waves\wave_top_stream_tb.ps1
```

---

## Block Diagrams

Each project includes HTML diagrams in its `diagrams/` or `Diagrams/` folder. Open in a browser to view architecture details.
