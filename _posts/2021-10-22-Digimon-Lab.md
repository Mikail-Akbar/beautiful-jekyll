## Welcome to my Digimon Lab!

#### Below is my code:

```{python}

import csv

def avgSpeed(filePath): #function that inputs the Digimon dataset and outputs the average speed of all Digimon
    with open(filePath, "r") as f:
        data = csv.DictReader(f)
        d = {"average speed": []} 
        '''I created dictionary "d".
        The keys are called "average speed", 
        and the values are an empty list where I will put of the Digimon speeds.
        '''
        for row in data: #for every data entry in the dataset
            d["average speed"].append(float(row["Lv50 Spd"]))
            '''
            I add the FLOAT values of the Digimon to the empty list I created.
            This is because the speed values are strings in the dataset.
            '''
        for character in d: 
            #for the values of d in dictionary d (only runs once because the values are just one list)
            d[character] = sum(d[character])/len(d[character]) 
            #i set all of the values in the list equal to the average speed of all Digimons
    return d
print(avgSpeed("datasets/DigiDB_digimonlist.csv")) 



def countDigimon(filePath, category, value): 
    '''
a function that inputs the digimon dataset, 
one of the categories of the dataset, and the value of that category. 
It prints out how many Digimon's have that certain attribute
    '''
    with open(filePath, "r") as f:
        num = 0 #This is the counter I create
        data = csv.DictReader(f)
        for row in data: #for every data entry in the dataset
            if row[category] == value: #if the inputted category of that Digimon has the inputted value
                num += 1 #the counter adds one
    print(num) #we are printing the counter to show how many Digimons have the inputted category AND value
countDigimon("datasets/DigiDB_digimonlist.csv", "Stage", "Baby") 
#here I run my code with "Stage" and "Baby", which prints out 5.



def digiAttack(filePath): 
    '''
    A function that inputs the Digimon dataset,
    and puts 3 digimons with a memory of <= 5 and attack of >= 100 
    (total <= 15 memory, >= 300 attack) in a list and prints it
    '''
    d = [] #here I create the list where I will put the three Digimons
    with open(filePath, "r") as f:
        data = csv.DictReader(f)
        for row in data: #for every entry in the dataset
            if float(row["Memory"]) <= 5 and float(row["Lv50 Atk"]) >= 100:
                '''
                if the memory of a given Digimon is <= 5 AND the attack is >= 100... 
                (I had to convert from string to float to avoid errors)
                '''
                d.append(row["Digimon"]) #then I append that Digimon in my list
    print(d[:3]) #I print only the first three Digimons on that list because we only need a team of 3 Digimon
digiAttack("datasets/DigiDB_digimonlist.csv") 

```

### The three functions:



##### 1. What is the average speed of all Digimon?

In my first function, I created a dictionary in which I add the speeds of all digimon in a list under a key called "average speed". After collecting all of the Digimon's speeds, I found the average of all of the speeds by dividing the sum of all speeds by the "len" of my list, or the number of elements in my list. 

By running my function, I found that the average Digimon speed is 120.40160642570281.

##### 2. Write a function that can count the number of Digimon with a specific attribute.

For this question, I created a function that inputs two additional values: the "category" of the Digimon's value, and the "value" of that category. Then, I created a counter that kept track of the number of Digimons for my code. Then comes the most important part of my code: for every Digimon in the dataset that shares the same inputted value in the inputted category, I add one to my counter. 

When I call my code, I test how many Digimons' "Stage" is "Baby", which returns 5. 

##### 3. If your team only has 15 Memory, name a team of up to 3 Digimon that has at least 300 attack (Atk) in total.

In this function, I locate how many Digimons have a memory less than or equal to 5, and an attack greater than or equal to 100. After placing all of these Digimons in a list, I print the first three values of the list to give me a list of Digimons whose memory is less than or equal to 15 and whose memory's are greater than or equal to 300.

When I call my code, the team of Digimons I get are 'Koromon', 'Tsunomon', and 'Tsumemon'. 

### My Reflection:

I really enjoyed working on this lab. Even though this lab was similar to the practices done in previous classes, this lab offered new problems for me to solve, and an engaging dataset. 

I worked on this lab by myself. The process I used while working on the lab is as follows: I would first read what I am expected to code, and then I would go back to my other python files to serve as an inspiration for what to do. Then, I would draw a mental picture in my head of the pseudocode. For example, I ask myself: do I need a nested dictionary? Will a list suffice? Once I get that sorted in my head, I proceed to the body of my code. 

I would follow the same structure of code as my other practice methods. For example, I keep the general idea of opening a read-only CSV file, and I iterate through every entry in the dataset. 

For me, the most important aspect of this lab is being able to index into the values of the dataset/the dictionaries that I created. Understanding this general concept allowed me to complete this lab successfully.

I would say that the biggest source of errors in my code had to be when I forgot to convert from a string to a float in my code. Unfortunately, Python cannot multiply or divide a string that contains only integers, so I have to convert each string in my list to an actual number for me to manipulate the values in my dataset. Furthermore, being able to correctly code the one crucial line in the code that moves the code or computes the data has been challenging. For example, correctly coding the line that finds all Digimon with a memory less than or equal to 5 and an attack greater than or equal to 100 in my third function, and the line of code that finds the average speed of all Digimon in my first function, has been especially difficult. 

Thank you for reading my blog! And stay updated for more labs!

![mikail](/assets/img/IMG_0975.png)

>**Mikail Akbar**
>
>A crazy good coder and data analyst
