# MetroNyan

This project consists of designing a Telegram bot, which will guide the users
of said application to the restaurant they decide. The restaurants will be
chosen between all the possible ones located in Barcelona, based on the users requirements. The bot will also guide the users to the chosen restaurant through the shortest path, combining metro and walking displacements.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. 

### Prerequisites

In order to install the needed packages for this project, the ```pip3``` command (to install)
and the ```.zip``` (containing the files and codes) are needed.


### Installing

From the ```.zip``` the following needed files will appear:
- ```barcelona.grf```, the graph with Barcelona's streets
- ```restaurants.csv```,```restaestacions.csv```,```accessos.csv```, that are the data files that contain the information about thes restaurants, stations and accesses respectively.
- ```restaurants.py```, the module that reads the restaurant's data and searchs it.
- ```metro.py```, the module that builds the metro graph from the stations and accesses information.
- ```city.py```, the module that builds and consults the Barcelona's city graph.
- ```bot.py```, the module that through a telegram bot, it helps users choose a restaurant and leads them to it.
- ```requirements.txt```, with the needed installation libraries.
- ```README.md```, this file
- ```*.png```, with the attached images of the documentation.

in order to install the libraries contained in ```requirements.txt```, the following command is needed:
```python3
 $ pip3 install -r requirements.txt
 ```
 It is important to know that this command has to be **executed in the same directory** where the ```requirements.txt``` is saven, and it installs in the system the packages annoted in this file.
 
 **EXCEPTION**: the ```osmnx```library is not included inside this file, because it has different ways to install it, depending on your operating system (it sometimes causes problems). You can install it as follows:
 - ```$ pip3 install osmnx```, if no error is shown this is the easiest and typical way to install it.
 - if the above command did not work, you can try to install it with conda, with
 ```python3
 $ conda config --prepend channels conda-forge
 $ conda create -n ox --strict-channel-priority osmnx
```
- you may also try to install an extra library, with ```$ brew install spatialindex```for Mac users or ```$ apt install libspatialindex-dev``` for Ubuntu.
 It is also important to remark that some of the imported libraries in the codes **depend on the python version** that is used. This is the case of ```TypeAlias```. We have imported it from ```typing_extensions```, but this is only accepted with python versions 3.9 or older. With posterior verisions, the import should be from ```typing``` library.
 
## Restaurants.py:
The principal functions from this module are the following ones:
- ```def read()```, that reads the data from the ```restaurants.csv``` and saves the remarkable one in its respective Restaurant attributes. It returns the posterior created restaurants list.
- ```def find(query : str, restaurants : Restaurants)```, that searches the restaurants that contain the specified query from the whole list. It follows a multiple and fuzzysearch at once, because it allows the user to search more than one word at a time and all of them have to appear in the attributes, but it also allows to search similar texts in case that the searched parameter and the found one differ from one error.
- this module also uses the class ```Restaurant``` to treat every given restaurant.

