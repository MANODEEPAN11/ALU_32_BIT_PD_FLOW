# Exp 5  Physical Design Flow of a 32-bit ALU using Cadence Tools

## Aim:

Execute floorplanning, power planning, and placement for the synthesised ALU block.

## Tool Required:

Physical Design: Innovus

## Mandatory Inputs for PD: 

1. Gate Level Netlist [Output of Synthesis] 

2. Block Level SDC [Output of Synthesis] 

3. Liberty Files (.lib)

4. LEF Files (Layer Exchange Format)

## Procedural Steps:

Ensure the Synthesis for the target design is complete, and then open a terminal from the corresponding workspace. 

• Initiate the Cadence tools and cmd:innovus (Press Enter) 

• For Innovus tool, a GUI opens, and the terminal also enters the Innovus command prompt, where the tool commands can be entered. 

After importing the Design, Perform the following Physical Design stages:

→ Floor Planning 

→ Power Planning

→ Placement

Note : Check the paths to properly read in the input files. 

•	Else, if you would like to import your design using GUI, open the Innovus tool and from the GUI, go to File → Import Design. 

o	A new pop-up window appears. 

o	First, load the netlist. You can browse for the file and select “Top cell : Auto Assign”.

•	Similarly, select your LEF files from the specified path.

•	Once LEF Files are loaded, Next step is to create the power supply pins both VDD and VSS

•	In order to load the Liberty File and SDC, create delay corners and analysis view, select the “Create Analysis Configuration” option at the bottom.

o	An MMMC browser Pops Up.

<img width="819" height="670" alt="image" src="https://github.com/user-attachments/assets/a40088b2-43dd-4250-b4ff-35ef4e00b9d2" />

The order of adding the MMMC Objects is as follows. 

1. Library Sets
   
2. RC Corners
   
3. Delay Corners
   
4. Constraints (SDC)
   
Once all of them are added, Analysis Views are created and assigned to Setup and Hold. 

In order to add any of the objects, make a right click on the corresponding label → Select New. 

Adding Liberty Files (slow.lib, fast.lib) under “Library Sets

• add slow.lib with a label Slow or any identifier of your own.

<img width="942" height="602" alt="Screenshot 2026-09-05 141027" src="https://github.com/user-attachments/assets/e908be45-f059-4473-b68c-0d66c7293a47" />

### Fig.1 Add slow Library set

• add fast.lib with a label Fast or any identifier of your own.

<img width="942" height="602" alt="Screenshot 2026-09-05 141030" src="https://github.com/user-attachments/assets/44d9695d-854c-412b-b53c-8989806cd865" />

### Fig.2 Add fast Library set

• Adding RC Corners can also be done in a similar process. The temperature value can be found under the corresponding liberty file. Also, cap table and RC Tech files can be added from Foundry where available.

<img width="582" height="475" alt="Screenshot 2026-09-05 142828" src="https://github.com/user-attachments/assets/86198473-42d0-441d-9d7f-458631deb4af" />

### Fig.3 Add RC corner

• Delay Corners are formed by combining Library Sets with RC Corners.

<img width="651" height="696" alt="Screenshot 2026-09-05 142839" src="https://github.com/user-attachments/assets/c99230b8-dbdd-4dc2-9209-5a2df5824b7b" />

<img width="651" height="696" alt="Screenshot 2026-09-05 142847" src="https://github.com/user-attachments/assets/58a6b947-ecd0-45f8-bac3-9d66d87b2437" />


### Fig.4 Add Delay corner Max_delay & Min_delay

• Similarly, SDC can be read under the MMMC Object of “Constraints”.


<img width="887" height="602" alt="Screenshot 2026-09-05 142908" src="https://github.com/user-attachments/assets/7e07e363-4f60-4e32-bd5f-42abd3b0c077" />

### Fig.5 SDC Constraint file

• Analysis Views are formed from combinations of SDC and Delay Corner.

<img width="362" height="187" alt="Screenshot 2026-09-05 142942" src="https://github.com/user-attachments/assets/1a2526e6-62dc-4c5e-871c-8611dab99f4f" />


   <img width="362" height="187" alt="Screenshot 2026-09-05 142947" src="https://github.com/user-attachments/assets/e3a05e08-a04e-41ce-8917-65fb31ffa597" />


### Fig.6 Add Analysis View Worstcase & Bestcase

• Once “Best” and “Worst” Analysis views are created, assign them to Setup and Hold.


### Fig.7 Add Setup Analysis View & Hold Analysis View

• Once all the process is done, Click on “Save&Close” and save the script generated with any name of your choice. 

• Make sure the file extension remains .view or .tcl 

• After saving the script, go back to Import Design window and Click “OK” to load your design.

<img width="829" height="504" alt="image" src="https://github.com/user-attachments/assets/2ea41359-4fb2-4251-aaca-1dfe54f40769" />

In the Import Design window click the save option to save the Default.globals file

