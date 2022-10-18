# File Directory
```bash
├── main.py
├── Menu.py
├── Rule.py
├── utils.py
├── Opago
│   ├── dataset
│   │   ├── 00000.npz
│   │   ├── ***
│   │   └── 03983.npz
│   ├── model
│   │  └── model_27.pth
│   ├── pre_dataset
│   │   ├── Renju1
│   │   ├── Renju2
│   │   └── Renju3
│   ├── cnn_utils.py
│   ├── create_dataset.py
│   ├── dataloader.py
│   ├── SimpleNet.py
│   └── train.py
├── image
│   ├── board.jpg
│   ├── black.png
│   └── white.png
├── making_board.ipynb
``` 

# pre requisite
- **`python 3.9`**
- **`pytorch 1.12`**


# Project Description
- Making Opago(오목 모델, Gomoku AI model) AI with pygame module in python.   
- cnn method is used
- model structure is very simple and hyperparameter are already tuned 


## Dataset
- Dataset from https://gomocup.org/results/
- input are some image in the middle of the game
- output is the image that is the next step of the input image
- we can get dozens of data from just one game
- there is a tremendous data in website, which is organized by year
- this project uses 2021, 2020, 2019 game data

## Files Description
### pre_dataset
+ coordinate information which is from website which is described in upside
+ Renju is one of the name which means a way playing Gomoku with specific rules(actually most popular)
### create_dataset.py & dataset
+ change coordinate information to numpy 15 * 15 array and save it as npz files in dataset folder for making the input in the cnn network
### dataloader.py & cnn_utils.py & SimpleNet.py & train.py
- train Opago AI model in cnn method.
- input size is (batchsize, 1, 15, 15) output size is (batchsize, 255) 
- we can know which probabilty is the highest by using sigmoid function as activation function in last layer with 255 size array
- we can get a 8 times data with flipping(updown leftright) and rotational(90 180 270 360) method because the board is symmetric
### Menu.py
- checking  whether total game is over or not by counting whether win over than twice or same
- Also, showing message if the game is over
### Rule.py
- checking  whether the game is over or not with an algorithm that is checking that there is 5 stones in arrow
### utils.py
- there are various functions necessary for visualize the game from drawing the stone on a board to letting AI get a point to win a game
### main.py 
- If the whole game is over, then quit a game
### making_board.ipynb
- making a board image with a cv2 and PIL module

## Game Specification
1. use 15*15 board
2. randomly divide black and white side
3. the starter is always black
4. the starter which is black must put the stone on a middle of the board
5. if anyside win twice, the whole game is over.
6. blocking samsam which is the strategy that black cannot use is not implemented yet
7. the second black stone cannot be placed in 5x5 center area.    
Because Black should be penaltied at least once for reason that the first stone is always black

