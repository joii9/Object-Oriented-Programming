# Object- Oriented Programming


```python
class Dog:
  sound = "Woof"

  def __init__(self, name, age):
    self.name = name
    self.age = age

  def bark(self):
    print(Dog.sound)
```


```python
Dog("Wero", 5).bark()
```

    Woof
    

In the above example, we are representing a real-world entity (a dog) as a class with properties (name and age) and methods (bark).


```python
class Employee:
  new_id= 1

  def __init__(self):
    self.id=Employee.new_id
    Employee.new_id += 1

  def say_id(self):
    print("My id is " +str(self.new_id))
  

e1= Employee()
e1.say_id()
e2= Employee()
e2.say_id()
```

    My id is 2
    My id is 3
    

## Inheritance


```python
class ParentClass:
  #class methods/properties...

class ChildClass(ParentClass):
  #class methods/properties...

```


```python
This form looks Inheritance
```


```python
class Animal: 
  def eat(self): 
    print("Nom Nom Nom...eating food!")


class Dog(Animal):
  def bark(self):
    print('Bark!')

class Cat(Animal):
  def meow(self):
    print('Meow!')

```


```python
fluffy = Dog()
zoomie = Cat()

fluffy.eat() # Nom Nom Nom...eating food!
zoomie.eat() # Nom Nom Nom...eating food!

```

    Nom Nom Nom...eating food!
    Nom Nom Nom...eating food!
    


```python
class Employee():
  new_id = 1
  def __init__(self):
    self.id = Employee.new_id
    Employee.new_id += 1

  def say_id(self):
    print("My id is {}.".format(self.id))
  
class Admin(Employee): #Inheritance
  pass

# Write your code below


e1 = Employee()
e1.say_id()
e2 = Employee()
e2.say_id()
e3= Admin()
e3.say_id()
```

    My id is 1.
    My id is 2.
    My id is 3.
    

## Overriding Methods

Sobrescribir un metodo


```python
class Animal:
  def __init__(self, name):
    self.name = name

  def make_noise(self):
    print("{} says, Grrrr".format(self.name))

pet1 = Animal("Rex")
pet1.make_noise() # Rex says, Grrrr
```

    Rex says, Grrrr
    


```python
class Cat(Animal): #Inheritance

  def make_noise(self):
    print("{} says, Meow!".format(self.name))

pet2 = Cat("Maisy") #Overriding method
pet2.make_noise() # Maisy says, Meow!

```

    Maisy says, Meow!
    

If you pay attention Cat has all the attributes and methods of Animal class. But if you call the make_noise() method of instance of cat. The behaviour changed to says Meow!

## Super()

When overriding methods we sometimes want to still access the behavior of the parent method. In order to do that we need a way to call the method of the parent class. Python gives us a way to do that using 
super()


```python
class Animal:
  def __init__(self, name, sound="Grrrr"):
    self.name = name
    self.sound = sound

  def make_noise(self):
    print("{} says, {}".format(self.name, self.sound))

class Cat(Animal):
  def __init__(self, name):
    super().__init__(name, "Meow!") #Here is the magic!

pet_cat = Cat("Rachel")
pet_cat.make_noise() # Rachel says, Meow!

```

    Rachel says, Meow!
    


```python
class Employee():
  new_id = 1
  def __init__(self):
    self.id = Employee.new_id
    Employee.new_id += 1

  def say_id(self):
    print("My id is {}.".format(self.id))

class Admin(Employee):
  def say_id(self):
    # Write your code below:
    super().say_id()
    print("I am an admin.")

e1 = Employee()
e2 = Employee()
e3 = Admin()
e3.say_id()


```

    My id is 3.
    I am an admin.
    

## Multiple Inheritance


```python
class Animal:
  def __init__(self, name):
    self.name = name
 
  def say_hi(self):
    print("{} says, Hi!".format(self.name))

class Cat(Animal):
  pass

class Angry_Cat(Cat):
  pass

my_pet = Angry_Cat("Mr. Cranky")
my_pet.say_hi() # Mr. Cranky says, Hi!

```

    Mr. Cranky says, Hi!
    


