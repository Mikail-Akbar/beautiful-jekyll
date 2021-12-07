# Welcome to my Animal Crossing Lab!

#### Below is my code:

```py
import requests
import csv

class Sock:
    #Sock class constructor
    def __init__(self, name, color1, color2): 
        self.color1 = color1
        self.color2 = color2
        self.name = name
    
    #String method for sock class
    def __str__(self):
        return f"{self.name},{self.color1},{self.color2}"

BASE_URL = "https://hm-cs.herokuapp.com"
API_KEY = "ArtOfDataKEY123"

'''
Function that takes ONE string, and divides the commas
in that string into a list of the strings. 
Important for dividing the response.text we will generate
'''
def stringToList(string):
    newList = list(string.split(","))
    return newList

'''
function that creates a CSV file, 
appends each index from the API into the CSV,
and returns the CSV.
'''   
def createCSV(filePath):
    with open(filePath, "w") as f:
        ENDPOINT = "/socks"
        n = 0
        while True:
            payload = {'key': API_KEY, 'idx': n}
            response = requests.get(BASE_URL+ENDPOINT, params=payload)
            if response.ok:
                data = stringToList(response.text)
                a = data[0]
                b = data[5]
                c = data[6]
                d = Sock(a,b,c)
                f.write(str(d) + "\n")
                n += 1
            else:
                break

print(createCSV("datasets/animalsocks.csv"))

'''
Function that takes the animalsocks CSV we just created.
Returns a list of all of the socks that have have the most 
variations.

Where I found the encoding info (to remove /ufeff tag on one the keys of d):
https://stackoverflow.com/questions/17912307/u-ufeff-in-python-string
'''
def findNumVarations(filePath):
    with open(filePath, "r", encoding='utf-8-sig') as f:
        data = csv.DictReader(f)
        d = {}
        for row in data:
            if row["Name"] not in d.keys():
                d[row["Name"]] = 1
            else:
                d[row["Name"]] += 1
        max_value = max(d.values())
        max_list = []
        for keys in d:
            if d.get(keys) == max_value:
                max_list.append(keys)
    return max_list
print(findNumVarations("datasets/animalsocks.csv"))

'''
Function that takes the animalsocks CSV we created.
Returns a dictionary that has the different sock colors as its keys,
and the # of socks that have the color as its values. 
'''
def findColors(filePath):
    with open(filePath, "r") as f:
        data = csv.DictReader(f)
        d = {}
        for row in data:
            if row["Color 1"] not in d.keys():
                d[row["Color 1"]] = 1
            else:
                d[row["Color 1"]] += 1
            if row["Color 2"] not in d.keys():
                d[row["Color 2"]] = 1
            else:
                d[row["Color 2"]] += 1
            if row["Color 1"] == row["Color 2"]:
                d[row["Color 1"]] -= 1
        return d
print(findColors("datasets/animalsocks.csv"))
```

### The questions:

#### Discuss how you used the API to obtain the dataset.
In order to obtain the dataset, we first had to create a variable for the BASE_URL, the API_KEY, and the ENDPOINT. Then, we created our payload: although the key is just our API key, we also have an index. In order to obtain the dataset, we have to iterate through the index to get each row of the data. So, I made the idx equal to variable n. But before that, I set n equal to 0, and in my code I am iterating through n by adding 1 to n at the end of the while loop. Once the response is not ok anymore, I break the while loop to stop the while loop from infinitely iterating. 

Now, I am iterating through each row of the entire dataset. However, the response.text returns each row of the dataset as one string. So, I had to create another function that splits the string into a list that has the values between the commas as the values of the list. 

Now that I got all of that sorted out, I only want to save the name, color 1, and color 2. So, I set 3 different variables of the 3 different indices of the data. Then, I made a new variable d that stores each object of Sock(name, color 1, color 2). After that, I appended those values into my new dataset. Yay we got it!

#### Which sock has the most variations? If there is more than one answer, then list all of them.
'argyle crew socks', 'color-blocked socks', 'frilly knee-high socks', 'holey tights', 'kiddie socks', 'mixed-tweed socks', 'no-show socks', 'semi-opaque socks', 'semi-opaque tights', 'sequin leggings', 'simple-accent socks', 'striped socks', 'striped tights', 'tube socks', 'ultra no-show socks', 'vivid leggings', 'vivid socks', 'vivid tights'

#### How many socks of each color are there? If a sock has two different colors, it should be counted in both. However, if a sock has the same Color1 and Color2, make sure you don’t double count it!

'Pink': 41, 'Red': 39, 'Green': 50, 'Light blue': 33, 'Orange': 27, 'Purple': 37, 'Blue': 47, 'Yellow': 33, 'Beige': 15, 'White': 85, 'Black': 59, 'Brown': 11, 'Gray': 31, 'Colorful': 14

### My Reflection

This was an enjoyable lab. I had fun trying to solve the main issue in this lab, which was iterating through the index. 

I worked on this lab by myself. Although most of the methods were self explanatory, I struggled with trying to iterate through the index. But before that, I didn't know what an index even meant! So, it took a while for me to conceptually understand what an index was and how to manipulate the index. Once I figured that out, I understood pretty easily that I needed a while loop to iterate through each index. However, the main issue was knowing where to put the payload and response variables, since in our previous examples they were outside of the  loop. But after that, I was able to print my data nicely, and most of my lab was complete.

There were 2 other small issues that took me a while to get around before successfully running the code. First, the response.text we generate is only one string, so it took me a while to understand that I needed to break up this string in order to index through the rows. 

Second, I was taken by utter shock when the keys of the dictionary of my findNumVariations function had some nasty /ufeff encoding on it. It took some time for me to understand what that meant, and my best friend [Stack Overflow](https://stackoverflow.com/questions/17912307/u-ufeff-in-python-string) helped me know why it is there. So, I knew to include encoding='utf-8-sig' as one of my parameters while opening the CSV.

##### Thanks for reading my lab! And stay tuned for more updates!
#### Mikail Akbar
