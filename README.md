# 7-Segment Digit Display via HDMI

This project demonstrates how to take quadrature encoder input signals (A and B) on an FPGA and display a corresponding hexadecimal digit as a large, pixel-based 7-segment figure on an HDMI monitor. It integrates quadrature decoding, VGA timing generation, HDMI output, and pixel-based graphics rendering, all running on an FPGA.

## How It Works

1. **Quadrature Encoder Input:**
   - The encoder provides two signals, A and B.
   - The `QuadratureEncoder` module interprets these to maintain a count.
   - Rotating forward increments the count; rotating backward decrements it.

2. **Hexadecimal Digit Rendering:**
   - The lowest 4 bits of the count determine which hex digit (0–F) to display.
   - Combinational logic maps this hex digit to a 7-segment pattern (a–g).

3. **Pixel-Based 7-Segment Display:**
   - The `vga_sync` module generates standard VGA timing signals and pixel coordinates.
   - Using `x_pix` and `y_pix`, the design checks if the current pixel falls within a segment’s area.
   - Pixels in segment regions are lit (white), others stay black, forming a large, readable digit.

4. **HDMI Output:**
   - A clock wizard IP generates the 25 MHz pixel clock and a 125 MHz 5x clock.
   - The `hdmi_tx_0` IP converts the VGA-like RGB and sync signals into HDMI format.
   - Connect the FPGA HDMI output to a monitor to see the digit update in real-time as you rotate the encoder.

## Getting Started

### Prerequisites
- **Vivado (Xilinx)**: For synthesis, implementation, and bitstream generation.
- **FPGA Board with HDMI out**: Must support TMDS_33 signaling and have the pin assignments specified.
- **Quadrature Encoder**: Connect A/B signals to the pins defined in your constraints file.

### Steps
1. **Clone the Repository:**
   ```bash
   git clone https://github.com/yourusername/7SegmentHDMI.git
   cd 7SegmentHDMI
Open in Vivado:
Add the RTL sources and constraints. Insert the hdmi_tx_0 and clk_wiz_0 IP cores from the IP catalog.

Synthesize & Implement:
Run synthesis, fix any issues, then implement.
Generate the bitstream once implementation is successful.

Program the FPGA:
Load the generated .bit file onto the FPGA.
Attach the FPGA’s HDMI output to a monitor.

Interact: Rotate the quadrature encoder to change the displayed hex digit instantly on the HDMI screen.

Customization
Adjust segment coordinates or sizes in the top-level module to change the digit’s appearance.
Extend logic to display multiple digits or integrate other inputs.
Troubleshooting
If no image appears, verify HDMI IP configuration and pin assignments.
If the digit doesn't change correctly, ensure encoder signals are stable and correctly routed.
License
MIT License. See LICENSE for details.

Acknowledgments
Xilinx Vivado and IP cores for clock and HDMI support.
Reference designs and application notes on quadrature encoders and VGA/HDMI output guided the development.
Copy code





