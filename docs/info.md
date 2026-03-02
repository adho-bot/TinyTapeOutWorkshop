## How it works

The **2×2 Bit-Serial Array Processor** is a compact and efficient processing engine designed for small-scale image processing tasks, demonstrating the capabilities of bit-serial computation in hardware. The processor consists of a **2×2 array of processing elements (PEs)**, each capable of performing arithmetic and logical operations in a bit-serial fashion.  

Each PE communicates with a local **bit-serial register file**, allowing sequential loading and shifting of data bits. The array architecture supports simultaneous computation across all PEs, enabling parallel execution of operations while using minimal silicon area.  

Key features include:  

- **Bit-serial ALU**: Performs addition, subtraction, and logical operations one bit at a time, reducing the complexity of combinational logic.  
- **Shift registers**: Enable serial input and output (SIPO/PISO) for efficient data streaming into and out of the array.  
- **Control interface**: Provides signals to enable, load, and shift data across the array and register files.  
- **Flexible memory mapping**: Each register file is memory-mapped, allowing the FPGA or host controller to address specific words in the array.  

The array can execute a wide range of small-scale computations, making it ideal for embedded image filters, simple matrix operations, or educational demonstrations of bit-serial arithmetic. By leveraging a **minimal I/O footprint** and small area, this design demonstrates the trade-off between computation speed and hardware efficiency in ASIC design.  

---

## How to test

Testing this design can be performed in both **simulation** and **FPGA prototype** environments.  

1. **Simulation (Cocotb)**  
   - The project includes a minimal testbench (`tb.v`) that instantiates the array processor.  
   - Use the provided Makefile to run Cocotb simulation:  
     ```bash
     make
     ```
   - The testbench performs a basic instantiation check and ensures the top module compiles correctly.  
   - For more advanced testing, you can drive the PISO and SIPO signals to load test vectors and observe the array outputs bit by bit.  

2. **FPGA Prototype (Optional)**  
   - Connect the **control signals** (`i_clk`, `i_rstn`, `i_piso_load`, `i_piso_shift`, `i_sipo_shift`, `i_PE_enable`) to switches or logic on the FPGA.  
   - Drive input data words via the bidirectional pins (`i_array_data`) and observe output words on (`o_array_data`).  
   - The PEs will process data serially, one bit per clock cycle, allowing you to verify functional correctness on real hardware.  

3. **Visualization**  
   - By feeding known input patterns into the array, you can trace the internal bit-serial computation using waveform viewers or logic analyzers.  
   - This allows inspection of intermediate results and verification of the bit-serial operations in each PE.  

4. **Notes for submission**  
   - The GitHub Actions workflow will automatically simulate your design using the minimal testbench to ensure it is synthesizable.  
   - No manual interaction is required to generate the GDS; once your repository is pushed with the updated `info.yaml`, Makefile, and source files, the workflow will compile, simulate, and produce your Tiny Tapeout chip layout.  

> This design serves as both a functional demonstration and a teaching tool for understanding bit-serial processing, array computation, and memory-mapped register operations in a small ASIC.