```python
class Employee():
  new_id = 1
  def __init__(self):
    self.id = Employee.new_id
    Employee.new_id += 1

  def say_id(self):
    print("My id is... {}.".format(self.id))

class Admin(Employee):
  def say_id(self):
    super().say_id()
    print("I am an admin.")

# Write your code below

class Manager(Admin):
  def say_id(self):
    super().say_id()
    print("My id is {}.".format(self.id))
    



e1 = Employee()
e2 = Employee()
e3 = Admin()
e4 = Manager()
e4.say_id()
```

    My id is... 4.
    I am an admin.
    My id is 4.
    

## Multiple Inheritance


```python
class Animal:
  def __init__(self, name):
    self.name = name

class Dog(Animal):
  def action(self):
    print("{} wags tail. Awwww".format(self.name))

class Wolf(Animal):
  def action(self):
    print("{} bites. OUCH!".format(self.name))

class Hybrid(Dog, Wolf):
  def action(self):
    super().action() #This super does not correspond to Wolf class but to Dog class because...
    Wolf.action(self) #This object and method correspond to Wolf class and it is necessary to give the argument self as a rule

my_pet = Hybrid("Fluffy")
my_pet.action() # Fluffy wags tail. Awwww
                # Fluffy bites. OUCH!

```

    Fluffy wags tail. Awwww
    Fluffy bites. OUCH!
    


```python
class Employee():
  new_id = 1
  def __init__(self):
    self.id = Employee.new_id
    Employee.new_id += 1

  def say_id(self):
    print("My id is {}.".format(self.id))

class User:
  def __init__(self, username, role="Customer"):
    self.username = username
    self.role = role

  def say_user_info(self):
    print("My username is {}".format(self.username))
    print("My role is {}".format(self.role))

# Write your code below
class Admin(Employee, User):
  def __init__(self):
    super().__init__()
    User.__init__(self, self.id, "Admin")
    

  def say_id(self):
    super().say_id()
    print("I am an admin.")

e1 = Employee()
e2 = Employee()
e3 = Admin()
e3.say_user_info()

```

    My username is 3
    My role is Admin
    

## Polymorphism


```python
class Animal:
  def __init__(self, name):
    self.name = name

  def make_noise(self):
    print("{} says, Grrrr".format(self.name))

class Cat(Animal):

  def make_noise(self):
    print("{} says, Meow!".format(self.name))

class Robot:
  
  def make_noise(self):
    print("beep.boop...BEEEEP!!!")

```


```python

an_animal = Animal("Bear")
my_pet = Cat("Maisy")
my_vacuum = Robot()
objects = [an_animal, my_pet, my_vacuum]
for o in objects:
  o.make_noise()

# OUTPUT
# "Bear says, Grrrr"
# "Maisy says, Meow!"
# "beep.boop...BEEEEP!!!"

```

    Bear says, Grrrr
    Maisy says, Meow!
    beep.boop...BEEEEP!!!
    

## Dunder Methods


```python
class Animal:
  def __init__(self, name):
    self.name = name

  def __repr__(self):
    return self.name

  def __add__(self, another_animal):
    return Animal(self.name + another_animal.name)

a1 = Animal("Horse")
a2 = Animal("Penguin")
a3 = a1 + a2
print(a1) # Prints "Horse"
print(a2) # Prints "Penguin"
print(a3) # Prints "HorsePenguin"

```

    Horse
    Penguin
    HorsePenguin
    


```python
The above code has the class Animal with a dunder method, .__add__(). This defines the + operator behavior when used on objects of this class type. 
```


```python
class Animal:
  def __init__(self, name):
    self.name = name

  def __repr__(self):
    return self.name
```


```python
a1 = Animal("Horse")
a2 = Animal("Penguin")
a3 = a1 + a2
print(a1) # Prints "Horse"
print(a2) # Prints "Penguin"
print(a3) # Prints "HorsePenguin"
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    Cell In[14], line 3
          1 a1 = Animal("Horse")
          2 a2 = Animal("Penguin")
    ----> 3 a3 = a1 + a2
          4 print(a1) # Prints "Horse"
          5 print(a2) # Prints "Penguin"
    

    TypeError: unsupported operand type(s) for +: 'Animal' and 'Animal'



```python
class Employee():
  new_id = 1
  def __init__(self):
    self.id = Employee.new_id
    Employee.new_id += 1

