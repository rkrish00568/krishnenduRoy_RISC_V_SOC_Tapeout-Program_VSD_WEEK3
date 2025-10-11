# Generate Timing Graphs Using OPENSTA

#### VSDBabySoC basic timing analysis
```
# -----------------------------
# OpenSTA Timing Analysis Script
# -----------------------------

# Load standard cell libraries
read_liberty -min /home/krish/vsd/week2/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_liberty -max /home/krish/vsd/week2/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib

# Load additional IP libraries
read_liberty -min /home/krish/vsd/week2/VSDBabySoC/src/lib/avsdpll.lib
read_liberty -max /home/krish/vsd/week2/VSDBabySoC/src/lib/avsdpll.lib
read_liberty -min /home/krish/vsd/week2/VSDBabySoC/src/lib/avsddac.lib
read_liberty -max /home/krish/vsd/week2/VSDBabySoC/src/lib/avsddac.lib

# Load the synthesized netlist
read_verilog /home/krish/vsd/week2/VSDBabySoC/output/post_synth_sim/vsdbabysoc.synth.v

# Link the design
link_design vsdbabysoc

# Read the timing constraints
read_sdc /home/krish/vsd/week2/VSDBabySoC/src/sdc/vsdbabysoc_synthesis.sdc

# Make sure output folder exists
exec mkdir -p /home/krish/vsd/week2/VSDBabySoC/STA_OUTPUT

# Generate timing report
report_checks -path_delay min_max -fields {nets cap slew input_pins fanout} -digits 4 > /home/krish/vsd/week2/VSDBabySoC/STA_OUTPUT/timing_report.txt

puts "✅ Timing analysis complete. Report saved to STA_OUTPUT/timing_report.txt"

```
![My BabySoC Timing Graph](images/3.png)
![My BabySoC Timing Graph](images/5.png)
![My BabySoC Timing Graph](images/4.png)


     
### **VSDBabySoC PVT Corner Analysis (Post-Synthesis Timing)**  
STA is performed across all PVT corners to validate that the design meets timing requirements.

The worst max path (Setup-critical) corners in sub-40nm nodes are generally:  
- **ss_LowTemp_LowVolt**  
- **ss_HighTemp_LowVolt** *(Slowest corners)*  

The worst min path (Hold-critical) corners are:  
- **ff_LowTemp_HighVolt**  
- **ff_HighTemp_HighVolt** *(Fastest corners)*  

The following TCL script can be executed to perform STA for the available PVT corners using the Sky130 timing libraries.  
The timing libraries can be downloaded from:  
[https://github.com/efabless/skywater-pdk-libs-sky130_fd_sc_hd/tree/master/timing](https://github.com/efabless/skywater-pdk-libs-sky130_fd_sc_hd/tree/master/timing)  

#### the TCL file is 
     set list_of_lib_files(1) "sky130_fd_sc_hd__tt_025C_1v80.lib"
     set list_of_lib_files(2) "sky130_fd_sc_hd__ff_100C_1v65.lib"
     set list_of_lib_files(3) "sky130_fd_sc_hd__ff_100C_1v95.lib"
     set list_of_lib_files(4) "sky130_fd_sc_hd__ff_n40C_1v56.lib"
     set list_of_lib_files(5) "sky130_fd_sc_hd__ff_n40C_1v65.lib"
     set list_of_lib_files(6) "sky130_fd_sc_hd__ff_n40C_1v76.lib"
     set list_of_lib_files(7) "sky130_fd_sc_hd__ss_100C_1v40.lib"
     set list_of_lib_files(8) "sky130_fd_sc_hd__ss_100C_1v60.lib"
     set list_of_lib_files(9) "sky130_fd_sc_hd__ss_n40C_1v28.lib"
     set list_of_lib_files(10) "sky130_fd_sc_hd__ss_n40C_1v35.lib"
     set list_of_lib_files(11) "sky130_fd_sc_hd__ss_n40C_1v40.lib"
     set list_of_lib_files(12) "sky130_fd_sc_hd__ss_n40C_1v44.lib"
     set list_of_lib_files(13) "sky130_fd_sc_hd__ss_n40C_1v76.lib"

     read_liberty /OpenSTA/examples/timing_libs/avsdpll.lib
     read_liberty /OpenSTA/examples/timing_libs/avsddac.lib

     for {set i 1} {$i <= [array size list_of_lib_files]} {incr i} {
     read_liberty /OpenSTA/examples/timing_libs/$list_of_lib_files($i)
     read_verilog /OpenSTA/examples/BabySOC/vsdbabysoc.synth.v
     link_design vsdbabysoc
     current_design
     read_sdc /OpenSTA/examples/BabySOC/vsdbabysoc_synthesis.sdc
     check_setup -verbose
     report_checks -path_delay min_max -fields {nets cap slew input_pins fanout} -digits {4} > 
     /OpenSTA/examples/BabySOC/STA_OUPUT/min_max_$list_of_lib_files($i).txt

     exec echo "$list_of_lib_files($i)" >> /OpenSTA/examples/BabySOC/STA_OUPUT/sta_worst_max_slack.txt
     report_worst_slack -max -digits {4} >> /OpenSTA/examples/BabySOC/STA_OUPUT/sta_worst_max_slack.txt

     exec echo "$list_of_lib_files($i)" >> /OpenSTA/examples/BabySOC/STA_OUPUT/sta_worst_min_slack.txt
     report_worst_slack -min -digits {4} >> /OpenSTA/examples/BabySOC/STA_OUPUT/sta_worst_min_slack.txt

     exec echo "$list_of_lib_files($i)" >> /OpenSTA/examples/BabySOC/STA_OUPUT/sta_tns.txt
     report_tns -digits {4} >> /OpenSTA/examples/BabySoO/STA_OUPUT/sta_tns.txt

     exec echo "$list_of_lib_files($i)" >> /OpenSTA/examples/BabySOC/STA_OUPUT/sta_wns.txt
     report_wns -digits {4} >> /OpenSTA/examples/BabySOC/STA_OUPUT/sta_wns.txt
     }
     



![Screenshot 2024-12-08 065913](https://github.com/user-attachments/assets/fc904026-5a3c-4bca-8e41-1624474f4852)

![Screenshot 2024-12-08 070712](https://github.com/user-attachments/assets/6daea128-878b-4286-96ab-08ea7bdd3b83)
