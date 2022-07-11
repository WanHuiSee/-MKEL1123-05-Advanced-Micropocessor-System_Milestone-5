# MKEL1123-05 Advanced Micropocessor System Milestone 5 - Fire Detection System

## Overview
**Group 3**
<br>  Group Member: 
| **Name** | **Matrics Number** |
| :-----------: | :-----------: |
| Low Q' Ying | MKE211099 |
| See Wan Hui | MKE211093 |
| Kukenraj a\l K.Pugalenthy | MKE211088 |

### 1.0 Overview of this project
In this project, a computer-vision based system will be implemented on a STM32 development board armed with Cortex embedded processor to detect fire and trigger fire alert alarm. The main idea of our project is to propose a system that is able to monitor surveillance data and reduce damages and life loss. The Edge Impulse is used to train the datasets for fire detection to be deployed into the STM32 MCU.

##### Figure below shows the connection of STM32F446RE with buzzer
![Connection](https://user-images.githubusercontent.com/105101813/178275164-7c0153df-62c8-4a14-9bc8-4bae68cd80d4.jpeg)

## 2.0 Equipments and Softwares
### 2.1 Equipments Required
- Microcontroller board with Cortex-M4 based processor, STM32F446 Nucleo-64 (STM32F446RET6 64 PINS)
- Personal computer 
- USB Type-A to Mini-B cable
- M-to-M wires
- M-to-F wires
- F-to-F wires
- Buzzer

### 2.2 Online Applications/Softwares used in this project:
 - Edge Impulse to train the data model
   <br>(Sign up for free at [Edge Impulse](https://www.edgeimpulse.com/))
 - STM32CubeIDE to deploy trained model into microcontroller board
   <br>(Download and install from [Integrated Development Environment for STM32](https://www.st.com/en/development-tools/stm32cubeide.html))
 - PuTTY to display test result
   <br>(Download and install from [Download PuTTY: latest release (0.77)](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html))

## 3.0 Overall Procedures 
### 3.1 Steps to build and train data model from Edge Impulse:
  1. The image dataset used is obtained and downloaded from Kaggle
     <br>(Link:[Fire Detection Dataset](https://www.kaggle.com/datasets/atulyakumar98/test-dataset?resource=download)(
  2. The dateset is then uploaded to Edge Impulse through the uploader. On "Dashboard", select "LET'S COLLECT SOME DATA".
  <br>![EI1](https://user-images.githubusercontent.com/105101813/178113464-8493a0d8-1ca8-40d4-be92-4d4a01ae0ceb.JPG)
  3. Choose "Upload data" and click "Go to the uploader".
  <br>![EI2](https://user-images.githubusercontent.com/105101813/178114867-a54bf1ec-3124-4984-a014-562d041a490b.JPG)
  4. In "Data acquisition" section, the "Choose Files" button is clicked and a total of 100 images are selected to upload into Edge Impulse. "Automatically split between training and testing" as a ratio of training data to testing data is selected under "Upload into category" section which can help in archieving high accuracy in the training phase later. Then, "Infer from filename" is chosen and clicked "Begin Upload".
  <br>![data_acquisition](https://user-images.githubusercontent.com/105101813/178133297-ee5b76aa-a8eb-4e43-ae73-5ad014f5fc6b.png)
  5. After all images are successfully uploaded, go to "Create Impulse" under "Impulse design", the impulse is created according to the image below and clicked on "Save Impulse". 
  <br>![Data Impulse](https://user-images.githubusercontent.com/105101813/178138922-e1dcb621-5feb-4910-a38e-72ec1ac5e7bd.png)
  6. Next, go to "Image" in "Impulse design" section, RGB is selected as Color Depth Parameter and clicked on "Save Parameter".
  <br>![Image](https://user-images.githubusercontent.com/105101813/178146341-815c9d71-a79c-4b56-bef9-b0f8cdd234fa.png)
  7. Once the parameter is saved, click "Generate features" button then both Raw and Processed features are generated and will be used in Model Training phase.
  <br>![Generate features](https://user-images.githubusercontent.com/105101813/178147535-a2a548ea-e996-4917-b81b-037477a7d266.png)
  8. In "NN Classifier" section, the values for  "Number of training cycles", "Learning rate", "Validation set size" to configure the Neural Network architecture are set as figure below and start training. Once the training process is done, the validation accuracy of the model in Model Training phase is shown and at the same time the best preforming model is saved and quantized into 8 bit fixed point model together with the inputs and outputs of that model.
  <br>![NN Classifier](https://user-images.githubusercontent.com/105101813/178152877-216dabe6-59cd-4a2f-9a51-943efe274546.png)
  9. Then, click the "Classify all" button in "Model testing" section and prediction on testing datasets is made by the best performing model and the testing accuracy is shown.
  <br>![Model Testing](https://user-images.githubusercontent.com/105101813/178153240-10998114-0af2-461d-9387-d890ef0dfc8f.png)
  10. Lastly, go to "Deployment" section and select "Cube.MX CMSIS-PACK" and make sure the EON Compiler is enabled before click the "Build" button. 
  <br>![image](https://user-images.githubusercontent.com/105101813/178153385-6d84e103-2356-4e45-b585-0d5b93dc228d.png)
  <br>![Enable EON™ Compiler](https://user-images.githubusercontent.com/105101813/178153362-5ad85af1-b30e-4c09-bed0-fb7e9c0e0e0a.png)
  Once the "Build" button has been clicked, the PACK file is downloaded and will be used in the STM32CubeIDE.
  <br>![image](https://user-images.githubusercontent.com/105101813/178279427-5c03286f-3014-4f67-a43a-bae88a97701e.png)


### 3.2 Steps to Deploy Model in STM32CubeIDE:
  1. First, open up the STM32CubeIDE and start a new STM32 project.
  2. Search for "NUCLEO-F446RE" under the "Board Selector" tab and click "Next".
  3. Enter the project name and select"C++" as the Targeted Language.
  4. Next, click 'Finish'. If there is a pop up, click 'Yes' to initialize all peripherals with their default Mode.
  5. Open .ioc file, go to 'Pinout & Configuration' > 'Computing' > 'CRC' and enable 'Activavated' checkbox.
  <br>![image](https://user-images.githubusercontent.com/105101813/178239741-b03c8a7c-0d79-4c73-a71c-f7632336cf23.png)
  7. Then, go to 'Help' > 'Manage Embedded Software Packages' > 'From Local...' and select the downloaded pack. 
  <br>![Embedded Software Packages](https://user-images.githubusercontent.com/105101813/178241928-bb589d66-6429-404a-a3b5-f24ac54306c9.png)
  Accept the license agreement and the pack will be installed. Now, the pack downloaded from Edge Impulse is added into the project.
  <br>![image](https://user-images.githubusercontent.com/105101813/178238108-306fb667-bb3c-473e-b08e-ac957bb69396.png)
  8. After the pack installation, switch back to .ioc file and go to Pinout & Configuration' > 'Software packs' > 'Select components'. Search for our project, expand the pack and checked on the checkbox under 'Selection'. Then, click "OK" to close the window.
  <br>![Software Packs Component Selector](https://user-images.githubusercontent.com/105101813/178234560-8d04441a-c4b5-4aa7-aeb5-e1fbf3fb015a.png)
  9. Back to 'Pinout & Configuration', under 'Additional software', click on the project name and click on the checkbox under 'Mode'.
  <br>![Additional software](https://user-images.githubusercontent.com/105101813/178234412-9eca997a-9012-4757-84f3-161e8f53ac9f.png)
  10. Click the "Project Explorer" on the left menu bar so the .ioc file loses focus. Press "CTRL"+"s" to save the workspace and click "Yes" for both questions "Do you want to regenerate the code?" and "This action can be associated with C/C++ perspective. Do you want to open this perspective now?". Make sure a "Middleware" folder is generated which stored all the impulses and required libraries.
  11. Rename the "main.c" file under Core/Src in "Project Explorer" to "main.cpp", as C++ language is preferred to be used.
  12. Then, the "main.cpp" script is edited as shown in the reference below.
   <br>(Link: [main.cpp](XXX))
  13. Click on the “Hammer” icon at the top to build the project and make sure there’s no error.
  <br>![image](https://user-images.githubusercontent.com/105101813/178243593-25326189-338e-4c2b-8aec-6d58747729d8.png)
  15. Click on the “Play” icon at the top to deploy the code on the board. Leave the settings as default and click “OK”. [** Make sure STM32F446RE board is connected to the laptop before click the "Play" icon.]
 
### 3.3 Steps to connect PuTTy as output of microcontroller:
  1. Open 'Device Manager' to check which USB COM is connected.
  <br> ![image](https://user-images.githubusercontent.com/105101813/178243771-ba974d19-c1f9-4756-9657-f15ea2f45cc0.png)
  2. Open PuTTY, change the connection type to 'Serial', enter the USB COM in 'serial line' column and set the speed to 115200. Then, click 'Open'.
  <br> ![image](https://user-images.githubusercontent.com/105101813/178243827-a54be592-dcd6-4f35-92d5-f72d44d8164b.png)
  3. Finally, the output can be seen from PuTTY serial console. The results can be compared with test result from Edge Impulse.
  <br>![image](https://user-images.githubusercontent.com/105101813/178241660-9914d25f-66aa-471b-850e-889fe193f440.png)
  <br>Figure below shows the board connection to get output from PuTTy and buzzer.
  <br>![Board Connection](https://user-images.githubusercontent.com/105101813/178276052-5e18f21b-e8a4-4cf5-a73f-d106ae5a3284.png)


## 4.0 Youtube Demo Video Link
- [Group 3: Product Demo](https://www.youtube.com/watch?v=Mi5RXnzab6Y&t=1s&ab_channel=ADVANCEDMICROPROCESSORSYSTEM)

## 5.0 References
### 5.1 Tutorial Video
  1. [How to Interface buzzer with STM32 || PWM || HAL || CubeMx](https://www.bing.com/videos/search?q=pwm+with+buzzer+stm32&qpvt=pwm+with+buzzer+stm32&view=detail&mid=9B67493FD1F2A456778A9B67493FD1F2A456778A&&FORM=VRDGAR&ru=%2Fvideos%2Fsearch%3Fq%3Dpwm%2Bwith%2Bbuzzer%2Bstm32%26qpvt%3Dpwm%2Bwith%2Bbuzzer%2Bstm32%26FORM%3DVDRE)
  
 ### 5.2 Website
  1. [Getting Started with STM32 - Introduction to STM32CubeIDE](https://www.digikey.my/en/maker/projects/getting-started-with-stm32-introduction-to-stm32cubeide/6a6c60a670c447abb90fd0fd78008697)