class Meeting:
  def __init__(self):
    self.attendees = []
  
  def __add__(self, employee):
    print("ID {} added.".format(employee.id))
    self.attendees.append(employee)

  # Write your code
  def __len__(self):
    return len(self.attendees)
  
    
e1 = Employee()
e2 = Employee()
e3 = Employee()
m1 = Meeting()

m1+e1
m1+e2
m1+e3

print(len(m1))
print(m1.__len__())

```

    ID 1 added.
    ID 2 added.
    ID 3 added.
    3
    3
    

## Abstraction


```python
from abc import ABC, abstractmethod #Abstract Base Class

class Animal(ABC): #Inherite ABC is the first step to making animal an abstract class. THIS class cannot be instantiated
  def __init__(self, name):
    self.name = name

  @abstractmethod #Import the decorator on the empty method. 
  def make_noise(self):
    pass

class Cat(Animal):
  def make_noise(self):
    print("{} says, Meow!".format(self.name))

class Dog(Animal):
  def make_noise(self):
    print("{} says, Woof!".format(self.name))

kitty = Cat("Maisy")
doggy = Dog("Amber")
kitty.make_noise() # "Maisy says, Meow!"
doggy.make_noise() # "Amber says, Woof!"

```

    Maisy says, Meow!
    Amber says, Woof!
    

The .make_noise() method exists since all animals make some form of noise, but the method is not implemented since each animal makes a different noise. Each subclass of Animal is now required to define their own .make_noise() method or an error will occur.
Other error that can occur is instantite 

an_animal = Animal("Scruffy")

# TypeError: Can't instantiate abstract class Animal with abstract method make_noise

## Getter, Setter, Deleter functions


```python
class Employee():
  new_id = 1
  def __init__(self, name=None):
    self.id = Employee.new_id
    Employee.new_id += 1
    self._name = name

  # Write your code below
  def get_name(self):
    return self._name
  
  def set_name(self, _name):
    self._name= _name
  
  def del_name(self):
    del self._name
  
    
  

e1 = Employee("Maisy")
e2 = Employee()



e1 = Employee("Maisy")
e2 = Employee()
print(e1.get_name())

e2.set_name("Fluffy")
print(e2.get_name())

#e2.del_name()
#print(e2.get_name())
```

    Maisy
    Fluffy
    


```python
class Box:
  def __init__(self, weight):
    self.__weight = weight #Variable with private encapsulation

  def getWeight(self):
    return self.__weight
 
  def setWeight(self, weight):
    if weight >= 0:
      self.__weight = weight
```


```python
box = Box(10)

print(dir(box))

box.setWeight(-5) # Creo que no se setea a -5 el peso por la restriccion de que el peso sea mayor o igual a 5 por eso toma la variable de dada en la clas
print(box.getWeight())

box.setWeight(5)
print(box.getWeight())
```

    ['_Box__weight', '__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getstate__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'delWeight', 'getWeight', 'setWeight', 'weight']
    10
    5
    

## Built-in property() function


```python
class Box:
  def __init__(self, weight):
    self.__weight = weight

  def getWeight(self):
    return self.__weight
 
  def setWeight(self, weight):
    if weight >= 0:
      self.__weight = weight

  def delWeight(self):
    del self.__weight

  weight = property(getWeight, setWeight, delWeight, "Docstring for the 'weight' property")
```


```python
box = Box(10)

print(box.weight) #this calls .getWeight()

box.weight = 5 #this called .setWeight()

del box.weight #this calls .delWeight()

box.weight = -5 #box.__weight is unchanged 

```

    10
    

## @property decorator


```python
class Box:
 def __init__(self, weight):
   self.__weight = weight

 @property
 def weight(self):
   """Docstring for the 'weight' property"""
   return self.__weight


 @weight.setter
 def weight(self, weight):
   if weight >= 0:
     self.__weight = weight

 @weight.deleter
 def weight(self):
   del self.__weight