### running the tests:
there are some tests that can be done in order to understand the full application of this module, and getting familiar with it:
Examples: you need to modify the ```main```function in order to execute the tests.
- to check if the ```read``` function runs correctly, you can try
```python3
def main():
    restaurants: Restaurants = read()  #contains all the bcn restaurants
    for restaurant in restaurants:
        print(restaurant.name)
        print(restaurant.addresses_district_name)
        print("--------")
```
like this you can compare with the ```.csv``` file and test if the information matches with the one obtained (the restaurant's name and district). Yo can access to any restaurant attribute if you want to.

- to check if the ```find``` function works properly, you can try
```python3
def main():
    restaurants: Restaurants = read()  #contains all the bcn restaurants
    found: Restaurants = find ("retaurant buger example", restaurants)  
    #contains the burger restaurants located in "l'Eixample", although 
    # the searched parameters are writted incorrectly.
    for restaurant in found:
        print(restaurant.name)  #it should return restaurants related with burgers
        print(restaurant.addresses_district_name)  # it should return "Eixample"
        print("--------")
```
You can execute this "find" command with any parameters of your interest, but you have to take into an account that some errors can be made due to the fact that the fuzzysearch also looks for near matches from the word, and sometimes this leads to restaurants that do not have the searched parameter but some similar and unrelated one. 


## Metro.py:
This module consists on the following main functions:
- ```def read_stations()```, that reads the stations from the ```estacions.csv``` and saves the important information in the station's attributes.
- ```def read_accesses()```, that reads the accesses from the ```accessos.csv``` and saves the important information in the accesses attributes.
- ```def get_point(str)```, that is an auxiliar function for the previous read ones, and gets the coordinates points in a tuple format from the attribute "geometry".
- ```def get_metro_graph()```, which creates the metro graph, using some auxiliar functions to create the nodes (stations and accesses) and to create the edges (links, accesses and sections of traintrack).
- ```def show(g: MetroGraph)```, that shows interactively the respective graph.
- ```def plot(g: MetroGraph, filename: str)```, that saves in the given file the metro graph with the city map background.
- This module also works with the classes ```Station```, ```Access``` and ```Edge```, in order to treat the stations, accesses and the needed edge's info attribute.

### running the tests:
The following tests may also help you to check the functionality of this module. You should modify the ```main``` function with the folowing possible applications:
- to check the ```read_stations```, do as follows:
```python3
def main():
    stations: Stations = read_stations()  # reads the stations
    for stat in stations:
        print(stat.NOM_ESTACIO)
        print(stat.GEOMETRY[0])  # prints the station 'x' coordinate
        print("--------")
 ```
 This will print the stations names, which you can compare with the ones given in the ```.csv``` file, and also prints the 'x' coordinate from the station, proving also the effectivity of the function ```get_point```, because of the separation between the coordinates of every station.

- in order to prove the ```read_accesses```, we will procede in the same way:
```python3
def main():
    accesses: Accesses = read_accesses()  # reads the accesses
    for acc in accesses:
        print(acc.NOM_ACCES)
        print(acc.GEOMETRY[1])  #prints the access 'y' coordinate
        print("--------")
 ```
That in this case prints the access name and its 'y' coordinate, proving that the ```get_point``` is also effective in the accesses case.

- To test the ```get_metro_graph()```, it is possible to make prints in the respective auxiliary functions in order to see if the nodes and edges are correctly added, but instead it is easier and more visual to execute directly the ```show```and ```plot```functions, because the graph is totally reflected there. So you could make:
```python3
def main():
    metro = get_metro_graph()  # builds the metro graph
    show(metro)  # shows interactively the graph
    plot(metro, 'plot_metro.png')  # saves the graph in the file 'plot_metro.png'
```
This will show the graph interactively in an independent window, as follows:
✅AÑADIR IMAGEN DEL SHOW INTERACTIVO DEL METRO
after you close that window, the execution will finish and the plot graph will be saven in the given file:
✅AÑADIR IMAGEN DEL PLOT DEL METRO

## City.py:
This module needs to import the previous one, ```metro.py```.The principal functions from this module are:
- ```def get_osmnx_graph()```, that creates Barcelona's street graph with the ```osmnx``` module, while at the same time uses the auxiliar functions ```load_osmnx_graph``` and ```save_osmnx_graph``` in order to load the once created graph and save the graph respectively.
- ```def build_city_graph(g1: OsmnxGraph, g2: MetroGraph) ```, which builds the city graph from the given metro and street graph. It uses some auxiliar functions such as ```aggregate_metro_graph```, ```aggregate_street_graph```and ```aggregate_union_edges```.
- ```def find_path(ox_g: OsmnxGraph, g: CityGraph, src: Coord, dst: Coord)```, that gives the shortest path from the source to the destiny, regarding the spent time.
- ```def path_time_dist(g: CityGraph, p: Path)```, that calculates the spent time and the traveled distance from a given path.
- ```def show(g: CityGraph)```, that as in the case of the ```metro.py```, shows interactively the city graph in an independent window.
- ```def plot(g: CityGraph, filename: str)```, which saves the city graph as an image in the given file.
- ```def plot_path (g: CityGraph, p: Path, filename: str)```, that saves in the file the found path between the source and the destiny.
- This module also works with the classes ```Edge```, in order to treat the needed edge's info attribute.

### running the tests:
The following tests may help you check the actions of this module. You can modify the ```main``` function with the following possible applications:
- to check the ```get_osmnx_graph```, do:
```python3
def main():
    streets = get_osmnx_graph()
```
This should create in your execution folder a file called ```street_graph.pickle``` (which proves that the ```save_osmnx_graph```function works correctly). The first time you prove this, it will take a long time to charge the graph, but the next ones it will be an inmediate operation, and this would prove that the ```load_osmnx_graph``` works correctly.

- to find if the ```build_city_graph``` is well implemented, we recommend you to prove it at the same time as the ```show``` and ```plot``` functions, and compare the result with the given images, in order to see wether the nodes and edges have been correctly added and connected. 
```python3
def main():
    streets = get_osmnx_graph()  # previously saven street graph
    city = build_city_graph(streets, metro)
    show(city)
    plot(city, 'city_plot.png')
```
Which should show the following:
✅AÑADIR IMAGENES DEL SHOW 
✅EL PLOT DEL CITY

- Finally, you could test the functions related to the path all at once, changing the coordinates as you wish. For example, the following ```main``` will check the path from the "Frankfurt Pedralbes" to the "Sagrada Familia":
```python3
def main():
    streets = get_osmnx_graph()  # previously saven street graph
    city = build_city_graph(streets, metro)
    
    frkt_coords: Coord = (2.1128, 41.38715)
    sgFam_coords: Coord = (2.174347, 41.403561)
    
    # shortest path from the frankfurt to the sagrada familia
    shortest_path: Path = find_path(streets, city, frkt_coords, sgFam_coords)
    # prints in the shell the spent time and travelled distance in the journey
    print(path_time_dist(city, shortest_path))
    # saves an image of the path route in the given file
    plot_path(city, shortest_path, 'Frkt_SgFam_path.png')
```
The plot path should let to something like this:
✅AÑADIR IMAGENES DEL PLOT PATH DE ESTA RUTA

## Bot.py:
The objective of this final module is to interact with the telegram users, helping to guide them to their chosen restaurant, based on the query/s. That's why this module combines the three others: first, it uses the ```restaurants.py``` to read the intial list of all the restaurants from barcelona, and then to find the restaurant based on every user query/s (with multiple and fuzzysearch). It also uses the module ```metro.py``` to get the metro graph from the city (based on the accesses and station data files). Lastly, it utilizes the ```city.py``` to get the city graph (obtained from the metro and street graphs) and to find the shortest path between two given coordinates (and also its plot).
The bot waits for the different users to connect, and it is important to remark that the petitions and conversations from the users **cannot be mixed!** or else it will result in a total chaos.
The module consists on the definition and implementation of different commands:
- ```/start```: it starts a conversation with the bot, that introduces its purposes. It also indicates the access to the ```/help``` command, so that the users take it into an account.
- ```/help```: it offers help regarding the available commands, for the user to find the bot options and capacities.
- ```/author```: shows the name of the authors of this project.
- ```/find <query> ```: searches which restaurants satisfy the query/s from the users, following a multiple and fuzzysearch. It then writes a numerated list for the first twelve ones maximum.
-  ```/info <number>```: shows the information about the specified restaurant by its index number, chosen from the previous list (the one obtained with ```/find```).
-  ```/guide <number>```: shows the map with the shortest path between the last sended location from the user to its specified restaurant by the index number (the index corresponds to the list obtained with ```/find```)


### running the tests:
the tests from this module need to be done with the Telegram bot directly, proving if the commands and its exceptions (definied to raise errors with their respective explanations) work correctly.
Here you can find an example video:
✅VIDEO DEL EJEMPLO

--------------------------------- 

[Image of the city graph](https://raw.githubusercontent.com/BlancaUG/MetroNyan/master/bcn.png)
![Screenshot](city.png)

https://raw.githubusercontent.com/BlancaUG/MetroNyan/master/bcn.png

## Authors

* **Xiao Segarra Banegas** 
* **Blanca Unanue Gambra**


## Acknowledgments

* Inspiration: we have been inspired by the introduction and explanation of the ```MetroNyan``` practice, done by Emma Rollon and Jordi Petit. We have also taken some ideas to treat the modules from it (for example the relation beetween the modules). 