• A rectangular or square box appears in your GUI if and only if all the inputs are read properly.

<img width="1920" height="1019" alt="image (10)" src="https://github.com/user-attachments/assets/b7129057-958b-427c-a4de-57bfe12edce0" />


### Fig.8 Core area
• The internal area of the box is called “Core Area”. 

• The horizontal lines running along the width of Core are “Standard Cell Rows”. Every alternate of them are marked indicating alternate VDD and VSS rows. 

• This setup is called “Flipped Standard Cell Rows”.

#### → Floorplan 

Steps under Floorplan :

1. Aspect Ratio [Ratio of Vertical Height to Horizontal Width of Core]
   
2. Core Utilisation [The total Core Area % to be used for Floor Planning]
   
3. Channel Spacing between Core Boundary to IO Boundary
   
• Select Floorplan → Specify Floorplan to modify/add concerned values to the above Factors. On adding/modifying the concerned values, the core area is also modified.

<img width="1920" height="1020" alt="image (11)" src="https://github.com/user-attachments/assets/cef71180-c835-4e3e-877e-51f63763e560" />


### Fig.9 Specify Floorplan 

• The Yellow patch on the Left Bottom are the group of “Unassigned pins” which are to be 
placed along the IO Boundary along with the Standard Cells [Gates].

#### → Power Planning

 Steps under Power Planning : 
 
1. Connect Global Net Connects
   
2. Adding Power Rings
   
3. Adding Power Strings
   
4. Special Route
   
Under Connect Global Net Connects, we create two pins, one for VDD and one for VSS connecting them to corresponding Global Nets as mentioned in Globals file / Power and Ground Nets.

 1. Select Power → Connect Global Nets.. to create “Pin” and “Connect to Global Net” as shown and use “Add to list”.
 
2. Click on “Apply” to direct the tool in enforcing the Pins and Net connects to Design and then Close the window.
   
• In order to tap in Power from a distant Power supply, Wider Nets and Parallel connections improve efficiency.

Moreover, the cells that would be placed inside the core area are expected to have shorter Nets for lower resistance. 

• Hence Power Rings [Around Core Boundary] and Power Stripes [Across Core Boundary] are added which satisfies the above conditions. 

• Select Power → Power Planning → Add Rings to add Power rings ‘around Core Boundary’.

• Select the Nets from Browse option OR Directly type in the Global Net Names separated by a space being Case and Spelling Sensitive. 

• Select the Highest Metals marked ‘H’ [Horizontal] for Top and Bottom and Metals marked ‘V’ [Vertical] for Right and Bottom. This is because Highest metals have Highest Widths and thus Lowest Resistance. 

• Click on Update after the selection and “Set Offset : Centre in Channel” in order to get the Minimum Width and Minimum Spacing of the corresponding Metals and then Click “OK”. 

• Similarly, Power Stripes are added using similar content to that of Power Rings.

• On adding Power Stripes, The Power mesh setup is complete as shown. However, There are no Vias that could connect Metal 9 or Metal 8 directly with Metal 1 [VDD or VSS of Standard Cells are generally made up of Metal 1]. 

• The connection between the Highest and Lowest Metals is done through Stacking of Vias done using “Special Route”. 

• To perform Special Route, Select Route → Special Route → Add Nets → OK. 

• After the Special Route is complete, all the Standard Cell Rows turn to the Color coded for Metal 1 

<img width="1920" height="1020" alt="image (12)" src="https://github.com/user-attachments/assets/972f9da8-4738-4e80-9668-44b91a60bca9" />

<img width="1920" height="1020" alt="image (13)" src="https://github.com/user-attachments/assets/8c25257c-0b0b-42b4-b20e-9aa1e74530bd" />


### Fig. 10 Power plan 

The complete Power Planning process makes sure Every Standard Cell receives enough power to operate smoothly.

#### → Placement 

1. The Placement stage deals with Placing of Standard Cells as well as Pins.
   
2. Select Place → Place Standard Cell → Run Full Placement → Mode → Enable ‘Place I/O Pins’ → OK → OK .
   
• All the Standard Cells and Pins are placed as per the communication between them, i.e., Two communicating Cells are placed as close as possible so that shorter Net lengths can be used for connections as Shorter Net Lengths enable Better Timing Results.
<img width="1920" height="1020" alt="image (15)" src="https://github.com/user-attachments/assets/e35b5915-bc76-4930-8285-2e850bf76424" />

<img width="1920" height="1020" alt="image (16)" src="https://github.com/user-attachments/assets/6fdead62-20b7-4d67-82b4-0e79fb004fe2" />

### Fig. 11 Placement of standard Cells 

• You can toggle the Layer Visibility from the list on the Right. The List of Layers available are shown on the right under “Layer” tab with colour coding.

## Result
Thus, the physical design stages up to placement for the Arithmetic Logi Unit were completed and verified.