```


```python
box = Box(10)

box.weight = 5

del box.weight

```


```python
Box.weight?
```


    [1;31mType:[0m        property
    [1;31mString form:[0m <property object at 0x000001AC3688FA10>
    [1;31mDocstring:[0m   Docstring for the 'weight' property



```python

```

## Review


```python
from abc import ABC, abstractmethod

class AbstractEmployee(ABC):
  new_id = 1
  def __init__(self):
    self.id = AbstractEmployee.new_id
    AbstractEmployee.new_id += 1

  @abstractmethod
  def say_id(self):
    pass

class User:
  def __init__(self):
    self._username = None

  @property
  def username(self):
    return self._username

  @username.setter
  def username(self, new_name):
    self._username = new_name

class Meeting:
  def __init__(self):
    self.attendees = []
  
  def __add__(self, employee):
    print("{} added.".format(employee.username))
    self.attendees.append(employee.username)

  def __len__(self):
    return len(self.attendees)

class Employee(AbstractEmployee, User):
    def __init__(self, username):
      super().__init__()
      User.__init__(self)
      self.username = username

    def say_id(self):
      print("My id is {}".format(self.id))
 
    def say_username(self):
      print("My username is {}".format(self.username))
```


```python
class School():
  def __init__(self, name, level, numberOfStudents):
    self.name= name
    self.level= level
    self.numberOfStudents= numberOfStudents

  def get_name(self):
    return self.name
  
  def get_level(self):
    return self.level
  
  def get_numberOfStudents(self):
    return self.numberOfStudents

  def set_numberOfStudents(self, numberOfStudents):
    self.numberOfStudents= numberOfStudents
  
  def __repr__(self):
    return "A {} school named {} with {} students.".format(self.level, self.name, self.numberOfStudents)
  

school_1=School("ESIME", "high", 10)
print(school_1)
print(school_1.get_name())
print(school_1.get_level())
print(school_1.get_numberOfStudents())
school_1.set_numberOfStudents(106)
print(school_1.get_numberOfStudents())
school_1.numberOfStudents=55
print(school_1.get_numberOfStudents())


class PrimarySchool(School):
  def __init__(self, name, numberOfStudents, pickupPolicy):
    super().__init__(name, "primary", numberOfStudents)
    self.pickupPolicy= pickupPolicy
  
  def set_pickupPolicy(self, pickupPolicy):
    self.pickupPolicy= pickupPolicy

  def get_pickupPolicy(self, pickupPolicy):
    return self.pickupPolicy
  
  def __repr__(self):
    parentRepr= super().__repr__()
    return parentRepr + " The pickup policy is {}".format(self.pickupPolicy)
  
P_School= PrimarySchool("Republica Dominicana", 100, "Pickup Allowed")
print(P_School)



class HighSchool(School):
  def __init__(self, name, numberOfStudents, sportsTeams):
    super().__init__(name, "high", numberOfStudents)
    self.sportsTeams= sportsTeams
  
  def get_sportsTeams(self, sportsTeams, i):
    self.sportsTeams= sportsTeams
    for self.i in self.sportsTeams:
      self.i
          
  def __repr__(self):
    parentRepr= super().__repr__()
    return parentRepr + "And the sports teams are: {}".format(self.sportsTeams)
    
  
h_school= HighSchool("Codecademy", 1, ["soccer", "box,", "tennis"] )

print(h_school)
#print(h_school.get_name())
#print(h_school.get_level())
#print(h_school.get_numberOfStudents())
#print(h_school.set_sportsTeams())

```

    A high school named ESIME with 10 students.
    ESIME
    high
    10
    106
    55
    A primary school named Republica Dominicana with 100 students. The pickup policy is Pickup Allowed
    A high school named Codecademy with 1 students.And the sports teams are: ['soccer', 'box,', 'tennis']
    


```python
sports=["soccer","box","tenis"]
print(str(sports)[1:-1])
```

    'soccer', 'box', 'tenis'
    


```python
string=""
for i in sports:
    string+= i+" "
print(string)
```

    soccer box tenis 
    


```python

```
