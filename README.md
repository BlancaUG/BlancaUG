# MetroNyam

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
- ```README.md```
- ```*.png```, with the attached images of the documentation.

in order to install the libraries contained in ```requirements.txt```, the following command is needed:
```python3
 $ pip install -r requirements.txt
 ```
 It is important to know that this command has to be executed in the same directory where the ```requirements.txt``` is saven, and it installs in the system the packages annoted in this file.
 
 EXCEPTION: the ```osmnx```library is not included inside this file, because it has different ways to install it, depending on your operating system (it sometimes causes problems). You can install it as follows:
 - ```$ pip3 install osmnx```, if no error is shown this is the easiest and typical way to install it.
 - if the above command did not work, you can try to install it with conda, with
 ```python3
 $ conda config --prepend channels conda-forge
 $ conda create -n ox --strict-channel-priority osmnx
```
- you may also try to install an extra library, with ```$ brew install spatialindex```for Mac users or ```$ apt install libspatialindex-dev``` for Ubuntu.
 It is also important to remark that some of the imported libraries in the codes depend on the python version that is used. This is the case of ```TypeAlias```. We have imported it from ```typing_extensions```, but this is only accepted with python versions 3.9 or older. With posterior verisons, the import should be from ```typing```.
 
## Restaurants.py:
The principal functions from this module are the following ones:
- ```def read()```, that reads the data from the ```restaurants.csv``` and saves the remarkable one in its respective Restaurant attributes. It returns the posterior created restaurants list.
- ```def find(query : str, restaurants : Restaurants)```, that searches the restaurants that contain the specified query from the whole list. It follows a multiple and fuzzysearch at once, because it allows the user to search more than one word at a time and all of them have to appear in the attributes, but it also allows to search similar texts in case that the searched parameter and the found one differ from one error.

### running the tests:
there are some tests that can be done in order to understand the full application of this module, and getting familiar with it:
Examples: you need to modify the ```main```function in order to execute the tests
- to check if the ```read``` function runs correctly, you can try
```python3
def main():
    restaurants: Restaurants = read()  #contains all the bcn restaurants
    for restaurant in restaurants:
        print(restaurant.name)
        print(restaurant.addresses_district_name)
        print("--------")
```
like this you can compare with the ```.csv```file and test if the information matches with the one obtained. Yo can access to any restaurant attribute if you want.


## Metro.py:

 
 
## Running the tests

Explain how to run the automated tests for this system

### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Deployment

Add additional notes about how to deploy this on a live system

## Built With

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags).

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* etc



**ngrita**
*cursiva*
# titol gran
## apartats que demana
### el k crteis tu

perue et surtin funcions coma pytho
```python3
def main(): -> rest
```
```hola```
- punt

imatges -- issues --> añadir issue i arrastres al foto on posa write, set crea un link, el copies i enganxes en el readme
