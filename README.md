# -MKEL1123-05-Advanced-Micropocessor-System_Milestone-5

## Overview
**Group 3**
<br>  Group Member: 
| **Name** | **Matrics Number** |
| :-----------: | :-----------: |
| Kukenraj a\l K.Pugalenthy | MKE211088 |
| Low Q' Ying | MKE211099 |
| See Wan Hui | MKE211093 |

<br>Online Application/Software used in this project:
  1. Edge Impulse to train the data model
     <br>(Sign up for free at [Edge Impulse](https://www.edgeimpulse.com/))
  2. STM32CubeIDE to deploy trained model into microcontroller board
     <br>(Download and install from [Integrated Development Environment for STM32](https://www.st.com/en/development-tools/stm32cubeide.html))
  3. PuTTY to display test result
     <br>(Download and install from [Download PuTTY: latest release (0.77)](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html))

<br>Step to build and train data model from Edge Impulse:
  1. The image dataset used is obtained and downloaded from Kaggle
     <br>(Link:[Fire Detection Dataset](https://www.kaggle.com/datasets/atulyakumar98/test-dataset?resource=download)(
  2. The dateset is then uploaded to Edge Impulse through the uploader. On "Dashboard", select "LET'S COLLECT SOME DATA".
  ![EI1](https://user-images.githubusercontent.com/105101813/178113464-8493a0d8-1ca8-40d4-be92-4d4a01ae0ceb.JPG)
  3. Choose "Upload data" and click "Go to the uploader".
  ![EI2](https://user-images.githubusercontent.com/105101813/178114867-a54bf1ec-3124-4984-a014-562d041a490b.JPG)
  4. On "Data acquisition" section, the "Choose Files" button is clicked and a total of 100 images are selected to upload into Edge Impulse. "Automatically split between training and testing" as a ratio of training data to testing data is selected under "Upload into category" section which can help in archieving high accuracy in the training phase later. Then, "Infer from filename" is chosen and clicked "Begin Upload".
  ![data_acquisition](https://user-images.githubusercontent.com/105101813/178133297-ee5b76aa-a8eb-4e43-ae73-5ad014f5fc6b.png)
  5. After all images are successfully uploaded, 
  ![Data Impulse](https://user-images.githubusercontent.com/105101813/178138922-e1dcb621-5feb-4910-a38e-72ec1ac5e7bd.png)

